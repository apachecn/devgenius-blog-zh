# 技术债务在多大程度上是有用的工具？

> 原文：<https://blog.devgenius.io/to-what-degree-is-technical-debt-a-useful-tool-6d7387332f40?source=collection_archive---------6----------------------->

![](img/80b5f0ef3e193ee92589bda7f7b51d46.png)

詹姆斯·哈里逊在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

当沃德·坎宁安创造术语“技术债务”时，唤起金融债务是有意的；当我们走捷径的时候，我们积累了技术债务，这些捷径给了我们一些直接的利益(运输能力，开发时间，市场竞争)，但是却招致了消耗我们资源的利息支付[1]。脸书的早期提供了一个很好的例子:PHP 被用作快速开发的框架，而 Zuckerberg 迅速试验新功能，但最终，这证明对可伸缩性和性能的消耗太大，债务通过切换到 C++来偿还[2]。写马虎的代码没有回报；许多著名的演讲者提出了他们自己的定义，但是他们同意错误的、仓促的或者丑陋的代码不是技术债务，当然也没有用。

软件开发专家 Martin Fowler 认为技术债务有两种性质；意向性和谨慎性[6]。意向性是你选择故意承担债务，而谨慎是衡量你计划如何偿还任何债务的标准。我们认为债务只有在同时具备这两种属性时才是有用的。

当科技债务被有意承担时，我们可以创建工具来监控其影响，并使用指标来确定处理它的最佳方式。史蒂夫·弗里曼在他的演讲“虚张声势者的技术债务指南”中提出了一个飓风地图的类比，以展示当债务得到良好跟踪时，团队如何能够在最明智的时候还清债务[3]。当无意识地承担债务时，很难确定债务在哪里以及它如何影响项目。努力可以是无组织的，没有项目改进的定性评估。团队最终可能会承担大卫·范德格里夫特称之为“也许”技术债务问题的任务。这些通常是个人喜好的问题，从任何客观的标准来看,“固定的”版本并不一定更好。

同样重要的是，团队要谨慎处理技术债务；意识到债务及其影响只有在团队能够还清债务的情况下才有价值。Twitter 和 Friendster 在迅速积累了大量用户基础后，都在可扩展性方面苦苦挣扎。这笔债务是为了在本世纪初的社交网络市场上竞争而有意承担的。当网站超过容量时，Twitter 的“失败鲸”最终被服务可靠性投资所扼杀。这涉及到从一个单一的 Ruby on Rails 系统迁移到多个独立的 JVM 系统，这些系统可以根据增加的用户流量进行伸缩[9]。然而，Friendster 的优先级不同。董事会如此专注于添加新功能，如 VoIP，以击败他们的竞争对手，其 40 秒的页面加载时间最终促使用户转向 MySpace 等更新的平台[10]。认真对待偿还科技债务的 Twitter 现在拥有超过 3 亿的活跃用户，而不谨慎行事的 Friendster 现在已经过时了。[11]

有时候，承担技术债务的策略可以避免浪费时间。即使在一个拥有无限资源的项目中，一些修正也不值得进行。Freeman 展示了开源框架的例子。虽然它们经常充满技术债务，但是它们也工作得很好，不再需要频繁的改变，并且更适合“浇注混凝土”[3]。大多数项目都有一个有限的生命周期，有些债务值得一直背负到最后。如果使用得当，技术债务可以成为一个强大的工具，帮助开发团队灵活地移动和处理眼前的挑战。然而，团队必须有意识地承担债务，以便他们能够理解它如何影响他们的项目，并谨慎地防止短期目标的不断优先化损害项目的未来。

与朱莉·艾米尔和杰克·墨里森合著

## 参考

[1]什么是技术债？【在线】。可从以下网址获得:https://www . product plan . com/glossary/Technical-debt/#:~:text = Technical。[访问日期:2021 年 2 月 19 日]。

[2]技术债务的隐性成本和收益。【在线】。可从 https://www . polymathlabs . co/blog/technical-debt 获取。[访问日期:2021 年 2 月 19 日]。

[3]史蒂夫·弗里曼(Steve freeman):一个骗子为他人技术债务的指南— sclconf 2018。【在线】。available from:https://www . YouTube . com/watch？v=jXpJVsv3Iec。[访问日期:2021 年 2 月 19 日]。

[4]技术性债务不是技术性的——埃纳尔·w·霍斯特[在线]。可从:https://www.youtube.com/watch？v=CXyNZYDO07Q。[访问日期:2021 年 2 月 19 日]。

Theciocfoconversation:技术性债务——一种模式？【在线】。可从以下网址获得:https://AWS . Amazon . com/blogs/enterprise-strategy/the-CIO-CFO-conversation-technical-debt-an-apt-term/。[2021 年 2 月 19 日查阅]。

[6]技术债务象限。【在线】。可从以下网址获取:https://Martin fowler . com/bliki/technical debt quadrant . html。

[7]技术债务是不真实的。【在线】。可用 from:https://medium . com/swlh/technical-debt-not-real-8803 ce 021 CAA。[访问日期:2021 年 2 月 22 日]。

[8]推特如何杀死失败的鲸鱼。【在线】。可查阅:https://business . time . com/2013/11/06/how-Twitter-slayed-the-fail-whale/。[访问日期:2021 年 2 月 22 日]。

[9]每秒新推文记录，以及如何！【在线】。可查阅:https://blog . Twitter . com/engineering/en _ us/a/2013/new-tweets-per-second-record-and-how . html，[2021 年 2 月 22 日查阅]。

[10] Friendster 由于未能扩大规模而失去了领先地位。【在线】。可从 http://high scalability . com/friendster-lost-lead-cause-failure-scale 获取。[访问日期:2021 年 2 月 22 日]。

[11]Twitter:2010 年至 2019 年每月活跃用户数。【在线】。可查阅:https://www . statista . com/statistics/282087/number-of-monthly-active-Twitter-users/，[2021 年 2 月 22 日查阅]。