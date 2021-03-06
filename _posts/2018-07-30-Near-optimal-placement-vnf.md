---
layout: post
title: Near Optimal Placement of Virtual Network Functions
excerpt: 
tags:
- NFV
- SFC

---

## Abstract

网络功能虚拟化（NFV）：网络功能在位于分布在网络中的小型云节点中的商用服务器上执行，其中软件定义机制用于控制网络流。这种模式是网络发展的一个重要转折点，因为它饱含了对增强经济网络服务的高期望，但同样是个技术挑战。在本文中，我们解决了该领域的主要技术挑战之一：**虚拟功能在物理网络中的实际部署。**部署对**网络性能**及其**可靠性**和**运营成本**具有重要影响。我们对NFV位置问题进行了彻底的研究，表明它引入了一种新的优化问题，并提供了**近似最优逼近算法**，保证了理论上经过验证的性能。评价方案表现的两个指标为：客户端与虚拟功能之间的距离成本，以及这些功能的设置成本。最后，使用广泛的模拟，我们表明所提出的算法在许多现实场景中表现良好。

## INTRODUCTION

近年来，我们正在观察对网络领域产生重大影响的几种演变趋势。
1. 正在向全IP网络（VoIP，LTE，IP DSLAM）的过渡。
2. 引入SDN，使数据与控制分离。
3. 云和新应用的出现，这些新应用正成为越来越多人的主要通信方式（例如，聊天应用，取代传统的语音呼叫和电子邮件）。
4. 最近的发展是NFV的出现，使网络功能在商业服务器上运行。

我们采用NFV论坛文档中使用的术语（参见原始白皮书）。
服务由一个或多个网络功能组成。每个功能的执行需要分布式服务器位置之一中的资源（计算，存储器，存储等）。在某些情况下，服务与特定网络节点相关联，并且必须在此节点上提供网络功能。例如，对于IMS服务，必须在运营商网络边缘执行SIP功能。但是，对于某些服务（如DPI），只要流是指向服务执行的位置，确切的网络位置就不重要。而且，不需要在单个服务器上执行整个功能。可以使用多个虚拟机（VM），同时使用SDN控制机制执行它们之间的流量分配和路由。然后问题是将服务器资源分配给各个位置处的网络功能，使得需要服务的所有流被满足，并且最小化操作成本。


**确定用于确定运营成本的确切指标。**我们遵循设施选址问题，并使用两种成本措施：（1）从客户到提供服务的地点的距离；（2）服务的设置成本。 总体成本定义为设置成本的总和，反映了具有执行功能的VM的成本，以及将流量转移到这些服务器的位置的成本。注意，当网络由具有节点之间的距离度量的图表表示时，从该图中的给定路径到节点的最短距离也是度量。因此（与facility location术语类似），我们使用术语“客户端”来指代相关流的路径。显然，在我们的模拟中，我们测量流路径和执行功能的位置之间的实际网络距离。

**本文工作。**我们的目标是：考虑全球网络和约束的同时，深入了解与底层网络中网络功能的位置相关的问题。为此，我们定义并研究了捕获网络功能虚拟化最重要方面的通用模型，然后评估了在各种实际使用案例中使用我们的方法的优势。

**问题描述。**通常，有一组客户端需要由一组网络功能服务，其中每个客户端需要一部分功能。定位功能是在实际环境中执行的，其中服务器分配功能的空间有限（在图中我们将此约束称为节点大小），我们的目标是以最小化整体网络成本的方式定位网络功能 ，同时坚持服务器的分配大小。我们将此问题称为NFV位置问题。

NFV位置问题包含了两个众所周知的NP-hard优化问题：<span class="tooltip" titles="Facility Location Problem">设施位置问题</span>和<span class="tooltip" titles="Generalized Assignment Problem">广义指派问题</span>，这两个问题在过去50年中都备受关注。设施位置问题要求打开一组设施为一组客户提供服务。在图表上定义了距离函数，并且每个客户端支付的连接成本等于提供服务的设施的距离。在节点上打开设施需要支付设置成本。目标是最小化连接成本和设置成本的总和。在设施位置问题的一些变体中，存在与每个设施相关联的容量，限制了可以获得服务的客户端的数量。在软容量的情况下，可以在节点处打开多于一个设施的副本。第二个优化问题是广义分配问题，其中给出了一组作业，要分配给一组机器。机器有容量限制，每个作业只需要分配给一台机器。每个作业的大小和成本都取决于机器。目标是找到满足大小限制的最小总成本的机器作业分配。

回到NFV位置问题，假设节点上没有大小限制。 这意味着功能可以彼此独立地位于节点处，因此定位每个功能的问题成为设施位置问题的实例。 相反，假设客户端和节点之间的所有距离都相等。功能没有容量限制，所以无需在其他位置再打开一个功能。因此，在这种情况下，我们得到了广义指派问题的一个实例。 总而言之，即使是最简单的NFV位置问题版本，在功能没有容量限制的情况下，也结合了两个经典的NP难题。

**NFV定位问题理论分析。**

1. 我们从统一需求开始，即所有客户具有相同需求的情况（单位需求而不失一般性）。首先，我们考虑功能不受限制的基本版本，即节点上的功能可以服务于任意数量的客户端。
2. 然后，我们考虑容量版本。但是，为了容纳更多客户端，可以在节点上定位多个函数副本。我们假设功能的容量与节点无关。
3. 最后，我们考虑最常见的版本，其中客户之间的需求可能不同。

我们所有的算法都提供了双标准近似因子。在问题的所有不同版本中，我们通过常数逼近目标函数

## 相关工作

本文为2015年，当时此方面的研究较少，主要介绍两个NP问题及其变体的研究。

该文<font size=1 color="gray">R. Ravi and A. Sinha. Approximation Algorithms for Multicommodity Facility Location Problems. SIAM Journal on Discrete Math, Vol. 24(2), pp. 538-551, 2010.</font>是这个问题的另一个变种，更接近我们的设置，并被称为多元商品设施位置。
该模型考虑了设施位置的自然扩展，其中存在有限的k个商品（对应于我们术语中的功能），并且每个客户需要这些商品的子集。然后，位置成本由固定设置成本（节点决定）和增量成本组成（商品决定）。节点上没有（容量）约束。该文提出了针对该问题的O(log*k*)近似算法。

>* 在[7]中提出了一个涉及多功能服务系统的工作，针对一个完全不同的环境，考虑到城市地区的警察系统。
* 在NFV和SDN的背景下，[3]考虑了单个服务（深度包检测），用启发式算法解决。
* [6]中介绍了虚拟化移动核心网络功能的放置，其中网络提供商需要在发生大型“大型”事件时提供最佳的蜂窝覆盖。虽然不接近我们的模型，但这些工作与我们的一般动机有关。

## 模型

#### 通用模型


#### GAP

近似算法基于求解（GAP-LP），然后将计算的分数解四舍五入为整数解。 显然，（GAP-LP）的最优解是最优积分解的下界。 四舍五入的整数解具有不超过最佳分数解的特性; 然而，它允许每台机器m分配到最多两倍的大小，这违反了可行性。