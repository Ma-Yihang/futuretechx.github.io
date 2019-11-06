---
layout:     post
title:      常用 Linux 命令的基本使用
subtitle:    "Linux"
date:       2016-03-06
author:     Cosmo-Ma
header-img: img/post-default.jpg
catalog: true
tags:
    - Linux
---

**目标**
- 理解学习 Linux 终端命令的原因
- 常用 Linux 命令体验

**01. 学习 Linux 终端命令的原因**
- Linux 刚面世时并没有图形界面，所有的操作全靠命令完成，如 磁盘操作、文件存取、目录操作、进程管理、文件权限 设定等
- 在职场中，大量的 服务器维护工作 都是在 远程 通过 SSH 客户端 来完成的，并没有图形界面，所有的维护工作都需要通过命令来完成
- 在职场中，作为后端程序员，必须要或多或少的掌握一些 Linux 常用的终端命令
- Linux 发行版本的命令大概有 200 多个，但是常用的命令只有 10 多个而已

**02. 常用 Linux 命令的基本使用**
序号	命令	对应英文	作用
01	ls	list	查看当前文件夹下的内容
02	pwd	print wrok directory	查看当前所在文件夹
03	cd [目录名]	change directory	切换文件夹
04	touch [文件名]	touch	如果文件不存在，新建文件
05	mkdir [目录名]	make directory	创建目录
06	rm [文件名]	remove	删除指定的文件名
07	clear	clear	清屏

小技巧

 - ctrl + shift + = 放大终端窗口的字体显示 
 - ctrl + - 缩小终端窗口的字体显示
- 自动补全，按下 tab 键
- 按 上／下 光标键可以在曾经使用过的命令之间来回切换
- 如果想要退出选择，并且不想执行当前选中的命令，可以按 ctrl + c