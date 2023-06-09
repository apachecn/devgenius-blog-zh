# 数据工程和分析中的重要 SQL 子句/函数

> 原文：<https://blog.devgenius.io/important-sql-clauses-functions-in-data-engineering-and-analytics-85d8d84c2d78?source=collection_archive---------4----------------------->

数据工程师/分析师应该知道这些。

众所周知，数据工程是关于结构化、半结构化或非结构化数据的。即使对于非结构化数据，我们通常也会应用一种或另一种转换来使其具有某种结构。这将确保我们可以对这些数据应用一个模式，以便能够提取报告、构建仪表板或运行某种业务分析。

![](img/d473995357a64c9a9011bbc1d038ec3a.png)

卢克·切瑟在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

当我们谈论数据时，无论是在数据仓库前端还是在运营前端，SQL 都是它的核心。有一些基本的 SQL 来创建数据库、表、视图、插入、更新、选择、连接等，这些在操作数据库和数据仓库中很常见。我们有聚合函数，如 min、max、sum、count、avg 等，在这两方面都很常见。

但是在本文中，我们列出并简要讨论了在数据工程/分析领域中更相关的函数。我将用示例数据创建更详细的文章，以便更清楚地说明它们是如何工作的，所以这里只是对这些函数的介绍性概述。虽然这些函数更具分析性，但也可以根据转换需求用于数据工程管道。

分析函数可以执行与聚合函数类似的汇总，它们可以以非顺序方式访问数据，可以产生与传入数据相同的行，将有助于获得没有连接的简单 SQL 代码，消除中间表等。这些函数将始终是查询中最后执行的 SQL 操作，因为它们是对查询结果执行的，它们不受 GROUP BY、HAVING 或 WHERE 子句的影响。

现在让我们列出分析函数并简要说明:

1.  **OVER:** 这是用来表示我们将使用的函数都是分析意义上的关键字。
2.  **PARTITION BY:** 也称为查询分区，类似于 group by，但是将数据分成块/分区。所使用的函数在分区内执行。
3.  **RATIO_TO_REPORT:** 计算值与组内合计的比率，这不是百分比，比率之和等于 1。
4.  **ORDER BY:** 这将对传入数据进行排序，并且是一些分析函数(如 ROW_NUMBER、LEAD、LAG 等)所必需的。
5.  **ROW_NUMBER:** 创建一个从 1 开始递增的整数值，后续行获得下一个更高的值。跨越分区边界时复位为 1。
6.  **LISTAGG:** 连接出现在单个列中的值，返回分隔值的字符串。也可以对列中的数据进行排序。
7.  **LEAD:** 根据当前行向前查看若干行，可以访问该行。
8.  **LAG:** 基于当前行回看若干行，可以访问该行。
9.  **排名:**根据 order by 列提供排名。如果有并列的排名，那么它跳过这些数字。例:1、2、2、4、5 等。
10.  **DENSE_RANK:** 类似于 RANK 但是如果有平局它不会跳过 RANK。例:1、2、2、3、4 等。
11.  **FIRST_VALUE:** 检索符合分区边界的列中的第一个值。应与 ORDER BY 一起使用。
12.  **LAST_VALUE:** 检索符合分区边界的列中的最后一个值。应与 ORDER BY 一起使用。
13.  **行:**这是按行限制数据的窗口函数。
14.  **范围:**这是通过列值限制数据的窗口函数。
15.  **第 n 个值:**返回分区中所需的行，它需要 ORDER BY 子句。可以从表格的顶部或底部检索数据。
16.  **保持:**基于数据的漏斗子集，不是基于分区或窗口，而是基于函数。ORDER BY required，OVER 子句不是必需的。
17.  **中位数:**有序数据的中间值。如果行数为偶数，则取 2 个中间值的平均值。
18.  **NTILE:** 单个参数表示所需桶的数量。返回一个整数，表示每一行的组包含。
19.  **CUME_DIST: N** 行数，其值小于或等于该行的值除以总行数。
20.  **PERCENT_RANK:** 对列使用 RANK 函数计算排名，减去 1，然后除以行数减 1。
21.  **PERCENT_DISC:** 将所需百分比与 CUME_DIST 函数值进行比较，返回与等于或高于所需百分比的 CUME_DIST 相关联的列值。
22.  **PERCENT_CONT:** 类似于 PERCENT_DISC，但执行线性插值，返回值不一定来自表格。
23.  **ROLLUP:** 除了我们期望从 GROUP BY 子句得到的常规聚合结果，ROLLUP 扩展还从右到左生成组小计和总计。
24.  **CUBE:** 除了由 ROLL UP 扩展生成的小计之外，CUBE 扩展还将为指定维度的所有组合生成小计。
25.  **分组:**它接受单个列作为参数，如果该列包含由 ROLL UP 或 CUBE 操作作为小计的一部分生成的空值，则返回“1”，对于任何其他值，包括存储的空值，则返回“0”。
26.  **WITH:** 整理大型 SQL 查询，防止重复子查询，可以在新定义的 WITH 子句中引用以前定义的 WITH 子句。
27.  **PIVOT 和 UNPIVOT:** 这两个函数分别用来把行变成列，把列变成行。
28.  **MERGE:** 允许在一条 SQL 语句中执行插入、更新和删除，可以使用 and 和 WHERE 添加附加标准，以确保适当的数据受到影响。

还有一些我认为可能没有涉及到，如果我能包括更多的分析子句/函数，请评论。此外，并非所有的数据平台都支持所有这些功能，所以我们在考虑使用任何功能时都需要小心。我在这里记录了所有的可能性，以便在任何平台上编写查询时有一些思考方向。在接下来的几篇文章中，我将尝试用示例数据记录相关的子句/函数。谢了。

参考资料:

[每位数据分析师需要了解的五大 SQL 分析函数| Dario rade ci |迈向数据科学](https://towardsdatascience.com/top-5-sql-analytic-functions-every-data-analyst-needs-to-know-3f32788e4ebb)

[https://www . analyticsvidhya . com/blog/2022/04/数据工程 sql 简介/](https://www.analyticsvidhya.com/blog/2022/04/introduction-to-sql-for-data-engineering/)

[https://www . plural sight . com/courses/adv-SQL-queries-Oracle-SQL-server](https://www.pluralsight.com/courses/adv-sql-queries-oracle-sql-server)

[https://docs . AWS . Amazon . com/redshift/latest/DG/c _ Window _ functions . html](https://docs.aws.amazon.com/redshift/latest/dg/c_Window_functions.html)

[](https://medium.com/membership/@guru.nie) [## 通过我的推荐链接加入媒体

### 阅读 Gururaj Kulkarni(以及媒体上成千上万的其他作家)的每一个故事。您的会员费直接…

medium.com](https://medium.com/membership/@guru.nie)