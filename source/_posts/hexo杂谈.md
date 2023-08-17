---
title: hexo杂谈
date: 2023-08-10 13:00:50
tags:
---
## 搭建

* 技术栈 hexo+githubpages+vercel

* 说明
  * 一般hexo+githubpages+vercel搭建，网上有很多教程，本文不做具体描述
  
    * 搭建`http://t.csdn.cn/T7e5I`
  
    * 优化`https://wdstql.github.io/2021/08/03/matery/`
  
  * 本文有以下个注意点：
    * 常规的hexo+githubpages搭建方法，只是将public下的文件，所以hexo生成的博客文件这只会造成在git托管了博客页面，没有托管源码，不便于我们管理
    * 本站采用git分支进行管理，利用hexo默认部署的方式，再将blog部署在main分支上然后创建分支，对源码（md文件和其他源文件）进行管理。
    * 将源码分支下载到本地，并清空分支中的东西，然后将.git文件复制到hexo根目录，即可还是原来的操作，只需再加入git的操作
  
  * 使用
  
    > hexo clean 清理
    > hexo new 文章名 新建
    > hexo g 生成页面
    > hexo s 运行
    > hexo d 上传部署  INFO  Deploy done: git 表示成功
    > 然后git同步即可
## 杂谈
* 重新安装hexo

  * 一般主题文件需要重新安装，因为主题文件也是一个git仓库
  * git clone https://github.com/blinkfox/hexo-theme-matery.git
  * 解决：删除主题文件夹中的.git文件夹，这样就可以将主题文件一起上传了

* 多平台部署-国内外分流
* 123
  
  