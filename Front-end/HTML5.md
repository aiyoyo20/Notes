# 介绍
HTML 即超文本标记语言 (英语：Hypertext Markup Language，简称：HTML ) 是一种用来结构化 Web 网页及其内容的标记语言。网页内容可以是：一组段落、一个重点信息列表、也可以含有图片和数据表。

HTML文档的内容构成了网页的基本骨架。

# 元素
HTML 不是一门编程语言，而是一种用于定义内容结构的标记语言。HTML 由一系列的元素（elements）组成，这些元素可以用来包围不同部分的内容，使其以某种方式呈现或者工作。 一对标签（ tags）可以为一段文字或者一张图片添加超链接，将文字设置为斜体，改变字号，等等。

标签分为单标签和双标签，且大多数为双标签。顾名思义就是成对出现或者是单独出现。
例如：`<p>hello</p>`，这是一个段落标签，一个双标签。`<p>`称为开始标签或开放标签，`</p>`则为结束标签或闭合标签，`hello`是该标签的内容，三个部分的组合就构成了一个元素。在网页中显示出来就是一个简单的段落。

单标签的标准写法。<br />

## 元素嵌套
有的元素是可以进行嵌套的，如`<div><a>hello</a></div>` 
由于浏览器的容错机制，有时在标签嵌套不规范、缺少闭合标签等的情况下，浏览器的显示不会受到影响，但是最好保持良好的元素使用，避免出现解析混淆的情况。

## 空元素
该元素不包含任何的内容，如<base />,<hr />,<img />等元素。

## 块级元素、内联元素
块级元素在页面中以块的形式展现 —— 相对于其前面的内容它会出现在新的一行，其后的内容也会被挤到下一行展现。块级元素通常用于展示页面上结构化的内容，例如段落、列表、导航菜单、页脚等等。一个以block形式展现的块级元素不会被嵌套进内联元素中，但可以嵌套在其它块级元素中。
内联元素通常出现在块级元素中并环绕文档内容的一小部分，而不是一整个段落或者一组内容。内联元素不会导致文本换行：它通常出现在一堆文字之间例如超链接元素<a>或者强调元素<em>和 <strong>。

## 元素的属性
元素可以具有属性，根据作用范围的又可以分为全局属性和元素属性
```
<p class="para"> this is paragraph </p>
<a class='anchor' href='#' />
```
class 便是一个全局属性，而 href 则是一个元素属性
一个属性必须包含如下内容：

一个空格，在属性和元素名称之间。(如果已经有一个或多个属性，就与前一个属性之间有一个空格。)
属性名称，后面跟着一个等于号。
一个属性值，由一对引号“ ”引起来。

布尔属性
有时你会看到没有值的属性，它是合法的。这些属性被称为布尔属性，他们只能有跟它的属性名一样的属性值。例如disabled 属性，他们可以标记表单输入使之变为不可用(变灰色)，此时用户不能向他们输入任何数据。

省略包围属性值的引号
当你浏览那些粗糙的web网站，你将会看见各种各样奇怪的标记风格，其中就有不给属性值添加引号。在某些情况下它是被允许的，但是其他情况下会破坏你的标记。

单引号或者双引号？
在目前为止，本章内容所有的属性都是由双引号来包裹。也许在一些HTML中，你以前也见过单引号。这只是风格的问题，你可以从中选择一个你喜欢的

# HTML 文档详解
[HTML 文档详解](https://developer.mozilla.org/zh-CN/docs/Learn/Getting_started_with_the_web/HTML_basics)
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>我的测试站点</title>
  </head>
  <body>
    <p>这是我的页面</p>
  </body>
</html>
```

<!DOCTYPE html>: 声明文档类型. 很久以前，早期的HTML(大约1991年2月)，文档类型声明类似于链接，规定了HTML页面必须遵从的良好规则，能自动检测错误和其他有用的东西。使用如下：
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
然而这种写法已经过时了，这些内容已成为历史。只需要知道 <!DOCTYPE html> 是最短有效的文档声明。
<html></html>: <html>元素。这个元素包裹了整个完整的页面，是一个根元素。
<head></head>: <head>元素. 这个元素是一个容器，它包含了所有你想包含在HTML页面中但不想在HTML页面中显示的内容。这些内容包括你想在搜索结果中出现的关键字和页面描述，CSS样式，字符集声明等等。以后的章节能学到更多关于<head>元素的内容。
<meta charset="utf-8">: 这个元素设置文档使用utf-8字符集编码，utf-8字符集包含了人类大部分的文字。基本上他能识别你放上去的所有文本内容。毫无疑问要使用它，并且它能在以后避免很多其他问题。
<title></title>: 设置页面标题，出现在浏览器标签上，当你标记/收藏页面时它可用来描述页面。
<body></body>: <body>元素。 包含了你访问页面时所有显示在页面上的内容，文本，图片，音频，游戏等等。

## <head>标签里有什么? Metadata-HTML中的元数据
在页面加载完成的时候，标签head里的内容，是不会在页面中显示出来的。它包含了像页面的<title>(标题) ,CSS(如果你选择用 CSS 来为 HTML 内容添加样式)，指向自定义图标的链接和其他的元数据(描述HTML的数据，比如，作者，和描述文档的重要关键词)。

### 元数据：<meta>元素
元数据就是描述数据的数据，而HTML有一个“官方的”方式来为一个文档添加元数据——  <meta> 元素。当然，其他在这篇文章中提到的东西也可以被当作元数据。有很多不同种类的 <meta> 元素可以被包含进你的页面的<head>元素，

许多<meta> 元素包含了name 和 content 特性：
name 指定了meta 元素的类型； 说明该元素包含了什么类型的信息。
content 指定了实际的元数据内容。

如今，几乎你使用的所有网站都会使用 CSS 让网页更加炫酷，使用JavaScript让网页有交互功能，比如视频播放器，地图，游戏以及更多功能。这些应用在网页中很常见，它们分别使用 <link>元素以及 <script> 元素。

图像（image）
图像元素通常具有两个属性：src，包含图像文件的路径;alt，是图像的描述内容，当图片不可见时给出提示，
使用例子：`<img src="images/firefox-icon.png" alt="测试图片">`

标题（heading）
标题元素有六个级别，从h1～h6,随着层级的增加标题逐渐缩小。
```
<h1>主标题</h1>
<h2>顶层标题</h2>
<h3>子标题</h3>
<h4>次子标题</h4>
```
>注：可以发现 MDN 网站上 第一级标题的主题是隐藏的。不要使用标题元素来加大、加粗字体，因为标题对于 无障碍访问 和 搜索引擎优化 等问题非常有意义。要保持页面结构清晰，标题整洁，不要发生标题级别跳跃。

段落（paragraph）
使用段落可以使用<p>元素实现。
`<p>这是一个段落</p>`

文本格式化
一些 HTML 标签除了具有一定的语义（含义）外，还有默认的样式，例如<b>（加粗）、<em>（倾斜）等，通过这些标签我们无需借助 CSS 就可以为网页中的内容定义样式。在这些具有语义和默认样式的标签中，有许多是针对文本的，通过这些标签我们可以格式化文本（为文本添加样式），例如使文本加粗、倾斜或者添加下划线等。
<strong>和<b>标签之间的区别
默认情况下，<strong>和<b>标签都可以使文本以粗体展示标签中的文本，但是<strong>标签的语义是标签中的内容具有很高的重要性，而<b>标签的语义仅仅是加粗文本以引起读者的注意，并没有特殊的意思。
同样，<em>和<i>标签默认情况下均以斜体显示标签中的文本，但是<em>标签具有强调的语义，用来表示标签中的内容很重要，而<i>标签仅仅用于定义斜体文本。

列表（list）
无序列表，用一个 <ul> 元素包围。
有序列表，用一个 <ol> 元素包围。
定义列别，用yige <dl> 元素包围。

|列表分类|	说明|
|有序列表|	<ol> 表示有序列表，<li> 表示列表中的每一项，默认使用阿拉伯数字编号。|
|无序列表|	<ul> 表示无序列表，配合 <li> 实现，默认使用●符号显示。|
|定义列表|	<dl> 与<dt>、<dd> 配合实现，<dt> 充当列表的标题，<dd> 是对 <dt> 的解释说明|

链接(anchor)（hypertext reference）
`<a href="https://www.mozilla.org/zh-CN/about/manifesto/">Mozilla 宣言</a>`

表格（table）
使用了<table>、<tr>、<td> 及 <th> 四个标签：
<table> 表示表格，表格的所有内容需要写在 <table> 和 </table> 之间。
<tr> 是 table row 的简称，表示表格的行。表格中有多少个 <tr> 标签就表示有多少行数据。
<td> 是 table datacell 的简称，表示表格的单元格，这才是真正存放表格数据的标签。单元格的数据可以是文本、图片、列表、段落、表单、水平线、表格等多种形式。
<th> 是 table heading 的简称，表示表格的表头。<th> 其实是 <td> 单元格的一种变体，本质上还是一种单元格。<th> 一般位于第一行，充当每一列的标题。大多数的浏览器会把表头显示为粗体居中的文本。

默认情况下，表格是没有边框的。但是我们可以使用 <table> 标签中的 border 属性来设置表格的边框宽度，单位是像素（px）。本例中我们将表格的边框宽度设置为 1px。注意，px 是默认的单位，不用显式指明。

我们常见的表格一般都有标题，表格的标题使用 <caption> 标签来表示。默认情况下，表格的标题位于整个表格的第一行并且居中显示。一个表格只能有一个标题，也就是说 <table> 标签中只能有一个 <caption> 标签。

表单
表单属于 HTML 文档的一部分，其中包含了如输入框、复选框、单选按钮、提交按钮等不同的表单控件，用户通过修改表单中的元素（例如输入文本，选择某个选项等）来完成表单，通过表单中的提交按钮将表单数据提交给后端程序。

在 HTML 中创建表单需要用到<form>标签，
HTML 表单中可以包含如下表所示的控件：

|控件/标签	|描述|
|<input>	|定义输入框|
|<textarea>	|定义文本域（一个可以输入多行文本的控件）|
|<label>	|为表单中的各个控件定义标题|
|<fieldset>	|定义一组相关的表单元素，并使用边框包裹起来|
|<legend>	|定义 <fieldset> 元素的标题|
|<select>	|定义下拉列表|
|<optgroup>	|定义选项组|
|<option>	|定义下拉列表中的选项|
|<button>	|定义一个可以点击的按钮|
|<datalist>	|指定一个预先定义的输入控件选项列表|
|<keygen>	|定义表单的密钥对生成器字段|
|<output>	|定义一个计算结果|

注释
```
<!--单行注释  -->
<!--
    多行注释
-->
```

内联框架
HTMl <iframe> 标签用来定义一个内联框架，使用它可以将另一个网页嵌入到当前网页中。<iframe> 标签会在网页中定义一个矩形区域，浏览器可以在这个区域内显示另一个页面的内容。

html5 与 html 的差异
更好的错误处理
现代 Web 应用程序支持
改进的语义
手机支持改进
视频和音频支持
矢量图形支持
