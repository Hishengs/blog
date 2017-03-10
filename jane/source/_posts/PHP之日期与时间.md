title: PHP之日期与时间
date: 2017-03-10 18:11:22
tags:
- php
---

> 由于一直依赖于 Javascript 的时间日期处理库 [Moment](http://momentjs.com/)，所以一直以为时间与日期方面的处理应该不算麻烦。然而 PHP 这方面的支持个人觉得并不是很好，每次需要处理时间我都是得进行一番搜索，这里拼一点，那里凑一点，没有一个统一的认识过程。因此，写下这篇文章用于整理 PHP 时间与日期处理方面的技巧。

<!-- more -->

其实，简单地来说，时间处理无非是两个方面之间的转换：1. 时间戳 2. 格式化时间/日期字符串。所以，我们从这两方面入手。


#### 时间戳
---
1. 获取当前时间戳(秒)
	```php
	time(); // 1489141262
	```
2. 创建时间戳
	> 函数原型：`int mktime ([ int $hour = date("H") [, int $minute = date("i") [, int $second = date("s") [, int $month = date("n") [, int $day = date("j") [, int $year = date("Y") [, int $is_dst = -1 ]]]]]]] )`

	```php
	mktime(0, 0, 0, 12, 31, 2001); // 1009756800
	```

#### 格式化时间/日期字符串
---
1. 使用 `date()` 获取格式化字符串
	> 函数原型：string date(string format [, int timestamp])

	```php
	// 获取当前时间格式化字符串
	date('Y-m-d'); // 2017-03-10
	// 获取指定时间戳格式化字符串
	date('Y-m-d',1218124800); // 2008-08-08
	```

#### 时间戳与字符串的转换
---
1. 字符串转为时间戳
	> strtotime()

	```php
	$str = '2016-06-08';
	$time = strtotime($str); // 1465344000
	```

2. 时间戳转为字符串
	> 可以使用上面介绍的 [`date()`](http://php.net/manual/en/function.date.php) 函数，或者使用 [`strftime()`](http://php.net/manual/en/function.strftime.php) 函数：

	```php
	strftime('%Y-%m-%d',1465344000); // '2016-06-08'
	```

#### 常用的时间日期函数
---
1. 验证时间是否合法有效
	```php
	Boolean checkdate(int month, int day, int year)
	checkdate(4, 31, 2010); // false
	```

#### 常用需求场景
