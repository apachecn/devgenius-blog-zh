# 想要更好的数据？投资于您的数据工程师。

> 原文：<https://blog.devgenius.io/want-better-data-invest-in-your-data-engineers-34479091990c?source=collection_archive---------5----------------------->

深入了解数据工程师如何让您的团队更好地处理数据

![](img/2d88623728b51725c2dc18e9b87fe38a.png)

迈克尔·泽兹奇在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

大公司的大多数团队倾向于拥有完整的数据科学家团队，运行模型和实验。这些模型和实验必须在干净的数据上运行，尽管他们仍然进行大多数转换，以达到他们可以使用数据进行机器学习的程度。

我们如何获得这些干净的数据？这通常是数据或软件工程师发挥作用的地方，但主要是数据工程师。这并不是我们隐藏的秘密，但是团队的每个部分都有一个目的，而我们的倾向于隐藏。数据工程为大多数业务的运行提供了基础。想一想。

我做过一些迁移，将管道从内部迁移到云，或者从一个云迁移到另一个云。这些迁移是最好的学习方式——您陷入了通常是一团糟的情况，然后必须用简单明了的数据模型将其转化为一件漂亮的新艺术品或数据管道。

从这些项目中，我发现了三个相似之处，数据工程师在其中发挥着至关重要的作用，这也是我今天要讨论的内容。

*   创建一两个数据模型
*   实现数据管道
*   设置和管理数据库

**创建一两个数据模型**

这就是数据工程师的闪光之处。数据工程师通常会与数据科学家或分析师交谈，以确定他们的具体用例是什么，然后实现一个数据模型，该模型将允许最佳查询来适应这些用例。

数据模型看起来像什么？最常使用的数据模型是星型模式、雪花模式或银河模式或它们的组合。这里有一篇很好的[文章](https://www.guru99.com/star-snowflake-data-warehousing.html)介绍了这两者之间的区别。

**建立和管理数据库**

一旦我弄清楚了数据模型是什么样的以及它的用例，我就对应该使用什么样的数据库有了更好的想法。有时，您可以对所有用例使用同一个数据库。然而，大多数时候情况并非如此。查看用例通常会排除一些我们可以使用的数据库。

用例 1:需要存储大量事务

像物联网(IoT)设备(如日志文件、网络或硬件设备以及大多数智能设备)一样思考。

几个选项:

1.  存储在对象或文件存储器中，并在其他地方进行计算。想想类似于 [Databrick 的数据湖库](https://databricks.com/discoverlakehouse?utm_medium=paid+search&utm_source=google&utm_campaign=13039235745&utm_adgroup=125064728314&utm_content=microsite&utm_offer=discoverlakehouse&utm_ad=569205865836&utm_term=data%20lakehouse%20architecture&gclid=Cj0KCQiAosmPBhCPARIsAHOen-NimDH4obvGUD6U81EOHpYqbs4T6vaTNvL6FgJ8xV-v8nGujcEDfjMaAqO9EALw_wcB)的东西。
2.  将最近的 x 天、周等存储在事务数据库中，并将历史数据保留在对象或文件存储中

用例 2:报告

这实际上取决于您有多少数据，以及数据的事务性如何。

用例 3:最新的价值和超快的速度

想象一下内存缓存。

在查看了用例之后，我们还必须查看我们需要从哪些源中提取数据。这通常也会消除数据库，使其中一个数据库成为显而易见的选择。

**实现数据管道**

耶！我们已经弄清楚了我们的用例是什么，我们的数据模型是什么，现在我们需要弄清楚如何将所有来源的数据放入我们的数据库。我们现在“只是”要把碎片连接起来哈哈。这大概占了我们工作的 80%,因为大部分数据质量问题都是通过实施彻底的流程和清理数据来避免的。你想在这里度过你的大部分时间。

在实际实现数据管道之前，我们还有另外两项任务。第一步是创建数据策略文档(稍后将详细介绍！)另一个是为我们将要实现的内容创建一个架构设计。这将允许我们在团队或公司中分享我们的目标时进行迭代的改变和调整。

这一切的底线是什么？数据工程师做了大量的工作，使数据科学家能够轻松地获得数据并进行分析或建模。有时数据工程师做分析并支持数据科学家。最终，数据工程师需要成为数据组织的一部分，因为他们提供了获取干净数据以供数据科学家使用所需的流程。