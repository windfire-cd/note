================================
Markdown And RestructuredText
================================

.. contents:: Table of Contents

概述
-----------

介绍配置使用Markdown和RestructuredText以及相关对比。
以及这两天配置和\
使用的部分经验，所有资料来自于网络，最开始想要使用这两种工具的起因是ppt对于代码高亮支持不够理想，
然后发现若干网络上面的代码高亮很不错

Markdown 安装以及工具链
----------------------------

需要安装 Pandoc_ ,这个比较好使，幻灯，代码高亮，pdf以及docx生成都可以使用\
这个工具也可以转换restructuredtext格式，但是似乎对于Markdown格式更加亲和。\
ubuntu的软件管理中存在该工具，如果需要更新到最新版本的进行如下操作：

.. code:: bash

    sudo apt-get install haskell-platform
    sudo cabal update
    sudo cabal install pandoc

在该网站上有若干 Example_ 可以供参考

.. _Pandoc: http://johnmacfarlane.net/pandoc/index.html

.. _Example: http://johnmacfarlane.net/pandoc/demos.html


Markdown 语法
------------------

`Markdown简明教程`__

__ http://wowubuntu.com/markdown/


RestructuredText安装以及工具链
----------------------------------

依赖
~~~~~~~~~

**texlive**

在ubuntu上面有texlive 2009，如果希望安装更新的版本的话需要按照\
Texlive官方安装文档手动安装，\
没有特殊的apt-get可用，需要下载 install-tl-unx.tar.gz_

.. _install-tl-unx.tar.gz: http://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz

在ubuntu 12.04上运行如下命令

.. code:: bash
    :number-lines: 

    $sudo tar -xvf install-tl-unx.tar.gz && cd install-tl-unx && sudo ./install-tl

选择<i>进行安装



RestructuredText 安装
~~~~~~~~~~~~~~~~~~~~~~

在官网 Document_ 下载对应的`Python`源码文件，然后运行

.. code:: python
    :number-lines:

    $sudo python setup.py install

RestructuredText 语法
-------------------------

主要语法参见 Document_, Primer_, QuickRef_, Directives_

.. _Document: http://docutils.sourceforge.net/rst.html#user-documentation
.. _Primer: http://docutils.sourceforge.net/docs/user/rst/quickstart.html
.. _QuickRef: http://docutils.sourceforge.net/docs/user/rst/quickref.html
.. _Directives: http://docutils.sourceforge.net/docs/ref/rst/directives.html


**目录级别**

一般按照::

    = - ` : ' " ~ ^ _ * + # < >

的顺序进行目录配置

**链接**

+ 当前链接::

  `test <http://google.com.hk>`__

+ 匿名链接::

    test anynomous link `link`__
    __ http://google.com.hk

+ 外部链接::

    test global link example_link_
    .. _example_link: http://google.com.hk


**图片**

+ 当前图片::

    .. image:: img/test.png
        :align: center
        :scale: 150%
        :alt: 额是
        :target: http://baidu.com

+ 全局图片::

    .. |TestImg| image:: img/test.png
        :align: top
        :scale: 105%
        :alt: ceshi
        :target: http://baidu.com

     文字中使用图片 |TestImg|

Markdown，RestructuredText技巧和应用
---------------------------------------

这里记录一些Markdown和RestructuredText的一些技巧和应用

RestructuredText
~~~~~~~~~~~~~~~~~~

**生成html**

可以用pandoc, sphinx以及rst2html生成html。这三个工具特点如下：

    1. *pandoc* : Haskell语言库，转化格式较多，但是需要Haskell
    2. *sphinx* : Python官方文档库，比较强大，对中文支持好，
           但是比较复杂转化pdf借助于texlive，texlive-2011对中文支持更好
    3. *rst2html* : 官方的转化程序，使用简单，对中文支持好，我们一直用它！

**语法高亮**

可以利用如下代码进行语法高亮
::

    .. code:: lang-name
        :number-lines:

        source



在新的Docutils中可以支持 *code* 指令，但是需要Pygments进行解析和高亮\
官方安装利用下面的命令

.. code:: bash
    :number-lines: 

    $sudo apt-get install python-pygments

但是官方比较老，支持代码高亮的只在Docutils 0.9版本上，所以最好源码安装\
根据官方安装文档 Pygments-installation_ 进行安装

.. _Pygments-installation: http://pygments.org/docs/installation/

首先生成对应的sheet

.. code:: bash
    :number-lines: 

    $pygmentize -S default -f html > style.css

然后利用生成的css进行渲染

.. code:: bash
    :number-lines: 

    $rst2html --stylesheet=style.css test.rst test.html

**Slides**

rst2slides, landslide, rst2s5等均支持ReST转化为幻灯片，但是从格式支持上来说，rst2s5更为合理


Markdown
~~~~~~~~~~~~

**语法高亮**

输入格式为
::

 ~~~~~~~~~~{.lang-name, .numberLines}
 source
 ~~~~~~~~~~

其中 `~` 需要上下一致，`lang-name` 代表语言名称，`.numberLines` 代表是否标识代码\
行数

然后利用pandoc指定选项可以生成不同风格的代码高亮，例子如下

.. code:: bash

    pandoc code.txt -s --highlight-style pygments[tango|kate|..] -o example.html

Markdown, RestructuredText的中文相关问题
-----------------------------------------

**Markdown**

利用 pandoc -s *source* -o *target*
可以处理大部分中文问题，注意需要指定-s, -o选项，否则会出现乱码

**RestructuredText**

利用 *rst2html* , *rst2tex* 等工具可以直接转化，不需要特殊注意中文问题


**中文pdf**

无论Markdown或者RestructuredText默认使用pdflatex处理pdf文档，所以都无法完美\
解决中文问题，这里我们需要使用xelatex解决中文字体问题，在texlive安装目录对应\
版本下的texmf-dist/tex/xelatex/目录下，新建zhfontcfg目录，在该目录中创建\
zhfontcfg.sty宏包内容如下

.. code:: tex

     \ProvidesPackage{zhfontcfg}
     \usepackage{fontspec,xunicode}
     \defaultfontfeatures{Mapping=tex-text} %如果没有它，会有一些 tex 特殊字符无法正常使用，比如连字符。
     
     % 中文断行
     \XeTeXlinebreaklocale "zh"
     \XeTeXlinebreakskip = 0pt plus 1pt minus 0.1pt
     
     %将系统字体名映射为逻辑字体名称，主要是为了维护的方便
     \newcommand\fontnamehei{WenQuanYi Micro Hei}
     %\newcommand\fontnamesong{SimSun}
     %\newcommand\fontnamekai{KaiTi_GB2312}
     \newcommand\fontnamemono{WenQuanYi Micro Hei Mono}
     %\newcommand\fontnameroman{Bitstream Vera Serif}
     
     %设置文档正文字体为宋体
     \setmainfont[BoldFont=\fontnamehei]{\fontnamehei}
     \setsansfont[BoldFont=\fontnamehei]{\fontnamehei}
     \setmonofont{\fontnamemono}
     
     %楷体
     %\newfontinstance\KAI{\fontnamekai}
     %\newcommand{\kai}[1]{{\KAI #1}}
     
     %黑体
     \newfontinstance\HEI{\fontnamehei}
     \newcommand{\hei}[1]{{\HEI #1}}
     
     %英文
     %\newfontinstance\ENF{\fontnameroman}
     %\newcommand{\en}[1]{\,{\ENF #1}\,}
     %\newcommand{\EN}{\,\ENF\,}S5_
    

然后运行

.. code:: bash

    sudo mktexlsr


其中设置正文字体通过

.. code:: bash

    fc-list :lang=zh-cn

获取

利用Markdown和RestructuredText生成.tex文件，然后在文件前面添加`\usepackage{zhfontcfg}`

最后用

.. code:: bash

    xelatex file.tex

生成相应的pdf文件

 
**中文换行**

如果在编辑器中直接打一个回车进行换行，那么在生成的文件中会回车处出现一个空格\
这使W3C的一个标准，但是可以进行屏蔽

在Markdown中在末尾处直接打'\\n'然后回车可以屏蔽该现象

在RestructuredText中末尾处直接打个'\\'然后回车可以屏蔽该现象
    

Markdown, RestructuredText对比
---------------------------------

Markdown是github主推的格式，比较简洁，就是一个text to html的格式\
其思想主要来源于email。\
ReST是Docutils的标记语法，Docutils是Python世界的文档工具集，Sphinx\
可以生成多种格式，有默认的生成工程过程，可以用`Makefile`进行管理 [m_or_r]_

但是在Stackflow上还有人说因为在mac上有实时的预览工具而选择Markdown


参考
--------------
.. [m_or_r] http://ieqi.net/2012/04/13/markdown-%E8%BF%98%E6%98%AF-restructuredtext/
