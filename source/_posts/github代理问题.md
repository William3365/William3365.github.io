---
title: github问题
date: 2023-08-10 13:22:49
tags:	git
categories:	
---

问题：
    * 在拉取、推送、克隆的时候常报错经常出现 Connection refused 的错误，大致有443错误、22错误
    ```
        常见git报错：

        1、Failed to connect to github.com port 443 after 21084 ms: Couldn‘t connect to serve

        2、ssh: connect to host github.com port 22: Connection timed out  （或者port 443）
        fatal: Could not read from remote repository.
    ```

分析：
    * 由于GitHub经常被墙，访问不方便。
  
    * 浏览器访问GitHub.com 网站是正常的，估计是域名解析被污染了
  
    * 这两个问题主要是因为连接github.com的22/443端口被拒绝了。
      ssh连接默认使用22端口，22不能用可以调整为443端口

解决：
    * 1、如使用的代理，则关闭代理，然后重新刷新DNS缓存，用cmd打开windows命令窗口，输入：
      `ipconfig/flushdns`

    * 2、改22端口为443端口
      * Git Bash窗口，`ssh -T git@github.com` 查看是否仍然报错
      * 若执行命令 `ssh -T -p 443 git@ssh.github.com` 后不再提示connection refused
      * 则说明改用443端口可行，输入 `vim ~/.ssh/config`
        ```
        Host github.com
          Hostname ssh.github.com
          Port 443
        ```
      * 重新执行 `ssh -T git@github.com` 
        显示 `Hi xxxxx! You've successfully authenticated, but GitHub does not provide shell access.`
        说明成功
      * ![](https://s1.ax1x.com/2023/08/25/pPNktxO.png)
    
    * 3、22、443端口都不能用了，但是网页访问github正常
      * 先刷新DNS，若是无效再进行下一步
      * 查看ssh.github.com这个域名对应的ip
        `https://ipaddress.com/website/ssh.github.com`
      * 查出ip后，测试ssh连接
        `ssh -T -p 443 git@140.82.114.36`
      *  显示 `Hi xxxxx! You've successfully authenticated, but GitHub does not provide shell access.`即成功
      *  输入 `vim ~/.ssh/config`
         ```
        只要将Hostname ssh.github.com换成ip地址140.82.114.36即可

         Host github.com
          Hostname 40.82.114.36
          Port 443
         ```
      *  大功告成  


        

