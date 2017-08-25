---
title: SVG和Canvas
date: '2014-09-02'
description:
categories:
- 技术
tags:

---

最近项目上需要改动一个六边形的logo，查了下CSS，发现竟然是用CSS3的transform，转动:before和:after的边界和角度，配上上下边界生成的。为了改动这个边框的粗细，涉及到8个不同CSS规则的修改。想到六边形其实也可以用其他方式来实现，就查了下<a href="http://www.w3.org/TR/SVGTiny12/">SVG</a>和<a href="http://www.whatwg.org/specs/web-apps/current-work/">Canvas</a>的文档。这里要赞下SVG的文档，真的很方便。反倒是Canvas的文档，首先作为HTML5的一部分，查阅起来就很麻烦，而且API的分类也很奇怪，通篇没有什么例子可用。

实现出来的效果大概是下面这样的。注意因为<a href="https://github.com/jsbin/jsbin/issues/943">jsbin bug</a>的关系，Chrome可能无法访问.

<iframe src="http://jsbin.com/dayudo/1/embed?html,css,js,output" class="" id="" style="border: 1px solid rgb(170, 170, 170); width: 100%; min-height: 300px;"></iframe>

第一个是用CSS3实现的，缺点就是CSS规则复杂，而且要通过包装多个节点来正确定位。第二个是SVG，基本上三行搞定，和Canvas一样被当成单个对象，所以定位什么的很轻松。第三个是Canvas做的，16行JS也还算好，坑爹的是像素点的计算很复杂，不像SVG那样直观。不过SVG和Canvas在IE11下显示很怪，需要进一步调整。

总的来说，我最喜欢SVG的方案，代码量少，易于定位，而且支持的浏览器肯定比CSS3和HTML5的Canvas更多一些吧。