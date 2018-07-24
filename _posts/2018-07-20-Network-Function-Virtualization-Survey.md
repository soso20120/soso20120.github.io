---
layout: post
title: Network Function Virtualization：State-of-the-art and Research Challenges
excerpt: 
tags:
- NFV

---

### 1. Introduction

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

 ![NFV applied in CPE]({{ site.baseurl }}/assets/img/nfv-applied-in-cpe.JPG)

##### 2.应用于<span class="tooltip" titles="Evolved Packet Core Network 分组核心网">EPC</span>
EPC是<span class="tooltip" titles="Long Term Evolution">LTE</span>的核心网络。图3左展示了LTE的基本架构。<span class="tooltip" titles="User Equipment">UE</span>通过E-UTRAN连接到EPC。EPC执行基本功能，包括用户跟踪，移动性管理和会话管理。由四个部分组成：<span class="tooltip" titles="Serving Gateway">S-GW</span>，<span class="tooltip" titles="Packet Data Network Gateway">P-GW</span>，<span class="tooltip" titles="Mobility Management Entity">MME</span>，<span class="tooltip" titles="Policy and Charging Rules Function">PCRF</span>。并且EPC还连接到外部网络，外部网络可以包括<span class="tooltip" titles="IP Multimedia Core Netword Subsystem IP多媒体核心网子系统">IMS</span>。目前EPC的所有功能都是基于专有设备。所以微小的改动都需要更换设备。

图3右则展示了EPC虚拟化的架构。这种方式更灵活、动态调整，做出更改更容易也更便宜。而且还可以更简单的软件升级，更快地革新。

 ![NFV applied in EPC](/assets/img/nfv-applied-in-epc.JPG)

#### 未解决的问题
* 实施是否转化为最初预期的好处。
* 有一些重要且未开发的研究挑战需要解决，例如测试和验证，资源管理，互操作性，实例化，VNF的性能等。
* 即使是正在探索的领域，如MANO，仍然存在悬而未决的问题，特别是在支持异质性方面。

**目前文献的局限性：**
* 在范围方面，他们没有考虑NFV的重要方面，例如它与SDN和云计算的关系。
* 对标准化活动进行有限的审查和分析。
* 对正在进行的研究和挑战的不完整的描述。

### 2. NFV架构及局限性
由ETSI提出

 ![NFV architecture proposed by ETSI]({{ site.baseurl }}/assets/img/NFV-architeture-proposed-by-ETSI.JPG)

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

### 3. 商业模式及设计注意事项

#### <span class="tooltip" titles="Infrastructure Provider 基建供应商">InP</span>





### 4. NFV与SDN和云计算的关机

### 5. NFV的主要项目和早期实现、用例、商业产品

### 6. Future Exploration

### 7. 总结







