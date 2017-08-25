---
title: 利用Coveralls收集测试覆盖率
date: '2014-10-14'
description:
categories:
- 技术
tags:

---

好吧，我承认有些盲目跟风了。那天我浏览github的时候，看到三个很好看的badge，构建状态、覆盖率和文档链接，于是我决定把这三个badge也要放到我的项目里面去。Travis是相对简单的，做一个配置，等着build的通知就可以了。文档也也就是一个link的问题。最麻烦的是测试覆盖率，因为数据必须从构建中获取，而Coveralls没有官方的Travis接口或者Go客户端的支持。

最后我使用的是[goveralls](https://github.com/mattn/goveralls)（Coveralls的Go客户端实现）配合一个[脚本](https://github.com/sdboyer/gogl/blob/master/test-coverage.sh)来合并不同package的测试结果，勉强得到结果。

最终的效果并不是理想，免费的Coveralls只能给出很简单的行覆盖率，邮件通知也要额外配置（并且configure按钮会在没有提醒的情况下冲掉已经输入的信息……），邮件的内容也显得比较苍白。