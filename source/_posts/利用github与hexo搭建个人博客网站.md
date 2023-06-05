---
title: 利用github与hexo搭建个人博客网站
date: 2023-03-19 20:24:44
categories: 
- 建站
tags: 
- github
- hexo
---

本文主要介绍如何通过github和hexo框架，不购买服务器资源实现部署个人博客

<!--more-->



## 一、安装nodejs

可在git命令行通过以下命令检查本地是否安装了nodejs和npm

```bash
$ node -v
$ npm -v
```

出现以下内容说明已安装，如果未安装，可以通过[官网](https://nodejs.org/en/) 提供的安装工具自行安装。

![image-20230224231949776](https://freezer712.oss-cn-hangzhou.aliyuncs.com/blog-img/image-20230224231949776.png)



## 二、安装和初始化hexo

1. 使用如下命令安装hexo

```bash
$ npm install hexo-cli -g
```

（如果npm速度较慢可以换国内源）

2. 初始化hexo

```bash
$ hexo init
$ npm install
```

3. 本地运行

```bash
$ hexo clean
$ hexo g
$ hexo s
```

如果出现提示`ERROR Try running: 'rm -rf node_modules && npm install --force'`，运行该命令，运行完成后重新运行上述命令

出现以下结果，表示运行正常，可在浏览器中访问给定网址，按"ctrl+c"可停止本地运行

![image-20230224233040783](https://freezer712.oss-cn-hangzhou.aliyuncs.com/blog-img/image-20230224233040783.png)

页面内容如下

![image-20230224233353905](https://freezer712.oss-cn-hangzhou.aliyuncs.com/blog-img/image-20230224233353905.png)



## 三、创建github仓库并上传代码

1. 登录[github](github.com), 点击右上角"+"，选择"new repository"，按如下内容创建仓库

![image-20230224233938038](https://freezer712.oss-cn-hangzhou.aliyuncs.com/blog-img/image-20230224233938038.png)

2. 安装hexo-deployer-git

   ```bash
   $ npm install hexo-deployer-git --save
   ```
   

   
3. 修改本地hexo目录下_config.yml文件，将最底下

   ```
   deploy:
     type: ''
   ```

   修改为

   ```yaml
   deploy:
     type:git
     repository:https://github.com/freezer712/freezer712.github.io.git
     branch:main
   ```

   

4. 创建仓库后，在本地hexo目录下用git命令行执行以下命令上传代码（如果未配置ssh可使用personal access token来push代码，获取流程可参考<a id="token">[token获取方法](#token)</a> 

```
#初始化本地仓库
git init
#添加远程git地址，jevonk是我的gitlab用户名
git remote add origin https://github.com/freezer712/freezer712.github.io.git
#添加需要管理文件
git add .
#提交内容
git commit  -m "init"
#修改默认分支名master为main
git branch -m master main
#强行推送到远程, 注意可能遇到主分支是受保护的，无法推送。自行百度处理
git push -f origin main

```

（使用token时）弹出下面界面可直接cancel

![image-20230225000325295](https://freezer712.oss-cn-hangzhou.aliyuncs.com/blog-img/image-20230225000325295.png)

依次弹出如下页面，输入github网站用户名和**token**

![image-20230225000454714](https://freezer712.oss-cn-hangzhou.aliyuncs.com/blog-img/image-20230225000454714.png)

![image-20230225000444761](https://freezer712.oss-cn-hangzhou.aliyuncs.com/blog-img/image-20230225000444761.png)

出现下图内容表示代码已经push到github仓库

![image-20230225001057788](https://freezer712.oss-cn-hangzhou.aliyuncs.com/blog-img/image-20230225001057788.png)

![image-20230225001133409](https://freezer712.oss-cn-hangzhou.aliyuncs.com/blog-img/image-20230225001133409.png)



## 四、在本地写博客并发布

1. 创建博客

```bash
#该命令会创建一片名为"first blog"的博客，在/source/_posts目录下生成一个"first-blog.md"文件，可以将已写好博客替换进去
$ hexo new "first blog"

```

2. 生成静态文件

   ```bash
   #清理缓存文件，是一个比较常用的命令
   $ hexo clean
   # 重新生成文件
   $ hexo g
   ```

3. 本地运行(访问http://localhost:4000/， 使用Ctrl+C关闭)

   ```bash
   #本地运行查看效果
   $ hexo s
   ```

4. 上传

   ```bash
   # 上传
   $ hexo d
   ```









## Utils



<a id="token">token获取方法</a>

1. github网站点击右上角头像，点击settings

![image-20230224235114197](https://freezer712.oss-cn-hangzhou.aliyuncs.com/blog-img/image-20230224235114197.png)

2. 左边栏最底下点击"Developer settings"， 点击"Personal access tokens",，点击"Tokens(classic)", 页面右上部点击"Generate new token", "Generate new token(classic)",按下图填入信息![image-20230224235628699](https://freezer712.oss-cn-hangzhou.aliyuncs.com/blog-img/image-20230224235628699.png)

点击"generate token"，即可获取token（请注意保存，不会再显示）

![image-20230224235844994](https://freezer712.oss-cn-hangzhou.aliyuncs.com/blog-img/image-20230224235844994.png)

[点我快速返回！](#token_back)