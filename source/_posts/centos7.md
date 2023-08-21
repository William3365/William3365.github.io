---
title: test2
date: 2023-08-19 20:47:04
tags:	centos7
categories:	
---
重启：reboot
查看驱动器：ls /dev/sd*
详细信息：blkid

===》
读不到磁盘
system steup，system biso，sata setting
1、embedded stata AHCI 兼容模式
2、write cache enabled 启用

===》
报错，Warning: /dev/root does not exist
https://blog.csdn.net/qq_33427869/article/details/126668794

分析
1.系统识别的U盘名和开机启动时设置的命名不一致，造成无法识别

解决
先查看自己的u盘设备名称，ls /dev/sd*,一般是sda4（建议blkid查看下类型）
选择test安装第二项，然后tab进入编辑，
inst.stage2=hd:LABEL=CentOS\x207\x20x86_64”字样更改为“inst.stage2=hd:/dev/sdb4，回车安装即可

tips
用UltraISO刻录镜像装机时会出现 Warning：dracut-initqueue timeout - starting timeout scripts 报错，原因在于系统找不到该镜像所在的正确位置，需要手动更改
报错之后，ls查看，blkid查看，记住设备名称
reboot重启，
按下tab，修改hd：xxxx为设备名称，回车安装即可

===》
磁盘空间不足，自定义分区，用-号，删除即可

