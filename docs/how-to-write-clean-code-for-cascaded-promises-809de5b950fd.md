# 如何为级联承诺编写干净的代码

> 原文：<https://medium.com/hackernoon/how-to-write-clean-code-for-cascaded-promises-809de5b950fd>

## 关于相互依赖的承诺的深入指导

![](img/a70001f357a6a360b4106f8aa7727997.png)

Photo by [Luis Perdigao](https://unsplash.com/photos/vYo_Arzy_WU?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

作为一名开发人员，我一直在寻找编写更干净代码的方法。

一年前，我发布了一个名为 [Premiere](https://github.com/pedsmoreira/premiere) 的库，旨在方便用 Javascript 在前端使用 Restful APIs。我现在正在构建一个 v2 版本的库，在这个过程中，我注意到还有让代码更干净的空间，特别是在承诺方面。

在这篇文章中，我不会解释承诺的基础，但是如果你正在寻找，看看戴夫·阿切利的文章，他在这方面做得很好。

*免责声明:寻找异步/等待示例？跳到最后，单击存储库链接。*

虽然承诺不是 HTTP 请求的唯一性，但这正是它们通常的用途，所以这将是本文示例的主题。

让我们开始吧:

这是一段直截了当的代码，工作做得很好。然而，如果我们采用相同的功能，并添加更多的功能，如缓存，它可以开始变得复杂。这里有一个例子:

如你所见，这个例子不像上一个例子那样干净。做的事情太多了。当然这不是世界末日，但是理想情况下每个函数应该只做一件事，所以测试和重用它更容易。

如果我们添加另一个级别的缓存，这个问题会变得更加明显。因此，让我们添加 Promise 缓存(以防止发出两个相同的请求)并看看它是什么样子的:

我们离“只做一件事”更远了。我们添加到代码中的东西越多，它就会变得越乱，也越难重用。例如，如果我们决定创建一个`fetchAndCacheItem`,这将要求我们复制所有的代码。

## 分解它

分解的第一步是将事情分成更多的功能，每个功能负责一个问题。我们要做的是创建三个函数，每个函数负责做三件事情中的一件:

1.  缓存承诺
2.  缓存结果
3.  取数据

这里的主要挑战是将一个片段连接到另一个片段，因为并不是所有的片段都需要每次都执行(例如缓存时)。为此，我们将提供对缓存函数的回调，以便在缓存不存在时调用它们。

下面是代码:*(为了清楚起见，隐藏了缓存方法)*

好多了吧？我们确实有更多的代码行，但是阅读维护要容易得多。回到`fetchAndCacheItem`提到的，随着我们关注点的分离，我们可以开始看到重用相同功能的途径。

## 下一步

我们已经达到了令人满意的程度，但是如果我告诉你我们可以做得更好呢？

看一下我们的最后一个函数`fetchAndCacheUser`，我们可以看到这些函数是以相反的执行顺序声明的，这可能会很混乱。我们还必须声明一个新的变量，并为每一步分配一个函数，这会使代码变得混乱。

为了解决这些问题，我创建了`promise-cascade`库。下面是使用`promise-cascade`时`fetchAndCacheUser``函数的样子:

如你所见，代码现在是按照自然顺序编写的，没有了`const ... = () => ...`的混乱。

在一些大量使用这些功能的情况下，扩展`PromiseCascade`并创建助手方法会很有帮助，因此可以调用`cascade.something(value1, value2)`而不是`cascade.push(something.bind(this), value1, value2)`。你可以在 GitHub repo 上看到这个[的例子。](https://github.com/pedsmoreira/promise-cascade)

更多细节和例子(包括`async`)请查看 GitHub。如果你喜欢它，我很感激你给它一个🌟明星。

[](https://github.com/pedsmoreira/promise-cascade) [## 佩兹莫瑞拉/无极瀑布

### JS 承诺级联变得简单

github.com](https://github.com/pedsmoreira/promise-cascade) 

## ❤️喜欢。分享一下。留下你的评论。

别忘了传播爱。加入你喜欢的，与你的朋友和同事分享。也非常欢迎你在下面留下你的评论。

你可以继续关注我在[twitter.com/pedsmoreira](https://twitter.com/pedsmoreira)上创作的东西，或者订阅我的时事通讯:

Don't worry, no spam ❤

## 额外的

如果你喜欢用爱制作的软件，我想邀请你参加 [GitShowcase](http://gitshowcase.com/) 。来获得你自己的摇滚明星作品集🤘。 *cc* [*维克托·桑托斯*](https://medium.com/u/f2368f957647?source=post_page-----809de5b950fd--------------------------------)

[](https://www.gitshowcase.com/) [## GitShowcase

### 开发人员，在即插即用产品组合中展示您的最佳项目。最棒的是，免费的。

www.gitshowcase.com](https://www.gitshowcase.com/)