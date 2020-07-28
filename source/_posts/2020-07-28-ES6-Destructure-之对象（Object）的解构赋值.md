---
title: ES6 Destructure 之对象（Object）的解构赋值
tags:
  - JavaScript
  - ES6
  - Destructure
categories:
  - 前端
author: Shane
img: >-
  https://myimagebed-1302088591.cos.ap-nanjing.myqcloud.com/%E6%96%87%E7%AB%A0%E7%89%B9%E5%BE%81%E5%9B%BE/42.jpg
toc: true
summary: ES5 从一个复杂的数据结构中提取数据是如何做的？ES6 有更优雅便捷的方式吗？
date: 2020-07-28 20:35:04
---

# ES6 Destructure 之对象（Object）的解构赋值

## 0 前言

从一个复杂的数据结构中提取数据，在 ES5 中需要层层遍历或者是引用；而 ES6 中可以使用解构赋值的方式更便捷地提取数据。

下面我们先就 Object 的解构赋值进行说明

## 1 简单的 Object 的解构赋值

### 1.1 两种形式

```javascript
let options = {
  title: 'menu',
  width: 100,
  height: 200
}
// 形式一：简写形式（因为对象是 key-value 的形式，而我们这里只写了变量），
// 变量名必须和 Object 的属性名一样，不然解构赋值时就不知道该和对象的哪个属性匹配了
let { title, width, height } = options
console.log(title, width, height) // menu 100 200
```

```javascript
let options = {
  title: 'menu',
  width: 100,
  height: 200
}
// 形式二：变量名可以和属性名不一样（如下面的“title: title2”，其中，title 是对象属性名，title2 是变量名）
let { title: title2, width, height } = options
console.log(title2, width, height) // menu 100 200
```

注意等于号左边和数组的解构赋值的区别，数组是中括号（[]），对象是大括号（{}）。

### 1.2 设置默认值

```javascript
let options = {
  title: 'menu',
  height: 200
}
let { title: title2, width = 130, height } = options // 设置 width 的默认值为 130
console.log(title2, width, height) // menu 130 200
```

## 2 复杂的 Object 的解构赋值

### 2.1 Rest 变量可用

复杂的数据结构比如说 Object 中有很多东西，现在只想取某几项，其它的又不想被垃圾回收器回收掉，还想继续存储着，这时该怎么办呢？数组是用的 Rest 变量来存储那些剩余的数据的，那么 Object 是否也有类似操作呢？

```javascript
let options = {
  title: 'menu',
  width: 100,
  height: 200
}
let { title, ...last } = options // Object 的解构赋值也可以使用 Rest 变量（这里即变量 last）
console.log(title, last) // menu {width: 100, height: 200}
```

是的，Object 也可以用 Rest 变量来存储那些剩余的不想被垃圾回收器回收掉的数据。

### 2.2 嵌套数据的处理

```javascript
// 处理对象中嵌套的数据
let options = {
  size: {
    width: 100,
    height: 200
  },
  items: ['Cake', 'Donut'],
  extra: true
}
// 解构赋值时，等号左侧声明变量时的数据结构，要和等号右侧的数据保持一样的数据结构
let { size: { width: width2, height }, items: [, item2] } = options
console.log(width2, height, item2) // 100 200 "Donut"
```

> 总结：解构赋值时，等号左右两侧的数据结构要一致。

思考：

1. 一个函数需要传入很多参数，是否可以利用解构赋值来简化操作呢？

2. 如何在业务开发中对接口数据进行解构赋值呢？