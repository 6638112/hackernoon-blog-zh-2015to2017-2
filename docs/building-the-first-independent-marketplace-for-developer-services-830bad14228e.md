# 构建第一个独立的开发者服务市场

> 原文：<https://medium.com/hackernoon/building-the-first-independent-marketplace-for-developer-services-830bad14228e>

## 创始人访谈

![](img/04dd28625ddd8675da977688f39a656c.png)

> *披露:* [*歧*](https://goo.gl/BEbFYn) *，开发者 marketplace，此前曾赞助黑客正午。* [*使用 code HACKERNOON 获得 25 美元的服务折扣。*](https://goo.gl/BEbFYn)

今天，我们将采访 Manifold 的联合创始人 Matt Creager，以了解他如何看待软件开发的未来，Manifold 的发展方向，以及是什么促使他这样做

**你能分享一下 Manifold 的进展细节吗？自从你最近发布以来，你学到了什么？**

我们无法预测开发人员会对开发人员服务独立市场的前景、任何云上服务的扩展选择以及避免云锁定的一些陷阱的潜力感到多么兴奋。我们被测试期间收到的反馈和反馈惊呆了。

就进展而言，我们很快发现开发人员希望能够管理他们构建的服务，以及他们在 Manifold 上发现的服务。

为此，我们推出了尚未公布的定制服务，以及针对 [Kubernetes](https://docs.manifold.co/docs/kubernetes-2KggAIsPRSGkOoiQqsMEYE) 和 [Terraform](https://docs.manifold.co/docs/terraform-7ejln6n2UwOwwwooo60wMg) 的两个新集成，这两个新集成今天[在](/@etcpeter/9dcf09703e5a)发布。

**你有一个漂亮的** [**狂野的&互动公司故事**](https://story.manifold.co/) **，围绕着一个被用平淡无奇的口粮围起来的社区展开。你认为开发者服务太孤立了吗？这是为什么呢？**

您购买计算产品的同一家公司提供了哪些服务组合？

如果你在 AWS 上，我打赌你用 SES，RDS 等。问题是，我们使用这些服务是因为它们是最好的，还是因为它可以省去我们设置另一个帐户和管理另一个账单的麻烦？

在所有条件相同的情况下，你会根据功能、文档质量、开发者体验、支持等来选择服务。除了在现实世界中——我们的选择受限于我们在哪里购买计算——这是混乱的。

你正在建立一个开发者服务中心。 **在众多用户中，哪种开发者服务组合最常见？您如何确定接下来将添加哪些新的开发人员服务的优先级？**

听到几乎每个项目都包括 [JawsDB Postgres](https://www.manifold.co/services/jawsdb-postgres) 和 [LogDNA](https://www.manifold.co/services/logdna) 你不会感到惊讶。然后，根据项目的不同，我们通常采用某种形式的队列，或者是 Redis Green，或者是 CloudAMQP，由 84 个代码组成。所以通常的嫌疑人。

我们即将推出两项新服务: [Graphcool](https://www.graph.cool/) ，一个 GraphQL BaaS/framework 和 [IOPipe](https://www.iopipe.com/) ，它们提供无服务器监控。我希望你能在 GQL 中看到更多的服务，并很快在平台上看到无服务器服务。

流形上目前提供的每一项服务都是精心挑选的。我们希望与真正关心并致力于开发者体验和开源社区的合作伙伴合作。

如果这描述了你正在构建或使用的服务，[给我写封短信](mailto: matt@manifold.co)！

**流形的商业模式是什么？**

Manifold 对开发者是免费的。我们不对团队访问、访问控制、集成收取额外费用，也不打算这样做。你也不会为你在 Manifold 上购买的服务多付钱。

这可能让你想知道我们如何赚钱？我们也在想同样的事情😂

[**你把自己的工作**](https://www.linkedin.com/in/matthewcreager/) **列为工程和开发者关系，之前你是 Heroku 的开发者关系总监。你如何平衡编写代码和管理大型开发人员社区？退一步说，在你的创始人生活中，一周是什么样的？**

我一直认为编程既是一种职业，也是一种爱好，所以在我成为创始人之前，我从来没有努力去寻找时间来构建东西。那么，生活中的一周是什么样子的呢？

我们刚刚改变了思路，开始扩大规模。Nick Tassone 和我用 React、Redux 和其他一些很酷的库构建了第一个版本的 Manifold 仪表盘，说实话，我怀念那些日子。我们有一个很棒的前端团队，所以我只会碍事😭

现在，我正在组建[开发者关系](https://jobs.alongside.com/details/developer-advocate/614121)和[产品营销](https://jobs.alongside.com/details/senior-manager-product-marketing/647957)团队。

**Heroku 的开发者关系总监是一份很棒的工作。你会给下一个考虑辞去好工作去领导自己的创业公司的工程领导者什么建议？**

当你创办一家公司时，你说服自己，为了戏剧性的效果，关于职业倦怠的故事必须被夸大；他们不是。

你要做出牺牲，越早认识到这一点，你就能越早开始有意识地优先考虑你不愿意牺牲的事情。我的女儿是在我们创建 Manifold 后不久出生的，我的联合创始人兼首席执行官刚刚生了第三个女儿。我们可能不会像我们希望的那样有那么多时间坐在 Xbox 前，但我们不会错过与孩子共度时光的机会。

**你最近募集了一个**[**【1500 万美元 A 轮**](https://blog.manifold.co/coming-out-of-the-fold-announcing-our-15m-series-a-ab184d61351d) **。你从这个筹资过程中学到了什么？你能告诉我们你打算怎么花这笔钱吗？**

开发人员服务的增长可能不足为奇，但市场上对为开发人员或为开发人员设计的产品有着健康的需求。

如果我们要建立一个*独立的*开发者服务生态系统，我们需要一个云不可知的解决方案来管理凭证。我们今天推出的 Terraform 和 Kubernetes 集成是一个开始，但我们相信开发人员应该能够使用他们最喜欢的编排工具、语言和框架，而不用担心管理凭证——因此，我们将继续在集成上投资。

软件开发变化很快。五年后，你认为软件开发人员的日常工作生活会有什么不同？

我认为我们倾向于高估未来两年内的变化，而低估未来五年内的变化。

五年前，我们谈论 web 2.0，我们使用..什么节点的 v0.8.0。如今，企业已经广泛采用了节点和..我们还在 web 2.0 上吗？好吧，有些事情永远不会改变。

五年后？这将会很有趣:

*   一些网络技术的组合将被用于构建 AR、VR 和硬件的界面
*   我们将花相当多的时间在 AR、VR 上——尤其是那些在分布式团队中工作的人
*   自动化测试可以是单元测试、集成测试、可视化回归测试等等。将由机器学习提供动力
*   我们将拥有一个蓬勃发展的开发者服务生态系统，它将不受云的限制，并将被称为多方面的😏
*   将会有一个新的前端框架

**我在** [**上看到你的社区页面**](https://www.manifold.co/community) **，你支持** [**通天塔**](https://opencollective.com/babel) **。你能谈谈巴别塔对你的价值/意义吗？总的来说，你如何支持开源社区？**

我们的前端项目，我们的主页，仪表板等都依赖于巴别塔。Babel 使得在支持每种浏览器的同时使用现代 javascript 成为可能。这是我们希望在服务器上实现的一种奢侈，想象一下，如果你可以在每个平台上使用任何服务？

Manifold 团队中的每个人都有机会支持他们日常使用的项目。我们还试图[开源我们认为可能有用的所有东西](https://github.com/manifoldco?utf8=%E2%9C%93&q=&type=public)——从我们的发布工具 propaved 到一个名为 [promptui](https://github.com/manifoldco/promptui) 的工具，该工具支持 Manifold CLI 中的交互式提示。

Manifold 上的许多提供商在开源社区中也很活跃，我们正在想办法让这些信息出现在 Manifold 上。

> 与[歧管](https://goo.gl/BEbFYn)保持同步:
> 
> 跟随— [@manifoldco](https://twitter.com/manifoldco) ，[歧](https://medium.com/u/ac777fe63007?source=post_page-----830bad14228e--------------------------------)
> 
> 阅读— [流形博客](https://blog.manifold.co/)
> 
> 手表— [Manifoldco](https://go.twitch.tv/manifoldco)
> 
> 喜欢— [Manifolddotco](https://www.facebook.com/manifolddotco/)