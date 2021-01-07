---
title: webscraper 入门到精通
description: 学习webscraper
keywords: webscraper,爬虫,熙文说
categories:
  - crawler
tags:
  - crawler
  - chrome
abbrlink: fb84304c
---
## 前言
如果你想爬一个网站内容，大家都想到用python或者其它语言写一个爬虫程序去抓取内容。但这涉及到熟悉语言或各种库、模块等。
有没有简单的方法呢？有，今天介绍的webscraper就非常方便。
首先，它是chrome的一个插件，安装就能用，如果不能翻墙，可以通过https://crxdl.com/这个网站来搜索安装。
其次，只有你熟悉dom结构，就可以随意抓取内容了
最主要的是，这个插件可视化。也就是抓取的内容有没有抓取成功，一眼就可以看到
本文默认你已安装了webscraper，如果不会，可以百度下chrome插件安装
<!--more-->

## 实战
### 抓取豆瓣上的电影《姜子牙》影评
《姜子牙》影评的地址 https://movie.douban.com/subject/25907124/reviews
第一步：打开网址，按F12进入开发者工具，将开发者工具调到浏览器下方,如下图
![开发者工具](/images/webscraper/1.png)

第二步：找到webscraper,点击进去。找到Create new sitemap,点击Create Sitemap,如下图
![添加站点](/images/webscraper/2.png)
给你要爬的网页取个名字,我这里的名字是douban-jangziya,将《姜子牙》影评的地址填入Start URL

第三步：点击刚刚创建的站点，可以看到以下界面
![添加站点](/images/webscraper/3.jpg)

第四步：点击Add new selector,增加以下配置
![添加元素配置](/images/webscraper/4.png)
Element表示元素，id随便取，我这里取的test,只要你理解就行
Selector表示你要选择的元素，这里为什么是.review-item呢？用chrome的select element工具看一下就明白了，如下图
![选择网页上的元素](/images/webscraper/5.png)
整个评论块都包含在.review-item这个样式下面
Multiple表示选择多个记录。从两个或多个选中 multiple 的选择器中提取的数据不会合并到一个单独记录中；

第五步：点击test进去,然后点击Add new selector。这表示从test这个元素中获取内容
如我要获取头像，点击Selector的Select,然后把鼠标放到头像上，这个时候插件会帮我们自动选择元素，然后我们只要点击Done selecting就可以了，如图
![选取头像](/images/webscraper/6.png)
同理，我们可以用同样的方法，获取昵称，影评时间等等

第六步：获取详情的影评内容
如果有的影评内容太长，就只会显示一部分，其它的截断了。我们根据标题点进去看了。我们要抓取详情内容怎么做呢
首先，我们在test下面创建标题选择器，如图所示
![选取标题](/images/webscraper/7.png)
然后我们点进commentTitle选择器，然后点击Add new selector，选择Link类型的，如图所示
![选取Link](/images/webscraper/8.png)
最后我们点击进入影评详情页，然后点击进入linkTitle选择器，点击Add new selector，选择Text类型的，如图所示
![选取详情](/images/webscraper/9.png)
在详情页，我们可以看到整个影评者在div.review-content下。如图
![详情内容](/images/webscraper/10.png)

第七步：运行
点击Sitemap douban-jangziya,选择Scrape,如图
![Scrape](/images/webscraper/11.png)
![start Scrape](/images/webscraper/12.jpg)

第八步：查看数据和导出数据
等插件运行完成，会出现如下图界面
![refresh](/images/webscraper/13.png)
点击refresh,出现如下图界面
![爬虫数据](/images/webscraper/14.png)
然后我们可以点击Exprot data as csv,如图
![导出数据](/images/webscraper/15.png)
我们点击download now就可以把数据导出了

# 欢迎关注作者公众号
![](https://gitee.com/xyzxiaoxi/picture/raw/master/2021-1-7/1610018774805-qrcode_for_gh_c467e04f3857_258.jpg)