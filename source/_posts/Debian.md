# Debian

* 版本选择指南：

  * 我认为官网弄得很乱，不明晰

  * 进入官网下载页面，默认下载当前最新稳定版，按需选择其他发行版本

  * 选择了对应版，页面上

    * 【安装信息】进入下载界面
    * 【安装指南】进入查看安装手册

  * 按需选择镜像介质、系统架构

    * amd64就是64位

    * 建议离线安装、选择DVD介质

      

## 安装流程

**建议断网离线安装，有些插件补丁下载需要外网，卡、慢**



* 安装程序选项

  * **Graphical install 图形化安装（更友好）**

    教程 `http://www.360doc.com/content/20/1217/02/11770334_951926947.shtml`

  * install 文字安装

    教程 `https://www.cnblogs.com/qinfangzhe/p/15915788.html`

* 选择系统语言、位置时区、键盘

  * 系统语言、键盘都选择 **English**，选择中文容易出现乱码

* 配置网络

  * 暂时不进行网络设置
  * 网络**主机名**，默认debian
  * 网络域名，可以不写

* 设置用户、密码

  * 设置 **root管理员账户** 密码

  * 设置普通账户、密码

  * debian**默认**以普通用户登录，不能以root用户登录，可以登录之后再切换

    > 修改默认设置，允许root登录
    >
    > --
    >
    > 首先确定ssh服务是否正在运行，是否开机自启    `systemctl status ssh`
    >
    > 修改配置文件  `vi /etc/ssh/sshd_config `
    >
    > 1. `PermitRootLogin yes    去掉注释符# ，修改为yes`
    > 2. `PermitEmptyPasswords yes     去掉注释符# ，修改为yes`  ，允许设置简单密码（可选）
    > 3. `systemctl restart ssh    重启 SSH 服务`

    

* 磁盘设置

  * 选择磁盘分区模式
    * guided引导程序自动分区，简单起见，选择整个引导磁盘 guided-use entire disk (可按需选择)
    * manual手动分区
  * 选择要分区的磁盘
  * 选择磁盘分区方案，简单起见，默认方案 All files in one partition (recommended for new users)
  * 安装程序显示磁盘配置、检查分区，无误就 finsh 继续，yes确认写入，有误就 undo 撤销

* 完成基本安装

* 是否扫描CD或DVD光盘安装其他的软件，选择 no

  * 基于最小安装原则，后续缺什么再装什么

* 选择包管理源、镜像源

* 软件安装

  * SSH、standard system utilities（必备，最小化安装）

* 将boot GRUD引导文件写入硬盘

  * install the grub boot loader on a hard disk，选择 yes
  * 选择对应 硬盘

* 安装完成重启系统



## 配置ip

> 查看网卡信息     ip a
>
> 查看原来的配置信息   cat   /etc/network/interfaces
>
> 修改配置文件     vi  /etc/network/interfaces
>
> ```
> auto 网卡名                 # 网卡自启动 
> iface 网卡名 inet static    # 改为static
> address 192.168.1.183
> netmask 255.255.255.0
> gateway 192.168.1.1
> dns-nameservers xxxxxxxx      # dns还需要在配置另一处
> ```
>
> 重启网卡  systemctl restart networking，    不生效直接重启系统，（进行到这一步，一般可以ping通外网IP，但是还不支持域名解析）
>
> 修改dns配置文件   vi   /etc/resolv.conf 
>
> ```
> search loacl    # 自动解析local域
> nameserver xxxxxxxx    # 可以写一个也可以写多个，另起一行 nameserver xxxxxxxx
> ```
>
> 重启系统，刷新网卡    reboot      测试ping baidu.com
>
> 

​              