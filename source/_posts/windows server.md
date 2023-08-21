---
title: windows server
date: 2023-08-19 20:47:08
tags: windows
categories:	
---
工作流程
1、装设备、装系统
2、设置用户、配ip、配端口
3、服务器管理器，开启【远程桌面，远程管理】，设置防火墙
4、测试，ping通，远程通
5、交付

===》
1、tft电脑，test，远程桌面连接测试
2、测试机，登录把tft电脑顶掉，测试
3、测试通过
4、用一楼的电脑进行远程连接测试
tips：
1、服务器管理器，开启，远程桌面、远程管理


===》
1、测试配置新ip
	--配置成功、ping成功、远程桌面成功
tips：
1、windows防火墙，入站规则，
	开启：---否则无法远程连接
		远程桌面（tcp-in 用户模式）
		远程桌面（udp-in 用户模式）
	          ---否则无法ping通
		核心网络诊断-icmp 回显请求（icmpv4-in） / 文件和打印机共享（回显请求-icmpv4-in）
		核心网络诊断-icmp 回显请求（icmpv4-in）
===》
2、测试修改端口号，在注册表中修改的，改成22789。防火墙中配置，然后重启remot desktop service
	--配置成功、【telnet ip 端口（跳到空窗口）】成功、远程桌面成功
tips：
1、配置端口：
	注册表中，修改两处端口号PortNumber，
	（
		路径1：hkey_local_machine\system\currentcontrolset\control\terminal server\wds\rdpwd\tds\tcp
		路径2：hkey_local_machine\system\currentcontrolset\control\terminal server\winstations\rdp-tcp
	 ）
	服务，remot desktop services 重启
	防火墙中新建入站规则--端口号
