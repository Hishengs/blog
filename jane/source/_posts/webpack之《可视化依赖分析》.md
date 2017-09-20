title: webpack之《可视化依赖分析》
date: 2017-05-23 12:09:29
tags:
- webpack
- javascript
---

## 前言
> 毋庸置疑，webpack 是一个非常好用的打包工具，当然它能提供的功能远不止于依赖打包。在日常的前端工作流中，我已经完全离不开 webpack 了。
不过，正是因为它的便捷，我发现我的项目依赖变得越来越臃肿，很多包的依赖 webpack 都帮你自动处理了，然而这一过程对你来说是不透明的，你很难知道是否有些东西是你不需要的或者由于错误的写法引入了不必要的包，增加了项目的体积。
不过幸好，webpack 提供了方法供我们对自己项目进行依赖分析，结合一些可视化的工具我们可以一目了然地看出项目整体的依赖情况。

<!-- more -->

## 正文

### 1. 生成依赖分析文件
这仅仅是命令行下一行命令就可以做到：
`webpack --profile --json > stats.json`
默认 webpack 配置文件是 `webpack.config.js`，如果你的配置文件不是这个名字，则手动指定：
`webpack --config=webpack-dev.config.js --profile --json > stats.json`
执行完成，会在当前目录下生成一个 `stats.json` 文件。

### 2.使用可视化工具
有了 `stats.json` 文件我们就可以通过把该文件上传到提供 webpack 可视化分析的网站进行分析，主要有两个：
1. [webpack analysis](http://webpack.github.io/analyse/)
2. [webpack visualizer](http://chrisbateman.github.io/webpack-visualizer/)

个人更偏向后者。
上传之后就可以看到分析结果了：
{% asset_img visualizer.png %}
