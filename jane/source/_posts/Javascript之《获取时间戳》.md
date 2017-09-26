title: Javascript之《获取时间戳》
date: 2017-09-26 00:35:00
tags:
- Javascript
- js-trick
---

JS 获取时间戳哪些方法？我们来总结一下。

<!-- more -->

### 方法一
```js
(new Date()).getTime(); // 1506357244477
```

### 方法二
ES6 提供的方法：`Date.now()`。
```js
Date.now(); // 1506357244477
```

### 方法三
利用 `Date -> Number` 之间的类型转换。
```js
+new Date(); // 1506357244477
// 或者
Number(new Date());
```
