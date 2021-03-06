---
title: 减少前台代码单元测试的尝试
date: '2014-10-21'
description:
categories:
- 想法
tags:

---

从后台转到前台开发后，经常困扰我的就是单元测试了。前台真的很难做单元测试，一方面没有很好的工具，另一方面需求的变化让维护单元测试成为一种负担。而且，在修复问题的时候，单元测试也没有做到保护和易于运行。对于后台来说，运行整个系统是很困难的，所以单元测试成了小规模验证变更的最佳工具。而到了前台，运行系统的界面反倒是相对容易的，而且设计的改良，使得任何操作的重现步骤都不会特别复杂。

单元测试对于前台开发还是必要的，但是如何控制投入产出比呢？

- 首先服务层是不用单元测试的，这个后台开发人员应该已经测试过。
- 界面的特性开发也可以不用单元测试，毕竟过几天说不定这个特性就已经不在了。
- 重复的功能缺陷可以用简单的单元测试，避免再次反复。
- 浏览器兼容性问题最好抽成自己的框架，避免重复犯错。

这样下来要写的单元测试就少很多了。不过如果单元测试完全不要写就好了，毕竟学习相应的测试工具也要花时间的。有什么更好的方法么？