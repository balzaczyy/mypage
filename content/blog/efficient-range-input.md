---
title: 高效的Range Input在Android浏览器下的替代方法
date: '2012-09-02'
description:
categories:
- 技术

---
最近业余时间利用个人的一些专业资源，在做一个个税筹划的小工具，其中需要用户输入一些数字。我首先想到的就是HTML5新引入的Range Input，可是查了[相关资料](http://caniuse.com/input-range)觉得这个控件的支持不是很理想。尽管也有一些跨浏览器的[jQuery插件](http://jquerytools.org/documentation/rangeinput/index.html)可以用，可是Android的默认浏览器却并不支持。又看了jQuery Mobile和jqTouch，虽然也有相应的控件，但是在Android默认浏览器上的性能实在是太差了，于是不得不寻求其他的方法。

受到优酷Android应用的启发，发现Scrollable DIV应该会在Android浏览器上表现不俗，可能是浏览器实现有相应优化的关系，配合scroll参数和简单的JS代码，可以完全替换所需的Range Input。比如下面这段代码：
	
	<span id="salary"></span>
	<div id="salary_sel" style="overflow-x: auto">
	  <img style="max-width: 2474px; height: 200px;" src="img/sunset.jpg" />
	</div>
   
	<script>
	$("#salary_sel").scroll(function(){
 	  $("#salary").text(this.scrollLeft);
	});
	</script>

配合上一张长背景图片（注：这里使用的是我在若尔盖草原拍的落日）就可以达到滑动输入的效果。鉴于没找到如何在新浪博客里使用JS的方法（注2013/11/14：MarkDown也不支持JS），所以并没有显示所拖动的位置。

<span id="salary"></span>
<div id="salary_sel" style="overflow-x: auto">
  <img STYLE="max-width: 2474px; height: 200px;" src="{{urls.media}}/sunset.jpg" />
</div>
<script>
$("#salary_sel").scroll(function() {
  $("#salary").text(this.scrollLeft);
});
</script>

下面也比较一下HTML5原生的Range Input在Android浏览器上的效果（苹果用户请忽略）：

<input type="range" name="test" min="100" max="300" value="150"></input>

就拖动输入而言，使用Scrollable DIV会比原生的Range Input控件快很多。如果是要做跨浏览器的滑动输入的话，不失为一个好的替代方案。