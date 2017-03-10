title: HTML5之Application Cache
date: 2017-03-08 17:48:55
tags:
- html5q
---

### 前言
> application cache 是 HTML5 用于支持离线应用的一项缓存技术。

### 构造一个简单的缓存应用
> 下面将一步步构造一个简单的缓存应用：只包括一个页面、一个标题和一张图片。


{% asset_img console_refresh.png %}

<!-- more -->

#### 1. 初始化应用，应用结构目录结构如下
{% asset_img catelog.png 应用结构目录结构 %}

#### 2. 页面 application-cache.html
```
<!DOCTYPE html>
<html manifest="example.appcache">
<head>
	<meta charset="utf-8">
	<title></title>
</head>
<body>
	<h1>应用缓存</h1>
	<img src="../static/img/example.png" alt="">
</body>
</html>
```
注意要在 html 元素添加属性：`manifest="example.appcache"`，其中 `example.appcache` 是缓存清单文件名，在此清单中罗列出你需要缓存的所有资源和页面。


#### 3. 缓存清单 example.appcache
```
CACHE MANIFEST
# v1 - 2017-03-08
# This is a comment.
http://localhost/test/html5/cache/application-cache.html
http://localhost/test/html5/static/img/example.png
```
在我们的缓存清单中，我们只简单地缓存了应用首页和其中引用到图片。至此，一个简单的离线应用就写好了。

#### 4. 测试
首先我们访问首页：
{% asset_img home.png 首页 %}
页面正常，查看控制台输出日志，我们发现，浏览器成功识别我们的缓存设置并将我们缓存清单中的资源进行了离线缓存。
点击控制台 `Application` => `Application Cache` => `example.appcache` => `top`，我们看到了已缓存的文件：
{% asset_img console_application_cache.png 已缓存的文件 %}
这时控制台切换到 `Network`，将 `Offline` 勾上(记住不要勾 `Disable cache` )。
{% asset_img console_offline.png %}
然后刷新浏览器，我们发现，页面依然可以正常访问。此时，我们再查看控制台：
{% asset_img console_refresh.png 刷新浏览器 %}
提示页面来自缓存。

### 兼容性
{% asset_img compatity.png 兼容性 %}

### 结论
通过简单的测试，我们发现 application cache 技术极大提升了用户体验，即使在弱网络环境下，用户也能正常地访问、浏览页面，使得 web 应用更接近于原生 app 的体验。更多详细信息参见：[使用应用缓存](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Using_the_application_cache#缓存清单文件)。