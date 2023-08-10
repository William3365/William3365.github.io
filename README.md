# William3365.github.io

## 技术栈
* hexo+githubpages+vercel
## 注意
* 常规的hexo+githubpages搭建方法，只是将public下的文件，所以hexo生成的博客文件这只会造成在git托管了博客页面，没有托管源码，不便于我们管理
  本站采用git分支进行管理，利用hexo默认部署的方式，再将blog部署在main分支上然后创建分支，对源码（md文件和其他源文件）进行管理。
  将源码分支下载到本地，并清空分支中的东西，然后将.git文件复制到hexo根目录，即可还是原来的操作，只需再加入git的操作
## 使用
hexo clean 清理
hexo new 文章名 新建
hexo g 生成页面
hexo s 运行
hexo d 上传部署  INFO  Deploy done: git 表示成功
然后git同步即可
