## 简介

Scrapy是一个网络爬虫和信息抽取框架。

## 准备

### 安装pip

根据参考3的步骤首先安装distribute，然后安装pip



将C:\Python27\Scripts填入环境变量


linux根据[python的包管理pip安装](http://blog.catlovefish.com/?p=131)

    wget  http://python-distribute.org/distribute_setup.py
    python2.7 distribute_setup.py
    wget  https://github.com/pypa/pip/raw/master/contrib/get-pip.py --no-check-certificate
    python2.7 get-pip.py

### 安装Twisted

如果安装的是mingwin32
需要在Lib\distutils中创建distutils.cfg，其内容如下
    [build]
    compiler=mingw32

同时修改cygwinccompiler.py，将其中的编译选项'-mno-cygwin'去掉

最后在shell中输入
    
    pip install Twisted

如果没有bz2的话，需要进行安装

    yum install -y libbz2-dev

或者

    sudo apt-get install libbz2-devel

如果没有root权限，则安装libbz2后重新编译Python

    ./configure --prefix=/newpan/cd/Install && make && sudo make instlall 


### 安装w3lib

输入

    pip install w3lib

### 安装libxml2

是一个c程序安装包，而不是python安装包，因此需要下载安装[主页地址](http://www.xmlsoft.org/)



### 安装pyOpenSSL

输入

    pip install pyOpenSSL

### 安装openssl.exe

在[这里](http://xmlsoft.org/sources/win32/)下载所需要的安装包并将对应的文件添加到C:\MinGW-4.7.1\中

### 安装lxml

在[这里](https://pypi.python.org/simple/lxml/)下载lxml-3.1.2.win32-py2.7.exe，进行安装

## 安装

*安装libbz2*

*编译Python*

    ./configure --enable-shared --prefix=/newpan/cd/Install

添加LD_LIBRARY_PATH

    echo LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/newpan/cd/Install/lib\n export LD_LIBRARY_PATH >> ~/.bashrc



*安装pip*

参见前面

输入

    pip install Scrapy



## 教程

### 建立下载工程文件夹

使用命令

    scrapy startproject tutorial

会在当前文件夹内建立tutorial文件夹
其内的结构如下

```shell
tutorial/
    scrapy.cfg
    tutorial/
        __init__.py
        items.py
        pipelines.py
        settings.py
        spiders/
            __init__.py
            ...
```
其中
- scrapy.cfg 工程属性文件
- tutorial 工程名称和包名称
- tutorial/items.py 工程元文件
- tutorial/pipelines.py 工程pipeline文件
- tutorial/setting.py 工程设置文件
- tutorial/spiders/ 放置spider的文件夹

### 定义元文件



## 参考

1. [Scrapy使用——抓取赶集网北京公交信息](http://wwwdigger.com/?p=111)
2. [Scrapy 轻松定制网络爬虫](http://blog.pluskid.org/?p=366)
3. [How to install pip on windows?](http://stackoverflow.com/questions/4750806/how-to-install-pip-on-windows)
4. [software](http://www.lfd.uci.edu/~gohlke/pythonlibs/#distribute)
5. [Offical Page](http://scrapy.org/)
