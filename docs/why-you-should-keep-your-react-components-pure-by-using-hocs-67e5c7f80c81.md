# 为什么您应该使用 HOCs 来保持 react 组件的纯净

> 原文：<https://medium.com/hackernoon/why-you-should-keep-your-react-components-pure-by-using-hocs-67e5c7f80c81>

![](img/d82fac5138788ce563c800dfdfa45527.png)

Image courtesy of [tahoepurewater](https://www.tahoepurewater.com)

如今构建前端应用程序非常复杂。一些 html 加上一点 jQuery 就能解决问题的日子已经一去不复返了。今天，我们希望响应迅速、丰富、动态的单页面应用程序( **SPA** )能够在大量的设备和浏览器上运行——这不是一件容易的事情。幸运的是，我们有强大的框架和库可以帮助我们。在本文中，我用一些 [React](https://facebook.github.io/react/) 的例子展示了从表示层分解状态如何既能降低复杂性又能促进代码重用——这是一个双赢的局面，有助于克服开发 spa 的挑战。虽然我使用的是 React，但这些经验是通用的，可以应用于任何 T4 框架。

> 警告，下面有大量代码

考虑一个简单的 toggle React 组件，它可以显示“ **on** ”或“ **off** ”:

我们在这里使用了一些 ES7 语法，但基本上组件可以呈现两个不同的元素，并通过用户点击它来切换状态。作为负责任的开发人员，我们可以用下面的代码来测试它(如果我们真的负责任，我们会首先编写这些测试😋):

到目前为止很简单…除了在测试数量上有点少——没关系。但是，假设我们有另一个本质上类似但不同的组件，足以保证它有自己的代码，例如，可以显示或隐藏消息的 info 组件:

该组件具有不同的属性，并显示不同的元素集；然而，测试结果非常相似，因为基本上组件是相同的:对单个布尔状态变量的条件呈现。

在每个组件中，很大一部分代码和测试都与管理状态有关。想象一下在一个大的代码库中重复这个过程——这可能会有点乏味。那么我们能做什么呢？

## 引入高阶元件，即 hoc

![](img/b9f93bc5334d68e4112d0bf426c3bdd9.png)

Image courtesy of [serenityatsummit](https://www.serenityatsummit.com)

什么是**特设**！？

> 高阶组件(HOC)是 React 中重用组件逻辑的一种高级技术。本质上，hoc 不是 React API 的一部分。它们是从 React 的组合性质中出现的一种模式。
> 
> 具体而言，**高阶分量是取一个分量并返回一个新分量的函数。**[https://Facebook . github . io/react/docs/higher-order-components . html](https://facebook.github.io/react/docs/higher-order-components.html)

下面的代码显示了一个 **HOC** ，它可以包装任何具有开/关布尔状态的组件，一个点击处理程序来切换标志:

注意，它只是一个带有单个参数`WrappedComponent`(添加额外功能的 react 组件)的函数，它返回一个新的 react 组件；该组件负责呈现原始组件，但用布尔属性`on`和管理状态的`toggle`函数进行了修饰；它还会传递您想要的任何其他属性。

关于 **HOC** 的惊人之处在于，因为它们只是简单的函数，我们可以将多个 **HOC** 组合在一起，以增加潜在的无限功能。我们可以创建简单的、通用的、经过良好测试的组件，最终得到复杂的、功能强大的组件。

让我们不要忘记对我们的**特设**的测试:

## 现在来看看我们的纯组件

![](img/24522871e8ee005e54ba96a54095f406.png)

Image courtesy of [eastcottvets](http://www.eastcottvets.co.uk)

> 纯函数是这样的函数，给定相同的输入，将总是返回相同的输出，并且没有任何可观察到的副作用。[https://dr boolean . git books . io/mosely-sufficient-guide/CH3 . html](https://drboolean.gitbooks.io/mostly-adequate-guide/ch3.html)

看看我们的 Toggle 组件现在有多漂亮。我们还可以在组件的属性上使用析构(`Toggle = ({on, toggle}) => ..`)，这使得如何使用组件变得非常声明性和明显，即它需要两个参数:`on`和`toggle`；如果我们检查`propTypes`对象，我们也可以看到它们分别是一个布尔 and 函数。*如果你想了解更多关于析构的知识，可以看看我的文章* [*JAVASCRIPT ES6 析构和一些有用的技巧*](/@DjamelH/javascript-es6-destructuring-and-a-few-useful-tricks-883c1c493783)

然后，我们使用我们的`withState` **HOC** 用`on`状态和`toggle`功能包装我们的纯组件。

我们的测试:

我们的测试现在已经改变了:我们只关心当组件被点击时切换功能是否被调用；我们相信实际的状态操作已经被测试过了——事实也的确如此！

让我们看看 Info 组件是如何被重写以使用`withState` **HOC** :

可爱！

测试是:

就像 Toggle 组件的测试一样非常简单。

# 结论

希望您已经看到了我们如何将一些状态委托给 **HOC** s，这通过允许我们开发可爱的纯函数来简化我们的 [React](https://hackernoon.com/tagged/react) 组件。由于我们最终可能会大量重用我们的 **HOC** ，这鼓励我们投入时间和精力来编写高质量的通用代码，并用单元测试彻底覆盖代码。例如，本文中介绍的简单 withState **HOC** 可能应该被重构，以使用一个函数来设置状态，而不是直接使用一个对象(有关更多信息，请参见本文[文章](/@shopsifter/using-a-function-in-setstate-instead-of-an-object-1f5cfd6e55d1))。对于我们上面的简单用例，这不会引起任何问题，但是如果它是一个可靠的可重用的 **HOC** ，我们真的应该这样做。

如果您想尝试本文中的代码，请随意克隆/派生我的 [repo](https://github.com/dhassaine/reactPureVsClass) 。

*如果你觉得这篇文章有用/有启发性* ***点击*** 💚这样其他人也可以享受。

感谢您的宝贵时间！关注我的[*Twitter*](https://twitter.com/DjamelH)*和*[*LinkedIn*](https://www.linkedin.com/in/dhassaine/)*。*

如果你对构建复杂的应用程序感兴趣，你可能会喜欢我的文章[sentinurl.com SaaS 的架构](/@DjamelH/architecture-of-a-saas-sentinurl-com-a53a5c3724ee)来获得一些高层次的架构建议。

[![](img/50ef4044ecd4e250b5d50f368b775d38.png)](http://bit.ly/HackernoonFB)[![](img/979d9a46439d5aebbdcdca574e21dc81.png)](https://goo.gl/k7XYbx)[![](img/2930ba6bd2c12218fdbbf7e02c8746ff.png)](https://goo.gl/4ofytp)

> [黑客中午](http://bit.ly/Hackernoon)是黑客如何开始他们的下午。我们是 [@AMI](http://bit.ly/atAMIatAMI) 家庭的一员。我们现在[正在接受投稿](http://bit.ly/hackernoonsubmission)并乐意[讨论广告&赞助](mailto:partners@amipublications.com)机会。
> 
> 如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！

![](img/be0ca55ba73a573dce11effb2ee80d56.png)