---
title: ES6 Function 之箭头函数
tags:
  - JavaScript
  - ES6
  - Function
categories:
  - 前端
author: Shane
img: >-
  https://myimagebed-1302088591.cos.ap-nanjing.myqcloud.com/%E6%96%87%E7%AB%A0%E7%89%B9%E5%BE%81%E5%9B%BE/31.jpg
toc: true
summary: ES6 中的箭头函数
abbrlink: 5bf28737
date: 2020-07-12 23:21:53
---

# ES6 中的箭头函数

## 0 前言

ES6 中的箭头函数长这样：`()=>{}`

## 1 ES6 之前声明函数的做法

```javascript
// 方式 1：函数声明
function hello1 () {}
// 方式 2：函数表达式，又叫函数字面量
let hello2 = function () {}
// 方式 3：函数构造法，参数必须加引号
let hello3 = new Function()
```

## 2 ES6 中使用箭头函数声明函数

### 2.1 箭头函数的声明

```javascript
// 声明一个函数，函数名为 hello
let hello = () => { // 注意：小括号不能省略哦
  console.log('hello world')
}
// 调用这个函数
hello() // hello world
```

上面声明的这个函数是无参的，如果想要传参数又该怎么办呢？可以这样做：

```javascript
// 声明一个函数，函数名为 hello，可以接收一个 name 参数
let hello = (name) => {
  console.log('hello world', name)
}
hello('jjLin') // hello world jjLin
```

上面是传了一个参数，如果想传第二个呢？可以这样写：

```javascript
let hello = (name, city) => {
  console.log('hello world', name, city)
}
hello('jjLin', 'shanghai') // hello world jjLin shanghai
```

以此类推，想传 3 个、4 个.....多个参数时，只要用逗号隔开，依次往后写即可。

***注意***：没有参数时，箭头（=>）前面的那对小括号不能省略哦！

### 2.2 箭头函数声明时的省略与简写

当且仅当只有一个参数时，箭头（=>）前面的那对小括号才能省略。

```javascript
let hello = name => {
  console.log('hello world', name)
}
hello('jjLin') // hello world jjLin
```

既然小括号可以省略，那么后面的花括号能不能省略呢？

是的，当箭头函数的函数体**只有**一个 `return` 语句时，可以省略 `return` 关键字和方法体的花括号。

```javascript
let sum = (x, y, z) => x + y + z // x + y + z 是一个表达式，这个表达式的值就是函数的返回值
console.log(sum(1, 2, 3)) // 6
```

当返回对象字面量时，记住用 `params => {object:literal}` 这种简单的语法是行不通的。

```javascript
var func = () => { foo: 1 };               
// Calling func() returns undefined!

var func = () => { foo: function() {} };   
// SyntaxError: function statement requires a name

let sum = (x, y, z) => {
  x: x,
  y: y,
  z: z
} // Uncaught SyntaxError: Unexpected token ':'
```

这是因为花括号（`{}`）里面的代码被解析为一系列语句（即 `foo` 被认为是一个标签，而非对象字面量的组成部分）。

所以，记得用圆括号把对象字面量包起来：

```javascript
var func = () => ({foo: 1});

let sum = (x, y, z) => ({
  x: x,
  y: y,
  z: z
})
console.log(sum(1, 2, 3)) // {x: 1, y: 2, z: 3}
```

我们可以把上述代码中箭头后面的这对圆括号的作用理解成运算表达式的作用，而里面的这对花括号，可不是函数体的花括号，而是字面量对象的花括号哦！

当然，如果不想记这些情况下的简写形式，也可以老老实实地加上函数体的花括号、加上 `return` 关键字。

```javascript
let sum = (x, y, z) => {
  return {
    x: x,
    y: y,
    z: z
  }
}
console.log(sum(1, 2, 3)) // {x: 1, y: 2, z: 3}
```

## 3 箭头函数没有单独的 this

在箭头函数出现之前，每一个新函数根据它是被如何调用的来定义这个函数的 this 值：

- 如果是该函数是一个构造函数，this 指针指向一个新的对象
- 在严格模式下的函数调用下，this 指向 `undefined`
- 如果是该函数是一个对象的方法，则它的 this 指针指向这个对象
- 等等

`this` 被证明是令人厌烦的面向对象风格的编程。

```javascript
function Person () {
  // Person() 构造函数定义 `this` 作为它自己的实例.
  this.age = 0

  setInterval(function growUp () {
    // 在非严格模式, growUp() 函数定义 `this` 作为全局对象,
    // 与在 Person() 构造函数中定义的 `this` 并不相同.
    this.age++
  }, 1000)
}

var p = new Person()
```

在 ESMAScript 3/5 中，通过将 `this` 值分配给封闭的变量，可以解决 `this` 问题。

```javascript
function Person () {
  var that = this
  that.age = 0

  setInterval(function growUp () {
    // 回调引用的是`that`变量, 其值是预期的对象.
    that.age++
  }, 1000)
}
```

或者，可以创建[绑定函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)，以便将预先分配的 `this` 值传递到绑定的目标函数（上述示例中的 `growUp() 函数` ）。

箭头函数不会创建自己的 `this，它只会从自己的作用域链的上一层继承 this`。因此，在下面的代码中，传递给 `setInterval` 的函数内的 `this` 与封闭函数中的 `this` 值相同：

```javascript
function Person () {
  this.age = 0

  setInterval(() => {
    this.age++ // this 正确地指向 p 实例
  }, 1000)
}

var p = new Person()
```

下面，我们举个前端面试中常出现的一个小题目：

```javascript
let test = {
  name: 'test',
  say: function () {
    console.log(this.name)
  }
}
test.say() // test
```

问 `test.say()` 的结果是什么？

没错，是“test”。那么，为什么是“test”呢？

在之前学习作用域时，我们总结过，判断 `this` 的指向时，可以看下是`谁在调用这个 function，那么 this 就指向谁`。

在这里，`say()` 是被 `test` 调用的，那么 `say()` 里面的 `this` 就是指向的 `test`，所以 `this.name` 就是 `test.name`，也就是“test”啦。

好，重点来了，我们把上面的这个 function 改成箭头函数，再看结果是什么。

```javascript
let test = {
  name: 'test',
  say: () => {
    console.log(this.name, this)
  }
}
test.say() // undefined {}
```

***普通函数和箭头函数对 this 的指向的定义不同，ES5 中，谁在调用这个 function，那么 this 就指向谁；而 ES6 中，定义的时候 this 的指向是什么，那执行的时候 this 的指向就是什么。***

可以看到，上面箭头函数中的 this 是空对象，这是为什么呢？

如果我们将上面的代码块放到 chrome 浏览器的 Console 中执行，可以看到 this 其实是 Window 对象。

![image-20200712175149712](https://myimagebed-1302088591.cos.ap-nanjing.myqcloud.com/2020-07-12-ES6-Function-%E4%B9%8B%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0/image-20200712175149712.png)

那前面的 this 为什么是空对象呢？

这是因为前面的代码是经 webpack 构建过的，构建过程中对代码进行了 eval（js 的 eval 函数，可以把字符串当代码来执行），eval 把我们代码最外层的作用域指向了一个空对象，所以 this 也就指向了一个空对象。