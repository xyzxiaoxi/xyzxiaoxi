---
title: 搭建hexo博客
description: 这是一篇在github上搭建hexo博客指南
date: '2020-11-10'
keywords: hexo,静态博客,免费博客,熙文说
categories: 
- hexo
tags:
- hexo
- github
- blog
abbrlink: 8e88d59c
---
## 前言
使用github pages服务搭建博客的好处有：  
1.全是静态文件，访问速度快  
2.免费，不需要花一分钱就可以搭建一个博客  
3.SEO化，让搜索引擎收录你的网站，让别人更容易搜索到你  
4.使用hexo的命令让你更容易打包、发布  
5.使用github的版本管理，让你想用哪个历史版本都可以
<!--more-->

### 本文依赖的环境  
Windows10  
node.js@12.16.1  
git@1.9.2  
hexo@5.2.0  

### 准备工作
* 有一个github账号，没有的话去注册一个；
* 安装了git for windows（或者其它git客户端）
* 安装node,nvm,nrm,hexo等(自行了解相关知道)

## 使用hexo创建一个博客
安装hexo完成后，请执行下列命令,hexo将会在指定文件夹中新建所需要的文件。
```
hexo init demo   
cd demo  
npm install
npm run build
```

然后运行命令 hexo server启动服务器，默认情况下，访问网址为： http://localhost:4000/

## 创建github仓库
新建一个名为你的(用户名).github.io的仓库，比如说，如果你的github用户名是test，那么你就新建test.github.io的仓库（必须是你的用户名，其它名称无效），将来你的网站访问地址就是 https://test.github.io

创建完成后，找到设置，找到GitHub Pages选项，将source设置为master,folder选择root,点击保存

## 修复_config.yml文件
找到Deployment下的deploy添加以下配置
```
type: git  
repo: https://github.com/test/test.github.io.git  
branch: master 
```

## 安装hexo-deployer-git模块
```
npm i hexo-deployer-git --save
```
## 将刚刚创建的hexo部署到github上
```
npm rum deploy
```
然后打开 https://test.github.io 就可以看到效果了

# 欢迎关注作者公众号
![](https://gitee.com/xyzxiaoxi/picture/raw/master/2021-1-7/1610018774805-qrcode_for_gh_c467e04f3857_258.jpg)