# UITableView 查看 iOS 11 中的前导和尾随滑动操作🎷

> 原文：<https://medium.com/hackernoon/uitableview-leading-trailing-swipe-actions-in-ios-11-18cb1f267f8a>

每个人都需要一个好的编辑..！！！✂️

![](img/ec3c65655443e7ed91d808bdd41d8892.png)

自从 **iOS 8** ， *Apple* 为我们提供了使用 U *ITableViewDelegate* 方法-t*ableView(_:editActionsForRowAt:)，将我们自己定制的动作添加到 U *ITableView 的*行中。*

> table view(_:editActionsForRowAt:)
> 
> 要求代理显示动作以响应指定行中的滑动。
> 
> 当您想要为表格中的一行提供自定义操作时，请使用此方法。当用户在行中水平滑动时，表格视图会将行内容移到一边以显示您的操作。点击其中一个动作按钮会执行与动作对象一起存储的处理程序块。

现在 iOS 11 已经发布，我们有了一些新的补充🤓表视图的编辑 API。让我们看看这对我们有什么好处。👀

# iOS 11 有什么新功能？

随着**iOS 11***的发布，苹果*推出了两种新方法😮用于处理 ***滑动动作*** 在 *UITableView* 中支持行的前沿和后沿滑动动作，即

1.  ***table view(_:leadingswipeactionconfigurationforrowat:)****—*显示在行的前沿的滑动动作
2.  ***table view(_:trailingswipeactionconfigurationforrowat:)****—*滑动动作显示在行的后沿

这些方法是作为 *UITableViewDelegate 的一部分引入的。*

# 滑动操作—可选

在 **iOS 11** 中处理滑动动作的方法是**可选的😅**，即

1.  如果实现，取代*table view(_:editActionsForRowAt:)*委托方法。
2.  如果没有实现，*table view(_:editActionsForRowAt:)*将作为默认行为被调用。

# 滑动操作-完全滑动

在 **iOS 11** 中，滑动动作默认显示为 ***全滑动*** 🤔，即滑动覆盖 *UITableView 的整个宽度。*

![](img/997314b0dd6d1f36e4b6bb5b321d4408.png)

使用***performsFirstActionWithFullSwipe***属性可以配置*全滑动*行为👏，作为*uiswipeactonconfiguration 的一部分引入—* 在表格的行上滑动时要执行的一组操作。

> 当此属性设置为 true 时，在该行中完全滑动会执行“动作”属性中列出的第一个动作。该属性的默认值为 true。

# 促销

别忘了阅读我的其他文章:

1.  [你一直想知道的关于 iOS 通知的一切](https://medium.freecodecamp.org/ios-10-notifications-inshorts-all-in-one-ad727e03983a)
2.  [拖动&放入收藏&表— iOS 11](/@p.gpt10/drag-it-drop-it-in-collection-table-ios-11-6bd28795b313)
3.  [Swift 4](https://hackernoon.com/everything-about-codable-in-swift-4-97d0e18a2999)中关于 Codable 的一切
4.  [用渐变给它上色——iOS](https://hackernoon.com/color-it-with-gradients-ios-a4b374c3c79f)
5.  [关于 iOS 10 中的今日扩展(Widget)你需要知道的一切](https://hackernoon.com/app-extensions-and-today-extensions-widget-in-ios-10-e2d9fd9957a8)
6.  [UICollectionViewCell 选择变得简单..！！](https://hackernoon.com/uicollectionviewcell-selection-made-easy-41dae148379d)

如果您有任何疑问，请随时发表评论。🙂🙃