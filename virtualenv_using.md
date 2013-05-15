# 无root多版本Python管理

## 问题

公司服务器python版本为2.4，好多依赖的库无法安装和使用，所以需要安装新的库，但是不能完全升级python，否则会造成其他依赖使用故障，比如yum

而且我又没有服务器的root权限，就解决该问题做以下几个步骤

## 安装python2.7.4

下载Python2.7.4.tar.bz2，解压后进入目录运行

```python
./configure --prefix=/newpan/cd/Install
make
make install
```

## 安装virtualEnv

下载源码后解压，进入目录后运行

```python
python2.7 setup.py install --prefix=/newpan/cd/Install
```



## VirtualEnv使用

创建环境

```shell
virtualenv env
```

激活环境

```shell
env/bin/activate
```
然后所有的pip以及easy_install安装的包都在当前目录下了，不会造成系统的污染。

## 其他安装

### 安装setuptools

在[setuptools](https://pypi.python.org/pypi/setuptools#files)下载源码后编译安装，注意要用python2.7

```python
python2.7 setup.py install --prefix=/newpan/cd/Install
```

### 安装virtualenvwrapper

```shell
easy_install 安装virtualenvwrapper --prefix=/newpan/cd/Install
```


## 参考

1. [多版本Python环境：virtualenv](http://www.leric.info/?p=231)
2. [在无root权限的情况下安装python模块 ](http://blog.chinaunix.net/uid-8487640-id-3171972.html)
3. [Python 的虛擬環境及多版本開發利器─Virtualenv 與 Pythonbrew](http://www.openfoundry.org/tw/tech-column/8516-pythons-virtual-environment-and-multi-version-programming-tools-virtualenv-and-pythonbrew)