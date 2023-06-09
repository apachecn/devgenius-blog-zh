# Kubernetes 成本优化的 8 个技巧

> 原文：<https://blog.devgenius.io/8-tips-for-kubernetes-cost-optimization-c64a454ee445?source=collection_archive---------4----------------------->

![](img/e787b2592b7dcf80051804783eb27cad.png)

[亚历山大·米尔斯拍摄的照片](https://unsplash.com/photos/lCPhGxs7pww)

Kubernetes 正在统治集装箱市场。根据 [CNCF 的一项调查](https://www.cncf.io/wp-content/uploads/2020/11/CNCF_Survey_Report_2020.pdf)，2020 年 Kubernetes 在生产中的使用率为 93%，高于 2019 年的 78%。此外，调查显示，2020 年生产中集装箱的使用率为 92%，比 CNCF 2016 年的首次调查高出 300%。

由于 DevOps 团队对 Kubernetes 的广泛采用以及开源社区的鼓励，这个数字在未来还会增长。如果它保持目前的价格，这个市场份额仍然是一个重要的部分。这意味着尽管 Kubernetes 让很多事情变得更容易，但正如调查所证实的那样,[挑战总是会出现。也就是说，列出的问题包括联网、存储、跟踪、监视、缺乏准备，当然还有成本管理。](https://microtica.com/blog/7-challenges-with-aws-costs/)

运营 Kubernetes 可能非常昂贵，尤其是在效率低下的情况下。当企业第一次尝试将 Kubernetes 整合到他们的组织中时，通常使用在最初的研究实验或小型应用程序中表现良好的相同架构和设置。然而，这种设置通常是不优化的，公司不会马上考虑费用。这可以节省很多不必要的成本，并鼓励从一开始就养成好习惯。

在本文中，我们将介绍几种控制和降低 Kubernetes 成本的方法，这些方法可用于各种 Kubernetes 用例。此外，由于[亚马逊 EKS 是自管理 Kubernetes](https://www.stackrox.com/kubernetes-adoption-security-and-market-share-for-containers/) 之后最常见的容器管理方法，我们将在 AWS 上提供更多关于 Kubernetes 成本优化的可行建议。

# Kubernetes 成本监控

这是开始更有效地管理 Kubernetes 成本的最合理的一步。这应该能让你知道你是如何花钱买 Kubernetes 的。

公共云服务对存储成本进行基本跟踪。除了实际费用，您还可以在他们的计费摘要中看到实际运行的内容以及影响成本的因素，例如存储或网络流量占成本的百分比。

另一方面，云供应商的总结将只包括对多租户 Kubernetes 集群仅有些许用处的简单概述，当然，在私有云中是无法访问的。因此，使用外部软件来监控 Kubernetes 的消费是很流行的。

在你决定了[你将使用的工具](https://microtica.com/blog/devops-toolchain/)以及你将如何监控你的 Kubernetes 成本之后，你可以开始为 Kubernetes 成本优化实施更具体的行动。

*查看我关于创建* [*AWS 成本优化策略*](https://microtica.com/aws-cost-optimization/?utm_source=devgenius&utm_medium=medium&utm_campaign=cost_optimization_pillar) *的指南。*

# 资源有限

有效的资源约束保证了 Kubernetes 系统的任何程序或操作者都不会使用过多的处理能力。因此，他们保护你免受不受欢迎的冲击，如意想不到的帐单变化。

限制资源是至关重要的，尤其是如果您的许多开发人员可以直接访问 Kubernetes。它们确保了可用资源的公平共享，从而减小了整个集群的规模。没有限制，一个人可以使用所有的能量，阻止其他人工作，导致需要更多的计算资源。

然而，注意不要在没有任何平衡的情况下限制你的资源。如果资源限制太低，工程师和软件就不能正常工作，如果资源限制太高，它们通常就没有价值。一些 Kubernetes 成本优化工具可以帮助您决定您想要的资源平衡。

# 自动缩放

自动扩展意味着按需付费。这就是为什么您必须根据您的特定需求来调整集群的大小。您可以让 Kubernetes 自动缩放能够适应快速变化。

水平和垂直自动缩放是两种可用的自动缩放类型。简而言之，水平自动缩放包括根据负载是高于还是低于指定水平来插入和移除 pod。单个单元的缩放与垂直自动缩放相平衡。

这两种自动缩放方法对于根据您的实际需求动态调整可用的计算能力都很有用。然而，这种方法不一定是理想的，因为它并不适用于所有用例，例如当某些东西需要计算资源，因此不能自动缩减规模时。因此，可以引入某些额外的步骤来进一步降低您的 Kubernetes 成本。

# 选择正确的 AWS 实例

用于管理 Kubernetes 集群的 AWS 实例直接影响 AWS Kubernetes 的成本。实例有许多不同的形式，具有不同的内存和计算资源组合。Kubernetes 豆荚也是这样，资源配置不同。控制 AWS Kubernetes 成本的关键是确保 pods 在 AWS 实例上有效堆叠。AWS 实例应该与 pod 的大小相匹配。

pod 的规模、数量和历史资源利用趋势都在决定使用哪个 AWS 实例时发挥了作用。应用程序可能有不同的存储或 CPU 要求，这会影响要使用的实例类型。

确保 Kubernetes pods 的资源消耗与它们使用的 AWS 实例上可用的整体 CPU 和内存相关，对于优化资源使用和降低 AWS 成本至关重要。

# 使用定点实例

就 AWS 实例而言，它们可以在几种计费配置文件中使用:按需、预留和现场实例。按需实例的成本最高，但灵活性最好。现货实例具有最低的价格，但可以在 2 分钟的警告后终止。为了节省成本，您还可以在一段时间内保留实例。因此，实例形式的选择直接影响到在 AWS 上运行 Kubernetes 的成本。

[Spot 实例](https://aws.amazon.com/ec2/spot/)通常用于那些不是永久需要的工作负载，并且可以处理大量的中断。AWS 声称，spot 实例将帮助您节省高达 90%的 EC2 按需实例价格。

如果 spot 实例不是您的应用程序的选择，因为它必须无延迟地运行，如果您同意在固定的时间内使用这些服务，您可能会得到折扣。根据 AWS，如果你同意一年或三年的使用期限，你将获得 40%至 60%的大幅折扣。

# 制定睡眠时间表

无论您是在按需、预留还是现场实例上运行 Kubernetes 集群，确保未充分利用的集群被终止对于成本管理都是至关重要的。AWS EC2 实例的费用是根据它们被提供的时间段来计算的。即使未被充分利用的实例对资源的影响比必要的要大得多，它们仍然会花费运行一个实例的全部费用。

简而言之，如果一个开发团队使用[云原生](https://microtica.com/blog/a-comprehensive-introduction-to-cloud-native-devops/) Kubernetes 环境，他们只在工作时间使用它。如果他们一周工作 40 个小时，而环境在其余时间仍在工作，他们就不必为剩余的 128 个小时付费。当然，并非每个团队都是如此，特别是如果他们有灵活的工作时间，但在无人工作时关闭环境可以显著提高 Kubernetes 的成本优化。

开发人员可以通过自动设定睡眠时间表来实现这一点，并且只在需要的时候唤醒环境。设置此计划意味着系统将自动缩减未使用的资源。这保证了环境的条件被保存，并且当再次需要时，环境将容易地和自动地“唤醒”,这意味着工程师的工作流程不会被打扰。

# 练习定期清理 Kubernetes

如果您给工程师完全的访问权限来按需构建名称空间，或者使用 Kubernetes 进行 CI/CD，那么您最终会得到大量未使用的对象或集群，而这些对象或集群仍然在耗费您的资金。如果您有一个减少计算资源的睡眠模式，它只是针对暂时不活动的资源，仍然保留存储和配置。这就是为什么，当你注意到你的一些资源已经很长时间不活动时，删除它们将是一个明智的做法。

# 调整 pod 大小

控制 AWS Kubernetes 成本通常需要很好地了解 pod 大小。DevOps 团队可以通过为每个容器分配最小数量的资源来设置 Kubernetes 的 pod 大小。

由于 pod 资源使用随时间变化，预留资源增加了复杂性。此外，由于缺乏资源使用的历史证据，很难做出这些决定。通常，开发人员的反应是保留比所需更多的资源，从而导致过载和资产损失。

持续监控 pod 资源使用情况，并确保为其提供正确数量的资源，将为整个 AWS 基础设施节省大量成本。

# 标签资源

在任何环境中，无论是云、内部部署还是容器，标记资源都是一个明智的想法。在具有大量测试、试运行和开发环境的企业 Kubernetes 环境中，任何服务都必然会被忽视。这些服务是 AWS 价格的长期负担，尽管它们并没有被使用。公司应该使用标签来保证所有的服务都受到控制。

AWS 提供了一个健壮的标记方案，可以用来标记属于 Kubernetes 的服务。您可以使用这些标签来掌握资源、资源持有者和资源使用情况。有效的标记使您能够轻松地分类和消除未使用的服务。在 AWS Billing dashboard 中启用这些标签后，您将能够为各种服务分配成本并查看费用明细。

# 结论

Kubernetes 成本优化的第一步是创建一个大纲并开始监控它们。然后，为了避免不必要的计算资源使用，您可以设置限制，这将使成本更易于管理。

确定对降低成本至关重要的资源的最佳规模，以及自动扩展也会有所帮助。如果您使用 AWS，您可以检查它们的成本较低的选项，如 spot 实例。移除闲置资源的其他步骤包括自动睡眠时间表和清理未使用的 Kubernetes 资源。最后，调整 pod 大小并实施资源标记，以便更好地优化 Kubernetes 的成本。

将这些技巧融入到您的流程中，将会产生一个成本优化的 Kubernetes 系统，为您节省更多关键业务运营和产品改进的成本。