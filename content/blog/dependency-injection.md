---
title: 依赖注入
date: '2012-09-11'
description:
categories:
- 技术
tags:
---

在移除Pebble的Spring安全模块之余，我不禁感叹起依赖注入来。我是在2009年接触到依赖注入的，当时主要是看了Spring的创始人Rod的一些文章，又结合了Google推出的Guice，深深为之所动。当时感觉这个依赖注入实在是太强大了，只要给定接口，相应的管理器就能根据具体配置返回实例，很方便。于是我开发了自己针对javax.inject的实现，并在项目里用了一段时间，可是效果却不好。总结下来，有以下的问题：
<ul>
	<li>针对接口的具体实现常常只有一个，直接使用Java创建对象的方式更容易；</li>
	<li>调试异常困难，特别是对参数sniff的逻辑和实例生命周期的管理，非常麻烦；</li>
	<li>延迟加载的成员，往往需要显示的以来DI框架对象，造成更多的以来问题；</li>
	<li>类和类之间的以来关系很乱，往往不知道先后顺序。</li>
</ul>
当然以上这些问题都可以通过一定的方法解决，但是维护的代价大过它本身解决的问题。移除依赖注入逻辑的过程也异常痛苦，感觉整个底层被重写了一般。好的框架在使用的时候应该毫无感觉，甚至能和应用本身融为一体。就目前而言，我用过的唯一符合这个标准的就剩下JAX-RS了，是我目前开发必用库之一。
