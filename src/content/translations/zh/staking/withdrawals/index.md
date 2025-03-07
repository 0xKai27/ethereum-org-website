---
title: 质押提款
description: 本页面概述质押推送提款是什么，它们如何工作，质押人需要做什么才能获得奖励
lang: zh
template: staking
image: ../../../assets/staking/leslie-withdrawal.png
alt: 犀牛莱斯利与她的质押奖励
sidebarDepth: 2
summaryPoints:
  - 上海升级在以太坊上启用质押提款
  - 验证者操作员必须提供一个提款地址以启用
  - 奖励每隔几天自动分发
  - 完全退出质押的验证者将收到他们的剩余余额
---

<UpgradeStatus dateKey="page-staking-withdrawals-when">
  质押提款将通过上海/卡佩拉升级启用。 这次以太坊网络升级预计将在 2023 年上半年进行。 <a href="#when" customEventOptions={{ eventCategory: "Anchor link", eventAction: "When's it shipping?", eventName: "click" }}>更多内容如下</a>
</UpgradeStatus>

上海/卡佩拉升级在以太坊上启用**质押提款**，允许人们解锁以太币质押奖励。 奖励支付将自动定期发送到与各个验证者关联的提款地址。 用户还可以完全退出质押，解锁他们全部的验证者余额。

## 质押奖励 {#staking-rewards}

对于有效余额已满 32 ETH 的活跃验证者账户，奖励支付将自动处理。

通过奖励获得的超过 32 ETH 的余额实际上并不构成本金，也不会增加该验证者在网络上的权重，因此每隔几天会自动提取作为奖励支付。 除了一次性提供提款地址外，这些奖励不需要验证者操作员采取任何行动。 这都是在共识层启动的，因此在任何步骤都不需要燃料（交易费）。

### 我们怎么发展到现在的？ {#how-did-we-get-here}

在过去的几年里，以太坊经历了几次网络升级，从依赖能源密集型挖矿的网络转变为由以太坊本身保护的网络。 现在，在以太坊上参与共识被称为“质押”，因为参与者自愿锁定以太币，将其“押注”以参与网络。 遵守规则的用户将获得奖励，而尝试欺骗的行为可能会受到惩罚。

自 2020 年 11 月质押存款合约启动以来，一些勇敢的以太坊先驱者自愿锁定资金以激活“验证者”，这些账户有权按照网络规则正式证明和提议区块。

在上海升级之前，您无法使用或访问您质押的以太币。 但现在，您可以选择自动将奖励发送到提供的帐户，并且还可以随时提取您抵押的以太币。

### 我应该如何准备？ {#how-do-i-prepare}

<WithdrawalsTabComparison />

### 重要通知 {#important-notices}

为任何验证器帐户提供提款地址是一个必需的步骤，否则无法从其余额中提取以太币。

<InfoBanner emoji="⚠️" isWarning>
  <strong>每个验证者帐号只能分配一个提款地址，且仅限一次。</strong>一旦选择一个地址并将其提交到信标链，这个地址不能撤消或再次更改。 在提交前，请仔细检查所提供地址的所有权和准确性。
</InfoBanner>

同时，<strong>您的资金不会因不提供提款地址而受到威胁</strong>。 未添加提款凭据只会将以太币保持锁定在验证者帐户中，直到提供提款地址为止。

## 完全退出质押 {#exiting-staking-entirely}

在从验证者帐户余额中转移*任何*资金之前，必须提供提款地址。

希望完全退出质押并取回全部余额的用户还必须使用验证者密钥签署并广播一个“自愿退出”的消息，这将启动退出质押的过程。 这是通过您的验证者客户端完成的，并提交给您的信标节点，无需燃料。

验证者从抵押退出的过程所需时间不同，具体取决于同时退出的人数。 一旦完成，此帐户将不再负责执行验证者网络职责，不再有资格获得奖励，并且不再拥有“质押”的以太币。 此时，帐户将被标记为完全“可提款”。

一旦帐户被标记为“可提款”，并且已提供提款凭据，用户除了等待之外，无需再做任何事情。 区块提议者会自动且持续地扫描是否有可退出资金，并在下一次<a href="#validator-sweeping" customEventOptions={{ eventCategory: "Anchor link", eventAction: "Exiting staking entirely (sweep)", eventName: "click" }}>扫描</a>期间将您帐户的余额全额转移（也称为“全额提款”）。

## 何时启用质押提款？ {#when}

提款功能将通过两部分同时进行的网络升级启用，即**上海 + 卡佩拉**。

<ShanghaiCapella />

## 提款支付是如何运作的？ {#how-do-withdrawals-work}

特定验证者是否有资格提款取决于验证者帐户本身的状态。 在任何时候，都不需要用户输入来确定帐户是否应该发起提款，整个过程由共识层在连续循环中自动完成。

### 更愿意通过视频学习？ {#visual-learner}

请查看 Finematics 对以太坊质押提款的解释：

<YouTube id="RwwU3P9n3uo" />

### 验证者“扫描” {#validator-sweeping}

当验证者被安排提议下一个区块时，需要构建一个最多包含 16 个合格提款的提款队列。 首先从验证者索引 0 开始，根据协议规则判断该帐户是否有合格的提款，如果有，则将其添加到队列中。 被安排提议下一个区块的验证者将从上一个验证者离开的地方继续，无限期地按顺序进行。

<InfoBanner emoji="🕛">
想象一个模拟时钟。 时钟的指针指向小时，朝一个方向前进，不跳过任何小时，最后在达到最后一个数字后再次回到开始。
<br/><br/>现在，想象这个时钟不再是 1 至 12，而是从 0 到 N<em>（在信标链上注册的验证者帐户的总数，截至 2023 年 1 月已超过 500,000 个）。</em><br/><br/>
时钟的指针指向需要检查是否符合提款条件的下一个验证者。 它从 0 开始，不跳过任何帐户，一直前进。 当达到最后一个验证者时，循环从头开始继续。
</InfoBanner>

#### 检查帐户的提款 {#checking-an-account-for-withdrawals}

在提议者扫描验证者以寻找可能的提款时，使用一系列简短的问题评估正接受检查的每个验证者，以确定是否应触发提款，如果是，应提取多少以太币。

1. **是否已提供提款地址？**如果未提供提款地址，则跳过该帐户，不会发起提款。
2. **验证者是否已退出且可提款？**如果验证者已完全退出，并且我们已到达帐户被视为“可提款”的时段，那么将处理全额提款。 这将把所有剩余余额转移到提款地址。
3. **有效余额是否达到 32 的最大值？** 如果帐户具有提款凭证，尚未完全退出，并且有超过 32 的奖励在等待，将处理部分提款，只将超过 32 的奖励转移到用户的提款地址。

在验证者生命周期中，验证者操作员只会执行以下两个直接影响此流程的操作：

- 提供提款凭证以启用任何形式的提款
- 退出网络，这将触发全额提款

### 免燃料费 {#gas-free}

这种质押提款方法不需要质押人手动提交交易来请求提款特定数量以太币。 这也意味着**不需要支付燃料（交易费用）**，并且提款也不会争夺现有执行层区块空间。

### 我会多久收到一次质押奖励？ {#how-soon}

单个区块最多可处理 16 笔提款。 以这个速度计算，每天可处理 115,200 个验证者提款（假设没有错过任何时隙）。 如上所述，没有符合条件的提款的验证者将被跳过，这将减少完成扫描所需的时间。

扩展这个算法，我们可以预估处理特定数量的提款所需的时间：

<TableContainer>

| 提款数量 | 所需时间 |
| :------: | :------: |
| 400,000  |  3.5 天  |
| 500,000  |  4.3 天  |
| 600,000  |  5.2 天  |
| 700,000  |  6.1 天  |
| 800,000  |  7.0 天  |

</TableContainer>

正如您所看到的，随着网络上的验证者数量增加，完成该过程的速度也会变慢。 增加错过区块可能会成比例地减缓该过程，但这通常代表了可能结果中较慢的一面。

## 常见问题 {#faq}

<ExpandableCard
title="在我提供了一个提款地址后，我能否将其改为另一个提款地址？"
eventCategory="FAQ"
eventAction="Once I have provided a withdrawal address, can I change it to an alternative withdrawal address?"
eventName="read more">
不，提供提款凭证的过程只需进行一次，一旦提交后就无法更改。
</ExpandableCard>

<ExpandableCard
title="为什么提款地址只能设置一次？"
eventCategory="FAQ"
eventAction="Why can a withdrawal address only be set once?"
eventName="read more">
通过设置执行层提款地址，该验证者的提款凭证已永久更改。 这意味着旧的提款凭证将不再起作用，新的提款凭证将指向执行层帐户。

提款地址可以是智能合约（由其代码控制），也可以是外部拥有的账户（EOA，由其私钥控制）。 目前，这些帐户无法向共识层传回信息以表示验证者凭证已更改，而添加此功能将给协议增加不必要的复杂性。

作为更改特定验证者提款地址的替代方案，用户可以选择设置智能合约作为他们的提款地址，该智能合约可以处理密钥轮换，例如 Safe。 将资金去向设置为自己的外部帐户的用户可以执行完全退出以提取所有的质押资金，然后使用新的凭证重新进行质押。
</ExpandableCard>

<ExpandableCard
title="如果我参与流动性质押衍生品或质押池质押，会怎样？"
eventCategory="FAQ"
eventAction="What if I participate in liquid staking derivatives or pooled staking"
eventName="read more">

<p>如果你是<a href="/staking/pools/">质押池</a>的一部分或持有流动性质押衍生品，则应向你的提供商详细咨询质押提款将如何影响您的安排，因为每个服务运作方式不同。</p>
<p>一般来说，用户可能不需要做任何事情，在升级后，这些服务将不再受到无法提取奖励或退出验证者资金的限制。</p>
<p>这意味着用户现在可以决定赎回其正在被质押的以太币，或更改他们使用的质押服务提供商。 如果特定的质押池变得过于庞大，资金可以退出并赎回，并重新使用<a href="https://pools.invis.cloud">规模较小的提供商</a>进行质押。 或者，如果你已经积累了足够的以太币，你可以<a href="/staking/solo/">自行质押</a>。</p>
</ExpandableCard>

<ExpandableCard
title="奖励支付（部分提款）是否会自动进行？"
eventCategory="FAQ"
eventAction="Do reward payments (partial withdrawals) happen automatically?"
eventName="read more">

<p>是的，只要你的验证者提供了提款地址。 必须提供一次才能启用任何提款，然后每隔几天，每次验证者扫描都会自动触发奖励支付。</p>
</ExpandableCard>

<ExpandableCard
title="全额提款是否会自动进行？"
eventCategory="FAQ"
eventAction="Do full withdrawals happen automatically?"
eventName="read more">

<p>不。如果您的验证者仍在网络上运行，则不会自动执行完全提款。 需要手动发起自愿退出。</p>
<p>一旦验证者完成退出过程，并且假设该账户具有提款凭证，则剩余余额<em>将</em>在下一个验证者扫描期间进行提款。</p>
</ExpandableCard>

<ExpandableCard title="我可以提取自定义数量的资金吗？"
eventCategory="FAQ"
eventAction="Can I withdraw a custom amount?"
eventName="read more">

<p>提款旨在自动推送，转移任何未积极为质押做贡献的以太币。 这包括帐号的全部余额。 </p>
<p>无法手动请求要提取以太币的具体数量。</p>
</ExpandableCard>

<ExpandableCard
title="我是一名验证者操作者，我在哪里可以找到更多关于准备的详细信息？"
eventCategory="FAQ"
eventAction="I operate a validator, where can I find more information on preparing?"
eventName="read more">

<p>建议验证者操作者访问<a href="https://launchpad.ethereum.org/withdrawals/">质押启动板提款</a>页面，详细了解如何做好准备、事件的时间安排以及提款如何运作。</p>
</ExpandableCard>

<ExpandableCard
title="退出后，我可以通过存入更多以太币来重新激活验证者吗？"
eventCategory="FAQ"
eventAction="Can I re-activate my validator after exiting by depositing more ETH?"
eventName="read more">

<p>否。 一旦验证者退出并提取其全部余额，存入该验证者的任何额外资金将在下一次验证者扫描期间自动转移到提款地址。 要重新质押以太币，必须激活新的验证者。</p>
</ExpandableCard>

## 延伸阅读 {#further-reading}

- [质押启动板提款](https://launchpad.ethereum.org/withdrawals)
- [EIP-4895：信标链提款推送操作](https://eips.ethereum.org/EIPS/eip-4895)
- [以太坊牧猫人组织 - 上海](https://www.ethereumcatherders.com/shanghai_upgrade/index.html)
- [PEEPanEIP #94：质押以太币提取（测试）与 Potuz 和王筱维](https://www.youtube.com/watch?v=G8UstwmGtyE)
- [PEEPanEIP#68：EIP-4895：信标链推送提款操作与 Alex Stokes](https://www.youtube.com/watch?v=CcL9RJBljUs)
- [了解验证者有效余额](https://www.attestant.io/posts/understanding-validator-effective-balance/)
