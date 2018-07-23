---
layout:     post
title:      "pyspider分布式——windows"
subtitle:   ""
date:       2018-03-25 
author:     "Loni"
header-img: "img/post-bg-digital-native.jpg"
catalog: true
tags:
    - Python
    - Pyspider
    - 分布式
---

谷歌，百度都翻烂了，也没找到在windows上分布式部署pyspider的例子，几乎绝望了。

查资料发现pyspider是通过redis传输任务。

只好开始一无所知的瞎折腾，总算是有点结果。slave上的fetcher，processor，result_worker三个模块都有信息在输出，我想，这应该是成功了。

废话结束--------------------------------------------------------------------------------------------------------------------------------------------------------

首先安装redis

安装好后将redis.windows.conf中

```
bind 127.0.0.1 改为 bind 0.0.0.0 #这样修改是为了让其它机器可以访问本机redis
protected-mode yes 改为protected-mode no  #在redis3.2之后，redis增加了protected-mode，在这个模式下，即使修改掉了bind 127.0.0.1，再访问redisd时候还是报错。
```

在redis目录下建立redis.6380.conf文件，6380是redis的端口，默认是6379，我这里修改成了6380，在redis.windows.conf也需要修改port 6379为port 6380

```
port 6380      
loglevel notice    
logfile ""D:/Redis/Logs/redis6380_log.txt""       
appendonly yes
appendfilename ""appendonly.6380.aof""   
cluster-enabled yes                                    
cluster-config-file nodes.6380.conf
cluster-node-timeout 15000
cluster-slave-validity-factor 10
cluster-migration-barrier 1
cluster-require-full-coverage yes
```

```
运行 redis-server.exe redis.windows.conf
```

的config.conf配置:

```
{
 ""taskdb"": ""mysql+taskdb://pyspider:pyspider-pass@192.168.209.128:3306/taskdb"",
  ""projectdb"": ""mysql+projectdb://pyspider:pyspider-pass@192.168.209.128:3306/projectdb"",
  ""resultdb"": ""mysql+resultdb://pyspider:pyspider-pass@192.168.209.128:3306/resultdb"",
  ""message_queue"": ""redis://127.0.0.1:6380/db"",
  ""logging-config"": ""/pyspider/logging.conf"",
  ""phantomjs-proxy"": ""/127.0.0.1:25555"",
  ""fetcher"": {
    ""xmlrpc-host"": ""0.0.0.0""
  },
 ""scheduler"": {
    ""xmlrpc-host"": ""0.0.0.0"",
    ""delete-time"": 10
  },
  ""webui"": {
    ""port"": 5000,
    ""username"": """",
    ""password"": """",
    ""need-auth"": false
  }
}
```

在master上运行：

```
pythona run.py -c E:/Spider/Spider/pyspider/config.json scheduler
pythona run.py -c E:/Spider/Spider/pyspider/config.json webui
pythona run.py -c E:/Spider/Spider/pyspider/config.json result_worker
```

slave 上运行：

```
python run.py -c E:/Spider/Spider/pyspider/config.json fetcher
python run.py -c E:/Spider/Spider/pyspider/config.json processor
```

以上方法也是我自己瞎折腾出来的，其中的原理还需要再进一步的研究。

很少写博客，文笔不好，请见谅。


