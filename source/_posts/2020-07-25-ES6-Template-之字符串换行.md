---
title: ES6 Template 之字符串换行
tags:
  - JavaScript
  - ES6
  - String
  - Template
categories:
  - 前端
author: Shane
img: >-
  https://myimagebed-1302088591.cos.ap-nanjing.myqcloud.com/%E6%96%87%E7%AB%A0%E7%89%B9%E5%BE%81%E5%9B%BE/39.jpg
toc: true
summary: ES5 中字符串换行怎么办？ES6 有更优雅便捷的方式吗？
abbrlink: 229f64b9
date: 2020-07-25 22:49:21
---

# ES6 Template 之字符串换行

## ES5 的做法：使用加号（+）

```javascript
let s1 = '我是第一行' +
'我是第二行'
console.log(s1)

/* 运行结果：
我是第一行我是第二行
*/
```

## ES6 的做法：使用一对反引号（``）包裹

```javascript
let s1 = `我是第一行
我是第二行`
console.log(s1)

/* 运行结果：
我是第一行
我是第二行
*/
```