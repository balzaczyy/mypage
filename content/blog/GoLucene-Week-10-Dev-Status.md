---
title: GoLucene Week 10 Dev Status
date: '2013-08-13'
description:
categories:
- 技术
tags:
- golucene
- go
- lucene
---

Since the migration of the basic flow is done, with a few places that would throws a panic, I have been focusing on fixing defects in the last two weeks. Some basic changes include:

1. Rewritten IndexReader and IndexReaderContext using AbstractClass pattern.
2. Added a testcase to verify basic full-text search function.
3. Added tons of logs to accelerate troubleshooting.
4. Fixed various issues related to SegmentFileName functions, AbstractClass pattern, DataInput, etc.
5. Implemented SlicedIndexInput.
6. Relocated FSDirectory/FSIndexInput code to fs.go.

There are also some new findings.

###### Interface null check

It's a little surprised for me to find out that interface can not do nil check. According to this [post](http://stackoverflow.com/questions/13476349/check-for-nil-and-nil-interface-in-go), interface variable consists of a type and pointer value, so it can never be nil. Those who relies on nil check would be very disappointed. One example is Commons-IO's IOUtils.CloseQuitely(...).

###### Nil pointer method invoke

I'm very surprised to see that even nil pointer can invoke its struct method. I would expect NPE but apparently it's not the case in Go. I have to test for nil inside methods that may have nil pointer received.

###### Byte range
Java's byte is [-128, 127], while Go's byte is [0, 255]. So don't test if byte is GE 0 because it's always true. Test if it's GE 128 instead.

###### Clone
Java has a very interesting Clone() method. It's much harder to do so in Go. There is still a TODO item to fix such problem.