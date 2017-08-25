---
title: GoLucene Week 8 Dev Status
date: '2013-07-28'
description:
categories:
- 技术
tags:
- golucene
- go
- lucene
---

It's the 8th week of GoLucene development. There are two major milestones:
1. Switch to Lucene 4.4 code base.
2. Fixed all compile errors.

It didn't take much effor to migrate existing code to 4.4 code base. But as the development continues, there could be major changes in search index read related logic in the coming Lucene releases. So it might delay the overall schedule. And I have been heavily using "stubbing" technique to avoid early migration of the code. Instead, I have planted lots of "panic" statement so in the future, I can do on-demand porting of the code. It also means that I will spend more effort in unit testing porting, since it's expected to meet more errors.

There are also some other findings.

###### Abstract class are ported into interface plus an impl struct.

After some trials, I found it more effective to represent abstract class with an interface and an partial impl struct. For example,

	abstract class AbstractClass {
		private int field;

		public abstract void methodA();

		public int methodB() {
			methodA();
			return field;
		}
	}

After it's ported into GoLucene, it would look like,

	type AbstractClass interface {
		methodA()
		methodB() int
	}

	type AbstractClassImpl struct {
		AbstractClass
		field int
	}

func (c *AbstractClassImpl) methodB() int {
	c.methodA()
	return c.field
}`

###### Remove an item from a slice
The best way is to use container/list which is actually a double ended queue (Deque) in Java. But it's also easy to remove an item from a slice. My way is,

	buf := make([]byte, 10)
	pos := 5 // remove item 6
	newBuf := make([]byte, 0, len(buf)-1)
	newBuf = append(newBuf, buf[0:pos])
	newBuf = append(newBuf, buf[pos+1:])
	buf = newBuf

###### About synchronized keyword
I hate to see synchronized keyword in Java. It also brings trouble in Go too. I have to use a sync.Mutex to Lock/Unlock in a method, to realize a synchronized environment.