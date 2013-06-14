# Using Puppet to manager Ubuntu

## 模式

确定使用Standalone模式进行开发和使用

## 安装

    sudo apt-get install puppet

## 配置

手动修改启动脚本配置

    $ sudo puppet resource service puppet ensure=running enable=true

主要配置文件是/etc/puppet/puppet.conf

其中对于所有的node来说，\[agen\]或者\[main\]包含下面的配置

- server: puppet master的hostname
- report: 大部分用户需要设置true
- pluginsync: 大部分用户需要设置true
- certname： 此节点的唯一标示

## 学习使用

### 基本概念

系统的配置由一系列的分子(molecules)组成，这里命名为资源(resource)

资源可以是一个系统账户，特定的文件，软件包，运行的服务，或者一个定时的任务。

类似的资源可以被分为一组

Puppet利用RAL(resource abstract layer)将资源分为

- types 高层次的资源定义
- providers 特定的系统实现

puppet利用RAL查询资源当前状态，目标状态，然后再利用RAL进行必要的更改

#### 资源概述

每个资源都是一个资源类的实例， 都有一个标题作为识别，有一系列属性和属性值，通过"=>"进行赋值

    user { 'dave':
      ensure     => present,
      uid        => '507',
      gid        => 'admin',
      shell      => '/bin/zsh',
      home       => '/home/dave',
      managehome => true,
    }

#### resource shell

resource shell 是一个puppet工具，可以用来查询和修改resource的属性。典型应用如下

    $ puppet resource user

user是resource type，后面还可以接resource name

    $ puppet resource user root

可以利用其修改属性

    $ puppet resource user dave ensure=present shell="/bin/zsh" home="/home/dave" managehome=true

#### 核心资源类型

puppet有若干内置类型

- notify
- file
- package
- service
- exec
- cron
- user
- group

可以在[这里](http://docs.puppetlabs.com/references/stable/type.html)找到其定义

可以通过-s获得帮助信息，如下面获取user信息

    puppet describe -s user

### 编写manifests

puppet可以在c/s架构下运行，但是也可以通过apply在单机下运行，如

    $ puppet apply my_test_manifest.pp


## 参考