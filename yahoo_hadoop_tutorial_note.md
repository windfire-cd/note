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


