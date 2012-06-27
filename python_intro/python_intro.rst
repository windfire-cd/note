.. include:: <s5defs.txt>

====================
Python 语言介绍
====================

:Authors: 陈东
:Date: $Date: 2012-06-26  (Tue, 26 June 2006) $


.. 这篇文章兼ppt是用restructedText完成的

.. contents::
   :class: handout

.. footer:: cd 2012-06-26 ver-1.0
    
历史及版本
============

.. container:: handout

    是一种面向对象、直译式计算机程序设计语言，由Guido van Rossum于1989年底发明，\
    第一个公开发行版发行于1991年。Python语法简捷而清晰，具有丰富和强大的类库。\
    它常被昵称为胶水语言，它能够很轻松的把用其他语言制作的各种模块（尤其是C/C++）轻松地联结在一起

* 由Guido van Rossum于1989年底发明,第一个公开发行版发行于1991年

* 分为2.x 和 3.x 版本

特点
=========

.. class:: small

* 简单易学
  
  .. container:: handout

        Python是一种代表简单主义思想的语言，语法简单

* 免费开源

  .. class:: handout

        Python是FLOSS（自由/开放源码软件）之一。使用者可以自由地发布这个软件的拷贝、阅读它的源代码\
        、对它做改动、把它的一部分用于新的自由软件中

* 高层语言，可移植性强

  .. class:: handout

        用Python语言编写程序的时候无需考虑诸如如何管理你的程序使用的内存一类的底层细节\
        Python已经被移植在许多平台上（经过改动使它能够工作在不同平台上）。这些平台包括Linux、Windows、\
        FreeBSD、Macintosh、Solaris、OS/2、Amiga、AROS、AS/400、BeOS、OS/390、z/OS、Palm OS、QNX、VMS、Psion、\
        Acom RISC OS、VxWorks、\
        PlayStation、Sharp Zaurus、Windows CE、PocketPC、Symbian以及Google基于linux开发的android平台

* 面向对象

  .. class:: handout

        Python即支持面向过程的编程也支持面向对象的编程。在 面向过程 的语言中，程序是由过程或仅仅是可重用\
        代码的函数构建起来的。在 面向对象 的语言中，程序是由数据和功能组合而成的对象构建起来的。与其他主要\
        的语言如C++和Java相比，Python以一种非常强大又简单的方式实现面向对象编程 

* 解释性

* 嵌入性强

    .. class:: handout
        
        你可以把Python嵌入你的C/C++程序，从而向你的程序用户提供脚本功能，反之亦可。

* 丰富标准库和第三方库

    .. class:: handout
        
        Python标准库确实很庞大。它可以帮助你处理各种工作，包括正则表达式、文档生成、单元测试、线程、数据库、网页浏览器、\
        CGI、FTP、电子邮件、XML、XML-RPC、HTML、WAV文件、密码系统、GUI（图形用户界面）、Tk和其他与系统有关的操作 


Hello World
==============

* IDLE

  .. code:: python

        >>>print 'Hello World'

* 脚本

  .. code:: python

            #hello_world.py
            print 'Hello World'

  .. code:: bash

        $python hello_world.py

基础类型
=============

.. class:: tiny


* 数

    - 整数： 2
    - 长整数： 20000
    - 浮点： 3.25， 52.3E-4
    - 复数： (-5+4j)

* 字符串
  
    - 单引号(')  
    - 双引号(")
    - 三引号(''' 或者 """)
    - 转义: '\\'
    - 自然字符串： r
    - Unicode: u

* 变量


控制流: if
============

.. code:: python
    
    if guss == True:
        print 'guss is true'
    elif guss is None:
        print 'guss is None'
    else:
        print 'gus is else'


控制流：while & for
========================

.. class:: tiny

* while

    .. code:: python
  
          while True:
              print 'True now'

* for
   
    .. code:: python
  
          for i in range(0,5):
              print 'i is %d' % i
          else:
              print 'i is out of range'


控制流: break & continue
===========================

.. class:: tiny

  * break
  
      .. code:: python
    
            while True:
                s = raw_input('please input a char: ')
                if s == 'q':
                    break;
  
  * continue
  
      .. code:: python
    
            while True:
                s = raw_input('please input a char: ')
                if s == 'q'
                    break;
                else:
                    continue
    


函数
=========

.. class:: tiny

* 定义函数

  .. code:: python

        def fun(a):
            print 'a is %d' % a

* 使用函数

  .. code:: python

        >>>fun(5)
        >>>a is 5

* global: 函数内部引用外部定义的变量，需要在声明变量为全局的

  .. code:: python

        x = 4
        def fun(a):
            global x
            return 'a add x is %d' % (a + x)





.. container:: handout
    
    DocString




模块
=========

.. container:: handout

    * .pyc文件
        输入一个模块相对来说是一个比较费时的事情，所以Python做了一些技巧，以便使输入模块更加快一些。\
        一种方法是创建 字节编译的文件 ，这些文件以.pyc作为扩展名。字节编译的文件与Python变换程序的中间状态有关\
        （是否还记得Python如何工作的介绍？）。当你在下次从别的程序输入这个模块的时候，.pyc文件是十分有用的——它会快得多\
        ，因为一部分输入模块所需的处理已经完成了。另外，这些字节编译的文件也是与平台无关的
    
    * __name__


.. class:: tiny

* 引用模块:
  
    .. code:: python

        import sys
        from sys import argv


* 定义模块：

    .. code:: python
         
        #Filename: mymodule.py
        def Hi():
            print 'Hi"

        version = 0.1


        #Filename: mymodule_demo.py
        import mymodule
        mymodule.Hi()
        print mymodule.version

数据结构: list
================

.. class:: small

list是处理一组有序项目的数据结构，即你可以在一个列表中存储一个 序列 的项目

.. class:: small

  * list.append(x)
  * list.extend(L)
  * list.insert(i, x)
  * list.remove(x)
  * list.pop([i])
  * list.index(x)
  * list.count(x)
  * list.sort()
  * list.reverse()


list: code
==============

.. class:: tiny

    * 代码

        .. code:: python

            >>> a = [66.25, 333, 333, 1, 1234.5]
            >>> print a.count(333), a.count(66.25), a.count('x')
            2 1 0
            >>> a.insert(2, -1)
            >>> a.append(333)
            >>> a
            [66.25, 333, -1, 333, 1, 1234.5, 333]
            >>> a.index(333)
            1
            >>> a.remove(333)
            >>> a
            [66.25, -1, 333, 1, 1234.5, 333]
            >>> a.reverse()
            >>> a
            [333, 1234.5, 1, 333, -1, 66.25]
            >>> a.sort()
            >>> a
            [-1, 1, 66.25, 333, 333, 1234.5]

        


数据结构：tuple
===================

.. class:: tiny

    * 元组和列表十分类似，只不过元组和字符串一样是 不可变的 即你不能修改元组

       .. code:: python
       
             >>> t = 12345, 54321, 'hello!'
             >>> t[0]
             12345
             >>> t
             (12345, 54321, 'hello!')
             >>> # Tuples may be nested:
             ... u = t, (1, 2, 3, 4, 5)
             >>> u
             ((12345, 54321, 'hello!'), (1, 2, 3, 4, 5))
             >>> # Tuples are immutable:
             ... t[0] = 88888
             Traceback (most recent call last):
               File "<stdin>", line 1, in <module>
               TypeError: 'tuple' object does not support item assignment
               >>> # but they can contain mutable objects:
               ... v = ([1, 2, 3], [3, 2, 1])
               >>> v
               ([1, 2, 3], [3, 2, 1])

数据结构：sets
===============

.. class:: tiny

    * 集合是一组无序且没有重复的元素所组成的
        .. code:: python
       
             >>> basket = ['apple', \
             'orange', 'apple', 'pear', 'orange', 'banana']
             >>> fruit = set(basket)    # create a set without duplicates
             set(['orange', 'pear', 'apple', 'banana'])
             >>> 'orange' in fruit     # fast membership testing
             True
             >>> 'crabgrass' in fruit
             False
             >>> a = set('abracadabra')
             >>> b = set('alacazam')
             set(['a', 'r', 'b', 'c', 'd'])
             >>> a - b                 # letters in a but not in b
             set(['r', 'd', 'b'])
             >>> a | b                 # letters in either a or b
             set(['a', 'c', 'r', 'd', 'b', 'm', 'z', 'l'])
             >>> a & b                 # letters in both a and b
             set(['a', 'c'])
             >>> a ^ b                 # letters in a or b but not both
             set(['r', 'd', 'b', 'm', 'z', 'l'])

数据结构：dict
=================

.. class:: tiny

* 字典可以认为是一种key:value的数组，其中key是唯一的
    
  .. code:: python

        >>> tel = {'jack': 4098, 'sape': 4139}
        >>> tel['guido'] = 4127
        >>> tel
        {'sape': 4139, 'guido': 4127, 'jack': 4098}
        >>> tel['jack']
        4098
        >>> del tel['sape']
        >>> tel['irv'] = 4127
        >>> tel
        {'guido': 4127, 'irv': 4127, 'jack': 4098}
        >>> tel.keys()
        ['guido', 'irv', 'jack']
        >>> 'guido' in tel
        True



Python中的引用及参数传递
============================

.. container:: handout
    
    在python中，类型属于对象，变量是没有类型的，这正是python的语言特性

* Python中类型是属于对象的，而不是属于变量的
* strings, tuples, 和numbers是不可改变的，而list, sets, dict是可改变的

因此传递strings, tuples, 和numbers等效于c语言中的传值，而传递list, sets, dict相当于传递引用

类
==========

* 类使用class关键字创建。类的域和方法被列在一个缩进块中
* 类的方法与普通的函数只有一个特别的区别——它们必须有一个额外的第一个参数名称: self\
  相当于c++中的this指针
* 支持继承
* 初始化函数__init__


类：code
===========

.. class:: tiny

* 代码

  .. code:: python

        class FileInfo(UserDict):
            "store file metadata"
            def __init__(self, filename=None):
                UserDict.__init__(self)        1
                self["name"] = filename 
            def PrintName(self):
                print self["name"]


类：多继承
================


* 继承自object的类为新式类，否则为经典类
* 经典类中，使用深度优先，从左至右的进行遍历查询方法
* 新式类中，使用广度优先，首先查找兄弟，从左至右遍历查询方法
* 一般最好少采用多继承


.. container:: handout
    
    .. code:: python

        class P1: #(object): # parent class 1 
            def foo(self): 
                print 'called P1-foo()' 
       
        class P2: #(object): # parent class 2 
            def foo(self): 
                print 'called P2-foo()' 
            def bar(self): 
                print 'called P2-bar()' 
       
        class C1(P1, P2): # child 1 derived from P1, P2 
            pass 
       
        class C2(P1, P2): # child 2 derived from P1, P2 
            def bar(self): 
                print 'called C2-bar()' 
       
        class GC(C1, C2): # define grandchild class 
            pass # derived from C1 and C2


    首先采用经典类，调用foo()时首先查找GC，没有则向上查找左面第一个父亲C1，也没找到\
    继续向上查找P1，找到后调用输出。对于bar()来说在P2找到后根本不会调用C2.bar()

    .. code:: python

         >>> gc = GC() 
         >>> gc.foo() # GC ==> C1 ==> P1 
         called P1-foo() 
         >>> gc.bar() # GC ==> C1 ==> P1 ==> P2 
         called P2-bar()

    然后将#(object)的注释去掉，查看新式类的调用顺序，调用foo()，首先查找GC，然后查找C1，C2\
    在P1中找到，查找bar()，首先查找GC，C1，然后在C2中找到，那么不再查找P2.bar()

    .. code:: python

        >>> gc = GC() 
        >>> gc.foo() # GC ==> C1 ==> C2 ==> P1 
        called P1-foo() 
        >>> gc.bar() # GC ==> C1 ==> C2 
        called C2-bar()

    新式类有个属性__mro__可以告诉你调用顺序

    .. code:: python

        >>> GC.__mro__
        (<class '__main__.GC'>, <class '__main__.C1'>, <class
        '__main__.C2'>, <class '__main__.P1'>, <class
        '__main__.P2'>, <type 'object'>)



文件操作
====================

.. class:: tiny

* 打开关闭
    
    .. code:: python
            
        file_object = open('thefile.txt')
        file_object.close()

* 读文件

    .. code:: python
            
        rfile = open('data', 'r')
        all_data = rfile.read()
        chunk_data = rfile.read(100)
        lines_data = rfile.readlines()
        rfile.close()

* 写文件

    .. code:: python

        wfile = open('data','w')
        wfile.write(all_data)
        wfile.writelines(lines_data)


异常处理
===========

.. class:: small

* Python 具有异常处理，通过使用 try...except 块来实现
* 使用不存在的字典关键字将引发 KeyError 异常
* 搜索列表中不存在的值将引发 ValueError 异常
* 调用不存在的方法将引发 AttributeError 异常
* 引用不存在的变量将引发 NameError 异常
* 未强制转换就混用数据类型将引发 TypeError 异常
* 用raise语句来引发一个异常。异常/错误对象必须有一个名字，且它们应是Error或Exception类的子类
* 使用try...finally语句以释放资源

异常处理:code(1)
=================

.. class:: tiny

* try...except
    .. code:: python

        try:
            s = raw_input('Enter something --> ')
        except EOFError:#处理EOFError类型的异常
            print '/nWhy did you do an EOF on me?'
            sys.exit() # 退出程序
        except:#处理其它的异常
            print '/nSome error/exception occurred.'

* raise exception
    .. code:: python

            class ShortInputException(Exception):
            '''你定义的异常类。'''
                def __init__(self, length, atleast):
                    Exception.__init__(self)
                    self.length = length
                    self.atleast = atleast



异常处理:code(2)
==================

.. class:: tiny

* raise exception
    .. code:: python

            try:
                s = raw_input('请输入 --> ')
                if len(s) < 3:
                    raise ShortInputException(len(s), 3)
            # raise引发一个你定义的异常
            except EOFError:
                print '/n你输入了一个结束标记EOF'
            except ShortInputException, x:#x这个变量被绑定到了错误的实例
                print 'ShortInputException: 输入的长度是 %d
            else:
                print '没有异常发生.'

异常处理:code(3)
==================

.. class:: tiny

* try... finally
    .. code:: python

        try:
            f = file('poem.txt')
            lines = f.readlines()
            for i in range(0,100):
                print lines[i]
        finally:
            f.close()
            print 'Cleaning up...closed the file'

标准库简介
==========
        
.. class:: tiny

* Python 标准库(Standard Library)包含了大量非常有用的模块(module)，并是Python的标准安装版的一部分

* 包含sys, time, shutil, os...大量覆盖不同需求的模块
    .. code:: python
  
          import sys
          def readfile(filename):
          f = file(filename)
          while True:
              line = f.readline()
              if len(line) == 0:
                  break
              print line, # notice comma
          f.close()
          if len(sys.argv) < 2:
              print 'No action specified.'
              sys.exit()
          if sys.argv[1].startswith('--'):
              option = sys.argv[1][2:]
              if option == 'version':
                  print 'Version 1.2'
              elif option == 'help':


PS1.2中Python的使用
=============================

.. class:: tiny

PS1.2中对于Python的使用主要有保障模块以及一些系统脚本，具体使用模块举例如下

.. class:: tiny

标准库使用

    .. class:: tiny

    * os模块，主要用于跨平台以及一些系统操作
    * ConfigParser模块，用于解析及修改配置文件
    * logging模块，用于记录日志
    * xml.dom
    * subprocess
    * re

.. class:: tiny

第三方库使用
    
    .. class:: tiny

    * Twisted
    * psutil



os模块
===========

.. class:: tiny

os 系统服务应用程序接口（API)，常用方法如下：
    * os.getcwd()函数得到当前工作目录
    * os.getenv()和os.putenv()函数分别用来读取和设置环境变量
    * os.listdir()返回指定目录下的所有文件和目录名
    * os.remove()函数用来删除一个文件。
    * os.path.isfile()和os.path.isdir()函数分别检验给出的路径是一个文件还是目录。
    * os.chdir(dirname):改变工作目录到dirname
    * os.path.exists(name):判断是否存在文件或目录name
    * os.path.join(path,name):连接目录与文件名或目录
    * os.system()函数用来运行shell命令
    * os.linesep字符串给出当前平台使用的行终止符
    * os.path.split()函数返回一个路径的目录名和文件名。
    * os.path.getsize(name):获得文件大小
    * os.path.abspath(name):获得绝对路径


os:code
==========

.. class:: tiny

* 代码：
  
    .. code:: python

        #filename: process_operation.py

            cur_dir = os.getcwd()
            if os.path.isdir(open_dir):
                os.chdir(open_dir)
                if open_args is not None:
                    cmd_str = open_name \
                                + " " + open_args
                else:
                    if os.path.isfile('run.sh'):
                        cmd_str = './run.sh'
                    else:
                        cmd_str = './' + open_name



ConfigParser模块
==================

.. class:: tiny

* ConfigParser模块主要用于解析ini格式的配置文件

  .. code:: python

        #filename: config_parse.python

        cf = ConfigParser.ConfigParser()
        success_parse_file = cf.read(cofig_name)
        if len(success_parse_file) == 0:
            raise NameError("No file avilable")
        self._local_ip = cf.get("LocalMachine","localip")
        self._data_dir = cf.get("LocalMachine","datadir")
        self._server_ip = cf.get("LocalMachine","serverip")
        self._moniter_time_interval = cf.getint("LocalMachine", \
                                    "monitertimeinterval")
        self._screen_width = cf.getint("LocalMachine", "screenwidth")

logging模块
===============


.. class:: tiny

* logging模块提供日志功能

  .. code:: python

        #file_name: config_parse.python
        ps_home = os.environ["PS_HOME"]
        log_path = ps_home + '/' + self._log_dir
        if not os.path.exists(log_path):
            os.makedirs(log_path)
        logfile = log_path + '/' + 'ps_daemon.log'
        logging.basicConfig(level=self._log_level,
        format='%(asctime)s %(filename)s[line:%(lineno)d] \
                            %(levelname)s %(message)s',
        datefmt='%a, %d %b %Y %H:%M:%S',
        filename=logfile,
        filemode='w')
        console = logging.StreamHandler()
        console.setLevel(logging.INFO)
        formatter = logging.Formatter('%(name)-12s: \
                        %(levelname)-8s %(message)s')
        console.setFormatter(formatter)

subprocess模块
================

.. class:: small

从python2.4版本开始，可以用subprocess 这个模块来产生子进程，并连接到子进程的标准输入 /输出/错误中去，\
还可以得到子进程的返回值

.. class:: small

subprocess 意在替代其他几个老的模块或者函数，比如：

    .. class:: small

        * os.system
        * os.spawn
        * os.popen
        * popen2
        * commands
 

subprocess:code
===================

.. class:: tiny

* 代码：
   .. code:: python

        #file_name: process_operation.py

        #windows platform
        if system_identify.g_sys_type is 0:
            p = subprocess.Popen(cmd_str,creationflags = \
                     subprocess.CREATE_NEW_CONSOLE)
        else:
            p = subprocess.Popen(cmd_str)


xml.dom模块
==============

.. class:: tiny

* 作为一个简单处理xml格式的模块，代码如下
    .. code:: python

        #file_name: ps12_daemon.py

        impl = minidom.getDOMImplementation()  
        newdoc = impl.createDocument(None, "Config", None)  
        rootNode = newdoc.documentElement
        #manager ip
        manageripNode = newdoc.createElement("MangerIP")  
        manageripNode.appendChild(newdoc.createTextNode(self.cf.get_sender_manager_ip()))  
        rootNode.appendChild(manageripNode)
        result_file = open(sender_xml_file, 'wb+')  
        writer = codecs.lookup('utf-8')[3](result_file)  
        newdoc.writexml(writer, encoding='utf-8')  
        writer.close()

re模块
============

.. class:: tiny

* re使得Python具有了正则表达式的功能
    .. code:: python

        #filename: pss_install.py
        def ShmParse(file,phymem):
            f = open(file,'r+')
            f_lines = f.readlines()
            for line in f_lines:
                line.strip()
            small_mem = phymem/4096
            max_mem = 2 * 1024 * 1024 * 1024
            max_pattern = re.compile(r'kernel.shmmax\s*=\s*\d*')
            min_pattern = re.compile(r'kernel.shmall\s*=\s*\d*')
            w_lines = []
            i = 0
            while i < len(f_lines):
                if f_lines[i][0] != '#':
                    if max_pattern.match(f_lines[i]):
                        print 'max match'
                    elif min_pattern.match(f_lines[i]):
                        print 'min match'
                    else:
                        w_lines.append(f_lines[i])
                else:
                    w_lines.append(f_lines[i])
            i = i + 1
            w_lines.append(('kernel.shmmax=%d\n' % max_mem))
            w_lines.append(('kernel.shmall=%d\n' % small_mem))
            f.seek(0)
            f.truncate()
            f.writelines(w_lines)
            f.close()

psutil库
===========

.. class:: tiny

* psutil作为一个提供当前系统运行状态的模块，比如cpu,内存等
    .. code:: python

        #filename: process_operation.py
            def close_process_by_name(self,name):
                if self._name_ids.has_key(name):
                    try:
                        id_list = self._name_ids[name]
                        for item in id_list:
                            if psutil.pid_exists(item):
                                locate_process = psutil.Process(item)
                                locate_process.kill()
                    except:
                        pass
                else:
                    logging.info('not found process by name %s ' % name)
        

Twisted库
============


* Twisted是一个事件驱动的异步网络开发框架
* Twisted技术体系包含2个层次：协议和工厂。协议负责连接成功以后对交互的处理，而工厂则是负责连接过程
* 和libevent(c), Boost.Asio(c++), Mina(Java)类似
* Twisted的实现是Reactor模式

.. container:: handout
    
    一个真正reactor模式的实现是需要实现循环独立抽象出来并具有如下的功能：

    1.监视一系列与你I/O操作相关的文件描述符（description)

    2.不停地向你汇报那些准备好I/O操作的文件描述符


    一个设计优秀的reactor模式实现需要做到：

    1.处理所有不同系统会出现的I/O事件

    2.提供优雅的抽象来帮助你在使用reactor时少花些心思去考虑它的存在

    3.提供你可以在抽象层外（treactor实现）使用的公共协议实现。


Twisted:code
===============

.. class:: tiny

* 代码：
    .. code:: python

        #filename: server.py
        class DaemonProtocol(Protocol):
            def __init__(self,factory):
                self.factory = factory
                self.stat_str={0:'is not running',1:'is running'}
            def dataReceived(self, data):
                #.... 
            class DaemonFactory(Factory):
                def __init__(self):
                self.stat_ = 1
                daemon.Start()
            def buildProtocol(self, addr):
                return DaemonProtocol(self)
        if __name__ == "__main__":
            #...
            reactor.listenTCP(int(port), DaemonFactory())
            reactor.run()
            #...

Python的不足以及发展
=======================

.. class:: small

Python的不足

.. class:: small

    * 和静态语言(c, java)相比速度较慢,只用Python的情况下和c相比大约是5-10倍的差异
    * GIL对多线程模式的阻碍
    * 强制缩进有时候会造成格式混乱和莫名的错误
    * 3.x版本不兼容2.x版本，部分第三方框架依然基于2.x版本
    * 调试效率低下

.. class:: small

Python的发展

.. class:: small

    * CPython
        .. container:: handout
                
            是一个Python语言的C实现，主要解决Python的效率问题，类似的还有JPython（Java), IronPython(.Net)

    * PyPy
        .. container:: handout

            PyPy 表示 “用 Python 实现的 Python”，但实际上它是使用一个称为 RPython 的 Python 子集实现的。\
            更准确地来说，PyPy 自身就是一种运行时，您可以在其中插入任何语言。 PyPy 整洁的语言设计使之非常适\
            合嵌入低级优化器，提供诸多优化优势。具体来说，PyPy 集成了一种即时 (JIT) 编译器。这与能够以革命性\
            的方式改变 Java 性能的知名技术 HotSpot 属于同一种技术的不同形式

            PyPY 的最新版本是 1.8，它充分实现了 Python 2.7.2，也就是说能够兼容这个版本的 CPython 的语言特性和行为\
            。然而，在许多基准使用当中，它的速度已经远远超过了 CPython 2.7.2。
    * stackless
        .. container:: handout

            Stackless Python是Python的一个增强版本。Stackless Python修改了Python的代码，提供了对微线程的支持。\
            微线程是轻量级的线程，与前边所讲的线程相比，微线程在多个线程间切换所需的时间更多，占用资源也更少 

            Stackless Python 是一种不在 C 堆栈上保存状态的 Python 实现。它的确有堆栈 -- 要多少有多少 -- 但这些是 Python 堆栈\
            受益最大的那些特定应用程序可能是 Swarm 仿真，或有许多角色扮演极小任务的多人游戏。一例就是正在使用 Stackless Python\
            开发的 EVE 游戏

    * Eventlet
        .. container:: handout

            开源的高度伸缩性的Python网络编程库

            - 非阻塞I/O模型
            - 协程(Coroutines)使得开发者可以采用阻塞式的开发风格,却能够实现非阻塞I/O的效果
            - 隐式事件调度,使得可以在Python解释器或者应用程序的某一部分去使用Eventlet

            .. code:: python

                 import eventlet
                 pool = eventlet.GreenPool()
                 while True:    
                    pool.spawn(func,args )

            其中
                - GreenPool 用来实现协程,保证并行
                - Spawn     用来调用相应的函数,完成具体业务



 .. container:: handout

       参考

       * `Python几种并发实现方案的性能比较`__

         __ http://www.elias.cn/Python/PyConcurrency?from=Develop.PyConcurrency

       * `协程才是未来-性能夸张的协程服务器`__

         __ http://y.jmeye.com/index.php?aid=273

