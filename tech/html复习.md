// html 复习 基础属性

**H**yper **T**ext **M**arkup **L**anguage

## 基本标签

```html?linenums
<p>段落</p>
<h1>一级标题</h1>
<a href="链接url">链接</a>
<img src="图像url" width="" height= ""/>
<br />
```

## html属性

属性为html元素提供附加信息，属性值应该始终被包括在引号内。

表：大多数html元素支持的属性：

|属性 |值       |描述              |
|-----|---------|------------------|
|class|classname|元素的类名        |
|id   |id       |元素的唯一id      |
|style|style_def|行内样式          |
|title|text     |规定元素的额外信息|

```html?linenums
<h1 align="center"></h1>
<body bgcolor="yellow"><body>
<table border="1">
<hr /> <--!水平线-->
```

## 段落

```html?linenums
<p>This is<br />a para<br />graph with line breaks</p>

<b>This text is bold</b>

<strong>This text is strong</strong>

<big>This text is big</big>

<em>This text is emphasized</em>

<i>This text is italic</i>

<small>This text is small</small>

This text contains<sub>subscript</sub>

This text contains<sup>superscript</sup>

<pre></pre><--!预格式文本-->

<code>Computer code</code>

<kbd>Keyboard input</kbd>

<tt>Teletype text</tt>

<samp>Sample text</samp>

<var>Computer variable</var>

<address>
Written by <a href="mailto:webmaster@example.com">Donald Duck</a>.<br />
Visit us at:<br />
Example.com<br />
Box 564, Disneyland<br />
USA
</address>

<acronym title="World Wide Web">WWW</acronym>

<--!如果浏览器支持 bi-directional override (bdo)-->
<bdo dir="rtl">
Here is some Hebrew text
</bdo>

<blockquote>
这是长的引用。这是长的引用。这是长的引用。这是长的引用。这是长的引用。这是长的引用。这是长的引用。这是长的引用。这是长的引用。这是长的引用。这是长的引用。
</blockquote>

<q>
这是短的引用。
</q>

<del>删除线</del>

<ins>下划线</ins>
```

## 样式

三种添加样式的方法。

```html?linenums
<style type="text/css">
	h1 {color: red}
	p {color: blue}
</style>

<a href="/example/html/lastpage.html" style="text-decoration:none">
	这是一个链接！没有下划线~
</a>

<link rel="stylesheet" type="text/css" href="/html/csstest1.css" >
```

| style | 定义样式定义。                 |
| ----- | ------------------------------ |
| link  | 定义资源引用。                 |
| div   | 定义文档中的节或区域（块级）。 |
| span  | 定义文档中的行内的小块或区域。 |


## 链接

```html?linenums
<a href="http://www.w3school.com.cn/" target="_blank">Visit W3School!</a>

<a name="label">文本</a>
<a href="#label">文本</a>

<a href="/index.html" target="_top">被锁在框架中了吗？请点击这里！</a>
```

## 图像

```html?linenums
<--! alt 属性用来为图像定义一串预备的可替换的文本 -->

<img src="boat.gif" alt="Big Boat">

<body background="/i/eg_background.jpg">

<p>图像 <img src="/i/eg_cute.gif" align="bottom"> 在文本中</p><--!默认-->
<p>图像 <img src ="/i/eg_cute.gif" align="middle"> 在文本中</p>
<p>图像 <img src ="/i/eg_cute.gif" align="top"> 在文本中</p>

<p>
<img src ="/i/eg_cute.gif" align ="left">
带有图像的一个段落。图像的 align 属性设置为 "left"。图像将浮动到文本的左侧。
</p>
<p>
<img src ="/i/eg_cute.gif" align ="right">
带有图像的一个段落。图像的 align 属性设置为 "right"。图像将浮动到文本的右侧。
</p>

<img src="/i/eg_mouse.jpg" width="50" height="50">

<body>
<p>
您也可以把图像作为链接来使用：
<a href="/example/html/lastpage.html">
<img border="0" src="/i/eg_buttonnext.gif" />
</a>
</p>
```

[创建图像映射](http://www.w3school.com.cn/tiy/t.asp?f=html_areamap)。

## 表格

<table border="2">
  <tr>
    <th>1</th>
    <th>2</th>
  </tr>
  <tr>
    <td>T11</td>
    <td>T12</td>
  </tr>
  <tr>
    <td>T21</td>
    <td>T22</td>
  </tr>
</table>

<hr />

<table border="1" cellpadding="10">
<tr>
  <td>First</td>
  <td>Row</td>
</tr>
<tr>
  <td>Second</td>
  <td>Row</td>
</tr>
</table>

<hr />

<table border="1" cellspacing="10">
<tr>
  <td>First</td>
  <td>Row</td>
</tr>
<tr>
  <td>Second</td>
  <td>Row</td>
</tr>
</table>

## 列表

<ul type="disc">
 <li>苹果</li><li>香蕉</li><li>柠檬</li><li>桔子</li>
</ul>

<ul type="circle">
 <li>苹果</li><li>香蕉</li><li>柠檬</li><li>桔子</li>
</ul>

<ul type="square">
 <li>苹果</li><li>香蕉</li><li>柠檬</li><li>桔子</li>
</ul>

<ol>
 <li>苹果</li><li>香蕉</li><li>柠檬</li><li>桔子</li>
</ol>

<ol type="A">
 <li>苹果</li><li>香蕉</li><li>柠檬</li><li>桔子</li>
</ol>

<ol type="a">
 <li>苹果</li><li>香蕉</li><li>柠檬</li><li>桔子</li>
</ol>

<ol type="I">
 <li>苹果</li><li>香蕉</li><li>柠檬</li><li>桔子</li>
</ol>

<ol type="i">
  <li>苹果</li><li>香蕉</li><li>柠檬</li><li>桔子</li>
</ol>

<ul>
  <li>咖啡</li>
  <li>茶
    <ul><li>红茶</li><li>绿茶</li></ul>
  </li>
  <li>牛奶</li>
</ul>

定义列表：

<dl>
  <dt>计算机</dt><dd>用来计算的仪器 ... ...</dd><dt>显示器</dt><dd>以视觉方式显示信息的装置 ... ...</dd>
</dl>

## div 和 span

块元素和内联元素：

1. 块元素：block，通常会以新行来开始（和结束）。
2. 内联元素：inline，通常不会以新行开始。

HTML `<div>` 元素是块级元素，它是可用于组合其他 HTML 元素的容器。`<div>` 元素没有特定的含义。除此之外，由于它属于块级元素，浏览器会在其前后显示折行。

如果与 CSS 一同使用，<div> 元素可用于对大的内容块设置样式属性。

`<div>` 元素的另一个常见的用途是文档布局，定义文档中的分区或节（division/section）。它取代了使用表格定义布局的老式方法。使用 `<table>` 元素进行文档布局不是表格的正确用法。`<table>` 元素的作用是显示表格化的数据。

HTML `<span>` 元素是内联元素，可用作文本的容器。`<span>` 元素也没有特定的含义。当与 CSS 一同使用时，`<span>` 元素可用于为部分文本设置样式属性。

## 使用div布局页面

看 CSS 的时候再说。


## 表单和输入

<form>
我喜欢自行车：
<input type="checkbox" name="Bike"><br />

我喜欢汽车：
<input type="checkbox" name="Car">
</form><br />

<form>
男性：
<input type="radio" checked="checked" name="Sex" value="male" />
<br />
女性：
<input type="radio" name="Sex" value="female" />
</form><br />

<form>
<select name="cars">
<option value="volvo">Volvo</option>
<option value="saab">Saab</option>
<option value="fiat">Fiat</option>
<option value="audi">Audi</option>
</select>
</form><br />

<form>
<select name="cars">
<option value="volvo">Volvo</option>
<option value="saab">Saab</option>
<option value="fiat" selected="selected">Fiat</option>
<option value="audi">Audi</option>
</select>
</form><br />

<textarea rows="2" cols="40">
The cat was playing in the garden.
</textarea><br />

<form>
<input type="button" value="Hello world!">
</form><br />

<form>
  <fieldset>
    <legend>健康信息</legend>
    身高：<input type="text" />
    体重：<input type="text" />
  </fieldset>
</form>

```html?linenums
<form action="/example/html/form_action.asp" method="get">
  <p>First name: <input type="text" name="fname" /></p>
  <p>Last name: <input type="text" name="lname" /></p>
  <input type="submit" value="Submit" />
</form>
```

```html?linenums
<form action="MAILTO:someone@w3school.com.cn" method="post" enctype="text/plain">

<h3>这个表单会把电子邮件发送到 W3School。</h3>
姓名：<input type="text" name="name" value="yourname" size="20">
电邮：<input type="text" name="mail" value="yourmail" size="20">
内容：<input type="text" name="comment" value="yourcomment" size="40">
<br />
<input type="submit" value="发送">
<input type="reset" value="重置">

</form>
```

## 框架

```html?linenums
<html>
<frameset cols="25%,50%,25%">
  <frame src="/example/html/frame_a.html">
  <frame src="/example/html/frame_b.html">
  <frame src="/example/html/frame_c.html">
</frameset>
</html>
```

```html?linenums
<html>
<frameset rows="25%,50%,25%">
  <frame src="/example/html/frame_a.html">
  <frame src="/example/html/frame_b.html">
  <frame src="/example/html/frame_c.html">
</frameset>
</html>
```

假如一个框架有可见边框，用户可以拖动边框来改变它的大小。为了避免这种情况发生，可以在frame标签中加入：noresize="noresize"。

body 与 frameset 不能同时使用。

```html?linenums
<frameset cols="25%,50%,25%">
  <frame src="/example/html/frame_a.html">
  <frame src="/example/html/frame_b.html">
  <frame src="/example/html/frame_c.html">
  <noframes>
  <body>您的浏览器无法处理框架！</body>
  </noframes>
</frameset>
```

```html?linenums
<frameset rows="50%,50%">
  <frame src="/example/html/frame_a.html">
  <frameset cols="25%,75%">
    <frame src="/example/html/frame_b.html">
    <frame src="/example/html/frame_c.html">
  </frameset>
</frameset>
```

导航

```html?linenums
<frameset cols="120,*">
  <frame src="/example/html/html_contents.html">
  <frame src="/example/html/frame_a.html" name="showframe">
</frameset>
```

内联框架

```html?linenums
<body>
  <iframe src="/i/eg_landscape.jpg"></iframe>
  <p>一些老的浏览器不支持 iframe。</p>
  <p>如果得不到支持，iframe 是不可见的。</p>
</body>
```

其中的一个框架设置了指向另一个文件内指定的节的链接。这个"link.htm"文件内指定的节使用 <a name="C10"> 进行标识。
```html?linenums
<frameset cols="20%,80%">
 <frame src="/example/html/frame_a.html">
 <frame src="/example/html/link.html#C10">
</frameset>
```
使用框架导航跳转至指定的节。
```html?linenums
<frameset cols="180,*">
  <frame src="/example/html/content.html">
  <frame src="/example/html/link.html" name="showframe">
</frameset>
```

## 内联框架

iframe 用于在网页内显示网页。`<iframe src="URL"></iframe>`。

1. width="200" height="200"
2. frameborder="0"
3. iframe 可用作链接的目标（target）。链接的 target 属性必须引用 iframe 的 name 属性：

```
<iframe src="demo_iframe.htm" name="iframe_a"></iframe>
<p><a href="http://www.w3school.com.cn" target="iframe_a">W3School.com.cn</a></p>
```

## 背景

<body> 标签中的背景颜色（bgcolor）、背景（background）和文本（text）属性在最新的 HTML 标准（HTML4 和 XHTML）中已被废弃。W3C 在他们的推荐标准中已删除这些属性。

应该使用层叠样式表（CSS）来定义 HTML 元素的布局和显示属性。