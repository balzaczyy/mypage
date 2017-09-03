---
title: "MarkoJS第一次尝试"
date: 2017-09-03T15:53:54+08:00
---

（以下为了简洁省去所有JS后缀，反正都是JS就是了）

第一次听到Marko是在两年前，当时在公司做一个前端项目要用到NodeJS，而当时PaaS系统出来的默认Node栈里用的就是Marko。我当时正从Angular一代被废弃的阴影中恢复过来，准备转投React的怀抱，所以二话没说，直接把Marko干掉了。干掉前也免不了偷偷嘲讽一下Marko奇怪的语法，虽然JSX也不见得有多优雅。直到最近，又有人向我安利起Marko，一问四周，真的有团队在重度使用，而且听起来性能是个亮点。于是，就有了这次尝试。

Marko的首页除了`.com`略显突兀之外，基本没毛病。我一下子get到了它的点：

- 单文件组件
- 简洁的HTML语法

性能并不怎么吸引我。在我看来以性能为卖点的产品，最终都被不断下降的硬件成本和不断优化的软件平台打败了。工具支持也不算特点，应该说是一个框架的必备吧。

Marko的文档很多地方都有着React的影子，但是引导部分并没有React做得好，进入的太快，如果是新手的话，做完第一个例子就会迷失了吧。而后面大部头的类似JavaDoc的文档，也不如React的那些来的生动有趣。好在我是个老手，也很快能读完了。

> ProTip: 建议前端专精的同学，看看语法和组件两篇文章就够了。

Marko文档的作者特别喜欢上面这种专家提示，有些提示充分显示了Marko作者的设计思路，比如说鼓励单文件组件。但这种有些自high的感觉让我想起了前东家……

Marko自带了命令行工具和starter模版，对应到create-react-app这样的工具，如果说从页面和SSR支持的角度，则更像next.js。和同事聊起来，发现他们是直接作为中间件使用的，我则比较偏好社区的这类工具，不用自己再维护开发工具链。

在starter默认的模板里，我尝试了简介的HTML语法，确实很帅。

```marko
<!DOCTYPE html>
html
  head
    meta charset="utf-8"
    meta name="viewport" content="width=device-width"
    title
      include(input.title)
  body
    header
      img.logo src="./logo.png" alt="marko logo"
      h1
        include(input.title)
      nav.menu
        a href="/" -- home
        a href="/hello/routing" -- routes
        a href="/layouts" -- layouts
    div.content
      include(input.content)
```

随后我也把默认的color-picker应用做了一遍。在写工具JS的时候，我用了一个我自认为很自然的写法`import { colors as flatColors } from 'flat-colors'`，然而marko却报错说不认识import这个关键字。我知道这是一个新关键字，需要babel支持，于是我换了marko-starter-babel，还是不行。给社区留言，没人在六个小时里面回信。然后我找到了这个[issue/1](https://github.com/marko-js/marko-starter-babel/issues/1)，开了有三个月，没人理。难道Marko的作者不用新语法写JS么？倒也不是，在Marko的模板里面，调用JS模块的关键字就是import，说明他们是考虑过的，但是为什么不支持新的语法，我不知道了。

测试也让我有些坑爹，还记得那个单文件组件的ProTip么？测试竟然不能写在那个单文件里，那倒也罢了，那能像Go那样写在那个文件相同的目录里么？答案是可以，但是这个组件的源代码必须测试一起放在一个单独的目录里。于是，热心的我，给开了[Feature Request](https://github.com/marko-js/marko-cli/issues/53)，哈哈。

一切到这里还算顺利，有些坑，但也能应付得来，但接下来的事情让我彻底崩溃。我准备按照marko-starter的文档上进行构建，一般的serve-static和build都没有问题，但是带上production标签以后，生成的目录里没有任何CSS、JS或者资源文件。失望之余，我给starter开了一个[Bug Report](https://github.com/marko-js/marko-starter/issues/15)。

后记：其实原本我是打算尝试用`now.sh`来部署这个学习项目的，这里批评一下[now的安装文档](https://zeit.co/download)。首先，它为了推它的客户端，让我误以为必须安装它的客户端，还撞进GFW这个坑里。接下来那[四个大大图标](https://zeit.co/download#command-line)让我又一次误以为要下载那些命令行文件，而其实在那后面的不显眼的一样里，写着：

>You can also install it with npm as follows:
>
  ```
  npm install -g now
  ```

等以后再有机会尝试`now`吧。