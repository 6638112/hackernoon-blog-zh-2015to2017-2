# 还是用 const 吧！原因如下。

> 原文：<https://medium.com/hackernoon/lets-use-const-here-s-why-6549dcb80708>

*在开发* [*软件*](https://hackernoon.com/tagged/software) *的时候，我们大部分时间都花在了阅读* [*代码*](https://hackernoon.com/tagged/code) *上。ES6 提供了* `*let*` *和* `*const*` *作为变量声明的新版本，这些语句的部分价值在于它们可以指示如何使用变量。当阅读一段代码时，其他人可以从这些信号中得到线索，以便更好地理解我们做了什么。像这样的线索对于减少人们花在解释一段代码上的时间是至关重要的，因此我们应该尽可能地利用它们。*

![](img/e44ad75a599c9966a59e70a856aba960.png)

一个`*let*`声明表明，由于时间死区规则，变量不能在声明前使用。这不是惯例，而是事实:如果我们试图在到达变量的声明语句之前访问它，程序将会失败。这些语句是块范围的，而不是函数范围的；这意味着我们需要阅读更少的代码，以便完全掌握如何使用一个`*let*`变量。

`const`语句也是块范围的，它也遵循 TDZ 语义。好处是`const`绑定只能在声明期间被赋值。

请注意，这意味着变量绑定不能改变，但这并不意味着值本身在任何方面都是不可变的或恒定的。引用一个对象的`const`绑定不能在以后引用不同的值，但是底层对象确实可以变异。

除了由`let`提供的信号之外，`const`关键字表明一个变量绑定不能被重新分配。这是一个强烈的信号。你知道价值会是多少？您知道，由于块范围的原因，绑定不能在其直接包含的块之外被访问；您知道，由于 TDZ 语义，绑定在声明之前不会被访问。

你只需阅读 `*const*` *声明语句就能知道所有这些，无需扫描该变量的其他引用。*

由`let`和`const`提供的约束是一种使代码更容易理解的强大方法。试着在你写的代码中增加尽可能多的约束。限制一段代码含义的声明性约束越多，将来人们阅读、解析和理解一段代码就越容易、越快。

当然，`const`声明比`var`声明有更多的规则:块范围、TDZ、声明时赋值、无重赋值。而`var`语句只表示函数作用域。然而，规则计数并没有提供太多的洞察力。最好根据复杂性来衡量这些规则:规则是增加了还是减少了复杂性？在`const`的例子中，块作用域意味着比函数作用域更窄的作用域，TDZ 意味着我们不需要为了在声明前发现用法而从声明向后扫描作用域，赋值规则意味着绑定将总是保持相同的引用。

受约束的语句越多，代码就越简单。随着我们对语句的含义增加约束，代码变得更加不可预测。这是静态类型的程序通常比动态类型的程序更容易阅读的最大原因之一。静态类型对程序编写者来说是一个很大的限制，但是它也对程序如何被解释有很大的限制，使得它的代码更容易理解。

考虑到这些论点，建议您尽可能使用`const`，因为它是给我们提供最少可能性的陈述。

```
if (condition) {
  // can't access `isReady` before declaration is reached
  const isReady = true
  // `isReady` binding can't be reassigned
}
// can't access `isReady` outside of its containing block scope
```

当`const`不是一个选项时，因为变量需要稍后被重新分配，我们可以求助于`let`语句。使用`let`具有`const`的所有优点，除了变量可以被重新分配。为了递增计数器、翻转布尔标志或推迟初始化，这可能是必要的。

考虑下面的例子，我们取一些兆字节并返回一个字符串，比如`1.2 GB`。我们使用`let`，因为如果满足条件，值需要改变。

```
function prettySize (input) {
  let value = input
  let unit = `MB`
  if (value >= 1024) {
    value /= 1024
    unit = `GB`
  }
  if (value >= 1024) {
    value /= 1024
    unit = `TB`
  }
  return `${ value.toFixed(1) } ${ unit }`
}
```

增加对 Pb 的支持需要在`return`语句前增加一个新的`if`分支。

```
if (value >= 1024) {
  value /= 1024
  unit = `PB`
}
```

如果我们想让`prettySize`更容易扩展新单元，我们可以考虑实现一个`toLargestUnit`函数，为任何给定的`input`及其当前单元计算`unit`和`value`。然后我们可以使用`prettySize`中的`toLargestUnit`来返回格式化的字符串。

下面的代码片段实现了这样一个功能。它依赖于支持的`units`列表，而不是为每个单元使用一个新的分支。当输入`value`至少是`1024`并且有更大的单元时，我们将输入除以`1024`并移动到下一个单元。然后我们用更新的值调用`toLargestUnit`，这将继续递归地减少`value`，直到它足够小或者我们达到最大的单元。

```
function toLargestUnit (value, unit = `MB`) {
  const units = [`MB`, `GB`, `TB`]
  const i = units.indexOf(unit)
  const nextUnit = units[i + 1]
  if (value >= 1024 && nextUnit) {
    return toLargestUnit(value / 1024, nextUnit)
  }
  return { value, unit }
}
```

引入 petabyte 支持过去涉及一个新的`if`分支和重复逻辑，但现在只需要在`units`数组的末尾添加`PB`字符串。

`prettySize`函数变得只关心如何显示字符串，因为它可以将其计算卸载给`toLargestUnit`函数。这种关注点的分离也有助于产生更可读的代码。

```
function prettySize (input) {
  const { value, unit } = toLargestUnit(input)
  return `${ value.toFixed(1) } ${ unit }`
}
```

每当一段代码有需要重新分配的变量时，我们应该花几分钟思考是否有更好的模式可以解决同样的问题而不需要重新分配。这并不总是可能的，但在大多数情况下可以完成。

一旦你找到了一个不同的解决方案，把它和你以前的方案进行比较。确保代码可读性确实得到了提高，并且实现仍然正确。单元测试在这方面很有帮助，因为它们可以确保你不会两次遇到同样的缺点。如果重构的代码在可读性或可扩展性方面看起来更差，请仔细考虑返回到以前的解决方案。

考虑下面的例子，我们使用数组连接来生成`result`数组。这里，我们也可以通过简单的调整从`let`变为`const`。

```
function makeCollection (size) {
  let result = []
  if (size > 0) {
    result = result.concat([1, 2])
  }
  if (size > 1) {
    result = result.concat([3, 4])
  }
  if (size > 2) {
    result = result.concat([5, 6])
  }
  return result
}
makeCollection(0) // <- []
makeCollection(1) // <- [1, 2]
makeCollection(2) // <- [1, 2, 3, 4]
makeCollection(3) // <- [1, 2, 3, 4, 5, 6]
```

我们可以用接受多个值的`Array#push`来代替重新分配操作。如果我们有一个动态列表，我们可以使用 spread 操作符来推送尽可能多的`...items`。

```
function makeCollection (size) {
  const result = []
  if (size > 0) {
    result.push(1, 2)
  }
  if (size > 1) {
    result.push(3, 4)
  }
  if (size > 2) {
    result.push(5, 6)
  }
  return result
}
makeCollection(0) // <- []
makeCollection(1) // <- [1, 2]
makeCollection(2) // <- [1, 2, 3, 4]
makeCollection(3) // <- [1, 2, 3, 4, 5, 6]
```

当你确实需要使用`Array#concat`时，你应该使用`[...result, 1, 2]`来代替，这样会更简单。

我们要讨论的最后一个案例是重构。有时，我们编写类似下一个代码片段的代码，通常是在一个更大的函数的上下文中。

```
let completionText = `in progress`
if (completionPercent >= 85) {
  completionText = `almost done`
} else if (completionPercent >= 70) {
  completionText = `reticulating splines`
}
```

在这些情况下，将逻辑提取到一个纯函数中是有意义的。这样，我们避免了较大函数顶部附近的初始化复杂性，同时将所有关于计算完成文本的逻辑聚集在一个地方。

下面这段代码展示了我们如何将完成文本逻辑提取到它自己的函数中。然后我们可以去掉`getCompletionText`，使代码在可读性方面更加线性。

```
const completionText = getCompletionText(completionPercent)
// ...
function getCompletionText(progress) {
  if (progress >= 85) {
    return `almost done`
  }
  if (progress >= 70) {
    return `reticulating splines`
  }
  return `in progress`
}
```

在`const`vs`let`vs`var`中你的立场是什么？

> 这篇文章摘自我正在写的一本书[实用 ES6](https://ponyfoo.com/books/practical-es6/chapters#toc) 。它在网上以 HTML 格式公开发布，在 GitHub 上以 AsciiDoc 格式发布。它最近**筹集了超过 12，000 美元***💰*在 Indiegogo 上资助[，并由发行商 O'Reilly Media 作为](https://www.indiegogo.com/projects/modular-javascript-a-pragmatic-js-book-series#/)[提前发布](http://shop.oreilly.com/product/0636920047124.do)。

*最初发表于*[*ponyfoo.com*](https://ponyfoo.com/articles/var-let-const)*。*

[![](img/50ef4044ecd4e250b5d50f368b775d38.png)](http://bit.ly/HackernoonFB)[![](img/979d9a46439d5aebbdcdca574e21dc81.png)](https://goo.gl/k7XYbx)[![](img/2930ba6bd2c12218fdbbf7e02c8746ff.png)](https://goo.gl/4ofytp)

> [黑客中午](http://bit.ly/Hackernoon)是黑客如何开始他们的下午。我们是 [@AMI](http://bit.ly/atAMIatAMI) 家庭的一员。我们现在[接受投稿](http://bit.ly/hackernoonsubmission)，并乐意[讨论广告&赞助](mailto:partners@amipublications.com)机会。
> 
> 如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！

![](img/be0ca55ba73a573dce11effb2ee80d56.png)