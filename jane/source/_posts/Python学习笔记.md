title: Python学习笔记
date: 2017-01-11 20:28:15
tags: 
- python
- 学习笔记
---

### raw_input 和 input
> raw_input 会把用户输入转换为字符串对象，而 input 则会保留原来的输入数据类型；然而在 python3 input 函数已经等同于 raw_input 的作用，如果想要实现 python2 input 的作用则需在 raw_input 之后使用 eval 函数将数据进行转换。

### print
> 在 python2 中，print 是一个语句；而在 python3，input 是一个函数，必须使用 () 将所需打印的信息包含起来。

<!-- more -->

### python 中的数据类型
> * 序列
	* list 列表
	* tuple 元组
	* string 字符串
	* unicode string 字符串
	* buffer 对象
	* xrange 对象
* dist 字典
* set 集合

### python 序列通用操作
#### 1.索引
> 与其他高级语言的索引方式相同，通过数字下标进行索引操作：`` numbers[index] ``

#### 2.分片
> 分片是 python 区别于其他语言的一个很有用的特性。通过分片可以对序列进行任意的切割，获取所需的数据。
分片的基本使用形式：`` numbers[left_index:right_index:step] ``，其中 left_index 是指分片的开始位置，right_index 是分片的结束位置，step 是分片时的步长。需要注意的是：1.分片是**左闭右开**的，也就是包含 left_index 位置的元素不包含 right_index 位置的元素；2.另外 left_index、right_index、step 均可省略。此时 [::] 代表的是复制整个序列。3.步长 step 可以为负数，此时必须满足 left_index > right_index，此时步长方向是从右到左截取元素。


#### 3.相加
> 必须是同一种序列类型才能进行相加的操作。
字符串：`` 'hisheng' + 'is' + 'handsome' // 'hisheng is handsome' ``
列表：`` [1,2,3] + [4,5] // [1,2,3,4,5] ``
元组：`` (1,2,3) + (4,5) // (1,2,3,4,5) ``

#### 4.相乘
> 必须是同一种序列类型才能进行相乘的操作。
字符串：`` 'hisheng'*2 // 'hishenghisheng' ``
列表：`` [1,2,3]*2 // [1,2,3,1,2,3] ``
元组：`` (1,2,3)*2 // (1,2,3,1,2,3) ``

#### 5.成员判断
> 判断某一元素是否是序列中的成员。( 判断是否存在序列中 )
`` 1 in [1,2,3] // True ``