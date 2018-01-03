title: HTML5之音频、视频
date: 2017-03-08 15:54:48
tags:
- html5
---

## 1. 使用方法
* 音频
	```
	<audio src="http://v2v.cc/~j/theora_testsuite/320x240.ogg">
	  你的浏览器不支持 <code>audio</code> 标签.
	</audio>
	```
* 视频
	```
	<video src="http://v2v.cc/~j/theora_testsuite/320x240.ogg">
	  你的浏览器不支持 <code>video</code> 标签.
	</video>
	```
	
<!-- more -->

## 2. 相关属性
> 只列举常见的属性。

* `src` 资源地址
* `volume` 音量
* `autoplay` 是否自动播放(布尔值)
* `loop` 循环(布尔值)
* `controls` 提供控制(布尔值)
* `preload` 预加载(枚举: `none`,`metadata`,`auto`)
* `controls` 提供控制
* `buffered` 已缓存资源信息
* `muted` 是否静音(布尔值)
* `played` 已播放的资源信息

## 3. 相关方法
* `play` 播放
* `pause` 暂停

## 4. source 元素

## 5. 例子