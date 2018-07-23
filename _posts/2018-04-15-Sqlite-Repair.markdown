---
layout:     post
title:      "Sqlite文件修复"
subtitle:   ""
date:       2015-04-15
author:     "Loni"
header-img: "img/post-bg-os-metro.jpg"
catalog: true
tags:
    - 随手记
    - Sqlite
---


<p>--先下载sqlite3.exe
  <br />--打开损坏的old.sqlite文件
  <br />sqlite3.exe old.sqlite
  <br />--导出到临时文件"old.tmp"(注意看导出后的文件最后一名是否为COMMIT,有时候会是ROOLBACK,如果是ROOLBACK就改为COMMIT,否则导入不成功)。
  <br />.output "old.tmp"
  <br />.dump
  <br />--退出，在退出前&rdquo;old.tmp&ldquo;可能还是0kb,当执行完&ldquo;.quit&rdquo;后就会改变大小。
  <br />.quit
  <br />--打开新建的sqlite文件，如果不存在正值的命令也会新建一个文件。
  <br />sqlite3.exe new.sqlite
  <br />--导入到旧数据到&ldquo;new.sqlite&rdquo;。
  <br />.read "old.tmp"
  <br />--退出。
  <br />.quit</p>

