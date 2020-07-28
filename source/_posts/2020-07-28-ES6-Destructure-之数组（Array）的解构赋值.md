---
title: ES6 Destructure 之数组（Array）的解构赋值
tags:
  - JavaScript
  - ES6
  - Destructure
categories:
  - 前端
author: Shane
img: >-
  https://myimagebed-1302088591.cos.ap-nanjing.myqcloud.com/%E6%96%87%E7%AB%A0%E7%89%B9%E5%BE%81%E5%9B%BE/41.jpg
toc: true
summary: ES5 从一个复杂的数据结构中提取数据是如何做的？ES6 有更优雅便捷的方式吗？
abbrlink: 3ec741fe
date: 2020-07-28 20:34:16
---

# ES6 Destructure 之数组（Array）的解构赋值

## 0 前言

从一个复杂的数据结构中提取数据，在 ES5 中需要层层遍历或者是引用；而 ES6 中可以使用解构赋值的方式更便捷地提取数据。

下面我们先就 Array 的解构赋值进行说明

## 1 简单变量的解构赋值

```javascript
// ES5 时从数组中取数据
let arr = ['hello', 'world']
let firstName = arr[0]
let surName = arr[1]
console.log(firstName, surName) // hello world
```

```javascript
// ES6 时从数组中取数据
let arr = ['hello', 'world']
let [firstName, surName] = arr // （简单变量的）解构赋值
console.log(firstName, surName) // hello world
```

## 2 跳过不关心的数据去解构赋值

```javascript
let arr = ['a', 'b', 'c', 'd']
let [firstName, , thirdName] = arr // 只把数组的第一、三项取出来赋值
console.log(firstName, thirdName) // a c
// 如上，如果想跳过某项不关心的数据，可以通过不写变量同时保留逗号（,）实现。
```

## 3 解构赋值的条件

只要是可遍历的对象就能进行解构赋值

```javascript
// 什么时候可以解构赋值呢？
// 只要是可遍历的对象（Array、Object、String、Set、Map......）就能进行解构赋值
// 左侧要使用中括号（[]）
let arr = 'abcd'
let [firstName, , thirdName] = arr
console.log(firstName, thirdName) // a c
let [firstName2, , thirdName2] = new Set([1, 2, 3, 4])
console.log(firstName2, thirdName2) // 1 3

// 总结：初步理解结构赋值：解构赋值的右边是一个可遍历的对象，
// 左边是一个中括号，中括号里是声明的新的变量，这些变量会默认按照索引的顺序去取值
```

## 4 把数据赋值到对象的属性上

如果左边不新生成变量，而是把需要的数据赋值到一个对象的属性上去，是否可以呢？

当然可以，如下：

```javascript
let user = { name: 's', surName: 't' };
[user.name, user.surName] = [1, 2] // （对象属性的）解构赋值
console.log(user) // {name: 1, surName: 2}
// 可见，解构赋值不仅可以赋值给简单的变量，还可以赋值给对象的属性，
// 需要注意的是，赋值给对象的属性时，不需要用 let/var/const 进行声明。
```

## 5 循环体中的解构赋值

```javascript
// ES5 时
let arr = ['hello', 'world']
for (let i = 0, item; i < arr.length; i++) { // 声明一个临时变量 item，用来保存数据
  item = arr[i]
}
```

```javascript
// ES6 时
let user = { name: 's', surName: 't' }
// for of 后面要求是可遍历的对象（Array/Set/Map......）
// Object.entries() 方法可以把对象转换成可遍历的 key-value 形式
for (let [k, v] of Object.entries(user)) { // 循环体内的解构赋值体现在这里的 let [k, v] 上
  // 隐式赋值（背后还是索引在工作，但是我们不需要书写，区别于之前形如 arr[1] 的显式索引）
  console.log(k, v)
}
/* 运行结果：
name s
surName t
*/
```

## 6 解构赋值对于 Rest 变量的处理

```javascript
let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]
let [firstName, curName, ...last] = arr // 使用 Rest 变量进行解构赋值
console.log(firstName, curName) // 1 2
console.log(last) // (7) [3, 4, 5, 6, 7, 8, 9]
```

```javascript
let arr = []
let [firstName, curName, ...last] = arr
console.log(firstName, curName, last) // undefined undefined []
// 可见，当数据量不够，变量没有对应数据时，通过解构赋值得到的变量值就跟没有赋值的情况一样，是 undefined。
```

## 7 解构赋值设置默认值

```javascript
let arr = []
let [firstName = 'hello', curName, ...last] = arr // 设置变量 firstName 的默认值为 "hello"
console.log(firstName, curName, last) // hello undefined []
```