title: JS中的null和undefined
date: 2016-03-16 00:04:57
tags:
- Javascript
---
夜深，今晚本来准备早早睡觉的，可突然想到JS中一个很有趣的问题(程序员的通病，总是把工作带到生活中去，(╯‵□′)╯︵ ┻━┻，摔！)：

> null和undefined的关系和区别？

<!-- more -->

先在前面放几篇我认为写的很好的文章，然后再发表一下我浅陋的看法...
* [探索JavaScript中Null和Undefined的深渊-颜海镜](http://yanhaijing.com/javascript/2014/01/05/exploring-the-abyss-of-null-and-undefined-in-javascript/)
* [undefined与null的区别-阮一峰的网络日志](http://www.ruanyifeng.com/blog/2014/03/undefined-vs-null.html)

引用一下《Javascript权威指南》中对二者的比较(第6版，32页)：
> Javascript中有两个特殊的原始值：null和undefined，它们不是数字，字符串和布尔值。它们通常分别代表了各自特殊类型的唯一的成员。

我自己结合前人博文和书籍的经验，认为：
1.null和undefined是Javascript中的关键字，同时也是基本数据类型之一。属于数据类型中的**原始类型**

{% asset_img 1.png %}

2.null表示 **正常情况** 下的空值，即表示该变量的值是空的，或者表示该对象是空的对象，不包含任何的属性和方法

3.undefined表示 **出乎意料**、 **有错误** 的值的空缺，当一个变量只是声明而未定义未初始化时，代表该变量的值是空缺的，此时其值就用undefined来表示

4.null和undefined从布尔值上来判断都等于false(因为都代表空值)，即 null == false , undefined == false , null == undefined

5.null和undefined都是一个 **值** ，它们都属于null和undefined类型的唯一成员

---
最后留一个问题

> 为什么 typeof null 得到的结果是 object ？