---
title: JavaScript第一步
description: 本文主要目的是让你对于JavaScript有一个大概的认识！以方便之后的学习。
tags: 
categories:
  - mdn
	- JavaScript
---

在此特地声明本文是根据 [mozilla官方教学文档](https://developer.mozilla.org/zh-CN/docs/Learn/html/Introduction_to_html) 学习的个人学习笔记，借用了大量的图片和文本内容，存在相当多的相同，但不是copy。如需查看mozilla官方文档，请点击前文链接！！
<!--more-->

<br>

# 什么是js
本节将在一定高度俯瞰 JavaScript，使你熟悉 JavaScript 的定义和用途。

1. 解释型语言、编译型语言

    编程语言可以分为解释型语言和编译型语言两种。

    - 在解释型语言中，代码自上而下运行，且实时返回运行结果。代码在执行之前，不需要将其转化为其他形式，将直接以文本格式被接受和处理。

    - 在编译型语言中，首先要将代码转化（编译）成另一种形式才能运行。比如 C/C++ 先被编译成汇编语言，再由链接器将汇编代码转化为二进制的格式运行。

    JavaScript 是轻量级解释型语言。浏览器接收到 JavaScript 代码，并以代码自身的文本格式运行它。技术上，几乎所有 JavaScript 转换器都运用了一种叫做 即时编译（just-in-time compiling）的技术。当 JavaScript 源代码被执行时，它会被编译成二进制的格式，使代码运行速度更快。尽管如此，JavaScript 仍然是一门解释型语言，因为编译过程发生在代码运行中，而非之前。

2. 服务器端代码、客户端代码

    - 客户端代码是在用户的电脑上运行的代码，在浏览一个网页时，它的客户端代码就会被下载，然后由浏览器来运行并展示。

    - 服务端代码是在服务器上运行的代码，接着运行结果才由浏览器下载并展示出来。流行的服务器端 web 语言包括：PHP、Python、Ruby、ASP.NET 以及...JavaScript！

    它不仅适用于客户端 JavaScript，又适用于描述服务器端语言。两种情况的意义略有不同，但又有所关联，且两者（服务器端和客户端）经常协同作战。
      - 客户端 JavaScript 则在用户端浏览器中动态生成新内容，比如说创建一个新的 HTML 表格，用从服务器请求到的数据填充，然后在网页中向用户展示这个表格。

      - 服务器端代码会在服务器上动态生成新内容，例如从数据库中提取信息。

3. 动态代码、静态代码

    - **动态**是指通过按需生成新内容来更新 web 页面 / 应用，使得不同环境下显示不同内容。

    - **静态**是指没有动态更新内容，所显示的内容不会改变。

<br>

## 广义的定义
JavaScript 是一种脚本，一门编程语言，它可以在网页上实现复杂的功能，网页展现给你的不再是简单的静态信息，而是动态变化的信息。例如 实时的内容更新，交互式的地图，2D/3D动画，滚动播放的视频等等。

> 注：JavaScript 是区分大小写的，而且非常精确。

JavaScript 是web前端的三支柱：
- **HTML**是一种标记语言，用来结构化我们的网页内容并赋予内容含义。
- **CSS**是一种样式规则语言，可将样式应用于HTML内容。
- **JavaScript**是一种脚本语言，可以用来创建动态更新的内容。

<br>

这三层依次建立，秩序井然。以文本标签（text label）简单示例。
1. 首先用HTML标记文本，赋予它结构和目的：
    ```html
    <p>标签1</p>
    ```
2. 加上CSS，添加样式：
    ```css
    p {
    font-family: sans-serif, '黑体';
    letter-spacing: 1px;
    text-transform: uppercase;
    text-align: center;
    border: 2px solid rgba(0, 0, 200, 0.6);
    background: rgba(0, 0, 200, 0.3);
    color: rgba(0, 0, 200, 0.6);
    box-shadow: 1px 1px 2px rgba(0, 0, 200, 0.4);
    border-radius: 10px;
    padding: 3px 10px;
    display: inline-block;
    cursor: pointer;
    }
    ```
3. 最后，加上一些 JavaScript 实现动态行为：
    ```js
    const para = document.querySelector('p');

    para.addEventListener('click', updateName);

    function updateName() {
    let name = prompt('输入一个新的名字：');
    para.textContent = '标签1：' + name;
    }
    ```

结果如图：

![](1.png)

<br>

## js可以做什么
客户端（client-side）JavaScript 语言的核心包含一些普遍的编程特性，可以做到如下的事：
- 在变量中储存有用的值。比如上文的实例中，将客户的输入的值储存到 `name` 变量中。
- 操作一段文本。在上文实例中，将字符串 "标签1：" 和 `name` 连结起来。
- 运行代码以响应网页中发生的特定事件。上文实例中，用一个 `click` 来检测按钮的事件。
- 以及更多等 ···

**应用程序接口（ Application Programming Interfaces(API) ）** 将为你的代码提供额外的超能力。API是已经建立好的一套代码组件，可以让开发者实现原本很难甚至无法实现的程序，就像现成的家具套件之于家具建设——不用从一钉一木开始。

API通常分为两类：

![](2.png)

**浏览器API** 内建于 web 浏览器中，它们不仅可以将数据从周边计算机环境中筛选出来，还可以做实用的复杂工作。例如：
- [文档对象模型 API（ DOM(Document Object Model) API ）](https://developer.mozilla.org/zh-CN/docs/Web/API/Document_Object_Model) 能通过创建、移除和修改 HTML，为页面动态应用新样式等手段来操作 HTML 和 CSS。比如当某个页面出现一个弹窗，或者显示了一些新内容（比如上文demo），这就是 DOM 在运行。
- [地理位置 API（Geolocation API）](https://developer.mozilla.org/zh-CN/docs/Web/API/Geolocation) 获取地理信息。这就是为什么谷歌地图可以找到你的位置。
- [画布（Canvas）](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API) 和 [WebGL](https://developer.mozilla.org/zh-CN/docs/Web/API/WebGL_API) API 可以创建生动的 2D 和 3D 图像。
- 诸如 [HTMLMediaElement](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLMediaElement) 和 [WebRTC](https://developer.mozilla.org/zh-CN/docs/Web/API/WebRTC_API) 等 影音类API 让你可以利用多媒体做一些非常有趣的事。比如在网页中直接播放音乐和影片，或用自己的网络摄像头获取录像，然后在其他人的电脑上展示。

**第三方 API** 并没有默认嵌入浏览器中，一般要从网上取得它们的代码和信息。比如：
- Twitter API、新浪微博 API 可以在网站上展示最新推文之类。
- 谷歌地图 API、高德地图 API 可以在网站嵌入定制的地图等等。


<br>

## js做了什么
JavaScript 最普遍的用处是通过 DOM API 动态修改 HTML 和 CSS 来更新用户界面（user interface）。浏览器在读取一个网页时，代码（html、css 和 js）将在一个运行环境（浏览器标签页）中得到执行。就像一间工厂，将原材料（代码）加工为一件产品（网页）。具体来讲，在 HTML 和 CSS 集合组装成一个网页后，浏览器的 JavaScript 引擎就会执行 JavaScript 代码。保证了当 JavaScript 开始运行之前，网页的结构和样式已经就位，否则 JavaScript 在 HTML 和 CSS 就位之前加载运行，就会引发错误。

![](3.png)

> 每个浏览器标签页都是其自身用来运行代码的独立容器（运行环境）。大多数情况下，每个标签页中的代码完全独立运行，而且一个标签页中的代码不能直接影响另一个标签页中的代码，使不法分子无法从其他网站盗取信息。不过，以安全的方式在不同网站/标签页中传送代码和数据的方法是存在的。

<br>

当浏览器执行到一段 js 代码时，通常会按从上往下的顺序执行这段代码。
```js
const para = document.querySelector('p');

para.addEventListener('click', updateName);

function updateName() {
let name = prompt('输入一个新的名字：');
para.textContent = '标签1：' + name;
}
```

这里我们选定一个文本段落（第 1 行)，然后给它附上一个事件监听器（第 3 行），使得在它被点击时，updateName() 代码块（code block） （5 – 8 行）便会运行。updateName() （这类可以重复使用的代码块称为“函数”）向用户请求一个新名字，然后把这个名字插入到段落中以更新显示。

**在引用对象之前，必须确保该对象已经存在。**否则就会报错！


<br>

# 在网页中应用js

<br>

## 向页面添加js
CSS 使用 `<link>` 元素链接外部样式表，使用 `<style>` 元素向 HTML 嵌入内部样式表；JavaScript 只需要一个元素——`<script>`。

<br>

### 内部javascript
```js
<!DOCTYPE html>
<html lang="zh-Hans">
  <head>
    <meta charset="utf-8">
    <title>使用 JavaScript 的示例</title>
    <script>
      document.addEventListener("DOMContentLoaded", function() {
          · · ·
      });
    </script>
  </head>
  <body>
    <button>点我呀</button>
  </body>
</html>
```

内部 JavaScript 写在 `<head>` 元素中，被 `<script>` 元素包裹，适用于整个页面。

<br>

### 外部javascript
.html 文件：
```js
<!DOCTYPE html>
<html lang="zh-Hans">
  <head>
    <meta charset="utf-8">
    <title>使用 JavaScript 的示例</title>
    <script src="script.js" defer></script>         //注意这里外部js的链接
  </head>
  <body>
    <button>点我呀</button>
  </body>
</html>
```

.js 文件：
```js
function createParagraph() {
  let para = document.createElement('p');
  para.textContent = '你点击了这个按钮！';
  document.body.appendChild(para);
}

const buttons = document.querySelectorAll('button');

for(let i = 0; i < buttons.length ; i++) {
  buttons[i].addEventListener('click', createParagraph);
} 
```

在这里我们把 JavaScript 写进一个外部文件。这样做可以使代码更加有序，更易于复用，且没有了脚本的混合，HTML 也会更加易读。

<br>

### 内联javascript处理器
在有些时候，HTML 中存在一丝 JavaScript 代码。
```js
function createParagraph() {
    const para = document.createElement('p');
    para.textContent = '你点击了这个按钮！';
    document.body.appendChild(para);
}
```

```html
<button onclick="createParagraph()">点我啊</button>
```

功能和之前的没有区别，只是在 `<button>` 元素中包含了一个内联的 `onclick` 处理器。不过，这会使 JavaScript 污染到 HTML，而且效率低下。

<br>

## 脚本调用策略
要让脚本调用的时机符合预期，需要解决一系列的问题。这里看似简单，实际大有文章。最常见的问题就是：HTML 元素是按其在页面中出现的次序调用的，在使用 DOM 管理页面元素的情况下，如果 js 加载先于预操作的 HTML 元素，代码就会出错。在上文“内部”、“外部”示例中，JavaScript 调用位于文档头处、解析 HTML 文档体之前，是有一定隐患的，我们需要使用一些结构来避免错误发生。

原先解决此问题的旧方法是：把脚本元素放在文档体的底端（`</body>` 标签之前，与之相邻），这样脚本就可以在 HTML 解析完毕后加载了。但是这个方案也有（以及上后面的 DOMContentLoaded 方案）问题：只有在所有 HTML DOM 加载完成后才开始脚本的加载/解析过程。对于有大量 JavaScript 代码的大型网站，可能会带来显著的性能损耗。

### 内部js

使用以下结构：
```js
document.addEventListener("DOMContentLoaded", function() {
  . . .
});
```
这是一个事件监听器，他监听浏览器的 "`DOMContentLoaded`" 事件，即 HTML 文档体加载、解释完毕事件。事件触发时调用 "· · ·" 处的代码，从而避免了错误发生。

### 外部js
就像之前说的，为解决有大量 js 代码的大型网站的脚本调用。我们可以使用 `async` 和 `defer` 两个属性。

async 属性会告知浏览器在遇到 `<script>` 元素时不要中断后续 HTML 内容的加载。当浏览器遇到 async 脚本时，浏览器不会阻塞页面渲染，而是直接下载然后运行。使脚本和 HTML 一起加载，让代码可以顺利执行。

不过，这样脚本的运行次序无法控制，它只实现了脚本调用和页面渲染的并行，当有多个脚本共同作用时，页面加载就有可能出现问题。因此只有，当页面的脚本之间彼此独立，且不依赖于本页面的其它任何脚本时，async 是最理想的选择。

```js
<script async src="js/vendor/jquery.js"></script>

<script async src="js/script2.js"></script>

<script async src="js/script3.js"></script>
```

例如，以上三个外部js文件的调用顺序是不确定的。jquery.js 可能在 script2 和 script3 之前或之后调用，如果这样，后两个脚本中依赖 jquery 的函数将产生错误，因为脚本运行时 jquery 尚未加载。

> 注：“外部”示例中，async 属性可以解决调用顺序问题，无需使用 DOMContentLoaded 事件。

defer 属性可以使脚本按照其在页面中出现的顺序加载和运行：
```js
<script defer src="js/vendor/jquery.js"></script>

<script defer src="js/script2.js"></script>

<script defer src="js/script3.js"></script>
```
第二个示例可确保 jquery.js 必定加载于 script2.js 和 script3.js 之前，同时 script2.js 必定加载于 script3.js 之前。

> 脚本调用策略小结：
>  - 如果脚本无需等待页面解析，且无依赖独立运行，那么应使用 async。
>  - 如果脚本需要等待页面解析，且依赖于其他脚本，调用这些脚本时应使用 defer，将关联的脚本按所需顺序置于 HTML 中。

<br>

# javascript初体验
接下来是一个全面的实践性项目——循环渐进地构建一个简易版“猜数字”游戏。

<br>

## 提出问题

---
我想让你开发一个猜数字游戏。游戏应随机选择一个 100 以内的自然数, 然后邀请玩家在 10 轮以内猜出这个数字。每轮后都应告知玩家的答案正确与否，如果出错了，则告诉他数字是低了还是高了。并且应显示出玩家前一轮所猜的数字。一旦玩家猜对，或者用尽所有机会，游戏将结束。游戏结束后，可以让玩家选择再次开始。

---
看到这个要求，首先我们要做的是将其分解成简单的可操作的任务，尽可能从程序员的思维去思考：
1. 随机生成一个 100 以内的自然数。
2. 记录玩家当前的轮数。从 1 开始。
3. 为玩家提供一种猜测数字的方法。
4. 一旦有结果提交，先将其记录下来，以便用户可以看到他们先前的猜测。
5. 然后检查它是否正确。
6. 如果正确：
    1. 显示祝贺消息。
    2. 阻止玩家继续猜测（这会使游戏混乱）。
    3. 显示控件允许玩家重新开始游戏。
7. 如果出错，并且玩家有剩余轮次：
    1. 告诉玩家他们错了。
    2. 允许他们输入另一个猜测。
    3. 轮数加 1。
8. 如果出错，并且玩家没有剩余轮次：
    1. 告诉玩家游戏结束。
    2. 阻止玩家继续猜测（这会使游戏混乱）。
    1. 显示控件允许玩家重新开始游戏。
9. 一旦游戏重启，确保游戏的逻辑和UI完全重置，然后返回步骤1。

<br>

## 解决问题
接下来，我会尝试构建这个示例，从而探索 JavaScript 的功能。

<br>

### 初始设置
首先，建立一个 HTML 骨架 [number-guessing-game-start.html](https://github.com/a-pin/learning-area/blob/main/javascript/js1/first-splash/number-guessing-game-start.html)。

我们可以在 HTML 底部的 `<script>` 元素中添加新的代码：
```html
<script>

  // 开始编写 JavaScript 代码

</script>
```

<br>

### 添加变量
先在 `<script>` 元素中添加以下代码：
```js
let randomNumber = Math.floor(Math.random() * 100) + 1;

const guesses = document.querySelector('.guesses');
const lastResult = document.querySelector('.lastResult');
const lowOrHi = document.querySelector('.lowOrHi');

const guessSubmit = document.querySelector('.guessSubmit');
const guessField = document.querySelector('.guessField');

let guessCount = 1;
let resetButton;
```

**变量**本质上是值的容器。你可以使用关键字 `let` （旧代码中使用 `var`）和一个变量名创建变量。

**常量**用于存储不希望更改的数据，用关键字 `const` 创建。

在示例中：
- 用数学算法得到一个1~100的随机数，并赋值给一个变量（randomNumber）。
- 接下来的三个常量均存储着一个引用，分别指向 HTML 结果段落中某个元素，用于在代码后面段落中插入值：
  ```html
  <p class="guesses"></p>
  <p class="lastResult"></p>
  <p class="lowOrHi"></p>
  ```
- 接下来的两个常量存储对表单文本输入和提交按钮的引用，并用于控制以后提交猜测：
  ```html
  <label for="guessField">请猜数：</label>
  <input type="text" id="guessField" class="guessField">
  <input type="submit" value="确定" class="guessSubmit">
  ```
- 倒数第二个变量存储一个计数器并初始化为1，最后一个变量存储对重置按钮的引用，这个按钮尚不存在（但稍后就有了）。

<br>

### 函数function
接下来，在之前的代码中添加以下内容：
```js
function.checkGuess() {
  alert('我是一个占位符');
}
```

函数是可复用的代码块，一次编写反复运行。定义函数的方法很多，这里只介绍个最简单的方式：
```txt
关键字 function + 函数名 + 一对花括号。（花括号内部是调用函数时要运行的所有代码）
```

当我们在 开发者工具 JavaScript 控制台，输入以下代码 `checkGuess();` 调用函数。

<br>

### 条件语句conditional
替换 checkGuess() 函数：
```js
function checkGuess() {
  let userGuess = Number(guessField.value);
  if (guessCount === 1) {
    guesses.textContent = '上次猜的数：';
  }
  guesses.textContent += userGuess + ' ';

  if (userGuess === randomNumber) {
    lastResult.textContent = '恭喜你！猜对了';
    lastResult.style.backgroundColor = 'green';
    lowOrHi.textContent = '';
    setGameOver();
  } else if (guessCount === 10) {
    lastResult.textContent = '!!!GAME OVER!!!';
    setGameOver();
  } else {
    lastResult.textContent = '你猜错了！';
    lastResult.style.backgroundColor = 'red';
    if(userGuess < randomNumber) {
      lowOrHi.textContent = '你猜低了！';
    } else if(userGuess > randomNumber) {
      lowOrHi.textContent = '你猜高了';
    }
  }

  guessCount++;
  guessField.value = '';
  guessField.focus();
}
```

- 第二行声明了一个 userGuess 变量，并将其设置为在文本字段中输入的值。我们还对这个值应用了内置的 Number() 方法，确保该值是一个数字。
- 接下来的 条件代码块 可以让你根据某个条件的真假来选择性地运行代码。

<br>

### 事件event
**事件**就是浏览器中发生的事情，比如点击按钮、加载页面、播放视频等。

侦听事件发生的结构称为**事件监听器（Event Listener）**；响应事件触发而运行的代码块被称为**事件处理器（Event Handler）**。

现在，我们还无法使用 checkGuess() 函数，它还没有被调用。理想中，我们希望在点击“确认”按钮时调用它，为此，我们需要使用事件。

在 `<script>` 元素中，checkGuess() 函数后添加以下代码：
```js
guessSubmit.addEventListener('click', checkGuess);
```

这里为 guessSubmit 按钮添加了一个事件监听器。addEventListener() 方法包含两个参数，监听事件的类型和当事件发生时要执行的代码。

<br>

### 补全游戏功能
保存以上代码，实例就可以工作了，但是不够完善。玩家猜对或游戏次数用完，就会出错。

因此，定义游戏结束时应运行的 setGameOver() 函数并添加到代码最后面。：
```js
function setGameOver() {
  guessField.disabled = true;
  guessSubmit.disabled = true;
  resetButton = document.createElement('button');
  resetButton.textContent = '开始新游戏';
  document.body.appendChild(resetButton);
  resetButton.addEventListener('click', resetGame);
}
```

- 前两行通过将 disable 属性设置为 true 来禁用表单文本输入和按钮。
- 接下来的三行创建一个新的 `<button>` 元素，设置它的文本为“开始新游戏”，并把它添加到当前 HTML 的底部。
- 最后一行在新按钮上设置了一个事件监听器，当它被点击时，resetGame() 函数就会被调用。

以下是定义的 resetGame() 函数，依然放在代码底部：
```js
function resetGame() {
  guessCount = 1;

  const resetParas = document.querySelectorAll('.resultParas p');
  for (let i = 0 ; i < resetParas.length; i++) {
    resetParas[i].textContent = '';
  }

  resetButton.parentNode.removeChild(resetButton);

  guessField.disabled = false;
  guessSubmit.disabled = false;
  guessField.value = '';
  guessField.focus();

  lastResult.style.backgroundColor = 'white';

  randomNumber = Math.floor(Math.random() * 100) + 1;
}
```

这段代码将游戏中的一切重置为初始状态：
- 将 guessCount 重置为 1。
- 清除所有信息段落。
- 删除重置按钮。
- 启用表单元素，清空文本域并聚焦于此，准备接受新猜测的数字。
- 删除 lastResult 段落的背景颜色。
- 生成一个新的随机数，这样就可以猜测新的数字了。

**一个猜数字游戏就完成了！**

<br>

### 循环loop
循环是一个非常重要的编程概念，它让你能够重复运行一段代码，直到满足某个条件为止。

resetGame() 函数中：
```js
let resetParas = document.querySelectorAll('.resultParas p');
for (let i = 0 ; i < resetParas.length ; i++) {
  resetParas[i].textContent = '';
}
```

这段代码通过 querySelectorAll() 方法创建了一个包含 <div class="resultParas"> 内所有段落的变量，然后通过循环迭代，删除每个段落的文本内容。

<br>

### 浅谈对象object
JavaScript 中一切都是对象。对象是存储在单个分组中的相关功能的集合。

在 `let resetButton` （脚本顶端部分）下方添加下面一行内容：
```js
guessField.focus();
```

这一行通过 focus() 方法让光标在页面加载完毕时自动放置于 `<input>` 输入框内，为使用户能投入游戏提供一个良好的视觉线索。

在本示例的特定情况下，创建了一个 guessField 常量来存储对 HTML 中的文本输入表单域的引用：
```js
const guessField = document.querySelector('.guessField');
```

使用 document 对象的 querySelector() 方法获得引用。querySelector() 方法使用一个 CSS 选择器选中需要引用的元素。

因为 guessField 现在包含一个指向 `<input>` 元素的引用，它现在就能够访问一系列的属性（存储于对象内部的基础变量）和方法（存储在对象内部的基础函数）。

<br>

## 注释
注释分为两类：
- 在双斜杠后添加单行注释，比如：
  ```js
  // 我是一条注释
  ```
- 在 /* 和 */ 之间添加多行注释，比如：
  ```js
  /*
  我也是
  一条注释
  */
  ```

<br>

# 变量
这一节开始学习 JavaScript 基础——变量。

一个变量就是一个用于存放数值的容器。JavaScript 中的变量由两个重要特征：数值可变和存储任何数据——不只是字符串和数值，更复杂的数据有函数等。

> 变量是用来存储数值的，那么有一个重要的概念需要区分。变量不是数值本身，它们仅仅是一个用于存储数值的容器。

<br>

## 变量类型
变量有不同的数据类型，这里将对其进行简短的介绍。

JavaScript是一种“动态类型语言”，不需要指定变量将包含什么数据类型，即**动态类型**。

例如，如果你声明一个变量并给它一个带引号的值，浏览器就会知道它是一个字符串：
```js
let myString = 'Hello';
```

<br>

### number
数字，包含整数和浮点数。在 JavaScript 中，你不需要声明变量类型。
```js
let age = 100;
```

<br>

### string
字符串是文本的一部分。为变量赋值时，需要用**单引号**或**双引号**将值包裹起来；否则 JavaScript 会把这个字符串理解成别的变量名。
```js
let name = 'Chris';
```

<br>

### boolean
Boolean 的值有两种：true或false。它们通常由于检测条件是否成立：
```js
let test = 6 < 3;
```

<br>

### array
数组是一个单个对象，其中包含很多值，方括号括起来，并用逗号分隔:
```js
let myNameArray = ['Chris', 'Bob', 'Jim'];
let myNumberArray = [10,15,40];
```

当数组被定义后，您可以使用如下所示的语法来访问各自的值，例如下行:

```js
myNameArray[0]; // should return 'Chris'
myNumberArray[2]; // should return 40
```

此处的方括号包含一个索引值，该值指定要返回的值的位置。

<br>

### object
在编程中，对象是现实生活中的模型的一种代码结构。比如，代表一个停车场的对象，并包含有关其宽度和长度的信息；或者代表一个人，并包含有关他们的名字，身高，体重，语言等。
```js
let dog = { name : 'Spot', breed : 'Dalmatian' };
```

要检索存储在对象中的信息，可以使用以下语法:
```js
dog.name
```

<br>

## 变量的声明与赋值
使用一个变量，首先就是声明它。声明一个变量的语法就是在 var 或 let 关键字之后加上这个变量的名字。

在 JavaScript 控制台中，定义变量：
```js
let name;
let age;
```

以上两个变量并没有返回值，它们是空的容器。当你定义好变量后，你会得到一个 undefined 的返回值。

<br>

---

**关于变量命名的规则**：
一般应当使用拉丁字符(0-9,a-z,A-Z)和下划线字符为变量命名。以下是一些限制： 
- 不应当使用规则之外的其他字符（因为它们可能引发错误，或对国际用户来说难以理解）。
- 不要以下划线开头（以下划线开头的被某些 JavaScript 设计为特殊的含义）。
- 不要以数字开头（将会引发一个错误）。
- 一个可靠的命名约定叫做“小写驼峰命名法”，用来将多个单词组在一起，小写整个命名的第一个字母然后大写剩下单词的首字符。例如，finalOutputValue。
- 让变量名直观，描述了所包含的数据。
- 避免使用 JavaScript 的保留字给变量命名（保留字是组成JavaScript的实际语法的单词）。

错误示例：
```txt
1
_12
var
```

---

<br>

当你定义好一个变量后，你就能够给它赋值，第一次给变量赋值被称为变量的**初始化**。在控制台输入以下命令：
```js
name = 'Chris';
age = 24;
```

可以看到控制台返回变量的值。

类似的，你可以将变量的声明和初始化结合在一起：
```js
let name = 'Chris';
```

<br>

## var与let的区别
“为什么我们需要两个关键字来定义变量?”，“为什么有 var 和 let 呢？"。

原因是有些历史性的。最初创建 JavaScript 时，是只有 var 的。 在大多数情况下，这种方法可以接受， 但有时在工作方式上会有一些问题——它的设计会令人困惑或令人讨厌 。 因此，let 是在现代版本中的 JavaScript 创建的一个新的关键字，用于创建与 var 工作方式有些不同的变量，解决了过程中的问题。

下面解释几个简单的差异：

首先，如果你编写一个声明并初始化变量的多行 JavaScript 程序，你可以在初始化一个变量之后用 var 声明它，它仍然可以工作。 例如：
```js
myName = 'Chris';

function logName() {
  console.log(myName);
}

logName();

var myName;
```

这是由于[变量的提升](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/var#%E5%8F%98%E9%87%8F%E6%8F%90%E5%8D%87)。

不过提升操作不再适用于 let ，因为初始化后再声明一个变量会使代码变得混乱和难以理解。

其次，当你使用 var 时，可以根据需要多次声明相同名称的变量，而 let 不能。
```js
var myName = 'Chris';
var myName = 'Bob';

// 等价于

let myName = 'Chris';
myName = 'Bob';
```

我们没理由重新声明变量，这会使代码变得混乱。

<br>

# 数字和操作符
JavaScript 有一套可用的全功能的数学功能。

<br>

## 数字
我们使用不同的术语来描述不同类型的十进制数，例如：

- **整数**：就是整数,例如 10, 400, 或者 -5.
- **浮点数**：有小数点或小数位，例如 12.5，和 56.7786543。
- **双精度**：双精度是一种特定类型的浮点数，它们具有比标准浮点数更高的精度。

<br>

## 操作符
运算符的优先级，用于确定一个表达式的计算顺序。在你不能确定优先级时，可以通过使用括号显式声明运算符的优先级。

下表列出了描述符的优先级，从最高到最低。

**运算符优先级**

| Operator type | Individual operators |
| --- | --- |
| member | `. []` |
| call / create instance | `() new` |
| negation/increment | `! ~ - + ++ -- typeof void delete` |
| multiply/divide | `* / %` |
| addition/subtraction | `+ -` |
| bitwise shift | `<< >> >>>` |
| relational | `< <= > >= in instanceof` |
| equality | `== != === !==` |
| bitwise-and | `&` |
| bitwise-xor | `^` |
| bitwise-or | `\|` |
| logical-and | `&&` |
| logical-or | `||` |
| conditional | `?:` |
| assignment | `= += -= *= /= %= <<= >>= >>>= &= ^= \|=` |
| comma | `,` |

<br>

### 算术运算符
算术运算符是我们进行数学计算最基本的运算符：
|**运算符**|**名称**|**作用**|**示例**|
|---|---|---|---|
|+|加法|两个数相加|6 + 9|
|-|减法|从左边减去右边的数|20 - 15|
|*|乘法|两个数相乘|3 * 7|
|/|除法|用右边的数除左边的数|10 / 5|
|%|求余（取模）|在你将左边的数分成同右边数字相同的若干整数部分后，返回剩下的余数|8 % 3 = 2|
|**|幂|取底数的指数次方|5 ** 5 = 3125|

参与到算术计算的数字被称为 操作数。

<br>

### 自增和自减运算符
有时候，您需要反复把一个变量加1或减1。这可以方便地使用增量（++）和递减（ -- ）运算符来完成。 

例如：
```js
let num1 = 4;
num1++;
```

执行此操作时，您会看到返回值为4，这是因为浏览器返回当前值，然后增加变量。

为此，你可以——递增/递减变量，然后返回值——将操作符放在变量的开头，而不是结束。 再次尝试上面的例子，但这次使用 ++num1 和 --num2。

<br>

### 赋值运算符
赋值运算符是向变量分配值的运算符。

|**运算符**|**名称**|**作用**|**示例**|**等价于**|
|- - -|- - -|- - -|- - -|- - -|
|+=|加法赋值|返回右边的数值加上左边的变量|x += 3|x = x + 3|
|-=|减法赋值|返回左边的变量减去右边的数值|x -= 3|x = x - 3|
|*=|乘法赋值|返回左边的变量乘以右边的数值|x *= 3|x = x * 3|
|/=|除法赋值|返回左边的变量除以右边的数值|x /= 3|x = x / 3|

<br>

### 比较运算符
|**运算符**|**名称**|**作用**|
|- - -|- - -|- - -|
|===|严格等于|测试左右值是否相同|
|!==|严格不等于|测试左右值是否不相等|
|<|小于|测试左值是否小于右值|
|>|大于|测试左值是否大于右值|
|<=|小于或等于|测试左值是否小于或等于右值|
|>=|大于或等于|测试左值是否大于或等于右值|

> 注：有些人可能使用 == 或 != 来判断相等或不相等，这些都是 JavaScript 中的有效运算符，但是它们只判断测试值是否相同，而数据类型可能不同；严格版本会测试值和值的数据类型是否都相同。

<br>

# 字符串
HTML为我们的文本提供了结构和意义， CSS 允许我们精确地设计它的样式，JavaScript包含许多操作字符串的特性，创建定制的欢迎消息，在需要时显示正确的文本标签，将术语排序到所需的顺序，等等。

<br>

## 基本知识
创建一个字符串：
```js
let string = 'Hello,js!';
```

你可以使用单引号或者双引号包裹字符串，但是必须使用同一种引号包裹字符串。否者就会出错，没有引号的任何字符串都被假定为变量名、属性名、保留字等。：
```js
let badQuotes = 'hello.js!"
```

不过，在使用一种引号包裹字符串情况下，字符串中可以使用另一种引号。
```js
let string = 'Would you eat a "fish supper"?';
```

**连接字符串**：使用加号（+）连接字符串。例如：
```js
let one = 'Hello,';
let two = 'js!';
let plus = one + two;
```

**数字与字符串之间的转换**：
- Number 对象将把传递给它的任何东西转换成一个数字。
  ```js
  let myString = '123';
  let myNum = Number(myString);
  typeof myNum;
  ```
- 每个数字都有一个名为 toString() 的方法，它将把它转换成等价的字符串。
  ```js
  let myNum = 123;
  let myString = myNum.toString();
  ```

<br>

## 字符串方法
除了基本的字符串语法，我们还可以使用字符串的内置方法。

**把字符串当作对象**，在 JavaScript 中，一切东西都可以被当作对象。一旦你的变量成为字符串对象实例，你就可以可以有大量的原型和方法编辑它。

<br>

### 字符串长度
使用 `length` 属性获取字符串长度：
```js
let browserTtype = 'edge';
browserType.length;
```

结果会返回一个数字4。

<br>

### 检索特定字符串字符
使用 方括号表示法 返回字符串中的任何字符。在方括号内的数字是要返回的字符的编号：
```js
browserType[0];
browserType[browserType.length-1];
```

<br>

### 查找和提取子字符串
在一个字符串中是否包含另一个特定字符串，使用 `indexOf()` 方法完成：
```js
browserType.indexOf('dge');
```

结果返回 1，因为子字符串从 edge 的第二个字符开始。

```js
browserType.indexOf('chrome');
```

结果返回 -1，因为在主字符串中找不到子字符串。

<br>

当你知道子字符串的开始和结尾，`slice()` 可以提取这个子字符串。
```js
browserType.slice(0,2);
```

结果是 ed —— 第一个参数是开始提取的字符位置，第二个参数是开始不要提取的位置。

其中，省略第二个参数可以省略。用以提取第一个参数之后的所有剩余字符。
```js
browserType.slice(1);
```

<br>

### 转换大小写
字符串方法 `toLowerCase()` 和 `toUpperCase()` 可以将所有字符分别转换为小写或大写。 例如，如果要在将数据存储在数据库中之前对所有用户输入的数据进行规范化，这可能非常有用。

```js
let radData = 'My NaMe Is MuD';
radData.toLowerCase();
radData.toUpperCase();
```

<br>

### 替换字符串
您可以使用 `replace()` 方法将字符串中的一个子字符串替换为另一个子字符串。

它需要两个参数 —— 要被替换下的字符串和要被替换上的字符串。例如：
```js
browserType.replace('moz','van');
```

<br>

# 数组
数组是一个包含了多个值的对象。数组对象可以存储在变量中，并且能用和其他任何类型的值完全相同的方式处理，区别在于我们可以单独访问列表中的每个值，并使用列表执行一些有用和高效的操作，如循环。 

<br>

## 基础知识

<br>

### 创建数组
数组由方括号构成，其中包含用逗号分隔的元素列表。例如：
```js
let shopping = ['bread', 'milk', 'cheese', 'hummus', 'noodles'];
```

你可以将任何类型的元素存储在数组中 —— 字符串，数字，对象，另一个变量，甚至另一个数组。
```js
let random = ['tree', 795, [0, 1, 2]];
```

<br>

### 访问和修改数组元素
你可以使用 括号表示法 访问数组中的元素，与 检索特定字符串字符 的方法相同。

例如：
```js
shopping[0];    // returns "bread"
```

您还可以简单地为单个数组元素提供新值来修改数组中的元素。 例如：
```js
shopping[0] = 'tahini';
```

<br>

### 获得数组元素
你可以通过使用 `length` 属性获取数组的长度，这与查找字符串的长度（以字符为单位）完全相同。
```js
sequence.length;    // should return 7
```

对于每个元素，可以使用 console.log() 将其打印到浏览器控制台。

<br>

## 数组方法

<br>

### 字符串和数组间的转换
通常，您会看到一个包含在一个长长的字符串中的原始数据，您可能希望将有用的项目分成更有用的表单，然后对它们进行处理，例如将它们显示在数据表中。为此，我们可以使用 字符串的 `split()` 方法。在其最简单的形式中，这需要一个参数——您要将字符串分隔的字符，并返回分隔符之间的子串，作为数组中的项。

例如：
- 首先，创建一个字符串：
  ```js
  let myData = 'Manchester,London,Liverpool,Birmingham,Leeds,Carlisle';
  ```
- 现在我们用每个逗号分隔它：
  ```js
  let myArray = myData.split(',');
  ```
- 最后，尝试找到新数组的长度，并从中检索一些项目：
  ```js
  myArray.length;
  myArray[0]; // the first item in the array
  myArray[myArray.length-1]; // the last item in the array
  ```
- 您也可以使用 `join()` 方法进行相反的操作。 尝试以下：
  ```js
  let myNewString = myArray.join(',');
  ```

将数组转换为字符串的另一种方法是使用 `toString()` 方法。`toString()` 可以比 `join()` 更简单，因为它不需要一个参数，但更有限制。使用 `join()` 可以指定不同的分隔符。
```js
let dogNames = ["Rocket","Flash","Bella","Slugger"];
dogNames.toString(); //Rocket,Flash,Bella,Slugger
```

<br>

### 添加和删除数组项
```js
let myArray = ['Manchester', 'London', 'Liverpool', 'Birmingham', 'Leeds', 'Carlisle'];
```

首先，要在数组末尾添加或删除一个项目，我们可以使用  `push()` 和 `pop()`。

- 使用 `push()` 添加一个或多个要添加到数组末尾的元素：
  ```js
  myArray.push('Cardiff');
  myArray.push('Bradford', 'Brighton');
  ```
  当方法调用完成时，将返回数组的新长度。如果要将新数组长度存储在变量中，例如：
  ```js
  var newLength = myArray.push('Bristol');
  newLength;
  ```
- 从数组中删除最后一个元素的话直接使用 `pop()` 就可以。例如：
  ```js
  myArray.pop();
  ```
  当方法调用完成时，将返回已删除的项目：
  ```js
  let removedItem = myArray.pop();
  removedItem;
  ```

`unshift()` 和 `shift()` 从功能上与 `push()` 和 `pop()` 完全相同，只是它们分别作用于数组的开始，而不是结尾。