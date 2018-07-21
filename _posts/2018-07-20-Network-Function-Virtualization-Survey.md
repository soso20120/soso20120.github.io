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

图2中基于NFV实现的案例，CPE的功能由ISP处的一个共享的基础设施实现。基于上述场景，在ISP中就能简单更新DHCP，或者为一部分人或所有人增加父母监控的功能。不仅节约操作费用，而且大规模应用下，CPE也能更便宜

![NFV applied in CPE]({{ site.baseurl }}/assets/img/nfv-applied-in-cpe.JPG)

##### 2.应用于<span class="tooltip" titles="Evolved Packet Core Network 分组核心网">EPC</span>
EPC是<span class="tooltip" titles="Long Term Evolution">LTE</span>的核心网络。图3展示了LTE的基本架构。

#### 未解决的问题





