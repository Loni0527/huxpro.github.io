---
author: Loni
date: 2018-03-10 12:00
layout: post
status: public
subtitle:
tags:
  - Python
  - Pyspider
  - 爬虫
  - Weibo
title: 基于Pyspider的weibo.cn爬虫
---

# 一些学习资料

1.  [Fiddler简易使用教程 抓cookies用**（必看）**](https://link.jianshu.com?t=http://xijiacs.lofter.com/post/1d96cd64_a0f4013)
2.  [PySpider简易教程 整个爬虫用到的框架**（必看）**](https://www.jianshu.com/p/36290e6acf45)
3.  [HTTP Header入门详解](https://link.jianshu.com?t=http://my.oschina.net/abian/blog/131548?fromerr=rY5qyfx5) 在模拟登录过程中要涉及到http头的设置，需要了解基本信息
4.  [全程模拟新浪微博登录2015](https://link.jianshu.com?t=http://blog.csdn.net/u010487568/article/details/46932839) 这个分析了新浪微博网页版现在还在用的登录过程，其中使用到的最新脚本ssologin.js版本号1.4.18。不过本文主要是基于wap版的爬虫，这个没必要看，如果想进一步爬取网页版的微博可以参考学习。
5.  [Sina微博爬取@pyspider](https://link.jianshu.com?t=http://blog.csdn.net/dipolar/article/details/49661083) 这篇文章通过用户名和密码获取wap版微博的cookies后再进行后续操作，也可参考。
6.  [PyQuery文档](https://link.jianshu.com?t=https://pythonhosted.org/pyquery/index.html) `&&` [CSS选择器](https://link.jianshu.com?t=http://www.w3schools.com/cssref/css_selectors.asp)`&&`[Python正则表达式re package文档](https://link.jianshu.com?t=https://docs.python.org/2/library/re.html)
    `Python`页面爬下来以后用于操作页面元素获取需要的内容**（必看）**

# 获取cookies用于模拟登陆

参考学习资料1里面设置好fiddler，然后打开<a>http://weibo.cn/</a> 没登陆的话登陆。在登录的状态下打开你要进行爬取的页面，观察fiddler里抓到的包，得到需要的cookies信息

   获取cookies
对应设置好PySpider里的`crawl_config`，需要注意的是`cookies`和`headers`，考虑到我的代码逻辑我把这两个都放在`crawl_config`里而不是具体的爬取函数里。关于头的设置也可以参考fiddler里`Headers`一栏，完整代码贴在最后可以参考我的设置。

# 爬虫逻辑

我的需求是对于指定的用户，给出用户主页（形如`http://weibo.cn/kaikai0818`或`http://weibo.cn/u/1788136742`），爬取TA全部的微博及相关信息（如发布时间、转发数等）。

入口函数`on_start`没什么可说的，因为设置了全局的headers和cookies这边在`self.crawl`的时候就不需要再发送了，如果没设置成全局的，必须在这边设置并发送。

`index_page`函数主要用来计算一共有多少页需要爬取，页面有一个类型为`hidden`的`<input>`元素记录了一共有多少页，然后一个for得到所有需要爬取的页面地址。

`list_single_page`用于处理每一页微博的内容，一页有十条，主要就是操作页面获取单条微博的地址（因为后续需求可能需要爬取每一条微博的转发和评论内容）。这边有个trick，和web版微博不同的是，wap版单条微博并没有一个所谓的地址，只有一个转发或者评论的地址，代码里用了转发的地址。值得注意的是**我自己测试这个爬虫的时候爬了1500条微博左右的时候账号被冻结了，建议在dashboard调一下rate、burst值。**不过后来登录后激活了一下账号又能用了，还没测试过多少值可以避免被冻，因为不清楚新浪冻结的机制，我的小号还要用来花痴的，不敢瞎搞了_(:з」∠)_

`detail_page`用来处理单条微博，然后就是css选择器+正则的应用了哇，没什么可说的，就是找规律，目前测试过了没啥问题，不过爬下来的1500多条也没认真检查过，大家自己再看看了哇。

一个能跑的代码如下：

```
#!/usr/bin/env python
# -*- encoding: utf-8 -*-
# Created on 2016-03-07 13:26:00
# Project: user_timeline

import re
import time
from pyquery import PyQuery
from pyspider.libs.base_handler import *

class Handler(BaseHandler):
    user_url = ""http://weibo.cn/kaikai0818""

    crawl_config = {
        'itag': 'v1',

        'headers': {
            'User-Agent': 'Mozilla/5.0 (Windows NT 6.1; WOW64; rv:44.0) Gecko/20100101 Firefox/44.0',
            ""Host"": ""weibo.cn"",
            ""Accept"": ""text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8"",
            ""Accept-Language"": ""zh-CN,zh-TW;q=0.8,zh-HK;q=0.6,en-US;q=0.4,en;q=0.2"",
            ""Accept-Encoding"": ""gzip, deflate"",
            ""DNT"": ""1"",
            ""Connection"": ""keep-alive""
        },

        'cookies': {
            ""_T_WM"":""I❤kkw(¯﹃¯)"",
            ""SUB"":""I❤kkw(¯﹃¯)"",
            ""gsid_CTandWM"":""I❤kkw(¯﹃¯)"",
            ""_T_WL"":""1"",
            ""_WEIBO_UID"":""I❤kkw(¯﹃¯)"" 
        }
    }

    @every(minutes=24 * 60)
    def on_start(self):        
        self.crawl(Handler.user_url, callback=self.index_page,method=""GET"")   

    @config(age=1 * 24 * 60 * 60)        
    def index_page(self, response):
        #计算该用户的微博共有几页
        pages = response.doc(""[type=hidden]"").attr[""value""]            
        for i in range(1,int(pages)+1):
            self.crawl(Handler.user_url+""?page=""+str(i), callback=self.list_single_page,method=""GET"")

    @config(priority=2) #数字越大优先级越高
    def list_single_page(self, response):
        #处理当前页的微博        
        url = ""http://weibo.cn/repost/""
        for each in response.doc(""div[id^=\""M_\""]"").items() : mid = each.attr(""id "") self.crawl(url + mid[2 : ], cookies = response.cookies, callback = self.detail_page)#self.crawl可加上参数exetime = time.time() + 1 * 60（即一分钟后再crawl）

@config(priority = 1) def detail_page(self, response) : res = response.doc(""#M_ "")

#判断是否为转发
if len(res.find(""span.cmt "")) != 0 : is_rt = 1
else: is_rt = 0

#判断是否含图片
if len(res.children(""div "").eq(1).find(""img "")) != 0 : has_pic = 1
else: has_pic = 0

if is_rt == 0 : text = res.find(""span.ctt "").text() orig_user = ""NA ""orig_text = ""NA ""
else: orig_user = res(""div: first - child span.cmt a "").text() orig_text = res.find(""span.ctt "").text() td = re.findall(r '</span>([\s\S]+)<span class=', res(""div: last - child "").html()) text = PyQuery(td[0]).text() return {
    ""screen_name "": res(""div: first - child & gt; a: first - child "").text(),
    ""time "": res.find(""span.ct "").text(),
    ""text "": text,
    ""is_rt "": is_rt,
    ""has_pic "": has_pic,
    ""orig_user "": orig_user[1 : ],
    ""orig_text "": orig_text,
    ""repo_cnt "": re.search('\d+', response.doc(""span.pms "").text()).group(),
    ""cmt_cnt "": re.search('\d+', response.doc(""span.pms "").siblings().eq(0).text()).group(),
    ""atti_cnt "": re.search('\d+', response.doc(""span.pms "").siblings().eq(1).text()).group()
} < /code>
```

原文作者：[兮嘉](https://www.jianshu.com/p/c15102a6eb21)