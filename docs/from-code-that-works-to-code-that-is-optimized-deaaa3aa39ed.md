# 从有效的代码到优化的代码

> 原文：<https://blog.devgenius.io/from-code-that-works-to-code-that-is-optimized-deaaa3aa39ed?source=collection_archive---------21----------------------->

## **使用 Deephaven 数据库中的查询范围**

![](img/860a803f677e76b65dbdb5286b4b3d2d.png)

由[马克·森德拉·马托雷尔](https://unsplash.com/@marcsm?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

哈里森·斯皮萨克

在 Deephaven 数据实验室，我们强调雇佣最好的开发人员向我们的客户提供最好的产品的重要性。那么是什么造就了顶级开发者呢？许多因素造就了一名优秀的开发人员，例如职业领域的经验、多种编码语言的知识以及创建最高效代码的能力。在编写长时间运行的程序时，创建高效的代码是非常重要的。在使用 Deephaven 的数据库时，创建将分析数百万(如果不是数十亿)行数据的程序是很常见的。使用大数据进行编码可能会导致长运行时间——对 Deephaven 用户来说幸运的是，我们的开发人员预见到了这些挑战，并在查询语言中内置了一个工具集来帮助优化和加速代码。一个这样的函数是 *QueryScope* 函数，它允许用户向查询语言添加变量。

# **现实生活中的例子**

我最近创建了一个程序，存储股票市场的日末期权和股票价格。该程序分析了超过 350 亿行数据，并将数据缩小到仅相关的 1000 万行。排序和保存所有这些数据的运行时间超过了 15 个小时，但是如果我没有优化我的代码，运行时间将会是原来的三倍。

第一个程序

在我的第一次尝试中，我成功地创建了一个程序，它做了我想要它做的事情——存储一天结束时的值。**然而，分析一天的数据并保存这些数据需要 7 分多钟。**我需要我的最终程序来分析大约一年半的股票和期权数据，以每天 7 分钟的速度，它必须运行 2 天以上。不顾一切地减少运行时间，我回头看看我的代码，看看如何优化它。经过进一步的检查，很明显我正在排序的表中的每一行都被调用了 *convertDateTime* 函数。 *convertDateTime* 函数的目的是获取一个字符串输入并将其转换为 DBDateTime 格式；然而，这种转换在被调用 350 亿次时是缓慢的。在我的第一个程序中，我将 convertDateTime 函数放在了*中，其中*函数:因为*。其中()*根据函数中的参数过滤每一行， *convertDateTime* 被调用每一行，仅一天的数据就被调用多达 1 亿次。这是多余的，因为 *convertDateTime* 函数在同一天返回相同的值。事实证明，优化这段代码很简单:我所要做的就是利用 Deephaven 的 *QueryScope* 函数，并将 *convertDateTime* 函数移出 *where* 函数。

在 Deephaven 数据库中，用户可以选择使用 Groovy 或 Python 进行编码。不管用户选择哪一个，当使用诸如 *where* 和 *update* 之类的函数操作表时，都会使用 Deephaven 查询语言。 *QueryScope* 函数的工作原理是从 Python 或 Groovy 获取一个变量，并使该变量对查询语言可用。例如，在我的第一个程序中，我使用了 *QueryScope* 函数将变量“day”添加到查询范围，这允许我在 *where* 函数中使用该变量。我的第二个程序利用 *QueryScope* 函数在查询范围内创建一个变量，该变量是 *convertDateTime* 函数的结果。

第二个程序

这只需要增加一行代码，但是差别是很大的:现在， *convertDateTime* 函数每天只被调用一次，这个变量可以在查询语言中用变量“Time”来访问。有了这个小小的改变，一天的运行时间减少到了 2 分钟以下。这是一个很好的例子，说明了有效代码和优化代码之间的区别。

# **总结**

仅仅因为一个程序有效并不意味着它是最好的。通常有一些方法可以减少运行时间，让读者更容易理解代码。理想情况下，如果可以避免，代码不会多次调用函数，Deephaven 的数据库提供了一个简单的工具来有效地处理表，因为函数可以使用 QueryScope 保存为变量。始终关注改进代码和编码技能的方法。