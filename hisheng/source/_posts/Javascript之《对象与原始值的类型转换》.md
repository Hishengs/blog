---
title: Javascript之《对象与原始值的类型转换》
date: 2018-03-20 10:24:29
tags:
- javascript
---

在 Javascript 中，数据类型可分为原始值和对象。原始值包括 null, undefined, string, bool, number，其他一般归为对象，譬如 Object, Array, Date...

<!-- more -->
由于 Javascript 是一门动态语言，在运行时难免出现类型转换的情况，那么，对象遇到原始值时如何进行转换呢？

其实在 ECMAScript 规范中，对象内部实现了一个 ToPrimitive 的内部函数，用于将对象转为原始值。

所以，对象与原始值的操作可理解为：

1. 对象调用本身的 ToPrimitive 方法将自己转换为原始值。

2. 转换后的原始值与另一个原始值进行操作。

例如：
```js
var obj = {};
console.log(obj + 'hello'); // 输出 [object Object]hello
```
在上例中，对象调用 ToPrimitive 转为原始值，即字符串 `'[object Object]'`，然后与 `'hello'` 进行普通的字符串连接操作。

那么，对象转换为原始值的规则是如何的呢？

一般，转换规则如下：

1. 如果对象存在 `valueOf` 方法，则调用此方法。如果结果是原始值，则直接输出，否则进行下一步。

2. 如果对象存在 `toString` 方法，则调用此方法。如果结果是原始值，则直接输出，否则进行下一步。

3. 如果既没有 `valueOf` 方法，也没有 `toString` 方法，则直接抛出 `TypeError` 错误。

在这里，如果遇到和字符串的转换，则会优先调用 `toString` 方法直接将对象转为字符串进行操作。

下面举几个例子：

```js
console.log({} + 1); // '[object Object]1'
console.log({} + 'hello'); // '[object Object]hello'
console.log({} + true); // [object Object]true

console.log([] + 1); // 1
console.log((function(){}) + 1); 'function (){}1'
```