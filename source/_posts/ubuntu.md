---
title: Ubuntu
date: 2023-08-30 17:36:56
tags: Ubuntu
---

### 安装系统

* UEFI + GPT

* 制作U盘启动盘的时候，官网下载的是混合镜像，可以iso加载，可以dd加载，推荐iso

  

### 用户

* Ubantu默认禁止使用root用户，登录的是普通用户，要么切root，要么sudo，大多数命令都要带sudo

  > 登录之后是普通用户，设置root密码
  >
  > `sudo passwd root ` 



### 安装软件

*  `apt`
  * centos  `yum`



### 配置静态ip

> * ip a   # 查看 网卡
>
> *  cd /etc/netplan 
>
> * ls   # 查看.yaml文件
>
> * sudo vi yaml文件     # 用文本编辑器打开
>
> * 编辑
>
>   ```
>   yaml对格式、缩进有严格要求！！！
>   
>   网卡名
>      dhcp4: false    # 动态改成false
>         addresses: [192.168.3.86/24]   # 前面是ip地址，24对应的子网掩码是255.255.255.0
>         gateway4: 192.168.3.1    # 网关
>         nameservers:
>           addresses: [192.168.3.1]   # DNS
>   ```
>
> * 退出vi文本编辑器
>
> *  sudo netplan apply  # 保存
>
> 



