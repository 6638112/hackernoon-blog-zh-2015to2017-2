# 什么是 DevOps，为什么您应该拥有它

> 原文：<https://medium.com/hackernoon/what-is-devops-and-why-i-should-have-it-e60f1ee446d2>

到本文结束时，您将对 DevOps 方法有一个大致的了解。我将描述 DevOps 在我们公司是如何实现的，以及坚持 DevOps 实践来开发软件为什么如此重要。

![](img/4bfbed4122539c2df831e99386b76e14.png)[![](img/7b05be6e4bb5a57d333e7b4d4316c7a2.png)](https://djangostars.com/services/python-django-development/?utm_source=medium&utm_medium=hackernoon.com&utm_campaign=whatisdevops&utm_content=banner_services)

# DevOps 是什么？

把事情说清楚——devo PS 是一种方法论。这种方法的理念是创造一种新的思维模式。开发人员和运营人员共同努力实现共同目标的心态。

![](img/b2f6900824e657702f2245e8dddf7e89.png)

有时它会被错误地与工具或角色混淆。它不是工具，尽管它使用工具链来自动化软件交付和部署。这也不是一个职位，尽管运营和开发人员都应该扩大他们的责任。

> [继续在 Django Stars 博客](https://djangostars.com/blog/what-is-devops/?utm_source=medium&utm_medium=hackernoon.com&utm_campaign=whatisdevops&utm_content=continuereading)上阅读这篇关于 devops 的文章。

# 没有 DevOps

传统上，或者说 10 年前，开发团队可以大致分为开发人员——知道如何编写代码的人，和操作人员。对于那些仍然想知道这些操作究竟是谁的人:
他们是管理员——系统管理员、网络管理员、数据库管理员和所有其他了解基础设施的人。

所以……运营部门对保持稳定感兴趣，以最小化软件冲突的机会。而开发人员最关心的是新特性、新版本，当然还有错误修复。上述所有问题的主要问题是缺乏合作和沟通。结果，软件不能以期望的速度交付。

# 使用 DevOps

现在，把开发人员和运营人员合并成一个团队，用相互支持的理念来驱动他们。你得到了 DevOps。
DevOps 方法允许频繁地交付软件，只需少量的迭代更改。

**好处:**

*   用户经常收到新功能和更新。您的客户会更频繁地收到新功能和错误修复。你的公司变得更有竞争力。
*   尽量减少暴行的机会。即使发生了令人发指的事情，一切都可以在几分钟内修复(有时只需刷新一次)，这样用户甚至不会注意到有什么地方出了问题。

# 此外

除了文化部分，DevOps 方法之所以成为可能，要归功于以下方法:

*   **代码为**的基础设施是一种可以自动配置服务器的方法。这里的想法是把你的服务器基础设施想象成一个抽象的概念。这很简单，因为今天的许多服务器都是基于云的。下一步是在配置文件中简单描述服务器的配置。好处如下:你可以快速配置任意数量的服务器，所有的配置都用相同的代码记录。
*   微服务架构是软件开发中的一种方法，将应用程序分成松散耦合的部分。想象一下，你有一个现代社交媒体消息应用程序，包含聊天、故事、语音通话、机器人等等。所有这些都可以像独立的迷你应用程序一样开发。这种方法使得维护、测试和重用部分应用程序变得更加容易。另一方面，开发过程变得更加复杂，因为代码由更多的部分组成。开发人员应该考虑应用程序中服务之间的通信。
*   DevOps 热爱**自动化**。现代飞速发展的软件开发行业需要自动化。每天都有几十个持续集成的版本排队等待部署，你不可能手工测试它们。这同样适用于服务器配置。
*   开发人员利用**工具**的武器库。如果没有像 Jenkins、Ansible、Docker 或 Puppet 这样的工具，DevOps 的大多数方面都是不可能的。尽管如此，工具只是促进了过程，并允许实现目标。知道如何创建 Docker 容器并不意味着你是 DevOps 俱乐部的一员。

![](img/d21c739707ddf75fffe90b71c4f5f586.png)

# 为什么需要 DevOps？

这完全取决于项目的规模。如果你的目标是发布一个最小可行产品(MVP)来测试你的想法，很有可能你可以不用 DevOps 实践。如果你的软件已经发布了几个版本，是时候开始考虑规模和竞争力了——想想 DevOps。

从头开始设置 DevOps 环境需要更多的时间。在早期阶段，人们会感到困惑，为什么要花费额外的时间和金钱来设置 Docker 和 Ansible。答案很简单——现在需要多花一点时间，因此，从长远的角度来看，要节省时间。

# 我们如何实现 DevOps

在 Django Stars 中，实施在很大程度上取决于我们打交道的客户。以下是最常见的请求“类型”列表:

*   想要构建 MVP 的客户

这是最常提出的要求，原因很简单，因为有一天，任何公司都过了 MVP 的初级阶段。对于这样的小项目来说，增加一个发布工程师或系统管理员将会是一种矫枉过正和浪费客户金钱的行为。这些项目通常由开发人员自己部署。

我们试图说服客户，最好在这个早期阶段就播下 DevOps 的种子，并坚持 DevOps 的常见做法，如使用微服务构建应用程序。在大多数情况下，开发人员还将部署和维护产品。它允许最小化花费。产品本身是根据客户偏好构建的，但即使客户更喜欢 monolith 类型的应用程序，而不是微服务，我们仍然为未来实施微服务奠定了良好的基础。

*   已经拥有由他人开发的项目的一部分的客户

很多时候是最难的情况。我们喜欢避开那些已经被别人启动，并且由于某种原因而被放弃的项目。尽管如此，当项目有足够的前景去冒险时，还是有一些罕见的例外。案例完全取决于客户。有时，我们开发的应用程序考虑到了最佳 DevOps 实践，并要求将应用程序从 Python 2 升级到 Python 3。而另一个则需要从头开始完全重写。

*   拥有成熟应用程序的长期客户和合作伙伴

这个案例与一个“完美的 DevOps 世界”最为相关。我们的软件工程师与客户的运营或开发工程师紧密合作。
每当我们收到实施新功能的请求时，我们的开发人员都会向客户的运营团队提供以下信息:

*   必需的依赖关系
*   预期负载功能可以处理
*   受即将推出的功能影响的服务

运营团队根据开发人员的要求安装服务器。这反过来又使我们的开发人员今后的生活更加轻松。

# 工具链

无论我们处理什么项目，这些都是我们日常使用的工具:

![](img/f086d13bbf86b9abe4ffff053b8175ed.png)

*   集装箱化码头工人。查看我们下面的分步指南:
*   [詹金斯](https://jenkins.io/)和[圈 CI](https://circleci.com/) 持续集成和交付。我们的指南:
*   [哨兵](https://sentry.io/)进行实时误差跟踪
*   [ELK](http://www.elkmonitor.com/) 用于度量和记录
*   [Terraform](https://www.terraform.io/) 和 [Ansible](https://www.ansible.com/) 用于服务器供应和基础设施
*   [Nagios](https://www.nagios.org/) 和[新遗迹](https://www.newrelic.com/)进行监控

你可以在我们的博客上查看我们的 [CI 对比](https://djangostars.com/blog/continuous-integration-circleci-vs-travisci-vs-jenkins/?utm_source=medium&utm_medium=hackernoon.com&utm_campaign=whatisdevops&utm_content=cicomparison)和 [Docker 教程](https://djangostars.com/blog/what-is-docker-and-how-to-use-it-with-python/?utm_source=medium&utm_medium=hackernoon.com&utm_campaign=whatisdevops&utm_content=dockertutorial):

[](https://djangostars.com/blog/continuous-integration-circleci-vs-travisci-vs-jenkins/?utm_source=medium&utm_medium=hackernoon.com&utm_campaign=whatisdevops&utm_content=cicomparison) [## 持续集成。切尔莱西 vs 特拉维斯奇 vs 詹金斯

### 本文向您介绍了持续集成的基础知识，并比较了 3 个最流行的 CI 系统:CircleCI…

djangostars.com](https://djangostars.com/blog/continuous-integration-circleci-vs-travisci-vs-jenkins/?utm_source=medium&utm_medium=hackernoon.com&utm_campaign=whatisdevops&utm_content=cicomparison) [](https://djangostars.com/blog/what-is-docker-and-how-to-use-it-with-python/?utm_source=medium&utm_medium=hackernoon.com&utm_campaign=whatisdevops&utm_content=dockertutorial) [## 什么是 Docker 以及如何在 Python 中使用它(教程)

### 这是一个介绍 Docker 容器的教程。到本文结束时，你将知道如何在…上使用 Docker

djangostars.com](https://djangostars.com/blog/what-is-docker-and-how-to-use-it-with-python/?utm_source=medium&utm_medium=hackernoon.com&utm_campaign=whatisdevops&utm_content=dockertutorial) 

DevOps 是一种将开发人员和运营人员结合起来的方法，与传统的孤岛式方法相比，它可以更高效地开发和交付软件。团队不仅限于开发人员和 IT 运营人员。在大多数情况下，这种方法也在 QA、PMs 和安全专家中传播。在早期阶段实施开发运维的公司为可扩展的增长创造了基础。

[![](img/a91a9ba82290b94c1a9655fbc07e947b.png)](https://djangostars.com/services/python-django-development/?utm_source=medium&utm_medium=hackernoon.com&utm_campaign=whatisdevops&utm_content=banner_end)

> 文章由[**VOLODYMYR DMYTRIIEV**](https://djangostars.com/blog/author/volodymyr/)—[Django Stars](https://djangostars.com)的技术内容撰稿人撰写。[这篇关于 devops 的文章最初发布在 Django Stars 的博客](https://djangostars.com/blog/what-is-devops/?utm_source=medium&utm_medium=hackernoon.com&utm_campaign=whatisdevops&utm_content=originallyposted)上。
> 
> 特别分享给 [Hackernoon](https://medium.com/u/4a8a924edf41?source=post_page-----e60f1ee446d2--------------------------------) 社区。

我们随时欢迎您提出问题，分享您想阅读的话题！

> *如果你觉得这篇文章有用，请点击👏下面的按钮:)*

[![](img/50ef4044ecd4e250b5d50f368b775d38.png)](http://bit.ly/HackernoonFB)[![](img/979d9a46439d5aebbdcdca574e21dc81.png)](https://goo.gl/k7XYbx)[![](img/2930ba6bd2c12218fdbbf7e02c8746ff.png)](https://goo.gl/4ofytp)![](img/be0ca55ba73a573dce11effb2ee80d56.png)