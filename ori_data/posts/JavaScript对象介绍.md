---
title: JavaScript对象介绍
description: 本文将详细介绍 JavaScript 对象的理论和语法，再介绍如何创建对象。
tags:
- JavaScript
categories:
- web
---

在此特地声明本文是根据 [mozilla官方教学文档](https://developer.mozilla.org/zh-CN/docs/Learn/html/Introduction_to_html) 学习的个人学习笔记，借用了大量的图片和文本内容，存在相当多的相同，但不是copy。如需查看mozilla官方文档，请点击前文链接！！
<!--more-->

<br>

# javascript对象基础
本节将学习有关对象基础的语法，并且回顾一些之前学习过的 JavaScript 的一些特点，使你明白你所使用过的一些功能实际上是由对象提供的。

我们将用以下 <span id="exercises"></span>oojs-exercises.html 作为基础探索对象的基础语法：
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Object-oriented JavaScript example</title>
  </head>

  <body>
    <p>This example requires you to enter commands in your browser's JavaScript console (see <a href="https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_are_browser_developer_tools">What are browser developer tools</a> for more information).</p>

  </body>

    <script>

    </script>
</html>
```

<br>

## 对象基础
对象是一个包含相关数据和方法的集合（通常由一些变量和函数组成，我们称之为对象里面的属性和方法）。

如同 Javascript 中的很多东西一样，创建一个对象通常先定义初始化变量。 尝试在您已有的文件中 JavaScript 代码下面输入以下内容, 保存刷新页面:
```js
var person = {};
```

如果你在浏览器控制台输入 person，你会得到如下结果：
```js
[object Object]
```

这是一个空对象，因此更新下我们的对象：
```js
var person = {
  name : ['Bob', 'Smith'],
  age : 32,
  gender : 'male',
  interests : ['music', 'skiing'],
  bio : function() {
    alert(this.name[0] + ' ' + this.name[1] + ' is ' + this.age + ' years old. He likes ' + this.interests[0] + ' and ' + this.interests[1] + '.');
  },
  greeting: function() {
    alert('Hi! I\'m ' + this.name[0] + '.');
  }
};
```

保存刷新后, 尝试在你的浏览器控制台输入下面的内容:
```js
person.name[0]
person.age
person.interests[1]
person.bio()
person.greeting()
```

对象成员的值可以是任意的，在我们的 person 对象里有字符串、数字、两个数组和两个函数。前4个成员是资料项目，被称为对象的**属性**；后两个成员是函数，允许对象对资料做一些操作，被称为对象的**方法**。

一个对象由许多的成员组成，每一个成员都拥有一个名字，和一个值。每一个名字/值（name/value）对被逗号分隔开，并且名字和值之间由冒号（:）分隔，语法规则如下所示：

```js
var objectName = {
  member1Name : member1Value,
  member2Name : member2Value,
  member3Name : member3Value
}
```

一个如上所示的对象被称之为对象的**字面量(literal)**——手动的写出对象的内容来创建一个对象。不同于从类实例化一个对象，我们会在后面学习这种方式。

当你想要传输一些有结构和关联的资料时常见的方式是使用字面量来创建一个对象，举例来说，发起一个请求到服务器以存储一些数据到数据库，发送一个对象要比分别发送这些数据更有效率，而且比起数组更为易用，因为你使用名字(name)来标识这些资料。

<br>

## 创建对象
Javascript 没有像许多面向对象的语言一样有用于创建 class 类的声明，而是用一种称为**构建函数**的特殊函数来定义对象和它们的特征。**构建函数**提供了创建你所需对象（实例）的有效方法，将对象的数据和特征函数**按需联结**至相应对象。

JavaScript 在对象间使用和其它语言的共享机制不同，JavaScript 构建函数创建的新实例的特征并非全盘复制，而是通过一个叫做**原形链**的参考链链接过去的，因此这个新实例算不上真正的实例。

除了直接声明一个对象，我们还可以使用构造函数、Object()构造函数 和 create()  方法创建对象。

<br>

### 构造函数
这个构建函数是 JavaScript 版本的类。它只定义了对象的属性和方法，除了没有明确创建一个对象和返回任何值和之外，它有了您期待的函数所拥有的全部功能。
```js
function person(name) {
  this.name = name;
  this.greeting = function() {
    alert('Hi! I\'m ' + this.name + '.');
  };
}
```

调用构建函数创建新的实例：
```js
var person1 = new person('Bob');
var person2 = new person('Sarah');
```

上述代码中，关键字 new 跟着一个含参函数，用于告知浏览器我们想要创建一个对象，非常类似函数调用，并把结果保存到变量中。

> 值得注意的是每次当我们调用构造函数时，我们都会重新定义一遍 greeting()，这不是个理想的方法。为了避免这样，我们可以在原型里定义函数，接下来我们会讲到。

这就是利用构造函数实现 person 对象的结果：<span id="person"></span>
```js
function person(first, last, age, gender, interests) {
  this.name = {
    'first': first,
    'last': last
  };
  this.age = age;
  this.gender = gender;
  this.interests = interests;
  this.bio = function() {
    alert(this.name.first + ' ' + this.name.last + ' is ' + this.age + ' years old. He likes ' + this.interests[0] + ' and ' + this.interests[1] + '.');
  };
  this.greeting = function() {
    alert('Hi! I\'m ' + this.name.first + '.');
  };
};
```

<br>

### Object()构造函数
使用 `Object()` 构造函数创建一个新对象：
```js
var person1 = new Object();
```

然后, 可以根据需要, 使用点或括号表示法向此对象添加属性和方法：
```js
person1.name = 'Chris';
person1['age'] = 38;
person1.greeting = function() {
  alert('Hi! I\'m ' + this.name + '.');
}
```

还可以将对象文本传递给Object() 构造函数作为参数，用属性/方法填充它：
```js
var person1 = new Object({
  name : 'Chris',
  age : 38,
  greeting : function() {
    alert('Hi! I\'m ' + this.name + '.');
  }
});
```

<br>

### create()方法
JavaScript 有个内嵌的方法 `create()`，可以基于现有对象创建新的对象：
```js
var person2 = Object.create(person1);
```

person2 是基于 person1 创建的，它们具有相同的属性和方法。

<br>

## 设置对象成员
更新对象成员的值：
```js
person.age = 45
person['name']['last'] = 'Cratchit'
```

创建新的成员：
```js
person['eyes'] = 'hazel'
person.farewell = function() { alert("Bye everybody!") }
```

括号表示法不仅可以动态的去设置**对象成员的值**；还可以动态的去设置**成员的名字**。

比如说，我们想让用户能够在他们的数据里存储自己定义的值类型，通过两个 input 框来输入成员的名字和值：
```js
var myDataName = nameInput.value
var myDataValue = nameValue.value
```

我们可以这样把这个新的成员的名字和值加到 person 对象里：
```js
person[myDataName] = myDataValue
```

这是使用点表示法无法做到的，**点表示法只能接受字面量的成员的名字，不接受变量作为名字**。

<br>

## 访问对象
当创建好一个对象后，我们需要访问对象内的属性和方法。现在有两种方法可以使用：点表示法、括号表示法。

<br>

### 点表示法
在上面的例子中，你使用了**点表示法**来访问对象的属性和方法。对象的名字表现为一个**命名空间**，它必须写在第一位——当你想访问对象内部的属性或方法时，然后是一个点(.)，紧接着是你想要访问的项目：
```js
person.age    //属性的名字
person.interests[1]    //数组属性的一个子元素
person.bio()    //对象的方法调用
```

<br>

**子命名空间**：可以用一个对象来做另一个对象成员的值。

例如：
```js
name : ['Bob', 'Smith'],

//改成

name : {
  first : 'Bob',
  last : 'Smith'
},
```

这样，我们实际上创建了一个**子命名空间**，当你想访问它时，你只需要链式的再使用一次点表示法：
```js
person.name.first
person.name.last
```

<br>

### 括号表示法
使用括号表示法：
```js
person.age
person.name.first
```

使用如下所示的代码：
```js
person['age']
person['name']['first']
```

这看起来很像访问一个数组的元素，从根本上来说是一回事儿，你使用了关联了值的名字，而不是索引去选择元素。因此对象有时被称之为**关联数组**（对象做了字符串到值的映射，而数组做的是数字到值的映射）。

> 注：每个页面在加载完毕后，会有一个 Document 的实例被创建，叫做 document，它代表了整个页面的结构，内容和一些功能，比如页面的 URL。同样的，这意味 document 有一些可用的方法和属性。例如，`document.createElement('div');` 和 `document.querySelector('video');`。

<br>

## this的含义
```js
greeting: function() {
  alert('Hi! I\'m ' + this.name.first + '.');
}
```

关键字 this 指向了当前代码运行时的对象，它保证了当代码的上下文改变时变量的值的正确性（比如：不同的person对象拥有不同的name这个属性，很明显greeting这个方法需要使用的是它们自己的name）。

例如：
```js
var person1 = {
  name : 'Chris',
  greeting: function() {
    alert('Hi! I\'m ' + this.name + '.');
  }
}

var person2 = {
  name : 'Brian',
  greeting: function() {
    alert('Hi! I\'m ' + this.name + '.');
  }
}
```

在这里，person1.greeting() 会输出："Hi! I'm Chris."；person2.greeting() 会输出："Hi! I'm Brain."，即使 greeting 这个方法的代码是一样的。在字面量的对象里this看起来不是很有用，但是当你动态创建一个对象（例如使用构造器）时它是非常有用的。

<br>

# 对象原型
通过原型这种机制，JavaScript 中的对象从其他对象集成功能特性。这种继承机制与经典的面对对象编程语言的继承机制不同。本文将探讨这些差别，解释原型链如何工作，并了解如何通过 prototype 属性向已有的构造器添加方法。

<br>

## 基于原型的语言
Javascript 常被描述为一种**基于原型的语言(prototype-based language)**，每个对象拥有一个**原型对象**，对象以原型为模板、从原型继承方法和属性。原型对象也可以拥有原型，并从中继承方法和属性，一层一层、以此类推。这种关系被称为**原型链(prototype chaim)**，他解释了为何一个对象会拥有定义在其他对象中的属性和方法。

在传统的 OOP 中，首先定义类，以及创建对象实例，类中定义的所有属性和方法都被复制到实例中。在 JavaScript 中并不是这样，而是在对象实例和它的构造器之间建立一个连接（它是对象的 `__proto__` 属性，是从构造函数的 prototype 属性派生的），之后通过上溯原型链，在构造器中找到这些属性和方法。

>  注：理解对象的原型（可以通过 `Object.getPrototypeOf(obj)` 或者已被弃用的 `__proto__` 属性获得）与构造函数的 prototype 属性之间的区别是很重要的。前者是每个实例上都有的属性，后者是构造函数的属性。也就是说，`Object.getPrototypeOf(new Foobar())` 和 `Foobar.prototype` 指向着同一个对象。

<br>

## 使用javascript中的原型
在 javascript 中，每个函数都有一个特殊的属性叫作原型（prototype），正如下面所展示的。打开一个控制台，复制粘贴下面的 JavaScript 代码，然后运行：
```js
function doSomething(){}
console.log( doSomething.prototype );
// It does not matter how you declare the function, a
//  function in javascript will always have a default
//  prototype property.
var doSomething = function(){};
console.log( doSomething.prototype );
```

正如上面所看到的, doSomething 构造函数和对象都有一个默认的原型属性：
```js
{
    constructor: ƒ doSomething(),
    __proto__: {
        constructor: ƒ Object(),
        hasOwnProperty: ƒ hasOwnProperty(),
        isPrototypeOf: ƒ isPrototypeOf(),
        propertyIsEnumerable: ƒ propertyIsEnumerable(),
        toLocaleString: ƒ toLocaleString(),
        toString: ƒ toString(),
        valueOf: ƒ valueOf()
    }
}
```

现在，我们可以添加一些属性到 doSomething 的原型上面：
```js
function doSomething(){}
doSomething.prototype.foo = "bar";
console.log( doSomething.prototype );
```

结果：
```js
{
    foo: "bar",   //ownproperty 属性
    constructor: ƒ doSomething(),
    __proto__: {
        constructor: ƒ Object(),
        hasOwnProperty: ƒ hasOwnProperty(),
        isPrototypeOf: ƒ isPrototypeOf(),
        propertyIsEnumerable: ƒ propertyIsEnumerable(),
        toLocaleString: ƒ toLocaleString(),
        toString: ƒ toString(),
        valueOf: ƒ valueOf()
    }
}
```

<br>

使用 new 运算符来在现在的这个原型基础之上，创建一个 doSomething 的实例，并在这个对象上面添加一些属性：
```js
function doSomething(){}
doSomething.prototype.foo = "bar"; // add a property onto the prototype
var doSomeInstancing = new doSomething();
doSomeInstancing.prop = "some value"; // add a property onto the object
console.log( doSomeInstancing );
```

结果：
```js
{
    prop: "some value",
    __proto__: {
        foo: "bar",
        constructor: ƒ doSomething(),
        __proto__: {
            constructor: ƒ Object(),
            hasOwnProperty: ƒ hasOwnProperty(),
            isPrototypeOf: ƒ isPrototypeOf(),
            propertyIsEnumerable: ƒ propertyIsEnumerable(),
            toLocaleString: ƒ toLocaleString(),
            toString: ƒ toString(),
            valueOf: ƒ valueOf()
        }
    }
}
```

![](2.png)

所以回过头来每个实例对象（ object ）都有一个私有属性（称之为proto）指向它的构造函数的原型对象（prototype），就像上面看到的，doSomeInstancing 的 `__proto__` 属性就是 doSomething.prototype。

当你访问 doSomeInstancing 的一个属性, 浏览器首先查找 doSomeInstancing 是否有这个属性。如果 doSomeInstancing 没有这个属性, 然后浏览器就会在 doSomeInstancing 的 `__proto__` 中查找这个属性(也就是 doSomething.prototype)。如果 doSomeInstancing 的 `__proto__` 有这个属性, 那么 doSomeInstancing 的 `__proto__` 上的这个属性就会被使用。否则, 如果 doSomeInstancing 的 `__proto__` 没有这个属性。浏览器就会去查找 doSomeInstancing 的 `__proto__` 的 `__proto__`，看它是否有这个属性。默认情况下, 所有函数的原型的 `__proto__` 属性就是 window.Object.prototype。所以 doSomeInstancing 的 `__proto__` 的 `__proto__`（也就是 doSomething.prototype 的 `__proto__`(也就是 Object.prototype)）会被查找是否有这个属性。如果没有在它里面找到这个属性，然后就会在 doSomeInstancing 的 `__proto__` 的 `__proto__` 的 `__proto__` 里面查找。然而这有一个问题: doSomeInstancing 的 `__proto__` 的 `__proto__` 的 `__proto__` 不存在。最后, 原型链上面的所有的 `__proto__` 都被找完了，浏览器所有已经声明了的 `__proto__` 上都不存在这个属性，然后就得出结论，这个属性是 undefined。
```js
function doSomething(){}
doSomething.prototype.foo = "bar";
var doSomeInstancing = new doSomething();
doSomeInstancing.prop = "some value";
console.log("doSomeInstancing.prop:      " + doSomeInstancing.prop);
console.log("doSomeInstancing.foo:       " + doSomeInstancing.foo);
console.log("doSomething.prop:           " + doSomething.prop);
console.log("doSomething.foo:            " + doSomething.foo);
console.log("doSomething.prototype.prop: " + doSomething.prototype.prop);
console.log("doSomething.prototype.foo:  " + doSomething.prototype.foo);
```

结果：
```js
doSomeInstancing.prop:      some value
doSomeInstancing.foo:       bar
doSomething.prop:           undefined
doSomething.foo:            undefined
doSomething.prototype.prop: undefined
doSomething.prototype.foo:  bar
```

> 注：没有官方的方法用于直接访问一个对象的原型对象——原型链中的“连接”被定义在一个内部属性中，在 JavaScript 语言标准中用 [[prototype]]。然而，大多数现代浏览器还是提供了一个名为 `__proto__` 的属性，其包含了对象的原型。你可以尝试输入 `object.__proto__` 和 `person1.__proto__.__proto__`，看看代码中的原型链是什么样的！

> 就我个人理解来说，构造函数的 prototype 属性一开始创建的时候就是其本身，这个原型对象的所有属性供给 new doSomething() 生成实例对象继承，给构造函数添加属性会添加到构造函数实例对象的属性之中（doSomething是函数，当然也是一个对象，但它是靠new Function()生成的实例对象），而且因为不在原型之中是后来添加的所以不会被继承。给实例对象添加属性默认是私有属性而不是添加到原型之中。
> 
> ![](1.png)
> 
> 所以如果执行doSomething.foo，它会在Function.prototype上找foo这个属性，结果没找到，自然是undefined。不过由于在上图第一个例子中添加了 foo 属性，会返回 'bar'。
>
> ![](4.png)
> 
> 一句话：构造函数的原型对象是给构造函数生成的实例对象用的，而不是给构造函数自己用的。
> 
> ![](2.png)

<br>

## prototype属性
那么，那些继承的属性和方法在哪儿定义呢？如果你查看 [Object 参考页](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object)，会发现左侧列出许多属性和方法——大大超过我们在 person1 对象中看到的继承成员的数量。某些属性或方法被继承了，而另一些没有——为什么呢？

原因在于，对象所继承的属性和方法是定义在 `prototype` 属性之上的（你可以称之为子命名空间）那些以 `Object.prototype.` 开头的属性，而非仅仅以 `Object.` 开头的属性。`prototype` 属性的值是一个对象，我们希望被原型链下游的对象继承的属性和方法，都被储存在其中。

于是 `Object.prototype.watch()`、`Object.prototype.valueOf()` 等等成员，适用于任何继承自 `Object()` 的对象类型，包括使用构造器创建的新的对象实例。

`Object.is()`、`Object.keys()`，以及其他不在 `prototype` 对象内的成员，不会被“对象实例”或“继承自 `Object()` 的对象类型”所继承。这些方法/属性仅能被 `Object()` 构造器自身使用。

> 注：这看起来很奇怪，构造器本身就是函数，你怎么可能在构造器这个函数中定义一个方法呢？但其实函数也是一个对象类型，你可以查阅 [Function() 构造器](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function)的参考文档以确认这一点。

在控制台输入尝试：
```js
Object.prototype
```

你会看到 Object 的 prototype 属性上定义了大量的方法；如前所示，继承自 Object 的对象都可以使用这些方法。

JavaScript 中到处都是通过原型链继承的例子。比如，你可以尝试从 String、Date、Number 和 Array 全局对象的原型中寻找方法和属性。它们都在原型上定义了一些方法，因此当你创建一个字符串时：
```js
var myString = 'This is my string.';
```

myString 立即具有了一些有用的方法，如 split()、indexOf()、replace() 等。

> 重要：prototype 属性大概是 JavaScript 中最容易混淆的名称之一。你可能会认为，this 关键字指向当前对象的原型对象，其实不是（原型对象是一个内部对象，应当使用 `__proto__` 访问）。prototype 属性指向一个对象，你在这个对象中定义需要被继承的成员。

<br>

## create()
我们讲过如何用 Object.create() 方法创建新的对象实例。

例如，在 JavaScript 控制台中输入：
```js
function person(){};
var person1 = new person();
var person2 = Object.create(person1);
```

`create()` 实际做的是从指定原型对象创建一个新的对象。这里以 person1 为原型对象创建了 person2 对象。在控制台输入：
```js
person2.__proto__
```

结果返回对象 person。

![](5.png)

<br>

## constructor属性
每个实例对象都从原型中继承了一个 constructor 属性，该属性**指向**了用于构造此实例对象的构造函数。

例如，在控制台中尝试下面的指令：
```js
person1.constructor
person2.constructor
```

都将返回 person() 构造器，因为该构造器包含这些实例的原始定义。

一个小技巧是，你可以在 constructor 属性的末尾添加一对圆括号（括号中包含所需的参数），从而用这个构造器创建另一个对象实例。毕竟构造器是一个函数，故可以通过圆括号调用；只需在前面添加 new 关键字，便能将此函数作为构造器使用。

在控制台中输入：
```js
var person3 = new person1.constructor('Karen', 'Stephenson', 26, 'female', ['playing drums', 'mountain climbing']);
```

通常不会去用这种方法创建新的实例；但如果因为某些原因**没有原始构造器的引用**，这种方法就很有用了。

此外，constructor 属性还有其他用途。比如，想要获得某个对象实例的构造器的名字，可以这么用：
```js
instanceName.constructor.name
```

<br>

## 修改原型
从我们从下面这个例子来看一下如何修改构造器的 prototype 属性。

回到 [oojs-exercises.html](#exercises) 的例子，在本地为源代码创建一个副本。在已有的 JavaScript 的末尾添加如下代码，这段代码将为 [person 构造器](#person)的 prototype 属性添加一个新的方法：
```js
person.prototype.farewell = function() {
  alert(this.name.first + ' has left the building. Bye for now!');
}
```

保存代码，在浏览器中加载页面，然后在控制台输入：
```js
person1.farewell();
```

你会看到一条警告信息，其中还显示了构造器中定义的人名。更关键的是：**整条继承链动态地更新了，任何由此构造器创建的对象实例都自动获得了这个方法。**

再想一想这个过程。我们的代码中定义了构造器，然后用这个构造器创建了一个对象实例，此后向构造器的 prototype 添加了一个新的方法：
```js
function person(first, last, age, gender, interests) {

  // 属性与方法定义

};

var person1 = new Person('Tammi', 'Smith', 32, 'neutral', ['music', 'skiing', 'kickboxing']);

person.prototype.farewell = function() {
  alert(this.name.first + ' has left the building. Bye for now!');
}
```

![](7.png)

这样，旧有对象实例的可用功能被自动更新了。这种继承模型下，上游对象的方法不会复制到下游的对象实例中；下游对象本身虽然没有定义这些方法。但浏览器会通过上溯原型链、从上游对象中找到它们，提供了一个强大而可扩展的功能系统。

不过，你很少看到属性定义在 prototype 属性中，因为如此定义不够灵活。比如，你可以添加一个属性：
```js
person.prototype.fullName = 'Bob Smith';
```

但人不可能都叫这个名字。用 name.first 和 name.last 组成 fullName ：
```js
person.prototype.fullName = this.name.first + ' ' + this.name.last;
```

![](6.png)

然而，这么做是无效的，因为本例中 [this](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this) 引用全局范围（无论是否在严格模式下，在全局执行环境中{在任何函数体外部}this 都指向全局对象），而非函数范围（在函数内部，this 的值取决于函数被调用的方式）。访问这个属性只会得到 undefined undefined。this 指向了原型对象，导致在构造函数中定义的属性无法和添加在原型中的属性灵活交互。但这个语句若放在 先前定义在 prototype 上的方法中则有效，因为此时语句位于函数范围内，从而能够成功地转换为对象实例范围。你可能会在 prototype 上定义常属性（不变的属性），但一般来说，在构造器内定义属性更好。

**事实上，一种极其常见的对象定义模式是，在构造器（函数体）中定义属性、在 prototype 属性上定义方法（属性值可变无法继承，方法不变并继承）。**如此，构造器只包含属性定义，而方法则分装在不同的代码块，代码更具可读性。而且，**由于属性定义在构造函数中，属性是无法继承的，即属性不在原型里。**例如：
```js
// 构造器及其属性定义

function Test(a,b,c,d) {
  // 属性定义
};

// 定义第一个方法

Test.prototype.x = function () { ... }

// 定义第二个方法

Test.prototype.y = function () { ... }

// 等等……
```
在 Piotr Zalewa 的 [school plan app](https://github.com/zalun/school-plan-app/blob/master/stage9/js/index.js) 样例中可以看到这种模式。

<br>

# javascript中的继承
了解了 OOJS 的大多数细节后，接下来将介绍如何创建子对象类别（构造器）并从父类别中继承功能。

<br>

## 原型式的继承
到目前为止我们已经了解了一些关于原型链的实现方式以及成员变量是如何通过它来实现继承，但是之前涉及到的大部分都是浏览器内置函数（比如 String、Date、Number 和 Array），那么我们自己如何创建一个继承自另一对象的JavaScript对象呢？

正如前面课程所提到的，有些人认为 JavaScript 并不是真正的面向对象语言，在经典的面向对象语言中，你可能倾向于定义类对象，然后可以简单地定义哪些类继承哪些类，JavaScript 使用了另一套实现方式，继承的对象函数并不是通过复制而来，而是通过原型链继承（通常被称为 原型式继承 —— prototypal inheritance）。

<br>

将 [oojs-start.html](https://github.com/a-pin/learning-area/blob/main/javascript/oojs/advanced/oojs-start.html) 文件复制到您本地，你能看到一个只定义了一些属性的 Person() 构造器：
```js
function Person(first, last, age, gender, interests) {
  this.name = {
    first,
    last
  };
  this.age = age;
  this.gender = gender;
  this.interests = interests;
};
```

所有的方法都定义在构造器的原型上，比如：
```js
Person.prototype.greeting = function() {
  alert('Hi! I\'m ' + this.name.first + '.');
};
```

<br>

## 定义Teacher()构造器函数
假如，我们想要创建一个 Teacher 类，这个类不仅会继承 Person 的所有成员，也包括：
- 一个新的属性：subject 这个属性包含了教师教授的学科。
- 一个被更新的 greeting() 方法，这个方法打招呼听起来比一般的 greeting() 方法更正式一点。

我们要做的第一件事是创建一个 Teacher() 构造器——将下面的代码加入到现有代码之下：
```js
function Teacher(first, last, age, gender, interests, subject) {
  Person.call(this, first, last, age, gender, interests);

  this.subject = subject;
}
```
 
这里有一个我们从没见过的函数——[`call()`函数](https://www.w3school.com.cn/js/js_function_call.asp)。

call() 方法调用一个函数, 其具有一个指定的 this 值和参数列表，改变 this 指针的指向。可以让 call() 中的对象调用当前对象所拥有的函数。

第一个参数指定了 this值——将 Teacher 函数作为 Person 构造函数的 this 值。你可以在接下来的参数列表指定参数作为 Person 构造函数的参数，为 Teacher() 创建了要继承的属性。

> 注：在这个例子里我们在创建一个新的对象实例时同时指派了继承的所有属性，但是你需要在构造器里将它们作为参数来指派，即使实例不要求它们被作为参数指派（比如在创建对象的时候已经得到了一个设置为任意值的属性）

所以在这个例子里，我们很有效的在 Teacher() 构造函数里运行了 Person() 构造函数，得到了和在 Teacher() 里定义的一样的属性，但是用的是传送给 Teacher()，而不是 Person() 的值（我们简单使用这里的this作为传给call()的this，意味着this指向Teacher()函数）。

在构造器里的最后一行代码简单地定义了一个新的 subject 属性，这是教师特有的属性。

当然，我们可以这么做：
```js
function Teacher(first, last, age, gender, interests, subject) {
  this.name = {
    first,
    last
  };
  this.age = age;
  this.gender = gender;
  this.interests = interests;
  this.subject = subject;
}
```

但是这只是重新定义了一遍属性，并不是将他们从 Person 中继承过来的。

### 从无参构造函数继承
请注意，如果您继承的构造函数不从传入的参数中获取其属性值，则不需要在call()中为其指定其他参数。例如：
```js
function Brick() {
  this.width = 10;
  this.height = 20;
}
```

您可以这样继承width和height属性（以及下面描述的其他步骤）：
```js
function BlueGlassBrick() {
  Brick.call(this);

  this.opacity = 0.5;
  this.color = 'blue';
}
```

![](8.png)

请注意，我们仅传入了 this 到 call() 中，因为我们不会继承那些需要参数设置的父级属性。

<br>

## 设置Teacher()的原型和构造器引用
可以看到，在使用 call() 函数继承父级对象的属性后，子对象并没有继承父对象的原型，原型默认是 Object。这就说明你没办法使用父对象（例如 Person 对象）定义在原型上的方法。

为了从 Person() 的原型对象里继承方法，你需要设置子对象的原型：

先在之前的代码后面添加这一行：
```js
Teacher.prototype = Object.create(Person.prototype);
```

在这里我们用 `create()` 函数来创建一个和 Person.prototype 一样的新的**原型属性值**（这个属性指向一个包括属性和方法的对象），然后将其作为 Teacher.prototype 的属性值。这意味着 Teacher.prototype 现在会继承 Person.prototyp e 的所有属性和方法。

现在 Teacher() 的 prototype 的 constructor 属性指向的是 Person() , 这是由我们生成 Teacher() 的方式决定的。(这篇 [Stack Overflow post 文章](https://stackoverflow.com/questions/8453887/why-is-it-necessary-to-set-the-prototype-constructor)会告诉您详细的原理)。

进入JavaScript控制台，输入以下代码来确认：
```js
Teacher.prototype.constructor;
```

这或许会成为很大的问题，所以我们需要将其正确设置——您可以回到源代码，在底下加上这一行代码来解决：
```js
Teacher.prototype.constructor = Teacher;
```

当您保存并刷新页面以后，输入 Teacher.prototype.constructor 就会得到 Teacher()。

> 注：每一个函数对象（Function）都有一个 prototype 属性，并且只有函数对象有 prototype 属性，因为 prototype 本身就是定义在 Function 对象下的属性。当我们输入类似 `var person1=new Person(...)` 来构造对象时，JavaScript实际上参考的是 `Person.prototype` 指向的对象来生成 person1。另一方面，Person() 函数是 Person.prototype 的构造函数，也就是说 Person===Person.prototype.constructor。

在定义新的构造函数 Teacher 时，我们通过 function.call 来调用父类的构造函数，但是这样无法自动指定 Teacher.prototype 的值，这样 Teacher.prototype 就只能包含在构造函数里构造的属性，而没有方法。因此我们利用 Object.create() 方法将 Person.prototype 作为 Teacher.prototype 的原型对象，并改变其构造器指向，使之与 Teacher 关联。

任何您想要被继承的方法都应该定义在构造函数的 prototype 对象里，并且永远使用父类的 prototype 来创造子类的 prototype，这样才不会打乱类继承结构。

<br>

## 对象成员总结
总结一下，您应该基本了解了以下三种属性或者方法：
1. 那些定义在构造器函数中的、用于给予对象实例的。这些都很容易发现——在你自己的代码中，它们是构造函数中使用 `this.x = x` 类型的行；在内置的浏览器代码中，它们是可用于对象实例的成员（通常通过使用 new 关键字调用构造函数来创建，例如 `var myInstance = new myConstructor()`）。
2. 那些直接在构造函数上定义、仅在构造函数上可用的。这些通常仅在内置的浏览器对象中可用，并通过被直接链接到构造函数而不是实例来识别。 例如Object.keys()。
3. 那些在构造函数原型上定义、由所有实例和对象类继承的。这些包括在构造函数的原型属性上定义的任何成员，如 `myConstructor.prototype.x()`。

<br>

## ECMAScript 2015 类
ECMAScript 2015(ES6) 将类语法引入 JavaScript，使用更简单、更干净。ES6 编写可重用类（JavaScript 类是 JavaScript 对象的模板），类似于 C++ 或 Java 中的类。

在本节中，我们将把"人员"和"教师"示例从原型继承转换为类，以向您展示它是如何完成的。

> 注：所有现代浏览器都支持这种现代的类编写方式，但是如果你处理的项目需要支持不支持此语法的浏览器（最明显的是 Internet Explorer），则仍然值得了解底层原型继承。

让我们看一下 Person 示例的重写版本，类样式：
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

  greeting() {
    console.log(`Hi! I'm ${this.name.first}`);
  };

  farewell() {
    console.log(`${this.name.first} has left the building. Bye for now!`);
  };
}
```

class 语句指示我们正在创建一个新类。在这个块中，我们定义了类的所有功能：
- `constructor()` 方法定义了表示 Person 类的构造函数。
- `greeting()` 和 `farewell()` 是类方法。任何你想要与类关联的方法都在构造函数之后定义。在此示例中，我们使用模板文本而不是字符串串联，以使代码更易于阅读。

现在，我们可以使用 new 运算符实例化对象：
```js
let han = new Person('Han', 'Solo', 25, 'male', ['Smuggling']);
han.greeting();
// Hi! I'm Han

let leia = new Person('Leia', 'Organa', 19, 'female', ['Government']);
leia.farewell();
// Leia has left the building. Bye for now
```

> 注：事实上在表层下，你的类正在转换为原型继承模型。

<br>

### 使用类语法进行继承
在本节中，我们将创建专用类，使其继承自使用现代类语法。为了创建一个子类，我们使用 `extends` 关键字来告诉 `JavaScript` 我们想要基于我们的类的类：
```js
class Teacher extends Person {
  constructor(subject, grade) {
    this.subject = subject;
    this.grade = grade;
  }
}
```

但是这里有一点问题：与老式构造函数不同，在旧式构造函数中，new 运算符会初始化 `this` 到新分配的对象，而对于由 `extends` 关键字定义的类，它不会自动初始化。

因此，运行上述代码将给出错误：
```js
Uncaught ReferenceError: Must call super constructor in derived class before
accessing 'this' or returning from derived constructor
```

对于子类，对 `this` 的初始化始终依赖于父类构造函数，即被扩展类的构造函数。对于 Teacher 类，你需要使用 `super()` 方法初始化对象以及 this 的值：
```js
class Teacher extends Person {
  constructor(subject, grade) {
    super(); // Now 'this' is initialized by calling the parent constructor.
    this.subject = subject;
    this.grade = grade;
  }
}
```

由于 `super()` 方法实际上是父类构造函数，因此需要传递必要的参数给 Person 构造函数用来初始化子类中的父类属性，从而继承它们：
```js
class Teacher extends Person {
  constructor(first, last, age, gender, interests, subject, grade) {
    super(first, last, age, gender, interests);

    // subject and grade are specific to Teacher
    this.subject = subject;
    this.grade = grade;
  }
}
```

现在，当我们实例化 Teacher 对象时，我们可以调用在两者上定义的方法和属性。
```js
let snape = new Teacher('Severus', 'Snape', 58, 'male', ['Potions'], 'Dark arts', 5);
snape.greeting(); // Hi! I'm Severus.
snape.farewell(); // Severus has left the building. Bye for now.
snape.age // 58
snape.subject; // Dark arts
```

<br>

## getter和setter
有时，我们可能想要更改我们创建的类中属性的值，或者我们不知道属性的最终值是什么。以 `Teacher` 举例，在我们创建它们之前，我们可能不知道老师会教什么科目，或者科目会随学期的变化而变化。

我们可以用 `getter` 和 `setter` 一起处理这种情况，它们往往成对工作：
- `getter` 返回变量的当前值
- `setter` 将变量的值更改为它定义的值。

修改后的 Teacher 类如下所示：
```js
class Teacher extends Person {
  constructor(first, last, age, gender, interests, subject, grade) {
    super(first, last, age, gender, interests);
    // subject and grade are specific to Teacher
    this._subject = subject;
    this.grade = grade;
  }

  get subject() {
    return this._subject;
  }

  set subject(newSubject) {
    this._subject = newSubject;
  }
}
```

在我们上面的类中，我们为 `subject` 属性设置了 getter 和 setter 。我们使用 `_`(下划线) 创建一个单独的值，用于存储相应地属性（如果不遵循此约定，则每次调用 get 或 set 时都会收到错误）：
- 为了显示 `snape` 对象 `_subject` 属性的当前值，我们可以使用 getter 方法。
  ```js
  Teacher.subject
  ```
- 为了给 `_subject` 属性分配新值，我们可以使用 setter 方法。
  ```js
  Teacher.subject="new value"
  ```

![](9.png)

> setter 和 getter 实际上是为了检查和更新属性值而自定义的方法，不仅仅可以在 ES6 中使用。使用原型链形式编写的对象也可以定义它们。

<br>

## 何时在javascript中使用继承
JavaScript 的强大和灵活性来自于它的对象体系和继承方式。在某种程度上来说，你一直都在使用继承，无论是使用 WebAPI 的不同特性还是调用字符串、数组等浏览器内置对象的方法和属性的时候，你都在隐式地使用继承。

就在自己代码中使用继承而言，你可能不会使用的非常频繁，特别是在小型项目中或者刚开始学习时。但是随着您的代码量的增大，您会越来越发现它的必要性。如果您开始创建一系列拥有相似特性的对象时，那么创建一个包含所有共有功能的通用对象，然后在更特殊的对象类型中继承这些特性，将会变得更加方便有用。

> 注: 考虑到 JavaScript 的工作方式，由于原型链等特性的存在，在不同对象之间功能的共享通常被叫做 **委托**（特殊的对象将功能委托给通用的对象类型完成）。这也许比将其称之为继承更为贴切，因为“被继承”了的功能并没有被拷贝到正在“进行继承”的对象中，相反它仍存在于通用的对象中。

在使用继承时，建议不要使用过多层次的继承，并仔细追踪定义方法和属性的位置。过多的继承会在调试代码时给您带来无尽的混乱和痛苦，以至于你的代码会不应该的临时修改浏览器内置对象的原型。

总之，对象是另一种形式的代码重用，就像函数和循环一样，有他们特定的角色和优点。如果你发现自己创建了一堆相关的变量和函数，还想一起追踪它们并将其灵活打包的话，对象是个不错的主意。对象在你打算把一个数据集合从一个地方传递到另一个地方的时候非常有用。这些都可以在不使用构造器和继承的情况下完成。如果你只需要一个单一的对象实例，使用对象常量就很不错。

<br>

# 使用json
JavaScript 对象表示法（JSON）是用于将**结构化数据**表示为 **JavaScript 对象**的标准格式，通常用于在网站上表示和传输数据（例如从服务器向客户端发送一些数据，因此可以将其显示在网页上）。

你会经常遇到它，所以在本文中，我将介绍如何使用 JavaScript 处理 JSON 的所有工作，包括访问 JSON 对象中的数据项并编写自己的JSON。

<br>

## 什么是json
JSON 是一种按照 JavaScript 对象语法的数据格式。虽然它是基于 JavaScript 语法，但它独立于 JavaScript，这也是为什么许多程序环境能够读取和生成 JSON。 

JSON 可以作为一个对象或者字符串存在，前者用于解读 JSON 中的数据，后者用于通过网络传输 JSON 数据。JavaScript 提供一个全局的可访问的 JSON 对象来对这两种数据进行转换。

一个 JSON 对象可以被储存在它自己的文件中，这基本上就是一个文本文件，扩展名为 .json，还有 MIME type 用于 application/json。

### json对象
JSON 对象基于 JavaScript 对象，你可以把 JavaScript 对象原原本本的写入 JSON 数据——字符串、数字、数组、布尔还有其它的字面值对象。这允许您构造出一个对象树，如下：
```js
{
  "squadName" : "Super hero squad",
  "homeTown" : "Metro City",
  "formed" : 2016,
  "secretBase" : "Super tower",
  "active" : true,
  "members" : [
    {
      "name" : "Molecule Man",
      "age" : 29,
      "secretIdentity" : "Dan Jukes",
      "powers" : [
        "Radiation resistance",
        "Turning tiny",
        "Radiation blast"
      ]
    },
    {
      "name" : "Madame Uppercut",
      "age" : 39,
      "secretIdentity" : "Jane Wilson",
      "powers" : [
        "Million tonne punch",
        "Damage resistance",
        "Superhuman reflexes"
      ]
    },
    {
      "name" : "Eternal Flame",
      "age" : 1000000,
      "secretIdentity" : "Unknown",
      "powers" : [
        "Immortality",
        "Heat Immunity",
        "Inferno",
        "Teleportation",
        "Interdimensional travel"
      ]
    }
  ]
}
```

如果我们要加载对象进入 JavaScript 程序，以保存为一个名为 superHeroes 对象为例，我们使用 `.` 或 `[]` 访问对象内的数据：
```js
superHeroes.hometown
superHeroes["active"]
```

为了访问对象中的对象，您只需简单地链式访问（通过属性名和数组索引）。例如，访问 superHeroes 对象中的 members 数组对象的第二个元素的 powers 数组对象的第三个元素，您可以这样做：
```js
superHeroes["members"][1]["powers"][2]
```

> 注：在 [JSONText.html](https://a-pin.github.io/demo/json/JSONText.html) 实例中，JSON 对象进入变量并且可访问。尝试加载它并且在您的浏览器上访问对象数据。

<br>

### json数组
我们已经可以推测出 JSON 对象就是基于 JavaScript 对象，而且这几乎是正确的——我们说几乎正确的原因是**数组对象**也是一种合法的 JSON 对象，例如：
```js
[
  {
    "name" : "Molecule Man",
    "age" : 29,
    "secretIdentity" : "Dan Jukes",
    "powers" : [
      "Radiation resistance",
      "Turning tiny",
      "Radiation blast"
    ]
  },
  {
    "name" : "Madame Uppercut",
    "age" : 39,
    "secretIdentity" : "Jane Wilson",
    "powers" : [
      "Million tonne punch",
      "Damage resistance",
      "Superhuman reflexes"
    ]
  }
]
```

上面是完全合法的 JSON，你只需要通过数组索引就可以访问数组元素，如 `[0]["powers"][0]`。

### 其他注意事项
- JSON 是一种纯数据格式，它只包含属性，没有方法。
- JSON 要求在**字符串**和**属性名称**周围使用双引号，单引号无效。
- 一个错位的逗号或分号就可以导致 JSON 文件出错。你可以通过像 [JSONLint](https://jsonlint.com/) 的应用程序来检验 JSON。
- JSON 可以将任何标准合法的 JSON 数据格式化保存，不只是数组和对象。比如，一个单一的字符串或者数字可以是合法的 JSON 对象。虽然不是特别有用处。
与 JavaScript 代码中对象属性可以不加引号不同，JSON 中只有带引号的字符串可以用作属性。

<br>

## 一个json示例

<br>

### 开始
首先，拷贝 [heroes.html](https://github.com/a-pin/learning-area/blob/main/javascript/oojs/json/heroes.html) 和 [style.css](https://github.com/a-pin/learning-area/blob/main/javascript/oojs/json/style.css) 文件。前者包含了简单的 HTML，后者包含了简单的 CSS。
```html
<header>
</header>

<section>
</section>
```

添加 `<script>` 元素来包含我们的 JavaScript 代码。当前它只有两行，获得了 `<header>` 和 `<section>` 的引用，保存在变量中。
```js
var header = document.querySelector('header');
var section = document.querySelector('section');
```

我们要使用的 JSON 数据在[这里](https://github.com/a-pin/learning-area/blob/main/javascript/oojs/json/superheroes.json)。

我们准备把它加载到我们的页面中，然后使用漂亮的 DOM 操作来展示它，就像这样：

![json-superheroes](10.png)

<br>

### 加载json
为了载入 JSON 到页面中，我们将使用一个名为 `XMLHTTPRequest` 的 API（常称为XHR）。这是一个非常有用的 JavaScript 对象，使我们能够通过代码来向服务器请求资源文件（如：图片，文本，JSON，甚至HTML片段），意味着我们可以更新小段内容而不用重新加载整个页面。

1. 首先，我们将保存一个即将访问的 URL 作为变量。在您的 JavaScript 代码的底部添加下面的代码：
  ```js
  var requestURL = 'https://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json';
  ```
2. 为了创建一个 HTTP 请求，我们需要创建一个 HTTP 请求对象，通过 new 构造函数的形式。在最下面的代码中写入：
  ```js
  var request = new XMLHttpRequest();
  ```
3. 现在我们需要使用 `open()` 函数打开一个新的请求，添加如下代码：
  ```js
  request.open('GET', requestURL);
  ```
  这个函数至少含有两个参数，其它的是可选参数。对于示例我们只需要两个强制参数
  - HTTP 方法，网络连接时使用。这个示例中 GET 就可以了，因为我们只要获得简单的数据。
  - URL，用于指向请求的地址。我们使用之前保存的变量。
4. 接下来，添加，两行代码，我们设定 `responseType` 为 JSON，所以服务器将知道我们想要返回一个 JSON 对象，然后发送请求：
  ```js
  request.responseType = 'json';
  request.send();
  ```
5. 最后一点内容涉及相应来自服务器的返回数据，然后处理它，添加如下代码在您先前的代码下方：
  ```js
  request.onload = function() {
    var superHeroes = request.response;
    populateHeader(superHeroes);
    showHeroes(superHeroes);
  }
  ```
这儿我们保存了相应我们请求的数据(访问 `response` 属性) 于变量 `superHeroes`；这个变量现在含有 JSON！我们现在把 `superHeroes` 传给两个函数，第一个函数将会用正确的数据填充 `<header>`，同时第二个函数将创建一个信息卡片，然后把它插入 `<section>` 中。

我们把代码包在事件处理函数中，当请求对象 load 事件触发时执行代码，这是因为请求对象 load 事件只有在请求成功时触发；这种方式可以保证事件触发时 `request.response` 是绝对可以访问的。

### 定位header
现在我们已经获得我们的 JSON 数据，让我们利用它来写两个我们使用的函数。首先，添加下面的代码于之前的代码下方：
```js
function populateHeader(jsonObj) {
  var myH1 = document.createElement('h1');
  myH1.textContent = jsonObj['squadName'];
  header.appendChild(myH1);

  var myPara = document.createElement('p');
  myPara.textContent = 'Hometown: ' + jsonObj['homeTown'] + ' // Formed: ' + jsonObj['formed'];
  header.appendChild(myPara);
}
```

我们称参数为 `jsonObj`，那也是为什么我们要在其中调用 JSON 对象。这儿我们首先使用 `createElement()` 创建了一个 `<h1>` 节点，将它的 `textContent` 设为 JSON 对象的 `squadName` 属性，然后通过 `appendChild()` 把它加入 `<header>` 中。然后我们对段落做了相同的一件事情：创建，设置内容，追加到 `<header>`。唯一的不同在于它的内容设为一个与 JSON 内属性 `homeTown` 和 `formed` 相关联的字符串。

### 创建英雄信息卡片
接下来，添加如下的函数到脚本代码底部，这个函数创建和展示了superhero cards：
```js
function showHeroes(jsonObj) {
  var heroes = jsonObj['members'];

  for(i = 0; i < heroes.length; i++) {
    var myArticle = document.createElement('article');
    var myH2 = document.createElement('h2');
    var myPara1 = document.createElement('p');
    var myPara2 = document.createElement('p');
    var myPara3 = document.createElement('p');
    var myList = document.createElement('ul');

    myH2.textContent = heroes[i].name;
    myPara1.textContent = 'Secret identity: ' + heroes[i].secretIdentity;
    myPara2.textContent = 'Age: ' + heroes[i].age;
    myPara3.textContent = 'Superpowers:';

    var superPowers = heroes[i].powers;
    for(j = 0; j < superPowers.length; j++) {
      var listItem = document.createElement('li');
      listItem.textContent = superPowers[j];
      myList.appendChild(listItem);
    }

    myArticle.appendChild(myH2);
    myArticle.appendChild(myPara1);
    myArticle.appendChild(myPara2);
    myArticle.appendChild(myPara3);
    myArticle.appendChild(myList);

    section.appendChild(myArticle);
  }
}
```

首先，我们保存了 JSON 的 `members` 属性作为一个变量。这个数组含有多个带有英雄信息的对象。

接下来，我们使用一个循环来，遍历每个元素。对于每一个元素，我们：
1. 创建几个元素： 一个 `<article>`，一个 `<h2>`，三个 `<p>` 和一个 `<ul>`。
2. 设置 `<h2>` 为当前英雄的 `name`。
3. 使用他们的 `secretIdentity`,`age`,`"Superpowers:"` 介绍信息列表填充三个段落。
4. 保存 `powers` 属性于另一个变量 `superPowers`，包含英雄的 `superpowers` 列表。
5. 使用另一个循环来遍历当前的英雄的 `superpowers`，对于每一个元素我们创建 `<li>` 元素，把 `superpower` 放进去，然后使用 `appendChild()` 把 `listItem` 放入 `<ul>` 元素中。
6. 最后一件事情是追加 `<h2>`，`<p>`还有 `<ul>` 进入 `<article>` (`myArticle`)。然后将 `<article>` 追加到 `<section>`。追加的顺序很重要，因为他们将被展示在 HTML 中。

> 注：如有疑难,试试引用我们的 [heroes-finished.html](https://github.com/a-pin/learning-area/blob/main/javascript/oojs/json/heroes-finished.html) 代码。

<br>

## 对象和文本间的转换
上述示例就访问 JSON 而言是简单的，因为我们设置了 XHR 来访问 JSON 格式数据：
```js
request.responseType = 'json';
```

但是有时候我们没有那么幸运，我们接收到一些字符串作为 JSON 数据，然后我们想要将它转换为对象。当我们想要发送 JSON 数据作为信息，我们将需要转换它为字符串，我们经常需要正确的转换数据，这两个问题在 web 环境中很普遍以至于浏览器拥有一个内建的 JSON，包含以下两个方法：
- `parse()`：以文本字符串形式接受JSON对象作为参数，并返回相应的对象。
- `stringify()`：接收一个对象作为参数，返回一个对应的JSON字符串。

你可以看看我们 [heroes-finished-json-parse.html](https://github.com/a-pin/learning-area/blob/main/javascript/oojs/json/heroes-finished-json-parse.html) 示例的第一个操作，除了返回的是 text，这做了一件与我们之前一模一样的事情，然后使用 `parse()` 来将他转换成为 JavaScript 对象。关键片段如下：
```js
request.open('GET', requestURL);
request.responseType = 'text'; // now we're getting a string!
request.send();

request.onload = function() {
  var superHeroesText = request.response; // get the string from the response
  var superHeroes = JSON.parse(superHeroesText); // convert it to an object
  populateHeader(superHeroes);
  showHeroes(superHeroes);
}
```

正如您所想，`stringify()` 做相反的事情. 尝试将下面的代码输入您的浏览器 JS 控制台：
```js
var myJSON = { "name" : "Chris", "age" : "38" };
myJSON
var myString = JSON.stringify(myJSON);
myString
```

这儿我们创建了一个 JavaScript 对象，然后检查了它包含了什么，然后用 `stringify()` 将它转换成 JSON 字符串，最后保存返回值作为变量，然后再一次检查。