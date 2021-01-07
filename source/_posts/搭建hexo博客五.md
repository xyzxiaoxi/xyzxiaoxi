---
title: 搭建hexo博客五
description: 给博客增加分类和标签
keywords: hexo,静态博客,免费博客,熙文说
categories:
  - hexo
tags:
  - hexo
  - github
  - blog
abbrlink: 53c7cb53
---
## 前言
给博客的文章增加分类和标签，便于查找和管理
<!--more-->

## 创建分类选项
```
hexo new page categories
```
成功后会提示：
```
INFO  Validating config
INFO  Created: ~\source\categories\index.md
```

打开index.md文件，并新增内容如下
```
type: "categories"
```

## 创建标签选项
```
hexo new page tags
```
成功后会提示：
```
INFO  Validating config
INFO  Created: ~\source\tags\index.md
```
打开index.md文件，并新增内容如下
```
type: "tags"
```

## 给文章增加标签和分类
打开需要添加标签的文章，为其添加tags属性和categories
```
categories: 
  - XXX
tags:
  - XXX
```

# 编译部署
```
npm run build
npm run deploy
```
等部署完成后，去看看效果吧！！

# 关闭标签页和分类页的评论
部署完成后，发现标签页和分类页出现了评论框，这是我所不想要的。
编辑tags的index.md文件，增加配置以下
```
comments: false
```
编辑categories的index.md文件，增加配置以下
```
comments: false
```
再次编译和部署，就可以发现标签页和分类页的评论没有了

# 欢迎关注作者公众号
![](https://gitee.com/xyzxiaoxi/picture/raw/master/2021-1-7/1610018774805-qrcode_for_gh_c467e04f3857_258.jpg)