在Python中用代码：

<a>?</a>

| 1 2 | `cfgFile ``=` `open``(``'config.json'``,``'r'``);` `jsonCfg ``=` `json.load(cfgFile);` |

解析json，对应的config.json如下：

| [

[username,心情栖息地], [password,123] ] |

但是结果出现“No JSON object could be decoded”错误：

| LINE 2684 : ERROR Unknown Error !

Traceback (most recent call last): File ""D:\tmp\WordPress\Others\to_wp\BlogsToWordpress\HiBaiduToWordpress\HiBaiduToWordpress\HiBaiduToWordpress_v2012-03-12-office.py"", line 2682, in <module> main() File ""D:\tmp\WordPress\Others\to_wp\BlogsToWordpress\HiBaiduToWordpress\HiBaiduToWordpress\HiBaiduToWordpress_v2012-03-12-office.py"", line 2497, in main jsonCfg = json.load(cfgFile); File ""D:\tmp\WordPress\DevRoot\Python27\lib\json\__init__.py"", line 278, in load **kw) File ""D:\tmp\WordPress\DevRoot\Python27\lib\json\__init__.py"", line 326, in loads return _default_decoder.decode(s) File ""D:\tmp\WordPress\DevRoot\Python27\lib\json\decoder.py"", line 366, in decode obj, end = self.raw_decode(s, idx=_w(s, 0).end()) File ""D:\tmp\WordPress\DevRoot\Python27\lib\json\decoder.py"", line 384, in raw_decode raise ValueError(""No JSON object could be decoded"") ValueError: No JSON object could be decoded |

【解决过程】

1.后来找了Python 2.7的手册看，函数的用法的对的啊，但是不知道为何此处错误，好像是json文件格式有问题。

2.网上找了下关于json的介绍资料：

<a>http://zh.wikipedia.org/wiki/JSON</a>

<a>http://www.json.org/json-zh.html</a>

然后去试了很多个：

{""username"":""心情栖息地""}

[username,心情栖息地]

结果都还是同样的错误。

然后又试了可用的示例：

| {

""firstName"": ""John"", ""lastName"": ""Smith"", ""male"": true, ""age"": 25, ""address"": { ""streetAddress"": ""21 2nd Street"", ""city"": ""New York"", ""state"": ""NY"", ""postalCode"": ""10021"" }, ""phoneNumber"": [ { ""type"": ""home"", ""number"": ""212 555-1234"" }, { ""type"": ""fax"", ""number"": ""646 555-4567"" } ] } |

结果还是不可以，那就说明此处代码有问题了。

3.网上找了N个关于此问题的解释，但是都没有解决我的问题。

4\. 最后经过自己的折腾，经过N多次的尝试，终于解决了此问题：

此处的方法是，去config.json中，把此文本的编码，从之前的UTF-8转换为ANSI编码。

然后json.loads就可以识别，并转换为python对象了。

但是很是诡异的是，如果我没理解错的话，Python 2.7的手册中的：

> 
> 
> If the contents of _fp_ are encoded with an ASCII based encoding other than UTF-8 (e.g. latin-1), then an appropriate _encoding_ name must be specified. Encodings that are not ASCII based (such as UCS-2) are not allowed, and should be wrapped with <tt>codecs.getreader(encoding)(fp)</tt>, or simply decoded to a <a><tt>unicode</tt></a> object and passed to <a><tt>loads()</tt></a>.
> 
> 

意思是，如果你的编码不是以ANSI为基础的UTF-8的话，那么是需要手动指定对应的encoding的。

但是我此处的编码，就是特意设置为了UTF-8结果还是无法解码的，最后是手动把UTF-8改为ANSI编码，才成功的解码的。

而且更加诡异的是，我去把json文件编码转换为UTF-8，然后代码中用：

jsonCfg = json.loads(cfgData, encoding=""utf-8"");

竟然还是无法解码，还是出现上述的错误。

刚刚才发现，原来即使把json文件转换为UTF-8编码的话，那也一定要转换为：

“无BOM的UTF-8格式”

<a></a>

【总结】

Python中的Json库去解析对应的字符串的时候，即使是你保证了json字符串（或文件）是UTF-8，那么也未必就可以正确解码的，因为如果是在Windows下，那么默认是带BOM的UTF-8，此时Json库也是无法识别对应字符串的。

只有确保为无BOM的Json字符串，Python中的Json库，才可以正确解析的。

图说即为：

<a></a>

【相关解释：默认的带BOM的UTF-8 和 无BOM的UTF-8的区别】

默认的UTF-8，是带BOM的，至少此处Notepad++的设置是这样的。

此处的代码，如果转为UTF-8。默认是带BOM的，即0xEF 0xBB 0xBF的：

<a></a>

而对应的无BOM的UTF-8的是不带0xEF 0xBB 0xBF的：

<a></a>

其中，windows下，对于UTF-8编码，一般默认都是带BOM的，所以开头会有个0xEF 0xBB 0xBF的。这点需要额外注意的。