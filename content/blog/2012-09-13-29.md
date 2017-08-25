---
title: 怎么确定是Java代码是老的？
date: '2012-09-13'
description:
categories:
- 技术
tags:
---

所谓老，是说用早期的Java语法来写的代码。重构这类代码是比较痛苦的，常常IDE里大量的编译器警告，对于我这样的Purist来说简直是灾难。下面是我发现的一些“特征”：
<ol>
	<li>没有指定类型。很多代码为了兼容1.4特地不写类型，这是可以接受的。可是还有一些则是滥用Object类型，把Map当成C的Struct来用，改起来很麻烦。这类问题需要从OO的角度重新设计对象来取代原先的“全类型”map。</li>
	<li>喜欢Hashtable。HashMap照理说是1.2就出现的对象，怎么不如Hashtable流行呢？搞不懂。</li>
	<li>喜欢StringBuffer。这个不解释。</li>
	<li>单元测试喜欢设计复杂的TestCase体系。估计是受到jUnit3的影响吧？</li>
</ol>
&nbsp;
