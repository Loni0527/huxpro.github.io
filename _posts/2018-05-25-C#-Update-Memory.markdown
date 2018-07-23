---
layout:     post
title:      "C# 32位程序申请大内存"
subtitle:   ""
date:       2018-05-25
author:     "Loni"
header-img: "img/post-bg-js-module.jpg"
catalog: true
tags:
    - 随手记
    - C#
---



最近在编写测试一个32位程序时（由于程序维护，并且使用的以前32位的dll文件，所以只能编译成32位），在程序运行内存占用到1.7G左右时总是出现程序崩溃。

　　后来添加日志发现是内存溢出(OutOfMemoryException）；本身32位程序只能申请到2GB内存，经过在网上找的各种方法和测试，如下方法可行，能申请到4GB内存。

1、管理员模式下运行CMD，输入：BCDEdit /set PAE forceenable Windows

 这里的BCDEdit是关于命令行的启动配置编辑器。使用上面的命令，你能启用物理地址扩展（PAE），让支持的内存大于4GB

2、管理员模式下运行CMD，输入：bcdedit /set increaseuserva 3072

来使得windows把2G以上的内存也分配给应用程序！

3、重启电脑。

4、重新编译程序。

5、在开始-》程序-》Visual Studio2012-》中找到“Visual Studio 命令提示(2012)”打开已设置VS环境变量的CMD窗口，在命令行下执行：

editbin /LARGEADDRESSAWARE 你的程序名.exe

如果要恢复2GB模式，则使用如下命令删除

1、BCDEdit /deletevalues PAE

2、BCDEdit /deletevalues increaseuserva

3、重启电脑。

[原文连接](https://www.cnblogs.com/AndyBian58/p/6639702.html)