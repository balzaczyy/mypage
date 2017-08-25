---
title: 用CSS制作简单的logo水印
date: '2014-08-17'
description:
categories:
- 技术
tags:

---

最近部门要办一个Bluemix和CloudFoundry的推广月活动，我应邀在第一周做一个讲座介绍Bluemix和CF命令行的使用。为了让讲座更炫一些，我照例又试用了一个新的slide工具<a href="http://imakewebthings.com/deck.js/">deck.js</a>。具体的ppt等我做完讲座再放出，这里要分享的是一个logo水印的制作方法。

在公司内部做讲座，常用到的ppt首页一般都有一个大大的公司logo（用来填补首页的空白……）。为了体现我们的团队，我特地把logo换成了我们的团队名称。为了制作这个logo水印，我尝试了office的艺术字和Paint.NET(PS不懂），效果都不太好。想起来自己也算是个前台开发人员（囧），就试着用CSS做了一个，期间遇到无数的问题，一一用谷歌解决。代码如下：

	.watermark {
	  font-size: 15em;
	  -webkit-transform: rotate(-30deg);
	  position: absolute;
	  right: 0;
	  bottom: 0;
	  opacity: 0.4;
	  margin-right: -5%;    
	  margin-bottom: -5%;
	}

什么，你没看到这里的水印？请务必留言给我。

<div class="watermark">ACE</dev>