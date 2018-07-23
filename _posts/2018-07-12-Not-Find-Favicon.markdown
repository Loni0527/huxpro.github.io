---
layout:       post
title:        "Favicon.ico文件找不到"
subtitle:     ""
date:         2018-07-12 12:00:00
author:       "Loni"
header-img:   "img/in-post/post-eleme-pwa/eleme-at-io.jpg"
header-mask:  0.3
catalog:      true
multilingual: true
tags:
    - 前端开发
    - WEB
---

<p>今天使用sublime以localhost方式打开html文件时（使用wamp环境提供一个Apache服务器，html文件存在于wamp环境的www文件夹下），出现favicon.ico文件找不到问题</p>
<p><img src=""http://image.bubuko.com/info/201705/20180110231725747947.png"" alt=""技术分享"" data-bd-imgshare-binded=""1"" />查看D:\wamp\logs文件夹的apache_error.log文件发现以下错误信息：</p>
<p>[Thu May 11 16:40:06 2017] [error] [client ::1] File does not exist: D:/wamp/www/favicon.ico, referer: http://localhost/js/test.html</p>
<p>仔细对照路径查看确实没有favicon.ico文件，后来查了相关的资料才知道，这是浏览器自动加载的，浏览器一般自动在网站根目录寻找，就是你页面卡片那个图标。</p>
<p>favicon.ico意指你的网站图标。 当有人（使用IE浏览器）将你的网站收藏为&ldquo;my favorite&rdquo;时，就会去参照网站根目录下的&ldquo;favicon.ico&rdquo;文件，这个图标也就是&ldquo;my favorite&rdquo;里显示的图标。&nbsp;<br />比如你将&ldquo;http://www.debian.org/&rdquo;列为&ldquo;my favorite&rdquo;的时候，你的&ldquo;my favorite&rdquo;清单会显示&ldquo;http://www.debian.org/favicon.ico&rdquo;这个图标。&nbsp;<br />当你的根目录下没有&ldquo;favicon.ico&rdquo;这个文件时，&ldquo;my favorite&rdquo;里将显示IE浏览器的图标，与此同时&ldquo;favicon.ico&rdquo;不存在的信息（404 not found）会写到你的apache2错误日志中去，这样你可以从这个日志中看出，什么时候，什么人（其IP网址）将你的网站设定为&ldquo;my favorite&rdquo;。</p>
<p>解决的方法：</p>
<p>1、做个favicon.ico文件放在根目录下，在head标签引入favicon.ico文件即可</p>
<pre class=""language-markup""><code>&lt;link href=""favicon.ico"" rel=""shortcut icon""&gt;</code></pre>
<p>2、在Stack Overflow搜索到的，直接在head标签插入以下代码也OK</p>
<pre class=""language-markup""><code>&lt;link rel=""shortcut icon"" href=""#"" /&gt;</code></pre>
<p>&nbsp;</p>
