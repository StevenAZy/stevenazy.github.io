+++
title = "NVML初始化失败"
date = 2021-03-24T21:49:25+08:00
images = []
tags = ['BUG']
categories = ['技术']
draft = false
+++

### 问题：Failed to initialize NVML: Driver/library version mismatch

### 环境
OS: Ubuntu 16.04 

Shell: zsh

GPU: Nvidia GTForce 2080 Ti

### 错误
查看GPU状态，输入`nvidia-smi`返回了`Failed to initialize NVML: Driver/library version mismatch的错误`。
经过一番百度+谷歌的操作，发现原因是：NVIDIA内核驱动版本和系统驱动版本不一样。



### 解决
第一种方式，由于作者需要安装深度学习的环境，所以直接卸载驱动然后安装CUDA，因为CUDA 10.x之后的版本都是自带有驱动的。当实际操作时，利用CUDA是无法进行驱动安装的，必须要在安装时将驱动安装的选项删掉，这样才可以保证CUDA的顺利安装。（这里具体是什么问题作者也不清楚，希望有好心人可以帮忙解答！）

第二种方式，利用CUDA安装驱动的方式失败之后，作者就直接想安装驱动。网上的大部分教程都是基于桌面进行的，作者是通过ssh远程连接的，最后找了很久才找到一个教程如何直接利用命令行进行Nvidia驱动安装（这里也呼吁一下大家，出教程的时候，也考虑一下无桌面的情况）。

### 命令行安装Nvidia驱动
从默认Ubuntu存储库中列出Nvidia的可用驱动程序:
   
`sudo ubuntu-drivers devices`

安装驱动程序:

`sudo ubuntu-drivers autoinstall`

或者安装指定版本的驱动:

`sudo apt install nvidia-driver-xxx`xxx是驱动版本号

### 2021.04.14更新
`sudo rmmod nvidia`
这个命令可以直接更新一下驱动，不在需要卸载驱动再重新安装。