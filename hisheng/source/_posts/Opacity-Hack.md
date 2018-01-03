title: Opacity Hack
date: 2015-12-26 16:37:49
tags: 
- css3 
- opacity 
- hack
---
IE8以下的浏览器不支持css3的opacity透明属性，但可以通过IE自带的方法来实现：<!-- more -->
    
>opacity: 0.45;
filter:alpha(opacity=45); /\*IE5-IE7\*/
-ms-filter:"progid:DXImageTransform.Mirosoft.Alpha(Opacity=45)"; /\*IE 8\*/