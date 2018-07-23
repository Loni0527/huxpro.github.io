---
layout:     post
title:      "json.decoder.JSONDecodeError"
subtitle:   ""
date:       2018-03-31 
author:     "Loni"
header-img: "img/post-bg-e2e-ux.jpg"
tags:
    - Python
    - Json
---


<p>在Python中用代码：</p>
<div>
<div id=""highlighter_77440"" class=""syntaxhighlighter notranslate py"">
<div class=""toolbar""><a class=""toolbar_item command_help help"" href=""https://www.crifan.com/fixed_problem_for_python_valueerror_no_json_object_could_be_decoded/"">?</a></div>
<table border=""0"" cellspacing=""0"" cellpadding=""0"">
<tbody>
<tr>
<td class=""gutter"">
<div class=""line number1 index0 alt2"">1</div>
<div class=""line number2 index1 alt1 highlighted"">2</div></td>
<td class=""code"">
<div class=""container"">
<div class=""line number1 index0 alt2""><code class=""py plain"">cfgFile&nbsp;</code><code class=""py keyword"">=</code> <code class=""py functions"">open</code><code class=""py plain"">(</code><code class=""py string"">'config.json'</code><code class=""py plain"">,</code><code class=""py string"">'r'</code><code class=""py plain"">);</code></div>
<div class=""line number2 index1 alt1 highlighted""><code class=""py plain"">jsonCfg&nbsp;</code><code class=""py keyword"">=</code> <code class=""py plain"">json.load(cfgFile);</code></div></div>
</td>
</tr>
</tbody>
</table>
</div>
</div>
<p>解析json，对应的config.json如下：</p>
<table border=""0"" width=""800"" cellspacing=""0"" cellpadding=""2"">
<tbody>
<tr>
<td valign=""top"" width=""800"">
<p>[<br /><br />[username,心情栖息地],</p>
<p>[password,123]</p>
<p>]</p>
</td>
</tr>
</tbody>
</table>
<p>但是结果出现&ldquo;No JSON object could be decoded&rdquo;错误：</p>
<table border=""0"" width=""800"" cellspacing=""0"" cellpadding=""2"">
<tbody>
<tr>
<td valign=""top"" width=""800"">
<p>LINE 2684 : ERROR Unknown Error !<br /><br />Traceback (most recent call last):</p>
<p>File ""D:\tmp\WordPress\Others\to_wp\BlogsToWordpress\HiBaiduToWordpress\HiBaiduToWordpress\HiBaiduToWordpress_v2012-03-12-office.py"", line 2682, in &lt;module&gt;</p>
<p>main()</p>
<p>File ""D:\tmp\WordPress\Others\to_wp\BlogsToWordpress\HiBaiduToWordpress\HiBaiduToWordpress\HiBaiduToWordpress_v2012-03-12-office.py"", line 2497, in main</p>
<p>jsonCfg = json.load(cfgFile);</p>
<p>File ""D:\tmp\WordPress\DevRoot\Python27\lib\json\__init__.py"", line 278, in load</p>
<p>**kw)</p>
<p>File ""D:\tmp\WordPress\DevRoot\Python27\lib\json\__init__.py"", line 326, in loads</p>
<p>return _default_decoder.decode(s)</p>
<p>File ""D:\tmp\WordPress\DevRoot\Python27\lib\json\decoder.py"", line 366, in decode</p>
<p>obj, end = self.raw_decode(s, idx=_w(s, 0).end())</p>
<p>File ""D:\tmp\WordPress\DevRoot\Python27\lib\json\decoder.py"", line 384, in raw_decode</p>
<p>raise ValueError(""No JSON object could be decoded"")</p>
<p>ValueError: No JSON object could be decoded</p>
</td>
</tr>
</tbody>
</table>
<p>【解决过程】</p>
<p>1.后来找了Python 2.7的手册看，函数的用法的对的啊，但是不知道为何此处错误，好像是json文件格式有问题。</p>
<p>2.网上找了下关于json的介绍资料：</p>
<p><a title="""" href=""http://zh.wikipedia.org/wiki/JSON"" data-original-title=""http://zh.wikipedia.org/wiki/JSON"">http://zh.wikipedia.org/wiki/JSON</a></p>
<p><a title="""" href=""http://www.json.org/json-zh.html"" data-original-title=""http://www.json.org/json-zh.html"">http://www.json.org/json-zh.html</a></p>
<p>然后去试了很多个：</p>
<p>{""username"":""心情栖息地""}</p>
<p>[username,心情栖息地]</p>
<p>结果都还是同样的错误。</p>
<p>然后又试了可用的示例：</p>
<table border=""0"" width=""800"" cellspacing=""0"" cellpadding=""2"">
<tbody>
<tr>
<td valign=""top"" width=""800"">
<p>{<br /><br />""firstName"": ""John"",</p>
<p>""lastName"": ""Smith"",</p>
<p>""male"": true,</p>
<p>""age"": 25,</p>
<p>""address"":</p>
<p>{</p>
<p>""streetAddress"": ""21 2nd Street"",</p>
<p>""city"": ""New York"",</p>
<p>""state"": ""NY"",</p>
<p>""postalCode"": ""10021""</p>
<p>},</p>
<p>""phoneNumber"":</p>
<p>[</p>
<p>{</p>
<p>""type"": ""home"",</p>
<p>""number"": ""212 555-1234""</p>
<p>},</p>
<p>{</p>
<p>""type"": ""fax"",</p>
<p>""number"": ""646 555-4567""</p>
<p>}</p>
<p>]</p>
<p>}</p>
</td>
</tr>
</tbody>
</table>
<p>结果还是不可以，那就说明此处代码有问题了。</p>
<p>3.网上找了N个关于此问题的解释，但是都没有解决我的问题。</p>
<p>4. 最后经过自己的折腾，经过N多次的尝试，终于解决了此问题：</p>
<p>此处的方法是，去config.json中，把此文本的编码，从之前的UTF-8转换为ANSI编码。</p>
<p>然后json.loads就可以识别，并转换为python对象了。</p>
<p>但是很是诡异的是，如果我没理解错的话，Python 2.7的手册中的：</p>
<blockquote>
<p>If the contents of&nbsp;<em>fp</em>&nbsp;are encoded with an ASCII based encoding other than UTF-8 (e.g. latin-1), then an appropriate&nbsp;<em>encoding</em>&nbsp;name must be specified. Encodings that are not ASCII based (such as UCS-2) are not allowed, and should be wrapped with&nbsp;<tt>codecs.getreader(encoding)(fp)</tt>, or simply decoded to a&nbsp;<a title="""" href=""mk:@MSITStore:D:%5Ctmp%5CWordPress%5CDevRoot%5CPython27%5CDoc%5Cpython272.chm::/library/functions.html#unicode"" data-original-title=""""><tt>unicode</tt></a>&nbsp;object and passed to&nbsp;<a title="""" href=""mk:@MSITStore:D:%5Ctmp%5CWordPress%5CDevRoot%5CPython27%5CDoc%5Cpython272.chm::/library/#json.loads"" data-original-title=""""><tt>loads()</tt></a>.</p></blockquote>
<p>意思是，如果你的编码不是以ANSI为基础的UTF-8的话，那么是需要手动指定对应的encoding的。</p>
<p>但是我此处的编码，就是特意设置为了UTF-8结果还是无法解码的，最后是手动把UTF-8改为ANSI编码，才成功的解码的。</p>
<p>而且更加诡异的是，我去把json文件编码转换为UTF-8，然后代码中用：</p>
<p>jsonCfg = json.loads(cfgData, encoding=""utf-8"");</p>
<p>竟然还是无法解码，还是出现上述的错误。</p>
<p>刚刚才发现，原来即使把json文件转换为UTF-8编码的话，那也一定要转换为：</p>
<p>&ldquo;无BOM的UTF-8格式&rdquo;</p>
<p><a title="""" href=""http://storage.live.com/items/9A8B8BF501A38A36!1117?filename=%e8%bd%ac%e4%b8%baUTF-8%e6%97%a0BOM%e7%bc%96%e7%a0%81%e6%a0%bc%e5%bc%8f.jpg"" data-original-title=""""><img title=""转为UTF-8无BOM编码格式"" src=""https://storage.live.com/items/9A8B8BF501A38A36!1117?filename=%e8%bd%ac%e4%b8%baUTF-8%e6%97%a0BOM%e7%bc%96%e7%a0%81%e6%a0%bc%e5%bc%8f.jpg"" alt=""转为UTF-8无BOM编码格式"" width=""588"" height=""331"" border=""0"" data-tag=""bdshare"" /></a></p>
<p>【总结】</p>
<p>Python中的Json库去解析对应的字符串的时候，即使是你保证了json字符串（或文件）是UTF-8，那么也未必就可以正确解码的，因为如果是在Windows下，那么默认是带BOM的UTF-8，此时Json库也是无法识别对应字符串的。</p>
<p>只有确保为无BOM的Json字符串，Python中的Json库，才可以正确解析的。</p>
<p>图说即为：</p>
<p><a title="""" href=""http://storage.live.com/items/9A8B8BF501A38A36!1118?filename=json%20decode%20not%20support%20BOM%20utf-8.jpg"" data-original-title=""""><img title=""json decode not support BOM utf-8"" src=""https://storage.live.com/items/9A8B8BF501A38A36!1118?filename=json%20decode%20not%20support%20BOM%20utf-8.jpg"" alt=""json decode not support BOM utf-8"" width=""1121"" height=""210"" border=""0"" data-tag=""bdshare"" /></a></p>
<p>【相关解释：默认的带BOM的UTF-8 和 无BOM的UTF-8的区别】</p>
<p>默认的UTF-8，是带BOM的，至少此处Notepad++的设置是这样的。</p>
<p>此处的代码，如果转为UTF-8。默认是带BOM的，即0xEF 0xBB 0xBF的：</p>
<p><a title="""" href=""http://storage.live.com/items/9A8B8BF501A38A36!1119?filename=with%20BOM%20UTF-8.jpg"" data-original-title=""""><img title=""with BOM UTF-8"" src=""https://storage.live.com/items/9A8B8BF501A38A36!1119?filename=with%20BOM%20UTF-8.jpg"" alt=""with BOM UTF-8"" width=""819"" height=""190"" border=""0"" data-tag=""bdshare"" /></a></p>
<p>而对应的无BOM的UTF-8的是不带0xEF 0xBB 0xBF的：</p>
<p><a title="""" href=""http://storage.live.com/items/9A8B8BF501A38A36!1120?filename=no%20BOM%20utf-8.jpg"" data-original-title=""""><img title=""no BOM utf-8"" src=""https://storage.live.com/items/9A8B8BF501A38A36!1120?filename=no%20BOM%20utf-8.jpg"" alt=""no BOM utf-8"" width=""819"" height=""195"" border=""0"" data-tag=""bdshare"" /></a></p>
<p>其中，windows下，对于UTF-8编码，一般默认都是带BOM的，所以开头会有个0xEF 0xBB 0xBF的。这点需要额外注意的。</p>
