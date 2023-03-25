# 从 Expressjs 4 迁移到 5

> 原文：<https://medium.com/hackernoon/migrating-from-expressjs-4-to-5-156dcd80eb11>

## 随着 2017 年的开始，是时候适应这些变化了

![](img/589248ba04191b598fa75c33d5e66857.png)

xpressJS 5.0 正处于 alpha 发布阶段，但我相信我们很快会将它作为一个依赖项添加到我们的`package.json`文件中。这篇文章给出了一些关于我们使用这个框架编写代码的方法，以及即使我们使用的是 express js*4.0*版本，我们也应该如何适应新的变化。

我先从最常见的东西比如`response`说起。

Express 5 不再支持签名`res.send`，取而代之的是我们应该以这种形式使用这种方法:

```
res.status(statusCode).send();
```

我们必须在发送响应对象之前设置状态代码。这个新版本的`res.send`基本上是两个方法的连锁:`res.status` & `res.send`。

考虑到这一点，ExpressJS 5 不赞成使用`res.send(statusCode)`方法，其中`statusCode`是表示 HTTP 响应头状态代码的数字。为了只发送 statusCode，即不发送响应对象，我们可以使用`res.sendStatus(statusCode)`方法。

与类似，其他改变的方法有:

```
 res.json() --> res.status().json()
res.jsonp() --> res.status.jsonp() 
```

另一个值得注意的方法是`res.sendfile()`，在下一个版本的 ExpressJS 中将会被弃用。相反，我们必须修改它的新形式，camelCase one: `res.sendFile()`，它已经被比`4.8.x`更高版本的 ExpressJS 所支持。它带有可选参数，您可以在这里 **查看这些参数 [**。**](http://expressjs.com/en/4x/api.html#res.sendFile)**

无论您计划使用 Express 5.0 的 alpha 版本还是继续使用 Express 4.0 的最新版本，我都建议您立即开始调整这些方法。

*在* ***这里可以找到完整的变更列表或官方的 Express 迁移指南。***

> ***感谢阅读。如果你觉得这个帖子有用，请点击*T3💚**按钮*这样这个故事就能接触到更多的*读者*。如果你想谈论更多，请在***[***Twitter***](https://twitter.com/amanhimself)***|***[***Goodreads***](https://goodreads.com/amandeepmittal)***|***[***书博***](https://amandeepmittal.wordpress.com/)***|*****

[![](img/50ef4044ecd4e250b5d50f368b775d38.png)](http://bit.ly/HackernoonFB)[![](img/979d9a46439d5aebbdcdca574e21dc81.png)](https://goo.gl/k7XYbx)[![](img/2930ba6bd2c12218fdbbf7e02c8746ff.png)](https://goo.gl/4ofytp)

> [黑客中午](http://bit.ly/Hackernoon)是黑客们如何开始他们的下午。我们是 [@AMI](http://bit.ly/atAMIatAMI) 家庭的一员。我们现在[接受投稿](http://bit.ly/hackernoonsubmission)并乐意[讨论广告&赞助](mailto:partners@amipublications.com)机会。
> 
> 如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！

![](img/be0ca55ba73a573dce11effb2ee80d56.png)