title: windows上更新npm
date: 2016-05-27 14:32:18
tags: 
- nodejs
- npm
---

今天遇到一个项目需要更新npm的版本，搜了一下如何更新npm的方法，有的人说直接重装node，npm版本就会是最新的，真是无力吐槽，要是每次更新都得这么麻烦还得了，我觉得一定有更好更简单的方法<!-- more -->，最后果然在[stackoverflow](http://stackoverflow.com/questions/18412129/how-do-i-update-node-and-npm-on-windows 'stackoverflow')发现了一个很有用的方法，只需要简单的几步：
windows上以**管理员身份**打开powershell，输入：
```
Set-ExecutionPolicy Unrestricted -Scope CurrentUser -Force
```
接着在cmd输入
```
npm install -g npm-windows-upgrade
```
然后输入
```
npm-windows-upgrade
```
就可以更新npm了，还可以选择要更新的版本，相当方便

具体可以查看该插件官方的[github](https://github.com/felixrieseberg/npm-windows-upgrade 'github')教程
