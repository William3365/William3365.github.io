---
title: hexo杂谈
date: 2023-08-19 20:22:11
tags:	hexo
categories:
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
    > hexo new xxx 新建文章，hexo new page xxx  新建页面
    > hexo g 生成页面
    > hexo s 运行
    > hexo d 上传部署  INFO  Deploy done: git 表示成功
    > 然后git同步即可

## 其他问题
### 配置admin后台管理系统
    * 不用再md文件里直接写，可以避免很多语法、格式问题
      ```
      安装：npm install --save hexo-admin
      运行：hexo server -d
      地址：http://localhost:4000/admin/
      ```
    * 添加用户名密码
      ```
      根目录_config.yml
      
      admin:
      username://用户名
      password_hash://用户名密码不喜欢的可以不设置，这里通过bcrypt hash
      secret: hey hexo deploy//用以cookies安全；
      Command: 
      ```


### 重新安装hexo

  * 一般主题文件需要重新安装，因为主题文件也是一个git仓库
  * git clone https://github.com/blinkfox/hexo-theme-matery.git
  * 解决：删除主题文件夹中的.git文件夹，这样就可以将主题文件一起上传了

### 多平台部署-国内外分流
  * 采用github、gitee，流程差不多，需要注意的是，GitHub可以自动更新，gitee需手动
  * 书写格式，网上教程很多也很旧，自己多写试试
  * 协议最好一致，要么都是https，要么都是ssh
  * 分支最好也一致
    ```
    deploy:
    type: git 
    repo:
        github: git@github.com
        gitee: git@gitee.com
    branch: master
    ```
  
### 本地运行预览正常，部署上线无效果
  * 可能是浏览器缓存问题，ctrl+F5，强制刷新
  * 可能是分支问题，尤其是的两个特殊点，1本案例采用的部署一个分支，源码一个分支的方式，2本案例双平台部署存在自动和手动问题。更要注意比如GitHub是main分支，gitee是master分支，这里提供思路就是去比较分支的提交和活跃，就知道代码被提交到哪里了，再看部署选择的是哪一个分支
  
  