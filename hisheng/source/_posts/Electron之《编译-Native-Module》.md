---
title: Electron之《编译 Native Module》
date: 2018-02-12 18:13:35
tags:
- electron
---

由于在项目中使用了 [`ffi`](https://github.com/node-ffi/node-ffi) 这个原生的模块，折腾了好久才发现在 Electron 环境下使用 native module 和 Node 环境下是有区别的，区别在于你的原生模块必须在 Electron 下重新编译一遍才能使用。

<!-- more -->

下面以 [`ffi`](https://github.com/node-ffi/node-ffi) 模块为例，讲一下如何在 Electron 环境下使用 native module。

### 安装 `ffi` 模块
`npm i --save node-ffi`

### 安装 `electron-rebuild`
`npm i --save-dev electron-rebuild`

### 在项目目录下执行
`.\node_modules\.bin\electron-rebuild.cmd`（window 环境）等待编译完成

### 新建 `index.js`
```js
const ffi = require('ffi');
```

### 测试
`node index.js`，如果没有报错，说明模块可以正常使用。

> 参考：[使用 Node 原生模块](https://electronjs.org/docs/tutorial/using-native-node-modules)