---
title: VNC
date: 2023-10-09 17:41:44
tags:	远程控制
categories:	
---



# VNC



## 什么是vnc

* Virtual Network Computing，VNC就是一个通过软件方式实现ATM 网络计算机模式的软件系统，它是由AT&T开发的一套远程控制的开源软件。
* 当网络中的计算机安装了相应的VNC 软件后，就可以在计算机上随时建立和取消对远端计算机的管理控制，所以给这个软件起名为“虚拟网络计算机”
* VNC采用Server/Client模式，由VNC Server和VNC Viewer（Client）两部分组成，所有不同平台版本的VNC，不管是Server还是Client，都支持VNC的通讯协议RFB，这样就能够很容易地实现不同平台的相互操作。
* **VNC Server**的操作系统和TCP/IP协议栈都能正常工作，具有能访问到的IP地址，并且启动VNC Server后，才能对它进行远程控制。
* **VNC Viewer（Client）**，通常工作在5900端口，使用时需提前获得server的ip(有时需要端口)、用户名和密码



## 远程管理技术之间的区别

* **VNC**是一种软件级别的远程桌面协议，它允许用户在本地计算机上通过网络连接到远程计算机，并实时地查看、控制远程计算机的桌面界面。主要用于远程桌面连接和控制。
* **IPMI**是一种硬件级别的管理接口，它允许管理员通过网络连接到远程服务器或设备，进行监控、管理和控制操作。IPMI提供了诸如远程开关机、系统重启、传感器数据监测、事件日志记录等功能。IPMI可以在服务器关机或操作系统崩溃的情况下，仍然对硬件进行管理和维护。IPMI主要用于服务器硬件管理



## 远程管理方式之间的区别

* workbench连接
  * 线管理云服务器的工具，利用浏览器直接登录云服务器，无需安装任何软件或插件。workbench的优点是方便快捷，不受网络环境和操作系统的限制，但缺点是功能相对较少，不能进行复杂的操作和设置。
* VNC连接
  * 优点是功能强大，可以进行图形化界面的操作和设置，但缺点是需要安装客户端软件，必须在同一网络，并且受网络环境和防火墙的影响
* SSH连接
  * 比较灵活，可以根据不同的操作系统和需求选择不同的工具，比如linux利用shell工具（xshell，finalshell）进行连接，windows使用自带的远程桌面连接（mstsc）或第三方软件如PuTTY来连接
  * 使用时需要确保电脑和云服务器之间的网络通畅，并且服务器的安全组规则（防火墙）允许您的电脑访问云服务器的远程桌面或SSH端口（默认为3389或22）





## 注意事项

#### VNC远程不能输入字符问题

* vnc server会要求vnc viewer的OS的输入法和vnc server那边OS的语言一致。一般Linux系统都是英文的，所以使用vnc viewer连入的时候，关闭本地OS的输入法切换到英语就可以了。

#### 安全问题

* 为了保证数据安全，除管理员外，要设置对应的账号、权限，做到每一个操作都必须被授权，每一个账号的密码不冲突



## 硬件VNC

* 云手Ez2Pc单口远程IP控制器
* ![](https://z1.ax1x.com/2023/10/09/pPxJuFJ.jpg)