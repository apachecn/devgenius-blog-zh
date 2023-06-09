# 关于异常值

> 原文：<https://blog.devgenius.io/on-outlier-values-f23be20d1bfa?source=collection_archive---------5----------------------->

## 应该如何对待他们？

![](img/8b09ee19b955efabe6b9011ebdd736f9.png)

马库斯·斯皮斯克在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

在马尔科姆·格拉德威尔的 *离群值*中，一个人在投入 10000 小时的练习后，会变得非常擅长某件事。甲壳虫乐队现场演出超过 10，000 小时，成为世界上最伟大的乐队之一。贝比·鲁斯在投手丘上度过了 10，000 多个小时，成为美国最著名的棒球运动员之一。我们谈论的是那些在某件事情上非常出色的人，在同一领域的其他专业人士永远达不到他们的水平。如果你在数据中发现一个异常值，也可以这么说。与其他数据相比，它远远超出了定义的范围。

> 离群值是一个**对象，它明显偏离对象集合**的其余部分。

是对数据点的异常观察。它远离其他价值观。离群值是偏离结构良好的数据的观察结果。

想象一个基于两点的线性方程。离群值不在线上或线附近。它可能离结构良好的数据太远，以至于在图上看不到该点。

**如果我们在数据中看到这种情况，那么应该如何处理异常值？**

有几个选项:

1.  丢弃离群值。
2.  尝试不同的模型。
3.  尝试规范化数据。
4.  使用受异常值影响较小的算法。

## 丢弃离群值。

要删除离群值，只有当它是垃圾值时才能这样做。

分配变量意味着为该变量保留一些内存。在一些编程语言中(如 C ),如果一个变量被分配但没有被赋值，它就被称为“垃圾值”,也就是说，一些信息被计算机内存中的任意一部分保存。

以下面的例子为例:

在给定的数据集中，成年人的身高存储为 int，或者表示某个范围的数学整数(例如 1，10，100)的数据类型。这里，我们看到一个异常值，如下所示:

> 成年人的身高= XYZ 英尺。

这不可能是真的，因为高度不能是字符串值。

> 字符串通常被**认为是一种数据类型**，并且通常被实现为字节(或字)的数组数据结构，它使用某种字符编码来存储一系列元素，通常是字符。

那么，字符串就是一个字符或一系列字符。

*在这种情况下，可以移除离群值，因为数据类型是不允许的。*

或者，如果异常值具有极值，则可以将其移除。

例如，如果所有的数据点都聚集在 0 到 10 之间，但是有一个点位于 100，那么我们可以删除这个点。

丢弃异常值并不总是可能的。在这种情况下，

## 尝试不同的模式。

被线性模型检测为异常值的数据可以被非线性模型拟合。因此，一定要选择正确的型号。

线性模型将连续响应变量描述为一个或多个预测变量的函数。它们可以帮助你理解和预测复杂系统的行为，或者分析实验、金融和生物数据。

线性回归是一种用于创建线性模型的统计方法。该模型将因变量 yy(也称为响应)之间的关系描述为一个或多个自变量 XiXi(也称为预测值)的函数。线性模型的一般方程为:

> y=β0+∑ βiXi+ϵiy=β0+∑ βiXi+ϵi

*其中ββ代表待计算的线性参数估计值，ϵϵ代表误差项。*

非线性模型**描述了实验数据**中的非线性关系。非线性回归模型通常被假设为参数模型，其中模型被描述为非线性方程

## 尝试规范化数据。

这样，极端数据点被拉到相似的范围。

> 规范化是重新组织数据库中数据的过程，以满足两个基本要求:

1.  没有数据冗余，所有数据都只存储在一个地方。
2.  数据依赖是逻辑的，所有相关的数据项都存储在一起。

每个条目的每个单元格只能有一个值，并且每个记录必须是唯一的。

## 您可以使用受异常值影响较小的算法。

算法是在计算或其他解决问题的操作中要遵循的一个过程或一组规则，尤其是计算机要遵循的。

*随机森林就是一个例子。*

![](img/681c94fddad67fcca71f1aa4b51cc974.png)

照片由[简·侯伯](https://unsplash.com/@jan_huber?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

**随机森林是一种监督学习算法。它建立的“森林”是决策树的集合，通常用“装袋”方法训练，这是一种增加整体结果的学习模型的组合。**

随机森林是一种机器学习技术，用于解决回归和分类问题。它利用集成学习，这是一种结合许多分类器来提供复杂问题解决方案的技术。

该算法基于决策树的预测建立结果。

*它通过取各种树输出的平均值或均值进行预测。*

增加树的数量可以提高结果的精确度。

决策树是随机森林算法的构建块。决策树是一种形成树状结构的决策支持技术。决策树的概述将帮助我们理解随机森林算法是如何工作的。

> 决策树由三部分组成:

1.  决策节点
2.  叶节点
3.  根节点

**决策树算法将一个训练数据集划分为多个分支，再进一步将其分离为其他分支。这个序列继续下去，直到到达一个叶节点。叶节点无法进一步分离。**

决策树中的节点表示用于预测结果的属性。决策节点提供了到叶子的链接。

总的来说，如果数据类型不允许或者异常值具有极值，则可以移除异常值。如果异常值不能被删除，那么尝试使用不同的模型、标准化数据或使用不易受异常值影响的算法。