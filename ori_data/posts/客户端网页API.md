---
title: 客户端网页API
description: 探索什么是API，以及如何使用一些在你开发中将经常遇见的API。
tags:
  - JavaScript
categories:
  - mdn
	- web前端
---

在此特地声明本文是根据 [mozilla官方教学文档](https://developer.mozilla.org/zh-CN/docs/Learn/html/Introduction_to_html) 学习的个人学习笔记，借用了大量的图片和文本内容，存在相当多的相同，但不是copy。如需查看mozilla官方文档，请点击前文链接！！
<!--more-->

<br>

# Web API简介
API 是什么？它们如何工作？如何在代码中使用它们以及它们是如何组织的？我们也将看看不同主要类别的API以及它们的用途。

<br>

## 什么是API
应用程序接口（API，Application Programming Interface）是基于编程语言构建的结构，使开发人员更容易地创建复杂的功能。它们抽象了复杂的代码，并提供一些简单的接口规则直接使用。

来看一个现实中的例子：如果你想在房子里用电，只要把电器的插头插入插座就可以，而不是直接把它连接到电线上。

![](1.png)

类似的，显示一些3D图形，使用以更高级语言编写的 API（例如 JavaScript 或 Python）将会比直接编写直接控制计算机的 GPU 或其他图形功能的低级代码（比如C或C++）来执行操作要容易得多。

<br>

**客户端JavaScript中的API**

客户端 JavaScript 中有很多可用的 API —— 他们本身并不是 JavaScript 语言的一部分，却建立在 JavaScript 语言核心的顶部，为使用 JavaScript 代码提供额外的超强能力。他们通常分为两类：
- 浏览器 API 内置于 Web 浏览器中，能从浏览器和电脑周边环境中提取数据，并用来做有用的复杂的事情 。例如 Geolocation API 提供了一些简单的 JavaScript 结构以获得位置数据，浏览器在后台使用了一些复杂的低级代码（C++ 等）与设备的 GPS 硬件通信来获取位置数据并把这些数据返回给您的代码中使用浏览器环境（这种复杂性通过 API 抽象出来）。
- 第三方 API 缺省情况下不会内置于浏览器中，通常必须在 Web 中的某个地方获取代码和信息。例如 Twitter API 可以用来请求 Twitter 服务并返回特殊的信息。

<br>

**JavaScript，API和其他JavaScript工具之间的关系**

如上所述，我们讨论了什么是客户端 JavaScript API，以及它们与 JavaScript 语言的关系。让我们回顾一下，使其更清晰，并提及其他 JavaScript 工具的适用位置：
- JavaScript：一种内置于浏览器的高级脚本语言，你可以用来实现 Web 页面/应用中的功能。
- 客户端 API：内置于浏览器的结构程序，位于 JavaScript 语言顶部，使你可以更容易的实现功能。
- 第三方 API：置于第三方普通的结构程序（例如Twitter、Facebook），使你可以在自己的 Web 页面中使用那些平台的某些功能。
- JavaScript 库：通常是包含具有特定功能的一个或多个 JavaScript 文件，把这些文件关联到你的 Web 页以快速实现功能。
- JavaScript 框架：从库开始的下一步，JavaScript 框架视图把 HTML、CSS、JavaScript 和其他安装的技术打包在一起，然后用来从头编写一个完整的 Web 应用。

<br>

## API可以做什么
在主流浏览器中有大量的可用 API，你可以在代码中做许多的事情，对此可以查看 [MDN API index page](https://developer.mozilla.org/zh-CN/docs/Web/API)。

<br>

**常见浏览器API**

常见的浏览器API类别：
- **操作文档的 API** 内置于浏览器中。例如 DOM API，它允许你操作 HTML 和 CSS，创建、移除以及修改 HTML，动态地将新样式应用到页面等。每当你看到一个弹出窗口出现在一个页面上，或者显示一些新的内容时，这都是 DOM 的行为。
- **从服务器获取数据的 API** 用于更新网页的一部分——更新网页的一小部分而不从服务器重新加载整个页面将。包括的 API 有 XMLHttpRequest 和 Fetch API（Ajax）。
- **用于绘制和操作图形的 API** 目前已被浏览器广泛支持，最流行的是允许你以编程方式更新包含在 HTML `<canvas>` 元素中的像素数据以创建2D和3D场景的 Canvas 和 WebGL。
- **音频和视频 API**，例如 HTMLMediaElement、Web Audio API 和 WebRTC。它们可以使用多媒体来创建用于播放音频和视频的自定义 UI 控件，为视频添加字幕，或者添加效果到音轨，等等。
- **设备 API** 是检索现代设备硬件中的数据的API。例如 Geolocation API。
- **客户端存储 API** 可以用来创建一个应用程序来保存页面加载之间的状态，让设备在处于脱机状态时可用。

<br>

**常见第三方 API**

第三方API种类繁多，下列是一些比较流行的第三方 API：
- Twitter API：在网站上展示您最近的推文等。
- Google Maps API：在网页上对地图进行操作。
- Facebook suite of API：可以将很多 Facebook 生态系统中的功能应用到你的 app。比如，它提供了通过 Facebook 账户登录、接受应用内支付、推送有针对性的广告活动等功能。
- YouTube API：可以将 Youtube 上的视频嵌入到网站中去，同时提供搜索 Youtube，创建播放列表等功能。
- Twilio API：为 app 提供了语音通话和视频聊天的框架，实现了发送短信息或多媒体信息等功能。

<br>

## API如何工作
不同的 JavaScript API 以不同的方式工作，但它们通常具有共同的特征和相似的主题。

<br>

**基于对象**

API 使用一个或多个 JavaScript 对象在你的代码中进行交互，这些对象用作 API 使用的数据（对象属性）的容器以及 API 提供的功能（对象方法）。

例如 Geolocation API，它由几个简单的对象组成：
- Geolocation：其中包含三种控制地理数据检索的方法
- Position：表示在给定的时间的相关设备的位置。 — 它包含一个当前位置的 Coordinates 对象。还包含了一个时间戳,这个时间戳表示获取到位置的时间。
- Coordinates：其中包含有关设备位置的大量有用数据，包括经纬度，高度，运动速度和运动方向等。

<br>

**有可识别的入口点**

使用 API 时，应确保知道 API 入口点的位置。在 Geolocation API 中，入口点是 Navigator.geolocation 属性, 它返回浏览器的 Geolocation 对象，所有有用的地理定位方法都可用。

DOM API 的功能往往挂在 Document 对象，或任何你想影响的 HTML 元素的实例，例如：
```js
var em = document.createElement('em'); // 创建一个新的 em 元素
var para = document.querySelector('p'); // 引用一个现有的 p 元素
em.textContent = 'Hello there!'; // 给 em 元素添加文本
para.appendChild(em); // 向 para 添加 em 子节点
```

<br>

**使用事件来处理状态的变化**

有些 Web API 包含一些事件，例如 XMLHttpRequest 对象的每一个实例都代表一个到服务器的 HTTP 请求，有很多方法可以使用。

例如，在资源成功返回时触发 onload 事件：
```js
var requestURL = 'https://xxx.xxX.XXX';
var request = new XMLHttpRequest();
request.open('GET', requestURL);
request.responseType = 'json';
request.send();

request.onload = function() {
  var superHeroes = request.response;
  populateHeader(superHeroes);
  showHeroes(superHeroes);
}
```

前五行指定了我们要获取的资源的位置，使用 `XMLHttpRequest()` 构造函数创建请求对象的新实例，打开 HTTP 的 GET 请求以取得指定资源，指定响应以 JSON 格式发送，然后发送请求。

然后 onload 处理函数指定我们如何处理响应，将包含 JSON 的响应保存在变量中，然后将其传递给两个不同的函数进行进一步的处理。

<br>

**在适当的地方有额外的安全机制**

Web API 有着与 JavaScript 和其他 Web 技术相同的安全考虑，并且有时会有额外的安全机制。例如，一些更现代的 Web API 将只能在通过 HTTPS 提供的页面上工作。