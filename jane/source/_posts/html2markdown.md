title: HTML 2 Markdown
date: 2015-12-05 03:37:35
tags: 
- Markdown
---
>最近用了一个Markdown编辑器，界面甚得我心，只是还不太成熟，有太多bug
最坑爹的是只能markdwon to html，而不能反过来...

于是...
我决定研究一下，自己写一个函数来将html转为markdown语法<!-- more -->
古语云：知己知彼，方能百战百胜
所以要先弄清楚markdown的原理(好吧，我就是不熟，暴露了=_=!)
看一下伟大的维基百科: [Markdown](https://zh.wikipedia.org/wiki/Markdown),可知
* 空格 => 换行
那么这里直接将换行标签替换成空格
换行标签有 br 和 块级元素 p div ol ul 

---
2015-12-11 更新
我发现我真是太天真了...不是我现在的水平能写出来的东西啊~
所以最后用了这个 [to-markdown](https://github.com/domchristie/to-markdown)