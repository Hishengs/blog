title: Javascript之《var、let、const》
date: 2017-09-26 17:19:30
tags:
- Javascript
---

ES6 引进了 let，const 新的变量声明方式，那么它们和 var 以及各自的区别是什么呢？

<!-- more -->

## var
var 我想不需要过多介绍，只提一些需要注意的点：
1. var 声明的变量会进行 **变量提升**。
2. var 声明的变量默认属于全局对象的属性。（在浏览器环境是 `window`，Node 环境是 `global`）

## let
1. 不会进行变量提升。
2. 不会挂载在全局对象上。
3. 具有块作用域。

## const
> 用于定义常量或者不会被重新赋值的变量。

1. 尽量使用 const 来定义变量。