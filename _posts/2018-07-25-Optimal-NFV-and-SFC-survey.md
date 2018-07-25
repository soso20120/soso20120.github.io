---
layout: post
title: Optimal Network Function Virtualization and Service Function Chaining: A Survey
excerpt: 
tags:
- NFV
- SFC

---

## <span class="tooltip" titles="Network Function Virtualization 网络功能虚拟化" >NFV</span>

#### NFVI

* 硬件资源：服务器和存储/网络设施
* 虚拟资源：虚拟机（VM），虚拟节点和虚拟链路

#### VNF

* VNF是在虚拟机上运行的网络功能的软件实例
* 单个VNF可以由部署在多个虚拟机上的多个子功能组成

#### MANO

MANO提供VNF的配置，并配置它们和相关的基础设施。包括三个部分：
* <span class="tooltip" titles="NFV orchestrator 协调器">NFVO</span>：负责创建端到端的服务，管理网络服务的生命周期。
	1. 在服务目录中注册网络服务及其所需参数和相关规则;
	2. 创建，查询，更新和删除转发规则和网络服务序列;
	3. 创建，扩展，更新和终止网络服务。
* <span class="tooltip" titles="Virtual network functions manager 虚拟网络功能管理器">VNFM</span>：负责管理VNF生命周期，包括创建，扩展，更新，升级和终止VNF。VNFM和EMS都被分配来管理VNF，因此它们之间的职责划分在不同的情况下可能会有所不同。

