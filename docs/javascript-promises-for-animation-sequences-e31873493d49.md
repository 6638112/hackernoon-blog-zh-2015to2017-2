# Javascript 承诺动画序列

> 原文：<https://medium.com/hackernoon/javascript-promises-for-animation-sequences-e31873493d49>

![](img/16080254c885590cb261629d453cb13a.png)

我最近有机会参加了令人惊叹的 [creativecoding.club](http://creativecoding.club) 并拼凑了一个花朵落地的树的动画。这棵树首先使用随机算法建造(灵感来自 survivol 的这支[生长](http://codepen.io/survivol/pen/pbGpog)笔)，然后将花朵随机连接到新生长的树的树枝末端。

作为后端[工程师](https://hackernoon.com/tagged/engineer)的经验比设计或动画方面的经验多，我立即想到使用 [Javascript](https://hackernoon.com/tagged/javascript) 承诺帮助我排序一切，就像一堆数据库事务与 API 调用交错。它涉及到异步递归，这一开始看起来很棘手，所以我想我应该写一个解释，以防它可能会帮助其他想以同样的方式将它用于动画的人。😊

# 种植树木

![](img/ec84fdca3c3b44c0b567cd1d7153f55d.png)

From tiny acorns…

第一步是弄清楚如何创建随机树。我们使用递归，这实际上是一种奇特的方式，说明我们是在已经做好的工作的基础上进行构建的。这是一个高层次的想法:

1.  从树干开始——我们知道它的起点(地面)和终点(树干离地面的高度)。
2.  画树干。
3.  接下来，从主干上创建一些分支——它们从主干结束的地方开始。我们在树干的左右两侧随机选取一些角度，一些比树干本身稍短的随机长度，并用它们来计算新树枝的末端。
4.  画树枝。
5.  对于两个新分支中的每一个，我们取它们的端点，并从它们上面再长出两个分支，就像步骤 3 中一样。
6.  重复，直到我们达到了我们想要的树的深度！

所以这个算法会给我们一棵树，但是如果我们边走边画的话，它的绘制速度会和计算机能够绘制和计算的速度一样快，可能太快了。如果我们想给树添加动画，让它看起来长得更慢，会怎么样？嗯，我们可以加一个延时！

在步骤 3 和 4 之间，计算然后绘制新的分支，我们可以等待(使用 setTimeout())来绘制分支。由于重复发生在绘制之后，所以树会慢慢散开，计算、等待、绘制、计算、等待、绘制等。

因此，我们最终得到的代码可能大致如下所示(假设未定义的函数做了它们目前所说的事情):

# 寻找最后一个分支的末端

一旦我们种了树，我们就知道最后的树枝在哪里，我们想把它们都收集起来，这样我们就可以在下一阶段给它们加上花。具体来说，当我们意识到我们的 newRemainingBranches ≤ 0 时，我们知道我们不会再分支，因此我们知道我们计算的终点是一个结束分支。

如果我们没有将所有这些延迟添加到代码中，我们本可以找到某种方法将分支的末端返回给 growTree()的调用者。所以我们需要想出另一种方法来获得所有这些分支末端…

我们可以先尝试的一种方法是，创建一个数组，把分支末端放进去。我们可以将数组传递给 growTree()/growBranch()，或者使用一个全局变量。不管怎样，我们都不确定*什么时候*所有的分支都在数组中。我们可以尝试计算我们期望的分支数量，但是我们仍然需要等待和投票来得到正确的数量。

如果我们只是在所有分支创建时才得到通知，不是更好吗？

# 输入承诺

“I’m sorry, but I’m just thinking of the right words to say” for this section which is hard to explain

[承诺](https://developers.google.com/web/fundamentals/getting-started/primers/promises)是做到这一点的好方法！假设我们的 growTree()函数返回一个承诺，无论何时计算并绘制了所有的分支，它都会告诉我们并给我们分支。然后我们可以用这些树枝来做花的动画。

由于 growTree()只是一个带有特殊参数的对 growBranch()的调用，因此让 growBranch()返回该承诺是有意义的。但是 growBranch()递归地调用自己，尽管是以一种延迟的方式。因此，如果我们说 growBranch()返回的是对一组端点的承诺，我们可以开始构建一个递归的承诺“树”(现在在计算机科学的意义上)。当我们得到所有这些承诺的结果时，我们可以将它们展平，得到一个分支结尾的数组。

Promise 库有几个不同的方面，所以让我们分别来看一下:

*   **Promise.resolve()** 是一个效用函数，它说，“我保证我会给你这个值，但是，就像，现在。”这使得我们总是从函数中返回一个承诺变得一致，所以无论谁调用它，包括我们自己，都可以这样对待它。
*   **Promise.all()** 是另一个实用程序，用于承诺您将返回您传递的所有承诺解析(您承诺返回的实际内容)的数组。换句话说，它一直等到几件事情都完成了，然后将它们作为一个包返回。
*   让我们以完全定制的方式创建一个新的承诺。它接受一个函数，并使用 resolve()函数调用该函数。当您在该函数中调用 resolve()时，它将解析为您为 resolve()提供的参数。第一次看到它时，很难理解，但是在我们的例子中，我们只是试图将 growBranch()递归调用的输出返回给父节点。如果这没有意义， [Mozilla 有一个更清晰、更深入的解释](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)。
*   **Promise.prototype.then()** 让我们将计算链接到承诺的末尾。在这种情况下，我们希望将树中所有已解析的值展平到端点的平面数组中。

# 最终产品

所以我希望这一切都有意义，但有很多事情正在发生，所以它可能只是有助于分叉和玩这个代码笔只有树。

运行检查器，您应该能够看到输出到控制台的所有端点的数组。这支笔中的代码与上面 gists 中的代码略有不同，为了清楚起见，我*试图*简化这些代码。

最后，一旦你对上面的树动画有所了解，你可以看看这支笔，它使用树枝端点来种花:

如果你最终使用了这个技巧，请在 Twitter [@OngEmil](https://twitter.com/OngEmil) 上与我分享或者作为下面的回应！🌸🌸🌸

*好吧，我不打算发布那个 gif，问你是否喜欢这个帖子，所以作为回报…你愿意吗*💚*如果你喜欢这篇文章，请关注？:D*

[![](img/50ef4044ecd4e250b5d50f368b775d38.png)](http://bit.ly/HackernoonFB)[![](img/979d9a46439d5aebbdcdca574e21dc81.png)](https://goo.gl/k7XYbx)[![](img/2930ba6bd2c12218fdbbf7e02c8746ff.png)](https://goo.gl/4ofytp)

> [黑客中午](http://bit.ly/Hackernoon)是黑客如何开始他们的下午。我们是阿妹家庭的一员。我们现在[接受投稿](http://bit.ly/hackernoonsubmission)并乐意[讨论广告&赞助](mailto:partners@amipublications.com)的机会。
> 
> 如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！

![](img/be0ca55ba73a573dce11effb2ee80d56.png)