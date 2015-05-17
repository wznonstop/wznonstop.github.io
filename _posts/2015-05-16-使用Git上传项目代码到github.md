---
layout: default
title: 使用git上传项目代码到github
---
#使用git上传项目代码到github#
1. 先在线上创建一个新的项目
2. 进行使用前的相关配置，如SSH Key的设置
3. 在本地的项目文件中（如文件夹ajaxdemo，要点进该文件夹），右键，选 "Git Bash"
4. 使用`git status`查看状态
5. 使用`git init`初始化
6. 添加文件

	*`git add .`句号代表所有文件
	
	*`git add README.md`或者是添加某一具体文件，此处为"README.md"
	
7. `git commit -m "first commit"`
8. `git remote add origin git@github.com:wznonstop/ajaxdemo.git`其中"wznonstop"的部分为具体的用户名，"ajaxdemo"为创建的项目名
9. 提交到线上`git push -u origin master`
