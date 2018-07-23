---
layout:     post
title:      "List、Dict元素操作（python）"
subtitle:   ""
date:       2018-04-14 
author:     "Loni"
header-img: "img/post-bg-unix-linux.jpg"
catalog: true
tags:
    - Python
    - List
    - Dict
---

增加元素：

list[]:

**1\. append() 追加单个元素到List的尾部**，只接受一个参数，参数可以是任何数据类型，被追加的元素在List中保持着原结构类型。

此元素如果是一个list，那么这个list将作为一个整体进行追加，注意append()和extend()的区别。

```
>>> list1=['a','b']
>>> list1.append('c')
>>> list1
['a', 'b', 'c']
```

**2\. extend() 将一个列表中每个元素分别添加到另一个列表中**，只接受一个参数；extend()相当于是将list B 连接到list A上。

```
>>> list1
['a', 'b', 'c']
>>> list1.extend('d')
>>> list1
['a', 'b', 'c', 'd']
```

**3\. insert() 将一个元素插入到列表中，但其参数有两个（如insert(1,”g”)），**第一个参数是索引点，即插入的位置，第二个参数是插入的元素。

```
>>> list1
['a', 'b', 'c', 'd']
>>> list1.insert(1,'x')
>>> list1
['a', 'x', 'b', 'c', 'd']
```

**4\. + 加号，将两个list相加，会返回到一个新的list对象，注意与前三种的区别。**前面三种方法（append, extend, insert）可对列表增加元素的操作，他们没有返回值，是直接修改了原数据对象。 注意：将两个list相加，需要创建新的list对象，从而需要消耗额外的内存，特别是当list较大时，尽量不要使用“+”来添加list，而应该尽可能使用List的append()方法。

```
>>> list1
['a', 'x', 'b', 'c', 'd']
>>> list2=['y','z']
>>> list3=list1+list2
>>> list3
['a', 'x', 'b', 'c', 'd', 'y', 'z']
```

dict{}

```
dict['key']=value

合并方法1：

dictMerged1=dict(dict1.items()+dict2.items())
合并方法2：

dictMerged2=dict(dict1, **dict2)
方法2等同于：

dictMerged=dict1.copy()
dictMerged.update(dict2)

或者

dictMerged=dict(dict1)
dictMerged.update(dict2)
方法2比方法1速度快很多
```

删除元素：

```
list[]:

del list(key) #删除指定下标元素

pop（）#删除最后一个数， list.pop()

remove()#删除指定的一个值，list.remove(value)

clear()#清空列表，list.clear()

dict{}:

pop()#删除并返回给定健对应的值，如：dict.pop('key')

clear()#清空字典内容，dict.clear()

popitem()#随机返回并删除字典中的一对键和值(一般删除末尾对)。, dict.popitem()
```

