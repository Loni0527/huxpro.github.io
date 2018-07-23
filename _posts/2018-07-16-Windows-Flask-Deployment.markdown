---
layout:       post
title:        "如何在Windows server上部署flask"
subtitle:     ""
date:         2018-07-16 17:22:00
author:       "Loni"
header-img:   "img/in-post/post-eleme-pwa/eleme-at-io.jpg"
header-mask:  0.3
catalog:      true
multilingual: true
tags:
    - python
    - flask
    - 部署
---

在Linux下一般以Flask+uWSGI+Nginx的形式部署，win下部署起来确实很麻烦，如果不是大规模的正式应用的话，可以用tornado-server来部署。具体方法很简单，在你的flask项目里原来的入口程序假设为run.py的同级目录添加tornado应用程序tornado_server.py，内容如下：

```
#coding=utf-8
from tornado.wsgi import WSGIContainer
from tornado.httpserver import HTTPServer
from tornado.ioloop import IOLoop
from run import app
http_server = HTTPServer(WSGIContainer(app))
http_server.listen(9000)  #flask默认的端口
IOLoop.instance().start()```
