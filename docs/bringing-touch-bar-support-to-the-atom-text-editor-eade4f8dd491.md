# 为 Atom 文本编辑器带来触摸条支持

> 原文：<https://medium.com/hackernoon/bringing-touch-bar-support-to-the-atom-text-editor-eade4f8dd491>

六周前，我一头扎进了 USB-C 和 Touch Bars 的古怪世界，订购了一台闪亮的新 MacBook Pro。大约从 1997 年开始，我就成为了苹果的用户，跟随苹果走过了黑暗的日子，经历了 CPU 的变化和操作系统的变化。但最近的这一波机器似乎比以往任何时候都引发了更多的抗议，我认为主要是因为许多用户认为苹果显示出放弃其“专业”用户群的强烈迹象。我最终会得到一个完整的 MacBook Pro 评测，但在这篇文章中，我想专注于特定应用程序使用的特定硬件功能。

批评者和客户普遍认为一些新 MacbBook Pro 机型顶部的 touch bar 是一个愚蠢和失败的想法，但就像许多新功能一样，如果做得好，它有它的用途。随着支持它的应用程序数量的增长，它的使用也在增长，我每天使用的一些应用程序仍然在等待支持它。

我经常在工作中使用一个应用程序，GitHub 的文本编辑器 [Atom](https://atom.io/) ，它基于 [Electron](https://electron.atom.io/) 框架。最近版本的框架[引入了对触摸条](https://electron.atom.io/docs/api/touch-bar/)的支持，而 Atom 的 1.19 版本也为 Atom 带来了这种支持。一些勇敢的开发者已经发布了增加 touch bar 功能的包，所以我决定去看看。

# Touchbar 注册表

我将从这个包开始，因为它是另一个包的依赖项，将电子 API 抽象为 Atom。您将它包含在您的包 *package.json* 文件中，并添加如下按钮:

```
consumeTouchBar(touchbarRegistry){ touchbarRegistry.addItem( newTouchBarButton({ label:'Hello Dzone', backgroundColor:'#0288d1', click:()=>console.log('Hey there!') }) ); }
```

这将(无益地)添加一个标签为“Hello Dzone”的按钮，单击该按钮会向 Atom 的控制台记录一条消息。当然，这个包还有更有用的用例，我想作者希望其他开发者会在他们的包中使用它，但是到目前为止，很少有人这样做。

[https://atom.io/packages/touchbar-registry](https://atom.io/packages/touchbar-registry)

# Linter 用户界面

我喜欢 Atom [linter](https://atom.io/packages/linter) 包，以及它支持的所有 linter。在一个窗格中，我可以看到我的代码&文本的各种各样的问题，并可以通过我的方式修复它们。这个包将警告类型的摘要添加到 touch bar 中，但是此时按下按钮没有任何作用。

深入研究 [*touchbarUI.js*](https://github.com/haklop/linter-ui-touchbar/blob/master/lib/touchbarUI.js) 文件，看看这是如何工作的。

![](img/0454a8dcae70af3a71abaf6f00951d12.png)

【https://atom.io/packages/linter-ui-touchbar 

# 触摸栏实用程序

这个包允许您在一个数组中添加一系列按钮、标签和 Atom 动作，例如，默认情况下是:

```
[{ "type":"label", "label":"touch-bar-utility rocks! ����" },{ "type":"button", "label":"��", "clickDispatchAction":"atom-beautify:beautify-editor", "backgroundColor":"#b355d6" },{ "type":"button", "label":"//", "clickDispatchAction":"editor:toggle-line-comments", "backgroundColor":"#4899a8" }]
```

![](img/9a1dfe91bfd51cebf4232e2afb8fb14c.png)

第一个除了显示一个带有图标的标签之外什么也不做，第二个分配一个带有彩色背景的表情图标，点击后运行“美化”动作，第三个切换代码中的注释。它还可以让你为图标，弹出窗口，滑块，间隔等等分配文件。我改变了我的，为自己创造了更多有用的快捷方式:

```
[{ "type":"button", "label":"🔗", "clickDispatchAction":"markdown-writer:insert-link" },{ "type":"button", "label":"💅", "clickDispatchAction":"atom-beautify:beautify-editor" },{ "type":"button", "label":"//", "clickDispatchAction":"editor:toggle-line-comments" }]
```

![](img/cccfbd5c8a88fa9aacdd45828bbfdeb0.png)

到目前为止，这是对我最有用的包，但我希望能够添加实用按钮，如字数统计。

[https://atom.io/packages/touch-bar-utility](https://atom.io/packages/touch-bar-utility)

# 触摸栏

这与上一个包的工作方式类似，添加了一个切换键盘快捷键( *ctrl-alt-o* )，目前缺少一个设置窗格，将配置移动到一个 *lib/config.json* 文件中，这意味着您需要直接在 *~/中找到它。atom/packages/touchbar* 文件夹，我不确定软件包更新将如何工作。一旦进入，选项是相似的，但是稍微清晰一些，默认文件给出了更多的例子。为了创建类似我上面创建的东西，我使用了下面的 JSON，它也添加了一个表情滑块和一个颜色选择器。

![](img/26260db11bfef01c818c31c71bec42c8.png)![](img/585db7057a6907232b4d0fa6d1c31ab0.png)![](img/f865d0f76f4b2f6118e7b303f8c54c78.png)

```
{ "elements":[ { "name":"comment-button", "type":"button", "label":"//", "command":"editor:toggle-line-comments" }, { "name":"beautify-button", "type":"button", "label":"💅", "command":"atom-beautify:beautify-editor" }, { "name":"color-picker", "type":"color-picker" }, { "type":"popover", "label":"😁", "elements":[{ "name":"emoji-scrubber", "type":"scrubber", "label":"😊", "items":"emojis"}] }, { "name":"markdown-links", "type":"button", "label":"🔗", "command":"markdown-writer:insert-link" } ] }
```

[https://atom.io/packages/touchbar](https://atom.io/packages/touchbar)

# 原子触摸栏

另一个包遵循与前两个包相似的思想，但是较少被记录，它定义了 *~/中的动作。atom/packages/atoms-touch bar/lib/touch bars/action . js*并且需要代码和 JSON 配置。这提供了更多的灵活性(和更好的功能)，但是需要更多的关于你在做什么的初步知识。我从文档中得到的印象是，该设置允许您添加不同的“栏”并根据上下文动态调用它们，这是唯一允许这样做的包，并且更符合 touch bar 的精神，但需要一种方法让其他包实现它，使它真正有用。

![](img/d98abcc7a415ee1805ad542f9881a9ac.png)

[https://atom.io/packages/atoms-touchbar](https://atom.io/packages/atoms-touchbar)

# Atom touchbar

这个包并没有声称是可配置的，你应该把它当作一个如何创建你自己的定制包的例子(尽管你可以看到，已经有足够多的 Atom touch bar 包了)。它提供了用于切换命令面板、模糊查找器、linter 面板、Git 面板和注释/取消注释选择的按钮。如果您没有启用任何这些功能，那么按钮将不起作用。

![](img/95aaaa784dcda3194164f714f7e9e6db.png)

[https://atom.io/packages/atom-touchbar](https://atom.io/packages/atom-touchbar)

# Touchbar Git

将 git 信息添加到 touch bar，但它对我不起作用，如果这是你想要的，请查看存储库。

[https://atom.io/packages/touchbar-git](https://atom.io/packages/touchbar-git)

# 提高标准

touch bar 的要点是对上下文敏感，到目前为止，除了`atoms-touchbar`(据我所知)之外，所有的包都是基于特定的用例来修复按钮，而不是基于动态用例。合乎逻辑的下一步是让包开发者都利用一个依赖包，并向他们的包添加功能，然后允许用户从设置窗格切换他们想要使用的按钮。由于文本编辑器用户通常是重度键盘用户，从理论上讲，touch bar 可能是有用的，但它们高度可定制的特性意味着这将是多么真实还有待观察。

*原载于*[](https://dzone.com/articles/bringing-touch-bar-support-to-the-atom-text-editor)**。**