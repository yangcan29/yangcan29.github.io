layout:     post
title:      hexo+gitee博客搭建成长之路
subtitle:   部署在gitee上的博客
date:       2020-03-24
author:     YC
header-img: img/post-bg-20200324.jpg
catalog: true
tags:
    - Blog
---
# 一、环境准备
## 1.Git
官方安装地址：[https://git-scm.com/downloads](https://git-scm.com/downloads)  
额，可能国外的网站访问比较慢，我下载了很多次都失败了，后来借了一个VPN才下载成功，我下载的是Windows64位的。安装基本都是默认和next，不过我习惯性改了安装路径，这都没关系。  
**确认是否成功**：在Windows自带的cmd或者刚刚装好的Git CMD里输入`git --version`，若出现Git版本号即安装成功。
## 2.nodejs
官方安装地址：[https://nodejs.org/en/](https://nodejs.org/en/)  
这个安装也很简单，一路默认就好，路径允许修改。  
**确认是否成功**：cmd里面输入`node -v`，若出现版本号即node安装成功。再输入`npm -v`，若出现版本号则npm安装成功。  
由于npm是国外的服务器，下载可能失败，所以我们更换淘宝的镜像源cnpm。在cmd里面输入以下指令：

```
npm install -g cnpm --registry=https://registry.npm.taobao.org

```
等待下载完毕，再输入`cnpm -v`，若出现版本号，则安装成功。
## 3.Hexo
现在我们可以用刚刚下载的cnpm下载Hexo了，在cmd里面输入以下指令并等待下载成功：
```
cnpm install -g hexo-cli
```
当然也可以用`npm install -g hexo`来下载hexo，可能不成功，但是多尝试失败了也没什么关系。  
**确认是否成功**：cmd里输入`hexo -v`，出现版本号则hexo安装成功。  
# 二、本地localhost浏览博客
## 初始化hexo
- 新建文件夹，我的是取名为“blog”，放在D盘。（新建的文件夹命名和路径都无所谓）
- 选中该`blog`文件夹右键选择Git Bash Here，打开Git Bash终端输入`hexo init`回车
- 耐心等待，一定要耐心等待，直到再次出现和刚打开Git Bash时的状态，类似下面的内容：
```
PAIGE@LAPTOP-B5A31ATB MINGW64 /d/blog
$
```
- 然后可以看到`blog`文件夹下出现如下内容：
![blog文件下内容](https://s1.ax1x.com/2020/03/24/8LMTkF.jpg)
- Git Bash中输入`hexo s`打开hexo服务器
![启动hexo](https://s1.ax1x.com/2020/03/24/8LQ2ND.jpg)
- 打开浏览器，输入`http://localhost:4000/`
![本地博客](https://s1.ax1x.com/2020/03/24/8LQxvn.jpg)
# 三、部署到gitee
如果没有码云，先注册，官网地址：[https://gitee.com/](https://gitee.com/)  
- 新建仓库
- 获取仓库地址为`https://gitee.com/huoshanmao/huoshanmao.git`
- 修改配置在`blog`文件夹里找到：`_config.yml`，记事本打开并修改默认

```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: ''
-------修改为以下代码，repo后面为刚刚获取的仓库地址------
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: https://gitee.com/huoshanmao/huoshanmao.git
  branch: master
```
- 选中该`blog`文件夹右键选择Git Bash Here，打开Git Bash终端输入`cnpm install hexo-deployer-git --save`或者`npm install hexo-deployer-git --save`回车
- 等待等待再等待，然后在Git Bash中输入`hexo d`回车，会弹出一个对话框，提示输入码云的账号密码，输入账号和密码
- 等待一会儿，查看本地的`blog`文件夹下会多一个`public`的文件夹,查看码云仓库里会多一些文件
- 打开pages服务，具体操作是：服务-----Gitee Pages-----启动。
- 等待一会儿就会出现：已开启 Gitee Pages 服务，网站地址： http://huoshanmao.gitee.io
- 浏览器中打开`http://huoshanmao.gitee.io`就可以看到和本地博客一样的内容啦~


参考博文：   
1.[Hexo-github搭建个人博客](https://blog.csdn.net/longlongqin/article/details/104643987)  
2.[Hexo+Gitee搭建个人博客](https://ouwen666.gitee.io/2020/01/29/Hexo+Gitee%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/)  
3.[基于Gitee+Hexo搭建个人博客](https://blog.csdn.net/cungudafa/article/details/104260494)  