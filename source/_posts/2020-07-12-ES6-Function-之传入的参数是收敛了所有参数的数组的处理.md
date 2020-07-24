---
title: ES6 Function 之传入的参数是收敛了所有参数的数组的处理
tags:
  - JavaScript
  - ES6
  - Function
categories:
  - 前端
author: Shane
img: >-
  https://myimagebed-1302088591.cos.ap-nanjing.myqcloud.com/%E6%96%87%E7%AB%A0%E7%89%B9%E5%BE%81%E5%9B%BE/30.jpg
toc: true
summary: ES5 和 ES6 中处理参数确定但传入的参数是收敛了所有参数的数组的区别
abbrlink: 2f26d31c
date: 2020-07-12 23:17:41
---

## 如何处理参数确定但传入的参数是收敛了所有参数的数组的问题

上一小节中，我们讲述了使用 Rest 参数处理不确定参数的内容，即函数在定义时，参数是不确定的，这时就可以用 Rest 参数将这些不确定的参数收敛进 Rest 参数这个数组中来。那么，还有一种与之相反的情况，就是函数在设计参数的时候，参数是确定的，但是函数在接收参数时，接收到的是一个收敛了所有参数的数组参数。

下面我们用求和来举例说明。

### 1. ES5

```javascript
function sum (x = 1, y = 2, z = 3) {
  return x + y + z
}
let data = [4, 5, 6] // 假设为后端给的数据，需要是一个数组
// 方法 1：通过索引把数据一个一个取出来
console.log(sum(data[0], data[1], data[2])) // 15
// 方法 2：使用 apply 方法
console.log(sum.apply(this, data)) // 15
```

### 2. ES6

```javascript
function sum (x = 1, y = 2, z = 3) {
  return x + y + z
}
let data = [4, 5, 6] // 假设为后端给的数据，需要是一个数组
// 方法 3（ES 6 中的做法）：使用 Spread Operator “...”
console.log(sum(...data)) // 15
```

