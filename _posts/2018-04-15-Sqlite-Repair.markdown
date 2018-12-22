---
author: Loni
catalog: true
date: 2015-04-15 00:00
layout: post
status: public
subtitle:
tags:
  - 随手记
  - SQLite
title: Sqlite文件修复
---

--先下载sqlite3.exe  
--打开损坏的old.sqlite文件  
sqlite3.exe old.sqlite  
--导出到临时文件"old.tmp"(注意看导出后的文件最后一名是否为COMMIT,有时候会是ROOLBACK,如果是ROOLBACK就改为COMMIT,否则导入不成功)。  
.output "old.tmp"  
.dump  
--退出，在退出前”old.tmp“可能还是0kb,当执行完“.quit”后就会改变大小。  
.quit  
--打开新建的sqlite文件，如果不存在正值的命令也会新建一个文件。  
sqlite3.exe new.sqlite  
--导入到旧数据到“new.sqlite”。  
.read "old.tmp"  
--退出。  
.quit  