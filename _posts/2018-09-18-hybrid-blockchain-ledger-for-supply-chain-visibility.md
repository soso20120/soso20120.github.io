---
layout: post
title: A Hybrid Blockchain Ledger for Supply Chain Visibility
tags:
- Blockchain
- Supply Chain

---

## Abstract

通过提高贸易伙伴的可见度来优化实物分销可直接影响产品成本。然而，当前的供应链信息系统通常缺乏经济有效地将地面实况信息近乎实时地传递给所有利益相关者，最重要的是在运输过程中向供应商和客户传递的能力。本文提出了一种通过点对点架构解决这一差距的解决方案，该架构可以支持在供应链的物流分配阶段对可见性和及时交付信息的不断增长的需求。所提出的解决方案的附加特征包括传递给贸易伙伴的信息的可扩展性，隐私性和有效性。该解决方案使小型，中型和大型企业能够通过私有区块链子分类账以动态和以货物为中心的方式进行交互，该子分类帐将每批货物的托管链转移数字化。此私人分类帐中的信息由公共事件分类帐增强，该分类帐近乎实时地反映货件的移动。第三方监视器通过将事件形式的物理接近度发布到公共分类帐，从而验证货物的地理位置。

## INTRODUCTION

全球供应链（SC）是供应商，制造商，仓储商，运营商和客户之间交互和权衡的复杂而动态的组合，以便在合适的时间和正确的条件下提供正确的产品[1]。典型的SC包括八个主要流程：客户关系管理，客户服务管理，需求管理，订单履行，制造管理，供应商关系管理，产品开发和退货管理[2]。支持这些流程中的权衡决策以便最大化利润而不仅仅是为了最小化成本的数据分布在全球SC中，系统和基础数据的所有权根据所做出的决策类型而变化。在过去的二十年中，企业解决方案已经开发出来，将大多数这些流程数字化。此外，建立了电子数据交换（EDI）[3]标准，以实现贸易伙伴之间的自动电子文件交换。后来，SC运营网络（SCONs）[4]出现，以实现跨交易网络成员的全球交易。这些解决方案通常与各个合作伙伴的企业系统集成，从而使组织中SC流程的信息流能够扩展到其客户和供应商。

尽管有上述信息流功能，但仍存在重大差距。这种差距涉及在所有利益攸关方之间货物运输过程中实时共享货物的有效状态。通常，一旦它离开供应商的场所，货物通常由第三方（承运人）处理。运输状态信息通常由承运人转发给客户和供应商。遗憾的是，由于货运配送网络的复杂性，这种信息流通常不能及时有效地进行，这使得与利益相关者共享信息的延迟成为一种常见做法。本文介绍了一种众包解决方案（crowd sourcing solution），该解决方案可提高供应商和客户在货运过程中的可视性，这是SC订单履行流程的重要阶段。

第二部分将介绍相关工作。第III和IV节分别描述了拟议的设计及其实施。第五节总结了本文，并为今后的工作提出了方向。

## Related Work

拟议的框架在对等网络上使用区块链技术。该数据模型的第一个应用是数字货币比特币[5]。区块链分类帐中的每条记录都对应一个交易。一组交易被收集到一个块中，每个块被链接到分类账中的前一个区块上。在比特币实施中，分类账是公开的，并在所有参与者之间共享。此外，在将其添加到分类帐之前，每个块都由第三方-矿工验证-多数共识进行验证。这些共享和验证特征使区块链分类帐不可变且防止发生变化，而无需中央治理。

自比特币出现以来，区块链数据模型扩展到数字货币之外的其他各个领域。例如，在金融部门，区块链正在考虑进行自动清算和结算[6]。在卫生部门，已提出各种应用，从个人健康记录到管理假药[7]。区块链的其他应用包括电子政务和公共服务[8]。这些应用中的一些应用保持原始区块链数据模型（即，分布式对等网络上的公共分类账），而有些引入的修改数据模型以满足底层应用程序施加的隐私和安全要求。 [9]中介绍了各种区块链数据模型的完整分类。该分类法将区块链数据模型分为公共与私有，脱链与链上数据存储以及集中式/基于云的与分布式/对等体系结构。

区块链技术已被用于实现[10]和[11]中的端到端SC解决方案。后一个例子是基于云的，前者是分布式的。两种解决方案都依赖于私人分类账。其他SC区块链应用包括B2B交易[12]和产品所有权管理[13]。本文提出了区块链技术在SC领域的新应用，**专门针对分销阶段贸易伙伴之间的可见性差距**。此外，为了在利用区块链技术的益处的同时满足目标应用的实际要求，提出了一种由分布式对等通信平台上的混合私有/公共分类账组成的新架构。

## System Design

所提出的混合对等物理分发（HP3D）[14]，[15]框架的体系结构如图1所示。该框架由索引服务器，节点，管理节点和外部监视器组成。

索引服务器从参与网络的节点收集IP地址，并根据请求与其他节点共享它们。每个对等体（即节点）必须以规则的时间间隔向索引服务器发送心跳消息，以便保持其信息最新。

节点是网络中可以与任何贸易伙伴关联的对等体。每个货物与私人分类帐相关联，并且允许参与该货物的节点通过使用相应的私有对等子网络来交换货运信息。

对于每个贸易伙伴，其中一个节点被指定为管理节点。该节点参与涉及贸易伙伴的所有子网络，并充当合作伙伴的内部信息系统（例如，ERP，CRM，传感器）和HP3D之间的接口。管理节点允许每个组织将相关的装运信息导出到其贸易伙伴。此外，它还存储所有与货件相关的消息，并充当丢失与网络连接的对等方的备份。

HP3D中的第四种组件是外部监视器。这些监视器验证运载货物的卡车的地理位置（即经度和纬度），并将该现场信息发布到公共分类帐。此分类帐中的信息在公共对等网络中共享（图1），并由客户和供应商访问，以便检索其货件的最新地理位置。

#### Blockchain Model

拟议系统中使用的区块链模型由私人子分类账和单个公共分类账组合而成。 此设计旨在保护贸易伙伴的隐私，同时向他们提供来自现场的准确信息。 每批货物中的贸易伙伴都维护一个私人子分类帐。 但是，公共分类账由外部监控人员维护。 **这种方法将私人信息和公共信息分开，并使用私人子分类帐获取货物信息，并使用公共分类帐获取与货物在运输过程中相关的地理定位信息。** 两个分类账都是**分布式的**，包括三种类型的事件，如图2的示例所示。

* 原始事件启动装运，并在由客户向供应商发出采购订单时触发。
* custody event托管事件构成以货件为中心的子分类帐，对于供应商，承运商和客户而言是私有的。这些合作伙伴中的每一个都将其分类帐的副本存储在本地数据库中。
* 监视事件由外部监视器提交给公共分类帐。 想要参与网络的每个监视器必须从其他监视器获取最新的公共分类帐。 公共分类帐存储在监视器的本地数据库中。

在公共和私人分类账中，事件由发行者进行数字签名，并且一组事件被组合成链接到其他块的块。这些事件块在参与者之间不断共享。

**就私人子分类账而言，参与者是特定货物的客户，供应商和承运人。**在公共分类帐的情况下，参与者是外部监视器。当运货卡车在外部监视器（例如，另一车辆）的物理附近时，在卡车和监视器之间建立无线电通信信道。然后，监视器将向卡车发送挑战（随机数），卡车用他的私钥签名并将签名发送回监视器。外部监视器使用卡车的公钥验证签名，使用监视器的私钥对卡车的当前地理位置进行签名，并将监视事件发布到公共分类帐。在此模型中向私人和公共分类账发布事件受若干支持和核心流程的约束，这些流程将在下面讨论。

#### Support Processes

HP3D的主要支持流程是：a）建立以货运为中心的子网，b）查询IP地址和c）移动对等身份验证。 在装运信息可以在贸易伙伴之间共享之前，必须建立以装运为中心的子网络。 也就是说，同行需要知道有关同一货件中涉及的其他同行的信息。 此信息通常包含在由客户的ERP系统发布并与其他贸易伙伴共享的采购订单中。 客户的管理节点将从客户的ERP中检索采购订单，并使用该信息建立以货件为中心的子网络。

第二个进程，查询IP地址，涉及查询索引服务器有关其他对等体的IP地址（图3）。对等体通过向索引服务器发送目标对等体的ID来启动查询IP地址进程。然后，索引服务器将在其本地数据库中搜索相应的对等IP，如果数据库中不存在目标对等ID，则使用0.0.0.0 IP地址进行回复。否则，索引服务器将比较目标对等方的时间戳与当前系统时间。如果这两次之间的差异大于某个预设阈值，则表示目标对等体未激活，它将回复1.1.1.1 IP地址。否则，目标对等方处于活动状态，索引服务器将回复目标对等方的IP地址。此支持过程在对等体之间进行任何交换之前启动，以确保IP地址是最新的，因为网络中的大多数对等体预期是移动设备，并且当它们进出网络时它们的IP可能会发生变化。

第三个支持流程包括防止未经授权的移动用户参与网络的身份验证。此过程依赖于IMEI号，该号码在所有设备上都是唯一的，用于识别移动设备。移动对等体认证过程包括密钥交换，然后验证移动设备的IMEI号，如图4所示。假设移动设备和索引服务器已交换必要的密钥以保护后续通信，移动设备将检索其IMEI号并加密它。然后将加密的IMEI号发送到索引服务器。索引服务器将依次解密IMEI号并使用它来搜索其本地数据库。如果在数据库中预先注册了该号码，则索引服务器为移动设备生成ID并将其返回给发布设备。如果在数据库中找不到该设备，则会生成错误。但是，不会返回任何消息以防止索引服务器因错误或恶意请求而过载。

#### Core Processes

HP3D有三个核心流程，即a）心跳消息，b）本地传感器消息和c）地理定位更新。心跳消息由网络中的活动节点周期性地发送到索引服务器。收到心跳消息后，索引服务器将更新服务器数据库中发布节点的时间戳。

第二个核心流程涉及与贸易伙伴共享合作伙伴的内部信息。例如，公司可能在其本地操作内部具有传感器或检查点信息，他们可能愿意与其贸易伙伴共享（例如，装运/卸载）。公司的管理节点负责获取这些传感器信号并将相关消息广播到同一公司的其他节点。此节点将更新其本地数据库，然后将消息广播到货件中涉及的其他贸易伙伴的节点。为此，它将向索引服务器查询与货件关联的其他节点的最新IP地址。例如，当供应商想要通知承运人关于装货点处货物的可用性时，使用该过程。

第三个核心流程是地理位置更新流程（图5），该流程允许贸易伙伴共享货件的地理位置状态。工作流程从查询由监视器维护的公共分类帐的节点开始。该节点将主要与客户和供应商相关联，因为这些是在运输的运输阶段缺乏现场可见性的合作伙伴。外部监视器将在其本地数据库中搜索目标卡车ID，并使用相应卡车的最新地理位置更新来回复请求节点。然后，请求节点将更新消息广播给贸易伙伴。

## System Implementation

HP3D的核心和支持流程已在多个常用平台上实施。 此外，还开发了一个模拟器，以在拟议框架中触发所需的事件序列。 索引服务器和节点的软件应用程序具有三层体系结构，具有表示层，中间层和数据层。 在索引服务器和管理节点的情况下，Javascript和HTML用于表示层，MGO和Golang用于中间层，MongoDB用于数据层。 对于移动节点，Couchbase Lite用于数据层。 HP3D中节点之间的数据交换使用JSON格式。 接下来讨论这些应用程序的基础模块。

#### Data Structure

为了支持HP3D中所需的数据交换，有三种类型的数据结构，即：a）节点信息，b）订单信息和c）卡车地理定位信息。 索引服务器在其本地数据库中为包括移动节点在内的所有对等体维护节点信息。 Peers交换订单信息，该信息被加密并存储在以货件为中心的子分类帐中。 外部监视器使用Truck Geolocation数据结构来记录卡车的经度和纬度，并将此信息发布到公共分类帐。

如上所述，**节点信息**用于节点和索引服务器之间交换的消息中。 它由以下六个领域组成。

* Reqtype是一个标识请求类型的整数：
	2. Reqtype 0对应于心跳消息。
	3. Reqtype 1对应于IP地址查询。
	4. Reqtype 2对应于使用IMEI号进行验证。
* timestamp字段是用于Reqtype 1的系统时间。
* IPAddr字段包含目标节点的IP地址。 如果未找到目标节点或它处于非活动状态，则分别返回IP地址0.0.0.0或1.1.1.1。
* 密钥和IMEI字段是字节数组，用于移动验证例程。
* ID字段包含由索引服务器生成的节点的唯一ID。

第二种数据结构，**订单信息**（图6），用于支持第二种类型的消息（即托管事件）。 托管事件的一个例子如图2所示。它表示货物从一方（例如供应商）转移到另一方（例如承运人）。 订单信息基于EDI214 [3]标准。 该标准在SC中广泛用于装运状态消息。

订单信息由以货件为中心的子网络中的节点交换，并用于更新参与节点中每个子分类帐的副本。 该数据结构由五个主要字段组成：OrderDetails和四个散列值：先前事件散列值，当前事件散列值，先前块散列值和当前块散列值。 事件和块哈希值分别用于在块内和私有分类帐中的块之间创建链。

OrderDetails（图6）是订单信息数据结构的子组件，其字段符合EDI214标准运输承运人货件状态消息。 具体地，在Loop1100中，AT7是为货物的带时间戳状态保留的段，MS1用于装运位置，MS2用于识别所有者。 代码MS104（经度）和MS105（纬度）用于捕获货物的地理位置。

**监视事件**是第三种类型的消息。 用于支持监视事件的数据结构包括五个字段：监视信息，先前事件哈希值，当前事件哈希值，先前块哈希值和当前块哈希值。 与订单信息的情况一样，事件和块哈希值用于将事件链接到前一事件或块到公共分类帐中的前一块。 在监控信息下分组的其余字段包括以下内容：

* MonitorID：发出事件的外部监视器的ID。
* 时间戳：事件发生的时间。
* 显示器看到卡车的位置的经度和纬度。
* TruckID：卡车的唯一ID。

以下小节说明了索引服务器，监视器和HP3D中的节点如何使用上述三种数据结构来交换信息。

#### Index Server

索引服务器参与两个不同的支持过程。 它一直处于活动状态，以便接收和处理来自所有节点的请求。 它侦听传入的请求，在发生连接时接受连接并调用receiveMsg（）（图7），该调用使用上述节点信息数据结构提取连接中的数据。 然后使用Reqtype字段来调用与请求类型相对应的操作。 例如，queryByCode（）函数用于在另一个节点请求时检索目标节点的IP地址。 它将ID作为输入条件，并在节点信息数据结构中返回文档。 同样，UpdateTime（）函数用于处理传入的心跳消息。 该函数首先调用queryByCode（）来查找发布节点的当前记录，然后更新与索引服务器数据库中的节点相关联的时间。

#### Network Node

网络中的每个节点都必须侦听和处理传入的消息。 例如，为了处理来自管理节点的更新消息，给定节点必须侦听传入消息，如图8所示。一旦接收到新连接，将调用receiveSensorMsg。 节点将使用图6中所示的Order Details EDI214数据结构从连接中提取传入消息。然后，它将更新其本地分类帐并将事件发送到其他节点。 函数UpdateDatabase（）（图9）用于所有三种类型的事件（即创世，保管和监控）。 它计算哈希值，链接连续事件和块并更新分类帐。 目前，块大小是预定义的。 未来的工作将根据交换量探索动态块大小。

#### Example Test Scenario

建议的框架在由索引服务器，两个外部监视器（M1和M2），区块链参与者（P4）和三个节点组成的环境上进行测试。 后面的节点代表给定货物的客户（P1），供应商（P2）和承运人（P3）。 测试场景中的事件由事件模拟器触发。 接下来描述的测试场景显示了在不同参与者之间交换的消息。

图10显示了触发由客户（P1）发起的创世纪事件的模拟器，并代表了货物分配阶段的步骤1。然后，客户通过查询其他子网络参与者（即，供应商（P2）和运营商（P3））的IP地址来建立用于货件的子网络。客户还将创世纪事件的详细信息发送给供应商和承运人。该信息存储在图10的步骤3中的这些参与者的私人分类帐中。在第四步中，客户计算起源事件的散列值并将该信息发送给包括监视器（M1和M2）和其他区块链参与者（P4）。验证后，此信息将添加到公共分类帐。

图11显示了步骤2,3和4中消息的内容。在步骤2中，客户通过使用类型1请求和供应商的ID来请求供应商的IP地址。索引服务器返回请求的IP地址。在步骤3中，客户将创世纪事件发送给供应商。创建事件的哈希值也由客户计算并在步骤4中发送到参与公共分类帐的节点。

在测试场景的第二阶段，模拟器用于触发custody event，如图12所示。

此custody事件表示承运人的卡车到达供应商（P2）处所。 供应商创建此保管事件并与货件中的参与者共享（P1和P3）。 为了开始这个阶段，供应商首先向索引服务器发送请求，以获得参与者的最新IP地址。 该步骤类似于客户在上面讨论的起源事件开始时执行的步骤。 使用索引服务器返回的IP地址，供应商然后将保管事件消息发送给货件中的参与者。 此外，与发生事件的情况一样，custody事件的哈希值也由供应商计算并发送给公共分类账的参与者（即P4，M1和M2）。 这种情况下的消息类似于图11中所示的消息。

在交付货物的卡车在物理上接近监视器时触发monitoring事件，在这种情况下接近监视器M1。 测试场景的第三阶段如图13所示。监视器（M1）将图14所示的事件消息广播到整个网络。 验证后，此事件将添加到公共分类帐。

## Conclusions

SC是从制造商到客户交付货物的端到端流程。它包括要求几个贸易伙伴互动的不同阶段。本文提出了一个框架，通过在该阶段的物流部分提供近实时可见性，可以提高SC的订单履行阶段的效率。建议的框架使用混合对等体系结构，该体系结构允许为每个货物动态创建子网络。通过增强的区块链模型来促进所交换数据的隐私性和有效性，该区块链模型将私有子分类账与公共分类账相结合。

需要进一步研究以改进拟议的框架，特别是在公共分类账方面。例如，需要机制来整合与单个卡车相关的不同监控事件。鉴于可以发布到公共分类帐的大量事件，还需要允许有效搜索给定卡车ID和修剪公共分类帐的方法。最后，需要在具有多个参与者的大型SC网络内评估这些和其他操作的性能。