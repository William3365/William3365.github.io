---
title: idrac-ipmi
date: 2023-09-04 15:37:50
tags:  戴尔PowerEdge
---


# IPMI

* Intelligent Platform Management Interface，是一种用于管理和监控服务器的标准接口



## idrac

* Integrated Dell Remote Access Controller，戴尔集成远程访问控制器。是一个远程管理系统，由一块集成电路板组成，内置了支持和管理硬件的固件。idrac提供了一个Web界面，用户可以通过这个界面对服务器进行监控、管理、远程重启、重新启动操作系统等各种操作。同时，idrac还支持命令行方式和SNMP协议，以便更加方便地远程管理服务器。
* 默认登录凭据：用户名：root，密码：calvin



## 配置IPMI

* 仅针对戴尔服务器
  * 其他操作教程: `https://www.ngui.cc/el/1966116.html?action=onClick`



* 常规操作流程

  * 进入系统设置，选择 system BIOS

  * 选择 iDRAC Settings
  * 到最下边，选择 reset idrac configguration to defaults
  * 选择yes，等待结束，选择continue
  * 再次选择 iDRAC Settings，选择 network（使用专用网络接口）
  * NIC相关配置，Enabled启用nic，选择 dedicated
  * 网络设置，IPv4 设置，ip，网关，掩码
  * IPMI Over LAN（通过局域网启用IPMI）选项，选择Enabled
  * 配置好之后，能ping通，能登录访问即可