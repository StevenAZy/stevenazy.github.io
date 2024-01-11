+++
title = "Cmpress和compress真不一样"
date = 2023-07-12T21:34:45+08:00
images = []
tags = ['安装教程']
categories = ['技术']
draft = false
+++
​
最近在博主在复现一篇[论文](https://www.biorxiv.org/content/10.1101/2022.09.09.507333v1)​​​​​​​，该论文在处理数据集时用到了一个命令`cmpress`。当输入这个命令时，终端提醒`command not found`，于是博主Google了一下，找到的词条都是`compress`，也许是作者写错了README，应该就是`compress`，博主还自以为是的在Github上给作者提了个[issue](https://github.com/uw-ipd/RoseTTAFold2NA/issues/44)并沾沾自喜。后续在对代码进行调试时发现，``cmpress``对数据的操作不应该是压缩，而应该是对数据集进行其他的操作。
经过博主在网上一番冲浪终于找到了``cmpress``的出处，它来自于一个叫``infernal``的工具，这个工具主要是用于搜索结构RNA序列同源性的测序数据库，以及实现基于序列或结构的RNA序列比对。``infernal``包含的命令主要有以下几个``cmalign``，``cmbuild``，``cmcalibrate``，``cmconvert``，``cmemit``，``cmfetch``，``cmpress``，``cmscan``，``cmsearch``，``cmstat``，具体的用途可以查阅其官方的[文档](http://eddylab.org/infernal/Userguide.pdf)。
既然弄清楚了``cmpress``怎么来的，接下来就讲一讲如何安装``infernal``。首先需要到[官网](http://eddylab.org/infernal/)去下载最新的``infernal``压缩包，博主采用的是``wget``下载。
```
# 下载infernal包
wget http://eddylab.org/infernal/infernal-1.1.4.tar.gz
# 解压缩
tar xf infernal-1.1.4.tar.gz
# 进入infernal包
cd infernal-1.1.4
```
![下载截图](/images/download.png)
下载解压完成之后，就可以开始安装了。
```
# 配置安装路径
./configure  --prefix=/home/steven/infernal
# 安装
make && make install
```
![遇到的错误](/images/error.png)
安装过程中还遇到了一个错误，`./configure`配置路径是要用绝对路径不可以使用相对路径。
以上``infernal``的安装就结束啦！使用时带上路径，例如使用``cmpress``，直接路径加上命令``/home/steven/infernal/bin/cmpress``就可以了。
![成功截图](/images/success.png)
如果要是嫌这个麻烦的话，可以直接将路径添加到环境变量就可以直接使用对应的命令，不用在加上路径。至于如何添加环境变量，网上的资源已经很多了，自己去搜就可以了。

