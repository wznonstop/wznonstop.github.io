---
layout: default
title: karma和jasmine初探
---


karma和jasmine初探
===================


karma和jasmine组合的大致理解：karma呢，就可以理解为我们赖以运行的架子，而jasmine呢，我们写具体的测试用例，用的是jasmine的语法。jasmine是在karma这个架子里的一部分，那些自动刷新啊，运行哪些文件啊，这些功能是karma提供的，jasmine就是我们选择的一种语法吧。

执行 karma init 之后会生成这个 karma.conf.js 文件 

![tree](https://raw.githubusercontent.com/wznonstop/wznonstop.github.io/master/images/2016-03-18-1.png)

具体的配置文件内容：[【点我进入参考链接】](http://www.cnblogs.com/wushangjue/p/4539189.html "reference")

![tree](https://raw.githubusercontent.com/wznonstop/wznonstop.github.io/master/images/2016-03-18-2.png)

所谓通的，意思就是。。。在 try1.js 文件里写的函数，可以在 try2.js 文件里进行测试，也可以在一个文件里又写功能函数，又写测试的函数。就像下面这样：

![tree](https://raw.githubusercontent.com/wznonstop/wznonstop.github.io/master/images/2016-03-18-3.png)

写好文件之后,在根目录下执行 karma start，就会自动打开 Chrome 窗口，像这样：

![tree](https://raw.githubusercontent.com/wznonstop/wznonstop.github.io/master/images/2016-03-18-4.png)

进入 debug 页面之后发现是空的。。。F12吧！

![tree](https://raw.githubusercontent.com/wznonstop/wznonstop.github.io/master/images/2016-03-18-5.png)

![tree](https://raw.githubusercontent.com/wznonstop/wznonstop.github.io/master/images/2016-03-18-6.png)

jasmine的语法，这个 [【点我进入参考链接】](http://www.cnblogs.com/wushangjue/p/4541209.html "reference") ，感觉基础的就够够的了吧，反正我也还没真的用上，不知道。高级些的东西在这里 [【点我进入参考链接】](http://www.cnblogs.com/wushangjue/p/4575826.html "reference") 

参考资料：

1.《Javascript测试框架Jasmine（一）：简介》 [【点我进入参考链接】](http://keenwon.com/1191.html "reference")

2.《前端自动化测试之路——karma 浏览器配置》 [【点我进入参考链接】](http://www.html-js.com/article/2544 "reference") (这个系列的"karma配置"这篇文章，有非常详细的关于karma配置的参数的介绍 )















