title: Javascript之《类数组转数组》
date: 2017-09-24 22:08:04
tags:
- javascript
- js-trick
---

介绍将类数组转为数组的几种常见方法。

<!-- more -->

### 什么是类数组？
简单地来讲，具有 `length` 属性并且可遍历（iteratee）的对象称为类数组，即类似数组的对象。例如：函数的参数对象 `arguments`、DOM 元素列表等。

### 如何将类数组转为数组？

#### 方法一
使用 Array.prototype.slice.call（略难记......）。
```js
// 哈哈，名字略长
function transformAlikeArrayToArray(arr){
  return Array.prototype.slice.call(arr);
  // 注：这里也可以使用 Reflect.slice.call(arr);
}
// 用一个匿名函数来验证结果
(function(){
  console.log(transformAlikeArrayToArray(arguments));
})(1, 2, 3);
// 打印出：[1, 2, 3]
```

#### 方法二
使用 Array.from。
```js
function transformAlikeArrayToArray(arr){
  return Array.from(arr);
}
// 用一个匿名函数来验证结果
(function(){
  console.log(transformAlikeArrayToArray(arguments));
})(1, 2, 3);
// 打印出：[1, 2, 3]
```

#### 方法一
使用扩展运算符。
```js
function transformAlikeArrayToArray(arr){
  return [...arr];
}
// 用一个匿名函数来验证结果
(function(){
  console.log(transformAlikeArrayToArray(arguments));
})(1, 2, 3);
// 打印出：[1, 2, 3]
```