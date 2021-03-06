---
layout: post
title: A Novel Blockchain-Based Product Ownership Management System (POMS) for Anti-Counterfeits in the Post Supply Chain
tags:
- Blockchain
- Supply Chain

---

## Abstract

十多年来，射频识别（RFID）技术在供应链中提供防伪措施方面非常有效。然而，后供应链中无法保证RFID标签的真实性，因为这些标签可以很容易地克隆在公共空间中。在本文中，我们提出了一种新的产品所有权管理系统（POMS），用于防伪产品，可用于后期供应链。为此，我们利用比特币区块链的概念，任何人都可以查看拥有余额的证据。通过提议的POMS，即使使用正版的RFID标签信息，如果卖方不拥有所有权，客户也可以拒绝购买假冒产品。 我们实施了一个概念验证实验系统，该系统采用基于区块链的分散式应用平台Ethereum，并评估其成本绩效。结果表明，通常，管理最多六次转让的产品所有权的成本低于1美元。

## INTRODUCTION

假冒产品，如品牌商品，是在国内/国际市场上应对的最重要和最困难的问题之一。由于经合组织（经济合作与发展组织）于2007年宣布国际贸易中的假冒产品可能达到约2500亿美元[1]，这已经被认可十多年了。由于电子商务和电子商务的快速发展，显然迫切需要开发防伪系统。另一方面，十多年来，RFID（射频识别）作为物联网（物联网）世界的关键技术，因其可插入供应链，例如[2] - [5]，用于检测的伪造品而受到很多关注。在支持RFID的供应链中，每个产品都分配了一个EPC（电子产品代码），并写入RFID标签。这种附有标签的产品从制造商运送到供应链方。在运输过程中，每个相关方都询问RFID标签并将额外的证据数据添加到标签中。通过这种方式，下一方可以检查产品是否已通过合法供应链。如果发现任何不一致，此类产品可能被视为假冒产品。

然而，一旦产品到达供应链的末端并在零售商店中展示，它们的真实性就不再有保证，因为任何拥有RFID阅读器的人都可以查询和克隆标签的信息。因此，开发防伪系统非常重要，即使在后供应链中克隆了标签的信息也是如此。

在本文中，我们提出了一种新颖的产品所有权管理系统（POMS），它使反伪者克隆真正的标签变得多余，因为它们无法证明在该系统上拥有产品。为此，我们利用比特币的概念，比特币是一种分散的加密货币系统，其中可以在称为区块链的公共分类账中证明拥有用户的平衡[6]。特别是，通过借用比特币中使用的“拥有平衡证明”中首先提出的想法，我们在这里介绍了“产品发布证明”的概念。此外，必须首先确定几个问题，然后解决这些问题，以便利用区块链技术成功实现POMS。例如，只有合法制造商才能声称拥有自己产品的第一个所有权。为了符合这些要求，在本文中，我们提出了一种基于区块链的防伪POMS，它对后供应链非常有效。首先，确定整体实际系统要求。然后，我们推出了一个完整的协议，使各方（包括供应链合作伙伴和客户）能够转移和证明RFID标签附加产品的所有权。建议的POMS的一个重要优点是，在卖方不拥有所有权的情况下，即使使用真正的EPC，客户也可以拒绝购买反补贴。基于提出的协议，在以太坊平台上实现了概念验证实验系统。绩效评估结果表明，当所有者转移的数量不超过6时，使用建议的POMS管理产品的成本低于1美元。

本文的其余部分结构如下。 第二部分介绍了系统模型，回顾了以前发表的文献，并讨论了在我们的研究背景下如何使用区块链和比特币技术的基本问题。 第三节详细描述了拟议POMS的实际操作。 性能评估可以在第IV节中找到，而关于我们的POMS的开放性问题将在第V节中讨论。最后，结论在第VI节中介绍。

## PRELIMINARIES

在本节中，首先介绍系统模型。 然后，将介绍以前发表的论文的概述和我们工作背后的动机。 第三，解释了区块链和比特币技术的基本原理，以及如何在区块链操作中考虑这些技术。

#### A. SYSTEM MODEL

图1显示了由两条链组成的典型产品流，即支持RFID和后供应链。第一条通常由三方组成，即制造商，分销商和零售商[7]。 制造商在分销收到的产品并将其进一步运送给零售商时，为分销商创建，组合和运送产品。 在后期供应链中，零售商将其产品库存并出售给客户，而这些客户又可以转售它们，例如， 在二手店或互联网上。

我们认为每个供应链方都有EPCglobal Class 1 Gen 2（C1G2）兼容的RFID阅读器制造商为每个产品分配EPC，EPC写入附在产品上的标签，以便任何一方可以在到达时识别产品。 还假设每一方都通过计算机和/或智能手机/平板电脑进行互联网连接。

#### B. PREVIOUS WORK AND MOTIVATION

十多年来，RFID技术已经整合到防伪的供应链中。 FDA（食品和药品管理局）[9]提出了第一个基于RFID的食品和药品行业防伪方法。在他们的提案中，每个供应链方都配备了RFID阅读器，并跟踪每种产品的运输和接收事件。通过这种方式，供应链各方能够跟踪和跟踪产品的产品流。但是，正如[2]中指出的那样，这种方法容易受到克隆标记的攻击。具体而言，一旦攻击者复制附在真品上的RFID标签，就可以在供应链中插入带有克隆RFID标签的伪造品。以这种方式，通过上述跟踪和追踪方法不能识别具有克隆标签的伪造品。到目前为止，处理这个问题的研究工作可以分为两类。第一个涉及安全标签分发方案的开发，以便攻击者不能复制供应链中的标签内容，例如，见[7]，[10] - [14]。在这些工作中，最重要的可能是基于秘密共享的密钥分配方案[7]。在该方案中，标签的信息使用对称加密方案加密，加密密钥通过秘密共享方案分成多个共享[7]。秘密共享方案意识到，如果他/她可以获得超过一定数量的唯一份额，则可以提取密钥[15]。加密的EPC和密钥的份额被写入产品的标签中。收到产品后，授权合作伙伴会询问标签并从足够数量的份额中恢复密钥。然后，用提取的密钥解密EPC。第二类涉及支持RFID的供应链中的克隆标签检测方案，例如，见[2] - [5]，[16] - [18]。例如，在[4]中，当标签到达供应链方时，它将到达证据写入标签存储器中的下一个可用位置。然后，该方请求能够获得供应链信息的检测器检查标签中的信息是否有效。通过这样做，检测器可以识别伪造品，如果发现任何不一致，即，写入的位置是错误的和/或书写的单词不匹配。

然而，一旦产品在零售商店中出售，即在后供应链方案中，则执行任何这样的跟踪和跟踪方法以及安全的EPC分配方案是不可行的。在这种情况下，当前使用的跟踪和跟踪方法都不能保证标签附加产品的真实性，因为它们利用标签的秘密信息。此外，很明显，一旦公开展示，任何安全的EPC分发都没有多大意义。因此，EPC不再保证是独特和真实的。因此，即使在后供应链中也必须考虑伪造品检测。为此，在[19]中提出了一种客户可以检查产品合法性的防伪方案。但是，这种方法需要为每个产品提供特殊的计算标签，因此不能使用公开提供的现成标签。此外，如果客户将此类产品出售给二手店或拍卖，则还要求客户在PKI（公钥基础设施）上注册其证书，这是不现实的。

受上述启发，我们的基本想法是在这里介绍证明“拥有产品”的概念，并设计一种新颖的POMS，管理和跟踪从制造商到现有所有者的产品拥有情况。利用这种方案，如果一方不能证明拥有所要求保护的产品，则可以检测到伪造品。例如，假设客户想通过二手店购买品牌产品。真正的EPC附属于这种销售产品，但实际上，它实际上是假冒产品。在这种情况下，顾客不可能检查卖方是否拥有所要求保护的EPC的所有权。为了检查这一点，我们需要验证是否（i）产品的初始所有者与要求保护的EPC必须是其制造商，以及（ii）具有要求保护的EPC的产品的当前所有者必须是卖方。验证这两个条件的明显而直接的方法是制造商构建一个管理其产品所有权的大规模系统。然而，这是一个非常复杂和昂贵的过程，因为它也必须防止攻击，例如， DDoS（分布式拒绝服务）攻击[20]。此外，这种系统通常需要许多方的参与和相当复杂的程序，包括消费者登记他们的身份，即处理敏感数据，例如， ID /密码对。因此，需要更有效地操作POMS来处理这些问题，同时与支持RFID的供应链兼容。

#### C. BLOCKCHAIN TECHNOLOGY

为了实现这样一个POMS，我们利用了比特币的概念，这是一个分散的加密货币系统，其中可以在称为区块链的公共分类账中证明拥有用户的平衡[6]。具体而言，我们将“拥有平衡证明”的概念替换为我们称之为“产品拥有证明”的同等概念。一些创业公司刚刚开始（或很快计划启动）区块链服务，以管理产品的真实性[21]，[22]。例如，Everledger似乎是钻石特有的最成功的服务[21]。 Everledger提供钻石认证和相关交易历史的永久分类帐。该特殊分类账用于保险公司，业主，索赔人和执法部门的验证。另一个例子是Blockverify，它似乎使用区块链技术来制药和奢侈品[22]。但是，没有任何关于这些商业服务的公开信息，这意味着它的安全和隐私问题无法在我们的论文中进行审查。然而，为基于区块链的POMS提出严格而透明的协议显然非常重要。为了做到这一点，接下来将介绍区块链技术的概述，然后我们将在下一节详细介绍我们的POMS。

（1）BITCOIN AND BLOCKCHAIN

我们首先关注比特币，这是一种分散的加密货币，任何可信赖的权威机构是不存在的，例如银行，因为比特币是第一个使用区块链技术的成功系统。利用区块链，比特币允许用户在没有任何身份验证和集中授权的情况下证明其余额的所有权。首先简要说明用户如何将比特币转移给另一个用户是有用的。在比特币中，称为交易的数据结构用于识别要转移的金额，发件人和收件人。图2示出了这种比特币交易的示例，其呈现了用户A将他/她的比特币转移到用户B然后用户B将他/她的比特币转移到用户C的详细过程，如图2中的第一交易所示。对于用户A将他/她的比特币转移到用户B，从A的公钥计算的用户A的地址，比特币的来源（未使用的余额用户A拥有），以及由用户A的私钥计算的其签名在输入部分中指定。交易在其输出部分，用户A指定要转移的金额和用户B的地址，该地址是从用户B的公钥计算的。用户A还指定他/她自己的地址或可能由用户A拥有的他/她新创建的地址以接收改变。如图2中的第二交易所示，当用户B将比特币转移到用户C时，用户B遵循用户A所做的相同过程。众所周知，在比特币中，任何用户都可以检查每笔交易。因此，如果将相同的地址用于多个事务，则这可能是隐私问题的问题。为了减少此隐私问题的影响，建议用户为每个事务生成一个新地址。由于管理多个地址是一项复杂的任务，因此使用名为wallet的应用程序为每个事务有效地存储和生成公钥/私钥对。

由于比特币是分散的，因此需要一致的算法，以便每个用户都同意交易的顺序。如果没有达成共识，任何恶意用户都可能会尝试两次使用已用完的余额，即所谓的双倍花费。比特币通过引入区块链概念实现（概率）共识，区块链概念是一个不断增长的包含已批准交易的区块链。图3示出了用于构建区块链的一系列区块。通过强加潜在的块创建者（称为矿工）来创建块，以解决难以解决但易于检查的计算难题。更具体地说，矿工需要找到满足其（SHA-256）散列值的随机数（一次使用的数字）以及对前一个块的引用，并且一组未经证实的事务降低目标值。由于需要先前的块来生成下一个块，因此会创建一个不断增长的块链，即区块链。为了让矿工遵循这样的协议，采用以下激励机制：块的第一个解算器获得新铸造的比特币作为奖励，此外，包括在块中的所有交易费用。

虽然这种基于区块链的分散共识机制首先用于“货币”，但它可以扩展到需要公开验证的其他应用程序。显然，POMS就是这样一种应用，因为它可以通过用“产品”代替“货币”的概念来实现基于区块链。这个概念已经体现为CC（彩色币）协议，因为任何比特币用户都可以发行自己的货币。例如，CC可以表示资产或财产，例如，汽车或房子。大多数CC协议，如[23]和[24]，是通过利用比特币的脚本功能构建的，其中发送者可以指定发送比特币的规则。在另一种方法中，建议通过发布和交换“我有一个容器”和“我收到一个容器”构建一个具有CC协议的容器跟踪系统，这些代币最初由制造商和其他方发布[25] 。但是，应该强调的是，CC协议不能用于POMS，因为它缺乏成功实施所必需的操作要求。虽然这些要求将在第III-A节中详细介绍，但值得一提的是，对于POMS，有必要向合作方提供激励，以便各方遵守协议。不幸的是，由于比特币上的CC协议相当简单，因此不可能满足这样的要求。因此，为了实现功能良好的POMS，我们必须选择另一个基于区块链的共识平台，该平台可以支持任何代码的执行。迄今为止，以太坊是唯一能够满足这一条件的平台[26]，因此下面将对其操作进行描述。

（2）ETHEREUM

以太坊是一种基于区块链的分散式加密存储，可以执行任何代码[26]。要启用代码执行，帐户需要内存存储。出于这个原因，以太坊有两种类型的帐户：CA（合同帐户）和EOA（外部帐户）。一方面，EOA管理自己的平衡。另一方面，CA具有其自己的代码以及存储，并且当从另一个CA或EOA接收消息时执行代码。要为CA编写代码，通常使用称为Solidity的脚本语言[27]。用Solidity编写的代码被编译成基于堆栈的编程语言，以便CA可以执行。由于任何算法都可以在具有Solidity的以太坊上进行描述，因此用于防伪的POMS也可以在以太坊上实现。支持编程语言意味着攻击者可以使矿工继续计算无意义的代码，例如导致无限循环，旨在浪费计算资源和能源。为了避免这种攻击，任何改变存储的代码执行都要求发送方根据程序签订足够数量的“气体”，例如：数据量和计算步骤数[28]。如果在执行代码期间“气体”耗尽，状态将恢复为原始状态，但“气体”的成本不会返回给发送者。

## THE PROPOSED POMS

在本节中，将介绍拟议的POMS的概述。 特别是，首先概述关键系统要求，然后是以太坊实施合同的伪代码。 接下来，将确定实现所提议的POMS所需的所有各方之间的算法过程的细节。 正如本节最后一部分所显示的那样，提出的POMS的主要优点是它使标签克隆毫无意义，因为即使标签被伪造者克隆，它们也无法证明产品的所有权。

#### A. POMS OPERATIONAL REQUIREMENTS

在详细描述POMS协议之前，我们提出了关键要求并解释了它们对所提出的产品所有权证明系统的正确运行的必要性。

1. 只有合法制造商才能申请产品的初始所有权（原产地）;
2. 每个制造商只能申报自己的产品;
3. 事件"发货"和"收到"可以分开;
4. 制造商必须对遵循POMS协议的每一方给予一些奖励。

第一个要求是必须避免任何非授权方（包括造假者）非法发布产品所有权。 第二个也是必需的，因为没有它，
可能会出现这样的情况：制造商M1声称制造商M2的产品的初始所有权。 这可以通过利用SGTIN-96的EPC格式指定的公司前缀来避免，SGTIN-96是用于识别产品的96位EPC格式。 表1显示了SGTIN-96的消息格式。 从该表中可以看出，SGTIN-96包含标识其制造商的公司前缀。 实际上，每个制造商可以在支持RFID的供应链中将其自己的公司前缀登记在GS1中。 通过利用这一点，制造商可以仅声明其自己的EPC的初始所有权，其公司前缀由GS1注册。

关于第三个要求，我们划分所有权转移过程的原因是为了避免当前所有者在没有到达目的地时将产品发送给接收者的情况。 在这种情况下，如果仅实现了仅仅转移产品所有权的功能，则可能发生以下不期望的情况：转移所有权，但产品本身未到达收件人。 最后一项要求将使整个系统能够正常运行，因为除制造商外的每一方都必须支付费用才能签发转让产品所有权的合同。 因此，如果没有激励机制，非制造方将会亏损，最终没有动力遵循POMS协议。

#### B. IMPLEMENTED CONTRACTS

为了满足上述要求，我们实施了两个合同，即MM（制造商经理）和PM（ProductsManager）。 一方面，MM提供管理制造商信息的功能，例如， 注册在GS1注册的公司前缀和制造商的地址。 另一方面，PM由每个制造商操作并提供管理产品信息的功能，例如， 注册新产品和所有权转让。

与PM相反，在MM中，我们假设存在管理制造商信息的管理员。为避免冒充，只有管理员才能修改任何制造商的信息。管理候选人之一是GS1，因为它管理公司前缀。尽管这可能打破了完全分散的系统的假设，但为了避免冒充者，这是不可避免的。造假者，从注册自己好像是合法的制造商。实际上，有可能通过利用Namecoin的概念使我们的MM分散[29]。 Namecoin是一个分散的域名系统，通过强制注册成本避免“大规模”注册。但是，如果我们的MM可以通过引入像Namecoin这样的注册费来构建，那么伪造者可能有机会通过支付适当的费用来非法注册为真正的公司。但是，仍然有可能使MM分散。这是关于基于区块链的POMS的一个悬而未决的问题。接下来，将详细介绍MM和PM的伪代码。用Solidity编写的关键缩写代码可以在附录中找到。

（1）Manufacturers Manager(MM)

MM主要由两个功能组成：（i）在区块链中注册制造商的信息，以及（ii）检查请求制造商注册产品的EPC的作者身份。

ALG.1显示了enrollManufacturer（）的伪代码，该代码注册了产品存储在区块链中时所需的制造商信息。 由于我们的POMS只需要一个管理员，例如GS1，可以注册制造商的信息，在步骤2检查此条件。如果是True，则管理员在区块链中注册制造商的信息。

ALG.2示出了伪代码checkAuthorship（），其检查消息发送者是否拥有所声明的EPC的作者。 当消息发送者（可能是制造商M）声称是其产品的初始所有者时，将调用此函数。 在这种情况下，首先通过查询区块链中的地址来检索邮件发件人的公司前缀。 然后，将其与从参数中可用的EPC中提取的公司前缀进行比较。 如果这些前缀匹配，则可以确认消息发送方实际上是已注册的制造商Mand该函数返回True。 否则，它只返回False。

(2）Products Manager(PM)

与MM相比，合同PM由每个制造商创建，包括四个主要功能：
1. enrollProduct（）：当制造商M第一次注册自己的产品，产品由独特EPC指定，并声称其初始所有权时，调用该函数;
2. shipProduct（）：当前所有者与产品分开并指定收件人时调用;
3. receiveProduct（）：由新所有者调用，以便在成功收到产品时成功转让其所有权;
4. getCurrentOwner（）：返回当前所有者的地址。

Alg.3显示了enrollProduct（）的伪代码，该代码注册了产品存储在区块链中时所需的制造商信息。 由于我们的POMS限制只有一个管理员，例如GS1，可以注册制造商的信息，在步骤2检查该条件。如果发现是True，则管理员在区块链中登记制造商的信息。 请注意，我们假设管理员在发送此事务之前已手动检查制造商的信息是否合法。 这个概念类似于在PKI中注册证书[30]。

Alg.4显示了shipProduct（）的伪代码，用于当前所有者将产品转移到下一个所有者。 首先，该函数检查区块链上是否存在给定的EPC，并且消息的发送者实际上拥有EPC的所有权。 然后，如果这是True，则shipProduct（）将“收件人”指定为下一个收件人的地址Arec和EPC的状态为已发货。 请注意，此时，POMS不会更改产品的所有权，因为这可能会在运输过程中丢失。

Alg.5描述了receiveProduct（），它用于接收器确认产品的到货。该功能检查当前所有者是否指定了所声明的EPC，以及EPC的状态是否已发货。如果为True，则所有权成功转移到邮件发件人的地址。此外，产品的制造商向消息发送者提供激励，即一些ETH，作为服从协议的奖励。由于以太坊需要为每笔交易收取执行费用，当当前所有者将产品发送给收件人时，他/她可能不愿意发出交易shipProduct（）。为避免这种情况，引入了以下程序。如果所有权转移已成功完成，则产品制造商会将财务奖励transferReward返还给前一个所有者。制造商应该支付这种奖励的原因在于，通过这种方式，可以检测到伪造品并因此通过它们的合作来识别伪造品。需要注意的是，为了避免双方反复来回转移以获得奖励，我们指定了最大转移次数，称为MAXTRANSFER。为transferReward和MAXTRANSFER选择合适的值将取决于制造商为实施POMS所做的实际投资。但是，这一主题超出了我们目前的研究范围，因此不会进一步考虑。

#### C. ALGORITHMIC PROCEDURES

图4示出了所提出的POMS的详细系统模型，其中识别了两组参与方。 第一个属于供应链，即GS1，制造商，分销商和零售商等管理员。 第二组属于后供应链方，即二手商店和消费者。 每一方都拥有以太坊账户，并通过在个人电脑或智能手机/平板电脑上运行的钱包应用程序进行管理。 接下来，将介绍（i）供应链和（ii）后供应链各方的程序。

（1）THE SUPPLY CHAIN

在供应链中，采取以下五个操作步骤。
1. 制造商M向合同MM发送交易enrollManufacturer（）以注册其在EPC中指定的公司前缀和公司名称。 请注意，此注册步骤需要进行身份验证，以避免伪造者非法声明未授权的公司前缀和名称。
2. 制造商M生*N产品*并为每种产品*i*指定一个由EPC*i*表示的独特EPC，其中1≤*i*≤*N产品*。 同时，为了声明产品的初始所有权，制造商M向合同PM发送交易enrollProduct（）以注册*Nproducts* EPC，即（EPC1，EPC2，......，EPC*N产品*）。 由于现成的智能手机和平板电脑没有配备RFID阅读器，因此将EPC写入QR码[8]或NFC（近场通信）标签[19]。
3. 在运送*Nproducts*产品之后，制造商M向每个产品发出交易shipProduct（）到PM，以通知分销商D制造商M现在准备转移产品的所有权。
4. 在收到产品时，经销商D读取标签的EPC并检查EPC的真实性。 具体而言，对于每个EPC，分销商D调用getManufacturerAddress（）并获得制造商的地址。 然后，分销商D调用getRecipient（），getProductStatus（）和getCurrent Owner（），如果满足以下所有条件，则经销商认可EPC的真实性，并向具有相互作用的EPC的合同PM发出交易receiveProduct（）：
	* 经销商D的地址被指定为收件人;
	* 产品状态为发货;
	* 当前所有者的地址是制造商M的地址。
上述步骤3和4完成了从制造商M到分销商D的所有权转移。
5. 如果经销商D进一步将产品转移到其他方，即零售商，则遵循与上述步骤3中相同的程序。 同样，当任何一方收到产品时，收件人遵循与步骤4相同的程序。

（2）THE POST SUPPLY CHAIN

在后供应链中，消费者将在确认卖方实际拥有产品所有权后决定购买产品。 因此，与“供应链情况”相反，在卖方发出交易shipProduct（）之前需要额外的步骤。 在下文中，我们假设消费者C即将从其当前所有者处购买产品的情况。
1. 消费者C获得所需产品的EPC和当前所有者的地址。 关于EPC，买方可以在他实际进入商店时通过RFID阅读器，QR码或NFC询问产品的EPC。 相反，当买方无法物理访问产品时，例如 通过网上购物，产品的EPC将从网站上获得。 正如稍后将在第III-D.1节中讨论的那样，当前所有者必须提供真实的EPC和他的地址，因为这些信息可以在区块链中进行验证。 消费者C使用EPC调用getManufacturerAddress（）并获取制造商的地址。 然后，他调用getProductStatus（）和getCurrentOwner（）到制造商M的PM。 如果产品状态为拥有，并且获得的地址是当前所有者的地址，则买方将决定通过支付其销售价格来购买产品。
2. 当前所有者发出交易shipProduct（），其中包含要转移的产品的EPC和买方的地址。
3. 当收到产品时，买方向具有询问EPC的合同PM发出交易receiveProduct（）。

#### D. VALIDATION

在本节中，我们首先解释如何通过拟议的POMS的操作程序识别和避免伪造品。 然后，我们提出并讨论有关POMS实际运作的各种实际问题和案例。

(1) PROTOCOL VERIFICATION

让我们考虑以下所有可能的情况：一方可以是产品的新所有者，检查他/她将从其当前所有者收到的产品的真实性。 让我们假设这位当前的所有者是伪造者，并试图向新的所有者出售/转移假冒产品。 为简单起见，在下文中，我们分别表示当前所有者和新所有者作为卖方和买方。

在这种情况下，有三种情况是可能的：
1. 卖方拥有假冒EPC的假冒商品; 
2. 卖方拥有假冒产品并知道其真实的EPC但不拥有其所有权;
3. 卖方拥有正品及其所有权，并拥有一些假冒产品

对于第一种情况，买方可以拒绝购买假冒产品，因为他/她可以在购买前从其EPC检查产品信息。 EPC本身包括产品信息，例如 公司前缀，项目参考和序列号，因此该方可以验证EPC是否真正与要购买的产品相关联。

对于第二个，尽管买方确信EPC与所需产品真正相关，但是卖方是否拥有产品的所有权是令人怀疑的。买方首先通过查询getCurrentOwner（）获取该EPC的所有者地址。卖方将声称该地址是他/她自己的。因此，买方希望通过让卖方发出交易shipProduct（）来确认此索赔，因为只有当前所有者才能发行。但是，卖家可能会在支付款项之前拒绝这样做。在这种情况下，买家可以通过另一种简单的方式来检查。在买方获得当前所有者的地址后，他/她使用伪随机数生成器生成质询消息并使卖方签名。如果使用生成当前所有者地址的公钥验证签名，则可以合理地确定买方是卖方真正是其地址的所有者。但是，在假定伪造者不拥有其EPC所有权的情况下，签名验证肯定会失败。因此买方可以中止这笔交易。

在最后一种情况下，买方确定卖方拥有产品的所有权。 在这种情况下，卖方可能运送其中一个伪造品并发出交易shipProduct（）及其EPC。 但是，我们认为伪造者没有经济上的优点。 由于卖方必须将其EPC的所有权转让给买方，因此不再销售原装正品和任何其他具有相同EPC的假冒产品。 由于假冒伪劣产品比原始产品便宜得多，因此伪造者最终会造成损失，因此伪造者没有任何优点。

(2) MULTIPLE OWNERS CASE

在先前描述的协议验证子部分中，隐含地假设只有一方可以声明一种产品（EPC）的所有权。 但是，多方可能共同拥有一种产品，因此情况比单一所有者情况更复杂。 我们的POMS可以通过在enrollProduct（）中为每个EPC存储多个所有者的地址来处理这种情况。 此外，当转移产品的所有权时，必须事先设定条件，例如， 与所有业主达成协议。 当然，这有时可能很复杂，例如可能需要精确的保持率。

在这种情况下，这些信息也必须存储在区块链中。 因此，根据所有权状态，必须更改所有者的数据结构。

(3) ARBITRATION BETWEEN OWNER AND BUYER

关于交易，如同电子商务的情况一样，可能发生以下不幸情况：买方在他/她不运送产品时向产品所有者支付实际货币，反之亦然。 一般来说，这个问题是通过在买方和卖方之间引入受信任的第三方来解决的，即托管[31]。 但是，我们的POMS不处理托管，因为它在所有权证明方面超出了范围。 实际上，如果通过加密货币支付费用，例如 ETH，通过指定一个聪明的合同规则来实现托管，没有可信任的第三方，这样骗子就会失去他/她的钱[27]，[32]。

(4) OWNER’s PRIVACY

可以认为，由于任何所有者地址存储在PM中，这可能是客户的隐私问题。 但是，客户可以通过为每种产品生成新的公钥/私钥对来解决此问题。 实际上，因为这个过程可以通过以太坊的钱包应用程序自动化，所以客户不必采取任何预防措施。

(5) IMPERSONATION AVOIDANCE 避免重复使用

人们还可以考虑当攻击者伪装成受害者而非法发布交易的情况，例如， 在受害人的地址下发出交易。 例如，让我们考虑以下情况：客户C1拥有产品EPC1的所有权，并且攻击者想要窃取EPC1的所有权。 在这种情况下，攻击者可以通过将其参数指定为EPC1来非法发出shipProduct（）的交易。 但是，在以太坊中，每个交易必须使用发件人的私钥进行签名，该私钥也会生成他/她的地址。 因此，除非客户泄露他/她的私钥，否则没有其他人可以生成他/她的有效签名。 显然，可以通过这种方式避免冒充。

(6) CUSTOMER PARTICIPATION

我们假设参与POMS的每一方遵循上述协议。 尽管某些方面（如普通客户）可能忘记甚至可能不愿意发布shipProduct（）和receiveProduct（）交易，但可以假设所有参与方都遵守该协议，因为POMS的经济利益提供。 如前所述并将在下一节中强调，POMS的主要应用是用于处理不太便宜的产品，例如 品牌商品。 因此，客户非常希望获得此类产品的所有权证明。

## PERFORMANCE EVALUATION AND DISCUSSION

拟议的POMS已经根据其运营成本进行了评估。特别是，总成本通过测量过程中涉及的所有功能的总气体量来估算，即（i）注册（enrollProduct（）），（ii）运输（shipProduct（））， （iii）接收产品（receiveProduct（）），然后将其转换为真实货币。由于在以太坊中每次操作的气体量是固定的，例如， SHA3​​计算需要20个气体[28]，执行功能的总气体量也是固定的。表2显示了此评估中使用的参数。特别是，我们使用以太坊的测试环境工具testrpc [34]来测量气体量，因为该工具能够自动计算气体量。最后，通过参考转换图CoinGecko [33]以美元换算总气体量。在评估时，速率为1gas = 0.00001ETH = 1.443×10-6USD。

图5显示了管理产品的成本（以美元计）
所有权转移的数量。由于对于每个功能，气体成本是固定的，因此随着所有权转移的数量增加，成本增加。然而，所获得的结果清楚地表明总成本仍然很低，例如，对于六次转账，它不到1美元。注意，该成本与产品的实际价格无关。显然，拟议的POMS更适用于相对昂贵的产品，例如，售价超过100美元。显然，在实践中，相对便宜的产品并不值得伪造。

进一步强调的是，与先前的RFID防伪方案相比，POMS具有若干优点。**第一个优点是，即使标签被克隆，任何相关方也可以决定产品是否是真品。因此，即使在后供应链情景中，POMS也可以检测到伪造品。第二个优点是每个参与方不需要更新标签的内容以进行伪造检测。这非常重要，因为对于跟踪产品的其他类似的基于RFID的管理系统通常容易出现读/写错误，并且它们需要更长的时间来在标签中写入数据[4]**。

## OPEN PROBLEMS

有一些开放的问题有待进一步研究。 第一个涉及当产品的接收者成功发出合同receiveProduct（）时应支付多少转移奖励transferReward。 这个问题可以通过对每一方的行为进行建模并通过博弈论找到转移报酬的均衡来解决。 此外，虽然我们只是引入一个常数MAXTRANSFER来避免任何两方反复转移所有权以保持收益的情况，但进一步调查其他方法来实现这一目标将是令人感兴趣的。 例如，（i）通过转移数量逐渐减少激励nTransferred和（ii）考虑到最后一个receiveProduct（）和shipProduct（）之间的时差可能是可能的。

第二个主题与POMS的安全性问题有关，特别是与以太坊操作有关的问题。由于以太坊本身仍处于开发阶段，其安全性尚未得到充分验证。换句话说，如果在以太坊中发现任何严重的安全问题，我们的系统将直接受到影响。因此，与提出的POMS一起进一步验证以太坊的安全性也是一个重要的课题。

第三个主题涉及制造商的隐私。也就是说，由于产品的痕迹是通过向POMS查询其EPC获得的，因此这些产品的销售信息可以由制造商的可能竞争者推断。这意味着POMS需要具备以下两个难以同时满足的特性：（i）透明度，即任何人都可以检查产品的所有权及其可追溯性，以及（ii）匿名性，即可追溯性产品不可行，而产品的所有权可以证明。近年来，已经广泛提出了几种主要关注匿名性的加密货币。 [35]，[36]。对于与POMS相关的未来工作，研究如何将这两种特性共同用于其最佳折衷操作将是非常有趣的。

## Conclusions

我们已经为后期供应链提出了一种新的基于区块链的产品所有权管理系统（POMS），这使得造假者克隆真正标签的努力变得多余，因为它们无法证明在该系统上拥有产品。首先，确定了整体实际系统要求。然后，我们推出了一套完整的协议，使各方（包括供应链合作伙伴和客户）能够转让并证明RFID标签附加产品的所有权。建议的POMS的一个重要优点是，在卖方不拥有其所有权的情况下，即使使用真正的EPC，客户也可以拒绝购买假冒产品。协议验证已显示我们的POMS的有效性。基于所提出的协议，在以太坊平台上实现了概念验证实验系统。绩效评估结果表明，当所有者转移的数量小于或等于6时，使用建议的POMS管理产品的成本低于1美元。