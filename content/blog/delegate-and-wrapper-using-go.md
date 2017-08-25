---
title: Delegate and Wrapper using Go
date: '2013-12-17'
description:
categories:
- 技术
tags:
- Go

---
Lucene的测试套件中有很多封装现有对象，并提供额外控制，如节流、锁检测和关闭检测等功能。这些类一般使用Delegate的封装形式，实现以恶服务接口，给定一个内部对象做实际的工作，同时添加一些额外的功能。这种写法通常都十分啰嗦，特别是有很多方法的接口，会出现大量类似的无用代码：

	public void method1(...) {
	  delegate.method1(...);
	}
	
	public void method2(...) {
	  delegate.method2(...);
	}

事实上，新的类所扩展的功能可能就只是涉及到一两个方法而已。为了解决这种问题，一般可以再创建一个中间wrapper，把每个方法都交给delegate，然后再让扩展的类去覆盖一两个方法就好了。当然，这样就又创建了一个新的无用对象。

在Go当中，如果要实现Delegate这种封装形式，可以直接使用嵌入对象。事实上，Delegate本身就[源自基于原型的面向对象](http://en.wikipedia.org/wiki/Delegation_(programming))，所以使用类似机制的Go可以相对简单的实现这种需求。

	type extendedClass struct {
	  *parentObject
	}

只要这三行，就可以使扩展类无缝的使用父类的方法，就好像继承了一样。如果要扩展某几个方法，就只要相应的实现这些方法就可以了。当然这也存在一些问题：

1. 缺少delegate关键字，对代码理解会有些影响。不过如果Go代码看多了，也会习惯的。
2. 多个delegate对象会比较乱。
3. 如果包含的是接口，那么涉及到内部字段访问的方法会比较困难。

使用了这个方法以后，从Lucene测试套件转换过来的Go代码精简了至少一半。

关于Delegate和封装的模式可以看[这里](http://patterns.instantinterfaces.nl/current/Refactoring-and-Design-Patterns-WRIA-REL.html)。