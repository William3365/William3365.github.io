---
title: centos7
date: 2023-08-19 20:47:04
tags:	centos7
categories:	
---
## 注意

* 安装完成，拔出U盘，重启进入bios将启动顺序恢复至原来的顺序，**无论安装什么系统，都要这样!!!**

  其实大多数设备拔U盘之后，读不到U盘，就直接从系统盘读了，但是有时多系统，多硬盘的话，最好设置下启动项

* > * sata模式： stata AHCI （一般选择它，兼容模式）    # 如果需要做Raid，选择raid模式
  > *  write cache enabled 启用
  > * 引导模式：UEFI（推荐）



## 常用命令

重启：reboot
查看驱动器：ls /dev/sd*
详细信息：blkid



## bug

### 读不到U盘

* 报错，`Warning: /dev/root does not exist`

* 分析
  * 系统识别的U盘名和开机启动时设置的命名不一致，造成无法识别
    * 用UltraISO刻录镜像装机时会出现 Warning：dracut-initqueue timeout - starting timeout scripts 报错，原因在于系统找不到该镜像所在的正确位置，需要手动更改

* 解决
  * 先查看自己的u盘设备名称，**ls /dev/sd***
  * 然后  **blkid** 查看类型，记住，然后重启**reboot**
  * 选择安装项，然后**e**或者**tab**进入编辑，
    在**linux16**那边，**inst.stage2=hd:LABEL=CentOS\x207\x20x86_64**，更改为**inst.stage2=hd:/dev/U盘设备名**，
  * **回车**或者**ctrl+x**，即可正常安装
