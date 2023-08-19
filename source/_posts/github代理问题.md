---
title: github代理问题
date: 2023-08-10 13:22:49
tags:	git
categories:	
---
* 443问题
因为使用clash进行互联网活动，所以有时打开github会有报错，比如在拉取、推送、克隆的时候常报错。
  
`git报错：Failed to connect to github.com port 443 after 21084 ms: Couldn‘t connect to serve`

解决办法：
直接关闭代理，然后重新刷新DNS缓存，用cmd打开windows命令窗口，输入：
`ipconfig/flushdns`

* 22问题
  ```
   ssh: connect to host github.com port 22: Connection timed out
   fatal: Could not read from remote repository.

   这个错误提示的是连接github.com的22端口被拒绝了。
   
   解决办法：
   1、使用443
   ssh -T git@github.com。还是报错
   执行命令ssh -T -p 443 git@ssh.github.com 后不再提示connection refused
   在git branch中进行
        vim ~/.ssh/config
        
        Host github.com
          Hostname ssh.github.com
          Port 443

        ssh -T git@github.com
        Hi xxxxx! You've successfully authenticated, but GitHub does not provide shell access. 成功
  ```
