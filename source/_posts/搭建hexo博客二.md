---
title: 搭建hexo博客二
description: 在前面博客中已经提到如何创建hexo博客。但有一个问题，就是有人查看你的文章，但你不知道有多少人阅读了。因此需要添加阅读数
keywords: hexo,静态博客,免费博客,熙文说
categories: 
- hexo
tags:
- hexo
- github
- blog
abbrlink: 40ab5305
---
## 前言
在前面博客中已经提到如何创建hexo博客。但有一个问题，就是有人查看你的文章，但你不知道有多少人阅读了。因此需要添加阅读数
<!--more-->

## 使用next主题
从网上搜索hexo 阅读数，都推荐使用next主题。因此我们安装next主题到themes目录下
```
git clone https://github.com/theme-next/hexo-theme-next themes/next
```

## 修改站点配置文件_config.yml
找到theme,然后将值改为next
```
theme: next
```
## 注册[LeanCloud](https://leancloud.cn)并创建应用，如图所示
![创建应用](/images/LeanCloud1.png)

## 创建Class
在应用的数据配置界面,找到存储，然后点击创建class,并命名为Counter如图所示
![创建应用](/images/LeanCloud2.jpg)

## AppID和AppKey
在应用的设置界面，找到应用Keys，将里面的AppID和AppKey拷出来。然后配置next的_config.yml,找到leancloud_visitors，修改配置以下。
注意 security设置为false,因为server_url配置为国内域名的，由于我们部署在github上，由于设置为true时，通不过编译
```
leancloud_visitors:
  enable: true
  app_id: AppID
  app_key: AppKey
  security: false
```
# 修改busuanzi_count配置
```
busuanzi_count:
  # count values only if the other configs are false
  enable: true
  # custom uv span for the whole site
  site_uv: true
  site_uv_header: <i class="fa fa-user"></i> 访问人数
  site_uv_footer: 人次 
  # # custom pv span for the whole site
  site_pv: true
  site_pv_header: <i class="fa fa-eye"></i> 总访问量
  site_pv_footer: 次 
  # custom pv span for one page only
  page_pv: false
  page_pv_header: <i class="fa fa-file-o"></i> 阅读
  page_pv_footer: 次 
```
# 部署
```
npm run build
npm run deploy
```
等部署完成后，去看看效果吧！！

# 欢迎关注作者公众号
![](https://gitee.com/xyzxiaoxi/picture/raw/master/2021-1-7/1610018774805-qrcode_for_gh_c467e04f3857_258.jpg)