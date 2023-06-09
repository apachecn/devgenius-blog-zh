# 上限定理权衡

> 原文：<https://blog.devgenius.io/the-cap-theorem-trade-off-133962f8a716?source=collection_archive---------3----------------------->

🚀 [**打造分层微服务**](https://learnbackend.dev/books/build-layered-microservices) 这本书出来了！现在就在 [learnbackend.dev](https://learnbackend.dev/books/build-layered-microservices) 购买你自己的副本。

![](img/87753b7ff61b84e254c11e78a77b22d8.png)

在分布式系统中，就像基于[微服务架构的系统一样，](/a-simple-introduction-to-microservices-ecd031973117)对于数据存储，有三种保证可以相互权衡:*一致性*、*可用性*和*分区容差*。

CAP 定理(也称为 Brewer 定理)指出，当系统处于故障模式时，只能维持这三种保证中的两种，因为事实上，没有一个分布式系统可以免受网络故障的影响，并且必须容忍网络分区，至于当它发生时，必须决定是否确保一致性或可用性之一。

# 担保定义

*一致性*——不同于 ACID 事务的一致性，它是关于维护数据约束的——意味着每个读操作都接收最近一次写操作的值或一个错误。

*可用性*意味着每一个读操作都接收到一个不是错误的有效响应，但不能保证它包含最近一次写操作的值。

*分区容忍度*是指尽管网络在节点间丢弃或延迟了任意数量的消息，系统仍能继续运行。

# 一致性与可用性

## 牺牲一致性

牺牲一致性意味着我们决定让我们的服务处理传入的请求，尽管有*网络* *分区*的限制，我们仍然保持服务的可用性，同时冒着提供可能过时的数据的风险。

这又意味着分区在接受写入时持续的时间越长，这种重新同步将变得越困难。

这种系统被称为 *AP 系统*。

## 牺牲可用性

另一方面，牺牲可用性意味着为了保持一致性，每个数据库节点必须能够知道它拥有的数据副本与其他节点中的副本是相同的。

在节点无法协调的分区环境中，唯一的选择是通过发送错误消息来拒绝响应请求。

该系统被称为 *CP 系统*。

# 哪个最好？

既然我已经向您介绍了两种可能的系统权衡，那么显而易见的问题仍然存在:这些解决方案中哪一个是最好的？

简单的答案是:这取决于它将产生的业务影响。

想象一下，你正在开发一个像优步一样的 PHV 应用程序，客户可以实时跟踪他们的司机的位置和到达他们上车地点的预计时间。

如果司机的实时位置相差几百米，或者到达上车地点的预计时间实际上相差几分钟，这会导致客户取消乘车吗？

如果答案是否定的，那么用一致性换取可用性可能是正确的答案，因为客户宁愿要一个大概的信息，也不愿什么信息都没有。

现在想象一下，一个司机接受了邀请，正开车去接车的地方。

如果收件地址实际上是上一次乘坐的最后一个已知地址，而不是客户正在等待的实际地址，会有问题吗？

如果答案是肯定的，那么用可用性换取一致性可能是正确的答案，因为将司机送到错误的地址会导致客户取消乘坐，司机也不会信任你的平台。

# 下一步是什么？

不要忘记👏🏻如果你喜欢读我的作品！

👉你喜欢这种内容？在 [https://learnbackend.dev](https://learnbackend.dev/) 查看《如何使用 Express framework 构建生产就绪的分层认证微服务》一书 [**构建分层微服务**](https://learnbackend.dev/books/build-layered-microservices) ，该书从第一行代码到最后一行文档都符合开发实践和软件架构方面的行业标准。