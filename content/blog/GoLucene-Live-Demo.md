---
title: 寻找哈姆雷特
date: '2014-10-07'
description:
categories:
- 技术
tags:

---

GoLucene的开发终于告一段落了，基本的创建索引、查询解析和搜索都已经完成。为了能实际演示现有的功能，增加些知名度，同时收集一些查询解析的实际用例，我利用职务之便，做了一个[网站](http://hamlet.mybluemix.net/)。这个网站的功能还挺简单的，它索引了莎士比亚的一个剧本，哈姆雷特，通过关键字可以查询剧本原文。网站的布局采用了[AMUI](http://amazeui.org/)的CSS框架，Go写的后端，部署在[Bluemix](https://ace.ng.bluemix.net/)上面。值得注意的是，Bluemix虽然没有Go的运行时，但是可以通过[CloudFoundry官方的buildpack](https://github.com/cloudfoundry/go-buildpack)来提交部署，需要定义启动命令即可。

回想起来，距离移植工作开始也超过一年了，期间因为工作的关系陆陆续续地中断了几个月，不过先在也算是到里程碑了。接下来如果没有实际的项目需要，基本上只需要紧跟Lucene的发布脚步就可以了。