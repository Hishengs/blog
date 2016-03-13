title: ubuntu界面无法登陆
date: 2016-01-09 16:59:52
tags: 
- linux 
- ubuntu
---
在云服务器上装了ubuntu,不过只有命令行，于是装了下界面，操作也方便
>sudo apt-get install ubuntu-desktop

这是一件安装的方法，如果对linux不太熟悉，最好就用这个简单了事
<!-- more -->
安装后重启顺利出现了欢迎界面，可是发现只能以游客的身份登入，每次以用户密码登入时都会闪一下重新返回登陆界面，我猜想可能是密码不对，然后ctrl+alt+f1回到命令行，输入用户名密码发现可以登陆，看来不是这个原因，网站搜索了一下，发现[这篇文章](http://blog.sina.com.cn/s/blog_4ba5b45e0102ejmn.html)介绍的方法可以解决问题，具体步骤如下：
* 1 删除对应账户主目录下的.Xauthority 例如我的帐户名是ubuntu,那我的home目录就在 /home/ubuntu
```
//为以防万一，建议先copy一下这个文件
sudo rm /home/ubuntu/.Xauthority
```

* 2 删除/tmp/.X0-lock
```
sudo rm /tmp/.X0-lock
```

到这里差不多就ok了，接着命令行输入 sudo service lightdm restart 重新启动进入界面
不过，我在进入界面登陆后提示 Could'not update ICEauthority...
分析一下应该是没有这个文件的权限，重新ctrl+alt+f1进入命令行一看，果然.ICEauthority这个文件不是属于ubuntu而是root，那么问题就很容易解决了
```
sudo chown -R ubuntu /home/ubuntu
```
把主目录及其下所有的文件所有改为ubuntu

重新进入界面，登陆成功！