# 如何移植遗留代码

> 原文：<https://medium.com/hackernoon/how-to-graft-react-on-to-legacy-code-3ad86e55e2f1>

![](img/d75b3d932f8700b4c87f6861654bc81b.png)

有很多活的项目是使用旧的 web 技术栈构建的。从头开始通常是不可能的，升级代码库可能是一项艰巨的任务，尤其是在没有单元测试或合适的构建工具的情况下。本文讨论并演示了一个简单的工作演示，通过使用 Redux 和 [Ducks++](/@DjamelH/ducks-redux-reducer-bundles-44267f080d22) 模式，将 Backbone/jQuery 应用程序与 [React](https://hackernoon.com/tagged/react) 集成。如果你没有听说过 Ducks，它基本上是一个简单的设计模式，用于模块化你的 Redux 代码。

# 该应用程序

在 [CodePen](https://codepen.io/dhassaine/pen/ybwqQZ?editors=1011) 可以找到一个现场工作演示，整个项目也可以在 [GitHub](https://github.com/dhassaine/legacy2react) 上找到。app 演示了两个开关:一个是用 Backbone/jQuery 实现的，一个是用 React 实现的；然而，两者都是通过主干模型和 Redux 存储同步的。React 代码被打包并放入到传统的应用程序中——实际上，它是一个可以立即调用的函数表达式，行为就像一个库。

# 反应模块

遗留应用程序仍然处于主导地位，负责构建和安装 React 代码:

```
var reactToggleApp = window.reactModule.make(
  { 
    el: document.getElementById('react-module') 
  }
);reactToggleApp.render();
```

React 代码可通过一个工厂函数获得，该函数是全局可用的。这允许我们传入必要的回调和选项，例如错误处理机制或翻译功能。React 模块还需要一个 DOM 元素来挂载。运行工厂函数后，将返回一个具有以下接口的对象:

```
{
  render,
  destroy,
  store,
  ducks
}
```

渲染和销毁允许父应用程序启动和删除 react 应用程序。Redux 存储和 ducks 模块是实现两个世界同步的关键。

# 这座桥

![](img/08e0b3294d7bdcbe82edbd846c63a75e.png)

工厂函数公开了 Redux 存储，这允许我们订阅存储中的任何更改，并将这些更改传播到主干模型。类似地，对主干模型的更改可以通过分派适当的动作传播到 Redux 存储。实现这一点的诀窍是遵循 Ducks++模式，该模式将动作和选择器捆绑在一起。注意在下面的代码中，我们使用`actionCreators`和`selectors`将主干模型的属性`on`同步到`keyValues`鸭子的属性`toggle` 。

```
model.on('change:on', function (model, value) {
  window.reactModule.store.dispatch(
    window.reactModule.ducks.keyValues.actionCreators.setValue(
      'toggle', value
  ));
});window.reactModule.store.subscribe(function() {
  var state = window.reactModule.store.getState();
  var value = window.reactModule.ducks.keyValues.selectors.getValue(
    state, 'toggle'); model.set('on', value);
});
```

我们现在有能力用 react 模块替换遗留组件，并最终替换所有遗留代码。

# 结论

考虑到我们正在将一个全新的代码库合并到一个遗留系统中，这种方法出人意料地直接。我们甚至可以在一个单独的存储库中实现 React 代码，并像对待一个绿地项目一样对待它——面对现实吧，谁不想在绿地上工作呢！？

请记住，如果您想尝试本文中的代码，请随意克隆/派生我的 [repo](https://github.com/dhassaine/legacy2react) 。

*如果你觉得这篇文章有用/鼓舞人心* ***点击*** 💚这样其他人也可以享受。

感谢您的宝贵时间！关注我的[*Twitter*](https://twitter.com/DjamelH)*和*[*LinkedIn*](https://www.linkedin.com/in/dhassaine/)*。*

[![](img/50ef4044ecd4e250b5d50f368b775d38.png)](http://bit.ly/HackernoonFB)[![](img/979d9a46439d5aebbdcdca574e21dc81.png)](https://goo.gl/k7XYbx)[![](img/2930ba6bd2c12218fdbbf7e02c8746ff.png)](https://goo.gl/4ofytp)

> [黑客中午](http://bit.ly/Hackernoon)是黑客如何开始他们的下午。我们是阿美族家庭的一员。我们现在[接受投稿](http://bit.ly/hackernoonsubmission)并乐意[讨论广告&赞助](mailto:partners@amipublications.com)机会。
> 
> 如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！

![](img/be0ca55ba73a573dce11effb2ee80d56.png)