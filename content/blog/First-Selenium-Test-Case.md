---
title: First Selenium Test Case
date: '2014-03-20'
description:
categories:
- 技术

---

今天终于完成了人生第一个基于Selenium的UI自动化测试脚本（本想说是第一次UI自动化，但突然想起来我也曾经用RFT写过WebSphere产品中帮助模块的自动化测试滴）。话说Selenium真是个坑啊，花了我整整两天时间，才把各种问题一一解决掉。我用的是[WebdriverJS](https://github.com/camme/webdriverjs)和Mocha。

1. 弃用官方driver。官方的[WebDriverJS](https://code.google.com/p/selenium/wiki/WebDriverJs)文档不齐全，查个API还要google下用法。而且对像我这种从静态语言转过来的开发来说，官方driver中倡导的的promise和defer用法，简直就是天书。哪里要嵌套，哪里可以连续写，没有个准数。后来我切换到了非官方的，一律统一使用flow的写法，简单明了。
2. 避免页面切换。我要测试的应用本来是个单页面应用，可是要测试的功能涉及到登录操作。由于认证采用的是oauth加回调，有两次页面切换。本来Selenium是提供了隐式等待的功能，可是实际测试运行的时候，总是出现各种随机的错误。最后，把认证方式切换到简单post之后，问题便解决了。
3. 为测试显示隐藏元素。有些功能，比如说hover-to-display，利用了浏览器hover改变CSS的特性，Selenium是不支持的。我尝试了moveToObject和scroll命令，都没有办法对隐藏元素进行hover操作。最后，我直接修改了CSS，把display: none去掉以后，就可以了。
4. 利用CSS3选择器。用Selenium之前，总是听说元素定位如何如何困难，什么Dojo都是动态ID，什么复杂的XPath等等。真正使用以后，发现CSS3选择器已经够用了。比如说下面这个，用来定位app-container下app类，同时是第二个元素，下的名字，真心方便。

		#app-container .app:nth-child(2) .name

俗话说，不以测试通过为目的的开发都是耍流氓。有了Selenium以后，妈妈再也不用担心我乱改代码了。