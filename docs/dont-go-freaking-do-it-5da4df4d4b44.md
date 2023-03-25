# 不要“去他妈的做吧”——聪明的合同分析

> 原文：<https://medium.com/hackernoon/dont-go-freaking-do-it-5da4df4d4b44>

![](img/052abbccc65bf37d642c906cdad57062.png)

刚刚在[黑客新闻](https://news.ycombinator.com/item?id=15843738)上看到一个关于一个叫做“[去他妈的做吧](https://gofreakingdoit.com/)”的[以太坊](https://www.ethereum.org/)智能合约的好主意，于是决定看看它是如何运作的。这篇文章描述了我们发现的一些错误。

# 介绍

我的朋友 [Nico](https://hamstah.com/) 和 [I](https://tandem.engineering) 都对信息/网络安全感兴趣，最近注意到智能合同中可用的攻击面。目前，我们主要着眼于可靠性和 EVM 字节码，试图自动化寻找漏洞的过程，以及做一些手工代码审计。

该合同的代码在 Etherscan 上[，可以直接在那里进行审计。如果你对可靠性不熟悉，看看这个备忘单](https://etherscan.io/address/0x2d4991d05131cbf3cdf81439e96b11a93ccb7af0#code)。感谢合同的作者 Karolis Ramanauskas ，他执行了一个如此巧妙的想法。

# 什么是“去他妈的做吧”

这个概念很简单:你把$$$和你想要完成的目标一起存入合同，还有一个可选的“主管”联系人，他将核实你是否在给定的日期完成了目标。如果他们说你做到了，那么你可以拿回你的美元。如果没有，“去他妈的做吧”会保留它，所有者会为他们建造它的努力赚些钱。

# 发现低严重性问题

**数据丢失。**不检查目标是否已经包含给定的散列。如果提交了具有相同发件人/描述/价值/截止日期的目标，可能会导致目标丢失(和$$$)。

```
function setGoal() {
    (...snip for brevity...) bytes32 hash = keccak256(msg.sender, _description, msg.value, _deadline); Goal memory goal = Goal(...snip for brevity...); goals[hash] = goal; (...snip for brevity...)
}
```

*解决方案:要么拒绝重复项，要么在哈希中添加一个随机数。*

一个超级用户负责所有任务。 这个契约有两类用户，“所有者”和其他所有人。这样做的问题是，契约有一些内务处理功能，这些功能可能运行在某个外部系统上(比如 setEmailSent())，然后这个系统将可以访问凭证，这些凭证可以对契约做任何事情。(虹吸钱，转移所有权，销毁它。).

*解决方案:最好将权限分层，并有一个额外的帐户，“会计”或类似的帐户。*

**数据泄露。**因为所有目标都是公开的，所以您可以看到所有用户输入的电子邮件地址、目标和金额。

```
Goal[] public activeGoals;
```

*解决方案:不要标记为 public。*

# **发现高严重性问题**

**不允许将目标设置为失败。setGoalFailed 缺少“onlyOwner”保护。这意味着任何人都可以在任何时候“辜负”合同中每个用户的目标，实质上是将他们所有的钱都捐给了合同所有者。**

```
function setGoalFailed(uint _index, bytes32 _hash) {
    assert(goals[_hash].amount > 0);
    // assert(goals[_hash].emailSent == true); goals[_hash].completed = false;
    activeGoals[_index].completed = false; owner.transfer(goals[_hash].amount); // send ether to contract owner setGoalFailedEvent(_hash, false);
}
```

*解决方案:在函数声明中添加 onlyOwner 守护。*

**没有版本控制或升级的可能性。**因为所有的状态都存储在契约本身中，所以升级是不可能的。

*解决方案:拥有独立的业务和数据逻辑，或者使用 delegatecall 会有所帮助。参见* [*此处*](https://blog.colony.io/writing-upgradeable-contracts-in-solidity-6743f0eecc88) *和* [*此处*](/aigang-network/upgradable-smart-contracts-what-weve-learned-at-aigang-b181d3d4b668) *关于可升级合同的精彩文章。*

# 我们是谁

英国伦敦的两名金融科技首席技术官。

更多关于[杰斯珀](https://tandem.engineering) |更多关于[尼科](https://hamstah.com)。

# 笔记

在发表这篇帖子前不久，HN [上的用户“mpeg”发现了同样的 setGoalFailed() bug](https://news.ycombinator.com/item?id=15845374) 。

# 更新

好消息！😎作者指出，他正在研究 V2，并将解决悬而未决的问题。