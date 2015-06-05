---
layout: default
title: 使用git上传项目代码到github
---
#Learning PHP, MySQL, JavaScript和CSS 2nd 读书笔记（一）#

##第一章
(1) 动态网页Request和Response执行过程的具体步骤：
<ul>
	<ol>1. 在浏览器的地址栏输入 http://server.com</ol>
	<ol>2. 浏览器会查询server.com对应的IP地址（通过域名访问Web服务器时，浏览器借助域名服务器，即DNS的辅助英特网服务找到与服务器对应的IP地址，然后利用这个IP地址和计算机进行通信）</ol>
	<ol>3. 浏览器向server.com的主页发送一个请求</ol>
	<ol>4. 这个请求通过Internet传输到达server.com的Web服务器端</ol>
	<ol>5. 接受到这个请求的Web服务器会在它的硬盘上寻找这个网页</ol>
	<ol>6. Web服务器注意到现在在内存中的主页面是一个包含PHP脚本的文件，将该页面传送给PHP解释器</ol>
	<ol>7. PHP解释器运行这些PHP代码</ol>
	<ol>8. 某些PHP包含MySQL语句，PHP解释器将这些MySQL语句传送给MySQL数据库引擎</ol>
	<ol>9. MySQL数据库引擎将MySQL语句的执行结果返回给PHP解释器</ol>
	<ol>10. PHP解释器将PHP代码的执行结果连带先前MySQL数据库引擎的执行结果返回给Web服务器</ol>
	<ol>11. Web服务器将页面返回给发出请求的客户端浏览器</ol>
	<ol>12. 浏览器将这个网页显示出来</ol>
</ul>





