# Yahoo Hadoop Tutorial Note

## Module 4

### MapReduce Basics

*FUNCTIONAL PROGRAMMING CONCEPTS*

对于可以划分的大数据输入，可以用MR模型进行处理，如果对于需要随时同步，或者难以进行并行划分的任务来说，不适合MR

MR中的所有数据都是不可被更新的

*LIST PROCESSING*

MR将输入的序列组处理后变为输出序列组，一个MR过程会有两次这个过程，一个是map一个是reduce

*MAPPING LISTS*

Mapper函数接受一个输入 数据，然后独立的将其转换为输出数据

![Figure 4.1: Mapping creates a new output list by applying a function to individual elements of an input list.](http://farm3.static.flickr.com/2151/3529146569_f80eb39a44_o.png)

*REDUCING LISTS*

reducing将输入的数据进行整合，将一组输入整合成为一个输出数据

![Figure 4.2: Reducing a list iterates over the input values to produce an aggregate value as output.](http://farm4.static.flickr.com/3213/3529959720_273aca53fe_o.png)

*PUTTING THEM TOGETHER IN MAPREDUCE*

一个MR有两个部分，一个是map，另一个是erduce

在MR的过程中所有的的输入输出都是key value的方式

所有相同key的value在一个reducer中输出

![Figure 4.3: Different colors represent different keys. All values with the same key are presented to a single reduce task](http://farm4.static.flickr.com/3602/3529959740_6756f2f531_o.png)

*EXAMPLE: WORD COUNT*

```java
public static class MapClass extends MapReduceBase
    implements Mapper<LongWritable, Text, Text, IntWritable> {

    private final static IntWritable one = new IntWritable(1);
    private Text word = new Text();

    public void map(LongWritable key, Text value,
                    OutputCollector<Text, IntWritable> output,
                    Reporter reporter) throws IOException {
      String line = value.toString();
      StringTokenizer itr = new StringTokenizer(line);
      while (itr.hasMoreTokens()) {
        word.set(itr.nextToken());
        output.collect(word, one);
      }
    }
  }

  /**
   * A reducer class that just emits the sum of the input values.
   */
  public static class Reduce extends MapReduceBase
    implements Reducer<Text, IntWritable, Text, IntWritable> {

    public void reduce(Text key, Iterator<IntWritable> values,
                       OutputCollector<Text, IntWritable> output,
                       Reporter reporter) throws IOException {
      int sum = 0;
      while (values.hasNext()) {
        sum += values.next().get();
      }
      output.collect(key, new IntWritable(sum));
    }
  }
```
*THE DRIVER METHOD*

```java
  public void run(String inputPath, String outputPath) throws Exception {
    JobConf conf = new JobConf(WordCount.class);
    conf.setJobName("wordcount");

    // the keys are words (strings)
    conf.setOutputKeyClass(Text.class);
    // the values are counts (ints)
    conf.setOutputValueClass(IntWritable.class);

    conf.setMapperClass(MapClass.class);
    conf.setReducerClass(Reduce.class);

    FileInputFormat.addInputPath(conf, new Path(inputPath));
    FileOutputFormat.setOutputPath(conf, new Path(outputPath));

    JobClient.runJob(conf);
  }
```
JobClient.runJob(conf)会向MR提交一个工作，它会阻塞到那里直到工作完成。如果工作失败，会扔出一个IOException，
JobClient 还提供一个非阻塞的版本, 函数为submitJob()。

*MapReduce Data Flow*

![Figure 4.4: High-level MapReduce pipeline](http://farm4.static.flickr.com/3126/3529146657_5b5d025a5f_o.png)

>对于hadoop pipes来说，其c++接口的 bool runTask(const Factory& factory)运行job，如果成功返回true，否则打印error信息并返回false

对于不同的map和reduce来说，彼此并不知道对方的存在和信息。map到reduce的信息交换式MR中的唯一一个信息交换过程。

*A CLOSER LOOK*
![Figure 4.5: Detailed Hadoop MapReduce data flow](http://farm3.static.flickr.com/2275/3529146683_c8247ff6db_o.png)


## Module 5: Advanced MapReduce Features

### Custom Data Types

*WRITABLE TYPES*

有默认的IntWritable, LongWritable, FloatWritable, BooleanWritable, Text，还可以自己实现接口

*CUSTOM KEY TYPES*

由于reduce收到的key是有序的，所以对于自定义类型的key，需要实现一个相对严格的接口WritableComparable

注意hashCode()需要实现

*USING CUSTOM TYPES*

一旦定义了自己的需要的类型，可以用setOutputKeyClass和setOutputValueClass使用自定义的实现。

*FASTER COMPARISON OPERATIONS*

快速比较操作，对于key的默认操作来说，首先通过readFields读取数据，然后调用compareTo比较大小。可以在不读取所有的数据的情况下进行比较操作，比如字符串，一旦读取到不同的字符，就可以做出比较的结果。自己可以定义类似快速操作接口WritableComparator 

### Input Formats

可以自定义InputFormat对数据输入格式进行定制。对于输入的灵活性很有帮助，另外，很重要的一点是定义InputFormat可以帮助输入文件的分块

*CUSTOM FILE FORMATS*

一般来说不直接实现InputFormat而是继承FileInputFormat是更好的方法。

### Output Formats

### Partitioning Data

Partitioning是决定由哪个reducer来处理map发送的key和value的处理过程。如果key的分布不是平均的，那么用默认的hashCode处理的Partitioning过程就会造成部分reducer负担过重

### Reporting Custom Metrics

自定义的计数器可以反映map和reduce的运行状态

### Distributing Auxiliary Job Data

有时候需要所有的map读取整个的文件，文件不大只是M级别的。我们可以用distributed cache将文件分布在所有的node上，

### Distributing Debug Scripts

在分布式的大部分机器上有若干日志，有时候我们只需要部分。可以根据自定义的脚本将日志上传到指定的路径中去。

