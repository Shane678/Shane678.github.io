---
title: ES6 Function 之参数默认值的处理
tags:
  - JavaScript
  - ES6
  - Function
categories:
  - 前端
author: Shane
img: >-
  https://myimagebed-1302088591.cos.ap-nanjing.myqcloud.com/%E6%96%87%E7%AB%A0%E7%89%B9%E5%BE%81%E5%9B%BE/28.jpg
toc: true
summary: ES5 和 ES6 中参数默认值处理的区别
abbrlink: cfa4ba82
date: 2020-07-12 23:08:32
---

## 函数参数默认值的处理

[TOC]

### 1. ES5

```javascript
function f (x, y, z) {
  if (y === undefined) {
    y = 7
  }
  if (z === undefined) {
    z = 42
  }
  return x + y + z
}

console.log(f(1))
console.log(f(1, 8))
console.log(f(1, 8, 43))

/* 运行结果：
50
51
52
*/
```

### 2. ES6

```javascript
// 注意：没有默认值的参数写在前面，有默认值的参数写在后面
function f (x, y = 7, z = 42) {
  return x + y + z
}

console.log(f(1))
console.log(f(1, 8))
console.log(f(1, 8, 43))
// 使用“undefined”实现中间参数的默认值赋值
console.log(f(1, undefined, 43))

/* 运行结果：
50
51
52
51
*/
```

参数的默认值可以指定为常量，也可以是“前面”参数的运算表达式：

```javascript
function f (x, y = 7, z = x + y) {
  return x * 10 + z
}

console.log(f(1, undefined, 2)) // 1 * 10 + 2 = 12
console.log(f(1)) // 1 * 10 + (1 + 7) = 18
console.log(f(1, 9)) // 1 * 10 + (1 + 9) = 20
console.log(f(1, undefined)) // 1 * 10 + (1 + 7) = 18

/* 运行结果：
12
18
20
18
*/
```

参数的默认值如果指定为其它参数的表达式，那么表达式中的参数必须是前面已定义的参数，所以像下面这样指定 y 参数的默认值是错误的：

```javascript
function f (x, y = x + z, z = 7) { // 'z' was used before it was defined.
  return x * 10 + y
}
console.log(f(1)) // Uncaught ReferenceError: Cannot access 'z' before initialization
```

查看当前函数的参数信息：

```javascript
function f (x, y = 7, z = x + y) {
  console.log(arguments) // 通过 arguments 查看当前函数的参数的信息
  console.log(arguments.length) // 当前函数传入的参数个数
  console.log(Array.from(arguments)) // 当前函数传入的参数信息，Array.from 用来转换伪数组为数组
  return x * 10 + z
}

console.log(f(1, undefined, 2)) // 传了 3 个参数
console.log(f(1, 2)) // 传了 2 个参数

/* 运行结果：
Arguments(3) [1, undefined, 2, callee: (...), Symbol(Symbol.iterator): ƒ]
3
(3) [1, undefined, 2]
12
Arguments(2) [1, 2, callee: (...), Symbol(Symbol.iterator): ƒ]
2
(2) [1, 2]
13
*/
```

上述代码的运行结果截图：

![image-20200705164938961](https://myimagebed-1302088591.cos.ap-nanjing.myqcloud.com/2020-07-12-ES6-Function-%E4%B9%8B%E5%8F%82%E6%95%B0%E9%BB%98%E8%AE%A4%E5%80%BC%E7%9A%84%E5%A4%84%E7%90%86/image-20200705164938961.png)

上面我们使用了 arguments 来获取当前函数传入的参数信息，但到了 ES6 中，其实是禁止使用 arguments 的，那怎么办呢？有办法，我们后面再讲，这里先讲一下如何获取“***函数定义时未指定默认值的参数个数***”，我们可以使用“函数名.length”的方式实现

```javascript
function f (x, y = 7, z = x + y) { // 注意：没有默认值的参数写在前面，有默认值的参数写在后面
  console.log(f.length) // 1
  return x * 10 + z
}

console.log(f(1, undefined, 2))

/* 运行结果：
1
12
*/
```

下面我们把上面函数参数列表中的 y 的默认值去掉，再看 `f.length` 的值：

```javascript
function f (x, y, z = x + y) { // 注意：没有默认值的参数写在前面，有默认值的参数写在后面
  console.log(f.length) // 2
  return x * 10 + z
}

console.log(f(1, undefined, 2))

/* 运行结果：
2
12
*/
```

> 总结：`arguments.length` 和 `function.length` 的区别：
> `arguments.length` 获取到的是“函数执行时接收到的参数个数”；
> `function.length` 获取到的不是“函数执行时接收到的参数个数”，而是“函数定义时未指定默认值的参数个数（出现首个有默认值的参数前的参数个数）”。