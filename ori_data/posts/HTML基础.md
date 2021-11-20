---
title: HTML基础
description: 本文主要介绍了html的基础知识
tags: 
- html
categories:
- web
---
在此特地声明本文是根据 [mozilla官方教学文档](https://developer.mozilla.org/zh-CN/docs/Learn/html/Introduction_to_html) 学习的个人学习笔记，借用了大量的图片和文本内容，存在相当多的相同，但不是copy。如需查看mozilla官方文档，请点击前文链接！！
<!--more-->

<!-- toc -->
- [html入门](#html入门)
  - [什么是html](#什么是html)
  - [剖析一个html元素](#剖析一个html元素)
    - [嵌套元素](#嵌套元素)
    - [块级元素和内联元素](#块级元素和内联元素)
    - [空元素void-elements](#空元素void-elements)
  - [属性](#属性)
    - [为一个元素添加属性](#为一个元素添加属性)
    - [布尔属性](#布尔属性)
  - [html文档](#html文档)
  - [实体引用：在html中包含特殊字符](#实体引用在html中包含特殊字符)
  - [html注释](#html注释)
- [head标签和metadata-html中的元数据](#head标签和metadata-html中的元数据)
  - [什么是html头部元素？](#什么是html头部元素)
  - [添加标题](#添加标题)
  - [元数据-meta元素](#元数据-meta元素)
    - [字符的编码](#字符的编码)
    - [添加作者和描述](#添加作者和描述)
    - [其它类型的元数据](#其它类型的元数据)
  - [自定义图标](#自定义图标)
  - [在html中应用css和javascript](#在html中应用css和javascript)
  - [为文档设定主语言](#为文档设定主语言)
- [<a id="h1">html文字处理基础</a>](#html文字处理基础)
  - [标题和段落](#标题和段落)
    - [标题](#标题)
    - [段落](#段落)
    - [语义](#语义)
  - [列表Lists](#列表lists)
    - [无序-unordered](#无序-unordered)
    - [有序-ordered](#有序-ordered)
    - [嵌套列表-nesting-lists](#嵌套列表-nesting-lists)
    - [描述列表](#描述列表)
  - [重点强调](#重点强调)
    - [强调](#强调)
    - [非常重要](#非常重要)
    - [斜体字-粗体字-下划线](#斜体字-粗体字-下划线)
  - [高级文字排版](#高级文字排版)
    - [引用](#引用)
      - [块引用](#块引用)
      - [行内引用](#行内引用)
      - [引文](#引文)
    - [缩略语](#缩略语)
    - [标记联系方式](#标记联系方式)
    - [上标和下标](#上标和下标)
    - [展示计算机代码](#展示计算机代码)
    - [标记时间和日期](#标记时间和日期)
- [超链接](#超链接)
  - [链接的创建](#链接的创建)
  - [电子邮件链接](#电子邮件链接)
  - [统一资源定位器和路径入门](#统一资源定位器和路径入门)
    - [文档片段](#文档片段)
    - [绝对url和相对url](#绝对url和相对url)
- [文档与网站架构](#文档与网站架构)
  - [文档的基本组成部分](#文档的基本组成部分)
  - [用于构建内容的html](#用于构建内容的html)
  - [html布局元素细节](#html布局元素细节)
    - [无语义元素](#无语义元素)
    - [换行与水平分割线](#换行与水平分割线)
  - [规划一个简单的网站](#规划一个简单的网站)
- [html调试](#html调试)
<!-- toc -->

<br>

***html是一种相对简单的、由不同元素组成的标记语言，它可以应用于文本片段，使文本在文档中具有不同的含义——它是一个段落、项目列表或表格吗？<br>
它可以将文档结构化为逻辑块，可以将图片，影像等内容嵌入到页面中。***

<br>

# html入门
将介绍html最基础的部分，对元素、属性以及可能涉及的一些重要术语，并明确它们在语言中所处的位置。<br>
将讲解html元素和页面的组织方式，以及其他一些重要的基本语言特性。

<br>

## 什么是html
html（Hyper Text Markup Language）不是一门编程语言，而是一种用来告知浏览器如何组织页面的标记语言。<br>
它由一系列的元素（elements）组成，这些元素可以用来包围不同部分的内容，使其以某种方式呈现或者工作。<br>
一对标签（tags）可以为一段文字或者一张图片添加超链接，将文字设置为斜体，改变字号等等。
> 你的名字 (Q_Q)<br>
> ------将这段文字封装成一个\<p>段落元素------><br>
> \<p>你的名字 (Q_Q)\</p>

>注意：html标签*不区分大小写*

<br>

## 剖析一个html元素

元素的主要部分：

|名称|定义|
|---|---|
|开始标签|包含元素的名称，例如p，被左、右角括号所包围。表示元素从这里开始或开始起作用。|
|结束标签|与开始标签相似，在其元素名前包含了一个斜杠，表示元素的结尾。|
|内容|元素的内容。|

<br>

### 嵌套元素
把元素放到其他元素之中。
>\<p>你的\<strong>名字\</strong> (Q_Q)\</p>

在上面例子中，先打开\<p>元素，然后再打开\<strong>元素；因此必须先关闭\<p>元素。<br>

所有的元素都需要正确的打开和关闭；如果进行了错误的嵌套，那么浏览器就会猜测你想要表达的意思，得出错误的结果。

<br>

### 块级元素和内联元素
***块级元素和内联元素是重要元素类别，但是html5重新定义了元素的类别***
- 块级元素在页面中以块的形式展现——相对于其前面的内容他会出现在新的一行，其后的内容也会被挤到下一行展现。块级元素通常用于展示页面上结构化的内容，例如段落、列表、导航菜单、页脚等等。

    一个以block形式展现的块级元素不会被嵌套进内联元素中，但可以嵌套在其它块级元素中。

- 内联元素通常出现在块级元素中环绕文档内容的一部分，而不是一整个段落或者一组内容。内联元素不会导致文本换行：它通常出现在一堆文字之间，例如超链接元素\<a>或者强调元素\<strong>和\<em>。
例如
>\<em>一\</em>\<em>二\</em>\<em>三\</em><br>
>
>\<p>四\</p>\<p>五\</p>\<p>六\</p>

输出
>*一二三*<br>
>一<br>
>二<br>
>三<br>

\<em>是一个内联元素，\<p>是一个块级元素。

<br>

### 空元素void-elements
不是所有的元素都拥有开始标签，内容，结束标签。一些元素只有一个标签，通常用来在此元素所在位置插入/嵌入一些东西。例如\<img>是用来插入一张指定的图片。<br>

>\<img src="https://*URL*">

<br>

## 属性
属性包含元素的额外信息，这些信息不会出现在实际的内容中。例如，class这个属性给元素赋了一个识别的名字（id），这个名字可以被用来识别此元素的样式信息和其他信息。

![图片二](1.png)
>属性必须包含的内容：
>1. 一个空格，在属性与元素名称之间或属性与属性之间。
>1. 属性名称，后面跟着一个等于号。
>1. 一个属性值，由一对引号 **""** 引起来。

<br>

### 为一个元素添加属性
```html
<p>欢迎来到<a href="https://www.bilibili.com" title="B站" target="_blank">B站</a>!!</p>
```
元素\<a>是锚，它使被标签包裹的内容成为一个超链接。此元素可以添加属性。<br>
- href：声明超链接的Web地址。
- title：为超链接声明额外的信息。
- target：用于指定链接如何呈现出来。`target="_blank"`将在新标签页中显示链接。

<br>

### 布尔属性
布尔属性是一种没有没有值的属性。它们只能有跟它的属性名一样的属性值。例如`disabled`属性，他们可以标记表单输入使之变成不可用（变灰色）。<br>
```html
<input type="text" disabled="disabled">
```

> 注意：属性值可以用双引号或单引号包裹，但不能在一个属性值中混用。<br>
> 支持引号中嵌套另一种引号；如果想将引号当作文本显示在html中，需使用**实体引用**。

<br>

## html文档
这些特定元素是怎么被结合起来的，从而形成一个完整的html页面？
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>测试站点</title>
  </head>
  <body>
    <p>一个页面</p>
  </body>
</html>
```
分析如下：
1. `<DOCTYPE html>`：声明文档类型。他是最短最有效的文档声明。
2. `<html></html>`：\<html>元素。这个元素包裹整个完整的页面，是一个根元素。
3. `<head></head>`：\<head>元素。是一个容器，包含所有你想包含在html页面中，但不想在html页面中显示的内容。页面描述、CSS样式、字符集声明等。
4. `<meta charset="utf-8">`：这个元素设置文档使用utf-8字符集编码。
5. `<title></title>`：设置页面标题，出现在浏览器标签上。
6. `<body></body>`：\<body>元素，包含你访问页面时所有显示在页面上的内容，文本、图像、音频、视频等。

> 注意：无论你在html元素的内容中使用多少空格和换行，当渲染这些代码的时候，html解释器会将连续出现的空白字符减少为一个单独的空格符。
```html
<p>a     b
   c</p>

等于

<p>a b c</p>
```

<br>

## 实体引用：在html中包含特殊字符
在html中，字符 `<` ， `>` ， `"` ， `'` , `&` 是特殊字符。它们本身就是html语法的一部分。<br>
哪怎么使它们不被浏览器视为代码并被解释？将这些字符包含进文本中？<br>
**我们需要使用字符引用——表示字符的特殊编码，每个字符引用以符号&开始，以分号 ; 结束。


|原义字符|等价字符引用|
|---|---|
|<|\&lt;|
|>|\&gt;|
|"|\&quot;|
|'|&apos;|
|&|\&amp;|
|---|---|
```html
<p>html中使用 &lt;p&gt; 来定义段落元素</p>
```

<br>

## html注释
注释是被浏览器忽视的，且对用户不可见。
```html
<!-- 注释内容 -->
```

<br>

# head标签和metadata-html中的元数据
页面加载完成的时候，head标签的内容是不会在页面中显示出来的。它包含了页面的`<title>`(标题)、CSS，指向自定义图标的链接和其他的元数据。

<br>

## 什么是html头部元素？
它的内容不会在浏览器中显示，它的作用是保存页面的一些 元数据
```html
<head>
  <meta charset="utf-8">
  <title>我的测试站点</title>
</head>
```
大型页面的head会包含很多元数据，这里只介绍几项重要的常用元素。

<br>

## 添加标题
- `<title>`为**文档**添加标题。
- `<h1>`为body添加标题。
同时，`<title>`的内容可以被作为建议的书签名，也被显示在搜索的结果当中。<br>

<br>

## 元数据-meta元素
元数据就是描述数据的数据，`<meta>`元素是为文档添加元数据的方式。有很多不同种类的`<meta>`元素可以被包含进页面的`<head>`元素。

<br>

### 字符的编码
```html
<meta charset="utf-8">
```
这个元素简单的指定了文档的字符串编码。<br>
utf-8是一个通用的字符集，它包含人类语言中的大部分字符。（包括中文和藏文）

<br>

### 添加作者和描述
很多`<meta>`元素包含`name`和`content`特性。
- `name`指定了meta元素的类型；说明该元素包含什么类型的信息。
- `content`指定了实际的原数据内容。

这两个meta元素可以定义页面的作者和提供页面的简要描述。
```html
<meta name="author" content="apin">
<meta name="description" content="This is a webpage writed to present how to use meta elements in order to point auhor and show some masseges.">
```
指定包含关于页面内容的关键字的页面内容的描述是很有用的，因为它可以使你的页面更容易出现在搜索引擎的相关搜索中。（即Search Engine Optimization,or SEO）<br>
description也被使用在搜索引擎显示的结果页中。<br>

<br>

### 其它类型的元数据
一个网页可能包含了很多其他类型的元数据，它们可以提供许多功能。它们很多都是专有创作的，目的是向某些网站（如社交网站）提供可使用的特定信息。 <br>
例如，Facebook编写的元数据协议Open Graph Data；

<br>

## 自定义图标
显示在浏览器中每一个打开的页面的标签页中以及书签面板中的书签页面中。

页面添加图标的方式：
1. 将其保存在与网站的索引页面相同的目录中，以.ioc格式保存。
2. 添加html\<head>元素：
   ```html
   <link rel="shortcut icon" href="favicon.ioc" type="image/x-icon">
   ```

<br>

## 在html中应用css和javascript
使用[CSS](https://baike.baidu.com/item/CSS/5457)让网页更加炫酷，使用[JavaScript](https://baike.baidu.com/item/javascript/321142)让网页有交互功能；它们分别使用`<link>`元素以及`<script`元素。

- `<link>`元素常位于文档的头部。这个link元素有2个属性，rel="stylesheet"表明这是文档的样式表，而href包含了样式表文件的路径：<br>
  `<link rel="stylesheet" href="my-css-file.css">`
- `<script>`部分没必要一定放在文档头部；实际上，把它放在`<body>`的尾部是一个更好的选择，这样可以确保在加载脚本之前浏览器已经解析了html内容（*如果脚本加载某个不存在的元素，浏览器会报错*）：<br>
  `<script src="my-js-file.js"></script>`
  > `<script>`不是一个空元素，它需要一个结束标记。<br>
  > `<script>`不仅可以指向外部脚本文件，还可以将将脚本直接放入`script`元素中。

<br>

## 为文档设定主语言
可以通过 添加`lang`属性到html开始标签 为网页设定语言。<br>
```html
<html lang="zh-CN">
```
通过设定语言，你的html文档可以被搜索引擎更有效地索引。

将文档的分段设置为不同的语言。
```html
<p>日语：<span lang="jp">皆さん、こんにちは</span>。</p>
```
> 语言编码标准：IOS 639-1

<br>

# <a id="h1">html文字处理基础</a>
html的主要工作是编辑文本结构和文本内容（语义--semantics），以便浏览器能正确的显示。

<br>

## 标题和段落
大部分的文本结构由标题和段落组成。内容结构化会使读者的阅读体验更轻松、更愉快。

<br>

### 标题
每个标题（heading）是通过“标题标签”进行定义的：
```html
<h1>这是一个标题</h1>
```
`<h1>`,`<h2>`,`<h3>`,`<h4>`,`<h5>`,`<h6>`都是标题元素标签，分别为顶级标签、二级子标签、三级子标签······

- 最好每个页面只使用一次顶级标签
- 确保在层次结构中以正确的顺序使用标题
- 在可用的六个标签中，除非必要，你应该尽量使每个页面只使用三个级别的标签

<br>

### 段落
在html中，每个段落是通过`<p>`元素标签进行定义的：
```html
<p>这是一个段落！</p>
```

> 内容结构化的原因：
> 1. 快速查找信息的需要
> 2. 标题是搜索引擎**对网页建立索引**和**进行网页搜索排名**的重要关键字
> 3. 方便使用听力阅读网页，即使用屏幕阅读器
> 4. CSS和JavaScript有效定位的需要

<br>

### 语义
语义——我们依靠以前的经验就可以知道日常事物代表什么——我们需要保证使用正确的元素来给予内容正确的意思、作用以及外形。<br>
```html
<h1>一个标题</p>
```
不仅浏览器会给他一个更大的字形，更重要的是它的语义值会以多种方式被使用，比如搜索引擎和屏幕阅读器。

任一元素都可以看起来像是一个标题。
```html
<span style="font-size: 32px; margin: 21px 0;">这是标题吗？</span>
```
**`<span>`元素没有语义，你可以对它包裹的内容使用CSS或JS，且不需要附加任何额外的意义。**<br>
以上就是使用CSS使它看起来像是一个标题，但实际上它不具有标题的作用。

<br>

## 列表Lists
列表随处可见，大致包含了三种不同类型的列表。

<br>

### 无序-unordered
无序列表用于标记列表项目顺序无关要紧的列表。

无序列表先用`<ul>`包裹所有项目，在用`<li>`元素将每个项目单独包裹起来
```html
<ul>
  <li>包子</li>
  <li>豆浆</li>
  <li>豆腐脑</li>
  <li>油条</li>
<ul>
```
效果：
> - 包子
> - 豆浆
> - 豆腐脑
> - 油条

<br>

### 有序-ordered
有序列表需要按照顺序列出项目。

有序列表的结构和无序列表一样，只不过要用`<ol>`元素将所有项目包裹。
```html
<ol>
  <li>我</li>
  <li>有</li>
  <li>一</li>
  <li>个</li>
  <li>梦</li>
  <li>想</li>
<ol>
```
效果：
> 1. 我
> 1. 有
> 1. 一
> 1. 个
> 1. 梦
> 1. 想

<br>

### 嵌套列表-nesting-lists
将一个列表嵌入到另一个列表是完全可以的。
```html
<ol>
  <li>找好装修公司</li>
  <li>请第三方监理</li>
  <li>前期设计
    <ul>
      <li>明确装修过程涉及的面积。特别是贴砖面积、墙面漆面积、壁纸面积、地板面积</li>
      <li>明确主要墙面尺寸。特别是以后需要设计摆放家具的墙面尺寸</li>
    </ul>
  </li>
  <li>现场交底等</li>
</ol>
```

### 描述列表
第三种列表——描述列表，标记一组项目及其相关描述。

描述列表使用`<dl>`标签，每一个项目都用`<dt>`元素闭合，其相关描述使用`<dd>`元素闭合。
```html
<dl>
  <dt>html</dt>
    <dd>html就是整合网页结构和内容显示的一种语言</dd>
  <dt>CSS</dt>
    <dd>用来定义如何显示html元素</dd>
  <dt>JavaScript</dt>
    <dd>用于实现网页的功能，完成一些交互</dd>
</dl>
```
**一个术语可以同时拥有多个描述。**

浏览器的默认样式会在**描述术语**和**描述部分**之间产生缩进。

浏览器渲染效果：
>**html**<br>
&ensp;&ensp;html就是整合网页结构和内容显示的一种语言<br>
>**CSS**<br>
&ensp;&ensp;用来定义如何显示html元素<br>
>**JavaScript**<br>
&ensp;&ensp;用于实现网页的功能，完成一些交互<br>

<br>

## 重点强调
html提供了突出文本重点的相应标签，用于标记某些文本，使其具有加粗、倾斜、下划线等效果。

<br>

### 强调
在口语表达中，我们有时会强调某些字，用来**改变**这句话的意思。在书面语中，可以使用斜体达到这种效果。例如：

I am glad you weren't late.<br>
I am *glad* you weren't *late*.

第一句话听起来真的松了一口气。相反，第二句话听起来具有讽刺性而且具有隐含的攻击性。

在html中，使用`<em>`（emphasis）元素标记这样的情况。它可以被屏幕阅读器识别并以不同的语调发出。浏览器默认风格是*斜体*，但不应该纯粹使用这个标签来获得斜体风格；而是使用`<span>`元素和CSS，或`<i>`元素。
```html
<p>I am <em>glad</em> you weren't <em>late</em>.</p>
```

<br>

### 非常重要
为了**强调**重要的词，在口语方面我们往往用重音强调，在文字方面则是用粗体字来达到强调的效果。例如：

This is a **pen**.<br>
We will be late.**Hurry up**!

在html中，使用`<strong>`（strong importance）元素来标记这样的情况。同样可以被屏幕阅读器识别。浏览器默认粗体，但最好使用`<span>`元素和一些CSS，或者`<b>`元素。
```html
<p>This is a <strong>pen</strong>.</p>

<p>We will be late.<strong>Hurry up</strong>!</p>
```

<br>

### 斜体字-粗体字-下划线
`<b>`,`<i>`,`<u>`出现在人们需要在文本中使用粗体、斜体等，但CSS不被完全支持的时期。<br>
这样的元素，仅仅影响表象而且没有语义，被称为**表象元素（presentational elements)**。

> html5用新的语义规则重新定义了`<b>`,`<i>`和`<u>`,使得它们的语言显得稍微有点混乱

如果没有更合适的元素，那么使用 `<b>`、`<i>`或`<u>`来表达传统上的`粗体`、`斜体`或`下划线`表达的意思是合适的。然而，始终拥有*可访问性*的思维模式是至关重要的。

> 注意：因为我们常常会认为网页中的下划线代表着一个超链接，所以最好只用下划线来代表超链接。

<br>

## 高级文字排版
html中有很多元素可以用来格式化文本，这些没有在[html文本处理基础](#h1)中出现的元素，虽然使用的少，但依旧值得学习。

<br>

### 引用
html有用于标记引用的特性，分别使用不同的元素标记引用的一块或一行。

<br>

#### 块引用
如果一个块级内容（若干个段落、列表等）被引用，使用`<blockquote>`元素标记，并在`<cite>`属性里用URL指向引用的资源。

`<cite>`是一个标注引用的信息的来源文档或者相关信息的URL。通常用来描述能够解释引文的上下文或者引用的信息。

```html
<blockquote cite="https://developer.mozilla.org/en-US/docs/Web/html/Element/blockquote">
<p>The <strong>html <code>&lt;blockquote&gt;</code> Element</strong> (or <em>html Block Quotation Element</em>) indicates that the enclosed text is an extended quotation.</p>
</blockquote>
```
浏览器在渲染块引用时默认会增加缩进，作为引用的一个指示符。

<br>

#### 行内引用
行内元素用同样的方式工作，除了使用`<q>`元素。
```html
<p>The quote element — <code>&lt;q&gt;</code> — is <q cite="https://developer.mozilla.org/en-US/docs/Web/html/Element/q">intended
for short quotations that don't require paragraph breaks.</q></p>
```
浏览器默认将其作为普通文本放入**引号**内表示引用。

<br>

#### 引文
cite属性内容不会被浏览器显示、屏幕阅读器阅读，需使用 JavaScript 或 CSS，浏览器才会显示cite的内容。如果你想要确保引用的来源在页面上是可显示的，更好的方法是为`<cite>`元素附上链接：
```html
<p>According to the 
<a href="https://developer.mozilla.org/en-US/docs/Web/html/Element/blockquote">
<cite>MDN blockquote page</cite>
</a>:
</p>
<blockquote cite="https://developer.mozilla.org/en-US/docs/Web/html/Element/blockquote">
<p>The <strong>html <code>&lt;blockquote&gt;</code> Element</strong> (or <em>html Block Quotation Element</em>) indicates that the enclosed text is an extended quotation.</p>
</blockquote>

<p>The quote element — <code>&lt;q&gt;</code> — is <q cite="https://developer.mozilla.org/en-US/docs/Web/html/Element/q">intended
for short quotations that don't require paragraph breaks.</q> -- <a href="https://developer.mozilla.org/en-US/docs/Web/html/Element/q">
<cite>MDN q page</cite></a>.</p>
```
引文默认的字体样式为斜体。

<br>

### 缩略语
缩略语`<abbr>`，它常被用来包裹一个缩略语或缩写，并提供缩写的解释（包含在`<title>`属性中）。
```html
<p>使用 <abbr title="超文本标记语言（Hyper text Markup Language）">html</abbr> 组织网页文档。</p>

<p>第 100 届 <abbr title="夏季奥林匹克运动会">奥运会</abbr> 将于 2200 年 12 月在火星举行。</p>
```

<br>

### 标记联系方式
用于标记文档编写者联系方式的元素——`<address>`。
```html
<address>
  <p>银河系太阳系火星HCY</p>
</address>
```
可以插入超链接。

<br>

### 上标和下标
- 下标：`<sub>`
- 上标：`<sup>`
两者是内联元素，需要闭合。

<br>

### 展示计算机代码
- `<code>`：用于标记计算机通用代码
- `<pre>`：用于保留空白字符（常用于代码块）。由于浏览器会忽略缩进和多余的空白，我们可以使用`<pre>`包裹空格。
- `<var>`：用于标记具体变量名。
- `<kbd>`：用于标记输入电脑的键盘（或其他类型）输入。
- `<samp>`：用于标记计算机程序的输入。

```html
<pre><code>const para = document.querySelector('p');

para.onclick = function() {
  alert('噢，噢，噢，别点我了。');
}</code></pre>

<p>请不要使用 <code>&lt;font&gt;</code> 、 <code>&lt;center&gt;</code> 等表象元素。</p>

<p>在上述的 JavaScript 示例中，<var>para</var> 表示一个段落元素。</p>


<p>按 <kbd>Ctrl</kbd>/<kbd>Cmd</kbd> + <kbd>A</kbd> 选择全部内容。</p>

<pre>$ <kbd>ping mozilla.org</kbd>
<samp>PING mozilla.org (63.245.215.20): 56 data bytes
64 bytes from 63.245.215.20: icmp_seq=0 ttl=40 time=158.233 ms</samp></pre>
```
![图片3](3.png)

<br>

### 标记时间和日期
将时间和日期标记为可供机器识别的格式——`<time>`元素
```html
<!-- 标准简单日期 -->
<time datetime="2021-10-30">2021年10月30日</time>
<!-- 只包含年份和月份-->
<time datetime="2021-10">October 2021</time>
<!-- 只包含月份和日期 -->
<time datetime="10-30">30 October</time>
<!-- 只包含时间，小时和分钟数 -->
<time datetime="21:08">21:08</time>
<!-- 还可包含秒和毫秒 -->
<time datetime="21:08:08.891">21:08:08.891</time>
<!-- 日期和时间 -->
<time datetime="2021-10-30T21:08">9.8pm, 30 October 2021</time>
<!-- 含有时区偏移值的日期时间 -->
<time datetime="2021-10-30T21:08+01:00">9.8pm, 30 October 2021 is 9.8pm in France</time>
<!-- 调用特定的周 -->
<time datetime="2021-W04">The fourth week of 2021</time>
```
time元素 提供了清晰的、可被机器识别的时间日期。

# 超链接
超链接是互联网的一个特性，它使互联网成为一个互联的网络。超链接使我们能够将自己的文档链接到任何其他文档，也可以链接到文档的指定部分。几乎任何网络内容都可以转化为链接（URL）。
> 注意：URL可以指向html文件、文本文件、图像、文本文档、视频和音频文件以及可以在网络上保存的任何其他内容。<br>
> 如果浏览器不知道如何显示或处理文件，它会询问用户是否打开文件（使用本地应用）或下载文件。

<br>

## 链接的创建
**通过将文本或其它内容（块级链接）转化为`<a>`元素内的链接来创建基本链接，在`href`属性内包含你想指向的网址。**
```html
<p>这是一个
<a href="https://www.bilibili.com">B站</a>
的超链接。</p>
```

<br>

**`<a>`元素中还可以添加一个显示标题的属性，它可以补充关于链接的信息。**
```html
<p>这是一个
<a href="https://www.bilibili.com" title="一个适用于娱乐和学习的网站">B站</a>
的超链接。</p>
```
效果：*[B站](https://www.bilibili.com "一个适用于娱乐和学习的网站")*

<br>

**块级链接**
除了可以将文本内容转换为链接，*块级元素*也可以转化为超链接。<br>
例如，将一张图片转化为链接：
```html
<a href="https://www.bilibili.com">
  <img src="bilibili-image.png" alt="链接至 B站 的图片">
</a>
```

<br>

## 电子邮件链接
当点击一个链接或按钮时，打开一个新的电子邮件发送信息。使用`<a>`元素和`mailto:URL方案`。<br>
其最基本和最常用的使用形式为一个`mailto:link`（链接），链接简单说明收件人的电子邮件地址。例如:
```html
<a href="mailto:nowhere@example.com">发送一个邮件</a>
```
当`mailto:`后没有内容，用户的邮件客户端会打开一个新的发送邮件的窗口；这种特性可以在“分享”链接中使用，用户选择邮件地址分享内容。

***除了电子邮件地址，您还可以提供其他信息。***<br>
事实上，任何标准的邮件头字段可以被添加到你提供的邮件URL。 其中最常用的是主题(subject)、抄送(cc)和主体(body) (这不是一个真正的头字段，但允许您为新邮件指定一个短内容消息)。 每个字段及其值被指定为查询项。
```html
<a href="mailto:nowhere@mozilla.org?cc=name2@rapidtables.com&bcc=name3@rapidtables.com&subject=The%20subject%20of%20the%20email&body=The%20body%20of%20the%20email">
Send mail with cc,bcc,subject and body
</a>
```
> 每个字段的值必须是URL编码的。 也就是说，不能有非打印字符（不可见字符比如制表符、换行符、分页符）和空格。同时注意使用问号（?）来分隔主URL与参数值，以及使用&符来分隔`mailto:`中的各个参数。这是标准的URL查询标记方法。

<br>

## 统一资源定位器和路径入门
URL和path是全面链接连接目标的需要。

统一资源定位符（英文：Uniform Resource Locator，简写：URL）是定义了在网络上的位置的一个文本字符串。

URL使用路径查找文件。路径指定文件系统中所有文件的位置。

<a id="img2">![图片二](2.png)</a>
在网站工作时，用户会有整个网站的目录。在根目录中，`index.html`将会成为网站的主页或登录页面。

在根目录下，有categories和tags目录，它们包含一个`index.html`文件。因为它们在不同的目录下，可能是项目相关信息的主页面。

- **指向当前目录**：只需指定想要链接的文件名。
- **指向子目录**：通过目录名称和正斜杠指定文件路径，最后再指定文件名。
- **指向上级目录**：两个英语点号——`..`——表示*返回上一级目录*。

<br>

### 文档片段
超链接除了可以连接到文档外，还可以链接到文档中的特定部分（即文档片段）。<br>
首先，给想要链接的元素分配一个`id`属性。
```html
<h1 id="mail_address">邮寄地址</h1>
```
在URL的结尾使用一个井号链接到元素id<br>
不同的文档下：
```html
<p>请将信件寄至<a href="mails.html#mail_address">我的地址</a>。</p>
```
同一文档下：
```html
<p>请将信件寄至<a href="#mail_address">我的地址</a>。</p>
```

<br>

### 绝对url和相对url
**绝对URL**：指向由其在Web上的绝对位置定义的位置，包括协议和域名。
用上面的[网站](#img2)举例，有一个index.html页面在categories目录下，web站点的域名为https://a-pin.github.io，那么这个页面就可以通过https://a-pin.github.io/categories/index.html访问；或者通过https://a-pin.github.io/categories/来访问，因为在没有指定特定的URL的情况下，大多数web服务会默认访问加载index.html这类页面。

**相对URL**：指向与您链接的文件相关的位置，更像我们在前面一节中所看到的位置。一个相对URL将指向不同的位置，这取决于它所在的文件所在的位置。

<br>

<br>

<br>

使用超链接时，你应该注意的：
> - 使用清晰的连接措辞；不要重复将URL作为链接文本的一部分，不要把“链接”、“链接到”放到链接文本中，尽量使链接标签尽可能的短。
> - 尽可能使用相对链接；当链接在同一网站的其他位置时，使用相对链接。<br>
  当使用绝对URL时，浏览器首先通过DNS查找服务器的真实位置，然后再转到该服务器并查找所请求的文件，这代表你的浏览器会不断地做额外工作。
> - 链接到非html资源；当链接到一个要下载的资源或流媒体或具有意想不到的效果的资源，你应该添加明确的信息。<br>
  在下载链接时使用download属性：提供一个默认的保存文件名（仅适用于同源URL）。


```html
<a href="https://download.mozilla.org/?product=firefox-latest-ssl&os=win64&lang=zh-CN" download="firefox-latest-64bit-installer.exe">下载最新的Firefox 中文版-Windows（64位）</a>
```

<br>

# 文档与网站架构
html不仅能定义网页的单独部分，还可以使用块级元素（标题栏、导航菜单、主内容列）来定义网站中的复合区域。

<br>

## 文档的基本组成部分
网页的外观多种多样，但都倾向使用类似的标准组件。

- **页眉**<br>
  通常横跨于整个页面顶部有一个大标题和一个标志。这是网站的主要一般信息，通常存在于所有网页。
- **导航栏**<br>
  指向网站各个主要区段的超链接。通常用菜单按钮、链接或标签页表示。
- **主内容**<br>
  中心的大部分区域是当前网页大多数的独有内容。
- **侧边栏**<br>
  一些外围信息、链接、引用、广告等。通常与主内容相关，可能存在其他的重复元素，如辅助导航系统。
- **页脚**<br>
  横跨页面底部的狭长区域。和标题一样，页脚是放置公共信息的，一般使用较小字体，且通常为次要内容。

![图片4](4.png)

<br>

## 用于构建内容的html
通过合适的CSS，可以使用相当多种的任意页面元素来环绕在不同的页面区域来做成你想要的样子——**我们要敬畏语义，正确选用元素**。

视觉效果不是一切，我们可以修改一些内容来吸引用户的注意，但这些对视障人士是没用的。
[全球视障人数!](https://www.who.int/zh/news/item/08-10-2019-who-launches-first-world-report-on-vision)

html代码可以根据功能来为区段添加标记，使用元素来无歧义地表示内容区段，屏幕阅读器等辅助技术可以识别这些元素。

区段的专用标签：
- `<header>`：页眉
- `<nav>`：导航栏
- `<main>`：主内容
  - `<article>`
  - `<section>`
  - `<div>`
- `<aside>`：侧边栏，常嵌在`<main>`中
- `<footer>`：页脚

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>二次元俱乐部</title>
    <link href="https://fonts.googleapis.com/css?family=Open+Sans+Condensed:300|Sonsie+One" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css?family=ZCOOL+KuaiLe" rel="stylesheet">
    <link href="style.css" rel="stylesheet">
  </head>

  <body>
    <header> <!-- 本站所有网页的统一主标题 -->
      <h1>聆听电子天籁之音</h1>
    </header>

    <nav> <!-- 本站统一的导航栏 -->
      <ul>
        <li><a href="#">主页</a></li>
        <!-- 共n个导航栏项目，省略…… -->
      </ul>

      <form> <!-- 搜索栏是站点内导航的一个非线性的方式。 -->
        <input type="search" name="q" placeholder="要搜索的内容">
        <input type="submit" value="搜索">
      </form>
    </nav>

    <main> <!-- 网页主体内容 -->
      <article>
        <!-- 此处包含一个 article（一篇文章），内容略…… -->
      </article>

      <aside> <!-- 侧边栏在主内容右侧 -->
        <h2>相关链接</h2>
        <ul>
          <li><a href="#">这是一个超链接</a></li>
          <!-- 侧边栏有n个超链接，略略略…… -->
        </ul>
      </aside>
    </main>

    <footer> <!-- 本站所有网页的统一页脚 -->
      <p>© 2050 某某保留所有权利</p>
    </footer>
  </body>
</html>
```

<br>

## html布局元素细节
理解所有html区段元素具体含义是很有益处的，更多细节请查阅 [html 元素](https://developer.mozilla.org/zh-CN/docs/Web/html/Element)参考。

以下是主要元素的意义：
- `<main>`存放网页主要内容，它是每个页面的独有内容。每个页面只能用一次main元素，且直接位于`<body>`中。
- `article`包围的内容即一篇文章，与页面其他内容无关。
- `<section>`用于组织页面使其按功能分块。
- `<aside>`包含一些间接信息。
- `<header>`是简介形式的内容。如果它是`<body>`的子元素，那么就是网站的全局页眉。
- `<nav>`包含页面主导导航功能。
- `<footer>`包含页面的页脚部分。

<br>

### 无语义元素
对于一些要组织的项目或要包装的内容，现有的语义元素均不能很好对应。

可能只想将一组元素作为一个单独的实体来修饰来响应单一的 CSS 或 JavaScript。为了应对这种情况，html提供了 `<div>` 和 `<span>` 元素。应配合使用 class 属性提供一些标签，使这些元素能易于查询。

`<span>` 是一个**内联**的无语义元素，最好只用于无法找到更好的语义元素来包含内容时，或者不想增加特定的含义时。
```html
<p>警察气的浑身发抖，大步走出门。<span class="editor-note">[编辑批注：警察从没见过这种人]</span></p>
```

`<div>` 是一个**块级**无语义元素，应仅用于找不到更好的块级元素时，或者不想增加特定的意义时。例如，一个电子商务网站页面上有一个一直显示的购物车组件。
```html
<div class="shopping-cart">
  <h2>购物车</h2>
  <ul>
    <li>
      <p><a href=""><strong>银耳环</strong></a>：$99.95.</p>
      <img src="../products/3333-0985/" alt="Silver earrings">
    </li>
    <li>
      ...
    </li>
  </ul>
  <p>售价：$237.89</p>
</div>
```
这里不应使用 `<aside>`，因为它和主内容并没有必要的联系（你想在任何地方都能看到它）；甚至不能用 `<section>` ，因为它也不是页面上主内容的一部分。
> `<div>`没有语义值，会使html代码变得混乱，要小心使用。

<br>

### 换行与水平分割线
`<br>` 可在段落中进行换行；
`<br>` 是唯一能够生成多个短行结构（例如邮寄地址或诗歌）的元素。比如：
```html
<p>我有一个恋爱——<br>
我爱天上的明星；<br>
我爱它们的晶莹：<br>
人间没有这异样的神明。</p>
```

`<hr>` 元素在文档中生成一条水平分割线，表示文本中主题的变化（例如话题或场景的改变）。一般就是一条水平的直线。例如：
```html
<p>市场东边是斗狮场，还可以看见大概的规模；在许多宏壮的废墟里，这个算是情形最好的。外墙是一个大圆圈儿，分四层，要仰起头才能看到顶上。</p>
<hr>
<p>下三层都是一色的圆拱门和柱子，上一层只有小长方窗户和楞子，这种单纯的对照教人觉得这座建筑是整整的一块，好像直上云霄的松柏，老干亭亭，没有一些繁枝细节。</p>
```

<br>

## 规划一个简单的网站
> 声明，以下这些信息和方法都来自mozilla的[html教程](https://developer.mozilla.org/zh-CN/docs/Learn/html/Introduction_to_html/Document_and_website_structure)

在完成页面内容的规划后，一般应按部就班地规划整个网站的内容，要可能带给用户最好的体验，需要哪些页面、如何排列组合这些页面、如何互相链接等问题不可忽略。这些工作称为**信息架构**。

对于一个只有几个页面的简单网站，规划设计过程可以更简单，更有趣！

1. 时刻记住，大多数（不是全部）页面会使用一些相同的元素，例如导航菜单以及页脚内容。若网站为商业站点，不妨在所有页面的页脚都加上联系方式。请记录这些对所有页面都通用的内容：
![图片5](5.png)
2. 接下来，可为页面结构绘制草图（这里与前文那个站点页面的截图类似）。记录每一块的作用：
![图片6](6.png)
3. 下面，对于期望添加进站点的所有其它（通用内容以外的）内容展开头脑风暴，直接罗列出来。
![图片6](7.png)
4. 下一步，试着对这些内容进行分组，这样可以让你了解哪些内容可以放在同一个页面。这种做法和 卡片分类法 非常相似。
![图片7](8.png)
5. 接下来，试着绘制一个站点地图的草图，使用一个气泡代表网站的一个页面，并绘制连线来表示页面间的一般工作流。主页面一般置于中心，且链接到其他大多数页面；小型网站的大多数页面都可以从主页的导航栏中链接跳转。也可记录下内容的显示方式。
![图片8](9.png)

<br>

# html调试
介绍查找和修复html错误的工具。

浏览器不会将html编译成其他形式，而是直接解析并显示结果（解释）。相比其他编程语言的编译运行，浏览器解析html的过程更**宽松**。

两种主要类型的错误：
- **语法错误**：由于拼写错误导致程序无法运行
- **逻辑错误**：不存在语法错误，但代码无法按预期运行

html不容易出现语法错误，浏览器是以宽松模式运行的，这意味着即使出现语法错误浏览器依旧会继续运行。浏览器有**内建规则**解析书写错误的标记。
> Web创建的初心就是：人人可以发布内容，不必纠结代码语法。因此html以宽松的方式解析。

保持良好的html格式相当重要。但是一个非常庞大、复杂的html文档需要查找错误，要怎么做呢？<br>
最好的方法就是让你的html页面通过[Markup Validation Service](https://validator.w3.org/)。由W3C（制定html、CSS和其它网络技术标准的组织）创立并维护的标记验证服务。把一个html文档加载至W3C页面并运行，网页会返回一个错误报告——接受网址、html文档、或直接输入一些html代码。

<br>

<br>
