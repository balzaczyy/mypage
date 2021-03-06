---
title: 懒是一种美德
date: '2015-10-14'
description:
categories:
- 工作

tags:

---

看到oschina上的一篇文章（[懒Redis是更好的Redis](http://www.oschina.net/translate/lazy-redis-is-better-redis)）颇有些感受，简单来说是把原本时间复杂度高的Redis命令用异步的方式完成了，中间还尝试过延迟、增量、数据结构优化等操作。延迟或者异步，这种非阻塞的方式，对于资源释放来说是一种很好的方法，虽然并没有实际提高系统吞吐量，但能够显著提高系统响应，对于用户来说，系统感觉变快了。在实际工作中我也遇到过类似的应用，比如说在云环境中，为了提高资源利用率而进行的scale down，机器升级或者迁移，都涉及释放计算资源。资源释放并不是简单的操作，牵涉到很多设备和配置的改动。原先释放一个虚拟机资源的可能需要十几分钟，后来采用异步的方式，先禁用该虚拟机，然后放进一个池子里，如果需要，可以根据需求选择并重新启用，超过一段时间后再后台释放。采用异步的方法后，资源释放非常快，几乎是瞬间完成，而且成功率很高，即使有错误也可以后台忽略或者修复。当然这种方法在分层系统中，和下游系统自身的缓存机制如何结合也是很巧妙的，处理不当会造成资源浪费。

这让我想起曾经拼命搞专利的那段时间，一些看似简单的工程化方法，运用在不同的场合和领域，往往能解决原本非常棘手的问题。

另外最近比较累，显然没有从之前的旅行疲劳中恢复，加上新的突发事件，感觉很不顺。