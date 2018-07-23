---
layout:     keynote
title:      "Python 内建函数大全"
subtitle:   ""
iframe:     "//huangxuan.me/pwa-in-my-pov/"
navcolor:   "invert"
date:       2018-06-05
author:     "Loni"
tags:
    - Python
    - 随手记
---


<div>
<div>
<p>Python 解释器内置了许多函数和类型，列表如下（按字母排序）（省略了几个我没用过或者不常用的）。</p>
<table>
<thead>
<tr>
<th>-</th>
<th>-</th>
<th>内建函数表</th>
<th>-</th>
<th>-</th></tr>
</thead>
<tbody>
<tr>
<td>abs()</td>
<td>delattr()</td>
<td>hash()</td>
<td>memoryview()</td>
<td>set()</td></tr>
<tr>
<td>all()</td>
<td>dict()</td>
<td>help()</td>
<td>min()</td>
<td>setattr()</td></tr>
<tr>
<td>any()</td>
<td>dir()</td>
<td>hex()</td>
<td>next()</td>
<td>slice()</td></tr>
<tr>
<td>ascii()</td>
<td>divmod()</td>
<td>id()</td>
<td>object()</td>
<td>sorted()</td></tr>
<tr>
<td>bin()</td>
<td>enumerate()</td>
<td>input()</td>
<td>oct()</td>
<td>staticmethod()</td></tr>
<tr>
<td>bool()</td>
<td>eval()</td>
<td>int()</td>
<td>open()</td>
<td>str()</td></tr>
<tr>
<td>breakpoint()</td>
<td>exec()</td>
<td>isinstance()</td>
<td>ord()</td>
<td>sum()</td></tr>
<tr>
<td>bytearray()</td>
<td>filter()</td>
<td>issubclass()</td>
<td>pow()</td>
<td>super()</td></tr>
<tr>
<td>bytes()</td>
<td>float()</td>
<td>iter()</td>
<td>print()</td>
<td>tuple()</td></tr>
<tr>
<td>callable()</td>
<td>format()</td>
<td>len()</td>
<td>property()</td>
<td>type()</td></tr>
<tr>
<td>chr()</td>
<td>frozenset()</td>
<td>list()</td>
<td>range()</td>
<td>vars()</td></tr>
<tr>
<td>classmethod()</td>
<td>getattr()</td>
<td>locals()</td>
<td>repr()</td>
<td>zip()</td></tr>
<tr>
<td>compile()</td>
<td>globals()</td>
<td>map()</td>
<td>reversed()</td>
<td><code>__import__()</code></td></tr>
<tr>
<td>complex()</td>
<td>hasattr()</td>
<td>max()</td>
<td>round()</td>
<td>&nbsp;</td></tr>
</tbody>
</table>
<h2 class=""heading"" data-id=""heading-0"">abs(<em>x</em>)</h2>
<p>返回一个数字的绝对值。参数可以是整数或浮点数。如果参数是一个复数，则返回它的模。</p>
<h2 class=""heading"" data-id=""heading-1"">all(<em>iterable</em>)</h2>
<p>如果 <code>iterable</code> 的所有元素均为 True（或 <code>iterable</code> 为空），则返回 <code>True</code>。相当于：</p>
<pre class=""language-python""><code>def all(iterable):
    for element in iterable:
        if not element:
            return False
    return True</code></pre>
<h2 class=""heading"" data-id=""heading-2"">any(<em>iterable</em>)</h2>
<p>如果 <code>iterable</code> 中有任何一个元素为 true，则返回 <code>True</code>。如果 <code>iterable</code> 为空，则返回 <code>False</code>。相当于：</p>
<pre class=""language-python""><code>def any(iterable):
    for element in iterable:
        if element:
            return True
    return False</code></pre>
<h2 class=""heading"" data-id=""heading-3"">ascii(<em>object</em>)</h2>
<p>类似 <code>repr()</code>，返回一个包含对象的可打印表示的字符串，但使用 <code>\x</code>，<code>\u</code> 或 <code>\U</code> 转义符转义由 <code>repr()</code> 返回的字符串中的非 ASCII 字符。这会生成一个类似于 Python 2 中 <code>repr()</code> 返回的字符串。</p>
<pre class=""language-python""><code>In [1]: s = 'python \n 中文'

In [2]: ascii(s)
Out[2]: ""'python \\n \\u4e2d\\u6587'""

In [3]: repr(s)
Out[3]: ""'python \\n 中文'""</code></pre>
<h2 class=""heading"" data-id=""heading-4"">bin(<em>x</em>)</h2>
<p>将整数转换为以 &ldquo;0b&rdquo; 为前缀的二进制字符串。结果是一个有效的 Python 表达式。如果 <code>x</code> 不是Python <code>int</code> 对象，则必须定义返回整数的 <code>__index __()</code> 方法。一些例子：</p>
<pre class=""language-python""><code>&gt;&gt;&gt; bin(3)
'0b11'
&gt;&gt;&gt; bin(-10)
'-0b1010'</code></pre>
<p>可以使用以下任意方式，控制是否需要前缀 &ldquo;0b&rdquo;：</p>
<pre class=""language-python""><code>&gt;&gt;&gt; format(14, '#b'), format(14, 'b')
('0b1110', '1110')
&gt;&gt;&gt; f'{14:#b}', f'{14:b}'
('0b1110', '1110')</code></pre>
<p>有关更多信息，另请参阅 <code>format()</code>。</p>
<p>当 <code>x</code> 不是 <code>int</code> 类型时</p>
<pre class=""language-python""><code>In [1]: class Test:
   ...:     def __init__(self, n):
   ...:         self.n = n
   ...:
   ...:     def __index__(self):
   ...:         return self.n
   ...:

In [2]: t = Test(10)

In [3]: bin(t)
Out[3]: '0b1010'</code></pre>
<h2 class=""heading"" data-id=""heading-5""><em>class</em> bool([<em>x</em>])</h2>
<p>返回一个布尔值，即 <code>True</code> 或 <code>False</code> 中的一个。 x 使用标准<a href=""https://link.juejin.im?target=https%3A%2F%2Fdocs.python.org%2F3.7%2Flibrary%2Fstdtypes.html%23truth"" target=""_blank"" rel=""nofollow noopener noreferrer"">真值测试方式</a>进行转换。如果 x 为 false 或省略，则返回 <code>False</code>; 否则返回 <code>True</code>。 bool 类是 <code>int</code> 的子类。它不能进一步子类化。它唯一的实例是 <code>False</code> 和 <code>True</code>。</p>
<h2 class=""heading"" data-id=""heading-6"">class bytearray([<em>source</em>[, <em>encoding</em>[, <em>errors</em>]]])</h2>
<p>返回一个新的字节数组。 bytearray 类是一个在 <code>0 &lt;= x &lt; 256</code> 范围内的可变整数序列。</p>
<p>可选的 <code>source</code> 参数可以用几种不同的方式初始化数组：</p>
<ul>
<li>如果它是一个字符串，则还必须给出 encoding（以及可选的 errors）参数; 然后 <code>bytearray()</code> 使用 <code>str.encode()</code> 将字符串转换为字节。</li>
<li>如果它是一个整数，则将其作为数组的长度，并将用空字节进行初始化。</li>
<li>如果它是符合缓冲区接口的对象，则将使用该对象的只读缓冲区来初始化字节数组。</li>
<li>如果它是一个 iterable，必须是 <code>0 &lt;= x &lt;256</code> 范围内的可迭代对象，它们将被用作数组的初始内容。</li></ul>
<p>没有参数，就会创建一个大小为 0 的数组。</p>
<pre class=""language-python""><code>In [11]: bytearray(5)
Out[11]: bytearray(b'\x00\x00\x00\x00\x00')

In [12]: bytearray([23, 32, 4, 67, 9, 96, 123])
Out[12]: bytearray(b'\x17 \x04C\t`{')

In [13]: bytearray()
Out[13]: bytearray(b'')</code></pre>
<h2 class=""heading"" data-id=""heading-7"">class bytes([<em>source</em>[, <em>encoding</em>[, <em>errors</em>]]])</h2>
<p>返回一个新的 &ldquo;bytes&rdquo; 对象，它是一个在 <code>0 &lt;= x &lt;256</code> 范围内的不可变整数序列。<code>bytes</code> 是 <code>bytearray</code> 的不可变版本 - 它具有相同的非变异方法和相同的索引和切片行为。</p>
<p>因此，构造函数参数解释请参考 <code>bytearray()</code>。</p>
<p>字节对象也可以使用文字创建。请参阅<a href=""https://link.juejin.im?target=https%3A%2F%2Fdocs.python.org%2F3.7%2Freference%2Flexical_analysis.html%23strings"" target=""_blank"" rel=""nofollow noopener noreferrer"">字符串和字节文字</a>。</p>
<h2 class=""heading"" data-id=""heading-8"">callable(<em>object</em>)</h2>
<p>如果 object 参数可调用，则返回 <code>True</code>，否则返回 <code>False</code>。如果返回 true，调用失败仍然是可能的，但如果是 false，调用 object 将永远不会成功。请注意，类是可调用的（调用一个类返回一个新的实例）; 如果类有一个 <code>__call __()</code>方法，则实例可以被调用。</p>
<p>3.2版本中的新功能：此功能在 Python 3.0 中首先被删除，然后在 Python 3.2 中恢复。</p>
<pre class=""language-python""><code>In [19]: a = 1

In [20]: callable(a)
Out[20]: False

In [21]: def func():
    ...:     pass
    ...:

In [22]: callable(func)
Out[22]: True

In [23]: class A:
    ...:     pass
    ...:

In [24]: a = A()

In [25]: callable(a)
Out[25]: False

In [26]: class A:
    ...:     def __call__(self, *args, **kwargs):
    ...:         pass
    ...:

In [27]: a = A()

In [28]: callable(a)
Out[28]: True</code></pre>
<h2 class=""heading"" data-id=""heading-9"">chr(<em>i</em>)</h2>
<p>返回表示 Unicode 代码点为整数 i 的字符的字符串。例如，<code>chr(97)</code> 返回字符串 <code>'a'</code>，而 <code>chr(8364)</code> 返回字符串 <code>'&euro;'</code>。这是 <code>ord()</code> 的逆过程。</p>
<p>参数的有效范围是从 0 到 1,114,111（基于 16 的 0x10FFFF）。如果超出这个范围，将会抛出 ValueError。</p>
<h2 class=""heading"" data-id=""heading-10"">@classmethod</h2>
<p>将方法转换为类方法。</p>
<p>类方法将类作为第一个参数接收（隐式的），就像实例方法接收实例一样。为了声明一个类方法，习惯用法如下：</p>
<pre><code class=""hljs python"" lang=""python""><span class=""hljs-class""><span class=""hljs-keyword"">class</span> <span class=""hljs-title"">C</span>:</span>
<span class=""hljs-meta"">    @classmethod</span>
    <span class=""hljs-function""><span class=""hljs-keyword"">def</span> <span class=""hljs-title"">f</span><span class=""hljs-params"">(cls, arg1, arg2, ...)</span>:</span> ...
</code></pre>
<p>!&gt; 注意：类方法和静态方法不是一个概念</p>
<h2 class=""heading"" data-id=""heading-11"">class complex([<em>real</em>[, <em>imag</em>]])</h2>
<p>返回值为 real + imag*1j 的复数或者将字符串或数字转换为复数。如果第一个参数是一个字符串，它将被解释为一个复数，并且该函数必须在没有第二个参数的情况下被调用。第二个参数不能是一个字符串。每个参数可以是任何数字类型（包括复数）。如果省略了 imag，它将默认为零，并且构造函数用作像 int 和 float 这样的数字转换。如果两个参数均被省略，则返回 0j。</p>
<p>!&gt; 从字符串转换时，该字符串不得在 <code>+</code> 或 <code>-</code> 运算符周围包含空格。例如，<code>complex('1+2j')</code> 很好，但 <code>complex('1 + 2j')</code> 会引发 <code>ValueError</code>。</p>
<h2 class=""heading"" data-id=""heading-12"">delattr(object, name)</h2>
<p>参数是一个对象和一个字符串。该字符串必须是对象属性之一的名称。该函数删除指定的属性（只要该对象允许）。例如， <code>delattr(x, 'foobar')</code> 等价于 <code>del x.foobar</code>。</p>
<h2 class=""heading"" data-id=""heading-13"">dict</h2>
<p>class dict(<code>**kwarg</code>)<br /> class dict(<code>mapping</code>, <code>**kwarg</code>)<br /> class dict(<code>iterable</code>, <code>**kwarg</code>)</p>
<p>创建一个新的字典</p>
<pre><code class=""hljs python"" lang=""python"">In [<span class=""hljs-number"">38</span>]: dict(name=<span class=""hljs-string"">'jack'</span>,age=<span class=""hljs-number"">18</span>)
Out[<span class=""hljs-number"">38</span>]: {<span class=""hljs-string"">'name'</span>: <span class=""hljs-string"">'jack'</span>, <span class=""hljs-string"">'age'</span>: <span class=""hljs-number"">18</span>}

In [<span class=""hljs-number"">39</span>]: dict({<span class=""hljs-string"">'name'</span>: <span class=""hljs-string"">'jack'</span>}, age=<span class=""hljs-number"">18</span>)
Out[<span class=""hljs-number"">39</span>]: {<span class=""hljs-string"">'name'</span>: <span class=""hljs-string"">'jack'</span>, <span class=""hljs-string"">'age'</span>: <span class=""hljs-number"">18</span>}

In [<span class=""hljs-number"">40</span>]: dict([(<span class=""hljs-string"">'name'</span>, <span class=""hljs-string"">'jack'</span>),(<span class=""hljs-string"">'age'</span>, <span class=""hljs-number"">18</span>)])
Out[<span class=""hljs-number"">40</span>]: {<span class=""hljs-string"">'name'</span>: <span class=""hljs-string"">'jack'</span>, <span class=""hljs-string"">'age'</span>: <span class=""hljs-number"">18</span>}
</code></pre>
<h2 class=""heading"" data-id=""heading-14"">dir([<em>object</em>])</h2>
<p>尝试返回 object 的有效属性列表。如果没有参数，则返回当前本地作用域中的名称列表。</p>
<p>如果对象具有名为 <code>__dir__()</code> 的方法，则将调用此方法，并且必须返回属性列表。这允许实现自定义 <code>__getattr__()</code>或 <code>__getattribute__()</code> 函数的对象自定义 <code>dir()</code> 报告其属性。</p>
<p>默认的 <code>dir()</code> 机制对不同类型的对象有不同的表现，因为它试图产生最相关的信息，而不是完整的信息：</p>
<ul>
<li>如果对象是模块对象，则列表包含模块属性的名称。</li>
<li>如果对象是一个类型或类对象，则该列表包含其属性的名称，并递归地显示其基础的属性。</li>
<li>否则，该列表包含对象的属性名称，其类属性的名称以及其类的基类的属性的递归。</li></ul>
<p>结果列表按字母顺序排序。例如：</p>
<pre><code class=""hljs python"" lang=""python""><span class=""hljs-meta"">&gt;&gt;&gt; </span><span class=""hljs-keyword"">import</span> struct
<span class=""hljs-meta"">&gt;&gt;&gt; </span>dir()   <span class=""hljs-comment""># show the names in the module namespace  </span>
[<span class=""hljs-string"">'__builtins__'</span>, <span class=""hljs-string"">'__name__'</span>, <span class=""hljs-string"">'struct'</span>]
<span class=""hljs-meta"">&gt;&gt;&gt; </span>dir(struct)   <span class=""hljs-comment""># show the names in the struct module </span>
[<span class=""hljs-string"">'Struct'</span>, <span class=""hljs-string"">'__all__'</span>, <span class=""hljs-string"">'__builtins__'</span>, <span class=""hljs-string"">'__cached__'</span>, <span class=""hljs-string"">'__doc__'</span>, <span class=""hljs-string"">'__file__'</span>,
 <span class=""hljs-string"">'__initializing__'</span>, <span class=""hljs-string"">'__loader__'</span>, <span class=""hljs-string"">'__name__'</span>, <span class=""hljs-string"">'__package__'</span>,
 <span class=""hljs-string"">'_clearcache'</span>, <span class=""hljs-string"">'calcsize'</span>, <span class=""hljs-string"">'error'</span>, <span class=""hljs-string"">'pack'</span>, <span class=""hljs-string"">'pack_into'</span>,
 <span class=""hljs-string"">'unpack'</span>, <span class=""hljs-string"">'unpack_from'</span>]
<span class=""hljs-meta"">&gt;&gt;&gt; </span><span class=""hljs-class""><span class=""hljs-keyword"">class</span> <span class=""hljs-title"">Shape</span>:</span>
<span class=""hljs-meta"">... </span>    <span class=""hljs-function""><span class=""hljs-keyword"">def</span> <span class=""hljs-title"">__dir__</span><span class=""hljs-params"">(self)</span>:</span>
<span class=""hljs-meta"">... </span>        <span class=""hljs-keyword"">return</span> [<span class=""hljs-string"">'area'</span>, <span class=""hljs-string"">'perimeter'</span>, <span class=""hljs-string"">'location'</span>]
<span class=""hljs-meta"">&gt;&gt;&gt; </span>s = Shape()
<span class=""hljs-meta"">&gt;&gt;&gt; </span>dir(s)
[<span class=""hljs-string"">'area'</span>, <span class=""hljs-string"">'location'</span>, <span class=""hljs-string"">'perimeter'</span>]
</code></pre>
<h2 class=""heading"" data-id=""heading-15"">divmod(<em>a</em>, <em>b</em>)</h2>
<p>以两个（非复数）数字作为参数，并在使用整数除法时返回由它们的商和余数组成的一对数字。使用混合操作数类型时，适用二元算术运算符的规则。对于整数，结果与 <code>(a // b, a % b)</code> 相同。对于浮点数，结果是 <code>(q, a % b)</code>，其中 q 通常是 <code>math.floor(a / b)</code>，但可能小于 1。在任何情况下， <code>q * b + a % b</code> 都非常接近 a，如果 <code>a % b</code> 不为零，则它具有与 b 相同的符号，并且 <code>0 &lt;= abs(a % b) &lt; abs(b)</code>。</p>
<pre><code class=""hljs python"" lang=""python"">In [<span class=""hljs-number"">53</span>]: divmod(<span class=""hljs-number"">10</span>, <span class=""hljs-number"">3</span>)
Out[<span class=""hljs-number"">53</span>]: (<span class=""hljs-number"">3</span>, <span class=""hljs-number"">1</span>)

In [<span class=""hljs-number"">54</span>]: divmod(<span class=""hljs-number"">10.1</span>, <span class=""hljs-number"">3</span>)
Out[<span class=""hljs-number"">54</span>]: (<span class=""hljs-number"">3.0</span>, <span class=""hljs-number"">1.0999999999999996</span>)
</code></pre>
<h2 class=""heading"" data-id=""heading-16"">enumerate( <em>iterable</em>, <em>start=0</em>)</h2>
<p>返回一个枚举对象。 iterable 必须是一个序列，一个迭代器或其他支持迭代的对象。由 <code>enumerate()</code> 返回的迭代器的 <code>__next__()</code> 方法返回一个元组，该元组包含一个计数（从 start 开始，默认值为 0）以及遍历迭代获得的值。</p>
<pre><code class=""hljs python"" lang=""python""><span class=""hljs-meta"">&gt;&gt;&gt; </span>seasons = [<span class=""hljs-string"">'Spring'</span>, <span class=""hljs-string"">'Summer'</span>, <span class=""hljs-string"">'Fall'</span>, <span class=""hljs-string"">'Winter'</span>]
<span class=""hljs-meta"">&gt;&gt;&gt; </span>list(enumerate(seasons))
[(<span class=""hljs-number"">0</span>, <span class=""hljs-string"">'Spring'</span>), (<span class=""hljs-number"">1</span>, <span class=""hljs-string"">'Summer'</span>), (<span class=""hljs-number"">2</span>, <span class=""hljs-string"">'Fall'</span>), (<span class=""hljs-number"">3</span>, <span class=""hljs-string"">'Winter'</span>)]
<span class=""hljs-meta"">&gt;&gt;&gt; </span>list(enumerate(seasons, start=<span class=""hljs-number"">1</span>))
[(<span class=""hljs-number"">1</span>, <span class=""hljs-string"">'Spring'</span>), (<span class=""hljs-number"">2</span>, <span class=""hljs-string"">'Summer'</span>), (<span class=""hljs-number"">3</span>, <span class=""hljs-string"">'Fall'</span>), (<span class=""hljs-number"">4</span>, <span class=""hljs-string"">'Winter'</span>)]
</code></pre>
<p>相当于：</p>
<pre><code class=""hljs python"" lang=""python""><span class=""hljs-function""><span class=""hljs-keyword"">def</span> <span class=""hljs-title"">enumerate</span><span class=""hljs-params"">(sequence, start=<span class=""hljs-number"">0</span>)</span>:</span>
    n = start
    <span class=""hljs-keyword"">for</span> elem <span class=""hljs-keyword"">in</span> sequence:
        <span class=""hljs-keyword"">yield</span> n, elem
        n += <span class=""hljs-number"">1</span></code></pre>
<h2 class=""heading"" data-id=""heading-17"">filter(<em>function, iterable</em>)</h2>
<p>用那些 function 返回 true 的 iterable 元素构造一个迭代器。iterable 可以是序列，支持迭代的容器或迭代器。如果 function 为 <code>None</code>，则假定标识函数为 false，即为 false 的所有元素都被删除。</p>
<p>!&gt; 请注意，如果 function 不是 <code>None</code> ，<code>filter(function, iterable)</code> 等价于生成器表达式 <code>(item for item in iterable if function(item))</code> 。如果 function 是 <code>None</code>，等价于生成器表达式 <code>(item for item in iterable if item)</code> 。</p>
<pre><code class=""hljs python"" lang=""python"">In [<span class=""hljs-number"">8</span>]: list(filter(<span class=""hljs-keyword"">None</span>, [<span class=""hljs-keyword"">False</span>, <span class=""hljs-keyword"">True</span>, <span class=""hljs-number"">0</span>, <span class=""hljs-string"">'test'</span>]))
Out[<span class=""hljs-number"">8</span>]: [<span class=""hljs-keyword"">True</span>, <span class=""hljs-string"">'test'</span>]
</code></pre>
<h2 class=""heading"" data-id=""heading-18""><em>class</em> float([<em>x</em>])</h2>
<p>返回一个由数字或字符串 x 构造的浮点数。</p>
<p>在删除前后空白字符后，输入必须符合以下语法：</p>
<pre><code class=""hljs python"" lang=""python"">sign           ::=  <span class=""hljs-string"">""+""</span> | <span class=""hljs-string"">""-""</span>
infinity       ::=  <span class=""hljs-string"">""Infinity""</span> | <span class=""hljs-string"">""inf""</span>
nan            ::=  <span class=""hljs-string"">""nan""</span>
numeric_value  ::=  floatnumber | infinity | nan
numeric_string ::=  [sign] numeric_value
</code></pre>
<p>对于一般的 Python 对象 x，<code>float(x)</code> 委托给 <code>x .__float__()</code>。</p>
<p>如果没有给出参数，则返回 0.0。</p>
<p>例子：</p>
<pre><code class=""hljs python"" lang=""python""><span class=""hljs-meta"">&gt;&gt;&gt; </span>float(<span class=""hljs-string"">'+1.23'</span>)
<span class=""hljs-number"">1.23</span>
<span class=""hljs-meta"">&gt;&gt;&gt; </span>float(<span class=""hljs-string"">'   -12345\n'</span>)
<span class=""hljs-number"">-12345.0</span>
<span class=""hljs-meta"">&gt;&gt;&gt; </span>float(<span class=""hljs-string"">'1e-003'</span>)
<span class=""hljs-number"">0.001</span>
<span class=""hljs-meta"">&gt;&gt;&gt; </span>float(<span class=""hljs-string"">'+1E6'</span>)
<span class=""hljs-number"">1000000.0</span>
<span class=""hljs-meta"">&gt;&gt;&gt; </span>float(<span class=""hljs-string"">'-Infinity'</span>)
-inf
</code></pre>
<h2 class=""heading"" data-id=""heading-19"">format(<em>value</em>[, <em>format_spec</em>])</h2>
<p>将值转换为 &ldquo;格式化&rdquo; 表示，由 format_spec 控制。 format_spec 的解释将取决于 value 参数的类型，不过，大多数内置类型都使用标准格式化语法：<a href=""https://link.juejin.im?target=https%3A%2F%2Fdocs.python.org%2F3.7%2Flibrary%2Fstring.html%23formatspec"" target=""_blank"" rel=""nofollow noopener noreferrer"">格式化规范迷你语言</a>。</p>
<p>默认 format_spec 是一个空字符串，通常与调用 str(value) 的效果相同。</p>
<p>对 <code>format(value, format_spec)</code> 的调用被转换为 <code>type(value).__format__(value, format_spec)</code>，它在搜索 value 的 <code>__format__()</code> 方法时绕过实例字典。如果方法搜索到达 object 并且 format_spec 非空，或者 format_spec 或返回值不是字符串，则会引发 TypeError 异常。</p>
<p>在 version 3.4 中：如果 format_spec 不是空字符串，则 <code>object().__format__(format_spec)</code> 会引发 <code>TypeError</code>。</p>
<h2 class=""heading"" data-id=""heading-20"">class frozenset([<em>iterable</em>])</h2>
<p>返回一个新的 frozenset 对象，可选地使用来自 iterable 的元素。 <code>frozenset</code> 是一个内置的类。</p>
<p><code>frozenset</code> 是不可变的，存在哈希值，它可以作为字典的 key，也可以作为其它集合的元素。一旦创建便不能更改，没有 add，remove 方法。</p>
<h2 class=""heading"" data-id=""heading-21"">getattr(<em>object</em>, <em>name</em>[, <em>default</em>])</h2>
<p>返回 object 的指定属性的值。name 必须是字符串。如果字符串是 object 属性之一的名称，则结果是该属性的值。例如，<code>getattr(x, 'foobar')</code> 等同于 <code>x.foobar</code>。如果指定的属性不存在，则返回默认值（如果提供），否则引发 <code>AttributeError</code>。</p>
<h2 class=""heading"" data-id=""heading-22"">globals()</h2>
<p>返回表示当前全局符号表的字典。它总是当前模块的字典（在函数或方法内部，它是定义它的模块，而不是从中调用它的模块）。</p>
<h2 class=""heading"" data-id=""heading-23"">hasattr(<em>object</em>, <em>name</em>)</h2>
<p>参数是一个对象和一个字符串。如果字符串是 object 属性之一的名称，则结果为 <code>True</code>，否则为 <code>False</code>。（这是通过调用 <code>getattr(object, name)</code> 并查看它是否引发 <code>AttributeError</code> 实现的。）</p>
<h2 class=""heading"" data-id=""heading-24"">hash(<em>object</em>)</h2>
<p>返回对象的散列值（如果有）。哈希值是整数。它们用于在字典查找期间快速比较字典键。比较相等的数值具有相同的散列值（即使它们具有不同的类型，就像 1 和 1.0 一样）。</p>
<p>!&gt; 对于具有自定义 <code>__hash__()</code> 方法的对象，请注意，<code>hash()</code> 会根据主机的位宽截断返回值。</p>
<pre><code class=""hljs python"" lang=""python"">In [<span class=""hljs-number"">1</span>]: <span class=""hljs-class""><span class=""hljs-keyword"">class</span> <span class=""hljs-title"">A</span>:</span>
   ...:     <span class=""hljs-function""><span class=""hljs-keyword"">def</span> <span class=""hljs-title"">__hash__</span><span class=""hljs-params"">(self)</span>:</span>
   ...:         <span class=""hljs-keyword"">return</span> <span class=""hljs-number"">111111111111111111111111111111111111111</span>
   ...:

In [<span class=""hljs-number"">2</span>]: a = A()

In [<span class=""hljs-number"">3</span>]: hash(a)
Out[<span class=""hljs-number"">3</span>]: <span class=""hljs-number"">1552656422630569496</span>

In [<span class=""hljs-number"">4</span>]: <span class=""hljs-class""><span class=""hljs-keyword"">class</span> <span class=""hljs-title"">A</span>:</span>
   ...:     <span class=""hljs-function""><span class=""hljs-keyword"">def</span> <span class=""hljs-title"">__hash__</span><span class=""hljs-params"">(self)</span>:</span>
   ...:         <span class=""hljs-keyword"">return</span> <span class=""hljs-number"">11111111111</span>
   ...:
   ...:

In [<span class=""hljs-number"">5</span>]: a = A()

In [<span class=""hljs-number"">6</span>]: hash(a)
Out[<span class=""hljs-number"">6</span>]: <span class=""hljs-number"">11111111111</span></code></pre>
<h2 class=""heading"" data-id=""heading-25"">help([<em>object</em>])</h2>
<p>调用内置的帮助系统。 （此功能用于交互式使用。）如果未提供参数，则交互式帮助系统将在解释器控制台上启动。如果参数是一个字符串，那么该字符串将被查找为模块，函数，类，方法，关键字或文档主题的名称，并在控制台上打印帮助页面。如果参数是任何其他类型的对象，则会生成对象上的帮助页面。</p>
<h2 class=""heading"" data-id=""heading-26"">hex(<em>x</em>)</h2>
<p>将整数转换为以 &ldquo;0x&rdquo; 为前缀的小写十六进制字符串。如果 x 不是 Python int 对象，则必须定义返回整数的 <code>__index __()</code> 方法。一些例子：</p>
<pre><code class=""hljs python"" lang=""python""><span class=""hljs-meta"">&gt;&gt;&gt; </span>hex(<span class=""hljs-number"">255</span>)
<span class=""hljs-string"">'0xff'</span>
<span class=""hljs-meta"">&gt;&gt;&gt; </span>hex(<span class=""hljs-number"">-42</span>)
<span class=""hljs-string"">'-0x2a'</span></code></pre>
<p>如果要将整数转换为带有前缀或不带前缀的大写或小写十六进制字符串，可以使用以下任一方式：</p>
<pre><code class=""hljs python"" lang=""python"">&gt;&gt;&gt; '%#x' % 255, '%x' % 255, '%X' % 255
('0xff', 'ff', 'FF')
&gt;&gt;&gt; format(255, '#x'), format(255, 'x'), format(255, 'X')
('0xff', 'ff', 'FF')
&gt;&gt;&gt; f'{255:#x}', f'{255:x}', f'{255:X}'
('0xff', 'ff', 'FF')
</code></pre>
<p>!&gt; 要获取浮点数的十六进制字符串表示形式，请使用 <code>float.hex()</code> 方法。</p>
<h2 class=""heading"" data-id=""heading-27"">id(<em>object</em>)</h2>
<p>返回一个对象的 &ldquo;identity&rdquo;。它是一个整数，它在其生命周期中保证对这个对象唯一且恒定。具有非重叠生命周期的两个对象可能具有相同的 id() 值。</p>
<p>CPython 实现细节：这是内存中对象的地址。</p>
<h2 class=""heading"" data-id=""heading-28"">input([<em>prompt</em>])</h2>
<p>如果 prompt 参数存在，则将其写入标准输出而没有尾随换行符。然后该函数从输入中读取一行，将其转换为一个字符串（剥离尾随的换行符），然后返回该行。读取 EOF 时，引发 EOFError。例：</p>
<pre><code class=""hljs python"" lang=""python"">&gt;&gt;&gt; s = input('--&gt; ')  
--&gt; Monty Python's Flying Circus
&gt;&gt;&gt; s  
""Monty Python's Flying Circus""
</code></pre>
<h2 class=""heading"" data-id=""heading-29"">int</h2>
<p>class int(x=0)<br /> class int(x, base=10)</p>
<p>返回一个由数字或字符串 x 构造的整数对象，如果没有给出参数，则返回 0。如果 x 不是数字，则返回 <code>x.__int__()</code>。</p>
<pre><code class=""hljs python"" lang=""python"">In [<span class=""hljs-number"">22</span>]: <span class=""hljs-class""><span class=""hljs-keyword"">class</span> <span class=""hljs-title"">A</span>:</span>
    ...:     <span class=""hljs-function""><span class=""hljs-keyword"">def</span> <span class=""hljs-title"">__int__</span><span class=""hljs-params"">(self)</span>:</span>
    ...:         <span class=""hljs-keyword"">return</span> <span class=""hljs-number"">10</span>
    ...:

In [<span class=""hljs-number"">23</span>]: a = A()

In [<span class=""hljs-number"">24</span>]: int(a)
Out[<span class=""hljs-number"">24</span>]: <span class=""hljs-number"">10</span></code></pre>
<p>如果 x 不是数字或给定了 base，那么 x 必须是一个 string， bytes 或 bytearray 实例，它表示以 base 为基数的整数文字。或者，文字可以在前面加上 <code>+</code>或 <code>-</code> （两者之间没有空格）。</p>
<pre><code class=""hljs python"" lang=""python"">In [25]: int('-10')
Out[25]: -10

In [26]: int('+10')
Out[26]: 10

In [27]: int('- 10')
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
&lt;ipython-input-27-a62cc7794a18&gt; in &lt;module&gt;()
----&gt; 1 int('- 10')

ValueError: invalid literal for int() with base 10: '- 10'

In [28]: int('1000',2)
Out[28]: 8

In [29]: int('ff',16)
Out[29]: 255
</code></pre>
<h2 class=""heading"" data-id=""heading-30"">isinstance(<em>object</em>, <em>classinfo</em>)</h2>
<p>如果 object 参数是 classinfo 参数的实例或其（直接，间接或虚拟）子类的实例，则返回 true。如果 object 不是给定类型的对象，则该函数总是返回 false。如果 classinfo 是类型对象的元组， object 是其中任何一个类型的实例，则返回 true。如果 classinfo 不是类型或一组类型的元组，则会引发 <code>TypeError</code> 异常。</p>
<pre><code class=""hljs python"" lang=""python"">In [<span class=""hljs-number"">30</span>]: isinstance(<span class=""hljs-number"">10</span>, int)
Out[<span class=""hljs-number"">30</span>]: <span class=""hljs-keyword"">True</span>

In [<span class=""hljs-number"">31</span>]: isinstance(<span class=""hljs-string"">""str""</span>, (int, str))
Out[<span class=""hljs-number"">31</span>]: <span class=""hljs-keyword"">True</span>

In [<span class=""hljs-number"">32</span>]: isinstance(max, int)
Out[<span class=""hljs-number"">32</span>]: <span class=""hljs-keyword"">False</span></code></pre>
<h2 class=""heading"" data-id=""heading-31"">issubclass(<em>class</em>, <em>classinfo</em>)</h2>
<p>如果 class 是 classinfo 的子类（直接，间接或虚拟），则返回 true。一个类被认为是它自己的一个子类。 classinfo 可以是类对象的元组，在这种情况下，将检查 classinfo 中的每个条目。在任何其他情况下，都会引发 <code>TypeError</code> 异常。</p>
<pre><code class=""hljs python"" lang=""python"">In [34]: issubclass(int, int)
Out[34]: True

In [35]: issubclass(10, int)
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
&lt;ipython-input-35-37910f193c07&gt; in &lt;module&gt;()
----&gt; 1 issubclass(10, int)

TypeError: issubclass() arg 1 must be a class

In [36]: issubclass(int, str)
Out[36]: False
</code></pre>
<h2 class=""heading"" data-id=""heading-32"">iter(<em>object</em>[, <em>sentinel</em>])</h2>
<p>返回一个迭代器对象。根据第二个参数是否存在，第一个参数的解释有所不同。如果没有第二个参数，object 必须是支持迭代协议（<code>__iter__()</code> 方法）的集合对象，或者它必须支持序列协议（整数参数从 0 开始的 <code>__getitem__()</code> 方法）。如果它不支持这两种协议，则会引发 <code>TypeError</code>。如果给出了第二个参数 sentinel，那么 object 必须是可调用的对象。在这种情况下创建的迭代器将调用没有参数的 object，以便对其 <code>__next__()</code> 方法进行调用；如果返回的值等于 sentinel，则会触发<code>StopIteration</code>，否则将返回该值。</p>
<p>第二种形式的 <code>iter()</code> 的一个例子是按行读取文件，直到到达某一行。以下示例读取文件，直到 <code>readline()</code> 方法返回空字符串：</p>
<pre><code class=""hljs python"" lang=""python""><span class=""hljs-keyword"">with</span> open(<span class=""hljs-string"">'mydata.txt'</span>) <span class=""hljs-keyword"">as</span> fp:
    <span class=""hljs-keyword"">for</span> line <span class=""hljs-keyword"">in</span> iter(fp.readline, <span class=""hljs-string"">''</span>):
        process_line(line)
</code></pre>
<h2 class=""heading"" data-id=""heading-33"">len(s)</h2>
<p>返回对象的长度（条目数量）。参数可以是一个序列（如 string，bytes，tuple，list 或 range）或集合（如字典，set 或 frozenset）。</p>
<p>也可用于实现了 <code>__len__()</code> 方法的任意对象</p>
<pre><code class=""hljs python"" lang=""python"">In [<span class=""hljs-number"">40</span>]: <span class=""hljs-class""><span class=""hljs-keyword"">class</span> <span class=""hljs-title"">A</span>:</span>
    ...:     <span class=""hljs-function""><span class=""hljs-keyword"">def</span> <span class=""hljs-title"">__len__</span><span class=""hljs-params"">(self)</span>:</span>
    ...:         <span class=""hljs-keyword"">return</span> <span class=""hljs-number"">10</span>
    
In [<span class=""hljs-number"">41</span>]: a = A()

In [<span class=""hljs-number"">42</span>]: len(a)
Out[<span class=""hljs-number"">42</span>]: <span class=""hljs-number"">10</span></code></pre>
<h2 class=""heading"" data-id=""heading-34"">class list([<em>iterable</em>])</h2>
<p>list 不是一个函数，它实际上是一个可变的序列类型。</p>
<h2 class=""heading"" data-id=""heading-35"">locals()</h2>
<p>更新并返回表示当前本地符号表的字典。在函数块中调用时，locals() 返回自由变量，但不能在类块中调用。</p>
<p>!&gt; 不应该修改其中的内容；更改可能不会影响解释器使用的本地变量和自由变量的值。</p>
<h2 class=""heading"" data-id=""heading-36"">map(function, iterable, ...)</h2>
<p>返回一个将 function 应用于每个 iterable item 的迭代器，从而产生结果。如果传递额外的 iterable 参数，function 必须采用多个参数并应用于并行所有迭代中的项目。使用多个迭代器时，当最短迭代器耗尽时，迭代器停止。</p>
<pre><code class=""hljs python"" lang=""python"">In [<span class=""hljs-number"">54</span>]: list1 = [<span class=""hljs-number"">1</span>, <span class=""hljs-number"">2</span>, <span class=""hljs-number"">3</span>, <span class=""hljs-number"">4</span>, <span class=""hljs-number"">5</span>, <span class=""hljs-number"">6</span>]
    ...: list2 = [<span class=""hljs-number"">4</span>, <span class=""hljs-number"">3</span>, <span class=""hljs-number"">7</span>, <span class=""hljs-number"">1</span>, <span class=""hljs-number"">9</span>]
    ...:

In [<span class=""hljs-number"">55</span>]: list(map(<span class=""hljs-keyword"">lambda</span> x, y: x+y, list1, list2))
Out[<span class=""hljs-number"">55</span>]: [<span class=""hljs-number"">5</span>, <span class=""hljs-number"">5</span>, <span class=""hljs-number"">10</span>, <span class=""hljs-number"">5</span>, <span class=""hljs-number"">14</span>]
</code></pre>
<h2 class=""heading"" data-id=""heading-37"">max</h2>
<p><code>max(iterable, *[, key, default])</code><br /> <code>max(arg1, arg2, *args[, key])</code></p>
<p>返回 iterable 中的最大项或两个或更多个参数中最大的项。</p>
<p>如果提供了一个位置参数，它应该是一个 iterable。iterable 中最大的 item 被返回。如果提供了两个或多个位置参数，则返回最大的位置参数。</p>
<p>有两个可选的关键字参数。 key 参数指定一个像 <code>list.sort()</code> 那样的单参数排序函数。如果提供的迭代器为空，则 default 参数指定要返回的对象。如果迭代器为空且未提供缺省值，则会引发 <code>ValueError</code>。</p>
<p>如果最大值包含多个 item，则该函数返回遇到的第一个 item。这与 <code>sorted(iterable, key=keyfunc, reverse=True)[0]</code> 和 <code>heapq.nlargest(1, iterable, key=keyfunc)</code> 等其他排序工具稳定性保持一致。</p>
<pre><code class=""hljs python"" lang=""python"">In [60]: list1 = [4, 3, 7, 1, 9]

In [61]: max(list1, key=lambda x: -x)
Out[61]: 1

In [62]: max([])
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
&lt;ipython-input-62-a48d8f8c12de&gt; in &lt;module&gt;()
----&gt; 1 max([])

ValueError: max() arg is an empty sequence

In [63]: max([], default=1)
Out[63]: 1
</code></pre>
<h2 class=""heading"" data-id=""heading-38"">min</h2>
<p><code>min(iterable, *[, key, default])</code><br /> <code>min(arg1, arg2, *args[, key])</code></p>
<p>返回 iterable 中的最小项或两个或更多个参数中的最小项。</p>
<p>如果提供了一个位置参数，它应该是一个 iterable。iterable 中的最小项被返回。如果提供两个或多个位置参数，则返回最小的位置参数。</p>
<p>有两个可选的关键字参数。 key 参数指定一个像 <code>list.sort()</code> 那样的单参数排序函数。如果提供的迭代器为空，则 default 参数指定要返回的对象。如果迭代器为空且未提供缺省值，则会引发 <code>ValueError</code>。</p>
<p>如果最小值包含多个 item，则该函数返回遇到的第一个 item。这与 <code>sorted(iterable, key=keyfunc, reverse=True)[0]</code> 和 <code>heapq.nlargest(1, iterable, key=keyfunc)</code> 等其他排序工具稳定性保持一致。</p>
<h2 class=""heading"" data-id=""heading-39"">next(<em>iterator</em>[, <em>default</em>])</h2>
<p>通过调用 <code>__next__()</code> 方法从 iterator 中检索下一个 item。如果给出了 default，则在迭代器耗尽时返回它，否则引发 <code>StopIteration</code>。</p>
<h2 class=""heading"" data-id=""heading-40"">class object</h2>
<p>返回一个新的无特征的对象。object 是所有类的基类。它具有所有 Python 类实例通用的方法。这个函数不接受任何参数。</p>
<p>!&gt; object 没有 <code>__dict__</code>，所以不能为 object 类的实例指定任意属性。</p>
<h2 class=""heading"" data-id=""heading-41"">oct(<em>x</em>)</h2>
<p>将整数转换为以 &ldquo;0o&rdquo; 为前缀的八进制字符串。结果是一个有效的 Python 表达式。如果 x 不是 Python int 对象，则必须定义返回整数的 <code>__index__()</code> 方法。例如：</p>
<pre><code class=""hljs python"" lang=""python""><span class=""hljs-meta"">&gt;&gt;&gt; </span>oct(<span class=""hljs-number"">8</span>)
<span class=""hljs-string"">'0o10'</span>
<span class=""hljs-meta"">&gt;&gt;&gt; </span>oct(<span class=""hljs-number"">-56</span>)
<span class=""hljs-string"">'-0o70'</span></code></pre>
<p>如果要将整数转换为八进制字符串，控制是否显示前缀 &ldquo;0o&rdquo;，则可以使用以下任一方式。</p>
<pre><code class=""hljs python"" lang=""python"">&gt;&gt;&gt; '%#o' % 10, '%o' % 10
('0o12', '12')
&gt;&gt;&gt; format(10, '#o'), format(10, 'o')
('0o12', '12')
&gt;&gt;&gt; f'{10:#o}', f'{10:o}'
('0o12', '12')
</code></pre>
<h2 class=""heading"" data-id=""heading-42"">open</h2>
<p><code>open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)</code></p>
<p>打开 file 并返回相应的文件对象。如果文件无法打开，则会引发 <code>OSError</code>。</p>
<p>file 是一个类似路径的对象，它提供要打开的文件的路径名（绝对或相对于当前工作目录）或要包装的文件的整数文件描述符。 （如果给出文件描述符，则在返回的 I/O 对象关闭时关闭，除非 closefd 设置为 <code>False</code>。）</p>
<p>mode 是一个可选字符串，用于指定打开文件的模式。它默认为 <code>'r'</code>，表示使用文本的方式打开文件来读取。其他常见的值是 <code>'w'</code> 用于写入（如果文件已经存在，则覆盖该文件），<code>'x'</code> 用于独占创建，<code>'a'</code> 用于附加（在某些 Unix 系统上，这意味着无论当前的搜索位置如何，所有写操作都会附加到文件末尾）。在文本模式下，如果未指定编码，则使用的编码与平台相关：调用 <code>locale.getpreferredencoding(False)</code> 以获取当前语言环境编码。（为了读取和写入原始字节，使用二进制模式并且不用指定编码）可用的模式有：</p>
<table>
<thead>
<tr>
<th>字符</th>
<th>含义</th></tr>
</thead>
<tbody>
<tr>
<td><code>'r'</code></td>
<td>用于读取（默认）</td></tr>
<tr>
<td><code>'w'</code></td>
<td>用于写入，首先覆盖文件</td></tr>
<tr>
<td><code>'x'</code></td>
<td>用于独占创建，如果文件已经存在则失败</td></tr>
<tr>
<td><code>'a'</code></td>
<td>用于写入，追加到文件末尾（如果存在）</td></tr>
<tr>
<td><code>'b'</code></td>
<td>二进制模式</td></tr>
<tr>
<td><code>'t'</code></td>
<td>文本模式（默认）</td></tr>
<tr>
<td><code>'+'</code></td>
<td>打开磁盘文件进行更新（读取和写入）</td></tr>
<tr>
<td><code>'U'</code></td>
<td>通用换行符模式（已弃用）</td></tr>
</tbody>
</table>
<p>默认模式是 <code>'r'</code>（用于读取文本，<code>'rt'</code> 的同义词）。对于二进制读写访问，模式 <code>'w+b'</code> 打开并将文件删减为 0 字节。 <code>'r+b'</code> 打开文件而不删减。</p>
<p>如概述中所述，Python 区分二进制和文本 I/O。以二进制模式打开的文件（mode参数中包括 <code>'b'</code>）将内容作为字节对象返回，而不进行任何解码。在文本模式下（默认情况下，或当 <code>'t'</code> 包含在 mode 参数中时），文件内容以 str 形式返回，字节首先使用平台相关编码进行解码，或者使用指定的编码（如果给出）。</p>
<p>!&gt; Python 不依赖于底层操作系统的文本文件概念；所有的处理都由 Python 自己完成，因此是平台无关的。</p>
<h2 class=""heading"" data-id=""heading-43"">ord(<em>c</em>)</h2>
<p>给定一个代表一个Unicode字符的字符串，返回一个表示该字符的 Unicode code 点的整数。例如，<code>ord('a')</code> 返回整数 97，<code>ord('&euro;')</code>（欧元符号）返回 8364。这是 <code>chr()</code> 的逆过程</p>
<h2 class=""heading"" data-id=""heading-44"">pow(<em>x</em>, <em>y</em>[, <em>z</em>])</h2>
<p>返回 x 的 y 次方；返回 x 的 y 次方再除以 z 的余数（计算效率比 <code>pow(x, y) % z</code> 更高）。双参数形式 <code>pow(x, y)</code> 等价于使用幂运算符：<code>x**y</code>。</p>
<h2 class=""heading"" data-id=""heading-45"">print</h2>
<p><code>print(*objects, sep=' ', end='\n', file=sys.stdout, flush=False)</code></p>
<p>将 objects 打印到文本流 file 中，以 sep 分隔，然后以 end 结尾。必须将 sep，end，file 和 flush（如果存在）作为关键字参数给出。</p>
<p>所有非关键字参数都会转换为像 <code>str()</code> 那样的字符串并写入流中，由 sep 隔开，然后结束。sep 和 end 都必须是字符串；它们也可以是 None，这意味着使用默认值。如果没有给出对象，<code>print()</code> 将只写入 end。</p>
<p>文件参数必须是带有 <code>write(string)</code> 方法的对象；如果它不存在或是 None，则将使用 <code>sys.stdout</code>。由于打印的参数会转换为文本字符串，<code>print()</code> 不能用于二进制模式文件对象。对于这些，请改用 <code>file.write(...)</code>。</p>
<p>输出是否缓冲通常由 file 决定，但如果 flush 关键字参数为 true，则强制刷新流。</p>
<h2 class=""heading"" data-id=""heading-46"">property</h2>
<p><code>class property(fget=None, fset=None, fdel=None, doc=None)</code></p>
<p>返回一个 property 属性。</p>
<p>fget 是获取属性值的函数。fset 是用于设置属性值的函数。fdel 是删除属性值时会调用的函数。doc 为该属性创建一个文档字符串。</p>
<p>典型的用法是定义一个托管属性 x：</p>
<pre><code class=""hljs python"" lang=""python""><span class=""hljs-class""><span class=""hljs-keyword"">class</span> <span class=""hljs-title"">C</span>:</span>
    <span class=""hljs-function""><span class=""hljs-keyword"">def</span> <span class=""hljs-title"">__init__</span><span class=""hljs-params"">(self)</span>:</span>
        self._x = <span class=""hljs-keyword"">None</span>

    <span class=""hljs-function""><span class=""hljs-keyword"">def</span> <span class=""hljs-title"">getx</span><span class=""hljs-params"">(self)</span>:</span>
        <span class=""hljs-keyword"">return</span> self._x

    <span class=""hljs-function""><span class=""hljs-keyword"">def</span> <span class=""hljs-title"">setx</span><span class=""hljs-params"">(self, value)</span>:</span>
        self._x = value

    <span class=""hljs-function""><span class=""hljs-keyword"">def</span> <span class=""hljs-title"">delx</span><span class=""hljs-params"">(self)</span>:</span>
        <span class=""hljs-keyword"">del</span> self._x

    x = property(getx, setx, delx, <span class=""hljs-string"">""I'm the 'x' property.""</span>)
</code></pre>
<p>如果 c 是 C 的一个实例，<code>c.x</code> 将调用 getx，<code>c.x = value</code> 将调用 setx ，<code>del c.x</code> 将调用 delx。</p>
<p>如果给定，doc 将是 property 属性的文档字符串。否则，该属性将复制 fget 的文档字符串（如果存在）。这使得使用 <code>property()</code>作为装饰器可以轻松创建只读属性：</p>
<pre><code class=""hljs python"" lang=""python""><span class=""hljs-class""><span class=""hljs-keyword"">class</span> <span class=""hljs-title"">Parrot</span>:</span>
    <span class=""hljs-function""><span class=""hljs-keyword"">def</span> <span class=""hljs-title"">__init__</span><span class=""hljs-params"">(self)</span>:</span>
        self._voltage = <span class=""hljs-number"">100000</span>

<span class=""hljs-meta"">    @property</span>
    <span class=""hljs-function""><span class=""hljs-keyword"">def</span> <span class=""hljs-title"">voltage</span><span class=""hljs-params"">(self)</span>:</span>
        <span class=""hljs-string"">""""""Get the current voltage.""""""</span>
        <span class=""hljs-keyword"">return</span> self._voltage
</code></pre>
<p><code>@property</code> 修饰器将 <code>voltage()</code> 方法转换为具有相同名称的只读属性的 &ldquo;getter&rdquo;，并将 voltage 的文档字符串设置为 <code>&ldquo;Get the current voltage.&rdquo;</code>。</p>
<p>property 对象具有可用作装饰器的 getter，setter 和 deleter 方法，这些方法创建属性的副本并将相应的存取器函数设置为装饰函数。这可以用一个例子来解释：</p>
<pre><code class=""hljs python"" lang=""python""><span class=""hljs-class""><span class=""hljs-keyword"">class</span> <span class=""hljs-title"">C</span>:</span>
    <span class=""hljs-function""><span class=""hljs-keyword"">def</span> <span class=""hljs-title"">__init__</span><span class=""hljs-params"">(self)</span>:</span>
        self._x = <span class=""hljs-keyword"">None</span>

<span class=""hljs-meta"">    @property</span>
    <span class=""hljs-function""><span class=""hljs-keyword"">def</span> <span class=""hljs-title"">x</span><span class=""hljs-params"">(self)</span>:</span>
        <span class=""hljs-string"">""""""I'm the 'x' property.""""""</span>
        <span class=""hljs-keyword"">return</span> self._x

<span class=""hljs-meta"">    @x.setter</span>
    <span class=""hljs-function""><span class=""hljs-keyword"">def</span> <span class=""hljs-title"">x</span><span class=""hljs-params"">(self, value)</span>:</span>
        self._x = value

<span class=""hljs-meta"">    @x.deleter</span>
    <span class=""hljs-function""><span class=""hljs-keyword"">def</span> <span class=""hljs-title"">x</span><span class=""hljs-params"">(self)</span>:</span>
        <span class=""hljs-keyword"">del</span> self._x
</code></pre>
<p>此代码与第一个示例完全等效。请务必为附加函数提供与原始 property 相同的名称（当前为 x）。</p>
<p>返回的 property 对象也具有与构造函数参数相对应的属性 fget，fset 和 fdel。</p>
<h2 class=""heading"" data-id=""heading-47"">range</h2>
<p><code>range(stop)</code><br /> <code>range(start, stop[, step])</code></p>
<p>range 不是一个函数，它实际上是一个不可变的序列类型</p>
<pre><code class=""hljs python"" lang=""python"">In [<span class=""hljs-number"">8</span>]: list(range(<span class=""hljs-number"">10</span>))
Out[<span class=""hljs-number"">8</span>]: [<span class=""hljs-number"">0</span>, <span class=""hljs-number"">1</span>, <span class=""hljs-number"">2</span>, <span class=""hljs-number"">3</span>, <span class=""hljs-number"">4</span>, <span class=""hljs-number"">5</span>, <span class=""hljs-number"">6</span>, <span class=""hljs-number"">7</span>, <span class=""hljs-number"">8</span>, <span class=""hljs-number"">9</span>]

In [<span class=""hljs-number"">9</span>]: list(range(<span class=""hljs-number"">0</span>, <span class=""hljs-number"">10</span>, <span class=""hljs-number"">2</span>))
Out[<span class=""hljs-number"">9</span>]: [<span class=""hljs-number"">0</span>, <span class=""hljs-number"">2</span>, <span class=""hljs-number"">4</span>, <span class=""hljs-number"">6</span>, <span class=""hljs-number"">8</span>]
</code></pre>
<h2 class=""heading"" data-id=""heading-48"">repr(<em>object</em>)</h2>
<p>返回一个包含对象可打印表示的字符串。对于许多类型，此函数尝试返回一个字符串，该字符串在传递给 <code>eval()</code> 时会产生一个具有相同值的对象，否则该表示是一个用尖括号括起来的字符串，其中包含对象类型的名称以及其他信息包括对象的名称和地址。一个类可以通过定义 <code>__repr__()</code> 方法来控制此函数为其实例返回的内容。</p>
<h2 class=""heading"" data-id=""heading-49"">reversed(<em>seq</em>)</h2>
<p>返回一个反向迭代器。seq 必须是具有 <code>__reversed__()</code> 方法或支持序列协议（ <code>__len__()</code> 方法和整数参数从 0 开始的 <code>__getitem__()</code> 方法）的对象。</p>
<h2 class=""heading"" data-id=""heading-50"">round(<em>number</em>[, <em>ndigits</em>])</h2>
<p>返回在小数点后舍入到精度 ndigits 的 number 。如果 ndigits 被省略或者是 <code>None</code>，它将返回最接近的整数表示。</p>
<p>对于支持 <code>round()</code> 的内建类型，值舍入到 10 的最接近的负 ndigits 次幂的倍数；如果离两个倍数的距离相等，则舍入选择偶数（因此，<code>round(0.5)</code> 和 <code>round(-0.5)</code> 都是 0，而 <code>round(1.5)</code> 是 2 ）。ndigits 可以是任何整数值（正数，零或负数）。如果使用一个参数调用则返回值是一个 integer，否则与 number 的类型相同。</p>
<pre><code class=""hljs python"" lang=""python"">In [<span class=""hljs-number"">10</span>]: type(round(<span class=""hljs-number"">10.9</span>))
Out[<span class=""hljs-number"">10</span>]: int

In [<span class=""hljs-number"">11</span>]: type(round(<span class=""hljs-number"">10.9</span>, <span class=""hljs-number"">2</span>))
Out[<span class=""hljs-number"">11</span>]: float
</code></pre>
<p>对于一般的 Python 对象 xxx，<code>round(xxx, ndigits)</code> 委托给 <code>xxx.__round__(ndigits)</code>。</p>
<p>!&gt; <code>round()</code> 对于浮点数的行为可能会令人惊讶：例如，<code>round(2.675, 2)</code> 给出 2.67，而不是预期的 2.68。这不是一个 bug：这是由于大多数小数不能完全表示为浮点数的结果。</p>
<h2 class=""heading"" data-id=""heading-51"">class set([<em>iterable</em>])</h2>
<p>返回一个新的集合对象，可选地使用来自 iterable 的元素。 set 是一个内置的类。</p>
<h2 class=""heading"" data-id=""heading-52"">setattr(<em>object, name, value</em>)</h2>
<p>它和 <code>getattr()</code> 是一对。参数是一个对象，一个字符串和一个任意值。该字符串可以是现有的属性名或新的属性名。如果该对象允许，该函数将 value 分配给该属性。例如，<code>setattr(x, 'foobar', 123)</code> 等同于 <code>x.foobar = 123</code>。</p>
<h2 class=""heading"" data-id=""heading-53"">slice</h2>
<p><code>class slice(stop)</code><br /> <code>class slice(start, stop[, step])</code></p>
<p>返回表示由 <code>range(start, stop, step)</code> 指定的一组索引的切片对象。start 和 step 参数默认为 <code>None</code>。切片对象具有只读数据属性 start、stop 和 step，它们只返回参数值（或它们的默认值）。他们没有其他明确的功能；然而，它们被 Numerical Python 和其他第三方扩展使用。当使用扩展索引语法时，也会生成切片对象。例如：<code>a[start:stop:step]</code> 或 <code>a[start:stop, i]</code>。</p>
<pre><code class=""hljs python"" lang=""python"">In [<span class=""hljs-number"">5</span>]: a = [<span class=""hljs-number"">0</span>, <span class=""hljs-number"">1</span>, <span class=""hljs-number"">2</span>, <span class=""hljs-number"">3</span>, <span class=""hljs-number"">4</span>, <span class=""hljs-number"">5</span>, <span class=""hljs-number"">6</span>, <span class=""hljs-number"">7</span>, <span class=""hljs-number"">8</span>, <span class=""hljs-number"">9</span>]

In [<span class=""hljs-number"">6</span>]: s = slice(<span class=""hljs-number"">1</span>, <span class=""hljs-number"">8</span>, <span class=""hljs-number"">2</span>)

In [<span class=""hljs-number"">7</span>]: a[s]
Out[<span class=""hljs-number"">7</span>]: [<span class=""hljs-number"">1</span>, <span class=""hljs-number"">3</span>, <span class=""hljs-number"">5</span>, <span class=""hljs-number"">7</span>]
</code></pre>
<h2 class=""heading"" data-id=""heading-54"">sorted</h2>
<p><code>sorted(iterable, *, key=None, reverse=False)</code></p>
<p>从 iterable 中的 item 中返回一个新的排序列表。</p>
<p>有两个可选参数，必须将其指定为关键字参数。</p>
<p>key 指定一个带有一个参数的函数，用于从每个列表元素中提取比较键：<code>key=str.lower</code>。默认值是 <code>None</code>（直接比较元素）。</p>
<p>reverse 是一个布尔值。如果设置为 <code>True</code>，那么列表元素按照每个比较被颠倒的顺序进行排序。</p>
<p>内置的 <code>sorted()</code> 函数排序是稳定的。如果确保不会更改比较相等的元素的相对顺序，则排序是稳定的 。</p>
<h2 class=""heading"" data-id=""heading-55"">@staticmethod</h2>
<p>将方法转换为静态方法。</p>
<p>静态方法不会收到隐式的第一个参数。要声明一个静态方法，习惯用法如下：</p>
<pre><code class=""hljs python"" lang=""python""><span class=""hljs-class""><span class=""hljs-keyword"">class</span> <span class=""hljs-title"">C</span>:</span>
<span class=""hljs-meta"">    @staticmethod</span>
    <span class=""hljs-function""><span class=""hljs-keyword"">def</span> <span class=""hljs-title"">f</span><span class=""hljs-params"">(arg1, arg2, ...)</span>:</span> ...
</code></pre>
<p>它可以在类（如 <code>C.f()</code>）或实例（如 <code>C().f()</code>）上调用。</p>
<p>Python 中的静态方法类似于 Java 或 C++ 中的。</p>
<h2 class=""heading"" data-id=""heading-56"">str</h2>
<p><code>class str(object='')</code><br /> <code>class str(object=b'', encoding='utf-8', errors='strict')</code></p>
<p>返回一个字符串对象</p>
<h2 class=""heading"" data-id=""heading-57"">sum(<em>iterable</em>[, <em>start</em>])</h2>
<p>从 start 开始，从左到右对 iterable 中的元素求和。 start 默认是 0，迭代的 item 通常是数字，并且不允许 start 的值为字符串。</p>
<p>对于有些情况，有比 <code>sum()</code> 更好的选择， 比如：连接字符串应该用 <code>''.join(sequence)</code>。浮点数求和用 <code>math.fsum()</code> 。要连接一系列 iterable，请考虑使用 <code>itertools.chain()</code>。</p>
<h2 class=""heading"" data-id=""heading-58"">super([<em>type</em>[, <em>object-or-type</em>]])</h2>
<p>返回一个代理对象，它委托方法给父类或者 type 的同级类。这对于访问类中被覆盖的继承方法很有用。搜索顺序与 <code>getattr()</code> 使用的顺序相同，只不过 type 本身被跳过。</p>
<p>type 的 <code>__mro__</code> 属性列出 <code>getattr()</code> 和 <code>super()</code> 使用的方法解析顺序。该属性是动态的，并且可以在继承层次结构更新时更改。</p>
<p>如果省略第二个参数，则返回的 super 对象是未绑定的。如果第二个参数是一个对象，则 <code>isinstance(obj, type)</code> 必须为 true。如果第二个参数是类型，则 <code>issubclass(type2, type)</code> 必须为 true（这对类方法很有用）。</p>
<p>super 有两种典型的使用情况。在具有单继承的类层次结构中，可以使用 super 来引用父类，而不必明确命名它们，从而使代码更易于维护。这种使用非常类似于在其他编程语言中 super 的使用。</p>
<p>第二种使用情况是在动态执行环境中支持协同多继承。这种使用情况是 Python 独有的，在静态编译语言或仅支持单继承的语言中找不到。这使得可以实现 &ldquo;菱形图&rdquo;，其中多个基类实现相同的方法。良好的设计指出此方法在每种情况下具有相同的调用顺序（因为调用的顺序在运行时确定，因为该顺序适应类层次结构中的更改，并且因为该顺序可以包括在运行时之前未知的兄弟类）。</p>
<p>对于这两种用例，典型的超类调用如下所示：</p>
<pre><code class=""hljs python"" lang=""python""><span class=""hljs-class""><span class=""hljs-keyword"">class</span> <span class=""hljs-title"">C</span><span class=""hljs-params"">(B)</span>:</span>
    <span class=""hljs-function""><span class=""hljs-keyword"">def</span> <span class=""hljs-title"">method</span><span class=""hljs-params"">(self, arg)</span>:</span>
        super().method(arg)    <span class=""hljs-comment""># This does the same thing as:</span>
                               <span class=""hljs-comment""># super(C, self).method(arg)</span></code></pre>
<p>!&gt; 注意，<code>super()</code> 只实现显式点分属性查找的绑定过程，例如 <code>super().__getitem__(name)</code>。它通过实现自己的 <code>__getattribute__()</code> 方法来实现这一点，以便以支持协同多继承需要的以可预测的顺序搜索类。因此，<code>super()</code> 没有定义隐式的查找语句或操作，例如 <code>super()[name]</code>。</p>
<p>!&gt; 另请注意，除了零参数形式外，<code>super()</code> 不限于在方法内部使用。如果两个参数的形式指定了准确的参数，就能进行正确的引用。零参数形式只能在类定义中使用，因为编译器会填充必要的细节以正确检索正在定义的类，以及访问普通方法的当前实例。</p>
<h2 class=""heading"" data-id=""heading-59"">tuple([<em>iterable</em>])</h2>
<p>tuple 不是一个函数，它实际上是一个不可变的序列类型</p>
<h2 class=""heading"" data-id=""heading-60"">type</h2>
<p><code>class type(object)</code><br /> <code>class type(name, bases, dict)</code></p>
<p>有一个参数时，返回 object 的类型。返回值是一个类型对象，通常与 <code>object.__class__</code> 返回的对象相同。</p>
<p>建议使用 <code>isinstance()</code> 内置函数来测试对象的类型，因为它会考虑子类。</p>
<p>有三个参数时，返回一个新的类型对象。这实质上是类声明的一种动态形式。name 字符串是类名，并成为 <code>__name__</code> 属性；bases 元组逐项列出基类，并成为 <code>__bases__</code> 属性；dict 是包含类体的定义的命名空间，并被复制到标准字典中以变为 <code>__dict__</code> 属性。例如，以下两条语句会创建相同的类型对象：</p>
<pre><code class=""hljs python"" lang=""python""><span class=""hljs-meta"">&gt;&gt;&gt; </span><span class=""hljs-class""><span class=""hljs-keyword"">class</span> <span class=""hljs-title"">X</span>:</span>
<span class=""hljs-meta"">... </span>    a = <span class=""hljs-number"">1</span>
...
<span class=""hljs-meta"">&gt;&gt;&gt; </span>X = type(<span class=""hljs-string"">'X'</span>, (object,), dict(a=<span class=""hljs-number"">1</span>))
</code></pre>
<h2 class=""heading"" data-id=""heading-61"">vars([<em>object</em>])</h2>
<p>返回一个模块、字典、类、实例或者其它任何一个具有 <code>__dict__</code> 属性的对象的 <code>__dict__</code> 属性。</p>
<p>模块和实例这样的对象的 <code>__dict__</code> 属性可以更新；但是其它对象可能对它们的 <code>__dict__</code> 属性的写操作有限制（例如，类使用 <code>types.MappingProxyType</code> 来阻止对字典直接更新）。</p>
<p>如果不带参数，<code>vars()</code> 的行为就像 <code>locals()</code>。注意，locals 字典只用于读取，因为对 locals 字典的更新会被忽略。</p>
<h2 class=""heading"" data-id=""heading-62"">zip(*iterables)</h2>
<p>制作一个迭代器，用于聚合来自每个迭代器的元素。</p>
<p>返回元组的迭代器，其中第 i 个元组包含来自每个参数序列或迭代的第 i 个元素。当最短的输入迭代耗尽时，迭代器停止。使用单个迭代参数，它将返回 1 元组的迭代器。没有参数，它返回一个空的迭代器。相当于：</p>
<pre><code class=""hljs python"" lang=""python""><span class=""hljs-function""><span class=""hljs-keyword"">def</span> <span class=""hljs-title"">zip</span><span class=""hljs-params"">(*iterables)</span>:</span>
    <span class=""hljs-comment""># zip('ABCD', 'xy') --&gt; Ax By</span>
    sentinel = object()
    iterators = [iter(it) <span class=""hljs-keyword"">for</span> it <span class=""hljs-keyword"">in</span> iterables]
    <span class=""hljs-keyword"">while</span> iterators:
        result = []
        <span class=""hljs-keyword"">for</span> it <span class=""hljs-keyword"">in</span> iterators:
            elem = next(it, sentinel)
            <span class=""hljs-keyword"">if</span> elem <span class=""hljs-keyword"">is</span> sentinel:
                <span class=""hljs-keyword"">return</span>
            result.append(elem)
        <span class=""hljs-keyword"">yield</span> tuple(result)
</code></pre>
<p>只有当您不关心后续的，来自较长迭代器的未尾匹配值时，才应该用 <code>zip()</code> 。如果这些值很重要，请改用 <code>itertools.zip_longest()</code>。</p>
<p>与 <code>*</code> 操作符一起使用 <code>zip()</code> 可用于解压缩列表：</p>
<pre><code class=""hljs python"" lang=""python""><span class=""hljs-meta"">&gt;&gt;&gt; </span>x = [<span class=""hljs-number"">1</span>, <span class=""hljs-number"">2</span>, <span class=""hljs-number"">3</span>]
<span class=""hljs-meta"">&gt;&gt;&gt; </span>y = [<span class=""hljs-number"">4</span>, <span class=""hljs-number"">5</span>, <span class=""hljs-number"">6</span>]
<span class=""hljs-meta"">&gt;&gt;&gt; </span>zipped = zip(x, y)
<span class=""hljs-meta"">&gt;&gt;&gt; </span>list(zipped)
[(<span class=""hljs-number"">1</span>, <span class=""hljs-number"">4</span>), (<span class=""hljs-number"">2</span>, <span class=""hljs-number"">5</span>), (<span class=""hljs-number"">3</span>, <span class=""hljs-number"">6</span>)]
<span class=""hljs-meta"">&gt;&gt;&gt; </span>x2, y2 = zip(*zip(x, y))
<span class=""hljs-meta"">&gt;&gt;&gt; </span>x == list(x2) <span class=""hljs-keyword"">and</span> y == list(y2)
<span class=""hljs-keyword"">True</span></code></pre></div>
<br />作者：wcode<br />链接：https://juejin.im/post/5ae3ee096fb9a07aa7676883<br />来源：掘金<br />著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。</div>