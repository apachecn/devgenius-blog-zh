# 以太坊虚拟机(EVM):技术概述

> 原文：<https://blog.devgenius.io/ethereum-virtual-machine-evm-a-technical-overview-56bf501b3978?source=collection_archive---------9----------------------->

![](img/637666f583e64b920a9bcd07d4b0fc07.png)

*区块链生态系统的主要动力，也是许多网络的首选基础设施。*

## 以太坊虚拟机是什么？

以太坊虚拟机(EVM)是一种负责执行智能合约和计算以太坊网络状态的协议。它位于以太坊的硬件和节点网络层之上，运行并调试计算机可读的智能合约。最初为以太坊开发，许多链成为 EVM 兼容。

## EVM 的属性是什么？

**图灵完备性**

图灵完备性定义了计算机何时能够解决问题和计算数据。这是艾伦·图灵在思考机器的能力时提出的假设，他们不能像人类一样思考或处理信息。

**分布式状态机**

以太坊不仅仅是保存所有记录的账本。根据其白皮书，它最初是为智能合同和应用程序而设计的。虽然它也作为一个分类帐，一个完整的机器状态被保存。契约是用可靠性编程的，模仿人类交流，比大多数编程语言更有表现力。

**智能合约**

智能合同是用代码编写的各方之间的协议。它们是自动执行的。无需信任即可删除第三方和功能。虽然这些交易是不可逆转的，但它们仍然是合法的。为了把概念说清楚，我们来举个例子；假设你想从自动售货机买水。首先，你写下号码，然后你支付价格。如果金额不足，机器会向你索要更多资金，如果资金多于价格，它会把水和找零还给你。你做了交易之后，你不能把交易拿回来，你有水。但有一个问题，交易不会记录在自动售货机上，但智能合同会记录在区块链上，这使得它是可证明的。

**确定性**

EVM 为同一组输入提供相同的输出。考虑到发生大量金融交易的 DeFi 应用程序，了解代码在执行时的反应是很有帮助的。因此，决定论是 EVM 的一个重要因素。

**隔离**

智能合约在隔离的环境中运行，使以太坊能够独立于应用程序抵御技术问题。它可能包含攻击、错误和其他问题，以便链正常工作。

**可终止**

以太坊使用气体来计算运算。这些操作会消耗大量的气体，为了更有效地构建应用程序，必须对其进行限制。为了让智能合约发挥作用，开发人员应该注意这些限制，如果操作的气体量超过限制，机器就会停止操作或暂停处理。

## EVM 是如何工作的？

在我们深入了解 EVM 的工作原理之前，让我们先来看看什么是虚拟机。虚拟机需要 CPU、内存和存储，但它们只运行计算机代码。理论上，它们可以由任何人运行，这为分散式网络提供了灵活性和可移植性。

与其他虚拟机的工作方式类似，EVM 是一个分散的节点网络，用于执行嵌入以太坊节点的智能合约，以执行与 EVM 兼容的智能合约。它需要智能契约、节点、操作码和 gas。

正如我们在属性中提到的智能合约一样，让我们来看看这些功能的其余部分是如何执行的:

**节点**

节点只是区块链网络上的计算机，它们有一个区块链的副本。在以太坊中，所有节点必须同意下一个节点执行相同的指令，使其图灵完整。每条指令都有一个分配给它的成本，并有一个基于智能合同的经济以及与之相关的成本，使它们对一个大的经济负责。

**操作码**

开发人员很容易创建操作码。虽然他们没有直接参与 EVM，以太坊中的所有程序都是用 Solidity 编写的。它们中的每一个被分配一个字节，并且限制为 256 个操作码。

**气**

气体是以太坊虚拟机的燃料。当进行交易时，用户必须支付交易费。同样，开发人员支付天然气费来部署他们的合同，这是智能合同中所有指令的总和。由于合同消耗大量的 gas，它有助于网络抵御和防止 DDoS 攻击，并保持网络安全。

## EVM 兼容哪些区块链？

以太坊，雪崩，Fantom 歌剧链，BNB 链，极光，多边形，卡尔达诺的 Mikomeda 侧链，和声，Arbitrum，和乐观主义。

你觉得 EVM 怎么样？你听说过 EVM 吗？你用过 EVM 网络吗？你听说过哪些 EVM 电视网？在下面的评论区分享你的想法和经历。