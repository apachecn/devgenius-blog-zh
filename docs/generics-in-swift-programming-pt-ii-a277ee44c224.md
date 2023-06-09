# Swift 编程中的泛型。二

> 原文：<https://blog.devgenius.io/generics-in-swift-programming-pt-ii-a277ee44c224?source=collection_archive---------10----------------------->

> IOS 开发和软件工程。

![](img/0241545fcf6f61e507811fed4dcc2fd1.png)

上一篇文章介绍了 Swift 编程语言中泛型背后的基础知识。今天我们将讨论在创建复杂算法或程序时使用泛型的两种非常灵活的方式！今天让我们深入探讨以下主题！

# 泛型的基础

*   关联类型
*   Where 子句

# 关联类型

Swift 语言是非常灵活的，因为它的类型安全语言是由 Apple Inc .开发的。但是当我们讨论关联类型时，泛型可以更加宽松！泛型令人困惑，但是想象一下专门为整数值创建一个协议。但是您决定接下来要有字符串值！这是一个棘手的情况，因为我们必须创建一个符合字符串值的新协议。

让我们帮你省点麻烦吧，因为相关的价值观会震撼我们的世界！我们看看下面的代码，再看看评论。我将指出我们的关联类型在哪里被使用。

关联值用于将字符串值和整数值相加。

我们有上面代码的两个例子；我希望大家注意“foundOne”结构，并看到它与“add task”结构的巨大差异。这是一个很好的关联价值观的例子，也是一个奇妙的方式来看看语言是多么强大，快捷！

# Where 子句

我想让我们考虑一下泛型，并注意到我们越了解代码在做什么，我们就能从中获得越多。如果我们知道使用了什么数据类型和使用了什么协议，Swift 使我们能够进行更熟练的算法。

Where 子句是使我们的泛型更加复杂和健壮的完美例子。假设我想利用可比较的协议，而我们的关联值目前不符合协议的严格准则。我们可以使用 Where 子句，并将可比较的协议添加到我们的关联类型中。我们可以使代码更加灵活，并在关联值中使用类似的运算符。

> 请看我的代码注释；我会指出我想让你明白的一切。这是一个扩展的代码示例，但是它充满了优秀的知识。

Where 子句用于分配可比较的和等同的协议。

# 结论

Where 子句和相关值是很难理解的话题，我强烈建议慢慢理解新概念，并使用泛型编程一些练习算法。我们将在下一篇文章中详细介绍泛型。

不管你能写多好的代码，都要练习精益求精。如果你获得了计算机科学学位或自学成才，只要行动胜于语言，任何人都可以成为成功的程序员。不要让一个错误的时刻毁了你的旅程。学会接受失败，但掌握自己的纪律，在那一刻做出反应。编码快乐！

[](https://www.linkedin.com/in/michael-balsa-9474431b0/) [## 迈克尔巴尔萨-技术作家-开发天才| LinkedIn

### 经验丰富的数据专家，负责监督维护美国的飞机数据和信息管理…

www.linkedin.com](https://www.linkedin.com/in/michael-balsa-9474431b0/)