# 与 Andrew Chalkley 一起使用 thingsSDK 研究微控制器上的 Javascript

> 原文：<https://medium.com/hackernoon/diving-into-javascript-on-microcontrollers-with-thingssdk-with-andrew-chalkley-c1ba50a4ba25>

安德鲁·查尔克利(Andrew Chalkley)是《创客秀》的主持人、 [@thingsSDK](https://twitter.com/thingsSDK) 的项目负责人，也是一名教师[@树屋](https://twitter.com/treehouse)。主持采访的是[塔隆·福克斯沃斯](http://twitter.com/anaptfox)，洛杉矶[的开发者传道者。](http://losant.com)

![](img/b6cc87fa4b2017ffdc1375314799ff18.png)

在本次对话中，我们重点讨论了 [thingsSDK](http://thingssdk.com/) ，这是一套工具，供 web 开发人员使用 [Javascript](https://hackernoon.com/tagged/javascript) 创建互联网连接的硬件项目。我们还涵盖:

*   Andrew 如何开始使用硬件
*   硬件和物联网的 3 个基本问题
*   为什么在构建物联网应用时应该使用 Javascript
*   为硬件构建 Javascript 平台的挑战
*   如何开始并为 thingsSDK 做贡献

# 安德鲁，你能介绍一下你自己的背景吗？

Taron Foxworth: 在我们深入讨论 thingsSDK 之前，你能介绍一下你自己的背景吗？

安德鲁·朝克莱:当然。白天我在网络学校[树屋](https://teamtreehouse.com/chalkers)教书，在那里我教授 JavaScript 和 SQL 等课程。晚上，我在修修补补:)我主持[创客秀](https://www.youtube.com/channel/UCtZkss5RBrUWLfrrieOJheg)，旨在打破进入创客运动的壁垒。我也是 thingsSDK 的项目负责人。

在我职业生涯的大部分时间里，我都在与计算机打交道。我是自学的，从事过 PHP、Ruby、Java 和 Objective-C 的开发工作，目前稳定在 JavaScript:)

**Taron Foxworth:** 自学成才的百事通！郑重声明，那个创客秀太棒了！《3D 打印入门》这一集让我迷上了 3D 打印。

# 是什么让你对成为一名创客感兴趣？

安德鲁·朝克莱:这些年来，我已经学习了很多编程语言。我不再觉得有挑战性了。在屏幕上推动像素的兴奋已经失去了吸引力。

所以我想拓展自己，涉足硬件。我觉得在我目前极限的边缘，我最能茁壮成长。硬件是一个出口。

Taron Foxworth: 所以，你转向了物质世界。尼斯（法国城市名）

# 你是从什么硬件或框架开始的？

**安德鲁·朝克莱:**我一开始用的是 [Arduino](http://arduino.cc) 。我学习的最好方法是让自己沉浸在我想学的东西的语言中。我在网上看了很多 Adafruit 视频和其他创客视频。

然后，我写了一篇文章“[Arduino](http://forefront.io/a/beginners-guide-to-arduino/)绝对初学者指南”。它仍然有很多流量，人们喜欢它，它似乎与初学者有共鸣——因为我也是初学者:)

塔隆·福克斯沃斯:是的！我喜欢这样。初学者也要写。听起来似乎 Arduino + [Adafruit](https://www.adafruit.com/) 是一个完美的硬件入门套件。这让我们想到了一些事情。

# 你能告诉我们什么是 thingsSDK，以及你是如何想出这个主意的吗？

**Andrew Chalkley:** 硬件和物联网存在三个基本问题。

*   首先，这些开发板的成本相当高，尤其是如果您想将 Arduino 连接到互联网。在 50 到 90 美元之间。
*   其次，编程语言对用户并不友好。C 和 C++对新的硬件爱好者来说有很多挑战，即使你一直在用更现代的语言编程。
*   第三，即使你能在设备上找到一种编程语言，也没有适合专业开发人员的现代开发工作流程。你不得不使用笨重的 ide。

这种挫折导致了事情的发展。我在俄勒冈州波特兰市运营一个 JavaScript 和物联网小组。我们大约有 500 人在册，每月有 30-40 人出现。在一次聚会结束时，我发泄了对以上几点的不满。我的一个好朋友克雷格·丹尼斯主动提出和我一起解决这个问题。

第一个问题——成本。我们希望能够向尽可能多的人开放。ESP8266 是一款内置 wifi 的廉价微控制器模块。开发板的价格在 2-4 美元之间！

ESP8266 可以运行 Lua，并且可以有 Arduino 草图闪现到其上。去年这个时候，MicroPython 正在做一个 Kickstarter，准备移植到董事会。Espruino 的 Gordon Williams 开始为 ESP8266 发布他的运行时二进制文件。你可以把 Espruino 想象成微控制器的节点。

我们创建了一个名为 [Flasher.js](http://forefront.io/a/introducing-flasher-js/) 的 GUI，为您基于 ESP8266 的开发板(如 NodeMCU 和 Adafruit Feather HUZZAH)提供一键安装。

Flasher.js 减少了开发人员在设备上获取 JavaScript 所需的时间和摩擦。

为了解决第三个也是最后一个问题，现代工作流，我想创建一个 CLI 实用程序，它足够固执己见，对于当前的 JavaScript web 开发人员来说很容易。他们不需要学习任何新东西，他们需要知道的只是节点和 npm。只需发出一条命令，您就可以将现代 ES2015 JavaScript 部署到微控制器上。

我制作了一个简短的视频来展示这些工具:

**塔隆·福克斯沃斯:**哦，太美了。你将便捷工具链的力量带到了现实世界。看起来我们有一个来自社区成员的问题:

# 为什么做 IoT 要用 Javascript？

> 为什么做 IoT 要用 Javascript？
> 
> **-** [**马丁·巴维奥**](https://sideway.com/user/mbavio)

安德鲁·朝克莱:好问题。因为它不是 c。我开玩笑。JavaScript 非常适合事件驱动编程。它也是异步的。你不必一直检查一个按钮的状态。您可以实现一个按钮按下时的处理程序。当有人按下按钮时，就会触发密码。HTTP 请求也是如此。加载数据时，您可以在屏幕上显示内容。编写非阻塞的 C 代码是可能的，但是具有挑战性。对于 JavaScript 开发人员来说，这是第二天性。JavaScript 意味着硬件！

我有一个关于 Marvell(一家芯片制造商)如何与索尼合作开发电子书阅读器的故事。在日本，固件和用户界面是用 c 编写的。在美国，用户界面是用 JavaScript 编写的。当比较这两个设备时，美国的设备比用 C 写的设备运行得更快！

我不是说人们不能写好的 C 代码，只是写响应性的 JavaScript 代码更容易:)

塔隆·福克斯沃斯:说得好！现实世界是事件驱动的，就像 javascript 一样。这使得自。但是，我相信这个任务不是微不足道的。

# 你在创作 thingsSDK 时面临的一些挑战是什么？

安德鲁·朝克莱:好问题。我从哪里开始？一些挑战与 ESP8266 器件的局限性有关。有了 JavaScript 解释器，复杂的应用程序就没有多少空间了。但大多数需要互联网连接和切换几个引脚的家庭自动化项目都没问题。或者，如果您想要驱动 5 台显示器并播放动画，这也很好。但是，如果你想驾驶 5 显示器*和*连接到互联网你推它。我们正在探索使用 ESP32 和其他一些设备，这样人们就可以真正用这种东西进城了。

其他问题包括能够破译 C 和 Python 代码来编写闪光器。许多源代码看起来很神奇。Craig Dennis 做得很好，他从这些语言中提取了闪光的代码，他甚至用 RxJS 重构了这些代码，用功能反应式编程来编写。我们希望其他芯片也能如此。

另一个挑战是不能直接控制运行时环境。理想情况下，我们需要一个小型运行时，只具备基于物联网的开发板所需的功能。许多运行时都有额外的开销和膨胀。我目前正在探索更低级别的替代方案，并真正推动我的能力极限:)

如果有人想在这方面提供帮助，请告诉我:)

**Taron Foxworth:** 所以，大部分的努力都是为了支持 ESP8266 设备。从表面上看，不久的将来是支持更多的设备，并找出一个更有效的运行时。

# thingsSDK 的未来是什么样子的？

Andrew Chalkley: 从一开始，我们就想让 thingsSDK 项目具有可移植性。CLI 使用我们称之为“策略”的东西来为目标运行时进行转换——在我们的例子中是 Espruino。但我们并没有与之结婚。我们——或者事实上的任何人——可以为其他运行时创建其他策略，比如 Kinoma 的 JavaScript 运行时 XS6。现在，我们正在考虑创建额外的抽象来与其他设备一起工作。

换句话说，如果您学习了 thingsSDK 周围的工具，即使在这个不断变化的物联网运行时和开发板世界中，您也不需要学习新的东西。

我们从某种程度上抽象了这一点——我们希望进一步抽象:)

Taron Foxworth: 太棒了！所以现在，我要问一个黄金问题。

# 如果我想开始使用 thingsSDK，我该如何开始？

**Andrew Chalkley:** 在[http://thingssdk.com](http://thingssdk.com)我们有入门指南和一些简单的入门项目的链接。我们也有一个到我们的[社区 Slack 频道](https://jsot-slack.herokuapp.com/)的链接，欢迎每个人。

在我们的 GitHub 上有一些唾手可得的问题，人们可以贡献自己的力量。我们已经有许多开源的第一次贡献者帮助这个项目，所以进来吧！

**Taron Foxworth:** 我可以诚实地说，JS IoT Slack 频道是我迄今为止看到的最好的硬件资源。那里有这么多聪明人！Andrew，感谢您领导如此出色的产品。我很高兴看到 thingsSDK 成长并为之做出贡献。

你有什么想补充的结束语吗？

**安德鲁·朝克莱:**感谢邀请我！我真的很期待看到未来会发生什么。我认为将这种[技术](https://hackernoon.com/tagged/technology)掌握在尽可能多的人手里将会催生一些令人敬畏的创新和产品。

如果你是硬件新手，一定要去看看 Maker Show，我们接下来的两集已经在“单板计算机”和“物联网”上拍摄了，应该会在接下来的几周内推出！敬请关注更多内容！

# 接下来呢？

确保你们关注了 Andrew 和 thingSDK，如果你们喜欢这个，请给它一颗心，或者在 Twitter 上告诉我！

这个采访最初被讨论为[“与 Andrew Chalkley 一起深入研究微控制器上的 Javascript”](https://sideway.com/room/bm)在[旁道](http://sideway.com)。

直到下一次，保持联系😉

[![](img/50ef4044ecd4e250b5d50f368b775d38.png)](http://bit.ly/HackernoonFB)[![](img/979d9a46439d5aebbdcdca574e21dc81.png)](https://goo.gl/k7XYbx)[![](img/2930ba6bd2c12218fdbbf7e02c8746ff.png)](https://goo.gl/4ofytp)

> [黑客中午](http://bit.ly/Hackernoon)是黑客如何开始他们的下午。我们是 AMI 家庭的一员。我们现在[接受投稿](http://bit.ly/hackernoonsubmission)并乐意[讨论广告&赞助](mailto:partners@amipublications.com)机会。
> 
> 如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！

![](img/be0ca55ba73a573dce11effb2ee80d56.png)