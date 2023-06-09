# 缩放应用第 1 部分—简介

> 原文：<https://blog.devgenius.io/scaling-applications-part-1-40d98b793cc0?source=collection_archive---------0----------------------->

![](img/fac8c541f84ad3b80e7659574b9cc0f3.png)

肖恩·波洛克在 [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral) 上的照片

这是关于如何扩展应用程序的 7 篇系列文章中的第一篇。本系列将涵盖常见的扩展模式，以及它们的优缺点和注意事项。*注意——随着系列的发展，这种结构可能会发生变化。

*   第 1 部分—简介
*   [第 2 部分—扩展 Monolith Web 应用程序(负载平衡)](https://medium.com/@hughie.coles/scaling-applications-part-2-scaling-the-monolith-web-application-90c21b7d77fb)
*   [第 3 部分—扩展整体数据库(读/写复制)](https://medium.com/@hughie.coles/scaling-applications-part-3-scaling-the-monolithic-database-3ac1bfbd0e1b)
*   [第 4 部分—分割整体数据库(分片)](https://medium.com/@hughie.coles/scaling-applications-part-4-scaling-the-monolithic-database-c912f0ea2a1f)
*   [第 5 部分—拆分整体式应用程序(服务)](https://medium.com/@hughie.coles/scaling-applications-part-5-splitting-the-monolithic-application-56dc31f5eae3)
*   [第 6 部分—增加消息传递(排队)的弹性](https://medium.com/@hughie.coles/scaling-applications-part-6-adding-resiliency-in-messaging-b095a9bfb914)
*   第 7 部分—超级分割整体应用程序(微服务)

我最近一直在面试。我的很多谈话都围绕着软件架构以及如何面对不断增长的负载进行扩展。这让我越来越多地思考当你从中级开发人员过渡到高级开发人员，或者从高级开发人员过渡到架构师时，在技能上可能形成的差距。我想写一系列文章，讨论何时、为什么以及如何扩展是有价值的。我不打算讨论高级的、固执己见的和特殊用途的架构，如 CQRS/事件源、Lambda 架构或无服务器架构。这些架构不是通用的，更多的是基于业务需求而不是性能。然而，我将介绍 SOA/微服务。本系列中的条目大致基于您通常应用这些技术的顺序。我将讨论这些模式可以解决的性能问题的类型，它们会导致什么问题，以及它们何时不合适。我还将介绍同步和异步通信以及排队。

*应用这些技术没有真正的路线图，因为它们都解决了负载下可能出现的不同问题。您的应用程序的特征(例如，读密集型和写密集型)将决定应用哪种模式以及何时应用。