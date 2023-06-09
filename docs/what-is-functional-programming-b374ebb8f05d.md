# 什么是函数式编程？

> 原文：<https://blog.devgenius.io/what-is-functional-programming-b374ebb8f05d?source=collection_archive---------25----------------------->

![](img/84f95ba9d80b7d14c114261db3b5376e.png)

诺德伍德主题公司在 [Unsplash](https://unsplash.com/s/photos/computer?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄的照片

顾名思义，函数式编程是一种用函数构建应用程序的编程风格。这是通过使用纯函数、递归和避免副作用、可变数据和共享状态来实现的。它本质上是声明性的，这意味着它将告诉程序它必须做什么，而不是解释它将如何做。这种范式可以在几种不同的语言中使用，如 Lisp、Python、Erlang、Haskell、Clojure、JavaScript 等。

## FP 的优势

函数式编程有几个好处。其中之一是，因为使用了纯函数，所以更容易预测结果，也更容易在出现问题时调试程序。如果你想了解更多关于纯函数的知识，可以参考我之前的帖子，[什么是纯函数？](https://medium.com/dev-genius/what-are-pure-functions-fbcda292cb32)

另一个优点是函数式代码使用惰性求值，只在需要时存储值，不进行任何临时计算。这是最优的，因为它避免了重复计算输入，从而减少了应用程序运行所需的内存。

函数式编程的另一个几乎显而易见的优点是，它使读取代码中的值变得更加容易。所有开发人员都知道，你不是唯一一个阅读和处理代码的人。让它对你的团队和未来的开发者有逻辑意义是更快生产的关键。

## 不足之处

现在，要记住函数式编程的缺点。编写一个纯函数的过程通常很容易，但是组合多个纯函数来构建一个应用程序是困难的部分，尤其是对于初学者来说。也有大量的高级数学术语用于描述范式，这可能令人生畏，也更难理解。由于函数代码中经常大量使用递归，再加上不可变值的使用，这会导致性能下降。

## 何时使用函数式编程？

当您的应用程序所基于的数据集是固定的时，这就是函数式编程最可取的时候。因此，依赖于执行数学计算或以并发性或并行性为目标的程序是函数范式的理想选择。

## 总之…

函数式编程可能不像面向对象编程等其他开发风格那样被广泛使用，但它在过去 20 年左右的时间里越来越受欢迎，因此了解和理解它仍然很重要。像往常一样，让我知道我在评论中做得如何，以及对未来的主题是否有任何建议。