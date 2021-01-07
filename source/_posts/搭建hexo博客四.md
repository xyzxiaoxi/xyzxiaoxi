---
title: 搭建hexo博客四
description: 在前面博客中已经提到如何给文章增加阅读数和评论功能，但是我们编辑的文章标题是中文名称的，这样导致了url乱码，修改标题后，url也变了，不利于搜索引擎收录。另外在对中文不友好的系统中，就解析不了url，比如IOS。我们使用abbrlink插件解决这个问题
keywords: hexo,静态博客,免费博客,熙文说
categories: 
- hexo
tags:
- hexo
- github
- blog
abbrlink: 4e25a916
---
## 前言
在前面博客中已经提到如何给文章增加阅读数和评论功能，但是我们编辑的文章标题是中文名称的，这样导致了url乱码，修改标题后，url也变了，不利于搜索引擎收录。另外在对中文不友好的系统中，就解析不了url，比如IOS。我们使用abbrlink插件解决这个问题
<!--more-->

## 安装abbrlink插件
```
npm install hexo-abbrlink --save
```

## 修改站点配置文件_config.yml
```
permalink: posts/:abbrlink.html
abbrlink:
    alg: crc32   #算法： crc16(default) and crc32
    rep: hex     #进制： dec(default) and hex
```

## 重新生成下
```
npm run build
```
生成完成后，可以看到原来md文件中会增加abbrlink 字段，值为生成的ID。这个字段确保了在我们修改了Front-matter 内的博客标题title或创建日期date字段之后而不会改变链接地址。
# 部署
```
npm run deploy
```
等部署完成后，去看看效果吧！！

# 欢迎关注作者公众号
![](https://gitee.com/xyzxiaoxi/picture/raw/master/2021-1-7/1610018774805-qrcode_for_gh_c467e04f3857_258.jpg)