---
title: ES6 Function 之不确定参数的处理
tags:
  - JavaScript
  - ES6
  - Function
categories:
  - 前端
author: Shane
img: >-
  https://myimagebed-1302088591.cos.ap-nanjing.myqcloud.com/%E6%96%87%E7%AB%A0%E7%89%B9%E5%BE%81%E5%9B%BE/29.jpg
toc: true
summary: ES5 和 ES6 中处理不确定参数问题的区别
abbrlink: 3e5c670f
date: 2020-07-12 23:12:55
---

## 如何处理不确定参数的问题

上一小节中，我们已经提到了 ES5 中如何处理不确定参数的问题，非常简单，就是使用 `arguments`，`arguments` 可以获取到当前函数接收到的所有参数。但是 ES6 中不让在函数内部使用 `arguments`，那该怎么做呢？

下面我们用求和来举例说明。

### 1. ES5

```javascript
function sum () {
  let num = 0
  // 方法 1：使用原型链和 call 方法遍历伪数组 arguments
  Array.prototype.forEach.call(arguments, function (item) {
    num += item * 1
  })
  return num
}

console.log(sum(1, 2, 3)) // 6

/* 运行结果：
6
*/
```

```javascript
function sum () {
  let num = 0
  // 方法 2：使用 ES6 中的 Array.from 方法先将伪数组 arguments 转化为数组，再使用 forEach 方法遍历数组
  Array.from(arguments).forEach(function (item) {
    num += item * 1
  })
  return num
}

console.log(sum(1, 2, 3)) // 6

/* 运行结果：
6
*/
```

> 总结：
> 知识点 1：ES5 中，用 arguments 获取到所有参数；
> 知识点 2：arguments 是伪数组，可以用 Array 原型链的 forEach，然后使用 call 方法，对 arguments 进行遍历；也可以用 ES6 的 Array.from 方法对 arguments 进行遍历。

### 2. ES6

ES6 中使用 Rest parameter（Rest 参数，形如`...参数名`）替代使用 arguments 的方法，Rest 参数接收函数的多余参数，组成一个***数组***，放在形参的最后，形式如下：

```javascript
function sum (...nums) {
  let num = 0
  nums.forEach(function (item) { // nums 是个数组，直接使用 forEach
    num += item * 1
  })
  return num
}
console.log(sum(1, 2, 3, 5))

/* 运行结果：
11
*/
```

假如我们需要对传入函数的第一个参数单独处理，可以这样写：

```javascript
function sum (base, ...nums) {
  let num = 0
  nums.forEach(function (item) {
    num += item * 1
  })
  return base * 2 + num // 第一个参数 base 乘以 2 后再与其它参数相加
}
console.log(sum(1, 2, 3)) // 7
```