# React 死了。反应万岁！

> 原文：<https://medium.com/hackernoon/the-react-is-dead-long-live-the-react-e97eea715f1c>

![](img/5066f48b225038250e24d6d0a44caa84.png)

## ***警告:本帖已过时。React 现在是麻省理工许可的了。***

*让我们找到最好的“类反应”库，不要成为脸书“专利战”的下一个受害者。或者可能成为。*

# 介绍

> TL；脸书可以使用自己的开源库作为专利战的武器。

来自脸书官方的解释:

> 专利授权说，如果你打算使用我们根据它发布的软件，如果你起诉我们侵犯专利，你就失去了我们的专利许可。

最好先看一下 [**官方 FB 回复**](https://code.facebook.com/posts/112130496157735/explaining-react-s-license/) 、反应回购****这个帖子里的**解释了所有的事情。******

> ******UPD** :看了一些推文/信息后，我发现有某种拥有**专利**的“黑魔法”。FB 必须公开相关专利，以消除这些限制。而且似乎所有“类似 React”的库也申请了专利，因为它们是最初 [React](https://hackernoon.com/tagged/react) 的衍生物。我猜，FB 在“基于组件”的模型或类似的东西上有专利。我不是律师，这只是我的假设。
> UPD2: [又一个假设。UPD3:还有，很奇怪为什么这种冲突只是在最近几天才流行起来。](/@vladimirmetnew/i-absolutely-agree-with-you-because-react-itself-is-a-composition-of-different-well-known-design-a4e6e509f951)[解释 FB 执照的帖子出现在一年多以前。](https://react-etc.net/entry/your-license-to-use-react-js-can-be-revoked-if-you-compete-with-facebook)****

# ****下一个英雄****

****Vue.js(MIT license)、Angular(MIT license)、Riot(MIT license)、Ember(MIT license)和其他框架都很棒，但我们只考虑“类似 React”的库，它们提供众所周知的“基于组件”的范例，具有(几乎)相同的 API、JSX 支持，并且已经有了来自社区的反馈。****

# ****预行动(麻省理工学院许可证)****

> ****具有相同 ES6 API 的快速 3kb 反应备选方案。组件和虚拟 DOM。****

****[](https://github.com/developit/preact) [## 发展/预测

### preact — ⚛️ Fast 3kb React 替代产品，采用相同的 ES6 API。组件和虚拟 DOM。

github.com](https://github.com/developit/preact) 

每个人都知道 Preact。如果你不知道什么是 Preact，那么看看这个简单的等式:

> Preact + "preact-compat" = React

是的，您仍然可以使用 Preact 和`[preact-compat](https://github.com/developit/preact-compat)`来处理 React。或许，你甚至不需要`preact-compat`，因为 Preact 已经有了自己的库，像`[preact-router](https://github.com/developit/preact#libraries--add-ons).`一样，Preact 有来自社区的强大支持，许多例子、库和插件。

# 地狱(麻省理工学院许可证)

> 用于构建现代用户界面的速度极快、反应灵敏的 JavaScript 库

[](https://github.com/infernojs/inferno) [## 地狱/地狱

### inferno——一个用于构建现代用户界面的速度极快、类似 React 的 JavaScript 库

github.com](https://github.com/infernojs/inferno) 

[魔族真的是**快**。](https://localvoid.github.io/uibench/)且猜猜，我们为什么要喜欢魔族？是的，因为它是一个现代的快速轻量级库+因为这个简单的等式:

> 地狱+地狱-兼容=反应

Inferno 和 Preact 之间有一些关键区别:

1.  与 React 和 Preact 不同，Inferno 在功能组件上有生命周期事件
2.  Inferno 的服务器端渲染速度比 React 快 5 倍左右，比 Angular 2 快 3 倍左右，比 Preact 和 Vue 快 1.5 倍左右。
3.  与 Preact 和其他类似 react 的库不同，Inferno 控制了输入/选择/文本区域元素的组件

> 很可能，我会选择《地狱》作为我的下一个项目。

# 麻省理工学院许可证

> 使用纯函数和虚拟 DOM 呈现界面

[](https://github.com/anthonyshort/deku) [## anthonyshort/deku

### deku——使用纯函数和虚拟 DOM 呈现界面

github.com](https://github.com/anthonyshort/deku) 

来自官方文件的精彩描述:

> Deku 不使用类和本地状态，而是使用函数，并将所有状态管理和副作用的责任推给像 [Redux](http://redux.js.org/) 这样的工具。它还旨在只支持现代浏览器，以保持简单。

*从我自己的经验来看:依靠 Flux/Redux 比使用组件的状态更好。*

还有[Rax(BSD-3 license:f b+Alibaba)](https://github.com/alibaba/rax)、 [Bobril](https://github.com/Bobris/Bobril) 、 [DIO](https://dio.js.org/) 、 [Imba](http://imba.io/home) 、 [vidom](https://github.com/dfilatov/vidom) 等类似 API 的库、框架、插件，但都没那么流行。

感谢您阅读这篇文章😈
Github:[@ met new](https://github.com/Metnew)
Twitter:[@ themet new](https://twitter.com/theMetnew)****