# ⚡Using 联邦航空局创建联邦航空局🍺

> 原文：<https://medium.com/hackernoon/using-faas-to-create-faas-bc554ccb7fa6>

## 使用 Azure Functions 又名 functions as a service 又名 FaaS 创建 FaaS 又名福利 as a service

最近我写了这篇博客

[](https://hackernoon.com/github-statuses-made-easy-with-faas-fd9236a41925) [## FaaS 让 GitHub 状态变得简单

### 使用 Azure 函数自动化你的请求验证

hackernoon.com](https://hackernoon.com/github-statuses-made-easy-with-faas-fd9236a41925) 

当我发微博时，它得到了这样的回复

![](img/7d8adb9a7425069b5e22c2d25011e076.png)

我的直觉告诉我必须这么做！

…而且必须以“企业的方式”来完成…所以今晚我给自己 10 分钟来做 A-Z 的所有事情(*博客文章不包括*)想出一个解决方案，8 分 56 秒后，我的概念验证开始运行&。
这是我想到的

![](img/4805f711ea6dd426c33ab06b9078407e.png)

很明显对吗？让我们一步一步地来看它，尽管它很疯狂——它实际上是一个很好的展示案例，展示了什么是非常容易做到的。

## 服务

那么福利提供的最好的服务是什么呢？显然是本周啤酒精选！所以为什么不开发一个 Twitter 机器人，给人们随机挑选啤酒！

## 推特

第一步，创建 epic twitter 账户:

[](https://twitter.com/FoleyAsAService) [## 福利即服务(@FoleyAsAService) | Twitter

### 福利即服务的最新推文(@FoleyAsAService)

twitter.com](https://twitter.com/FoleyAsAService) 

## IFTTT

Twitter APIs 很麻烦，让我们站在巨人的肩膀上，如果它很容易并且免费——一个付费的替代方案可能是 Azure Logic Apps，它有一个搜索 Twitter 触发器。

![](img/a2d6bfe42d93bc286b08708ae221fb4e.png)

因此，当我新创建的帐户被提及时，一个设置小程序被触发。IFTTT 暂时不要发布到 Azure 函数，但是它们可能会产生 GitHub 问题！

![](img/a4f5b07de97f7e11d47e9fe915d1bc3b.png)

## 开源代码库

IFTTT 获得一次提及的速度并不快，需要一分钟到一个小时，但当它最终获得提及时，它的效果非常好

![](img/e2d51585b95b4a7dff164c5e891dc597.png)

你说这对我们有什么帮助？当问题产生时，GitHub 可以触发 Azure 函数。

![](img/f80bdb40cfa2400a55bc43a9a8600943.png)

只需选择个别事件并将其缩小到问题范围——我认为这太棒了！

![](img/0743488198d110e7748c548c665381a4.png)

## Azure 功能 1

我们的第一个 Azure 函数将只接收 GitHub webhook 事件，挑选所需的数据，解析 GitHub 注释，然后将其排队到 Azure 存储队列中

队列项 GitHubIssue 类只是一个概念，没有什么特别的，看起来像这样

## Azure 函数 2

我们的第二个函数订阅 Azure 存储队列，并在被触发时重用同一个 GitHubIssue 类来获取类型化消息。

现在有趣的是，NOSQL 是当今的热门词汇，我想要一个玛丽·乔可以轻松管理自己的解决方案…

![](img/d7821a719a2cb818d748b36fc6d75ad6.png)

…还有什么比使用记事本管理我们的啤酒选择更好的解决方案呢，你说这怎么可能呢？

![](img/8cd741136fc82b04eea22bb6f417e2db.png)

显然，我们使用 OneDrive 来存储文件，可以从记事本轻松编辑！因为 Azure 现在在预览版中支持将参数绑定到 OneDrive 上的文件！所以我们需要做的就是读取文件中的行，并随机选择一行作为 tweet。不会说 Twitters API 太复杂，但时间紧迫，Buffer 提供了一个简单得多的 API，它只是一个 HTTP post，也让我可以转发带有评论的原始 tweet。

那么函数看起来是什么样的，对于仓促的工作来说，它实际上并没有那么糟糕( *IMHO* )。

它的绑定只是队列&外部文件进来

![](img/8e5425a2958520fa902e221b7d3e62fe.png)

外部文件是在预览中，还没有普遍可用，但它已经支持几个服务，所以我可以看到这在未来变得非常有用！

![](img/a5395b162bc132b46ac87ad349317bea.png)

## 结果呢

只要我没有用完信用点数，它就会在 60 分钟内返回给你一瓶啤酒

![](img/1de446b9f55ea8acaf54bd3cc68b0d92.png)

## 结论

一开始，我只是开玩笑，挑战自己 10 分钟能做多少事——我发现自己真的有点惊讶，原来复杂的事情竟然变得如此简单。显然代码需要重构、错误处理和测试——但是使用几个在线服务做一个概念验证是非常酷的。

所以谢谢你的主意，玛丽·乔！这是在 FaaS 的一次有趣的练习——福利服务🍺

## 更新

福利即服务在[视窗周刊第 506 集](https://twit.tv/shows/windows-weekly/episodes/506)上被特别报道

[![](img/50ef4044ecd4e250b5d50f368b775d38.png)](http://bit.ly/HackernoonFB)[![](img/979d9a46439d5aebbdcdca574e21dc81.png)](https://goo.gl/k7XYbx)[![](img/2930ba6bd2c12218fdbbf7e02c8746ff.png)](https://goo.gl/4ofytp)

> [黑客中午](http://bit.ly/Hackernoon)是黑客如何开始他们的下午。我们是 [@AMI](http://bit.ly/atAMIatAMI) 家庭的一员。我们现在[接受投稿](http://bit.ly/hackernoonsubmission)并乐意[讨论广告&赞助](mailto:partners@amipublications.com)机会。
> 
> 如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！

![](img/be0ca55ba73a573dce11effb2ee80d56.png)