---
title: Controller迁移
date: '2012-10-11'
description:
categories:
- 技术
tags:
- pebble
---

在迁移了部分JSP至VM（如首页、博客属性、创建文章等）之后，我开始准备改造Controller和Action映射部分的模块，以引入REST框架。Pebble是标准的MVC架构，每个页面对应一个Action模块，页面转换通过DefaultHttpController来进行，页面通过Action获得数据然后通过JSP按照模板来生成，而且支持主题。

从MVC转到REST是有些困难的。我做的项目里，后台部分使用REST将领域模型暴露成Web服务，为前台控件提供各种数据，而应用本身的用户交互和状态变化，则完全依靠HTML＋CSS＋JS来完成，并不需要后台参与。即使是用了VM，也只是为了Dojo框架提供一些全球化参数而已。把基于MVC的Pebble完全打散，使用REST＋页面的方法是我的Vision，但在目前阶段来说，困难过大，毕竟要重新理解和设计领域对象，还要把多个页面整合成单页面应用，对于一个业余项目来说，风险太大了。于是我尝试了一些渐进的改动方法。

首先是把DefaultHttpController用JAX－RS的资源类改写。将原本的Servlet改写成资源类还是比较简单的，逻辑基本没什么变化。但是Controller作为动作映射的模块，未免有些过于简单，也没有利用到REST的URL路由功能，所以准备拿些Action模块继续尝试。

REST＋VM的组合我是使用过的。在曾经一个Wiki项目里，我写过一个资源类，根据给定的路径载入相应的页面，动态的转换后，加载Wiki页面框架后返回。Pebble的设计有些类似，每个Action会根据博客的实际属性，声称一个视图，每个视图（原来是JSP，现在是VM）根据Action给的数据，填充并返回最终HTML页面。所以我也就仿照这个做法，创建了一个Blog的资源类：
<pre>@Path("/blog")
public class Blog {
  @GET
  @Path("/pages/{pageName}")
  public View page(@PathParam("pageName") String pageName) {
    ...
  }

  @GET
  @Path("/entries/page/{page}")
  public View entriesByPage(@PathParam("page") int page) {
    ...
  }

  ...
}</pre>
因为是渐进的改动，所以每个方法基本上都返回了Pebble原来自己的视图对象。当然我也提供了相应的ViewWriter（实现MessageBodyWriter接口）来渲染这些视图。

至此就完成了Controller和Action模块的改动设计，接下来就是体力活了。不过困难也是有的，还需要将认证和Pebble的安全令牌机制通过Servlet过滤器来实现，同时MultiBlog的概念也要相应保留。不管怎么说，距离我自己的博客系统又进了一步。
