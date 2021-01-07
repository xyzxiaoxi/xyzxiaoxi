---
title: 搭建hexo博客六
description: 博客SEO化
keywords: hexo,静态博客,免费博客,熙文说
categories:
  - hexo
tags:
  - hexo
  - github
  - blog
  - SEO
abbrlink: 55de0350
---
## 前言
之前的文章我们有说到搜索引擎收录博客文章，要想搜索引擎收录文章，就必须做好SEO
<!--more-->

## 添加sitemap
首先先安装两个模块
```
npm install hexo-generator-sitemap --save #sitemap.xml适合提交给谷歌搜素引擎
npm install hexo-generator-baidu-sitemap --save #baidusitemap.xml适合提交百度搜索引擎
```
然后在站点的_config.xml中添加以下配置
```
# 自动生成sitemap
sitemap:
  path: sitemap.xml
  baidusitemap:
  path: baidusitemap.xml
```
最后修改站点配置文件_config.yml
```
# URL
url: http://XXX.XX.XX //一般这样格式
```
然后运行
```
npm run build
```
你就会发现在/public目录下生成sitemap.xml和baidusitemap.xml，这就是你的站点地图。

## 创建robots.txt文件
在source文件夹中新建文件robots.txt,内容如下
```
# hexo robots.txt
User-agent: * Allow: /
Allow: /archives/
Disallow: /vendors/
Disallow: /js/
Disallow: /css/
Disallow: /fonts/
Disallow: /vendors/
Disallow: /fancybox/

Sitemap: https://XXX.XXX.XXX/sitemap.xml //XXX.XXX.XXX 是你的域名
Sitemap: https://XXX.XXX.XXX/baidusitemap.xml
```

## 注册百度搜索资源平台
[百度搜索资源平台](https://ziyuan.baidu.com/)，在平台上注册后，将你的网站提交后，验证网站。
百度提供三种验证方式，建议选择CNAME验证.


# 主动给百度提交文章链接
我们博客是部署在Github，它禁止百度爬虫访问博客，导致博客无法被百度收录。因此我们主动提交文章链接给百度。首先安装模块
```
npm install hexo-baidu-url-submit --save
```
然后在站点配置文件-config.yml文件中，增加以下配置
```
baidu_url_submit:
  count: 1 ## 提交最新的一个链接
  host: XXX.XXX.XXX ## 在百度站长平台中注册的域名
  token: your_token ## 请注意这是您的秘钥， 所以请不要把博客源代码发布在公众仓库里!
  path: baidu_urls.txt ## 文本文档的地址， 新链接会保存在此文本文档里
```
然后修改deploy选项
```
deploy:
  - type: git
    repo: https://github.com/test/test.github.io.git
    branch: master
  - type: baidu_url_submitter
```
# 编译部署
```
npm run build
npm run deploy
```
等部署完成后，去看看效果吧！！

# 欢迎关注作者公众号
![](https://gitee.com/xyzxiaoxi/picture/raw/master/2021-1-7/1610018774805-qrcode_for_gh_c467e04f3857_258.jpg)