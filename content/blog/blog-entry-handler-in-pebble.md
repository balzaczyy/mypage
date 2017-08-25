---
title: Pebble解析 － BlogEntry的事件处理
date: '2012-11-16'
description:
categories:
- 技术
tags:
- pebble
---

在实现WP的PostDAO的时候遇到了一个情况。为了决定是做一个从Post到BlogEntry的适配器，还是转换器，我看了BlogEntry的源代码。Pebble的BlogEntry继承于PageBasedContent和Content，设计上使用了很多JavaEE的方法（毕竟Pebble本来就是JavaEE的博客系统），其中最有意思的是在Content这个类上同时使用了Bean的PropertyChangeSupport工具类以及Pebble自己的事件处理。

<a href="http://zhouyiyan.cn/blog/wp-content/uploads/2012/11/content1.png"><img class="alignnone size-full wp-image-137" title="content" src="http://zhouyiyan.cn/blog/wp-content/uploads/2012/11/content1.png" alt="" width="600" height="171" /></a>

&nbsp;

<a href="http://docs.oracle.com/javase/6/docs/api/java/beans/PropertyChangeSupport.html">PropertyChangeSupport</a>的作用主要是收集字段值的变化，方法也相当的土，在每个子类修改属性的时候加一段代码：
<pre>public void setValue(String newValue) {
  String oldValue = this.value;
  this.value = newValue;
  this.pcs.firePropertyChange("value", oldValue, newValue);
}</pre>
而最终这些属性变化的事件集会统一在更新BlogEntry的时候以Pebble标准的事件被重新插入BlogEntry里，并通过Pebble的EventDispatcher来触发响应的监听器，这其中包括对BlogEntry添加、删除和修改所引发的簿记工作，以及响应衍生数据的变化。

事件监听和触发是一个很棒的设计，围绕在基本的核心系统周围，给现有的系统带来近乎无限的可扩展性，如同ServletFilter给Servlet带来的影响一般。只是目前Pebble的这种实现方式还是有些怪，毕竟平白增加了这么多需要理解的方法。
