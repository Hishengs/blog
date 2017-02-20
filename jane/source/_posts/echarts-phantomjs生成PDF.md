title: echarts+phantomjs生成PDF
date: 2017-02-15 18:09:57
tags:
- echarts
- phantomjs
---
## 需求分析
> 原本的方案是使用前端工具或者浏览器自带的生成 PDF 的功能，但是不同用户的浏览器类型、版本各异，生成的 PDF 效果大相径庭，不是很理想。于是急切需要一个稳定的、一致的 PDF 生成方案。


## 思路分析
> 主要有两种方案：1.前端收集所有 echarts 实例生成的 base64 图片回传到服务器，服务器根据图片数据替换掉原先模板所有的 echarts 位置，并返回一个静态页面给 phantomjs 调用生成 PDF，然后供用户下载；2.服务器端直接渲染动态的的页面，不过设置一个等待时间，这个时间预计是所有 echarts 图表实例完成渲染的时间，不过不够准确。

## 解决步骤
### 1.服务器端部署 phantomjs 
这一步并不难，直接官网下载 [zip](https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-windows.zip) 包，解压到你要安装的路径。解压后注意两点：
* 将 /bin 目录添加到环境变量中去。
* /examples 目录下的 rasterize.js 是我们用于生成 PDF 的工具文件，稍后将修改此文件。

### 2.前端收集页面所有的 echarts 实例 base64 url 并回传给服务器
这里主要是依次使用`echartsIns.getRenderedCanvas().toDataURL()`获取图表的 base64 url，最终回传的数据结构大致是：
```
[
	{
		id: 'xxx-line',
		base64url: 'base64url',
	},
	{
		id: 'xxx-bar',
		base64url: 'base64url',
	},
]
```

### 3.服务器端利用前端回传的数据构造静态页面
这里服务器端接收到前端回传的数据之后有两种方式构造静态页面：
1.根据 id 找到原先实例 div 设置其背景图片：`background-image:url('base64url');`
2.根据 id 找到原先实例 div，构造 img => `<img src="base64url">` 替换掉原先的 div
依次执行以上任一方法替换掉所有实例并生成一个静态页面。

### 4.phantomjs 根据生成的静态页面地址渲染 PDF 并返回 PDF 地址供用户下载
假设现在得到的静态页面地址是：`/xxx/yyy/static.html`，希望保存的 PDF 地址是 `/aaa/bbb/ccc.pdf`
执行命令 `phantomjs rasterize "/xxx/yyy/static.html" "/aaa/bbb/ccc.pdf"` ，phantomjs 就会生成 PDF 到相应的位置。
我们还可以指定生成的 PDF 页面大小：
`phantomjs rasterize "/xxx/yyy/static.html" "/aaa/bbb/ccc.pdf" "1080px*720px"`

> 以上是方案一的实现步骤，好处是直接渲染静态页面，速度快，缺点是实现相对复杂。接下来介绍方案二。

### 4.phantomjs 直接渲染动态页面。
假设我们要渲染的页面地址是：`/xxx/yyy/dynamic.html`，我们可以直接执行`phantomjs rasterize "/xxx/yyy/dynamic.html" "/aaa/bbb/ccc.pdf" "1080px*720px"` 生成 PDF，但是如果页面 echarts 图表实例较多，往往 PDF 生成时图表还没渲染完成，所以此时最好设置一段等待时间，等待图表渲染完成再让 phantomjs 去生成 PDF，主要实现方法是修改 rasterize.js:
将其中：
```
window.setTimeout(function () {
    page.render(output);
    phantom.exit();
}, 200);
```
setTimeout 的时间修改为你觉得合适的时间。