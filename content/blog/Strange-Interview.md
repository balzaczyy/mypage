---
title: 变了味的面试
date: '2013-10-23'
description:
categories:
- 工作

---

我一直不是很擅长面试，特别是在白板上写代码，难道他们假设程序员一天到晚是在白板上工作的么？还有些变了味的面试，记得有一次，遇到一个字符串分割逆序的问题，我使用了Java的字符串split和StringBuilder的方法，大概是这样的

	String[] words = str.split("\\s");
	for (int i = 0; i < words.length; i ++) {
		Stack stack = new Stack();
		for (int j = 0; j < words[i].length(); j ++) {
			stack.push(words[i].charAt(j));
		}
		StringBuilder builder = new StringBuilder(words[i].length());
		while (!stack.isEmpty()) {
			builder.append(stack.pop());
		}
		words[i] = builder.toString();
	}
	return StringUtils.join(words, " ");

面试官当时也没说什么，也没有让我做任何改进，我也只是稍稍解释了下这种方法的不足，应该换成stream操作，配合逆序迭代器，可以实现更高效率的方法。面试的结果相当不好，一开始我不能理解，怎么我这么强的人会被拒。后来google了才知道，妈的，原来你要[这个解法](http://blog.csdn.net/bingxx11/article/details/7802461)啊？！补充一下，“这个解法"是指不需要额外stack的原地交换方法。

只能说我自叹弗如了……我还是做回我自己的黑客吧，不跟他们玩了。