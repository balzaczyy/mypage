---
title: 研究Pebble
date: '2012-09-09'
description:
categories:
- 技术
tags:
- pebble
---

考虑到实验室里做的信息中心，从本质上来说也和CMS系统类似，所以决定研究下开源的项目，顺便汲取一些思路。为了不过分打击自己，就先从博客系统入手，挑了Roller和Pebble，最后选择了代码量稍小的Pebble。

首先从官网上下载了2011年发布的<a href="http://prdownloads.sourceforge.net/pebble/pebble-2.6.2.zip?download">2.6.2</a>，导入了我新建的<a href="https://github.com/balzaczyy/pebble-clone">pebble-clone</a>项目。然后加上jetty-maven-plugin，指定版本为7.0.1.v20091125。接着利用"mvn eclipse:eclipse"创建了Eclipse项目的配置文件，并把pebble.tld移到了WEB-INF目录下。上面这步很重要，为了避免适应Struts的API变化，以及避免m2e插件的不足而导致的错误，用“mvn jetty:run”看下启动是否正常。一切ok后，最后用Eclipse导入生成的项目，大功告成。

Pebble从代码量上来说和我做的项目相当，功能上要更加丰富，而我的项目主要还是初级阶段，以应付T级数据和每天百万级访问量为首要目标。从包的组织上，Pebble也比较类似，相对于Roller的明显的插件结构，Pebble则更加Java一些。使用的技术也基本和EE符合，Spring+Struts+JAXB的技术栈也没有什么大问题。Lucene的使用让我对它多少有些好感，毕竟我也做了好几年搜索了。Ant的使用让我有些疑惑，需要更加深入的理解。除此之外，Pebble似乎还自己开发了一套和Struts相适应的框架，难道是我看错了？

&nbsp;
