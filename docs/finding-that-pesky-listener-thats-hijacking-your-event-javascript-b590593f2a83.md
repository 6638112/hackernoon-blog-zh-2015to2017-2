# 找到劫持您事件的讨厌的监听器(Javascript)

> 原文：<https://medium.com/hackernoon/finding-that-pesky-listener-thats-hijacking-your-event-javascript-b590593f2a83>

这是一个关于如何确定什么事件监听器正在调用`event.preventDefault()`或`event.stopPropagation()`或其他一些完全随机的不允许您预期操作的事情的调试故事。

## 问题是

我们有这样一个表单，当我们点击输入框时，它不会聚焦。所以很明显，有什么东西在听这个输入框的焦点，或者在听别的什么东西的模糊点，并试图把焦点放在其他一些不在那里或隐藏在屏幕上的输入框上。

现在我们有了一个庞大的代码，其中包含了大量的意大利面条式的代码，不知何故，这些代码可以正常工作。(我们有 React 和 Backbone，我们有 [jQuery](https://hackernoon.com/tagged/jquery) 和下划线，我们拥有一切。我们即将完成迁移),因此很难找出导致这种情况的原因。事件侦听器是从许多地方添加的，但不知道有多少。

## 使用 Chrome DevTools 查找 DOM 修改

在 [Chrome](https://hackernoon.com/tagged/chrome) DevTools 中，要找出是否有东西正在修改 DOM 是非常容易的，只需在元素窗格中选择元素，右键单击，然后就可以选择中断子树修改、属性修改和节点删除。

![](img/7c0aca5c22c9747a79b60a7c7a1e16ce.png)

但是对于我们当前的问题，DOM 没有被修改，所以这在这里没有帮助。

## 列出特定事件的所有 DOM 事件侦听器

在 Chrome DevTools 的元素面板中，Styles 旁边有一个事件监听器标签。这里有一个列表，列出了所有事件和为该事件添加的事件侦听器，覆盖了在 Elements 窗格中选择的当前 DOM 元素的所有祖先。(*听起来像绕口令*😂)

![](img/dd48df1717a574b21207cb31dada6be9.png)

这里有删除侦听器的选项，或者您可以转到侦听器函数定义。但是如果你使用任何像 jQuery 或 React 这样的框架，它会带你到它的内部函数，所以这是没有帮助的。

所以我们想，让我们去掉监听器，我们可能会很幸运。我们移除了聚焦、模糊、点击等的监听器。如果这就是阻碍我们的原因。但是遗憾的是，我们移除了所有祖先上所有事件的所有侦听器，但是我们仍然无法将注意力集中在我们的输入框上。

## 这告诉我们什么？

这确实告诉我们一件事，监听器不是监听焦点或点击事件，而是监听我们的元素的不相交树中的一些其他元素的模糊事件。我们在存储库中搜索了`'blur'`、`"blur"` & `onBlur`，找到了超过 25 个实例。废话。这需要很长时间。我的同事开始到处添加调试器语句。

现在，我们可以在捕获阶段为`focus`在窗口上添加一个事件监听器，我们可以找到窃取焦点的罪魁祸首 DOM，但是它没有给我们设置焦点的罪魁祸首函数。我们需要一些额外的步骤来找到它。

## 我们能做得更好吗？输入时间线。

从脚本到时间轴面板中的渲染，您可以记录浏览器中发生的所有事情的火焰图。所以我们开始记录，点击输入框并停止，瞧，我们找到了事件和它的听众。

![](img/a990df8be71529e764d1f525c76cd204.png)

单击名称会将您带到源代码面板中的定义，它就在那里:

![](img/5b302e61473d0e6e6252758b40f29fcd.png)

查看预编译的代码，我们发现作者留下了一个注释。

```
parent[0].addEventListener('blur', function(e) {
  if (!e.relatedTarget) {
    return;
  }
  // **if tab key is pressed, and something out of modal-container is focused, snatch it back.**
  if (!$(this).find(e.relatedTarget).length) {
    return this.focus();
  }
}, true);
```

## 什么？？

如果有别的东西被聚焦，就把它抢回来。什么？？像这样的一段代码在做什么？

因此，这段代码被添加到了模态库代码中，这样，如果有人单击 tab 或 shift + tab，并且在模态背景后面有其他输入框，光标可能会移动到那里，或者如果您在您的身体上添加了一个隐藏的溢出，并且您的输入框在屏幕的底部，浏览器可能会向下滚动，用户可能看到的只是背景。

这是一段非常简洁的代码。感谢[普拉纳夫·古普塔](https://medium.com/u/37aa88e9375d?source=post_page-----b590593f2a83--------------------------------)的加入。

## 那么我们做错了什么？

所以正如我上面提到的，我们正在将我们的代码库从主干迁移到 React。我们所做的是在主干模型之上打开了一个 React 模型(用 React 编写的模型)。我们制作了两个不同的容器，一个用于所有主干模态，另一个用于所有反应模态，这就是为什么活动模态失去焦点会导致这个问题。添加了一些小条件，我们解决了这个问题。

## 带走- Chrome DevTools 时间轴

这可能不是有史以来最难的错误，但是使用时间线可以是一个有效的工具来发现到底发生了什么，一个操作有多慢或多快。它可以很容易地用于发现性能下降。于是**开始录制**。

![](img/946a10258b54ddcde53efb86e0102e1e.png)

你认为有更好的方法来调试这个吗？(*除了写出更好代码的明显方法*😂)请在评论中提到这一点。如果你学到了新的东西，推荐这个故事。

[![](img/50ef4044ecd4e250b5d50f368b775d38.png)](http://bit.ly/HackernoonFB)[![](img/979d9a46439d5aebbdcdca574e21dc81.png)](https://goo.gl/k7XYbx)[![](img/2930ba6bd2c12218fdbbf7e02c8746ff.png)](https://goo.gl/4ofytp)

> [黑客中午](http://bit.ly/Hackernoon)是黑客如何开始他们的下午。我们是 [@AMI](http://bit.ly/atAMIatAMI) 家庭的一员。我们现在[接受投稿](http://bit.ly/hackernoonsubmission)，并乐意[讨论广告&赞助](mailto:partners@amipublications.com)机会。
> 
> 如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！

![](img/be0ca55ba73a573dce11effb2ee80d56.png)