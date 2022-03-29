---
title: CSS第一步
description: 本文主要目的是让你对于CSS有一个大概的认识！以方便之后CSS的学习。
tags: 
categories:
  - mdn
    - CSS
---

在此特地声明本文是根据 [mozilla官方教学文档](https://developer.mozilla.org/zh-CN/docs/Learn/html/Introduction_to_html) 学习的个人学习笔记，借用了大量的图片和文本内容，存在相当多的相同，但不是copy。如需查看mozilla官方文档，请点击前文链接！！
<!--more-->

<br>

CSS（层叠样式表）用于设置和布置网页——例如，更改内容的字体，颜色，大小和间距，将其拆分为多个列，或添加动画和其他装饰功能。<br>
接下来，将为你掌握CSS准备一个良好的开端。

<br>

# 什么是css
在纯HTML页面中，浏览器可以解析页面并把它们显示出来。比如，标题部分看起来会比正常文本大，段落会另起一行并保持一定距离，链接通过下划线和不同颜色与其他文本区分开来，这些都是浏览器的默认样式。

但是如果所有网站都是纯HTML的话，互联网就会非常枯燥也有可能影响到阅读效率。而CSS可以完全控制浏览器如何显示HTML元素，从而充分展示你喜欢的设计样式。

<br>

## css用来干什么
CSS是用来指定文档如何展示给用户的一门语言——如网页的样式、布局等等。
一份文档是由标记语言组织起来的文本文件，而展示一份文档给用户实际上是将文档变成用户可用的文件，即浏览器都可以将文档在电脑屏幕等设备上进行可视化。

CSS可以用于给文档添加样式，也可用于创建布局，甚至可以做一些特效——例如动画。

> 注意：当我们在讨论CSS时，浏览器是user agent的主要形式。用户代理（user agent）代表一个人的计算机程序，例如，一个在 Web 上的 浏览器。

<br>

## css语法
CSS是一门基于规则的语言——你能定义用于你的网页中特定元素样式的一组规则。

将主标题变红变大：
```css
h1 {
    color: red;
    font-size: 5em;
}
```

语法由一个选择器起头，选择了我们将要用来添加样式的HTML元素。在上面代码中，选择的是一级标题。

接着输入一对大括号`{}`。在大括号内部定义一个或多个形式为 `属性(property): 值(value);` 的声明。每个声明都指定了我们所选择元素的一个属性，之后跟一个我们想赋给这个属性的值。

不同的CSS属性对应不同的合法值。例如 color 属性，可以接受许多颜色值；还有 font-size 属性，可以接受许多 [size units](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Values_and_units#numbers_lengths_and_percentages) 值。

在MDN上每个属性都有单独的页面，可以帮助你使用CSS。另外，当你想查找一个CSS特性的更多内容时，可以使用你的搜索引擎来搜索 `mdn css-feature-name` 。例如 “mdn color”和“mdn font-size”。

<br>

## css模块
CSS由许多 *模块(modules)* 构成，包含多个属性。

你可以在MDN上浏览这些模块的参考内容，也可以查看 CSS规范。比如，我可以查找一下 MDN reference 的 Backgrounds and Borders 模块的相关内容，来了解**它是用来做什么的**、**它还包括什么属性**、**它还有什么其它特性**等。

举个具体点的例子：如上文中的 Backgrounds and Borders 模块 — 你会发现 `background-color` 和 `border-color` 这两个属性在逻辑上相通。

<br>

**CSS规范**<br>
所有的标准web技术（HTML、CSS、JS等）都被定义在一个巨大的文档中，称作 规范（specifications,即specs），它是由（W3C,WHATWG,ECMA或Khronos)这些规范化组织所发布的，其中定义了各种技术是如何工作的。

CSS规范 旨在为工程师在用户代理(user agents)中实现对 CSS 各种特性的支持，而不是作为一本为Web开发者理解 CSS 内容的教程。

CSS 也不例外——它是由W3C(万维网联盟)中的一个名叫 CSS Working Group 团体发展起来的。这个团体是由浏览器厂商和其他公司中对 CSS 感兴趣的人作为代表组成的。也有其他的人员，比如受邀专家，他们作为不从属于任何组织的独立声音加入团体。

新的 CSS 特性被开发出来，或是因为某个浏览器热衷于开发新功能，或是因为Web设计人员与开发者要求增加一个新特性，又或是 CSS Working Group 内部的讨论决定。CSS 始终在发展，并伴随着新的特性。然而，有一件事情从始至终都未改变，那就是**不让新的改变破坏旧的网站**，即使是2000年建立的网站，如今也能正常访问！

<br>

## 浏览器支持

![](1.png)

当一个浏览器支持 CSS 后，我们就可以用它来进行Web开发了。这意味着我们写在 CSS 文件中的代码可以被指令执行，展示到荧幕中。

让所有的浏览器都同时支持一个 CSS 新特性是不现实的，通常都会一个空档期——一些浏览器已经支持而另一些仍未支持。因此，查看新特性的实现状态(implementation status)是非常有用的。在 MDN 上的每个属性的页面中都标有它们对应的状态，你可以通过这种方法来查看你是否可以去使用它。

<br>

# 开始css之旅
在这部分内容中，我将会拿一个简单的HTML文档做例子，并且在里面使用CSS样式。

<br>

## 从html开始
先以HTML文档展开叙述。
```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>开始学习CSS</title>
</head>

<body>

    <h1>我是一级标题</h1>

    <p>这是一个段落文本. 在文本中有一个 <span>span element</span>
并且还有一个 <a href="http://example.com">链接</a>.</p>

    <p>这是第二段. 包含了一个 <em>强调</em> 元素.</p>

    <ul>
        <li>项目1</li>
        <li>项目2</li>
        <li>项目 <em>三</em></li>
    </ul>

</body>

</html>
```

将改HTML文档保存并在相同目录下创建文件 styles.css 。

<br>

## 添加css试试
如果想使HTML文档遵循给定的CSS规则，其中有三种方式可以实现。

其中利用最普遍最有效的是 在文档的开头链接CSS。为了把 styles.css 和 index.html 连接起来，可以在 HTML文档 中，`<head>`语句模块里面加上下面的代码：
```html
<link rel="stylesheet" href="styles.css">
```

- 在 link 语句块里面，我们用属性 rel ，让浏览器知道有CSS文档存在，并利用属性 href 指定，寻找CSS文件的位置。

<br>

每个浏览器都自带一个包含默认样式的样式表，默认对任何页面都有效。当你不想使用默认样式时，你可以使用CSS更改默认样式——选定需更改的元素，加上一条CSS规则即可。

在 styles.css 文件中添加CSS样式并观察显示的结果：
```css
h1 {
    color: red;
}
```

效果如下：

![](2.png)

<br>



同样，可以实现剔除无序列表`<ul>`自带的项目符号：
```css
li {
    list-style-type: none;
}
```

<br>

## 样式化html元素
通过上一节将大标题变成红色的例子，我们已经展示了我们可以选中并且样式化 HTML 元素。<br>
我们通过触发**元素选择器**实现这一点——元素选择器，即直接匹配 HTML元素 的选择器。

例如，若要样式化一个文档中所有的段落，只需使用选择器 p 。若要将所有段落变成绿色，你可以利用如下方式：
```css
p {
    color: green;
}
```
用逗号将不同选择器隔开，即可一次使用多个选择器。譬如，将所有段落、列表变成绿色：
```css
p, li {
    color: green;
}
```

<br>

### 使用类名
目前为止，我们通过HTML元素名规定样式。这样子会使所有的元素都一样，而实际上我们想要应用不同的样式到同一类型的元素上。

你可以给HTML元素加个类名（class），再选中这个类名。

这是一个列表：
```html
<ul>
    <li>项目一</li>
    <li class="special">项目二</li>
    <li>项目 <em>三</em></li>
</ul>
```

在CSS中，选中这个 special 类，只需在选择器的开头加个英文句号（.）：
```css
.special {
    color: orange;
    font-weight: bold;
}
```

- 上面的CSS规则中，special类不只局限于列表。而是所有special类的元素。

在选择器中，元素选择器和类名可以一起出现：
```css
li.special {
    color: orange;
    font-weight: bold;
}
```

- 即“选中每个 special类 的 li元素 ”。也就是说规定了 special类 的选择范围，不会随便选择其它元素的 special类。

同样的，你可以这样：
```css
li.special,
span.special {
    color: orange;
    font-weight: bold;
}
```

<br>

### 根据元素在文档中的位置确定样式
有时候，你希望某些内容根据它在文档中的位置而有所不同。CSS有许多选择器可以使用，这里介绍几种选择器。

在我们HTML文档中有两个`<em>`元素——一个在段落中，另一个在列表项内。
```html
<h1>I am a level one heading</h1>

<p>This is a paragraph of text. In the text is a <span>span element</span> 
and also a <a href="http://example.com">link</a>.</p>

<p>This is the second paragraph. It contains an <em>emphasized</em> element.</p>

<ul>
    <li>Item <span>one</span></li>
    <li>Item two</li>
    <li>Item <em>three</em></li>
</ul>
```

仅选择嵌套在`<li>`元素内的`<em>`我们可以使用一个称为**包含选择符**的选择器，它只是单纯的在两个选择器之间加上一个空格。

将以下规则添加到样式表:
```css
li em {
    color: rebeccapurple;
}
```

- 该选择器将选择 li 内部的任何 em 元素（即 li 的后代）。

另一个是 在HTML文档中设置直接出现在标题后面并且与标题具有相同层级的段落样式，为此需在两个选择器之间添加一个 “+” 号（成为 **相邻选择符**）。

将这个规则添加到样式表中：
```css
h1 + p {
    font-size: 200%;
}
```

- 这个规则只会修改与标题同级的下一个段落（只会修改一个段落）。

而下面的规则是修改 下下个段落 ——上面那个规则要修改的下一个段落——而不是两个都修改。
```css
h1 + p + p{
    font-size: 200%;
}
```

<br>

### 根据状态确定样式
根据标签的状态确定样式。一个直观的例子就是当我们修改链接的样式时：当定位`<a>`标签后，对链接的修改取决于链接不同的状态——未访问的、访问过的、被鼠标悬停的、被键盘定位的或正在被点击。你可以使用CSS去定位这些不同的状态进行修饰。

使没被访问的链接颜色为粉色，访问过的变为绿色：
```css
a:link {
    color: pink;
}

a:visited {
    color: green;
}
```

类似的，改变链接被鼠标悬停时的样式，例如 移除下划线：
```css
a:hover {
    text-decoration: none;
}
```

你可以修改链接在任何时候都没有下划线，但一个好的网页需要让浏览者知道什么时链接。这样做会导致文档在添加CSS样式后，反而变得更加不清晰，不易浏览。实际上，我们使用CSS的目的之一就有使网页变得更加清晰明了。

> **注意**：我们的网页应当让每一个访客都能够理解、使用，在这里总结为“无障碍”。
> 
> 一个朴素的HTML文档一般来说对任何人都是可以无障碍访问的，当我们使用CSS为它添加样式，不要破坏这种可访问性。

<br>

### 同时使用选择器和选择符
```css
body h1 + p .special {
  color: yellow;
  background-color: black;
  padding: 5px;
}
```

效果如下：

![](3.png)

<br>

# 如何构建css
这部分关于语言本身的结构，会提及到很多概念。如果在之后学习中对一些概念有问题的话，可以回到这一部分回顾一下。

<br>

## 在html中应用css
在文档中应用css的三种方法。

<br>

### 外部样式表
在**开始css之旅**部分中，我们将外部样式表链接到页面。这是将css附加到文档中最常见和最有用的方法，因为这样可以将一个css应用到多个页面（有点类似于动态链接库了——最近有看一些二进制的内容）。在大多数情况下，一个站点的不同页面看起来几乎都是一样的，因此你可以使用相同的**规则集**来获得**基本的外观**。

外部样式表是指将CSS编写在扩展名为`.css`的单独文件中，并将HTML`<link>`元素引用它的情况：
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>My CSS experiment</title>
        <link rel="stylesheet" href="styles.css">
    </head>
    <body>
        <h1>Hello World!</h1>
        <p>This is my first CSS example</p>
    </body>
</html>
```
CSS文件如下：
```css
h1 {
    color: blue;
    background-color: yellow;
    border: 1px solid black;
}
p {
    color: red;
}
```
link 元素的 href 属性需要引用你的文件系统中的一个文件。

在上面的例子中，css文件和html文档在同一文件夹中，但你可以把css文件放在其他地方，并调整指定的路径以匹配：
```html
<!-- Inside a subdirectory called styles inside the current directory -->
<link rel="stylesheet" href="styles/style.css">

<!-- Inside a subdirectory called general, which is in a subdirectory called styles, inside the current directory -->
<link rel="stylesheet" href="styles/general/style.css">

<!-- Go up one directory level, then inside a subdirectory called styles -->
<link rel="stylesheet" href="../styles/style.css">
```

<br>

### 内部样式表
内部样式表是指不使用外部css文件，而是将css放在html文件 `<head>` 标签里的 `style` 标签之中。

比如：
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>My CSS experiment</title>
    <style>
      h1 {
        color: blue;
        background-color: yellow;
        border: 1px solid black;
      }

      p {
        color: red;
      }
    </style>
  </head>
  <body>
    <h1>Hello World!</h1>
    <p>This is my first CSS example</p>
  </body>
</html>
```
有的时候，这种方法会比较有用（比如你使用的内容管理系统不能直接编辑CSS文件），但该方法和外部样式表比起来更加低效。

<br>

### 内联样式
内联样式表存在于HTML元素的style属性之中。其特点是每个CSS表只影响一个元素：
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>My CSS experiment</title>
    </head>
    <body>
        <h1 style="color: blue;background-color: yellow;border: 1px solid black;">Hello World!</h1>
        <p style="color:red;">This is my first CSS example</p>
    </body>
</html>
```
**尽量别这么做！**它难以维护，并且这种方法将文档结构和文档修饰混合起来了，这会使代码变得难以阅读和理解。

但是在某些地方，内联样式更常见，甚至可取。它长时间被应用在HTML电子邮件中，以便与尽可能多的电子邮件客户端兼容。

<br>

## 选择器
为了样式化某些元素，我们会通过选择器来选中HTML文档中的这些元素。一般情况下，你的样式没有生效，就很有可能是你的选择器没有像你预想的那样选中元素。

每个CSS规则都是以一个选择器或一组选择器为开始，去告诉浏览器这些规则应该应用到哪些元素上——在上文的教程中我们已经列举了一些不同的选择器。

以下是有效的选择器或组合选择器的示例：
```css
h1
a:link
.manythings
#onething
*
.box p
.box p:first-child
h1, h2, .intro
```

<br>

**专一性**
通常情况下，两个选择器可以选择相同的HTML元素。

指向同一元素的选择器：
```css
.special {
    color: red;
}
p {
    color: blue;
}
```
```html
<p class="special">What color am I?</p>
```
**最后，这个段落会变成什么颜色？**
CSS语言有规则来控制在发生碰撞时哪条规则将获胜——这些规则称为**级联规则**和**专用规则**。

在下面代码中，我们为p选择器定义了两个规则，但是段落最后是蓝色的。这是因为将其设置为蓝色的声明将出现在样式表的后面，而稍后的样式将覆盖以前的样式。
```css
p {
    color: red;
}

p {
    color: blue;
}
```

但是，在我们同时使用了类选择器和元素选择器的例子中，类将获胜，使得段落变红。一个类被描述为比元素选择器更具体，或者具有更多的特异性，所以它获胜了。有时CSS可能不会像您预期的那样应用，因为样式表中的其他内容具有更高的特异性。

<br>

## 属性和值
在最基础的层面上，CSS由两个组成部分组成：
- **属性**：人可读的标识符，指示你想要更改的样式特征。
- **值**：每个指定的属性都有一个值，该值指示你希望如何更改这些样式特征。

下面的图像突出显示单个属性和值。属性名为 color ，值为 blue 。

![](4.png)

与值配对的属性称为CSS声明。CSS声明放在CSS声明块中。下一张图片显示了我们的CSS，并突出显示了声明块。

![](5.png)

最后，CSS声明块与选择器配对，以生成CSS规则集（或CSS规则）。

![](6.png)

> 在css中，**属性**和**值**是区分大小写的。<br>
> 如果属性未知或某个值对给定属性无效，则声明视为无效，被浏览器的CSS引擎完全忽略。<br>

<br>

**函数**

虽然大多数值是相对简单的关键字或数值，但也有一些可能的值以函数的形式出现。

这是一个 calc() 函数，它允许你在CSS中进行简单的计算：
```html
<div class="outer"><div class="box">The inner box is 90% - 30px.</div></div>
```
```css
.outer {
  border: 5px solid black;
}

.box {
  padding: 10px;
  width: calc(90% - 30px);
  background-color: rebeccapurple;
  color: white;
}
```
效果如下：

![](7.png)

一个函数由函数名和一些括号组成，其中放置了该函数的允许值。在上面的 calc() 示例中，我要求此框的宽度为包含块宽度的90%，减去30像素。这不是我们可以提前计算的东西，只是在CSS中输入值，因为我不知道90%会是什么。

另一个例子是`<transform>`，例如`rotate()`：
```html
<div class="box"></div>
```
```css
.box {
    margin: 30px;
    width: 100px;
    height: 100px;
    background-color: rebeccapurple;
    transform: rotate(0.8turn);
}
```

![](8.png)

<br>

## @规则
`@rules` 是一种特殊的规则，为CSS提供了一些关于如何表现的指导。

有些 @rules 规则很简单，有规则名和值。例如，将额外的样式表导入主CSS样式表，可以使用 `@import`：
```css
@import 'styles2.css';
```

另一个@规则是 `@media`，它允许你使用 媒体查询 来应用CSS——仅当某些条件成立（例如，当屏幕分辨率高于某一数量，或屏幕宽度大于某一宽度时）。

在下面的CSS中，我们将给 `<body>` 元素一个粉红色的背景色。但是，我们随后使用 @media 创建样式表的一部分，该部分仅适用于视口大于30em的浏览器。如果浏览器的宽度大于30em，则背景色将为蓝色。
```css
body {
    background-color: pink;
}
@media (min-width: 30em) {
    body {
        background-color: blue;
    }
}
```
在这些教程中，你将遇到一些其他的规则 @rules

查看是否可以将媒体查询添加到CSS中，该查询将根据视口宽度更改样式。更改浏览器窗口的宽度以查看结果。

<br>

## 速记属性
一些属性，如 `font`,`background`,`padding`,`border` 和 `margin` 等属性称为速记属性——这是因为它们允许你在一行中设置多个属性值，从而节省时间并使代码更整洁。

例如：
```css
padding: 10px 15px 15px 5px;
```
和下面四行代码是等价的：
```css
padding-top: 10px;
padding-right: 15px;
padding-bottom: 15px;
padding-left: 5px;
```

这一行：
```css
background: red url(bg-graphic.png) 10px 10px repeat-x fixed;
```

与这五行代码是等价的：
```css
background-color: red;
background-image: url(bg-graphic.png);
background-position: 10px 10px;
background-repeat: repeat-x;
background-attachment: fixed;
```

> 警告：速记允许忽略值，并且会将不包含值的部分重置为它们的初始值。这确保使用了一组合理的值。但是，如果你希望速记只更改传入的值，就会导致问题。

<br>

## 注释
CSS中的注释以 '/*' 开头，以 '*/' 结尾。

在下面的代码块中，注释标记了不同代码节的开始。当代码库变得更大时，这对于帮助您导航代码库非常有用——在代码编辑器中搜索注释可以高效地定位代码节。
```css
/* Handle basic element styling */
/* -------------------------------------------------------------------------------------------- */
body {
  font: 1em/150% Helvetica, Arial, sans-serif;
  padding: 1em;
  margin: 0 auto;
  max-width: 33em;
}

@media (min-width: 70em) {
  /* Let's special case the global font size. On large screen or window,
     we increase the font size for better readability */
  body {
    font-size: 130%;
  }
}

h1 {font-size: 1.5em;}

/* Handle specific elements nested in the DOM  */
/* -------------------------------------------------------------------------------------------- */
div p, #id:first-line {
  background-color: red;
  border-radius: 3px;
}

div p{
  margin: 0;
  padding: 1em;
}

div p + p {
  padding-top: 0;
}
```
在CSS中，像其它编程语言一样，测试中可以 注释掉 一段代码来禁用他们。

> 空白是指实际空格、制表符和换行。和HTML相同，浏览器往往忽略CSS中的大部分空白，许多空白只是为了提高可读性。

<br>

# css如何运行
浏览器如何获取CSS、HTML和将它们加载成网页？

<br>

## css是怎么工作的
当浏览器展示一个文件时，必须兼顾文件的内容和文件的样式信息。

以下是浏览器处理文件的基本流程，不同的浏览器可能不同：
1. 浏览器载入HTML文件。
2. 将HTML文件转化为一个DOM（Document Object Model），DOM是文件在计算机内存中的表现形式。
3. 接下来，浏览器会拉取该HTML相关的大部分资源，比如嵌入到页面的图片、视频和CSS样式，而JavaScript则会稍后进行处理。
4. 浏览器拉取到CSS之后会进行解析，根据选择器的不同类型（比如element、class、id等）把他们分到不同的“桶”中。浏览器基于它找到的不同的选择器，将不同的规则应用在对应的DOM的节点中，并添加节点依赖的样式（这个中间步骤称为渲染树）。
5. 上述的规则应用于渲染树之后，渲染树会依照应该出现的结构进行布局。
6. 网页展示在屏幕上（称为 着色）。

![](9.png)

<br>

## 关于DOM
一个DOM有一个树形结构，标记语言中的每一个元素、属性以及每一段文字都对应着结构树中的一个节点。

节点由节点本身和其他DOM结点的关系定义，有些节点有父节点，有些节点有兄弟节点。

对于DOM的理解会很大程度上帮助你设计、调试和维护你的CSS，因为DOM是你的CSS样式个文件内容的结合。

下面是HTML代码：
```html
<p>
  Let's use:
  <span>Cascading</span>
  <span>Style</span>
  <span>Sheets</span>
</p>
```

在这个DOM中，p 元素对应了父节点，它的子节点是一个 text 节点和三个对应了 span 元素的节点，span 节点同时是它们中的 text 节点的父节点。
```txt
P
├─ "Let's use:"
├─ SPAN
|  └─ "Cascading"
├─ SPAN
|  └─ "Style"
└─ SPAN
   └─ "Sheets"
```

浏览器生成以上的DOM树形结构并将它输出到浏览器。

<br>

## 应用css到DOM
接下来，添加一些CSS到文件里加以渲染：
```css
span {
  border: 1px solid black;
  background-color: lime;
}
```

在浏览器解析HTML创造DOM后，会解析CSS，并将CSS规则应用到元素上，然后渲染出图像到屏幕上。

**当浏览器遇到无法解析的CSS代码会发生什么？**
浏览器不一定会解析所有的CSS——发生冲突、浏览器不支持。那么，当浏览器遇到无法解析的CSS选择器或声明的时候会发生什么？

答案就是 浏览器什么都不会做，继续解析下一个CSS样式！

- 如果你使用最新的CSS优化，浏览器遇到无法解析的规则也不会报错。<br>
- 当你为一个元素指定多个CSS样式的时候，浏览器会加载样式表中的最后的CSS代码进行渲染。（如此你可以为同一个元素指定多个CSS样式来解决有些浏览器不兼容新特性的问题）

例如，在你想使用一个很新的CSS特性但是不是所有浏览器都支持的时候。一些老的浏览器不接收`calc()` 作为一个值（ CSS3 新增，为元素指定动态宽度、长度等，此处的动态是指计算之后得到一个确切的值）。

如下，定义了 calc 实现动态宽度。老式的浏览器由于无法解析忽略这一行；新式的浏览器则会把这一行解析成像素值，并且覆盖第一行指定的宽度。
```css
.box {
  width: 500px;
  width: calc(100% - 50px);
}
```