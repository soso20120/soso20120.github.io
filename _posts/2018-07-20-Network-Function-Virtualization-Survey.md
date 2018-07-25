---
layout: post
title: Network Function Virtualization：State-of-the-art and Research Challenges
excerpt: 
tags:
- NFV

---

## 1. Introduction

#### 背景：
* 目前的网络功能实现都是依靠特定的设备，而且服务组件有严格的连接。
* 而且协议要求高质量、稳定、严格的服务，使得产品周期长，敏捷性低，严重依赖于专用硬件。
* 用户对多样化、高速传输服务的要求仍不断增加。供应商需持续购买新设备密集部署，还需要高技术人员，使得费用（<span class="tooltip" titles="Opreating Expenses 营业费用">OPEX</span>和<span class="tooltip"  titles="Capital Expenses 资本支出">CAPEX</span>）增高。
* 而且，由于高竞争，这些投资无法转化为更多的利润。因此必须寻找更具动态和服务意识的网络。

#### NFV
* <span class="tooltip" titles="Network Function Virtualization 网络功能虚拟化">NFV</span>是用于将功能和物理网络设备分离。
*这意味着可以将网络功能（例如防火墙）作为普通软件的实例发送到TSP。*
* 许多网络设备可以合并到大容量服务器、交换机和存储器上。于是，在无需购买安装新硬件的情况下，运行一个或多个软件就可以实现一组虚拟网络功能。
* NFV具有更好的<span class="tooltip" titles="flexibility">灵活性</span>，部署新网络更快、更便宜。
	1. 软硬件分离。发展是独立的，开发时间表可以分离。
	2. 灵活的部署。分离后有利于重新分配和共享基础资源，因此，软件和硬件可以在不同事件执行不同的功能。
	3. 动态调整。根据实际流量提供。
* 还可以使用在虚拟化资源和硬件上运行的功能的混合方案。这在向NFV过度阶段非常有用。

#### NFV的历史
* 2012年10月诞生，由一批领先的<span class="tooltip" titles="Telecommunication Service Providers">TSPs</span>共同撰写了一份白皮书。*<font color="gray" size="1">R. Guerzoni, “Network Functions Virtualisation: An Introduction, Benefits, Enablers, Challenges and Call for Action. Introductory white paper,” in SDN and OpenFlow World Congress, June 2012.</font>*
* 2012年11月，7家运营商(AT&T, BT, Deutsche Telekom, Orange, Telecom Italia, Telefonica and Verizon)选择<span class="tooltip" titles="European Telecommunications Standards Institute 欧洲电信标准协会">ETSI</span>作为NFV行业规范的所在地。
* 2015年1月ETSI已完成第一阶段，出版了11个规范，包括基础架构概述，更新的架构框架以及基础架构的计算，虚拟机管理程序和网络域的描述，管理和协调，安全性和信任，弹性和服务质量指标。

#### NFV的案例
##### 1.应用于<span class="tooltip" titles="Customer Premises Equipment 客户端">CPE</span>
图1中示例，一个CPE由8个部分组成：<span class="tooltip" titles="Dynamic Host Configuration Protocol 动态主机配置协议">DHCP</span>，<span class="tooltip" titles="Network Address Translation 网络地址转换">NAT</span>，<span class="tooltip" titles="Universal Plug and Play 通用即插即用">UPnP</span>，路由，防火墙，调制解调器，无线电，交换机。这些功能可能有顺序要求。目前都是在客户所在场所的物理设备预设好。一旦需要更改功能时，<span class="tooltip" titles="Internet Service Provider 互联网服务提供商">ISP</span>的技术人员需要与每个客户商议，甚至有可能完全更换设备。这种操作很昂贵。

图2中基于NFV实现的案例，CPE的功能由ISP处的一个共享的基础设施实现。基于上述场景，在ISP中就能简单更新DHCP，或者为一部分人或所有人增加父母监控的功能。不仅节约操作费用，而且大规模应用下，CPE也能更便宜。

![NFV applied in CPE](/assets/img/nfv-applied-in-cpe.JPG)

##### 2.应用于<span class="tooltip" titles="Evolved Packet Core Network 分组核心网">EPC</span>
EPC是<span class="tooltip" titles="Long Term Evolution">LTE</span>的核心网络。图3左展示了LTE的基本架构。<span class="tooltip" titles="User Equipment">UE</span>通过E-UTRAN连接到EPC。EPC执行基本功能，包括用户跟踪，移动性管理和会话管理。由四个部分组成：<span class="tooltip" titles="Serving Gateway">S-GW</span>，<span class="tooltip" titles="Packet Data Network Gateway">P-GW</span>，<span class="tooltip" titles="Mobility Management Entity">MME</span>，<span class="tooltip" titles="Policy and Charging Rules Function">PCRF</span>。并且EPC还连接到外部网络，外部网络可以包括<span class="tooltip" titles="IP Multimedia Core Netword Subsystem IP多媒体核心网子系统">IMS</span>。目前EPC的所有功能都是基于专有设备。所以微小的改动都需要更换设备。

图3右则展示了EPC虚拟化的架构。这种方式更灵活、动态调整，做出更改更容易也更便宜。而且还可以更简单的软件升级，更快地革新。

 ![NFV applied in EPC](/assets/img/nfv-applied-in-epc.JPG)

#### 未解决的问题
* 实施是否转化为最初预期的好处。
* 有一些重要且未开发的研究挑战需要解决，例如测试和验证，资源管理，互操作性，实例化，VNF的性能等。
* 即使是正在探索的领域，如MANO，仍然存在悬而未决的问题，特别是在支持异质性方面。

目前文献的局限性：
* 在范围方面，他们没有考虑NFV的重要方面，例如它与SDN和云计算的关系。
* 对标准化活动进行有限的审查和分析。
* 对正在进行的研究和挑战的不完整的描述。

## 2. NFV架构及局限性
由ETSI提出

![NFV architecture proposed by ETSI](/assets/img/NFV-architeture-proposed-by-ETSI.JPG)

#### <span class="tooltip" titles="Network Funciton Virtualization Infrastructure 基础设施">NFVI</span>
* NFVI是硬件和软件的结合，**构成了部署VNFs的环境**。
* **物理资源**
	1. 商业现货（COTS）计算硬件
	2. 存储和网络（由节点和链路组成），为VNF提供处理，存储和连接。
* **虚拟资源**是计算，存储和网络资源的抽象。使用虚拟化层（基于管理程序）实现抽象，虚拟化层将虚拟资源与底层物理资源分离。
	1. 在数据中心环境中，**计算和存储资源**可以用一个或多个虚拟机（VM）表示
	2. **虚拟网络**由虚拟链路和节点组成
		*  **虚拟节点**是具有托管或路由功能的软件组件，例如封装在VM中的操作系统
		* **虚拟链路**是两个虚拟节点的逻辑互连，它们作为具有动态变化属性的直接物理链路出现。

#### <span class="tooltip" titles="Virtual Network Fuction and Services 虚拟网络功能">VNFs</span>
* 一个网络功能是网络基础设施中的功能块，有定义好的外部接口和功能。
* NF的实例：网关，DHCP，防火墙等。
* VNF部署在VM这样的虚拟资源上。
* 一个VNF可能由多个组件组成。
* 无论是基于专用设备还是基于VM的网络功能，在用户看来都是一致的。

#### <span class="tooltip" titles="NFV Management and Orchestration 管理和编排">NFV MANO</span>
* 管理硬件和软件资源的编排和生命周期，以及VNF的生命周期。
* 它还包括用于存储信息和数据模型的数据库，这些模型定义了部署以及功能，服务和资源的生命周期属性。
* 此外，该框架还定义了可用于NFV MANO不同组件之间通信的接口，以及与传统网络管理系统（如操作）的协调。

#### 局限性
* 没有考虑旧设备的控制和管理，难以指定旧设备与VNF端到端服务的操作。
* 还没有VNF，基础设施，MANO的最佳实践和参考实现，以及所需接口的详细定义。
* 供应商之间的看法不统一，应尽早解决接口定义等问题。

## 3.A 商业模式

![proposed-nfv-business-model](/assets/img/proposed-nfv-business-model.JPG)

#### <span class="tooltip" titles="Infrastructure Provider 基建供应商">InP</span>

* InP以数据中心和物理网络的形式部署和管理物理资源，并且决定如何将可用资源分配给TSP。
* 可以通过编程接口向一个或多个TSP提供和租用虚拟资源。
* 在NFV中，InP的示例可以是公共数据中心，例如亚马逊的公共数据中心，或TSP拥有的私人服务器。

#### TSP

* TSP从一个或多个InP租用资源运行VNF，并且确定这些功能的链接。
* TSP也可以将虚拟资源分租给其他TSP，此时它的角色是InP。
* 在InP是私有或内部的情况下，例如由TSP网络节点或服务器提供，则InP和TSP可以是一个实体。

#### <span class="tooltip" titles="VNF Providers">VNFPs</span>和<span class="tooltip" titles="Server Providers 服务器提供商">SPs</span>

* 传统网络设备供应商被分为两个部分：VNFP和SP。
* VNFP是为NF提供软件实现。它可以直接提供给TSP，也可以提供给InP。
* TSP开发自己的NF（软件）的情况下，VNFP和TSP将是一个实体。
* SP提供可以部署VNF的行业标准服务器。
* 服务器提供给InP时，功能将在云中运行；提供给TSP时，功能在TSP的网络节点中运行。
* 分开的好处是，TSP可以从一个实体购买VNF，从另一个实体购买服务器。

#### Brokers代理

* 当TSP从多个VNFP购买功能，或将多个InP资源部署到端到端的服务，需要代理人的角色。
* 代理的作用就是：已知资源和需求的情况下，协调、汇总资源（InP、VNFP、SP），再提供给TSP。
* 此角色仅包含在完整性模型中，因为在NFV生态系统的所有情况下可能不需要此角色。

#### 最终用户

* 最终用户是服务的最终消费者。
* 用户可以连接到多个TSP，以获得不同的服务。

## 3.B 设计注意事项

#### 性能

* NFV架构应该能够实现类似于在专用上运行的功能所获得的性能。
* 由于处理器卸载技术（例如数据移动的直接存储器访问和用于CRC的硬件辅助），需要与高带宽、低延迟的接口连接。
* 还有一些VNF需要由NFVI提供的硬件加速（例如<span class="tooltip" titles="Deep Packet Inspection 深度报文检测">DPI</span>）。
* 已有一些研究利用<span class="tooltip" titles="Data Plane Development Kits 数据平面开发套件">DPDKs</span>运行VNF，进行小型和大型的分组处理，性能接近原生非虚拟的。
* 也有研究证明FPGA可以提高VNF的性能。

#### 安全性和适应性

* NFV的动态性质要求安全技术，政策，流程和实践嵌入其遗传结构中。
* 来自不同订购者的功能或服务应相互保护/隔离，使它们不会对方的漏洞相互影响。
* 应保护NFVI不受所提供的订购服务的影响，可以通过防火墙实现。
* 相同服务的功能不应由同一安全域的物理资源托管。

#### 可靠性和可用性

* 电信业中，由于监管的需求，需要毫秒级的响应。
* 但是不是所有功能都要求高，比如电话对可用性要求最高，短信服务则较低。
* 可以定义多个可用性类，由NFV框架支持。
* 可以部署具有冗余的功能。

#### 支持异质性

* 任何NFV平台必须是开放共享环境，能够运行来自不同供应商的应用程序。
* InP必须能自由的做出硬件选择决策，更换硬件供应商并处理异构硬件。
* 平台应该能够屏蔽VNF与底层网络技术的细节（例如，光学，无线，传感器等）。
* 平台应该允许，不受限制地在多个基础结构域上创建端到端服务，并且不需要特定的解决方案。
* 用户应该可以从当前的TSP或其它已覆盖的TSP中自由选择服务，

#### 支持旧版

* 完成NFV转向需要过渡时间，因此需要既能物理的，也能支持虚拟NF。
* InP必须能够在虚拟化和物理环境中运行网络功能。

#### 可扩展性和自动化

* 所有功能都能自动化的情况下，NFV才会扩展。比如，目前都是通过VM实现VNF。如果每个NFV都部署一个VM，不仅占空间大、成本高，还会导致虚拟化层的可伸缩问题。
* 对动态环境的需求要求可以按需部署和删除VNF，并进行扩展以匹配不断变化的流量。

## 4. NFV与SDN与云计算

#### 云计算

云计算中，服务提供分为两个部分：
* <span class="tooltip" titles="infrastructure providers">基础设施提供者</span>：管理云平台，根据基于使用的定价模型租赁资源
* <span class="tooltip" titles="service providers">服务提供者</span>：从一个或多个基础设施提供商处租用资源来为最终用户提供服务

**特点**
* 按需自助服务：消费者提出需求的计算能力，如服务器时间和网络存储，无需人工交流。
* 广泛的网络访问：允许不同平台的客户机访问。
* 资源池：按消费者需求动态分配不同的物理和虚拟资源。
* 快速弹性：根据需求快速向内和向外扩展。
* 测量服务：云系统通过在适合于服务类型（例如，存储，处理，带宽和活动用户帐户）的某种抽象级别上利用计量能力来自动控制和优化资源使用。

**服务模型**
* <span class="tooltip" titles="Software as a Service 软件即服务">SaaS</span>：可以通过瘦客户机访问云上的应用程序。
* <span class="tooltip" titles="Platform as a Service 平台即服务">PaaS</span>：提供用户应用程序的运行环境，但是用户只能使用云提供编程语言、库、服务和工具。
* <span class="tooltip" titles="Infrastructure as a Service 基础架构即服务">IaaS</span>：将硬件设备等基础资源封装成服务供用户使用。

![cloud-service-model-and-mapping-to-nfv](/assets/img/cloud-service-model-and-mapping-to-nfv.JPG)

**云计算与NFV的关系**
* 由于NFV起源于电信业，且在电信业中发展更好。接下来都在运营级网络讨论。
* 目前NFV的早期实现是基于在云中的专用VM上部署功能。
* 在云中部署NF可能会改变服务和应用程序开发和交付方式的各个方面。
* 电信网络在以下三个方面与云计算环境不同：
	1. 电信网络的数据平面工作负载更高，需要更高的性能。
	2. 电信网络的拓扑结构对网络提出了严苛的要求。
	3. 电信行业需要可扩展性，可靠性和可用性。

![comparison-of-nfv-and-cloud](/assets/img/comparison-of-nfv-and-cloud.JPG)

**现有基于云的NFV的研究**
* OpenStack虽然被确定为基于云的NFV架构的组件之一，但它不提供包括服务质量（QoS）要求在内的网络资源的详细描述，也不支持资源预留服务，因此不提供任何资源预留接口。
* OpenANFV提出了一种基于OpenStack的框架，使用硬件加速来增强VNF的性能。

#### <span class="tooltip" titles="Software Defined Networking 软件定义网络">SDN</span>

SDN解耦网络控制和转发功能，允许网络控制通过开放接口直接可编程。它能简化网络管理。

**特点**
* 可编程的：由于控制与转发功能分离，是网络控制可编程。该特性可用于自动化网络配置。
* 敏捷：管理员可以动态调整网络范围的流量以满足不断变化的需求。并且该逻辑在软件中实现，发布周期更短。
* 集中管理：SDN控制器维护网络的全局视图。
* 基于开放标准和供应商中立：通过开放标准实施时，SDN简化了网络设计和操作。

**SDN和NFV的关系**
* 与NFV旨在在行业标准硬件上运行NF的方式相同，SDN控制平面可以实现为在行业标准硬件上运行的纯软件。
* NFV和SDN可能是高度互补的，可以将它们组合在一个网络解决方案中。比如，SDN控制器可以成为服务的一部分链。这意味着SDN中的控制和管理程序（如负载平衡、监控和流量分析）可以实现为VNF。同样，SDN可以通过提供灵活，自动化的链接功能，配置和配置网络连接和带宽，操作自动化，安全性和策略控制来加速NFV部署。（未证实）
* SDN和NFV是不同的概念，旨在解决软件驱动的网络解决方案的不同方面。
* NFV的目标是将NF与专用硬件元件解耦；而SDN则侧重于将数据包和连接的处理与整体网络控制分开，虚拟化是将抽象资源分配给特定客户端或应用程序。
* NFV可以在现有网络上工作，而SDN需要一个新的网络结构，它的数据和控制平面是分开的。

![comparison-of-nfv-and-sdn](/assets/img/comparison-of-nfv-and-sdn.JPG)

**现有基于SDN的NFV的研究**
NFV的独特需求可能需要一个大规模复杂的转发平面，将虚拟和物理设备与广泛的控制和应用软件相结合，主要从两个方面改进SDN：
* the Sounthbound API(OpenFlow):
	1. OpenFlow是SDN南向API的事实上的实现，但它并不是一个成熟的解决方案。因为Open-Flow针对L2-L4流程处理，所以它没有应用层协议支持和面向交换机的流量控制。因此，用户必须为上层流控制安排附加机制。所以，必须扩展OpenFlow以包括能够支持NFV的层L5-L7。
	2. 在虚拟EPC功能的实现中，通过定义虚拟端口来扩展OpenFlow1.2，实现封装和使用GTP隧道端点标识符（TEID）进行流路由。
	3. OpenFlow的部署仍依赖于单个控制器。扩展性差，可靠性差。因此，需要通过分布式架构来改进SDN。

* 控制器设计
	1. OpenNF提出了一种控制平面，它允许在NF实例集合中重新分配数据包处理，并在每个NF和控制器之间提供通信路径，以进行配置和决策。它使用事件和转发更新的组合来解决竞争条件，绑定开销以及适应各种NF。另外，有人设计了一个协议实现VNF和控制器之间的通信。*<font color="gray" size="1">J. Batalle, J. Ferrer Riera, E. Escalona, and J. Garcia-Espin, “On the Implementation of NFV over an OpenFlow Infrastructure: Routing Function Virtualization,” in Future Networks and Services (SDN4FNS), 2013 IEEE SDN for, Nov 2013, pp. 1–6.</font>*最后还有人提出了同时考虑SDN和NFV的架构。*<font color="gray" size="1">M. R. Sama, L. M. Contreras, J. Kaippallimalil, I. Akiyoshi, H. Qian, and H. Ni, “Software-defined control of the virtualized mobile packet core,” Communications Magazine, IEEE, vol. 53, no. 2, pp. 107–115, Feb 2015.</font>*
	2. OpenDaylight是在单一控制平台中支持广泛地集成技术的SDN控制平台。它是开源的。OpenDaylight计划的目标是通过开源SDN和NFV解决方案为可编程性和控制创建参考框架。

![relationship-between-nfv-sdn-cloud](/assets/img/relationship-between-nfv-sdn-cloud.JPG)

## 5. NFV的主要项目和早期实现、用例、商业产品

#### 标准化工作
* IETF服务功能链接工作组：因为服务中的功能都有严格的链接和顺序要求，放入云中前必需考虑这点。IETF SFC WG工作组旨在为服务功能链建立框架。
* IRTF NFV研究组：该小组的目的是在主要会议上组织会议和研讨会，并邀请知名出版物的特刊，共同研究NFV相关的问题。
* ATIS NFV论坛：由一家北美电信标准组织创建，该小组旨在开发NFV的规范，重点关注NFV的各个方面，包括运营商间的互操作性以及新的服务描述和自动化流程。
* Broadband论坛：致力于开发宽带网络规范的行业联盟。正在研究如何在多业务宽带网络中实施NFV。

![summary-of-nfv-standardizaiton-efforts](/assets/img/summary-of-nfv-standardizaiton-efforts.JPG)

#### 协作NFV项目
* <span class="tootip" titles="Zero-time Orchestration, Operations and Management 零时间编排，运营和管理">Zoom：</span>一个TM论坛项目，旨在定义实现VNF交付和管理所必需的运营环境，并确定将保护NFVI和VNF的新安全方法。

![summary-of-nfv](/assets/img/summary-of-nfv.JPG)

#### 实现

![summary-of-nfv-implementations](/assets/img/summary-of-nfv-implementations.JPG)

## 6. Future Exploration

#### 管理和编排

* NFV的部署要求改变现有的管理系统，使现有的功能都在连贯的基础上实例化，并确保方案仍可管理。
* 克莱曼等描述了一种基于协调器的体系结构，该体系结构确保虚拟节点的自动放置以及由它们收集和报告资源行为的监视系统支持的网络服务的分配。
* 目前的方案并没有结合SDN和NFV的要求。

#### 能源效率

* 基于NF的云在节省能源方面有巨大的潜力
* 但应该在节能和性能之间做决策

#### NFV性能

* ETSI的专项组证明，如果遵循最佳实践，不仅可以实现高性能，还是可预测的。
* 但有一些高性能NF可能难以虚拟化而且不会降低性能，虽然考虑硬件加速的解决方案，但是这违背了NFV的灵活性的理念。
* 对NFV进行分阶段迁移也是合适的，其中具有可接受性能的那些功能首先被虚拟化并且允许与非虚拟化或物理性功能一起运行。

#### 资源分配

* 需要有效的算法决定哪个物理资源部署哪个网络功能，能将一个功能移到另一个服务器，以实现负载平衡、节能、恢复等。
* 根据Mehraghdam的研究，在网络受限的情况下，应根据目标来部署功能。但这是一个NP-hard的优化问题。
* NFV系统应允许将一个或一组VNF迁移到不同的物理服务器。此时不仅要考虑效率，还要综合的管理。
* 不应该一个功能放在一个VM上，有的功能很轻，有的则无须隔离。可以考虑使用容器。
* 即使给定的功能必须在VM的操作系统中使用相同的资源，也可以使用调度技术来允许功能共享资源。

#### 安全，隐私和信任

* ETSI的安全专项组确认NFV存在一些安全问题。它们也提出了一些解决方案，但是并不详尽。
![potential-security-threats-in-nfv](/assets/img/potential-security-threats-in-nfv.JPG)
* 随着NFV的发展，信息截取也将会是一个威胁。

#### 资源，功能和服务建模

* 为这些多供应商资源，功能和服务提供易于理解，开放和标准化的描述符将是大规模NFV部署的关键。
* 建模时应考虑初始化部署、生命周期管理等。
* ETSI提出三个模型：
	1. **<span class="tooltip" titles="Topology & Orchestration Standard for Cloud Application 云应用程序的拓扑和编排标准">TOSCA</span>**:使用OASIS标准语言，用于描述基于云的Web服务的拓扑，其组件，关系以及管理它们的过程。TOSCA可用于VNF定义，节点监控以及诸如修复和扩展的主动策略。
	2. **NETCONF/YANG**:是IETF定义的“安装，操作和删除网络设备配置”的协议。
	3. **<span class="tooltip" titles="Information Framework">SID</span>**:是TM Forum的Frameworx的一个组成部分，旨在为企业提供信息模型和通用词汇表（如客户，位置和网络元素以及实体之间的关系)。

![summary-of-nfv-information-data-models](/assets/img/summary-of-nfv-information-data-models.JPG)

#### NFV的应用场景

* IoT：目前已有一些研究。挑战在于保证网络效率的同时，管理产生的大量数据。
* <span class="tooltip" titles="Information-Centric Networking 以信息为中心的网络">ICN</span>：ICN地址用数据命名，而不是主机，使得内容分发直接实现到网络结构中，而不是依赖于当前用于将内容映射到单个位置的复杂映射。可以在NFV中使用ICN来确定放置网络功能的最佳位置。

#### 本章总结

![summary-of-nfv-research-challenge.JPG](/assets/img/summary-of-nfv-research-challenge.JPG)




