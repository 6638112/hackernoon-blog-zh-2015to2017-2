# 您可能需要 jQuery

> 原文：<https://medium.com/hackernoon/you-might-need-jquery-5b6c0c757e61>

![](img/09e7d8fe4ba3ecb3eb24866c11170986.png)

jQuery 创建于遥远的 2006 年。当时，这对许多开发人员来说是一个巨大的时间节省。jQuery 解决了许多令人讨厌的跨浏览器问题，是每个新项目中事实上的库。

今天，浏览器每天都变得越来越智能，jQuery 的需求也慢慢消失了。许多人说现在是扔掉这个库的时候了，声称在我们的现代世界中没有 jQuery 的位置。

我认为不同，这篇文章将告诉你为什么。

# jQuery 开销大小

![](img/1eb6a30544ef012677fdd0555d5ebbd9.png)

我把所有的网页文件分成四类:

1.  关键内容—网站的第一个 100vh(必须尽快交付。比如我们牛逼的第一屏[**https://phoenix-startup.com**](http://phoenix-startup.com/?utm_source=medium&utm_medium=social&utm_campaign=landing)**💜**)
2.  主要内容——用户看到的所有文本、样式、图片和视频。
3.  脚本——你所有的动画、表单提交和其他漂亮的互动。用户可能会使用其中任何一个。
4.  其他—广告、分析、跟踪。用户不需要任何东西。

典型的网站或 webapp 脚本(逻辑)是第三类文件。这意味着用户在得到所有的 html、css 和一些图片后会需要它。让我解释一下:在获得页面后，用户会花一些时间来观察你的内容(文本、图片),决定做什么，点击哪里或者滚动到哪里。也就是说加上 *187ms** 的后台工作*没有任何意义*。
而且，是啊。您不能保证您的无 jQuery 代码会执行得更快😉

作为奖励，一个 GUI 工具可以创建你自己的 jQuery:[http://projects.jga.me/jquery-builder/](http://projects.jga.me/jquery-builder/)

最后一点也很重要。在开始指责 jQuery 之前，尝试修复您的主要加载速度和性能问题。看看谷歌 Chrome 开发工具的指标，发现你的服务器 ping，优化图像(并自动化)，杀死不必要的库等。

# 对新手不好

![](img/10dec4aaf9114ac62abde8933e42d6d0.png)

许多人说用 jQuery 开始学习 web 开发技术是一个糟糕的决定。他们说初学者不会充分理解这些东西。

我的立场相反。
我确定是 a-w-e-s-o-m-e 才能达到很酷的结果(嗯，*任何*结果！)开头快。它极大地激励了你，给了你完成学习的信心。

对我来说，很明显，在变得更强大之后，他肯定会更深入地挖掘，学习他需要的关于 web api 和所有其他很酷的 JavaScript 东西的一切。

# 重新发明轮子

![](img/442acd5cd44b228483e2fb81fb387592.png)

是的，从头开始创造所有的东西是可能的。
*干脆*别忘了:

1.  让它变得完美就像约翰辞职一样。
2.  留意更新你的资料。
3.  想想依赖注入和模块化加载。
4.  跨浏览器兼容性[https://twitter.com/jeresig/status/590199945174634497](https://twitter.com/jeresig/status/590199945174634497)
5.  使其可链接。
6.  教给每个新队员。

jQuery 的许多功能已经在 http://youmightnotneedjquery.com 的进行了重做，提供了甜蜜的香草片段。
像这样:

## jQuery

```
$(el).fadeIn();
```

## 普通 JavaScript (IE10+)

```
el.classList.add('show');
el.classList.remove('hide');.show {
  transition: opacity 400ms;
}
.hide {
  opacity: 0;
}
```

但是如果你稍微思考一下，你就会发现它比 jQuery 更好。fadeIn()要复杂和灵活得多:

1.  它不只是简单地将不透明度增加到 1，它*显示*一个具有适当显示的元素:{ value }；
2.  它提供回调。普通版本应该使用类似于[这个](https://developer.mozilla.org/en-US/docs/Web/Events/transitionend)的东西。
3.  它提供链接。

请不要盲目，谨慎选择。

# 链接

![](img/0af60a61dee31c5e0ae90312a2a806e7.png)

一个*不能*做这样的事情:

## 普通 JavaScript

```
let body = document.querySelector(‘body’);body
   .classList.add(‘state-success’)
   .classList.remove(‘state-error’); // *TypeError: body.classList.add(...) is undefined*
```

就我个人而言，我非常喜欢 jQuery，因为它提供了一种将我的代码开箱即用的能力:

## jQuery

```
let form = $('#js-form');             //get the formform
    .removeClass('state-error')       //remove red color
    .addClass('state-success')        //add green color
    .find('.js-success-message-text') //get the success text
        .fadeIn()                     //show the success text
    .[end()](https://api.jquery.com/end/)                            //get the form again
    .find('.js-error-message-text')   //get the error text
        .fadeOut()                    //hide the error text
```

# 插件

![](img/ed134863d4c3b2fe76a7ea4afc104a79.png)

在过去的 10 年中，jQuery 社区发展得非常大。jQuery 插件列表也是如此:[https://plugins.jquery.com](https://plugins.jquery.com)
你会在那里找到大量现成可用的插件。

# 结论

![](img/df3a45c183eed0a0278106f281379922.png)

jQuery 在过去做了令人难以置信的史诗般的工作。但是事情确实在变。今天，JavaScript 上升速度惊人，巴别塔使所有这些功能现在都可以访问，大多数浏览器倾向于立即更新自己，wasm 即将到来，人工智能入侵世界…

尽管如此，在某些情况下，好的 jQuery 仍然是可用的，而且非常有用。现在埋库太早了。

想想吧。

* *在平均移动网络(5Mbps)上下载 jQuery 2.1.1 (28.87KB gzipped)大约需要 47ms，在 Chrome 50 LG Nexus 5 上启动 jQuery 2.1.1 需要 140 ms。*

[![](img/50ef4044ecd4e250b5d50f368b775d38.png)](http://bit.ly/HackernoonFB)[![](img/979d9a46439d5aebbdcdca574e21dc81.png)](https://goo.gl/k7XYbx)[![](img/2930ba6bd2c12218fdbbf7e02c8746ff.png)](https://goo.gl/4ofytp)

> [黑客中午](http://bit.ly/Hackernoon)是黑客如何开始他们的下午。我们是这个家庭的一员。我们现在[接受投稿](http://bit.ly/hackernoonsubmission)并乐意[讨论广告&赞助](mailto:partners@amipublications.com)机会。
> 
> 如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！

[![](img/be0ca55ba73a573dce11effb2ee80d56.png)](https://goo.gl/Ahtev1)