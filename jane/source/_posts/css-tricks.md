title: css-tricks
date: 2017-03-01 15:47:47
tags:
- css-tricks
- css
---

## 前言
> 介绍一些常见的CSS技巧。

<!-- more -->

### 如何使文字居中？
> `text-align:center;` 或者 align="center"

### 如何设置块元素在父元素中水平居中？
> 1. 设置宽度，固定宽度、最小宽度或者最大宽度：`width: 500px;` or  `max-width: 500px;` or  `min-width: 500px;`
2. 左右外边距设置为 auto： `margin: 0 auto;`

### 如何清除上方元素的浮动？
> `clear: left;` 或者 `clear: right;` 或者 `clear: both;` 清除左浮动、右浮动和左右浮动。

### 如何解决由于浮动带来的高度坍塌？
> 给坍塌的容器添加 `overflow: auto;zoom: 1;`

### 关于 position 定位
> 1. 元素默认的 position 定位是  `position: static;`，不会产生任何效果，默认文档流行为。
2. 元素如果设置了 `position: relative;`，若没有设置 `left, right, top, bottom` 属性，则和一般的元素没有区别；如果设置了 `left, right, top, bottom`，则会相对于原来本身文档流的位置进行相对定位，但不会对其他元素产生影响。同时，设置了 `position: relative;` 的元素将作为其子元素定位的参照。
3. 元素如果设置了 `position: fixed;`，同时设置了 `left, right, top, bottom` 属性，将会相对于 **视窗** 进行定位，而不是文档，即使文档进行滚动，元素也不会随之滚动，而是停留在 **视窗** 固定的位置，好像是“粘”在屏幕上。
4. 元素如果设置了 `position: absolute;`，同时设置了 `left, right, top, bottom` 属性，则该元素将会相对于其最近一个设置了 `position: relative;` 的祖先元素的位置进行定位；如果没有这样的祖先元素，则会相对于 body 元素进行定位。

### 如何使用 flex 布局？
> 想要用简洁的几句话概括 flex 布局的用法不太容易，建议参考阮老师的文章：[《Flex 布局教程：语法篇》](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html?utm_source=tuicool)。