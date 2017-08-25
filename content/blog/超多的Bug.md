---
title: 超多的Bug
date: '2014-08-26'
description:
categories:
- 技术
tags:

---

最近我开始了GoLucene中涉及解析器和符号流逻辑的移植。可能是前段时间的压力过大，竟然发现了许多原本不会出现的bug。这些bug也很有意思，症状和原因往往牛头不对马嘴，花了我很多的跟踪时间。要怪只能怪Go没有好的图形化单步调试工具，GDB什么的我暂时也没时间学，一条一条的状态打印让人那个捉急啊。

第一个错发生在GoLucene内部的一条断言上，说某个字段应该可以被索引，但是标志位不对。按说这个字段类型是个静态值，改改也就对了。但改完，发现另外一个断言又错了。仔细看代码，发现原来Lucene里面StringField和TextField里面分别由STORED和NOT_STOREF两个类型，而且各自的标志位都不一样。因为Go没有类级别的scope，所以这种类型名必须要加上类的名字作为前缀加以区别。大多数的时候是不需要加的，毕竟重名的不多，但还是被我碰上了。

第二个错也是一个断言发现的（感谢Lucene内部大量的断言）。先是StandardTokenizer无法正确的抽取符号，debug发现内部的input从来没有被赋过值，但是代码上是有赋值的。再仔细看，发现在StandardTokenizer的reset方法里面没有调用Tokenizer父类的reset方法。加上后就直接“TokenStream contract violation”断言，原来是参数和字段重名，忘记加上类名了，而且断言条件也写反了。

第三个错和整数类型有关。Go中的int很奇特，在64位运行时里是64位的（废话……）。平时也没什么问题，但是如果是带符号位位移（在Java里面是&gt;&gt;&gt;)，而且没有制定uint32的话，得出的结果就不正确。糟糕的是症状是数组下标越位，经过无数的反向跟踪，才发现是哈希函数里的带符号位位移错了，因为int是64位的。

第四个错是死循环，而且还挺典型的。在Java里面有段代码

	main:
	while (off &lt;= limit) {
	    // ...
	    while (true) {
	        if (off &gt;= matchLimit) {
	            break main;
	        // do something
	    }
	    // ...
	}

在Go里面我写成了

	for offset &lt;= limit {
	    // ...
	    var hasMore bool
	    for hasMore = offset &lt; matchLimit; hasMore; offset++ {
	        // do something forever now
	    }
	    if !hasMore {
	        break
	    }
	    // ...
	}

因为我忘记重新计算hasMore标志了……其实只要协程下面这样就好了。

	for offset &lt;= limit {
	    // ...
	    var hasMore = offset &lt; matchLimit
	    for hasMore {
	        // do someting
	        offset++
	        hasMore = offset &lt; matchLimit
	    }
	    if !hasMore {
	        break
	    }
	    // ...
	}

第五个错也很典型。Go的类继承通过对象嵌入实现，当需要虚类来传值的时候，我一般会选择抽出一个interface加一个中间对象。但在这个bug中，我选择了使用虚类，然后用一个Value字段表示实际的对象。

	指针 -> 基础类 { 基础字段, Value -> 实际类 { 基础类指针, 其他字段 } }


这是一种挺tricky的解法，比较适合中间抽象类只有一层的情况。使用的时候经常需要做类型转换，比如说ptr.Value.(*ConcreteClass).concreteValue等等。容易出问题的就是初始化的时候，没有把类似双链表的指针指对。症状其实一点也看不出是这个问题，总是报排序错误，但实际上是FreqPostingsPostingsArray这个类没有正确的指向基础虚类，造成基础字段修改的值，没有得到更新，永远是空值。

最后一个错也和整数类型有关。要记住，Go的byte是0到255，所以千万不要以为两个byte相减会出现负数。

移植中最痛苦的就是修bug了。