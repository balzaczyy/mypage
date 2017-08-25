---
title: RAM Usage Estimator
date: '2014-03-28'
description:
categories:
- 技术
tags:
- Lucene

---

有一个大坑正在展开。Lucene有自己的JVM内存占用估算机制，用来估算在生成索引时的内存使用情况。基本的算法在RamUsageEstimator这个类里面，其它和生成索引相关的类中，也分别有各种记录内存使用的计数器。有些直接使用简单的整数类型，有些则是AtomicInteger，在ByteBlockPool和IntBlockPool的使用者中，则主要使用Counter。至于内存估算如何影响索引的生成，这个机制暂时还没有遇到，不过我估计和平衡CPU/IO的算法有关。

麻烦的是，RamUsageEstimator的算法不能简单移植到Go。比如说Go的复合数据类型可以直接使用简单数据，比如说map可以直接用int来做键和值，而Java则需要一个对象封装一下；Go的Slice可以通过cap来得到预留的空间数量，而Java则必须估算成2X等等。