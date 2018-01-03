title: Flex布局
date: 2016-06-02 11:30:46
tags:
- css
- css3
---
### 前言

开始学一些CSS3的东西，从flex布局入门，flex是flexible box的缩写，即“弹性布局”，或者译为“伸缩盒”，设置为flex的元素本身就成了一个可伸缩的容器。
一个flex容器有主轴和交叉轴两条基准线，一般默认水平方向为主轴，垂直方向为交叉轴，也可以设置垂直方向为主轴，容器内的项目沿两条轴排列或对齐。
<!-- more -->
flex布局主要从容器和容器内的元素入手。

### 容器属性

flex容器本身的属性有以下几种：

* flex-direction
* flex-wrap
* flex-flow
* justify-content
* align-items
* align-content

#### flex-direction

> 项目(items)在容器中主轴的排列方向，有四个可选的值：row, row-reverse, column, column-reverse

* row(默认): 沿主轴(水平)方向从左到右排列
* row-reverse: 和row相反，从右到左进行排列
* column: 沿主轴(垂直)方向从上到下排列
* column-reverse: 沿主轴(垂直)方向从下到上排列


#### flex-wrap

>当项目在主轴线上排列不下时，如何进行换行，该属性有三个可选的值：wrap, no-wrap, wrap-reverse

* no-wrap(默认): 不换行
* wrap: 换行
* wrap-reverse: 反向换行，换行后的项目(items)将从反方向开始排列
* flex-flow

flex-flow是flex-direction和flex-wrap的结合，可以同时设置容器项目的排列方向和换行属性，先后顺序为：```<flex-direction> || <flex-wrap>;```


#### justify-content

>该属性规定了容器项目的对齐方式，有五种可选的值：flex-start, flex-end, center, space-between, space-around

* flex-start(默认): 从主轴的开始方向对齐
* flex-end: 从主轴的结束方向对齐
* center: 在主轴上居中对齐
* space-between: 两端对齐，项目之间均等间隔
* space-around: 项目周围均等间隔，间隔大小依据空间分配


#### align-items

>该属性规定了容器项目在交叉轴上的对齐方式，有五种可选的值：flex-start, flex-end, center, baseline, stretch

* flex-start(默认): 从交叉轴的开始方向对齐
* flex-end: 从交叉轴的结束方向对齐
* center: 在交叉轴上居中对齐(垂直居中)
* baseline: 项目的第一行文字基线对准
* stretch(默认): 如果项目未设置高度，或者高度设为auto，将填满整个容器的高度


#### align-content

>该属性规定了容器项目各行(堆叠)的对齐方式，有六种可选的值：flex-start, flex-end, center, space-between, space-around, stretch

* flex-start(默认): 各行从弹性盒容器的起始位置堆叠
* flex-end: 各行从弹性盒容器的结束位置堆叠
* center: 各行从弹性盒容器的中间位置堆叠
* space-between: 各行在容器中均等分布
* space-around: 各行在容器中均等分布，且周围均等空间
* stretch(默认): 各行在容器内伸展以填满剩余空间

### 项目属性

flex的项目属性包括以下几种：

* order
* flex-grow
* flex-shrink
* flex-basis
* flex
* align-self


#### order

> ```<integer>;``` 该属性规定了容器中项目的排列顺序，数值越小，排得越靠前

#### flex-grow

> ```<number>;``` 该属性规定了容器中项目的放大比例，默认为0，即即使有剩余空间，也不放大

#### flex-shrink

> ```<number>;``` 该属性规定了容器中项目的收缩比例，默认为1，即如若空间不足，则默认收缩，若值为0，表示即使空间不足，也不收缩

#### flex-basis

> ```<length> | auto;``` 该属性规定了容器中项目在未放大之前，原本所占的空间大小，默认auto，即元素本身大小

#### flex

> ```none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]``` 该属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto，后两个属性可选

#### align-self

> ```auto | flex-start | flex-end | center | baseline | stretch;``` 该属性规定了容器中项目本身的对齐方式，若设置了，则会覆盖容器本身对齐方式的影响


### 结尾语

> 大概先总结到这，有时间写个demo把上面的属性都实践一遍。


### 参考

>[Flex 布局教程：语法篇](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html?utm_source=tuicool)
[Flexbox-CSS3弹性盒模型flexbox完整版教程](http://caibaojian.com/flexbox-guide.html)
