---
title: 工具类QA
date: 2023-08-19 21:32:00
tags: 工具类
---

* 软碟通解决：
  * 控制面板\时钟和区域——更改日期、时间或数字格式——管理——更改系统区域设置——beat版，使用unicode utf-8  取消勾选
* pe启动U盘：
  * 大白菜做好，测试好之后，直接把iso文件复制粘贴进去就好
  * USB-HDD模式：硬盘仿真模式，兼容性很高，适用于新机型，但对于一些只支持USB-ZIP模式的电脑则无法启动，**一般制作U盘启动盘选择该模式**。
  * USB-ZIP模式：大容量软盘仿真模式，在一些比较老的电脑上是唯一可选的模式，对新电脑来说兼容性不好，特别是2GB以上的大容量U盘。
* PE系统
PE是指Windows 预安装环境 (Windows PE) 是在Windows内核上构建的具有有限服务的最小 Win32 子系统，说白了就是把系统写进U盘里；iso是一种光盘镜像文件格式，装系统的过程说简单点都是把系统原版ISO镜像里的系统文件或者GHO压缩镜像里的系统文件写入C盘并给C盘加上引导程序的过程，如果说两种安装方式有区别那就是有些第三方制作的PE里可以附加程序，比如可以加入一些万能的驱动程序，或者嵌入一些广告应用程序等等，而纯净的系统ISO安装是不夹带这些的。

