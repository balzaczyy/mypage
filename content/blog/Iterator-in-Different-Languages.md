---
title: 不同语言的迭代器
date: '2013-10-18'
description:
categories:
- 技术
tags:
- Ruby

---

最近在通过《七周七语言》快速学习Ruby，目前是第二天。Ruby真的很适合做原型开发，特别是那种需要在白板上写写画画的情况，如果直接用Ruby的话，写的人方便，看的人也理解的快。最令我惊讶的就是Ruby的代码块了。
	
	[1..16].collect {|x| x * 2}

这不就是Scala里面map吗？

	List.range(1, 16).map((x) => x*2)

当然继承自Lisp的Clojure更加简单，但更难懂。

	(map #(* 2 %) (range 1 16))

所以从精简程度上，Ruby和Lisp系是比较接近的，而且形式上，以及和面向对象的角度上，都是更易于理解的。