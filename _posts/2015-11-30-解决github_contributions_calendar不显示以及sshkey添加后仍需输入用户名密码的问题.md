---
layout: default
title: 解决github_contributions_calendar不显示以及sshkey添加后仍需输入用户名密码的问题
keywords: github_contributions_calendar, sshkey 用户名密码
sitecontent: github_contributions_calendar, sshkey 用户名密码
---

解决github_contributions_calendar不显示以及sshkey添加后仍需输入用户名密码的问题
===================




上次写了那篇["JavaScript实现无序多叉树先序遍历的效果"](http://wznonstop.github.io/2015/11/23/JavaScript%E5%AE%9E%E7%8E%B0%E6%97%A0%E5%BA%8F%E5%A4%9A%E5%8F%89%E6%A0%91%E5%85%88%E5%BA%8F%E9%81%8D%E5%8E%86%E7%9A%84%E6%95%88%E6%9E%9C.html)的博客，早上鼓起勇气，给以疯狂吐槽我为乐的学长[呵呵](https://github.com/youngerheart)发了个链接，为避免遭到狂轰乱炸，我加了句“不准吐槽！”，万万没想到的是他居然真的没吐槽( •̀∀•́ )，不过只是没有针对那篇博客吐槽，他吐槽了我的github Contributions Calendar不显示以及提交代码要输入用户名密码。好，那我就把它们解决了，在这里记录一下。

----------


github Contributions Calendar不显示的问题
-------------

解决问题主要参考了这两篇博客：["contributions不显示在github上"](http://playbear.github.io/2014/08/11/no-contributions/)，["Github不记录Contributions的问题"](http://www.dss886.com/git/2014/09/15/01/)。第二篇博客解释的比较详细，并有Github关于Contributions说明的翻译，第一篇博客简单明了，两行代码解决问题：

    git config --global user.name "wznonstop"
    git config --global user.email "wznonstop@163.com"

然后查看一下：


![git-config](https://raw.githubusercontent.com/wznonstop/wznonstop.github.io/master/images/11_30_1.png)

然后再提交就会发现，小绿点又出现了！
我遇到这个问题的原因是，现在用的公司电脑，开始的时候根本就没有`.gitconfig`配置文件o_O，所以写一下就好了。


sshkey添加后仍需输入用户名密码的问题
-------------
提交代码要输入用户名密码，这是问题吗，我是怕自己忘了密码才故意这样的。。。好吧其实是懒，但这真的不是问题啊，不就是加个sshkey吗，分分钟的事。但是！我分分钟加好之后试了一下，发现╭(°A°`)╮怎么还要输用户名密码，上github的网页一看，它说我新加上的这个sshkey没用过，我就傻了，然后，当然是谷歌大法好了。看到了这篇博客————["github设置添加SSH"](http://www.cnblogs.com/ayseeing/p/3572582.html)，前面不用看，直接跳到第4步————“测试一下该SSH key”，跟着流程走了一遍，github上我新加的sshkey前面的小绿点就亮啦！搞定~


彩蛋！
-------------
好吧，其实不是彩蛋，再加一个刚才遇到的问题，我提交的时候把博客的名字写错了，修改之后又提交了一下，结果发现线上这两篇博客都存在，我pull也不能把之前那个错的pull下来，我push也不能把本地这个样子的push上去，怎么办呢，我想了个办法，把本地的删了，重新clone了一份下来，我以为这样把本地的那个错误的文件删了就可以push了，真是图样图森破，当然还是不行，只好谷歌，找到解决方法：

    git commit -a -m "A file was deleted"

	git push


这就是提交删除文件的操作。


总结
-------------

我解决了github Contributions Calendar不显示以及sshkey添加后仍需输入用户名密码的问题，很开心\(^o^)/~嗯，就酱，我的演讲结束了，谢谢大家！\(^o^)/


呃。。。
-------------
其实我在提交的时候发现，还是要输用户名、密码啊，我再找找原因。


嗯，找到了！
-------------
是这样的。。。还是上面的那篇博客————["github设置添加SSH"](http://www.cnblogs.com/ayseeing/p/3572582.html)，我在上面说，前面不用看，于是就把一个比较关键的地方漏掉了，下面内容摘自该博客：


> **https 和 SSH 的区别：**

> - 1、前者可以随意克隆github上的项目，而不管是谁的；而后者则是你必须是你要克隆的项目的拥有者或管理员，且需要先添加 SSH key ，否则无法克隆。
> - 2、https url 在push的时候是需要验证用户名和密码的；而 SSH 在push的时候，是不需要输入用户名的，如果配置SSH key的时候设置了密码，则需要输入密码的，否则直接是不需要输入密码的。

这就很明确了，虽然我的sshkey已经配得没问题了，但由于我是通过 https url 将项目克隆下来的，所以无论怎么折腾，都得输用户名、密码，我把本地的项目删了，用 SSH 重下了一下，再试就不用输了~