---
title: centos7
date: 2023-08-19 20:47:04
tags:	centos7
categories:	
---
## 注意

* 一般推荐**uefi**引导

* 安装完成，拔出U盘，重启进入bios将启动顺序恢复至原来的顺序，**无论安装什么系统，都要这样!!!**

  其实大多数设备拔U盘之后，读不到U盘，就直接从系统盘读了，但是有时多系统，多硬盘的话，最好设置下启动项

* > * sata模式： stata AHCI （一般选择它，兼容模式）    # 如果需要做Raid，选择raid模式
  > *  write cache enabled 启用
  > * 引导模式：UEFI（推荐）



## 常用命令

重启：reboot
查看驱动器：ls /dev/sd*
详细信息：blkid

## 配置静态ip

  * centos7
  
      > * vim /etc/sysconfig/network-scripts/ifcfg-XX（网卡名）
      >
      >   ```
      >   tips：
      >   1、新装系统，没有vim，用vi（vim兼容vi）
      >   vi /etc/sysconfig/network-scripts/ifcfg-XX（网卡名）
      >   ```
      >
      > * 修改
      >   ```
      >   BOOTPROTO=static   # 网卡的引导协议：DHCP动态、static或none静态
      >   ONBOOT=yes #开机启动时是否激活网卡设备 #centos7装完网卡后默认no
      >   ```
      >
      > * 添加
      >   ```
      >   IPADDR=192.168.88.139  #ip地址
      >   NETMASK=255.255.255.0  #子网掩码
      >   GATEWAY=192.168.88.2	#网关
      >   DNS1=192.169.88.2	#dns
      >   ```
      >
      > * 重启网卡
      >
      >   ```
      >   systemctl  restart  network  
      >   或  service network restart    # 老版本
      >   ```
      >
      >   


## 安装MySQL
* 1、更新yum资源包
  `sudo yum update`
* 2、下载MySQL 8的仓库文件
  `sudo wget https://dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm`
* 3、安装MySQL 8的仓库文件
  `sudo yum install mysql80-community-release-el7-3.noarch.rpm`
* 4、导入MySQL GPG密钥
  `sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022`
* 5、安装MySQL数据库服务器
  `sudo yum install mysql-community-server`
* 6、安装完成后，启动MySQL并配置开机自启动
  ```
    systemctl start mysqld # 启动
    systemctl enable mysqld # 开机自启

    MySQL安装完成后，会自动配置为名称叫做：mysqld的服务，可以被systemctl所管理
    检查MySQL的运行状态：systemctl status mysqld
    查看是否开机自启动：systemctl is-enabled mysqld
  ```

* 7、获取MySQL的初始密码
  ```
    grep 'temporary password' /var/log/mysqld.log
    或者：cat /var/log/mysqld.log
  ```


* 8、登录MySQL
    `mysql -uroot -p`

* 9、修改密码
    ```
    ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '密码';


    tips：
      **配置简单密码，必须先按照规则，修改一个密码，然后才可以配置简单密码，**
      例：
      ALTER USER 'root'@'localhost' IDENTIFIED BY 'ROOT_root_12';   # 符合要求的密码

      # 修改密码校验规则
      set global validate_password.policy=0;  # 密码安全级别低
      set global validate_password.length=1;  # 密码长度最低1位
      # 设置简单密码
      ALTER USER 'root'@'localhost' IDENTIFIED BY '000000';
      ALTER USER 'root'@'localhost' IDENTIFIED BY 'admin@123';
    ```


* 10、允许root远程
    默认情况下，root用户是不运行远程登录的，只允许在MySQL所在的Linux服务器登陆MySQL系统

    设置root远程登录，并配置远程密码使用如下SQL命令
    * `create user 'root'@'%' IDENTIFIED WITH mysql_native_password BY '密码!';`
* 11、检查端口
    MySQL默认绑定了3306端口，可以通过端口占用检查MySQL的网络状态
   * `netstat -anp | grep 3306`


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
