# Nodejs 应用程序 Sequelize 入门

> 原文：<https://medium.com/hackernoon/getting-started-with-sequelize-for-nodejs-applications-2854c58ffb8c>

![](img/e5970eea114c0dd5187abb2985ce4b60.png)

# ORM 简介

ORM 或对象关系映射是对象和关系数据库系统之间的映射过程。ORM 就像两个系统之间的接口。ORM 为开发人员提供了一些基本的优势，比如节省时间和精力，更注重业务逻辑。代码是健壮的而不是冗余的。ORM 有助于以有效的方式管理对多个表的查询。最后，ORM(像 [sequelize](http://docs.sequelizejs.com/en/v3/) )能够连接不同的数据库(当从一个数据库切换到另一个数据库时，这很方便)。

# Sequelize 入门

Sequelize 是 Node.js 的一个基于 promise 的 ORM。Sequelize 很容易学习，有几十个很酷的特性，比如同步、关联、验证等等。它还支持 PostgreSQL、MySQL、MariaDB、SQLite 和 MSSQL。我假设您的机器上已经启动了某种形式的 SQL 数据库服务。我目前正在使用 MySQL。

# 装置

Sequelize 可通过 npm 获得。

# 建立连接

Sequelize 确实在 rest API/应用程序和您的 SQL 数据库之间建立了一个连接。要设置两者之间的基本连接:

# 我如何设置我的序列连接？

为了简洁起见，我喜欢将代码分成模块。毕竟， [*一个程序/模块应该做一件事*](https://amandeepmittal.github.io/blog/2017/04/05/The-Node-Way-Philosophy-of-a-Platform/) 的 Unix 哲学是如今用 JavaScript 编写代码(并使用 Node.js 作为服务器端平台)背后的哲学的主要部分。

我从我的应用程序/api 文件夹的根目录中的`config.json` / `config.js`文件开始，在该文件夹中，我定义了设置与数据库的连接所需的一般约束:

如果你喜欢遵循这种模式，你可以在你的`.env`文件中这样做。有关这方面的更多信息，请参见`[dotenv](https://www.npmjs.com/package/dotenv)`。

在定义了配置变量之后，在我的`models/`文件夹中或者我在应用程序级定义数据库中的表模式的地方，我在一个`index.js`文件中创建连接:

注意到我公开了包含每个模型/表模式定义的`db`对象是很重要的。从现在开始，我只需导入`db`对象，使用它对特定的数据库表进行操作。

该设置可以在 [Sequelize CLI](https://github.com/sequelize/cli) 工具的帮助下自动生成，该工具有助于以有效的方式引导新项目(如上所述),并直接从终端处理数据库迁移。

# 结论

Sequelize 是一个功能丰富的 ORM for Node.js。它有一个文档，有时可能不会为您的问题提供直接的解决方案，但总是有 Github 的问题。我喜欢的是它基于承诺的控制流。来自 NoSQL 背景(并使用 MongoDB)，理解 Sequelize 真的花了更少的时间。大多数基于查询的模型与 MongoDB 中的非常相似(尤其是 CRUD 操作)。我正在寻找一个更明亮，更完善的文档和 Sequelize 的支持容易。

**想收到更多像这样的文章吗？订阅我** [**这里**](https://patreon.us17.list-manage.com/subscribe?u=ad4c168a6d5bb975f2f282d54&id=39e959cecd) **。有时，我会向我的订户发送“从未见过”的内容。**

***感谢阅读。如果你觉得这篇文章有用，请点击*** 💚 ***按钮，这样这个故事就能接触到更多的*读者*。如果你想谈论更多，请在***[***Twitter***](https://twitter.com/amanhimself)***上 ping 我。***

[![](img/50ef4044ecd4e250b5d50f368b775d38.png)](http://bit.ly/HackernoonFB)[![](img/979d9a46439d5aebbdcdca574e21dc81.png)](https://goo.gl/k7XYbx)[![](img/2930ba6bd2c12218fdbbf7e02c8746ff.png)](https://goo.gl/4ofytp)

> [黑客中午](http://bit.ly/Hackernoon)是黑客如何开始他们的下午。我们是 [@AMI](http://bit.ly/atAMIatAMI) 家庭的一员。我们现在[接受投稿](http://bit.ly/hackernoonsubmission)并乐意[讨论广告&赞助](mailto:partners@amipublications.com)机会。
> 
> 如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！

![](img/be0ca55ba73a573dce11effb2ee80d56.png)