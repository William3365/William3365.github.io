---
title: idrac-ipmi
date: 2023-09-04 15:37:50
tags:  戴尔PowerEdge
---


# IPMI

* Intelligent Platform Management Interface，是一种用于管理和监控服务器的标准接口



## idrac

* Integrated Dell Remote Access Controller，戴尔集成远程访问控制器。是一个远程管理系统，由一块集成电路板组成，内置了支持和管理硬件的固件。idrac提供了一个Web界面，用户可以通过这个界面对服务器进行监控、管理、远程重启、重新启动操作系统等各种操作。同时，idrac还支持命令行方式和SNMP协议，以便更加方便地远程管理服务器。
* 默认登录凭据：用户名：root，默认密码：calvin



## 配置IPMI

* 仅针对戴尔服务器
  * 其他操作教程: `https://www.ngui.cc/el/1966116.html?action=onClick`



* 常规操作流程

  * 开机F2进 **system setup** 系统设置

  * 选择 **iDRAC Settings**，进入
  
    > * 如果需要**恢复默认配置**，选择 **reset idrac configguration to defaults**
    >   * 选择yes，等待初始化完成即可，continue，跳到系统设置界面，重新进idrac settings界面
    > * 如果**忘记密码**、**修改密码**，选择 **user configuration**，进去修改即可
  
  * 
  
  * 选择 **network** 网络设置（使用专用网络接口）
  
    > network settings
    >
    > * 启用NIC，enable nic选择 **Enabled**
    > * nic selection自动有，failover network故障转移网络可以不选，直接none
  
  * IPv4 settings
  
    > enable ipv4，选择 enabled   ，启用ipv4
    >
    > enable DHCP，选择 disabled  ，禁用dhcp使用静态ip
    >
    > 设置，ip，网关，掩码，DNS
  
  * IPMI settings
  
    > enable IPMI Over LAN，选择Enabled  ，通过局域网启用IPMI
  
    
  
  * 配置好之后，保存、退出
  
    
  
  * **检验**
  
    * 能ping通，能登录访问即可
  
      > 排错：
      >
      > ​	检验，ping ip、网关、外网，三个全可以才行
      >
      > ​	若ping 外网显示 name unknown 之类的，首先想DNS问题