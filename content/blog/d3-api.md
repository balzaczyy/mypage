---
title: 获得暗黑3人物信息
date: '2012-09-05'
description:
categories:
- 技术
tags:
- diablo3
- jquery
---

老实说，我很久没玩暗黑3了。但是闲来无事想学习一下jQuery插件的写法，就挑了暗黑3的社区API来练练手。整个过程很顺利，推荐JS新手都可以玩一下。

首先是暗黑3的API：http://us.battle.net/api/d3/profile/battlename-tag/。其中battlename-tag其实就是包含数字的战网名中，把#替换成-而已。返回的JSON对象基本构成是：

<code>{
"heroes": [
{
"name": "Yharr",
"id": 1,
"level": 60,
"class": "Wizard",
...
},
...
],
"lastHeroPlayed": 3,
...
}</code>

其中lastHeroPlayed对应的是Hero的ID。其他参数请详见<a title="官方API文档" href="http://blizzard.github.com/d3-api-docs/" target="_blank">官方API文档</a>。获得Hero对象后，作为JS新手，我傻傻的输出了三行基本数据，代码如下：

<code>$this.append('&lt;span&gt;Hero: &lt;/span&gt;&lt;span&gt;' + hero.name + '&lt;/span&gt;&lt;br&gt;'
+ '&lt;span&gt;Level: &lt;/span&gt;&lt;span&gt;' + hero.level + '&lt;/span&gt;&lt;br&gt;'
+ '&lt;span&gt;Class: &lt;/span&gt;&lt;span&gt;' + hero.class + '&lt;/span&gt;');</code>

因为过于简单，所以不解释，直接看<a href="https://github.com/balzaczyy/d3profile" target="_blank">代码</a>。接下来想试试Wordpress的插件。
