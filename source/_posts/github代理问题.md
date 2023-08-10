---
title: github代理问题
date: 2023-08-10 13:22:49
tags:
---

因为使用clash进行互联网活动，所以有时打开github会有报错，比如在拉取、推送、克隆的时候常报错。
  
`git报错：Failed to connect to github.com port 443 after 21084 ms: Couldn‘t connect to serve`

解决办法：
直接关闭代理，然后重新刷新DNS缓存，用cmd打开windows命令窗口，输入：
`ipconfig/flushdns`