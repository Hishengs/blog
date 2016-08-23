title: 安装nginx的坎坷之路
date: 2016-01-10 00:25:33
tags: 
- linux 
- nginx
---
#### 前言
一直听说nginx有多好有多好，于是准备入入坑，刚好最近在腾讯云买了个服务器，装的ubuntu，于是就决定在这上面装个nginx，没想到问题连连，当然大多数问题跟nginx无关，基本折腾在系统上了，我不知道是我不熟悉linux系统呢，还是说这确实是linux系统的坑爹之处，如果让普通用户来使用linux，安装卸载个软件分分钟都能弄死人...
我把这篇文章当作一个记录吧，接下来慢慢记录我是怎么在linux上折腾nginx以及其他各种问题的...

---
<!-- more -->
### 2016-1-10 先写个新鲜的吧
>前因:安装了nginx，本地浏览器localhost能成功访问，但是通过云服务器给的公有ip地址访问时却访问不了，各种折腾什么iptables之类的暂且按下不表，还是不成功，于是打算卸了重装试试，于是坑爹之路开始了...

通过命令 sudo apt-get remove nginx ，ok，那么卸载完之后就自然 sudo apt-get install nginx，正美滋滋地敲下 sudo service nginx start，error了，提示配置文件测试错误(具体什么错误也忘了截图了)，反正就是/etc/nginx/nginx.conf有问题了，于是又卸载了一次，留了个心眼，查找之后发现很多nginx相关的文件都还存在，也就是说nginx其实并没有卸载干净，怪不得重新安装的时候那么快...
于是查了一下，用 sudo apt-get autoremove nginx会比较好，试了还是不行，又换成了 sudo apt-get --purge remove nginx，这个卸载得比较干净，但是有些相关的依赖还是没卸载彻底，折腾了一个晚上，差点想哭，我不就重新安装一个软件嘛，至于这么百般刁难吗...(cry~)
>这里插播一句吐槽一下度娘，真的在查询技术相关的东西时，百度差google真的不止十条解，每次都给我一些不知所云，完全不切题也不能解决问题的网页

好了继续，一番辛苦之后，终于让我"百度"出了一篇有用的文章，链接[在这](http://www.2cto.com/os/201506/404306.html)，看来还是有人跟我碰到一样的问题的哈哈
具体卸载步骤如下：
1. 先卸载
>sudo apt-get --purge remove nginx
sudo apt-get autoremove

2. 查找相关依赖 
>dpkg --get-selections|grep nginx
这是查找结果：
nginx-common deinstall

3.把这些相关的东西一个个卸载了 
>sudo apt-get --purge remove nginx-common

4.重新运行安装命令 
>sudo apt-get install nginx

5.测试
>sudo apt-get service nginx start

重新打开localhost，亲切的“welcome to nginx!”又回来了！！

---

### 2016-1-10 2:21 竟然能访问了！
>刚才试着重新从外部ip访问想到竟然访问成功了！！究竟是什么原因我还没弄清楚...好像也没做什么啊？
{% asset_img nginx.png %}
仔细想想好像是我刚开始选择服务器的时候只选择开放了22端口(ssh)，后来想想可能是这个原因于是更改了安全组，开放了所有的端口，不过当时问题还是依然存在，于是就排除了这个原因，继续去折腾iptables，弄得要死要活的...难道是腾讯的云服务器更改安全组需要一段生效时间？如果是这样，它改了哪里？为什么我自己配置不行呢？哎，百思不得其解！
ps，iptables这个鬼东西还是有必要了解一下的，具体看这里[介绍](http://zhidao.baidu.com/link?url=TQJvXheEqgRnRcIh1DLdMCrmqTTOaYHvAjNHy3cSRejGsx4jjEiDocF-upuF-9-J3CBtrGBS9011DCTTTn24UHmpb_ULOFKDIJF5StUuaN_)

---
### 安装PHP
>版本：5.6.17

安装步骤:
* 1 下载[php-5.6.17.tar-gz](http://php.net/get/php-5.6.17.tar.gz/from/a/mirror)包，解压，cd到解压后的目录

* 2 sudo ./configure -enable-fpm 记住要加-enable-fpm，因为php默认是不开启fpm
{% asset_img php-install-configure.png %}

* 3 make & make install
这个过程充斥了一大堆log
{% asset_img php-install-make.png %}
ok，貌似编译成功了
{% asset_img php-install-make-result.png %}
然后我们make test一下，这个过程很长，看了一下有九千多个测试事例，最后会给出一个测试结果
{% asset_img php-install-make-test-result.png %}

* 4 接着我们要把php添加到环境变量里去，在 make & make install 的输出结果已经告诉我们php-cli安装在了/usr/local/bin
vim /etc/profile
在末尾加入
PATH=$PATH:/usr/local/bin
export PATH
要使改动立即生效执行
. /etc/profile 或 source /etc/profile
ok，一气呵成，不能再爽了！
{% asset_img php-install-dev-configure.png %}

* 5 接下来是要配置php-pfm，先 cd /usr/local/etc/php-fpm/，然后 cp php-fpm.conf.default php-fpm.conf
ok，然后运行一下php-fpm，出现错误提示：cannot get gid for group "nobody"
修改php-fpm.conf
user = ubuntu  #这里改为你自己的用户名
group = sudo   #这里改为你的用户组
再运行一下，成功了！

* 6 接下来就是配置nginx去解析php了
> ps，折腾了一整天了，终于配置好了，好想哭啊~
截图为证：
{% asset_img php-install-phpinfo.png %}
应该怎么配置呢，上面php-fpm能运行成功就不用去管他了，主要在于ngixn的配置，之前查了好多资料都是说在nginx.conf上配置，然后我就是找nginx.conf，可是没想到同名文件在两个不同地方都有，分别是/etc/nginx和/usr/local/nginx/conf/，你让我配哪个？？
好吧，只好每个都试试咯，修改配置如下(在nginx.conf的http双花括号末尾加上)：
{% asset_img nginx-conf.png %}
在两个地方同一个文件都修改过，期间不断重启nginx，认真检查每个格式，还是毛用没有...
就在我即将放弃想洗洗睡的时候，看到/etc/nginx下有个sites-available文件夹，于是误打误撞进去看了一眼，里面有个default文件，vim了一下，长这样：
{% asset_img nginx-sites-available-default.png %}
咦？怎么看起来有点眼熟啊？于是就试着把上面的配置粘贴了一份放在这里，好，重启nginx，访问浏览器，有了！！好神奇...
{% asset_img nginx-sites-available-default-modified.png %}
原来是配置在这？真是日了狗了...
也不是说网上的经验帖不对，我怀疑是不是不同nginx版本，他们的配置文件位置都会随意改动...真的是得视情况而定了

> 最后，吐槽一下linux下的软件安装管理，我不知道他们这么做是不是有什么高明的目的，但是安装一个应用，源文件在一个文件夹，安装又在一个位置，配置又是另一个位置，有时候还得你自己去添加环境变量...这样的用户体验真心不敢苟同啊，也许真的是应用领域不同的，linux可能更适用于服务器或者大型系统吧，但目标使用人群注定了只能是懂计算机的那么一小戳人群，术业有专攻，需要用到的时候你还是得乖乖去学。

* 7 总结一下 nginx和php 安装后各个位置的作用
#### nginx
/etc/nginx 这个应该是主程序位置
/etc/nginx/sites-available/default or /etc/nginx/nginx.conf 这是配置文件
/usr/local/nginx/conf 这里也有配置文件(我不知道为什么要分开这么放...)
/usr/local/nginx/conf/fastcgi.conf 这个文件定义了fastcgi的一些参数，所以在上面的配置我们直接include进来，就不用写那么多参数了
/usr/share/nginx/www 这是web根目录啦
/usr/local/nginx/html 这个貌似也是web目录，不知道和上面那个什么区别，晕-_-||
#### PHP
由于php我使用的是包安装的方式，所以位置就可以由你自己决定了，我是放在/usr/local/src这里，需要注意的是安装之后上层目录会生成一些相关的文件夹，包括php-cli和php-fpm，要记得把../bin/php添加到环境变量中

> 至此nginx+php终于弄好了，完成时间是2016-1-9 至 2016-1-10 18:50
郑海生20347任重而道远，这个经验帖还结不了...


---
#### nodejs npm 的安装
> 2016-1-10 23:59
有些东西真的不要用apt-get去安装，虽然简单了事，但也会给你带来很多的问题，最好还是采用源码安装的方式，或者直接下载包
今晚装nodejs和npm的时候就遇到坑了，通过apt-get install的nodejs竟然是1.x和0.6.x版本的，这得是多久以前的啊...
npm install之后一直提示 failed to fetch from registry，查了一下可能是版本原因，果断抛弃apt-get，直接在官网下了二进制包，解压到你想要的位置
有一点要注意，环境变量需要我们手动去配置的，不然node -v和npm -v都出不来