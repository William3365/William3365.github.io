---
title: windows server
date: 2023-08-19 20:47:08
tags: windows
categories:	
---
# windows server

* 工作流程

1、装设备、装系统
2、设置用户、配ip、配端口
3、服务器管理器，开启【远程桌面，远程管理】，设置防火墙
4、测试，ping通，远程通
5、交付



## 业务操作

### 配置远程桌面

* 流程
  * 服务器管理器，开启，远程桌面、远程管理，需要进入 防火墙

  * windows防火墙，入站规则，开启服务：
    * ---否则无法远程连接
      		远程桌面（tcp-in 用户模式）
          远程桌面（udp-in 用户模式）
    * ---否则无法ping通
      		核心网络诊断-icmp 回显请求（icmpv4-in） / 文件和打印机共享（回显请求-icmpv4-in）
          核心网络诊断-icmp 回显请求（icmpv4-in）



### 配置新ip

* 流程
  * 配置ip，修改默认端口号
  * 配置成功、ping成功、telnet成功、远程桌面成功


* 修改默认端口号，

  * 改成5位，22xxx或者33xxx

    > 1、注册表中，修改两处端口号【 PortNumber 】
    >
    > * 路径1：hkey_local_machine \ system \ currentcontrolset \ control \ terminal server \ wds \ rdpwd \ tds \ tcp
    >
    > * 路径2：hkey_local_machine \ system \ currentcontrolset \ control \ terminal server \ winstations \ rdp-tcp
    >
    > 2、防火墙中新建入站规则--端口号
    >
    > 3、服务，重新启动服务 【remot desktop services】 
    





### 多用户远程登录

* 同一时间，多个用户，用一个账号登录，比如A，B，C，D四台机器，同时使用administrator这个账户登录服务器

* 流程

  * 首先开启远程桌面、远程管理

  * 服务器与管理器 》管理 》添加角色和功能向导 》基于角色或基于功能的安装

  * 远程桌面服务 》远程桌面(会话)主机、远程桌面授权

  * 确认安装所选内容，重启服务器

    ![](https://s1.ax1x.com/2023/08/31/pPw7KkF.png)

  * **直接执行以下操作也可以**
  
  * 运行/cmd，输入【gpedit.msc】打开策略组
  
  * 计算机配置\管理模板\Windows 组件\远程桌面服务\远程桌面会话主机\连接
  
  * 将远程桌面服务的用户限制到单独的远程桌面会话，禁用
  
  * 限制连接的数量，启用，允许的RD最大连接数——修改
  
  * cmd，输入【gpupdate /force】刷新策略，使策略生效 





## bugs

* 无法telnet

  > 一、打开控制面板
  >
  > 二、点击打开启用或关闭Windows功能
  >
  > 三、找到telnet客户端，勾选打开



