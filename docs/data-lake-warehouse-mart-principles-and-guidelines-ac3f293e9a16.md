# 数据(湖、仓库、集市)原则和指南

> 原文：<https://blog.devgenius.io/data-lake-warehouse-mart-principles-and-guidelines-ac3f293e9a16?source=collection_archive---------7----------------------->

这些可以避免事情失控。

在之前的[文章](/datalake-datawarehouse-and-datamart-7b465200387)中，我们已经了解了什么是数据湖、数据仓库和数据集市。在本文中，我们将探讨构建和维护这些数据存储的指导原则、原则和最佳实践。尽管它们之间有很多不同，但它们确实有一些共同的原则/最佳实践可以遵循。

![](img/0cd0ab4bb9dc1f6d37cc4bb280d6383d.png)

照片由[丹清](https://unsplash.com/@danclear?utm_source=medium&utm_medium=referral)在[的 Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 数据湖:

*   从不同来源接收的所有数据的不可变存储。它还允许您重建某个时间点的业务状态，这对于测试预测模型非常有用
*   应用数据掩蔽以确保 PII 和其他敏感数据在到达存储层之前得到保护。
*   分离存储和计算资源是基于云的数据湖的关键设计目标之一，使您能够优化成本，快速创新，并尝试不同的处理技术和供应商。
*   通过以下步骤确保治理和安全性到位:

1.  指定一个人/团队负责数据湖。
2.  有一个集中的数据目录和元数据。
3.  定义适当的用户和责任矩阵。
4.  通过对存储和计算进行定期审计和监督。

*   根据使用情况应用成本优化技术来存储数据，因为对于很少访问的数据，它们可以归档到低成本存储层。
*   根据法律/成本优化义务应用适当的保留政策。

# 数据仓库:

数据仓库通常由多个层组成，如原始/暂存(这一层包含从源系统接收的原始格式的数据)、企业/源(这一层包含从原始层转换为一致的单一格式数据(如 parquet、avro 等)的数据。)和集成/准备层(这一层包含跨不同源系统集成的最低粒度数据)。

下面是与这些层中的每一层相关的一些原则和指导方针。

*   任何进入原始/暂存层的数据都应该来自授权/黄金来源。
*   应该有一个针对数据及其控制的协议 SLA，以确保不会遗漏数据。
*   对于任何合同违约，如格式、SLA 等，应联系负责的来源支持团队。
*   登陆的数据应符合合规性和分类，如 GDPR、PCI-DSS、适用的监管规则等。
*   在原始/阶段层以及转换后的企业层中接收的数据应该是源系统的真实和完整的表示，没有任何其他转换。
*   不应有来自同一源系统的重复数据。
*   应该将一致同意的格式应用于企业层，如 parquet、avro 等。
*   集成层应该总是从企业层数据准备，以避免任何不一致或数据质量问题。
*   集成层中的数据应该尽可能粒度最小。
*   应该有一个集中的目录，与跨层的业务和技术沿袭一起维护。
*   所有的表或数据文件都应该创建数据仓库强制列，如 loaddate、isactive、createdon 或 updatedon 等。
*   应该有一个跨层应用的适当的分区逻辑，以实现高效的数据获取/处理。
*   应遵循基于个人用户、系统用户、用户组和功能组的访问机制，以避免数据的不受控制的访问/滥用。
*   跨层遵循一致的物理结构，这将避免重复/不一致的数据加载，数据探索可能是高效的，等等。
*   对数据应用适当的 SCD 逻辑，以确保维护历史和当前状态。
*   指定专门的数据治理团队在数据加载前和加载后控制/审核数据。
*   根据法律/成本优化义务应用适当的保留政策。

# **数据集市:**

数据集市通常是使用来自集成/企业层数据、直接来自源系统或来自数据仓库和源系统的组合的数据来创建的。因此，在构建数据集市时，可以应用以下指南或原则:

*   需要确保数据集市不依赖于其他数据集市，因为如果没有进一步的商业价值，存在可以删除/存档的短期数据源。
*   应遵循适当的命名和物理结构。
*   应遵循字符串访问机制，以确保其不被过度利用/滥用，这可能会影响实际的业务用例。
*   必须定义标准访问层，例如批准的 SQL 客户端、仪表板、报告提取流程等。
*   应遵循适当的数据建模设计，如星型或雪花型模式。
*   对数据应用适当的 SCD 逻辑，以确保维护历史和当前状态。
*   根据法律/成本优化义务应用适当的保留政策。

希望我已经涵盖了我能想到的大多数要点，请让我知道我是否遗漏了什么或可以进一步改进。在下一篇文章中，我将介绍大数据工程面临的复杂性/挑战。

**参考文献:**

[https://www . get dbt . com/blog/five-principles-that-keep-your-data-warehouse-organized/](https://www.getdbt.com/blog/five-principles-that-will-keep-your-data-warehouse-organized/)

https://www.width.ai/post/data-lake-implementation

【https://pages.matillion.com/rs/992-UIW-731/images/2019C2】T4—eBook.pdf 数据湖。

[](https://medium.com/membership/@guru.nie) [## 通过我的推荐链接加入媒体

### 阅读 Gururaj Kulkarni(以及媒体上成千上万的其他作家)的每一个故事。您的会员费直接…

medium.com](https://medium.com/membership/@guru.nie)