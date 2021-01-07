---
title: 搭建hexo博客三
description: 在前面博客中已经提到如何给文章增加阅读数，这次我们继续增加评论功能
keywords: hexo,静态博客,免费博客,熙文说
categories: 
- hexo
tags:
- hexo
- github
- blog
abbrlink: 2f7c508
---
## 前言
在前面博客中已经提到如何给文章增加阅读数，这次我们继续增加评论功能
<!--more-->

## 修改next配置文件_config.yml
找到valine,然后增加以下配置
```
valine:
  enable: true
  appid: AppID
  appkey: AppKey
  notify: false 
  verify: false 
  placeholder:  写评论！
  avatar: mm 
  guest_info: nick,mail,link 
  pageSize: 10 
  language: zh-cn
  visitor: true 
  comment_count: true 
```
AppID和AppKey可以在LeanCloud的应用设置界面找到
## 修改leancloud_visitors的配置
在之前我们配置阅读数时，配置了leancloud_visitors的enable的值为true。文档说明leancloud_visitors.enable不能和valine.enable同时为true,解决办法就是在valine配置visitor为true，同时将leancloud_visitors.enable设置为false
```
leancloud_visitors:
  enable: false
  app_id: AppID
  app_key: AppKey
  security: false
```

## 在LeanCloud的存储中增加Comment
在应用的数据配置界面,找到存储，然后点击创建class,并命名为Comment。过程如同前面博客中提到的创建Counter相似

# 部署
```
npm run build
npm run deploy
```
等部署完成后，去看看评论吧！！

# 欢迎关注作者公众号
![](https://gitee.com/xyzxiaoxi/picture/raw/master/2021-1-7/1610018774805-qrcode_for_gh_c467e04f3857_258.jpg)