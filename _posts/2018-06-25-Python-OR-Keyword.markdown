---
layout:     post
title:      "Python or 关键字"
date:       2018-06-24 12:00:00
author:     "Loni"
---

or 除了用在if中还可以用在赋值使用中

```
a = 1 or 2
```

等于

```
if a:
   a=1
else
   a=2
```

简单来说，在赋值时使用or关键字时会先判断or左边是否为True，为Tue则返回左边的值，否则返回右边的值。

```
a=1
b= a>0 or 2
print(b)
True
```