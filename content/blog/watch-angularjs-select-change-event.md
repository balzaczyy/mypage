---
title: 监视AngularJS的select控件
date: '2014-11-18'
description:
categories:
- 技术
tags:

---

今天遇到了一个棘手的问题，AngularJS的select控件不响应watch方法。HTML代码如下

	<select ng-model="currentInstance" ng-options="opt for opt in opts">

JS代码如下

	$scope.$watch('currentInstance', function(currentInstance) {
		// do something
	});

调试了很多时间，watch的方法除了初始化的时候调用两次之外，再也没被调用过。前几次谷歌都没有得到很好的解法，最后尝试了一个组合，得到了[这个答案](http://stackoverflow.com/questions/17536751/angularjs-updating-ngmodel-property-when-select-options-change)，顺利解决问题。基本解法是把currentInstance替换成一个对象的字段，HTML代码如下

	<select ng-model="choice.selectedId" ng-options="opt for opt in opts">

JS代码如下

	$scope.choice = {};
	$scope.$watch('choice.selectedId', function(currentInstance) {
		// do something
	});


不过这个答案并没有说明原因，官方文档表示ng-model是按引用比较，我尝试了字符串，发现也没有办法触发watch。在该问题的另一个答案中，提到在AngularJS里面，scope不应该作为模型的根，而是应该创建单独的对象，我估计这很可能和这个问题真正的root cause有关，不过也无从验证了。