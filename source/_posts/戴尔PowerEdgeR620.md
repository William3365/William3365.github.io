---
title: 戴尔PowerEdgeR620
date: 2023-08-25 22:14:50
tags:  戴尔PowerEdge
---
## PERC 阵列卡

* PERC 是 PowerEdge Raid Controller 的缩写
* 前缀S表示为Software软件阵列，H 表示为Hardware 硬件阵列 ,
* 从入门到高端型号第一位数字分别用1 3 7 8 表示，
* 第二三位数字位为产品代数，
* 结尾P表示 Performance 高性能型。

## PERC名词

* Disk Group：磁盘组，这里相当于是阵列，例如配置了一个RAID5，就是一个磁盘组。
* VD：Virtual Disk， 虚拟磁盘，虚拟磁盘可以不使用阵列的全部容量，也就是说一个磁盘组可以分为多个VD。
* PD：Physical Disk，物理磁盘。


## 配置Raid方法

* 1、F10直接做在生命周期控制器中，F10可选中文，会重启很麻烦
* 2、F2在系统设置中做  ----√   简单明了
* 3、ctrl+R做，界面繁琐麻烦
* 问题：同样的raid级别，在ctrl+R中配置和在F2中配置，容量会不一样，不知道为什么！

### 流程
* 1、改sata模式为raid
* 2、做raid
* 3、boot mode模式按需选择

## bugs
* 在安装系统时，系统文件里，不带有RAID 1的驱动程序，导致安装系统无法识别到RAID 1 的硬盘。需要手动加载 RAID 卡驱动程序
* raid版本和主板版本可能存在版本问题，注意匹配



