---
title: 弃用MiniTemplator
date: '2012-09-16'
description:
categories:
- 技术
tags:
- pebble
---

尝试使用<a href="http://www.source-code.biz/MiniTemplator/">MiniTemplator</a>来替代Pebble的JSP模板，发现有问题。因为Pebble允许主题自定制，所以模板可以使用的变量是相对自由的。但是MiniTemplator由于设计上的考虑，只提供简单变量，所以必须在模板生成的时候一次性将使用到的变量都注入才行。这违背了自定制主题可以自由使用变量的要求，因此觉得转向<a href="http://www.stringtemplate.org/">StringTemplate</a>再试试看。

补充：StringTemplate似乎也不是我想要的东西，看到形式化定义我就晕了。也许它真的很强大，可是我只是想要一个HTML模板引擎而已。看来，还是回到我喜爱的<a href="http://velocity.apache.org/">Velocity</a>算了。
