# 角度 NgRx:解析路径数据

> 原文：<https://medium.com/hackernoon/angular-ngrx-resolving-route-data-53f88e0b8a5d>

![](img/1206642b7253a18f3aef3bcdf13fa212.png)

在这些 **Angular NgRX** 故事系列中，我将介绍 Angular 应用程序的一些具体部分，这些部分用 NgRX 库实现起来并不明显。

[NgRx](https://github.com/ngrx) 是受 [Redux](https://hackernoon.com/tagged/redux) 启发，针对角度应用的 [RxJS](http://reactivex.io/rxjs/) 供电状态[管理](https://hackernoon.com/tagged/management)。它帮助我们管理应用程序的状态，并且比标准的面向服务的方法有一些好处。

# 短篇小说

如果你懒得阅读一步步的解释，请查看 [**Github 回购示例**](https://github.com/kobvel/ng-ngrx-resolve) 以了解完整的实现。

# 问题

我们正在用 NgRX 方法编写一个 Angular 应用程序。我们希望确保在进入 **Profile** 页面之前，我们有数据显示在该组件中。您可以从官方文档中查看[路由解析器的标准实现。我们将进一步了解如何通过 NgRX 状态管理来实现这一点。](https://angular.io/api/router/Resolve)

/app.routes.ts

## 先决条件

我们来看看`ProfileComponent` ***。*** 来自`ApiService` *的经典订阅可观察被网络调用返回。*不管`ProfileComponent`使用这些数据是为了什么，让我们假设我们需要在进入组件之前确定数据存在。

/profile/profile.component.ts

## 定义减速器和动作

我个人倾向于以面向特征的结构保存文件。因此，我们将把新文件放在与放置`ProfileComponent` 相同的文件夹中。这是我们创建了`profile.reducer.ts`和`profile.actions.ts`之后的一个新的文件夹结构。

配置文件文件夹结构

*   *profile.component.ts*
*   *profile.component.html*
*   *profile.actions.ts*
*   *profile.reducer.ts*

看一看`profile.actions.ts`

/profile/profile.actions.ts

*   `IProfileActions` —我们将用来操作与配置文件实体相关的数据的动作列表。如果需要扩展功能，可以添加`PORFILE_INIT`、`PROFILE_CHANGE`等动作。目前，我们对触发配置文件数据更新的操作没有问题。
*   `UpdateAction` —是我们定义的单一动作类型，用来描述获取新数据的动作(`IProfileData`类型)。

现在让我们在`profile.reducer.ts`中处理这个动作

/profile/profile.reducer.ts

*   `IProfileState` —描述我们将如何扩展基本减速器的应用。
*   `initialState`—`ProfileData`的默认值
*   `reducer` —处理单个动作(更新)以描述在用一些有效负载触发动作后的状态变化

## 延伸根部减速器

/app.state.ts

我们通过将 reducer *对象*添加到 all `reducers` (LOC: 11 `app.state.ts`)来组成应用程序的根状态。

/app.module.ts

最后一件事——我们用在`storeReducers` (LOC: 8 `app.module.ts`)之前创建的 reducers 来定义 StoreModule。

# 设置路径解析器

现在，让我们将 resolver 放在我们希望等待数据加载的路线上。

/app.routes.ts

继续用相应的类创建`profile.resolver.ts`，正如我们在上面的`app.routes.ts`中在 LOC: 8 上命名的那样。这一行表示等待导航到`/profile`路线，直到数据在`ProfileResolver`中被解析，我们马上就要实现。

/profile.resolver.ts

新创建的实现`[Resolve](https://angular.io/api/router/Resolve)`接口的类，它要求我们定义`*resolve*`功能。该函数可以直接返回**承诺**、**可观测**或预期类型。

**功能** `**waitForProfileDataToLoad**`:

*LOC 23:* Subscribe store 监听`profile`对象变化。

*LOC 24:* 从普通`profile`对象中获取唯一的`profileData`映射值

*LOC 25:* 忽略不存在`profileData`的所有触发器

*LOC 26:* take(1) —仅获取第一个值，只要我们需要一个值来解析路径

**功能** `**initProfileData**`:

获取位于商店中的`profile`对象的第一个值。如果没有值:

1.  使用`getProfileData()`获取数据
2.  将其转换为**承诺**(我们只需要一次，所以没有订阅可观察的点)
3.  用我们刚从服务器上得到的`data`派遣`UpdateAction`

## 路由解析器结论

我们通过从服务器获取数据来初始化数据，并为应用程序商店分派新的状态。同时，我们告诉我们的 **resolve** 函数监听商店的变化，并返回 **Observable** 和它将在商店中找到的第一个非空的`ProfileData`。

# 在组件中使用路线数据

最后，我们从路线快照中获取`profileData`，假设**必须**存在于此。

/profile/profile.component.ts

# 结论

NgRx 驱动的应用程序使整个应用程序的数据流过程非常清晰。我希望这能给你一些解决路径分解问题的模式。

这里有几件事你也可以做，以改善你的应用程序体验:

*   `**initProfileData**` **—** 可以移动或移除，如果你有一些不同的地方来初始化数据。
*   您可以实现 spinner 来显示路由解析器的运行情况。[全回购示例](https://github.com/kobvel/ng-ngrx-resolve/blob/master/src/app/app.component.html#L7)中有一些基本实现。
*   如果您希望从另一个地方更改数据，您的组件可以直接订阅 store。在这种情况下，您可以转换`ProfileResolver`以返回**布尔值**而不是数据。可能是掌握这个话题的很好的家庭作业😜。

## [Github 回购示例](https://github.com/kobvel/ng-ngrx-resolve)

> 感谢阅读！如果你想让我写更多类似的故事，推荐这篇文章(点击❤按钮)。
> 
> 把你的想法写在评论里，订阅我的[媒介](/@kobvel)寻找更多故事。