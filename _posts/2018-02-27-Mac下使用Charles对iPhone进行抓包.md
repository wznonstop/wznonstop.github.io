---
layout: default
title: Mac下使用Charles对iPhone进行抓包
keywords: Charles, Mac Charles, 抓包, iPhone抓包
sitecontent: Charles, Mac Charles, 抓包, iPhone抓包
---


Mac下使用Charles对iPhone进行抓包
===================

最近在使用[APIcloud](http://www.apicloud.com/)进行手机端的开发，嗯，说白了是在一个壳里面写页面嘛，换了个运行环境。今天get到了一个新的技能，就是用charles抓手机的包，看到手机上的请求刷刷的出现在眼前的时候，仿佛打开了新世界的大门，哈哈哈哈哈，感谢给我打开新世界大门的同事！


### PC上的相关配置
1. 首先，第一步，当然是下载Charles这个工具啦


2.第二步，试试这个工具好不好使，很简单，刷新一下浏览器，看到发出的请求就说明没问题了。什么，你说没看到？同学你是不是开了代理忘关了。。。


3. 第三步，设置端口：在上面的菜单栏选择 Proxy --> Proxy Settings... ，就可以配置端口了，默认的是 8888，用默认的就行了。


4. 查看电脑的IP地址，可以命令行输 ifconfig，也可以在Charles的菜单栏，选择 Help --> Local IP Address... ，都可以看到IP地址，假设为 10.129.104.104。


### iPhone上的相关配置
1. 前提：手机和电脑在同一局域网下。


2. 打开iPhone 设置 --> 无线局域网 --> 点击网络名后面的（i）图标 --> 滚到最下方的 "HTTP代理" 切换到 "手动" tab标签，在 "服务器" 一栏填写电脑的IP地址，如 10.129.104.104 ，在 "端口" 一栏填写前文在Charles里设置的端口号，如 8888。


3. 在手机上进行一个需要发请求的操作吧，Charles会弹出一个提醒，点击确定，就会发现新世界的大门已经打开啦～