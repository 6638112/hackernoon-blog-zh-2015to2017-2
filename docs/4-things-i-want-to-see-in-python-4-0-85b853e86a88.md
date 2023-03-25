# 我想在 Python 4.0 中看到的 4 件事

> 原文：<https://medium.com/hackernoon/4-things-i-want-to-see-in-python-4-0-85b853e86a88>

CPython 3.6 出来了，3.7 分支都设置好了，CPython 现在在 [GitHub](https://github.com/python/cpython) 上。Python 社区激动人心的时刻。

Python 2.7 是 2.x 系列的最后一个版本，所以根据贝德维尔爵士的逻辑， **Python 4.0 将是继 3.7 之后的下一个主要版本。**

![](img/1d0e2ef9cb88742829f7e62abef5ba2a.png)

> “所有的木头都会燃烧，”贝德维尔爵士说。“因此，”他总结道，“所有燃烧的都是木头。”

好吧，这是完全不合逻辑的，但是如果 4.0 很快就要出来了，你希望看到哪些特性？

在我们开始列表之前，提醒我们自己 CPython 项目中有什么是很重要的。Python 是 3 样东西，一个**语言**，一个**标准** **库**和一个**执行** **引擎**。相比之下， **JavaScript** 只是一种语言。它有**没有**标准库，Google v8 引擎执行**、**以及许多其他选项。

这是我的清单，它主要包括对 CPython 的*执行引擎*组件(又名“运行时”)的更改。我相信标准库是特性打包的，任何在标准库中找不到的东西都可以在 PyPi 上找到。这种语言不需要任何新的操作符，也不需要另外一种格式化字符串的方式。

# 1.JIT 作为第一类特性

JIT 或即时编译是一种在字节码发生时编译它们的方法，而不是一次编译所有的字节码。根据具体情况，它可以带来更好的性能。

[PyPy](http://pypy.org/) 是 Python 自带 JIT 的实现， [Pyston](http://pyston.org/) 是 Python 使用 [LLVM](http://llvm.org/) 作为 JIT 编译器的实现。这些都是在功能(或语言的正确性)和速度上的妥协。

为 CPython 提供一个一流的 JIT 插件架构将把性能和兼容性需求联系在一起，花在 PyPy、Numba 等上的精力可以投入到主要的 CPython 生态系统中。

好消息是什么？多亏了核心开发者布雷特·坎农和他的微软同事迪诺·维兰，这已经被认可为 PEP-52 3。API 是在 3.6 中添加的，但是我们还没有看到 API 的实现。Pyjion 项目仍然需要更新。

# 2.稳定的. 0 版本

## Python 3 发布历史

python 3.0—2008 年 12 月 3 日

*   python 3.1—2009 年 6 月 27 日
*   python 3.2—2011 年 2 月 20 日
*   python 3.3—2012 年 9 月 29 日
*   python 3.4—2014 年 3 月 16 日
*   python 3.5—2015 年 9 月 13 日
*   python 3.6—2016 年 12 月 23 日

Python 3 已经发布了 9 年，但是前两个版本(3.0，3.1)有很多严重的错误和安全问题。Python 3.3 是 3.x 系列中第一个包含快速`decimal`类型、作为核心函数的 virtualenv 和名称空间包支持的版本。

如今，PyPi 上大多数支持“Python 3”的主流包，比如`requests`都支持> 3.3。在 2008 年至 2012 年间尝试 Python 3 的早期采用者可能会认为它还没有准备好。第一印象不可能设定两次*。*

我对 4 的最大要求是，4.0 是一个主要的功能版本，而不是一个实验版本。

# 3.静态类型提示

任何关注 Mypy 项目的人都会看到 BDFL 的参与和支持，但是 Mypy 是 Python 的一个可选的静态类型提示器。

Mypy 旨在结合动态(或“duck”)类型化和静态类型化的优点。

```
def fib(n: int) -> Iterator[int]:
    a, b = 0, 1
    while a < n:
        yield a
        a, b = b, a+b
```

我希望在 Python 4.0 中看到这一点，因为随着越来越多的数据被 JSON 中的 REST-ful 服务消费，像 [schema](https://pypi.python.org/pypi/schema) 这样的库在类型检查输入中非常有用。

# 4.`multiprocessing`的 GPU 故事

使用 3.6(及更低版本)中的 [PyOpenCL](https://mathema.tician.de/software/pyopencl/) 和`multiprocessing`库，您可以利用 GPU 处理能力进行高度并行计算。对于 Python 来说，巩固其作为数据科学、机器学习之王的地位，对 GPU 并行处理的原生支持将是令人敬畏的。

看看 [NumbaPro](https://docs.continuum.io/numbapro/quickstart) ，它使用一个单独的 JIT 引擎来编译为并行原生线程，但它是特定于 NumPy 的。随着 PEP523 (JIT)的支持，本地编译模块可以使用 CPython 在 GPU 中并行执行。

# 5.更多社区贡献

好吧，我说的是 4，但这并不是一个真正的功能。在 4.x 中，我希望看到来自社区的更多更广泛的支持和贡献。随着 CPython 现在出现在 GitHub 上，这可能意味着两件事情中的一件，社区对问题跟踪器的功能进行了争论(参见其他核心语言项目)，或者，这意味着更多的人提出拉请求，修复 bug 并改进 Python 平台支持。

# 就这样吗？

我觉得每个专业/语言项目都有一个“*变化驼峰*”，。净是 1.1 比 2。 [PHP 是 5 比 7](https://www.slideshare.net/andreizm/the-good-the-bad-and-the-ugly-what-happened-to-unicode-and-php-6) ， [Perl 是 5 比 6](http://www.dagolden.com/index.php/2589/perl-5-and-perl-6-are-mortal-enemies/) 。

AngularJS 2？

一旦他们克服了这个变化的障碍，社区就可以安定下来，以创新的名义接受向后兼容性的微小损失，并为变化做计划。如果社区出现分歧，这通常意味着项目的结束，直到更好的东西出现。

Python 4 不需要像 3 一样有大量的突破性变化，但是这些变化是 Python 未来发展所需要的，现在我们可以谈论 4 中有趣的事情，而不是仍然讨论字符串类型。

# ……怎样？

三元运算符？像 C# 6.0 中的`??`。根据 [PEP-308](https://www.python.org/dev/peps/pep-0308/) ，Python 有`x if y else z`，不太可能有特定的操作符。

喜欢我的帖子？请点击💚下面。还有，可以随意评论自己的想法。

[![](img/50ef4044ecd4e250b5d50f368b775d38.png)](http://bit.ly/HackernoonFB)[![](img/979d9a46439d5aebbdcdca574e21dc81.png)](https://goo.gl/k7XYbx)[![](img/2930ba6bd2c12218fdbbf7e02c8746ff.png)](https://goo.gl/4ofytp)

> [黑客中午](http://bit.ly/Hackernoon)是黑客如何开始他们的下午。我们是阿妹家庭的一员。我们现在[接受投稿](http://bit.ly/hackernoonsubmission)并乐意[讨论广告&赞助](mailto:partners@amipublications.com)机会。
> 
> 如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！

![](img/be0ca55ba73a573dce11effb2ee80d56.png)