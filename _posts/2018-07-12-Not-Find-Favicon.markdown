---
author: Loni
catalog: true
date: 2018-07-12 12:00
layout: post
multilingual: true
status: public
subtitle:
tags:
  - 前端开发
  - WEB
title: Favicon.ico文件找不到
---

今天使用sublime以localhost方式打开html文件时（使用wamp环境提供一个Apache服务器，html文件存在于wamp环境的www文件夹下），出现favicon.ico文件找不到问题

查看D:\wamp\logs文件夹的apache_error.log文件发现以下错误信息：

`[Thu May 11 16:40:06 2017] [error] [client ::1] File does not exist: D:/wamp/www/favicon.ico, referer: http://localhost/js/test.html`

仔细对照路径查看确实没有favicon.ico文件，后来查了相关的资料才知道，这是浏览器自动加载的，浏览器一般自动在网站根目录寻找，就是你页面卡片那个图标。

favicon.ico意指你的网站图标。 当有人（使用IE浏览器）将你的网站收藏为“my favorite”时，就会去参照网站根目录下的“favicon.ico”文件，这个图标也就是“my favorite”里显示的图标。 
比如你将“http://www.debian.org/”列为“my favorite”的时候，你的“my favorite”清单会显示“http://www.debian.org/favicon.ico”这个图标。 
当你的根目录下没有“favicon.ico”这个文件时，“my favorite”里将显示IE浏览器的图标，与此同时“favicon.ico”不存在的信息（404 not found）会写到你的apache2错误日志中去，这样你可以从这个日志中看出，什么时候，什么人（其IP网址）将你的网站设定为“my favorite”。
解决的方法：
1、做个favicon.ico文件放在根目录下，在head标签引入favicon.ico文件即可

`<pre class=""language-markup""><code>&lt;link href=""favicon.ico"" rel=""shortcut icon""&gt;</code></pre>`
2、在Stack Overflow搜索到的，直接在head标签插入以下代码也OK
`<pre class=""language-markup""><code>&lt;link rel=""shortcut icon"" href=""#"" /&gt;</code></pre>`