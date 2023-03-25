# 网络开发者对抗特朗普议程的 10 种方式

> 原文：<https://medium.com/hackernoon/10-ways-web-developers-can-stand-up-to-the-trump-agenda-dff0ef12eaf2>

对我们许多人来说，选举后的日子是一种深深的、黑暗的情绪波动(愤怒、恐惧、沮丧、失望、悲伤),导致一种无助感。在此后的几周里，许多人已经将这些情绪转化为行动。面对危险的倒退态度和政策，作为网络开发者，我们如何运用我们的技能采取积极的行动？

![](img/98288feb6111dc4cd4b2bd0f5a132209.png)

# 1.构建可访问的界面

唐纳德·特朗普嘲笑残疾记者的画面深深印在我的脑海中，所以让我们把它作为开发更易访问的应用程序的动力。构建可访问的界面是迈向包容所有人的一步，不管他们的能力如何。可访问性信息的数量可能看起来太多了，但是这里有一些步骤可以让你的应用程序更容易访问:

*   读一篇[关于无障碍的好介绍](https://www.marcozehe.de/2015/12/14/the-web-accessibility-basics/)
*   使用可访问性清单( [A11y 项目](http://a11yproject.com/checklist.html)和 [WebAim](http://webaim.org/standards/wcag/checklist) 有好的清单)
*   使用屏幕阅读器浏览您的应用程序，如 [Chromevox](http://www.chromevox.com/) ，并改善体验
*   安装[到一个书签](https://khan.github.io/tota11y/)并使用它手动测试你的站点
*   使用诸如 [axe-core](https://github.com/dequelabs/axe-core) 或 [Pa11y](http://pa11y.org/) 之类的工具将自动化可访问性测试构建到您的构建过程中

# 2.关心使用旧设备和较慢连接的用户

作为专业的网络开发人员，我们更有可能拥有现代化的硬件和快速的网络连接，但这并不适用于所有人。例如，在美国，[五分之一的人拥有智能手机](http://www.pewinternet.org/2015/04/01/us-smartphone-use-in-2015/)，但要么在家里无法接入高速互联网，要么除了手机之外接入受限。当我们构建我们的网站和应用程序时，只考虑现代设备和连接，我们将这些人拒之门外。我们如何为所有用户构建现代且有弹性的应用程序？

*   [将渐进增强作为一个设计过程来应用](https://gdstechnology.blog.gov.uk/2016/09/19/why-we-use-progressive-enhancement-to-build-gov-uk/)，允许站点和应用程序优雅地后退
*   速度很重要！衡量并努力提高网站的性能。 [Smashing Magazine 有一个很棒的前端性能策略清单](https://www.smashingmagazine.com/2016/12/front-end-performance-checklist-2017-pdf-pages/)(响应时间的[80–90%](http://www.stevesouders.com/blog/2012/2/10/the-performance-golden-rule/)花费在这里)
*   考虑添加[离线功能](http://offlinefirst.org/)，允许用户访问你的内容，而不管连接性如何

# 3.构建包容性表单

表单允许用户直接与站点交互。它们通常是区分网站和网络应用的东西，输入我们的名字和性别通常是关键的组成部分。

在戴尔·卡耐基 1936 年颇具影响力的自助书籍《如何赢得朋友和影响他人》中，他说“对一个人来说，他的名字是任何语言中最甜美、最重要的声音。”名字是我们个人身份的核心部分。我们经常会认同他们，听到他们在房间另一边说话的声音就会转过身去，当一个我们刚刚认识的人理解我们的名字时，我们会本能地感激。

不幸的是，有可能做出导致错误处理少数群体名称的假设。在处理名称时，我们应该准备好各种字符、间距和独特的国际格式。

对许多人来说，性别不仅仅是出生时确定的男性或女性的二元性别。当我们将一个表单限制在这两个选项中时，我们排除了那些不认同这两个选项的人。当在表单中包含性别选项时，我们应该为自定义输入以及“不愿意说”选项留出空间。

为了提高您在表单中处理姓名和性别的能力，我推荐您阅读以下文章:

*   [你好，我叫 _ _ _ _ _ _ _ _](http://.codes/talks/hello-my-name-is/)由 Nova Patch
*   [大家好，我是 Aimee Gonzalez-Cameron](http://alistapart.com/article/hello-my-name-is-error)
*   程序员相信的关于名字的谎言
*   克莱尔·高尔的《如何询问性别》
*   [打破常规思考表格](http://www.lgbt.cusu.cam.ac.uk/campaigns/think/forms/)CUSU LBGT+

# 4.测试不同的用户

当我们只考虑周围人的意见时，我们可能会建立一些东西，把一些人拒之门外。当我们用不同的用户测试我们的应用程序时，我们确保这不会发生*和*制造更好的产品。大家都赢了！

Julie M. Young 的文章[包容性可用性测试最佳实践](https://www.juliemyoung.com/blog/2016/6/1/inclusive-usability-testing-best-practices)为招募和管理不同受众的用户测试提供了很好的指导。

# 5.到处使用 HTTPS

HTTPS 让网络变得更加隐私和安全，这两样东西随着川普政府的上台只会变得更加重要。像 EFF 和美国政府这样的组织。！！)一直在敦促网站所有者默认启用 HTTPS。

传统上，SSL/TLS 既棘手又昂贵。今天[让我们加密](https://letsencrypt.org/)和 [Certbot](https://certbot.eff.org/) 让它变得更加容易和完全免费。

# 6.确保用户的隐私

根据皮尤研究中心的调查，超过一半的美国人担心政府监控，91%的美国成年人认为消费者已经失去了对公司如何收集和使用个人信息的控制。用户浏览历史可以揭示宗教偏好、政治倾向，甚至在确诊前预测疾病。作为开发者，我们站在保护用户隐私的第一线。为了确保用户隐私，我们可以:

*   [尊重用户不跟踪设置](/@adamdscott/respecting-user-privacy-preferences-f5004c087ff#.ka8veb7cf)
*   设置 cookies 时通知用户
*   寻求分散用户数据
*   遵循[隐私感知](https://piwik.org/blog/2014/01/data-privacy-day-january-28th/)分析实践

# 7.保护用户数据

几乎每天都有数据泄露的新闻。对于我们收集的用户数据，保护这些信息比以往任何时候都更加重要。我们可以采取的一些实际步骤:

*   注意 [OWASP 前 10 名](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)
*   通过使用成熟且经过测试的 web 框架，为安全性打下坚实的基础
*   加密收集的所有数据
*   为用户提供多因素身份认证选项
*   强化您的[安全标题](https://www.keycdn.com/blog/http-security-headers)
*   创建[安全披露政策](https://titanous.com/posts/security-disclosure-policy-best-practices)

# 8.成为多元化员工的盟友

众所周知，技术人员存在多样性问题。当我们的领导人忽视我们国家精彩的多样性的时候，让我们真正致力于使之变得更好。对于我们这些来自多数群体的人来说，我们可以从成为好盟友开始。

*   致力于支持多元文化
*   意识到你的[无意识偏见](https://diversity.ucsf.edu/resources/unconscious-bias)
*   倾听并支持你的同事
*   如果你找不到多样化的候选人，那就改变你的招聘方式
*   阅读和利用(许多！)伟大的[项目包括](http://projectinclude.org/)资源

# 9.自愿贡献你的时间和技能

作为开发人员，我们有两个不可思议的资产:一个受欢迎的技能组合，和，通常，一个灵活的工作时间表。利用这些，好好利用它们。找到当地的进步组织，自愿为他们建立一个网站或者改进他们现有的网站(HTTPS！).或者利用你的弹性时间表来贡献你的时间。

# 10.分享你的财富

由于对发展技能的需求，我们许多人都很幸运地拥有一份高薪工作。用这些钱来支持争取平等和公民自由的组织。

最简单的捐赠方式是设立一个每月定期捐赠。可以这样想:如果你每月的订阅费用很少(网飞、AWS、数字海洋等。)你有能力支持一个致力于我们自由的进步组织。匹配其中一项服务的费用，并设立每月捐款。以下是我最喜欢的几个组织:

*   [美国民权联盟](https://www.aclu.org/)
*   [边境天使](http://www.borderangels.org/)
*   [全美有色人种协进会法律辩护基金](http://www.naacpldf.org/ways-get-involved)
*   [移民儿童权利青少年中心](https://jezebel.com/a-list-of-pro-women-pro-immigrant-pro-earth-anti-big-1788752078)
*   [电子前沿基金会](https://www.eff.org/)

Jezebel 整理了一份更详尽的名单，列出了需要你支持的[支持女性、支持移民、支持地球、反对偏见的组织](http://jezebel.com/a-list-of-pro-women-pro-immigrant-pro-earth-anti-big-1788752078)。

最重要的是，记住我们都在一起。正如奥巴马总统在他的告别演说中所说的，我们必须“愿意继续推进民主的艰苦工作。”我希望我们都能利用自己的才能和技能来建设一个更好的网络和国家。🇺🇸

[![](img/50ef4044ecd4e250b5d50f368b775d38.png)](http://bit.ly/HackernoonFB)[![](img/979d9a46439d5aebbdcdca574e21dc81.png)](https://goo.gl/k7XYbx)[![](img/2930ba6bd2c12218fdbbf7e02c8746ff.png)](https://goo.gl/4ofytp)

> [黑客中午](http://bit.ly/Hackernoon)是黑客如何开始他们的下午。我们是 [@AMI](http://bit.ly/atAMIatAMI) 家庭的一员。我们现在[接受投稿](http://bit.ly/hackernoonsubmission)并乐意[讨论广告&赞助](mailto:partners@amipublications.com)机会。
> 
> 如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！

![](img/be0ca55ba73a573dce11effb2ee80d56.png)