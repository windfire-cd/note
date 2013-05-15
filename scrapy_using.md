## 简介

## 准备

### 安装pip

根据参考3的步骤首先安装distribute，然后安装pip

将C:\Python27\Scripts填入环境变量

### 安装Twisted

如果安装的是mingwin32
需要在Lib\distutils中创建distutils.cfg，其内容如下
    [build]
    compiler=mingw32

同时修改cygwinccompiler.py，将其中的编译选项'-mno-cygwin'去掉

最后在shell中输入
    
    pip install Twisted

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

输入

    pip install Scrapy

## 使用

## 参考

1. [Scrapy使用——抓取赶集网北京公交信息](http://wwwdigger.com/?p=111)
2. [Scrapy 轻松定制网络爬虫](http://blog.pluskid.org/?p=366)
3. [How to install pip on windows?](http://stackoverflow.com/questions/4750806/how-to-install-pip-on-windows)
4. [software](http://www.lfd.uci.edu/~gohlke/pythonlibs/#distribute)
