---
author: Loni
date: 2018-11-08 15:00
layout: post
status: public
tags:
  - C#
  - 随手记
  - SQLite
title: 记一次环境部署
---

搬公司后第一次完成数据的抓取，需要重新部署一套程序来入库。
环境都是现成的，按道理只要点点点就完事了，却在最后一下报错了。
看日志```未能加载DbProviderFactory对象``` 这是啥问题，本地运行没毛病的呀。
找不到头绪，加日志吧。还好记录了一些有用的信息```未能加载文件或程序集“System.Data.SQLite”或它的某一个依赖项。试图加载格式不正确的程序。```
SQLite已经安装了，还报错那应该就是版本不对了。
既然找到问题了，就好解决。
[SQLite Down Page](http://system.data.sqlite.org/index.html/doc/trunk/www/downloads.wiki)
下载对应系统版本的的SQLite ,安装后把目录\bin下的```System.Data.SQLite.dll```文件替换之前的dll。
完事。