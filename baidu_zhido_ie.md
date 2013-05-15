## 问题

*百度知道数据抽取需求分析任务：分析百度知道详细页问题和答案的抽取*

详细页面抽取：

问题（可以不抽取，利用入口的问题），问题提问者，提问采纳者答案，采纳者（回答者），级别，采纳率；
其他回答者1，答案1，其他回答者2，答案2，...，其他回答者9，答案9
(至多抽取10个问题和答案)



## 草案

三种方式


1. python抽取html结构并解析
2. nginx模块，然后进行处理，需要考虑后续模块的可叠加性以及其他模块的编写便利
3. 利用GATE来使用其IE的功能，进行抽取。



## 时间估计

python编写模块并解析-4hours
熟悉GATE以及相关IE背景-5hours
解析背景以及完成相关准备-4hours
使用GATE进行抽取实践-4hours
编写nginx模块-8hours

### python mode

可以考虑用比较成熟的库，比如[BeautifulSoup](http://www.crummy.com/software/BeautifulSoup/),[urllib2](http://docs.python.org/2/library/urllib2.html)

豆瓣上有一个讨论的[主题](http://www.douban.com/group/topic/16925000/)
里面建议不用BeautifulSoup，存在内存泄露

其中关于PyQuory有以下介绍以及教程[Python学习笔记—PyQuery库的使用总结](http://www.newliu.com/post/18/)，[官方文档](http://pythonhosted.org/pyquery/),[教程](http://geoinformatics.cn/lab/pyquery/)

### 需求分析

简单的大纲

#### 任务

完成百度知道抓取，分析，保存的工作（索引？）

问题（可以不抽取，利用入口的问题），问题提问者，提问采纳者答案，采纳者（回答者），级别，采纳率；
其他回答者1，答案1，其他回答者2，答案2，...，其他回答者9，答案9
(至多抽取10个问题和答案)

#### 环境以及指标

原型可以使用python快速实践。后期需要对方案进行整体优化。
原型需要满足下面的要求

输入：百度知道的url
输出：对应每个url保存进数据库（mangodb文档数据库）

*性能*

原型仅仅满足可用性，后期优化对性能有所要求

*稳定性*

7*24




*一致性*

必要的弱一致性


*原型拓展*
可以对各个组成模块进行性能优化以及定制，需要对相互协议接口进行定制
可以多个爬虫，多个中间存储以及多个文档处理进程同时运行
多种结果存储模式
解析以及处理模块利用更快速的框架以及工具
利用zookeeper类似的保证全局一致性以及容灾性
增加爬虫和处理中间结果的存储方式（html压缩？）
定义通用的消息接口，必要的话采用消息队列
html解析考虑采用hadoop进行解析
最后的结果存储考虑利用hbase以及类似数据库



#### 方案

模块划分

各部分实现技术以及方案
可能遇到的问题



## 参考

1. [信息抽取 互动百科](http://www.baike.com/wiki/%E4%BF%A1%E6%81%AF%E6%8A%BD%E5%8F%96)
2. [Information extraction wiki](http://en.wikipedia.org/wiki/Information_extraction)
3. [General Architecture for Text Engineering-GATE](http://en.wikipedia.org/wiki/General_Architecture_for_Text_Engineering)



