---
layout:     post
title:      "修复Table 'XXX' is marked as crashed and should be repaired"
subtitle:   ""
date:       2018-02-01 12:00:00
author:     "Loni"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 随手记
    - 数据库
    - mysql
---

```
1、登录liunx服务器
2、cd /home/MysqlData/数据库名
3、myisamchk -c -r 表名.MYI​

无法修复时可尝试使用以下命令

myisamchk -r -f 表名.MYI -o -q

```

myisamchk命令使用总结:

myisamchk实用程序可以用来获得有关你的数据库表的统计信息或检查、修复、优化他们

1.常用于myisamchk的检查选项
```
--information, -i
打印所检查表的统计信息。

--fast，-F
只检查没有正确关闭的表。

--force, -f
如果myisamchk发现表内有任何错误，则自动进行修复。维护类型与-r选项指定的相同。

--medium-check, -m
比--extend-check更快速地进行检查。只能发现99.99%的错误，在大多数情况下就足够了。

长用命令如下：
快速的检查
[root@localhost ~]# myisamchk -im /var/lib/mysql/backup/t1

只检查没有正常关闭的表
[root@localhost ~]# myisamchk -iFm /var/lib/mysql/backup/*

仅显示表的最重要的信息
[root@localhost backup]# myisamchk -eis /var/lib/mysql/backup/t1
```
2.长用于myisamchk的修复选项
```
--backup, -B
将.MYD文件备份为file_name-time.BAK

--correct-checksum
纠正表的校验和信息。

--force, -f
覆盖旧的中间文件(文件名类似tbl_name.TMD)，而不是中断。

--quick，-q
不修改数据文件，快速进行修复。出现复制键时，你可以两次指定该项以强制myisamchk修改原数据文件。

--recover, -r
可以修复几乎所有一切问题，除非唯一的键不唯一时(对于MyISAM表，这是非常不可能的情况)。如果你想要恢复表，这是首先要尝试的选项。如果myisamchk报告表不能用-r恢复，则只能尝试-o。如果你有大量内存，你应增加sort_buffer_size的值。

--safe-recover, -o
使用一个老的恢复方法读取，按顺序读取所有行，并根据找到的行更新所有索引树。这比-r慢些，但是能处理-r不能处理的情况。该恢复方法使用的硬盘空间比-r少。一般情况，你应首先用-r维修，如果-r失败则用-o。如果你有大量内存，你应增加sort_buffer_size的值。

--tmpdir=path, -t path
用于保存临时文件的目录的路径。如果未设置，myisamchk使用TMPDIR环境变量的值。tmpdir可以设置为一系列目录路径，用于成功地以round-robin模式创建临时文件。在Unix中，目录名之间的间隔字符为冒号(‘:’)，在Windows、NetWare和OS/2中为分号 (‘；’)。

--unpack，-u
将用myisampack打包的表解包。

常用恢复命令：
首先尝试用这种恢复方式
[root@localhost ~]# myisamchk -iBfqr /var/lib/mysql/backup/t1
如果上面的恢复失败，再尝试用如下的方式，这个比较慢
[root@localhost ~]# myisamchk -iBfqo /var/lib/mysql/backup/t1
```
3.长用于myisamchk的分析选项
```
--analyze，-a
分析键值的分布。这通过让联结优化器更好地选择表应该以什么次序联结和应该使用哪个键来改进联结性能。要想获取分布相关信息，使用如下两个命令
mysql> show keys from t1;
或
[root@localhost ~]# myisamchk --description --verbose /var/lib/mysql/backup/t1

--description, -d
打印出关于表的描述性信息

--sort-index, -S
以从高到低的顺序排序索引树块。这将优化搜寻并且将使按键值的表扫描更快。

--sort-records=N, -R N
根据一个具体索引排序记录。这使你的数据更局部化并且可以加快在该键上的SELECT和ORDER BY的范围搜索。（第一次做排序可能很慢！）为了找出一张表的索引编号，使用SHOW INDEX，它以myisamchk看见他们的相同顺序，显示一张表的索引。索引从1开始编号。

如果键没有打包(PACK_KEYS=0)，它们的长度相同，因此当myisamchk 排序并移动记录时，只覆盖索引中的记录偏移量。如果
键已经打包(PACK_KEYS=1)，myisamchk必须先解开打包的键块，然后重新创建索引并再次将键块打包。(在这种情况下，重新创建索引比更新每个索引的偏移量要快）。
```
4.myisamchk内存使用

myisamchk默认只用3M的内存来修复，如果要修复大表的话，显然速度会巨慢，我们可以通过为myisamchk设置更多的内存，来使其运行的更快，
```
[root@localhost ~]# myisamchk --sort_buffer_size=16M --key_buffer_size=16M --read_buffer_size=1M --write_buffer_size=1M
```
一般sort_buffer_size的大小16m就足够用了。

myisamchk默认使用选项“--tmpdir”作为临时文件的，如果tmpdir指定内存的话，恢复的表比较大，很容易报内存的错误，所以我们可以用tmpdir指定一个比较大的文件系统

```[root@localhost ~]# myisamchk --sort_buffer_size=16m --key_buffer_size=16m --read_buffer_size=2m --write_buffer_size=1m --tmpdir=/tmp -iBfqr /var/lib/mysql/backup/t1```

5.myisamchk用于崩溃恢复
在使用myisamdchk修复会优化表时，必须保证mysqld服务器没有使用该表，最好关闭mysqld服务；如果不关闭mysqld，在运行myisamchk之前应执行mysqladmin flash-tables。如果服务器和myisamchk同时访问表，表可能会被破坏。

使用“--skip-external-locking”一般是系统的默认启用选项，mysql数据库一般也是应禁用该选项，因为使用系统的lock和mysql很容易产生死锁。

执行myisam表的恢复只要是修复表的三个文件，最常发生问题的文件是数据文件和索引文件
tbl_name.frm：定义(格式)文件
tbl_name.MYD：数据文件
tbl_name.MYI：索引文件

恢复步骤
A.检查myisam表的错误
```myisamchk -im --verbose /var/lib/mysql/backup/t1```

如果有错误，用perror命令查看错误码
[root@localhost ~]# perror 126
OS error code 126: Required key not available

B.初级修复myisam表
试图不接触数据文件来修复索引文件，
```myisamchk -rq tablename```

如果恢复失败，继续如下
#[root@localhost ~]# myisamchk -Br tablename

还不行就执行如下
#[root@localhost ~]# myisamchk -o tablename

C.中级修复myisam表
只有在索引文件的第一个16K块被破坏，或包含不正确的信息，或如果索引文件丢失，你才应该到这个阶段
```
1).把数据文件移到安全的地方。
2).使用表描述文件创建新的(空)数据文件和索引文件：
3).shell> mysql db_name
4).mysql> SET AUTOCOMMIT=1;
5).mysql> TRUNCATE TABLE tbl_name;
6).mysql> quit
```
如果没有TRUNCATE TABLE，则使用DELETE FROM tbl_name。
7).将老的数据文件拷贝到新创建的数据文件之中。 (记得保留一个副本以防某些东西出错)
8).在实行myisamchk -rq tablename应该就可以了
或
```mysql> REPAIR TABLE tbl_name USE_FRM```

D.高级恢复
1).从一个备份恢复描述文件然后执行“myisamchk -r tablename”
2).如果没有备份而知道表是怎样创建的，在另一个数据库中创建表的一个拷贝。删除新的数据文件，然后从其他数据库将描述文件和索引文件移到破坏的数据库中。这样在破坏的库里就有新的描述和索引文件，但是让.MYD数据文件独自留下来了。然后在执行“myisamchk -r tablename”

6.myisamchk对表优化
为了组合碎片记录并且消除由于删除或更新记录而浪费的空间
```shell> myisamchk -r tbl_name```

对所有的索引进行排序以便更快地查找键值
```myisamch -S tablename```

对指定的索引进行排序以便更快地查找键值
```mysql> show index from tablename;```
```myisamch -R 1 tablename```

如果你用动态大小的行更改MyISAM表(含VARCHAR、BLOB或TEXT列的表)或有删除了许多行的表，你可能想要不时地（每月一次）整理/组合表的空间

可以对有问题的表执行OPTIMIZE TABLE来优化。或者是，如果可以停一会mysqld服务器,执行如下命令：
``` myisamchk -r -s --sort-index -O sort_buffer_size=16M */*.MYI```