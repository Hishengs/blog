title: Javascript之call与apply
date: 2017-02-10 14:58:45
tags:
- javascript
---

### 1.前言
> [Function.prototype.call](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/call) 与 [Function.prototype.apply](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) 用于改变函数运行的上下文环境，通俗地说，其实就是改变函数内 this 的指向。下面以一个例子说明。

<!-- more -->
### 2.创建上下文
> 首先创建用于以下两个函数的上下文(可理解为对象)。

```
var ctx = {
	sayHello: function(name){
		console.log('hello,'+name)
	}
}
```

### 3.[Function.prototype.call](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/call)
> 语法 `fun.call(thisArg[, arg1[, arg2[, ...]]])`
> thisArg 用于指定函数运行时 this 指向对象。
> 参数以参数列表 `arg1, arg2, ...` 的形式列在 thisArg 之后。

```
// 定义函数
function say(name){
	console.log(this.sayHello(name));
	console.log('called by ',this);
}
// 使用 fun.call 形式运行函数
say.call(ctx,'hisheng');
// 运行结果
// hello,hisheng
// called by Object {...}
```

### 4.[Function.prototype.apply](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)
> 语法 `fun.apply(thisArg[, argsArray])`
> thisArg 用于指定函数运行时 this 指向对象。
> 参数(argsArray)以参数数组 `[arg1, arg2, ...]` 的形式列在 thisArg 之后。

```
// 定义函数
function say(name){
	console.log(this.sayHello(name));
	console.log('called by ',this);
}
// 使用 fun.apply 形式运行函数
say.apply(ctx,['hisheng']);
// 运行结果
// hello,hisheng
// called by Object {...}
```
