---
author: Loni
date: 2018-08-16 12:00
layout: post
status: public
tags:
  - Python
  - Package
title: 'python 相关模块安装 国内镜像地址'
---

python 相关模块安装 国内镜像地址

pipy国内镜像目前有：

[豆瓣](http://pypi.douban.com/)

[华中理工大学](http://pypi.hustunique.com/)  

[山东理工大学](http://pypi.sdutlinux.org/)  

[中国科学技术大学](http://pypi.mirrors.ustc.edu.cn/ )

[清华大学](https://pypi.tuna.tsinghua.edu.cn/ )

对于pip这种在线安装的方式来说，很方便，但网络不稳定的话很要命。使用国内镜像相对好一些，

如果想手动指定源，可以在pip后面跟-i 来指定源，比如用豆瓣的源来安装web.py框架：

pip install web.py -i http://pypi.douban.com/simple

注意后面要有/simple目录！！！

要配制成默认的话，需要创建或修改配置文件（linux的文件在~/.pip/pip.conf，windows在%HOMEPATH%\pip\pip.ini），修改内容为：

code:
```
[global]

index-url = http://pypi.douban.com/simple

推荐使用清华大学的源，速度快(依个人情况而定！)：

pip3 install -i https://pypi.tuna.tsinghua.edu.cn/simple django

pip3 install -i https://pypi.tuna.tsinghua.edu.cn/simple pillow

pip3 install -i https://pypi.tuna.tsinghua.edu.cn/simple paramiko

pip3 install -i https://pypi.tuna.tsinghua.edu.cn/simple cryptography==1.5.2

pip3 install -i https://pypi.tuna.tsinghua.edu.cn/simple django-session-security==2.4.0

pip3 install -i https://pypi.tuna.tsinghua.edu.cn/simple djangorestframework==3.5.3

pip3 install -i https://pypi.tuna.tsinghua.edu.cn/simple paramiko==2.0.2

pip3 install -i https://pypi.tuna.tsinghua.edu.cn/simple pycparser==2.16

pip3 install -i https://pypi.tuna.tsinghua.edu.cn/simple PyMySQL==0.7.9
```
