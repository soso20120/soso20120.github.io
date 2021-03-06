---
layout: post
title: Block-Supply Chain
date: 2018-08-12 11:11:11
tags:
- NFC
- Blockchain
- Supply Chain

---

## Abstract

现有的反造假的供应链都依赖于集中式授权。这种架构导致一些问题：单点处理，内存和故障。融入区块链技术可以提供有前景的解决方案。本文中，我们提出区块供应链，它是一种全新的分布式的供应链，使用区块链和NFC技术可以侦察出造假攻击。区块供应链代替了原有的集中式供应链，利用新的共识协议，完全分布式，在效率和安全间取得平衡。仿真表明，相比现有的共识协议Tendermint，该协议在满足安全性的同时表现突出。

## Tendermint

Tenermint 是一个软件，用于在多台机器安全一致地复制一个应用。能够容忍机器以任何一种、甚至包括危害系统的方式发生故障，被称为拜占庭容错（BFT）。拜占庭理论已经有几十年的历史，但是很大程度上，直到最近像比特币，以太坊这样区块链技术的成功，它的软件实现才得以进一步发展。区块链技术只是以一种现代化的方式对 BFT 的再形式化，而且重点关注 p2p 网络和密码验证。

Tendermint 包含了两个主要的技术组件：一个区块链共识引擎和一个通用的应用程序接口。共识引擎，叫做 Tendermint Core，保证了每一台机器以相同的顺序记录同一笔交易。应用程序接口，叫做应用程序区块链接口（ABCI），保证了交易可以通过任何一种编程语言进行处理。与其他预先打包内置状态机（比如键值存储或者一个奇怪的脚本语言）的区块链和共识方案不同，开发者可以使用 Tendermint 实现应用的 BFT 状态机复制，而这些应用可以用任何语言编写，而且开发环境对开发者也十分友好。

Tendermint是POS+BFT的共识引擎框架。通过编写该框架的应用，可以方便快捷地实现基于Tendermint共识引擎的区块链。因为基于BFT算法的共识，Tendermint可以在不超过1/3的错误节点的情况下，保证区块的一致性。

## INTRODUCTION

数十年来，假冒产品，特别是医药产品的问题一直困扰着国际社会[11]。 世界卫生组织（WHO）估计，在全球范围内，10％的药物是假药，在发展中国家上升到30％[2]。 打击假冒的斗争仍然是一项重大挑战。 这是一个值得关注的问题，因为假冒药品可能导致严重疾病，甚至死亡。 针对这种情况，已经提出了几种产品防伪方法。 然而，大多数现有工作是集中的，并依赖于可信服务器来协调和管理产品认证。

大多数传统的集中供应链利用射频识别（RFID）和NFC标签以及认证服务器等技术来打击假冒攻击。有三种常见的假冒攻击[10] :( 1）修改产品在标签上的详细信息，例如更改有效期，（2）克隆用于假冒产品标签的真品详细信息，以及（3）从正版产品中删除合法标签并将其重新应用于假冒产品。集中供应链的典型架构会产生一些问题。首先，服务器上存在巨大的处理负担，因为大量产品涌入供应链节点。其次，需要大量存储来存储所有产品的认证记录。第三，与集中式系统一样，传统供应链本身也存在单点故障的问题。为了克服这些问题，区块链技术是一个潜在的框架，可以建立一个现代化，分散，可靠，负责，透明和安全的反假冒攻击供应链[11]。

在过去的几年中，除加密货币以外，区块链技术一直是许多不同行业的有吸引力的解决方案[6]。其背后的原因是区块链提供的透明度，安全性，质量保证，全球点对点交易和权力下放[15]。从根本上说，区块链是一个公共的分布式分类帐，它包含链式块，每个块由几个事务组成。这些块在全局和透明上进行验证以保证安全性（即，它们仅由有效和正确的事务组成）。这些块通过点对点，分布式和分散式结构在节点之间共享和同步[11]。尽管有可能提升安全性，工作和存储分配以及供应链的透明度，但只有少数项目可以检查防伪供应链和区块链技术的整合。这促使我们利用这一有前景的技术，通过将我们之前的集中供应链[2]转变为分散的区块供应链来打击假冒商品。

我们在本文中提出的第一个问题是**集中式防伪供应链**。尽管它们有可能检测到假冒产品，但它们仍然会遇到单点处理，存储和故障。此外，它们不提供透明度，因为它们不允许供应链节点验证产品数据的真实性。为了克服这些问题，我们提出了块供应链，即利用区块链技术的分散供应链。在此链中，每个节点都为每个产品维护一个区块链。该区块链由链式块组成，每个块都是一个认证事件。由当前具有产品的节点（即，提议节点）向网络提出新块。然后，由我们称为验证器的许多其他节点验证这个新提出的块，以确保该块有效。成功验证后，块供应链网络中的所有节点都会将此块添加到区块链的副本中，这将在第3节中详细介绍。

我们在本文中讨论的第二个问题是**关于块验证器的数量和它们的选择方式**。区块链的验证器负责确保其安全性并执行其共识协议。存在相当多的现有共识协议。尽管如此，他们中的大多数都没有考虑验证器的数量或如何选择它们，如第2节所述。区块链网络中的验证器数量大大影响其安全性，特别是在完全分散的情况下。区块链，其中没有特殊节点;所有节点都是无信任的，就像我们的块供应链用例一样。在这种区块链中实现最佳安全性的最佳验证器数量将是网络中除提议节点之外的所有节点（即，n-1，其中n是节点的数量）。然而，这种选择导致：（1）对于每个验证事件，O（n）的大量验证工作，（2）在Tendermint [3]、PBFT [4]（实际拜占庭容错）等协议中与O（n2）达成共识的高通信开销，（3）巨大的块大小，因为包含每个验证者的签名作为其有效性的证据。另一种选择是在起源状态下选择的固定静态数量的验证器（例如，Tendermint和Hyperledger Fabric [5]）。然而，这种选择导致：（1）部分集中，（2）性能瓶颈，特别是如果验证器的数量相对较低，以及（3）节点之间的不公平选择，主要是节点具有相等的投票和计算能力。

为了克服验证器的选择问题，我们提出了一种基于Tendermint的新协议，能够为每个验证事件选择一组不同的验证器（即，提出一个新的块）。我们的协议利用两个随机性阶段来防止安全威胁并提供公平性（即节点之间的选择概率相等）。此外，它还保证了验证工作和权力下放的分配。我们的协议随机使用log n验证器，而不是n - 1验证器的最佳选择，并且与最佳选择相比，实现了令人满意的安全级别。导致该特定值（即log n）的推理是将验证工作从O（n）减少到O（log n），以及从O（n2）到O（（log n）的通信开销。 N）。这种减少导致性能的显着提高，并且降低了通信和存储开销。尽管如此，我们计划根据网络的敌意使验证器的数量动态变化。

本文的贡献有两个方面：
1. 它引入了一个利用区块链技术（区块供应链）的分散供应链，从而克服了前面提到的集中化问题。块供应链可以跟踪和跟踪产品，而无需集中跟踪服务器。此外，它通过透明地涉及供应链节点来检测三种反击攻击（修改，克隆和标记重新应用）。
2. 它引入了一个新的共识协议，处理选择验证器的问题。该协议有几个优点。首先，它是非常有效和可扩展的，与具有n - 1验证器的最佳安全Tendermint相比，它显示出相当大的性能改进。第二，它提供了令人满意的安全性。例如，它能够在具有200个节点的区块链网络中检测到具有98.4％检测率的伪造攻击，其中33％是恶意的。第三，在天才状态之后，我们的协议是完全集中的，即它不依赖于固定的验证器。相反，每次提出新块时，验证器的设置都会更改。第四，它提供了选中节点概率的公平性。

## Related Work

在本节中，我们将研究一些非常相关的现有作品。 相关文献分为两大类：（1）整合区块链和供应链技术的工作，（2）目前广泛使用的共识协议。

#### Block and Supply Chains

Tian [16]提出了使用RFID和区块链的农业食品供应链概念框架。 该供应链旨在追踪“从农场到餐桌”的农业食品。 

Saveen等人[1]讨论了在生产供应链中使用区块链技术的潜在好处。 然后，他们提出了一个纸板箱制造供应链的框架，该框架将区块链作为一个平台，用于收集，存储和管理每个产品在其整个生命周期中的产品细节。 这项工作介绍了使用区块链将集中式系统替换为分散式系统的总体概述。 

在Hackius等人发表的一项研究中，[6]作者进行了一项在线调查，并询问专业人士在供应链管理中使用区块链的意见。 作者发现大多数参与者都对区块链及其带来的好处持积极态度。

#### 共识协议

* PBFT（实际拜占庭容错）。 PBFT [4]是一种可以容忍拜占庭故障的复制算法。 PBFT通过一系列观点进展。 每个视图都有一个主节点（即提议者），它以循环顺序选择。 视图中的其他节点（副本）称为备份。 客户端向主服务器发送请求。 主服务器为备份的此请求组播已签名的预准备消息。 备份接受预备消息，并广播已签名的准备消息。 如果备份接收到2f为请求准备消息（其中f是可能有故障的最大副本数），则它们会多播签名的提交消息。 如果主服务器出现故障，备份将执行视图更改协议。 PBFT有以下问题[3]。 首先，改变视图是微妙的，有点复杂。 其次，自上次提交以来的所有先前客户端请求都将迁移到新视图。
* Tendermint。 Tendermint[3,7]提供了在多个节点上复制应用程序的安全性，因为它可以工作，即使网络中多达三分之一的节点以任意方式发生故障。 Tender-mint是一种共识协议，不包括工作量证明挖掘，它可以克服能源和资源消耗问题，并加快块的验证[7]。 Tendermint基于PBFT，它涉及三个阶段的投票以达成共识（建议，普遍和预先提交）。提议者提出一个新的块，然后验证器在块上出现，并且只有在收到超过2/3的prevotes时才进行预先提交。如果收到超过2/3的预先提交，验证者只接受该块。 Tenminmint需要一组固定的已知验证器。对一个区块的投票进行轮次，每轮都有一个新的提议者。参赛者投票决定是否进行拦截或进入下一轮。 Tendermint以其简单性，性能和分叉责任而着称[8]。尽管如此，验证者的数量会对Tendermint的表现产生强大的影响。这是由于两个投票阶段（即普遍投票和预先投票）产生的通信开销。这在性能和安全性之间进行了权衡，更多的验证者加强了安全性。我们的协议基于Tendermint，并继承了Tendermint提供的所有功能。但是，它通过在每个块提议上选择不同的随机验证器集来处理验证器的选择问题。
* Hyperledger Fabric采用PBFT作为其一致性算法[5]。 因此，它可以容忍区块链网络中多达1/3的拜占庭节点。 在Fabric v0.6中，存在固定数量的验证对等体，负责执行共识协议。 提议者可以向任何人提交交易。 然后，所选择的对等体将该事务广播给其他对等体。 其中一个验证对等体被选为领导者。 生成块时，领导者将其广播给所有对等体。 当验证对等体接收到该块时，它会散列它，将散列广播到所有其他对等体，并开始计算它们的响应。 如果使用相同的哈希接收到三分之二的响应，则会将新块提交到其本地分类帐。 与Tendermint一样，Hyperledger Fabric受到部分集中化，因为它使用固定的已知数量的验证对等体。
* 恒星共识议定书（SCP）。SCP[12]是一种利用法定人数的共识协议，其中法定人数是来自网络的一组节点，足以达成协议。SCP基于联邦拜占庭协议（FBA），其中SCP利用法定人数切片的概念。仲裁片是仲裁的子集，可以使一个特定节点达成协议。 FBA的关键思想是每个节点都选择自己的仲裁切片。当节点片段中的节点的阈值（例如，2/3）确认它时，节点接受投票或交易。但是，SCP要求法定人数切片重叠。先前讨论的协议（例如PBFT，Hyperledger Fabric和Tendermint）使用固定且全局已知的节点集来达成共识。相反，SCP为每个节点提供了选择一个或多个仲裁片的选择，每个仲裁片可能具有不同的节点。尽管这种设计很美，但它可能会导致破坏共识，因为法定人数切片可能不会重叠。

值得一提的是，我们在本节中仅考虑了BFT（拜占庭容错）协议，因为它们与我们提出的协议更相关。我们没有足够的空间来包括其他采矿共识协议，如PoW（prof-of-Work）[13]，PoS（Prof-of-Stake）[17]，或非BFT协议，如Paxos [9]和Raft [14]。

## Conclusions

我们提出了利用区块链和NFC技术的新的分散供应链（区块供应）。块供应链能够跟踪和追踪产品并检测修改，克隆和标记重新应用攻击。对于这个链，我们引入了一种新的可扩展且安全的共识协议。我们的仿真表明，我们的新协议对大型网络非常有效，这使其成为需要完全集中化的大型区块链的合适选择。

这是一项持续的工作，我们计划使其更加高效和稳健。例如，总是验证（即，即使攻击的可能性低，验证器总是验证）是性能缺陷，特别是在具有低敌意的区块链中。未来的工作包括应用游戏理论模型，因此验证者不是总是验证，而是以区块链敌意的一些概率进行验证。

此外，尽管每次提出新块时验证器的设置都会动态变化，但验证器的数量是静态的（即，lo n），这是一个可以被对手利用的知识。未来的解决方案是根据区块链的敌对因素使验证器的数量变得动态和可变。区块链节点定期学习这个因素并更新他们对网络的看法。结果，我们协议使用的验证器数量（以随机方式）与敌意因子成比例地变化。

最后，要考虑的一个限制是验证领导者节点可能产生非真正随机的分配。 这可能导致有效的验证者选择，并且如果验证领导者是恶意的并且与其他恶意节点合作，则可能危及网络的安全性。 一种可能的解决方案是让验证领导者参与上述游戏理论模型，以便在发生此类攻击时应用惩罚收益。 另一种解决方案是要求验证领导者提供某种工作证明。