---
title: Firefox and Eclipse
date: '2006-12-15'
description:
categories:
- 技术

---
Eclipse是一个成熟的、精心设计的以及可扩展的体系结构，也是迄今为止最成功、最受开发者欢迎的的开发框架。通过插件扩展，Eclipse能够成为完成各种功能的桌面应用程序。作为同样成功的、以插件扩展功能成名的软件，Firefox也是浏览器领域的佼佼者。从Firefox诞生起，插件和扩展架构便成为FF最引人注目的技术，而XUL更是让FF雄霸了各个OS平台。如今，各种FF扩展让FF不仅是一个浏览器，也能完成许多桌面应用。

Eclipse和Firefox越来越通用了。但是谁更强一些？

毫无疑问，Eclipse的架构是其引以为豪的资本，Eclipse甚至能够实现RCP浏览器。但是SWT和Java的效率让人不敢恭维，号称解决垃圾回收的Java并没有解决内存消耗的问题，交互速度也随着插件的增多和快速下降。如果Eclipse的RCP崩溃了，只能看到Java抛出的异常，保存的机会都没有，难怪Eclipse要自动保存和编译。

丰富的Web应用让Firefox大展拳脚，直接在Firefox上面就能完成修改网页和察看的功能。但是XUL和脚本扩展是其软肋，跨平台的代价是效率，常常用着用着就没响应了。扩展如果装多了，速度也会受到很明显的影响。

两者的效率都很难恭维，因此K-Meleon的非XUL实现以及控制Eclipse插件效率的机制都很让人期待，毕竟对于应用来说，用户体验很重要。

[FF的一些缺点](http://forums.mozine.org/lofiversion/index.php/t5022-50.html)对基础概念介绍的比较全，如XUL和FF4Win的调用方式
[为Eclipse实现FF的简单扩展方式](http://mea-bloga.blogspot.com/2006/10/what-eclipse-can-learn-from-firefox.html)