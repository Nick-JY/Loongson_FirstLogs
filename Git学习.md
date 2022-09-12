---
title: Git学习
date: 2022-09-11 16:38:30
tags: 
categories:
- [龙芯, Git]
---
- 常用命令
	- git init
		- 初始化，在本地git bash使用此命令后创建.git文件夹，使本地文件夹成为仓库，即每次版本的代码都会在里面
	- git clone <链接> 将所需要的东西下载到本地，且用此命令下载的是仓库，里面的每次修改也在里面，而直接download zip 只是最新版本
	- git add
		- git add 后可跟文件名也可直接git add -A 表示将所有文件送入暂存区
	- git commit
		- git commit -m “引号里面输入你对提交的信息的描述”    用于提交信息
	- git checkout <文件名>
		- 在工作区中的更改给打回去
	- git reset HEAD^
		- 提交后撤回
	- git push 推送当前分支的最新提交到远程
	- git pull   拉取远程分支最新的提交到本地
	- 本地远程双向更新先pull后push

- 分支
	- git checkout -b  <分支名> 从当前节点新建分支 
	- git branch 列举所有分支
	- git checkout <分支名> 单纯切换到某个分支
	- git branch -D <分支名> 删掉特定的分支
	- git merge <分支名> 合并分支


![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202209112251180.png)

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202209121048470.png)

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202209121055062.png)

![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202209121128369.png)
![](https://cdn.jsdelivr.net/gh/chengkhen/picture_via_picco/202209121131666.png)
