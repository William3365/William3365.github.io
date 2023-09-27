---
title: PVE
date: 2023-09-25 09:19:54
tags:	Linux
categories:	
---

# PVE

* 背景：

  一般练习可以使用VMware，练习一些windows、centos、Ubuntu单机操作。在我练习集群化部署的时候，劣势显现出来，物理机上先装windows server，再装vmware，然后部署虚拟机。影响效率和性能不说，主要是组网、配置也不方便。所以选择PVE服务器虚拟化平台，直接在物理机上安装PVE，在此基础之上部署多台虚拟机，和原来的比较，pve系统相当于win系统，省去了一个vmware，可以更好的发挥性能，也更便于部署一些中间件，更便于运维监控。
  
  

## 简介

* Proxmox Virtual Environment，通常简称为 PVE、Proxmox、Proxmox VE。是一个开源的服务器虚拟化环境 Linux 发行版。PVE 基于 Debian，使用基于 Ubuntu 的定制内核，包含安装程序、web控制台和cli工具

* pve就是一个linux系统，在此之上创建多个虚拟机，使用web控制台管理



## 命令

* 开、关、状态 ： `qm start / stop / status  VMid`
* 查询：`qm list`
  * 虚拟机关不上`ps -ef|grep "/usr/bin/kvm -id VMid"|grep -v grep`，查看进程id
  * 关闭`kill 进程id`



## 主机名配置

### 主机名配置

> hostnamectl     # 查看主机名
>
>  hostnamectl set-hostname XXX    # 配置主机名



### 主机名映射

* 1、Windows，管理员打开记事本、打开 C:\Windows\System32\drivers\etc，修改hosts文件

  ```
  ip 主机名
  192.168.88.131 node1
  192.168.88.132 node2
  192.168.88.133 node3
  ```
  
* 2、每一台linux机器都要配置 修改`/etc/hosts` 文件，和上边一样
  
  
  
  * 浏览器ip:8006、主机名:8006都能访问web控制台，shell远程工具可以ip、主机名访问。说明主机映射配置成功，奇怪啊，Windows配完就直接能访问了？我的理解，因为我的电脑和pve平台都在同一局域网，所以在我这配完就能访问了
  * 本机认识pve、node123
  * pve不认识 node123
  * node1不认识node2-------下周配置linux的host，这周把ssh互相登录解决（目前仅仅是pve单向登录node123，node123还没双向相互复制），建议先配置host再ssh

## SSH配置

* SSH服务是一种用于远程登录的安全认证协议。

  * 远程某台机器，生成了密钥，本地要想ssh连接，1，将ssh复制给这台机器自己，2，需把ssh下载到本地，并配置到远程工具中

    * 或者：本地先用这种方法连node1，然后node1把公钥复制给node2、3、4，再相互复制，这样不仅node1234可以互相登录，本机还可以利用一个公钥登录所有，即利用node1公钥登录noe1234

    

  

* SSH服务支持多种认证方式：

1. 口令：账户+密码

2. 密钥：账户+秘钥文件

3. keyboard  Interactive  服务器发给你信息然后你手动输入信息发回

   

   我们通过FinalShell远程连接到Linux，就是使用的SSH服务。（windows登录linux）

   

* 生成密钥

  * `ssh-keygen -t rsa -b 4096`  一路回车到底即可

    > -t rsa
    >
    > ​	-t，指定密钥的类型，密钥的类型有两种，RSA，DSA，
    >
    > -b 4096
    >
    > ​	-b，指定密钥长度，密钥长度为4096位

    > C:\Users\用户\.ssh
    >
    > .ssh文件夹
    >
    > * known_hosts   记录ssh访问过计算机的公钥（public key）
    >
    > * id_rsa    生成的私钥
    >
    > * id_rsa.pub   生成的公钥
    >
    > * authorized_keys    存放授权过的无密登录服务器公钥

* 复制密钥

  * `ssh-copy-id 远程主机`

    > 将本地生成的SSH公钥复制到远程主机
    >
    > 
    >
    > 想要互相登录，就要互相复制
    >
    > 建议先配置主机映射，再弄ssh，否则
    >
    > 优：ssh node1
    >
    > 坏：ssh 192.168.3.89



* SSH可以让我们通过SSH命令，远程的登陆到其它的主机上，比如：
  * 在node1执行：`ssh root@node2`，将以root用户登录node2服务器，输入密码即可成功登陆
  * 或者`ssh node2`，将以当前用户直接登陆到node2服务器。

* 退出登录
  * exit
  * ctrl +d



#### SSH免密配置

集群化部署，多数需要远程登录以及远程执行命令，简单起见，配置服务器之间的免密码互相SSH登陆，比如三台机器，node1、node2、node3

1. 在每一台机器都执行：`ssh-keygen -t rsa -b 4096`，一路回车到底即可

2. 在每一台机器都执行：

   ```
    ssh-copy-id node1
    ssh-copy-id node2
    ssh-copy-id 192.168.3.66
    
    
    # 此步骤前提是已经配置完了主机映射关系,否则就要像第三行那样
   ```

3. 执行完毕后，node1、node2、node3之间将完成root用户之间的免密互通







