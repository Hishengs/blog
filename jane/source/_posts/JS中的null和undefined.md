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

上班时间偷个懒，自问自答，同样先抛玉引“砖”，推荐几篇文章：
* [why is typeof null “object”? - StackOverflow](http://stackoverflow.com/questions/18808226/why-is-typeof-null-object)
* [The history of “typeof null” - ES Wiki](http://www.2ality.com/2013/10/typeof-null.html)
* [harmony:typeof_null - 2ality](http://wiki.ecmascript.org/doku.php?id=harmony:typeof_null)
* [typeof - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof)

看这段：
> "The “typeof null” bug is a remnant from the first version of JavaScript. In this version, values were stored in 32 bit units, which consisted of a small type tag (1–3 bits) and the actual data of the value. The type tags were stored in the lower bits of the units. There were five of them:
000: object. The data is a reference to an object.
1: int. The data is a 31 bit signed integer.
010: double. The data is a reference to a double floating point number.
100: string. The data is a reference to a string.
110: boolean. The data is a boolean.
That is, the lowest bit was either one, then the type tag was only one bit long. Or it was zero, then the type tag was three bits in length, providing two additional bits, for four types."

大概意思就是：
null其实是一个原始值，也是属于Null类型，本来 typeof null 结果应该是 "null" 才对，但是因为
> JS类型值是存在32位单元里,32位有1-3位表示TYPE TAG,其它位表示真实值，而表示object的标记位正好是低三位都是0，即
000: object. The data is a reference to an object.
而js里的Null是机器码NULL空指针,所以空指针引用加上对象标记还是0,最终体现的类型还是object.

so
> This is a bug and one that unfortunately can’t be fixed, because it would break existing code.

其实就是一个bug，曾经也有人提案建议修正，但是因为影响甚深，被否决了，所以也就不好再修改了，只好将错就错，就这么使用着貌似也没多大问题...