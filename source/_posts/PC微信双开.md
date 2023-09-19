---
title: PC微信双开
date: 
tags: 工具类
---


# PC微信双开

* 首先新建一个txt文件

  ```
  TASKKILL /F  /IM wechat.exe
  start "" "xxxx\WeChat.exe"
  start "" "xxxx\WeChat.exe"
  
  # 把xxxx改成wechat.exe的路径
  ```
* 保存文件，将txt文件改成后缀为bat

* 退出微信，使微信打开是扫码界面。然后关闭微信
* 双击bat文件，打开了两个扫码登录的界面，然后正常登录