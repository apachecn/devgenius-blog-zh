# JavaScript 中的数据类型

> 原文：<https://blog.devgenius.io/data-types-in-javascript-51258a45f52e?source=collection_archive---------14----------------------->

在这篇文章中，我将介绍 JavaScript 编程中使用的不同数据类型。

![](img/9d0bf0cc514b23385dc323e49be3d49e.png)

迈克尔·泽兹奇在 [Unsplash](https://unsplash.com/s/photos/data?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄的照片

根据您的观察，JavaScript 语言中有几种不同的数据类型。我将描述 8 种不同的 JavaScript 数据类型，它们属于 3 个不同的类别:原始、复合和特殊数据类型。

**原始或主要数据类型**

有 6 种数据类型被视为原始值。分别是`strings`、`numbers`、`bigint`、`boolean`、`undefined`和`symbols`。因为所有这些数据类型都不是对象，也没有自己的方法，所以它们被认为是原语，是语言实现的最简单层次。除此之外，原语是不能改变的，所以它们是不可变的。当把原始值赋给变量时，这不会使变量必然是原始的，因为变量本身的值有能力改变，所以它是可变的。

**复合或参考数据类型**

`Objects`、`arrays`和`functions`属于复合数据类型范畴。但是，在 JavaScript OOP 中，数组和函数被认为是对象，所以对象本质上是唯一的复合类型。这些被认为是复合类型的原因之一是因为它们可以有多个组合在一起的值。复合类型中的值还可以包含包含任何原始数据类型和复合类型的混合值。复合数据类型具有的另一个特性是，它们可以有与之相关联的属性和方法，这些属性和方法可以通过点符号和调用特定函数的尾随括号来访问。

**特殊数据类型**

`Null`值被认为是特殊的数据类型，也可以被称为特殊的基元类型，因为它们与基元相似。空值和原始值的区别在于，空值表示有意缺少数据或缺少与对象的关系。当需要一个对象，但没有相关的现有对象时，可以返回空值。

在使用任何编程语言时，理解数据类型都是非常重要的，因为数据可能会被不正确地存储，从而导致应用程序出现错误。