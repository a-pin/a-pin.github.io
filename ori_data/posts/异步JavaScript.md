---
title: 异步JavaScript
description: 本文将讲解异步为什么很重要，以及怎样使用异步来有效处理潜在的阻塞操作，比如从服务器上获取资源。
tags:
- JavaScript
categories:
- web
---

在此特地声明本文是根据 [mozilla官方教学文档](https://developer.mozilla.org/zh-CN/docs/Learn/html/Introduction_to_html) 学习的个人学习笔记，借用了大量的图片和文本内容，存在相当多的相同，但不是copy。如需查看mozilla官方文档，请点击前文链接！！
<!--more-->

<br>

# 异步javascript简介
本节将介绍一些 JavaScript 异步技术并展示如何使用这些技术解决问题。

在最基本的形式中，JavaScript 是一种同步的、阻塞的、单线程的语言，在这种语言中，一次只能执行一个操作。但 web 浏览器定义了函数和 API，允许我们当某些事件发生时不是按照同步方式，而是异步地调用函数（比如，时间的推移，用户通过鼠标的交互，或者获取网络数据）。

<br>

## js同步和异步的区别
js 是一门单线程语言，一次只能完成一件任务。如果有多个任务，就必须排队，前面一个任务完成，再执行后面一个任务。如果一个任务耗时过长，那么后面的任务就必须一直等待下去，会拖延整个程序。常见浏览器无反应，可能就是一段代码死循环，造成程序卡住在这个位置，无法继续。

- **同步任务**：指在主线程上排队执行的任务，只有前一个任务执行完毕，才能继续执行下一个任务。
- **异步模式**：指不进入主线程，而进入任务队列的任务，只有任务队列通知主线程，某个异步任务可以执行了，该任务才会进入主线程。

那么，JavaScript 中的异步是怎么实现的呢？

一个异步过程通常是这样的：**主线程**发起一个异步请求，相应的**工作线程**接收请求并告知主线程已收到(异步函数返回)。主线程可以继续执行后面的代码，同时工作线程执行异步任务。工作线程完成工作后，通知主线程，主线程收到通知后，执行一定的动作(调用回调函数)。
```js
A(args..., callbackFn)
```

从主线程的角度看，一个异步过程包括下面两个要素：发起函数(注册函数)A和回调函数callbackFn。它们都是在主线程上调用的，其中注册函数用来发起异步过程，回调函数用来处理结果。

异步过程中，工作线程在异步操作完成后需要通知主线程。这个通知机制是利用**消息队列**和**事件循环**实现的：工作线程将消息放到消息队列，主线程通过事件循环过程去取消息。
- 消息队列：消息队列是一个先进先出的队列，它里面存放着各种消息。
- 事件循环：事件循环是指主线程重复从消息队列中取消息、执行的过程。

实际上，主线程只会做一件事情，就是从消息队列里面取消息、执行消息，再取消息、再执行。当消息队列为空时，就会等待直到消息队列变成非空。而且主线程只有在将当前的消息执行完成后，才会去取下一个消息。这种机制就叫做事件循环机制，取一个消息并执行的过程叫做一次循环。

> 消息队列中放的消息具体是什么呢？
> 
> 消息的具体结构实际上跟具体的实现有关。消息队列中的每条消息实际上都对应着一个事件。

为简单起见，认为消息就是注册异步任务是添加的回调函数。用图表示具体异步过程：

![](1.png)

观察异步代码执行的过程，可以发现异步过程的回调函数，一定不在当前这一轮事件循环中执行。因为消息队列的长度是未知的。

<br>

## 实现异步
在 JavaScript 代码中，你经常会遇到两种异步编程风格：**老派 callbacks**，**新派 promise**。

<br>

### 异步callbacks
**异步 callbacks 其实就是函数**，只不过是作为参数传递给那些在后台执行的其他函数。当那些后台运行的代码结束，就调用 callbacks 函数，可以通知你工作已经完成，或者其他事情发生了。

举个例子，异步 callback 就是 addEventListener() 第二个参数，第一个参数是侦听的事件类型，第二个就是事件发生时调用的回调函数。
```js
btn.addEventListener('click' , callback);
```

当我们把回调函数作为一个参数传递给另一个函数时，仅仅是把回调函数定义作为参数传递过去而没有立刻执行，包含函数会在合适的时候**异步执行**回调函数。

例如，使用 XMLHttpRequest API 加载资源：
```js
function loadAsset(url, type, callback) {
  let xhr = new XMLHttpRequest();
  xhr.open('GET', url);
  xhr.responseType = type;

  xhr.onload = function() {
    callback(xhr.response);
  };

  xhr.send();
}

function displayImage(blob) {
  let objectURL = URL.createObjectURL(blob);

  let image = document.createElement('img');
  image.src = objectURL;
  document.body.appendChild(image);
}

loadAsset('coffee.jpg', 'blob', displayImage);
```

创建 `loadAsset()` 函数，把 URL、type 和回调函数同时都作为参数。函数用 XMLHttpRequest (简称 XHR) 获取给定 URL 的资源，在获得资源响应后再把**响应作为参数**传递给回调函数（ displayImage() ）去处理。`displayImage()` 函数接受 blob 生成 objectURL，然后生成一个 image 元素，把 objectURL 作为 image 的源地址，最后显示这张图片。

回调函数用途广泛，它不仅仅可以用来控制函数的执行顺序和函数之间的数据传递，还可以根据环境的不同，将数据传递给不同的函数，所以对下载好的资源，你可以采用不同的操作来处理，譬如 processJSON()、displayText() 等等。

**注意**：不是所有的回调函数都是异步的，存在一些是同步的。

例如，使用 Array.prototype.forEach() 来遍历数组：
```js
const gods = ['Apollo', 'Artemis', 'Ares', 'Zeus'];

gods.forEach(function (eachName, index){
  console.log(index + '. ' + eachName);
});
```

在这个例子中，我们遍历一个希腊神的数组，并在控制台中打印索引和值。`forEach()` 需要的参数是一个回调函数，回调函数带有两个参数，数组元素和索引值。它无需等待任何事情，立即运行。

<br>

### promises
Promises 是新派的异步代码，现代的 web APIs 经常用到。`fetch() API` 就是一个很好的例子，它基本上就是一个现代版的、更高效的 XMLHttpRequest。

例如：
```js
fetch('products.json').then(function(response) {
  return response.json();
}).then(function(json) {
  products = json;
  initialize();
}).catch(function(err) {
  console.log('Fetch problem: ' + err.message);
});
```

`fetch()` 把资源 URL 作为参数，不会立即返回一个值，而是返回一个 promise，由 promise 最终在以后提供该值。

JavaScript 中的 promise 是异步的，返回它的代码需要时间运行。promise 相当于一个运行异步代码的承诺，在js引擎空闲时，引擎不会等待而什么都不做，它会开始执行其他代码，等待 promise 的返回值。

这两种可能的结果都还没有发生，因此 fetch 操作正在等待浏览器在将来某个时候完成该操作的结果。之后，三个代码块链接到 `fetch()` 的末尾：
- 两个 `then()` 块。两者都包含一个回调函数，如果前一个操作成功，该函数将运行，并且该函数会接收前一个成功操作的结果作为输入，你可以继续对它执行其他操作。每个 `.then()` 块返回另一个 promise，这意味着可以将多个`.then()` 块链接到另一个块上，这样就可以依次执行多个异步操作。
- 如果其中任何一个 `then()` 块失败，则在末尾运行 `catch()` 块——与同步 `try...catch` 类似，`catch()` 提供了一个错误对象，可用来报告发生的错误类型。注意，同步 `try...catch` 不能与 promise 一起工作。

<br>

**Promises 对比 callbacks**

promises 与旧式 callbacks 有一些相似之处。它们本质上是一个返回的对象，你可以将回调函数附加到该对象上，而不必将回调作为参数传递给另一个函数。

然而，Promise 是专门为异步操作而设计的，与旧式回调相比具有许多优点：
- 可以使用多个 `then()` 操作将多个异步操作链接在一起，并将其中一个操作的结果作为输入传递给下一个操作。
- Promise 总是严格按照它们放置在事件队列中的顺序调用。
- 错误处理要好得多。所有的错误都由块末尾的一个 `.catch()` 块处理。

## 异步代码的本质
这个示例，进一步说明了异步代码的本质，展示了当我们不完全了解代码执行顺序以及将异步代码视为同步代码时可能发生的问题：
```js
console.log ('Starting');
let image;

fetch('coffee.jpg').then((response) => {
  console.log('It worked :)')
  return response.blob();
}).then((myBlob) => {
  let objectURL = URL.createObjectURL(myBlob);
  image = document.createElement('img');
  image.src = objectURL;
  document.body.appendChild(image);
}).catch((error) => {
  console.log('There has been a problem with your fetch operation: ' + error.message);
});

console.log ('All done!');
```

浏览器将会执行代码，看见第一个 `console.log()` 输出 “Starting”，然后创建 image 变量。

然后，它将移动到下一行并开始执行 `fetch()` 块，但是，因为 `fetch()` 是异步执行的，没有阻塞，所以在 promise 相关代码之后程序继续执行，从而到达最后的 `console.log()` 语句 “All done!” 并将其输出到控制台。

只有当 `fetch()` 块完成运行返回结果给 `.then()`，我们才最后看到第二个 `console.log()` 消息 “It worked ;)”。所以 这些消息 可能以和你预期不同的顺序出现：
```txt
Starting
All done!
It worked :)
```

如果你感到疑惑，考虑下面这个小例子：
```js
console.log("registering click handler");

button.addEventListener('click', () => {
  console.log("get click");
});

console.log("all done");
```

这在行为上非常相似——第一个和第三个 `console.log()` 消息将立即显示，但是第二个消息将被阻塞，直到有人单击鼠标按钮。第一个示例以相同的方式工作，只是在这种情况下，第二个消息在 promise 链上被阻塞，直到获取资源后再显示在屏幕上，而不是单击。

<br>

# 合作异步javascript：超时和间隔
在这里，我们将讨论传统 JavaScript 的方法，这些方法可以在一段时间（超时）或一段规则间隔（间隔）之后，以异步方式运行代码，并讨论它们的用途和固有问题。

<br>

## 介绍
很长一段时间以来，web 平台为 JavaScript 程序员提供了许多函数，这些函数允许你在一段时间间隔过后异步执行代码，或者重复异步执行代码块，直到您告诉它停止为止。

[`setTimeout()`](https://developer.mozilla.org/zh-CN/docs/Web/API/setTimeout)

$\qquad$ 在指定的时间后执行一段代码。

[`setInterval()`](https://developer.mozilla.org/zh-CN/docs/Web/API/setInterval)

$\qquad$ 以固定的时间间隔，重复运行一段代码。

[`requestAnimationFrame()`](https://developer.mozilla.org/zh-CN/docs/Web/API/window/requestAnimationFrame)

$\qquad$ setInterval() 的现代版本；在浏览器下一次**重新绘制显示**之前执行指定的代码块，从而允许动画在适当的帧率下运行，而不管它在什么环境中运行。

这些函数设置的异步代码实际上在主线程上运行（在其指定的计时器过去之后）。

在 `setTimeout()` 调用执行之前或 `setInterval()` 迭代之间可以运行其他代码。根据这些操作的处理器密集程度，它们可以进一步延迟异步代码，因为任何异步代码仅在主线程可用后才执行。

无论如何，这些函数用于在 web 站点或应用程序上运行不间断的动画和其他后台处理。在下面的部分中，我们将向您展示如何使用它们。

<br>

## setTimeout()
正如前述，`setTimeout()` 在指定的时间后执行一段特定代码. 它需要如下参数:
- 要运行的函数，或者函数引用。
- 表示在执行代码之前等待的时间间隔（以毫秒为单位）。如果指定值为0（或省略该值），函数将尽快运行，而不是立刻执行。
- 更多的参数：在指定函数运行时，希望传递给函数的值。

> 注：指定的时间不能保证在指定的确切时间之后执行，而是最短的延迟执行时间。在主线程上的堆栈为空之前，传递给这些函数的回调将无法运行。

结果，像 `setTimeout(fn, 0)` 这样的代码将在堆栈为空时立即执行，而不是立即执行。

在下面两个示例中，浏览器将在执行匿名函数之前等待两秒钟，然后显示alert消息：
```js
// With a named function
let myGreeting = setTimeout(function sayHi() {
  alert('Hello, Mr. Universe!');
}, 2000)

// With a function defined separately
function sayHi() {
  alert('Hello Mr. Universe!');
}

let myGreeting = setTimeout(sayHi, 2000);
```

如果一个函数既需要超时调用也需要响应某个事件，那么就可以使用函数引用作为参数，它可以帮助保持代码整洁。

我们希望传递给 `setTimeout()` 中运行的函数的任何参数，都必须作为列表末尾的附加参数传递给它。例如：
```js
function sayHi(who) {
  alert('Hello ' + who + '!');
}

let myGreeting = setTimeout(sayHi, 2000, 'Mr. Universe');
```

**清除超时**

最后，如果创建了 timeout，您可以通过调用 `clearTimeout()`，将 `setTimeout()` 调用的标识符作为参数传递给它，从而在**超时运行之前**取消。例如：
```js
clearTimeout(myGreeting);
```

<br>

## setInterval()
`setInterval()` 第一个参数指向被引用函数，重复执行的时间不少于第二个参数给出的毫秒数，被引用函数所需的参数添加到参数列表后面。

例如，下面的函数创建一个新的 `Date()` 对象，使用 `toLocaleTimeString()` 从中提取一个时间字符串，然后在 UI 中显示它。然后，我们使用 `setInterval()` 每秒运行该函数一次，创建一个每秒更新一次的数字时钟的效果。
```js
function displayTime() {
   let date = new Date();
   let time = date.toLocaleTimeString();
   document.getElementById('demo').textContent = time;
}

const createClock = setInterval(displayTime, 1000);
```

像 `setTimeout()` 一样，`setInterval()` 返回一个确定的值，稍后你可以用它来取消间隔任务。

**清除intervals**

将 `setInterval()` 返回的标识符传递给 `clearInterval()` 函数来取消间隔任务，否则它将会一直保持运行任务。
```js
const myInterval = setInterval(myFunction, 2000);

clearInterval(myInterval);
```

<br>

## 递归timeouts和interval
使用递归 `setTimeout()` 每100秒运行函数：
```js
let i = 1;

setTimeout(function run() {
  console.log(i);
  i++;
  setTimeout(run, 100);
}, 100);
```

使用 `setInterval()` 实现相同的效果：
```js
let i = 1;

setInterval(function run() {
  console.log(i);
  i++
}, 100);
```

**递归 setTimeout() 和 setInterval() 两者的差异是什么？**
- 递归 `setTimeout()` 保证执行之间的延迟相同。代码每次运行都是等待100ms，无论代码运行多长时间，间隔都是相同的。
- `setInterval()` 的间隔包括运行代码所花费的时间。假设代码需要40毫秒才能运行，那么间隔最终只有60毫秒。
- 当使用递归 `setTimeout()` 时，每次迭代都可以设置不同的延迟时间，即第二个参数是在代码再次运行前指定的不同等待时间。

当代码的运行时间可能比分配的时间间隔更长时，最好使用递归 `setTimeout()`。这将使执行之间的时间间隔保持不变，保证无论代码执行多长时间，都不会得到错误。

<br>

## requestAnimationFrame()
`requestAnimationFrame()` 是一个专门的循环函数，旨在浏览器中高效运行动画。它基本上是现代版本的 `setInterval()` —— 它在浏览器重新加载显示内容之前执行指定的代码块，从而允许动画以适当的帧速率运行，不管其运行的环境如何。

它是针对 `setInterval()` 遇到的问题创建的，比如 `setInterval()` 并不是针对设备优化的帧率运行，有时会丢帧。

该方法将 重新加载页面之前要调用的回调函数 作为参数。这是常见表达：
```js
function draw() {
   // Drawing code goes here
   requestAnimationFrame(draw);
}

draw();
```

先定义一个函数，在其中更新动画，然后调用它来开始这个过程。在函数的末尾，以 `requestAnimationFrame()` 传递的函数作为参数进行调用，指示浏览器在下一次显示重新绘制时再次调用该函数。并且这个操作连续执行，因为 `requestAnimationFrame()` 是递归调用的。

> 注：如果要执行某种简单的常规 DOM 动画，CSS 动画可能更快，因为它们是由浏览器的内部代码计算而不是 JavaScript 直接计算的。但是，如果你正在做一些更复杂的事情，并且涉及到在 DOM 中不能直接访问的对象（例如 2D Canvas API、WebGL objects），`requestAnimationFrame()` 在大多数情况下是更好的选择。

> 注：在 Internet Explorer 10 及更高版本中可用。

<br>

**你的动画跑得有多快？**

动画的平滑度直接取决于动画的帧速率（fps）。帧数越高，动画看起来就越平滑。

如果你希望显示达到60fps，则大约有 1000/60 毫秒来执行动画代码来渲染每个帧。我们需要注意每次通过动画循环时要运行的代码量，更多的帧意味着更多的处理，这通常会导致丢帧或跳帧。

`requestAnimationFrame()` 会尽其所能利用现有资源提升帧速，尽可能接近理想帧数率（60帧/秒）。但当你有一个非常复杂的动画并且在一个缓慢的计算机上运行它，你的帧速率通常会达不到理想值甚至更少。

<br>

**requestAnimationFrame() 与 setInterval() 和 setTimeout()有什么不同?**

使用 `requestAnimationFrame()`：
```js
function draw() {
   // Drawing code goes here
   requestAnimationFrame(draw);
}

draw();
```

使用 `setInterval()`：
```js
function draw() {
   // Drawing code goes here
}

setInterval(draw, 17);
```

如前所述，我们没有为 `requestAnimationFrame();` 指定时间间隔；它只是在当前条件下尽可能快速平稳地运行它。如果动画由于某些原因而处于屏幕外，浏览器就不会浪费时间运行它。

`setInterval()` 需要指定间隔。浏览器会尝试保持运行动画的帧数率超过60fps（17 > 1000/60），并保持这个速度不变，即使浏览器环境和运行条件发生改变。

<br>

**添加时间戳**

在 javascript 中，时间戳（timestamp）是指从格林威治时间1970年01月01日00时00分00秒（UTC/GMT的午夜）起至现在的总秒数。时间戳通常是一个字符序列，唯一地标识某一刻的时间。

传递给 `requestAnimationFrame()` 函数的实际回调可以被赋予一个参数（一个时间戳值），表示自 `requestAnimationFrame()` 开始运行以来的时间。这是很有用的，因为它允许你在特定的时间以恒定的速度运行，而不管你的设备有多快或多慢。

一般模式如下：
```js
let startTime = null;

function draw(timestamp) {
    if(!startTime) {
      startTime = timestamp;
    }

   currentTime = timestamp - startTime;

   // Do something based on current time

   requestAnimationFrame(draw);
}

draw();
```

<br>

**撤销requestAnimationFrame()**

`requestAnimationFrame()` 可用与之对应的 `cancelAnimationFrame()` 方法“撤销”（不同于 set 类方法的“清除”，此处更接近“撤销”）。
```js
cancelAnimationFrame(rAF);
```

<br>

**限制（节流）requestAnimationFrame() 动画**

`requestAnimationFrame()` 的限制之一是无法选择帧率。在大多数情况下，这不是问题，因为通常希望动画尽可能流畅地运行。但是，当要创建老式的8位类型的动画时，怎么办？

首先，先解释一下“精灵图序列”。图片如下：

![](2.png)

图中包含六个精灵，它们组成了一趟完整的行走序列。每个精灵的尺寸为 102 × 148 像素。为了整齐的显示一个精灵，可以通过 drawImage() 来从序列中裁切出单独的精灵并隐藏其他部分。不断切换不同动作的精灵，就可以实现走路了。

在此示例中，必须为角色在屏幕上的位置及显示的精灵设置动画。精灵动画中只有6帧。如果通过 `requestAnimationFrame()` 为屏幕上显示的每个帧显示不同的精灵帧，精灵的四肢就会移动太快，动画看起来很荒谬。因此，此示例使用以下代码限制精灵循环的帧率：
```js
if (posX % 13 === 0) {
  if (sprite === 5) {
    sprite = 0;
  } else {
    sprite++;
  }
}
```

因此，代码每13个动画帧（posX）循环一次精灵。

实际上，大约是每 6.5 帧，因为我们将每帧更新 posX 2个单位值（角色在屏幕上的位置）
```js
//计算如何更新每个动画帧中的位置
if(posX > width/2) {
  newStartPos = -( (width / 2) + 102 );
  posX = Math.ceil(newStartPos / 13) * 13;
  console.log(posX);
} else {
  posX += 2;
}
```

用于限制动画的方法将取决于特定代码。我们可以根据需要编写特定的代码实现节流 requestAnimationFrame 动画。

<br>

# 异步处理promises
Promise 允许你推迟进一步的操作，知道上一个操作完成或响应失败。当我们不知道函数的返回值或返回需要多长时间时，Promises 是构建异步应用程序的好方法。

<br>

## 什么是promises
本质上，Promise 是一个对象，代表操作的中间状态，正如它的单词含义 '承诺' ，它保证在未来可能返回某种结果。虽然 Promise 并不保证操作在何时完成并返回结果，但是它可以保证当结果可用时，你的代码能正确处理结果，当结果不可用时，你的代码可以用来处理错误。

Promise 常见的交互之一就是 Web API 返回的 promise 对象。

让我们设想一个视频聊天应用程序，你可以点击一个按钮对朋友视频呼叫。该按钮的处理程序调用 `getUserMedia()` 来访问用户的摄像头和麦克风。由于 `getUserMedia()` 必须确保用户具有使用这些设备的权限，并询问用户要使用哪个麦克风和摄像头等问题，因此它会产生阻塞，直到用户做出所有的决定，并启用摄像头和麦克风。

由于 `getUserMedia()` 是在浏览器的主线程进行调用，整个浏览器将会处于阻塞状态直到 `getUserMedia()` 返回。因此 `getUserMedia()` 返回一个 Promise 对象——只有当 MediaStream 流可用才去解析，而不是等待用户操作、启动选中的设备并直接返回从所选资源创建的 MediaStream 流。

上述视频聊天应用程序的代码：
```js
function handleCallButton(evt) {
  setStatusMessage("Calling...");
  navigator.mediaDevices.getUserMedia({video: true, audio: true})
    .then(chatStream => {
      selfViewElem.srcObject = chatStream;
      chatStream.getTracks().forEach(track => myPeerConnection.addTrack(track, chatStream));
      setStatusMessage("Connected");
    }).catch(err => {
      setStatusMessage("Failed to connect");
    });
}
```

这个函数在开头调用 `setStatusMessage()` 来更新状态显示信息 “Calling...”，表示正在尝试通话。接下来调用 `getUserMedia()`，请求具有视频及音频轨的流，一旦获得这个流，就将其显示在 selfViewElem 的 video 元素中。接下来将这个流的每个轨道添加到表示与另一个用户的连接的 WebRTC，参见 RTCPeerConnection。在这之后，状态显示为 “Connected”。

如果 `getUserMedia()` 失败，则 catch 块运行。这使用 `setStatusMessage()` 更新状态框以指示发生错误。

<br>

## 回调函数的麻烦
回想之前的 callback，理解它们造成的困难，明白为什么使用 promise。

我们以订购披萨为例。为了使你的订单成功，你必须按顺序执行：
1. 选择配料
2. 下订单
3. 接收披萨

对于旧式callbacks，上述功能的伪代码表示：
```js
chooseToppings(function(toppings) {
  placeOrder(toppings, function(order) {
    collectOrder(order, function(pizza) {
      eatPizza(pizza);
    }, failureCallback);
  }, failureCallback);
}, failureCallback);
```

重复的嵌套和多次调用的 failureCallback，这被称为回调地狱。

**使用promise改良**

Promises 使得上面的情况更容易编写，解析和运行。使用异步 promises 重写伪代码：
```js
chooseToppings()
.then(function(toppings) {
  return placeOrder(toppings);
})
.then(function(order) {
  return collectOrder(order);
})
.then(function(pizza) {
  eatPizza(pizza);
})
.catch(failureCallback);
```

`.then()` 块都会返回一个新的 promise，使我们能够一个接一个地链接多个异步操作；而 `.catch()` 块来处理所有错误；

使用箭头函数进一步简化代码：
```js
chooseToppings()
.then(toppings =>
  placeOrder(toppings)
)
.then(order =>
  collectOrder(order)
)
.then(pizza =>
  eatPizza(pizza)
)
.catch(failureCallback);
```

使用箭头 `() => x` 可以将括号内的参数传递给 x 函数。

> 注：你可以使用 async/await 语法进行进一步的改进，我们将在下一篇文章中深入讨论。

最基本的，promise 与事件监听器类似，但有一些差异：
- 一个 promise 只能成功或失败一次；操作完成后，promise 无法在成功和失败状态间切换。
- 如果 promise 已经成功或失败，你再添加成功/失败回调，promsie 依旧会调用正确的回调

<br>

## promise的基本语法
Promises 很重要，因为大多数现代 Web API 都将它们用于执行潜在冗长任务的函数。

<br>

接下来是一个 Web API 的简单示例。

1\. 首先，下载 [simple HTML template](https://github.com/a-pin/learning-area/blob/main/html/introduction-to-html/getting-started/index.html) 和 [sample image file](https://github.com/a-pin/learning-area/blob/main/javascript/asynchronous/promises/coffee.jpg)。

2\. 将 `<script>` 元素添加在HTML `<body>` 的底部。

3\. 在 `<script>` 元素内，添加以下行：
```js
let promise = fetch('coffee.jpg');
```

`fetch()` 将 URL 作为参数从网络中获取资源。我们将 `fetch()` 返回的 promise 对象存储在一个名为 promise 的变量中。这个对象代表了既不成功也不失败的中间状态，这个状态下的 promise 的官方术语叫作 pending。

> 对象的状态不受外界影响。Promise 对象代表一个异步操作，有三种状态：
> - pending: 初始状态，不是成功或失败状态
> - fulfilled: 意味着操作成功完成
> - rejected: 意味着操作失败

4\. 为了响应成功完成操作，我们调用 promise 对象的 `.then()` 方法。`.then()` 块中的回调接受 fecth 方法返回的原始 Response，经过 blob 方法处理后返回 Blob 格式的 Response 对象。

> Fetch API 的 Response 接口呈现了对一次请求的响应数据。
>
> Promimse 的构造函数接受一个函数，这个函数的两个参数分别是 resolve 方法和 reject 方法。当任务成功时，调用 resolve() 方法，失败时，调用 reject() 方法。调用 resolve 和 reject 时，传入的值将作为输入参数，传递到下一级 then 方法的 resolve 和 reject 中。
>
> fecth() 返回 promise 对象，then 中以 resolve 接收 response，同样会返回一个 promise 对象，构成了数据的流动。即传入 response 的是上一个 resolve 函数，接受 response 的是当前的 resolve 函数。

我们立即对此响应运行 `blob()` 方法以确保响应主体完全下载，并且当它可用时将其转换为我们可以执行某些操作的 Blob 对象。返回的结果如下：
```js
function(response) {
    return response.blob();
}

//简写
response => response.blob();
```

> `Response` 实现了 `Body` 接口，因此 `Body.blob()` 方法可用，它用于读取 Response 对象并且将它设置为已读（因为 Responses 对象被设置为了 stream 的方式，所以它们只能被读取一次），并返回一个被解析为 Blob 格式的 Promise 对象。

Fetch promises 不会产生 404 或 500 错误，只有在产生像网路故障的情况时才会不工作。总的来说，Fetch promises 总是成功运行，即使 response.ok 属性是 false。为了产生 404 错误，我们需要判断 response.ok，如果是 false，抛出错误，否则返回 blob。就像下面的代码这样做。
```js
let promise2 = promise.then(response => {
  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  } else {
    return response.blob();
  }
});
```

5\. 每次调用 `.then()` 都会创建一个新的 promise。因此 `blob()` 方法也返回一个 promise，我们可以通过调用第二个 promise 的 `.then()` 方法来处理它在履行时返回的 Blob 对象。因为我们想要对 blob 执行一些更复杂的操作，而不仅仅运行单个方法并返回结果，这次我们需要将函数体包装成花括号（否则会抛出错误）。

将以下内容添加到代码的末尾：
```js
let promise3 = promise2.then(myBlob => {})
```

6\. 现在让我们填写执行程序函数的主体。在花括号内添加以下行：
```js
let objectURL = URL.createObjectURL(myBlob);
let image = document.createElement('img');
image.src = objectURL;
document.body.appendChild(image);
```

这里我们运行 `URL.createObjectURL()` 方法，将其作为 Blob 在第二个 promise 实现时返回的参数传递。这将返回指向该对象的 URL。然后我们创建一个 `<img>` 元素，将其 src 属性设置为等于对象 URL 并将其附加到 DOM，这样图像就会显示在页面上。

如果你保存刚刚创建的 HTML 文件并将其加载到浏览器中，你将看到图像按预期显示在页面中。

> 注：这个例子的目的是展示 promise，其实不需要这么复杂。实际上，只需要建立 img 元素并设置 src 属性就可以。

<br>

**响应失败**

我们可以通过 promise 的 `.catch()` 方法来添加错误处理：
```js
let errorCase = promise3.catch(e => {
  console.log('There has been a problem with your fetch operation: ' + e.message);
});

//该错误将在浏览器的开发人员工具的控制台中报告
```

`.catch()` 使我们可以完全控制错误处理方式。在真实的应用程序中，你的 `.catch()` 块可以重试获取图像，或显示默认图像，或提示用户提供不同的图像 URL 等等。

<br>

**将代码块链在一起**

这是写出来的一种非常简便的方式，将 `.then()` 块以及 `.catch()` 块链接在一起：
```js
fetch('coffee.jpg')
.then(response => {
  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  } else {
    return response.blob();
  }
})
.then(myBlob => {
  let objectURL = URL.createObjectURL(myBlob);
  let image = document.createElement('img');
  image.src = objectURL;
  document.body.appendChild(image);
})
.catch(e => {
  console.log('There has been a problem with your fetch operation: ' + e.message);
});
```

*注意：完成运行的 promise 所返回的值将成为传递给下一个 `.then()` 块的执行函数的参数。*

> 注：promise 中的 `.then()/catch()` 块基本上是同步代码中 `try...catch` 块的异步等价物。但是，同步 `try ... catch` 在异步代码中不起作用。

<br>

> **promise回顾**
> 
> 1\. 创建 promise 时，它既不是成功也不是失败状态。这个状态叫作 pending（待定）。
>
> 2\. 当 promise 返回时，称为 resolved（已解决）
> 1. 一个成功 resolved 的 promise 称为 fullfilled（实现）。它返回一个值，可以通过将 `.then()` 块链接到 promise 链的末尾来访问该值。
> 2. 一个失败 resolved 的 promise 被称为 rejected（拒绝）了。它返回一个原因，一条错误消息，说明为什么 promise 没有成功解决。可以通过将 `.catch()` 块链接到 promise 链的末尾来访问此原因。

<br>

## 响应多个promises的实现
如果你想在一大堆 Promises 全部完成之后运行一些代码，该怎么办？你可以使用 `Promise.all()` 静态方法完成此操作。

`Promise.all()` 将一个 **promises 数组**作为输入参数，并返回一个新的 Promise 对象，只有当数组中的所有 promise 都满足时才会满足。例如：
```js
Promise.all([a, b, c]).then(values => {
  ...
});
```

如果它们都实现，那么数组中的结果将作为参数传递给 `.then()` 块中的执行器函数。

让显示网页 UI 为例来展示这一点：

1\. 构建本地环境。将[页面模板](https://github.com/a-pin/learning-area/blob/main/html/introduction-to-html/getting-started/index.html)和源文件([coffee.jpg](https://github.com/a-pin/learning-area/blob/main/javascript/asynchronous/promises/coffee.jpg), [tea.jpg](https://github.com/a-pin/learning-area/blob/main/javascript/asynchronous/promises/tea.jpg)和 [description.txt](https://github.com/a-pin/learning-area/blob/main/javascript/asynchronous/promises/description.txt))保存至本地同一目录下，并在 html 文件的 `</body>` 标记之前放置一个 `<script>` 元素。

2\. 在脚本中，首先定义一个函数，该函数返回我们要发送给 `Promise.all()` 的 promise。

如果我们只想运行 `Promise.all()` 块以响应三个 fetch() 操作完成，这将很容易。我们可以这样做：
```js
let a = fetch(url1);
let b = fetch(url2);
let c = fetch(url3);

Promise.all([a, b, c]).then(values => {
  ...
});
```

当 promise 是 fullfilled 时，传递到处理程序的 values 将包含三个 Response 对象。

> fecth() 返回 promise 对象，then 中以 resolve 接收 response。

但是，我们需要资源加载的数据。因此，我们得在获得代表资源的可用 blob 和可用的 txt 后再运行 `Promise.all()` 块。编写一个执行此操作的函数：
```js
function fetchAndDecode(url, type) {
  return fetch(url).then(response => {
    if (type === 'blob') {
      return response.blob();
    } else if (type === 'text') {
      return response.text();
    }
  })
  .catch(e => {
    console.log('There has been a problem with your fetch operation: ' + e.message);
  });
}
```

4\. 接下来，我们调用我们的函数三次以开始获取和解码图像和文本的过程，并将每个返回的 promises 存储在变量中。在以前的代码下面添加以下内容：
```js
let coffee = fetchAndDecode('coffee.jpg', 'blob');
let tea = fetchAndDecode('tea.jpg', 'blob');
let description = fetchAndDecode('description.txt', 'text');
```

接下来，定义一个 `Promise.all()` 块，仅当上面存储的所有三个 promise 都已成功完成时才运行一些代码。首先，在 `.then()` 调用中添加一个带有空执行程序的块，如下所示：
```js
Promise.all([coffee, tea, description]).then(values => {

});
```

你可以看到它需要一个包含 promises 作为参数的数组。执行者只有在所有三个 promises 的状态成为 resolved 时才会运行；当发生这种情况时，它将被传入一个数组，其中包含来自各个 promise 的结果，类似于 [coffee-results, tea-results, description-results]。

5\. 最后，在执行程序中添加以下内容。这里我们使用一些相当简单的同步代码将结果存储在单独的变量中（从 blob 创建对象 URL），然后在页面上显示图像和文本。
```js
console.log(values);
// Store each value returned from the promises in separate variables; create object URLs from the blobs
let objectURL1 = URL.createObjectURL(values[0]);
let objectURL2 = URL.createObjectURL(values[1]);
let descText = values[2];

// Display the images in <img> elements
let image1 = document.createElement('img');
let image2 = document.createElement('img');
image1.src = objectURL1;
image2.src = objectURL2;
document.body.appendChild(image1);
document.body.appendChild(image2);

// Display the text in a paragraph
let para = document.createElement('p');
para.textContent = descText;
document.body.appendChild(para);
```

保存并刷新，你应该看到所有UI组件都已加载。

![](3.png)

<br>

## finally()
在现代浏览器中，`.finally()` 方法可用，无论 promise 是实现还是拒绝，finally 块都将运行：
```js
myPromise
.then(response => {
  doSomething(response);
})
.catch(e => {
  returnError(e);
})
.finally(() => {
  runFinalCode();
});
```

> 注：`finally()` 允许你在异步代码中编写异步等价物 try/ catch / finally。

## 构建自定义promise
在某种程度上，你已经建立了自己的 promise。当你使用 `.then()` 块链接多个 promise 时，或者将它们组合起来创建自定义函数时，你已经在创建自己的基于异步声明的自定义函数。

迄今为止，你使用 promises 进行自定义事务的常见方式是将不同的基于 promise 的 API 组合在一起以创建自定义函数，展示了基于相同原则的大多数现代 API 的灵活性和强大功能。然而，还有另一种方式。

<br>

### 使用Promise()构造函数
你可以使用 `Promise()` 构造函数构建自己的 promise。

首先，新建一个 Promise 对象：
```js
new Promise(function (resolve, reject) {
    // 要做的事情...
});
```

Promise 构造函数只有一个参数，是一个函数，这个函数在构造之后会直接被异步运行，所以我们称之为起始函数。起始函数包含两个参数 resolve 和 reject。

当 Promise 被构造时，起始函数会被异步执行：
```js
new Promise(function (resolve, reject) {
  console.log("run");
})
```

这段程序会直接输出 **Run**。

**resolve 和 reject 都是函数，其中调用 resolve 代表一切正常，reject 是出现异常时所调用的。**你可以调用 resolve 来解释承诺（向 resolve 函数传入值），调用 reject 函数的承诺将被拒绝，并显示错误消息（向 reject 函数传入的值）。

resolve() 中可以放置一个参数用于向下一个 then 传递一个值，then 中的函数也可以返回一个值传递给 then。但是，如果 then 中返回的是一个 Promise 对象，那么下一个 then 将相当于对这个返回的 Promise 进行操作。

reject() 参数中一般会传递一个异常给之后的 catch 函数用于处理异常。但是请注意以下两点：
- resolve 和 reject 的作用域只有起始函数，不包括 then 以及其他序列；
- resolve 和 reject 并不能够使起始函数停止运行，别忘了 return。

这是一个实例：
```js
let timeoutPromise = new Promise((resolve, reject) => {
  setTimeout(function(){
    resolve('Success!');
  }, 2000);
});
```

此处，promise 成功运行则显示字符串 “Success!”。

将 `.then()` 块链接到末尾，它将传递给 `.then()` 块一个字符串 “Success!”。在下面的代码中，我们显示出该消息：
```js
timeoutPromise
.then((message) => {
   alert(message);
})

//更简化的版本：

timeoutPromise.then(alert);
```

<br>

### 拒绝一个自定义promise
我们可以创建一个 `reject()` 方法来拒绝承诺，就像 `resolve()` 一样，这需要一个值，但在这种情况下，它是出现异常的原因，即将传递给 `.catch()` 的错误块。

让我们扩展前面的例子，使其具有一些 `reject()` 条件，并允许在成功时传递不同的消息：
```js
function timeoutPromise(message, interval) {
  return new Promise((resolve, reject) => {
    if (message === '' || typeof message !== 'string') {
      reject('Message is empty or not a string');
    } else if (interval < 0 || typeof interval !== 'number') {
      reject('Interval is negative or not a number');
    } else {
      setTimeout(function(){
        resolve(message);
      }, interval);
    }
  });
};
```

在这里，我们将两个方法传递给一个自定义函数，一个用来做某事的消息，以及在做这件事之前要经过的时间间隔。在函数内部，我们返回一个新的 Promise 对象，调用该函数将返回我们想要使用的promise。

在 Promise 构造函数中，我们在 if ... else 结构中进行了一些检查：
- 首先，我们检查消息是否适合被警告。如果它是一个空字符串或根本不是字符串，我们会使用合适的错误消息拒绝该 promise。
- 接下来，我们检查间隔是否是适当的间隔值。如果是负数或不是数字，我们会使用合适的错误消息拒绝 promise。
- 最后，如果参数看起来都正常，我们使用 `setTimeout()` 在指定的时间间隔过后，使用指定的消息解释 promise。

由于 `timeoutPromise()` 函数返回一个 Promise，我们可以将 `.then()`，`.catch()` 等链接到它上面：
```js
timeoutPromise('Hello there!', 1000)
.then(message => {
   alert(message);
})
.catch(e => {
  console.log('Error: ' + e);
});
```

<br>

# async和await
async functions 和 await 关键字是最近添加到 JavaScript 语言里面的。它们是 ECMAScript 2017 JavaScript 版的一部分。简单来说，它们是基于 Promise 的语法糖，使异步代码更容易编写和阅读。通过使用它们，异步代码看起来更像是老式同步代码，因此它们非常值得学习。

<br>

## async/await基础

<br>

### async关键字
把 async 关键字放在函数声明之前，使其成为 async function。

例如：
```js
async function hello(){ return "hello" };
hello();
```

调用此函数会返回一个 promise。函数返回 promise 是异步函数的特征之一。

创建一个异步函数的表达式：
```js
let hello = async function() { return "Hello" };
hello();

//使用箭头函数

let hello = async () => { return "Hello" };
```

要实际使用 promise 完成时返回的值，我们可以使用 `.then` 块，它同样会返回一个 promise：
```js
hello().then((value) => console.log(value))

//简写

hello().then(console.log)
```

将 async 关键字加到函数申明中，可以要求它们返回 promise 而不是直接返回值。此外，它避免了同步函数为支持使用 await 带来的任何潜在开销。

<br>

### await关键字
await 只在异步函数里起作用。它可以放在任何异步的，基于 promise 的函数之前。它会暂停代码在该行上，直到 promise 完成，然后返回结果值。在暂停的同时，其他正在等待执行的代码就有机会执行了。

你可以在调用任何返回 promise 的函数时使用 await，包括 Web API 函数。

例如：
```js
async function hello() {
  return greeting = await Promise.resolve("Hello");
};

hello().then(alert);
```

> `Promise.resolve(value)` 方法返回一个解析给定值的 Promise 对象。
> - value：将被 Promise 对象解析的参数。
> - 返回值：返回一个带着给定值解析过的 Promise 对象。

<br>

## async/await实例
使用 async/await 重写 promise 代码，回顾上文的 fecth 示例：
```js
fetch('coffee.jpg')
.then(response => response.blob())
.then(myBlob => {
  let objectURL = URL.createObjectURL(myBlob);
  let image = document.createElement('img');
  image.src = objectURL;
  document.body.appendChild(image);
})
.catch(e => {
  console.log('There has been a problem with your fetch operation: ' + e.message);
});
```

将其转化为使用 async/await 的代码：
```js
async function myFetch() {
  let response = await fetch('coffee.jpg');
  let myBlob = await response.blob();

  let objectURL = URL.createObjectURL(myBlob);
  let image = document.createElement('img');
  image.src = objectURL;
  document.body.appendChild(image);
}

myFetch()
.catch(e => {
  console.log('There has been a problem with your fetch operation: ' + e.message);
});
```

它去除了 `.then()` 代码块，由于 async 关键字将函数转化为 promise，你可以重构以上代码——使用 promise 和 await 的混合方式，将函数后半部分抽取到新代码块中。这样做可以更灵活：
```js
async function myFetch() {
  let response = await fetch('coffee.jpg');
  return await response.blob();
}

myFetch().then((blob) => {
  let objectURL = URL.createObjectURL(blob);
  let image = document.createElement('img');
  image.src = objectURL;
  document.body.appendChild(image);
});
```

<br>

**它到底是如何工作的？**

使用 async 关键字创建一个异步函数，其中的代码异步执行；await 只能在异步函数内部工作。

在 `myFetch()` 函数定义中，你可以看到代码不需要附加 `.then()` 代码块到每个 promise-based 方法的结尾，你只需要在方法调用前添加 await 关键字，然后把结果赋给变量。await 关键字使 JavaScript 运行时暂停于此行，允许其他代码在此期间执行，直到异步函数调用返回其结果。一旦完成，你的代码将继续从下一行开始执行。例如：
```js
let response = await fetch('coffee.jpg');
```

解析器会在此行暂停，直到当服务器返回的响应变得可用。此时 `fetch()` 返回的 promise 将会完成（fullfilled），返回的 response 会被赋值给 response 变量。接着，解析器就会移动到下一行，创建一个 Blob。Blob 这行也调用基于异步 promise 的方法，因此我们也在此处使用 await。当操作结果返回时，我们将它从 `myFetch()` 函数中返回。

由于 `myFetch()` 返回一个 promise，我们可以将 `.then` 连接到它的末尾。async/await 用更少的 `.then` 块来封装代码，使得异步代码看起来更像同步代码，变得非常直观。

<br>

**添加错误处理**

添加错误处理有多种方式。

你可以将同步的 try...catch 结构和 async/await 一起使用，示例展示了第一个版本代码：
```js
async function myFetch() {
  try {
    let response = await fetch('coffee.jpg');
    let myBlob = await response.blob();

    let objectURL = URL.createObjectURL(myBlob);
    let image = document.createElement('img');
    image.src = objectURL;
    document.body.appendChild(image);
  } catch(e) {
    console.log(e);
  }
}

myFetch();
```

`catch() {}` 代码块会接收一个错误对象 e；将其显示到控制台，它将向我们提供详细的错误消息。

对于上面第二个版本代码，最好继续将 `.catch()` 块链接到 `.then()` 调用的末尾：
```js
async function myFetch() {
  let response = await fetch('coffee.jpg');
  return await response.blob();
}

myFetch().then((blob) => {
  let objectURL = URL.createObjectURL(blob);
  let image = document.createElement('img');
  image.src = objectURL;
  document.body.appendChild(image);
})
.catch((e) =>
  console.log(e)
);
```

这是因为 `.catch()` 块将捕获来自异步函数调用和 promise 链中的错误。如果在此处使用 try/catch 代码块，则在调用 myFetch() 函数时，仍可能会收到未处理的错误。

<br>

## 等待Promise.all()
**async/await 建立在 promises 之上，因此它与 promises 提供的所有功能兼容。**这包括 `Promise.all()`，你完全可以通过调用 `await Promise.all()` 将所有结果返回到变量中，就像同步代码一样。

将上文 `Promise.all()` 示例其转换为 async/await 格式：
```js
async function fetchAndDecode(url, type) {
  let response = await fetch(url);

  let content;

  if(type === 'blob') {
    content = await response.blob();
  } else if(type === 'text') {
    content = await response.text();
  }

  return content;
}

async function displayContent() {
  let coffee = fetchAndDecode('coffee.jpg', 'blob');
  let tea = fetchAndDecode('tea.jpg', 'blob');
  let description = fetchAndDecode('description.txt', 'text');

  let values = await Promise.all([coffee, tea, description]);

  let objectURL1 = URL.createObjectURL(values[0]);
  let objectURL2 = URL.createObjectURL(values[1]);
  let descText = values[2];

  let image1 = document.createElement('img');
  let image2 = document.createElement('img');
  image1.src = objectURL1;
  image2.src = objectURL2;
  document.body.appendChild(image1);
  document.body.appendChild(image2);

  let para = document.createElement('p');
  para.textContent = descText;
  document.body.appendChild(para);
}

displayContent()
.catch((e) =>
  console.log(e)
);
```

可以看到 `fetchAndDecode()` 函数只进行了一丁点的修改就转换成了异步函数：
```js
let values = await Promise.all([coffee, tea, description]);
```

在这里，通过使用 await，我们能够在三个 promise 的结果都可用的时候，放入 values 数组中。这看起来非常像同步代码。我们需要将所有代码封装在一个新的异步函数 `displayContent()` 中，尽管没有减少很多代码，但能够将大部分代码从 `.then()` 代码块移出，使代码得到了简化，更易读。

<br>

## async/await的缺陷
了解 async/await 是非常有用的，但还有一些缺点需要考虑。

async/await 让你的代码看起来是同步的，在某种程度上，也使得它的行为更加地同步。 await 关键字会阻塞其后的代码，直到 promise 完成，就像执行同步操作一样。它确实可以允许其他任务在此期间继续运行，但接下来的代码会被阻塞。

这意味着您的代码可能会因为大量 await 的 promises 相继发生而变慢。每个 await 都会等待前一个完成，而你实际想要的是所有的这些 promises 同时开始处理，就像我们没有使用 async/await 时那样。

有一种模式可以缓解这个问题——通过将 Promise 对象存储在变量中来同时开始它们，然后等待它们全部执行完毕。

没有经过优化的 async/await 代码，例如：
```js
async function timeTest() {
  await timeoutPromise(3000);
  await timeoutPromise(3000);
  await timeoutPromise(3000);
}
```

在这里，我们直接等待所有三个 `timeoutPromis()` 调用，使每个调用3秒钟。后续的每一个都被迫等到最后一个完成，完成时间即9秒。

优化后的代码：
```js
async function timeTest() {
  const timeoutPromise1 = timeoutPromise(3000);
  const timeoutPromise2 = timeoutPromise(3000);
  const timeoutPromise3 = timeoutPromise(3000);

  await timeoutPromise1;
  await timeoutPromise2;
  await timeoutPromise3;
}
```

在这里，我们将三个 Promise 对象存储在变量中，这样可以同时启动它们关联的进程。因为 promise 都在基本上同时开始处理，promise 将同时完成，即总时间为3秒。

你需要牢记 async/await 代码在性能上的这个缺陷，将等待执行的 promise 变量封装在异步函数中。

<br>

## async/await的类方法
我们可以在类/对象方法前面添加 async，以使它们返回 promises，并 await 它们内部的 promises。例如：
```js
class Person {
  constructor(first, last, age, gender, interests) {
    this.name = {
      first,
      last
    };
    this.age = age;
    this.gender = gender;
    this.interests = interests;
  }

  async greeting() {
    return await Promise.resolve(`Hi! I'm ${this.name.first}`);
  };

  farewell() {
    console.log(`${this.name.first} has left the building. Bye for now!`);
  };
}

let han = new Person('Han', 'Solo', 25, 'male', ['Smuggling']);
```

第一个实例方法可以使用如下：
```js
han.greeting().then(console.log);
```

> async/await 提供了一种很好的，简化的方法来编写更易于阅读和维护的异步代码。

<br>

# 选择正确的方法
在这里，我们将简要讨论之前章节谈论过的编码技术和功能，在不同情况乱下，你应该使用哪个，并提供适当的建议和提醒。

<br>

## 异步回调
通常在旧式 API 中找到，将函数作为参数传递给另一个函数，在异步操作完成时调用该函数，可以依次对结果执行某些操作。它不那么高效或灵活，仅在必要时使用。

缺陷
- 嵌套回调可能很麻烦且难以阅读（即“回调地狱”）
- 每层嵌套都需要故障回调，而使用 promises，您只需使用一个 `.catch` 代码块来处理整个链的错误。
- Promise 回调总是按照它们放在事件队列中的严格顺序调用；异步回调不是。
- 当传入到一个第三方库时，异步回调对函数如何执行失去完全控制。 

<br>

## setTimeout()
`setTimeout()` 是一种允许您在经过任意时间后运行函数的方法。

递归 `setTimeout()` 和 `setInterval()` 之间存在差异：
- 递归 `setTimeout()` 保证两次执行间经过指定的时间量；代码将运行，然后等待100毫秒再次运行。无论代码运行多长时间，间隔都是相同的。
- 使用 `setInterval()`，我们选择的时间间隔包含了运行代码所花费的时间。以100ms为例，假设代码需要40毫秒才能运行，间隔最终只会有60毫秒。

因此，当你的代码有可能比你分配的时间间隔更长时间运行时，最好使用递归的 `setTimeout()`，这将使执行之间的时间间隔保持不变，无论代码执行多长时间，你不会得到错误。

## setInterval()
`setInterval()` 函数允许重复执行一个函数，并设置时间间隔。不如 `requestAnimationFrame()` 有效率，但允许您选择运行速率/帧速率。

帧速率未针对运行动画的系统进行优化，并且可能效率低下。除非你需要选择特定（较慢）的帧速率，否则通常最好使用 `requestAnimationFrame()`。

<br>

## requestAnimationFrame()
`requestAnimationFrame()` 是一种允许您以给定当前浏览器/系统的最佳帧速率重复且高效地运行函数的方法。

`requestAnimationFrame()` 无法选择特定的帧速率，除非你需要特定的速率帧，否则你应该尽可能使用它而不要去使用 `setInterval()` 或者 递归 `setTimeout()`。

<br>

## Promises
Promises 是一种 JavaScript 功能，允许您运行异步操作并等到它完全完成后再根据其结果运行另一个操作，是现代异步 JavaScript 的支柱。

<br>

**Promise.all()**

一种 JavaScript 功能，允许您等待多个 promises 完成，然后根据所有其他 promises 的结果运行进一步的操作。

如果 `Promise.all()` 拒绝，那么你在其数组参数中输入的一个或多个 promise 就会被拒绝，或者可能根本不返回 promises。你需要检查每一个，看看他们返回了什么。

<br>

## async/await
构造在 promise 之上的语法糖，允许您使用更像编写同步回调代码的语法来运行异步操作。

缺陷
- 你不能在非 async 函数内或代码的顶级上下文环境中使用 await 运算符。
- 浏览器对 async/await 的支持不如 promise 那样好。