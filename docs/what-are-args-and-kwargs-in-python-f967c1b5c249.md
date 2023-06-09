# Python 中的*args 和**kwargs 是什么？

> 原文：<https://blog.devgenius.io/what-are-args-and-kwargs-in-python-f967c1b5c249?source=collection_archive---------11----------------------->

函数是 Python 的重要组成部分。如果您刚刚开始学习 Python，不管这是您的第一种编程语言，还是您从另一种语言来到 Python，那么您已经知道函数声明中的参数数量对应于调用时传递给函数的参数数量。

![](img/5aaff6e6f490fdb9c19b4cb55d48eb57.png)

照片由 [Hitesh Choudhary](https://unsplash.com/@hiteshchoudhary?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

这些是基本的。这有助于人们了解他们周围的世界。但是“参数个数等于实参个数”这句话给初学者的脑袋里放了一颗定时炸弹，是他在函数声明里看到神秘的`*args`或者`**kwargs`之后触发的。

不要让所有的徽章把你逼入昏迷。这里没有什么令人畏惧的。一般来说，如果你对这些结构不熟悉，我建议在那篇教程中讨论它们

# 位置和命名参数

为了理解`*args`和`**kwargs`，我们需要理解位置和关键字参数的概念。

首先，我们来谈谈它们有什么不同。在最简单的函数中，我们只是匹配变量和参数的位置。参数# 1 对应于参数# 1，参数# 2 对应于参数# 2，依此类推。

调用该函数需要这三个参数。如果您至少跳过其中一项，您将会收到一条错误消息。

如果在声明函数时为参数指定了默认值，则在调用函数时不再需要指定相应的参数。该参数成为可选参数。

当使用可选参数的名称调用函数时，也可以指定可选参数。

在下面的例子中，我们将三个参数设置为它们的默认值`None`,看看如何使用它们的名字给它们赋值，而不考虑调用函数时参数的顺序。

# 运算符“星号”

运算符`*`通常与人类的乘法运算联系在一起，但在 Python 中，它也有不同的含义。

该运算符允许您“解包”包含某些元素的对象。这里有一个例子:

在这里，列表的内容被取出`a`，解包，并放入列表`b`。

# 如何使用* args 和** kwargs

因此，我们知道 Python 中的“星号”操作符能够从对象中“提取”元素。我们还知道有两种类型的函数参数。有可能你自己已经想到了这一点，但是，为了以防万一，我要说一下。即，`*args`是“arguments”的简称，** kwargs 是“keyword arguments”的简称。

这些构造中的每一个都用于拆箱适当类型的参数，允许用可变长度的参数列表调用函数。例如，让我们创建一个可以显示学生在测试中输入的结果的函数:

我在声明函数`*args`时没有使用构造。相反，我有——`*scores`。这里有错误吗？这里没有错误。关键是“args”只是一组用来表示参数的符号。这里最重要的是操作员`*`。而他之后到底发生了什么，并没有起到特殊的作用。通过使用，`*`,我们已经根据函数被调用时传递给它的内容创建了一个位置参数列表。

我们想通了`*args`、`**kwargs`之后，理解应该没有问题。名字也不重要。主要是两个符号`**`。多亏了它们，创建了一个字典，其中包含调用函数时传递给函数的命名参数。

# 结果

以下是一些帮助您避免函数常见问题并扩展知识的提示:

*   使用传统设计`*args`和`**kwargs` 来捕获位置和命名参数。
*   `**kwarg` s 结构不能放在`*args`之前。如果您这样做，将会显示一条错误消息。
*   注意命名参数和`**kwargs`之间的冲突，如果一个值计划作为`**kwarg`参数传递，但是该值的键名与命名参数的名称相同。
*   操作符`*`不仅可以在函数声明中使用，也可以在被调用时使用。

**亲爱的读者们！**声明 Python 函数时最常用的参数是什么？