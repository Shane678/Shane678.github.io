---
title: ES6 Template 之 Tag 函数
tags:
  - JavaScript
  - ES6
  - String
  - Template
  - Tag
categories:
  - 前端
author: Shane
img: >-
  https://myimagebed-1302088591.cos.ap-nanjing.myqcloud.com/%E6%96%87%E7%AB%A0%E7%89%B9%E5%BE%81%E5%9B%BE/40.jpg
toc: true
summary: ES5 中字符串包含变量或表达式、包含逻辑运算怎么办？ES6 有更优雅便捷的方式吗？
abbrlink: 8f924eb8
date: 2020-07-25 22:49:39
---

# ES6 Template 之 Tag 函数

## 字符串包含变量或表达式

```javascript
const a = 20
const b = 10
const c = 'javascript'
// ES5 的做法：利用字符串拼接的方式
const str1 = 'my age is ' + (a + b) + ', i love ' + c
// ES6 的做法：使用反引号（`）和 ${}
const str2 = `my age is ${a + b}, i love ${c}`
console.log(str1) // my age is 30, i love javascript
console.log(str2) // my age is 30, i love javascript
```

## 字符串包含逻辑运算

```javascript
/* ES5 的做法 */

const retailPrice = 20 // 零售价
const wholeSalePrice = 16 // 批发价
const type = 'retail'
let showTxt = ''
if (type === 'retail') {
  showTxt = '您此次的购买单价是：' + retailPrice
} else {
  showTxt = '您此次的购买批发价是：' + wholeSalePrice
}
console.log(showTxt) // 您此次的购买单价是：20
```

```javascript
/* ES6 的做法：使用 tag（标签） 函数解决字符串模板问题 */

/**
 *
 * @param {Array} strings 字符串模板数组
 * @param {*} type 变量
 */
// 定义一个 tag 函数
function Price (strings, type) {
  let s1 = strings[0]
  let s2 = strings[1]
  const retailPrice = 20 // 零售价
  const wholeSalePrice = 16 // 批发价
  let showTxt
  if (type === 'retail') {
    showTxt = '购买单价是：' + retailPrice
  } else {
    showTxt = '购买批发价是：' + wholeSalePrice
  }
  return `${s1}${showTxt}${s2}`
}
// 调用该 tag 函数
let showTxt = Price`您此次的${'retail'}，全市最低价啊`
console.log(showTxt) // 您此次的购买单价是：20，全市最低价啊
```