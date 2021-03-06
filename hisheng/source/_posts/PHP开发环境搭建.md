title: PHP+Apache开发环境搭建注意事项
date: 2016-09-04 10:52:04
tags:
- PHP
- 开发环境搭建
---
又是因为重装系统的原因，不得不重新走一遍PHP+Apache+MySQL的路，发现每一次搭建都会遇到不一样的坑，这次依然是不是很顺利，一大堆问题，慢慢叙来。
<!-- more -->
#### 安装PHP
安装版本: [php-5.6.25-Win32-VC11-x64](http://windows.php.net/downloads/releases/php-5.6.25-Win32-VC11-x64.zip)
首先要注意的是，PHP和Apache的版本一定要对应，否则装了之后你会发现Apache一直启动不了，我就是在这个问题上困惑了很久...
其实php官方网站是有提到这一点的，只是当时不太注意，所以说还是要仔细看官网的东西。
php有VC9,VC11和VC14三种版本，分别对应的前置条件是你系统中必须先安装有[VS2008 SP1](http://www.microsoft.com/en-us/download/details.aspx?id=5582)、[VS2012](http://www.microsoft.com/en-us/download/details.aspx?id=30679)和[VS2015](http://www.microsoft.com/en-us/download/details.aspx?id=48145)
所以你系统中如果已经装了以上某个VS，就直接装上对应版本的PHP就好了。
另外每个版本的PHP有对应有TS和NTS版本，分别是线程安全和非线程安全版本，直接安装安全版本就好了。


#### 安装Apache
安装版本: [httpd-2.4.23-win64-VC11](http://www.apachelounge.com/download/VC11/binaries/httpd-2.4.23-win64-VC11.zip)
错误: <blockquote> The requiest operation has failed </blockquote>

我PHP安装的是php-5.6.25-Win32-VC11-x64，所以Apache也要安装对应的64位VC11版本。
安装完之后，将bin目录下的ApacheMonitor.exe添加到环境变量中，同时记复制php目录下的php.ini-development为php.ini，修改配置开启需要的extension，然后复制一份到C盘windows目录下。双击ApacheMonitor看是否能启动成功。


#### 安装MySQL
以前安装MySQL基本没什么问题，这一次出现了这么一个错误提示:
<blockquote> TIMESTAMP with implicit DEFAULT value is deprecated. </blockquote>

解决方法: 找到安装目录的my-default.ini，复制一份为my.ini，内容如下

<blockquote>
# For advice on how to change settings please see
# http://dev.mysql.com/doc/refman/5.6/en/server-configuration-defaults.html
# *** DO NOT EDIT THIS FILE. It's a template which will be copied to the
# *** default location during install, and will be replaced if you
# *** upgrade to a newer version of MySQL.

[mysqld]

# Remove leading # and set to the amount of RAM for the most important data
# cache in MySQL. Start at 70% of total RAM for dedicated server, else 10%.
innodb_buffer_pool_size = 128M

# Remove leading # to turn on a very important data integrity option: logging
# changes to the binary log between backups.
# log_bin

# These are commonly set, remove the # and set as required.
basedir = C:/Program Files/MySQL/MySQL Server 5.6
datadir = C:/Program Files/MySQL/MySQL Server 5.6/data
port = 3306
server_id = 1

default-character-set=utf8

# Remove leading # to set options mainly useful for reporting servers.
# The server defaults are faster for transactions and fast SELECTs.
# Adjust sizes as needed, experiment to find the optimal values.
join_buffer_size = 128M
sort_buffer_size = 2M
read_rnd_buffer_size = 2M 

sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES 

explicit_defaults_for_timestamp=true #重点是这一句
</blockquote>