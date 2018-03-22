---
title: Javascript之《严格相等与宽松相等比较》
date: 2018-03-21 10:26:03
tags:
- javascript
---

在 Javascript 中，使用 `===` 对两个值进行比较称为 **严格相等**，使用 `==` 对两个值进行比较称为 **宽松相等**。

<!-- more -->

## 严格相等
严格相等的规则如下：
1. 如果两个 **类型相同** 的 **原始值** 进行比较，则结果为相等。除了（NaN === NaN 不成立）之外；
```js
console.log(1 === 1); // true
console.log(NaN === NaN); // false
console.log('xx' === 'xx'); // true
console.log(undefined === undefined); // true
console.log(null === null); // true
console.log(false === false); // true
```
2. 如果两个 **类型相同** 的 **对象** 进行比较，则直接比较是否是同一个对象引用（变量），否则不相等；
```js
const obj1 = {}, obj2 = {};
obj3 = obj1;
console.log(obj1 === obj2); // false
console.log(obj1 === obj3); // true
```
3. **类型不相同** 的值之间的比较结果为不相等。
```js
console.log(1 === '1'); // false
console.log(undefined === null); // false
console.log(undefined === false); // false
```


### 宽松相等

#### undefined == null
二者宽松相等


#### 字符串 == 数字
字符串会尝试被转化为数字后进行比较（使用 `Number()` 进行转化）：
```js
console.log('' == 0); // true
console.log('0' == 0); // true
console.log('123' == 123); // true
console.log('123a' == 123); // false
```

#### 布尔值 == 非布尔值
布尔值与非布尔值进行比较时，首先会将布尔值转化为数字之后再与非布尔值进行比较：
```js
console.log(true == 1); // true
console.log(true == '1'); // true
console.log(false == ''); // true
console.log(false == '0'); // true
```

#### 对象 == 数字/字符串
对象与数字或者字符串进行比较时，会先调用 `valueOf` 或者 `toString` 得到对象的原始值，之后再进行比较：
```js
console.log({} == 1); // false
console.log({} == '[object Object]'); // true
```


#### 注意
在条件判断语句中，以下值被认为是假值：
1. null
2. undefined
3. 0, NaN
4. ''（空字符串）
5. false
但是，被认为是假值并不等于它们之间是宽松相等的：
```js
console.log(null == 0); // false
console.log(undefined == 0); // false
console.log(null == false); // false
console.log(undefined == false); // false
console.log(null == ''); // false
console.log(undefined == ''); // false
```
