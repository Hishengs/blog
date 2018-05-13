---
title: Javascript之《如何自动运行生成器》
date: 2018-05-12 14:33:32
tags:
- Javascript
- 生成器
---

在 es6 中，引入了一个新的特性：生成器（ generator ），用于控制函数运行流程，可实现对函数运行的中断与恢复。

<!-- more -->

## 生成器基本概念

一个简单的生成器对象定义如下：
```js
function* Gen(){
  const name = 'Hisheng';
  yield `hello, ${name}`;
  console.log('bye');
}
```

那么如何运行它呢？直接 `Gen()` 是不行的，我们必须为它实例化一个迭代器。
你只需要记住：生成器的实例化结果是一个迭代器，或者迭代器是由生成器实例化而来。

```js
const g = Gen();
g.next().value; // hello, Hisheng
g.next(); // bye
```

通过依次调用 `g.next()` 来依次运行函数中断点。


## 深入

那问题来了，要运行生成器，每次都要实例化并且手动调用 `g.next()` 多麻烦啊，能不能实现自动运行生成器呢？答案是肯定的。

我们先定义一个可以无限次迭代的生成器，例如典型的斐波那契函数：

```js
function* fibonacci(){
  let x = 0, y = 1, z = 0;
  yield 1;
  while(true && z < 200){
    z = x+y;
    yield z;
    x = y;
    y = z;
  }
}
```

因为仅仅是用于演示，我们在生成器内部限制了其调用次数，不让它可无限调用，尽管理论上定义一个无限运行的生成器是没有问题的。

同时，我写了一个可用于自动运行生成器的方法，主要是结合了强大的 `Promise`，具体实现见函数注释：

```js
function runGenerator(gen){
  // 先判断是否是生成器对象
  if(typeof gen !== 'function'){
    throw new TypeError('Generator must be a function');
  }
  const g = gen();
  if(!g.next){
    throw new TypeError('function is not a Generator');
  }
  const next = g.next();

  return new Promise((resolve, reject) => {
    handler(next).then(resolve).catch(reject);
  });

  function handler(next){
    return new Promise((resolve, reject) => {
      try {
        if(next.done){
          resolve();
        }else {
          const nnext = g.next();
          // 这一句只是为了打印出值来验证生成器是否有被运行，实际中可去掉
          console.log(nnext.value);
          // 递归调用 handler
          handler(nnext).then(resolve).catch(reject);
        }
      }catch (err){ // catch 生成器中可能抛出的异常
        reject(err);
      }
    });
  }
}
```

运行下看看

```js
runGenerator(fibonacci); // 结果打印出了 1, 1, 2, 3, 5, 8...233
```

ok，至此已经达到我们想要的效果了。

### 题外
关于生成器的使用，最出名的莫过于 大神 TJ 专门写的库：[co](https://github.com/tj/co)，实现更加巧妙。