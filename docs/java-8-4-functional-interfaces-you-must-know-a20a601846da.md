# 你必须知道的 Java 8: 4 函数接口

> 原文：<https://blog.devgenius.io/java-8-4-functional-interfaces-you-must-know-a20a601846da?source=collection_archive---------3----------------------->

## 软件工程之旅

## 软件工程师必须知道的 Java 函数接口

![](img/36be0396868ec635f534dd5dddfcda20.png)

照片由来自 unsplash.com[的](https://unsplash.com/)Ash Edmonds 拍摄

# 概观

函数接口是只包含一个抽象方法的接口。从 Java 8 开始，lambda 表达式可以用来表示函数接口的实例。一个函数接口可以有任意数量的默认方法。

在这篇文章中，我想推荐 Java 8 中最常用的四个函数接口，以及独立应用它们和 lambda 表达式的方法。

# #1 功能

我想提到的 Java 8 中的第一个函数接口是 Function，和 Java 中的普通函数一样。功能接口也有输入和输出，对于给定的输入，我们将通过“应用”方法接收相应的输出。然而，在 java 8 中，我们只能使用由 Function 和 BiFunction 表示的一个或两个输入来应用函数接口的函数。马上，我将提供一些例子来看看它的工作方式。

您可以在示例中看到，我们有普通功能，其他的使用功能，功能接口的双功能。它们具有相同的结果，对于函数接口，我们可以用更短的代码轻松地将两个函数组合在一行中。现在，让我们看看运行 main 方法后的输出:

![](img/1ef441d471f1c7f55c911c749cef303e.png)

在上面的例子中，我向你展示了功能接口的基本功能。你也可以看到 java 8 中的函数和 map 在 stream API 中的应用等等。除此之外，您还可以为您的代码应用一些额外的函数方法，如下所示:

## **功能:**

**compose:** 返回一个组合函数，该函数首先将 before 函数应用于其输入，然后将该函数应用于结果。

**然后:**返回一个复合函数，该函数首先将此函数应用于其输入，然后将 after 函数应用于结果。

**identity:** 返回一个总是返回其输入参数的函数。

## **双功能:**

**然后:**返回一个复合函数，该函数首先将此函数应用于其输入，然后将 after 函数应用于结果。

# 第二大消费者

与函数不同，消费者只有输入数据，完成后消费者不会返回任何数据。它类似于普通的空函数，我们可以处理任何没有结果的逻辑。为了执行一个消费者，我们将使用“接受”方法。然而，Java 8 只为消费者提供了由 Consumer 和 BiConsumer 表示的 1 和 2 个输入。现在，我将通过一个关于消费者的例子来展示如何应用消费者。

与函数的例子一样，这些例子也提供了普通的函数和函数接口的消费者。功能接口的消费者也使代码更短，并帮助我们更容易地组合功能。同样，让我们看看 main 的输出:

![](img/1cf977c703dca562656ab27e4134c3ef.png)

Consumer 和 BiConsumer 都有一个额外的方法 is，然后，您可以使用以下信息引用该方法:

**然后:**返回一个复合的双消费程序，它依次执行此操作和 after 操作。

# #3 谓词

这个函数接口的目标是检查我们的输入数据，主要的执行方法是“test ”,它为我们提供输入数据条件的结果。Java 8 提供了两种类型的谓词:谓词和双谓词，我们可以分别用一个和两个输入来检查它们。让我们深入这个例子来弄清楚它。

主方法的输出:

![](img/dd2adb3565a7994a6d8854901bee0a0d.png)

因为谓词用于检查条件，所以谓词中存在一些额外的方法来组合多个条件。谓词和双谓词都包含相同的附加方法。您可以参考以下方法:

**取反:**返回一个谓词，表示该谓词的逻辑取反。

**or:** 返回一个复合谓词，表示该谓词与另一个谓词的短路逻辑 or。

**and:** 返回一个复合谓词，表示该谓词与另一个谓词的短路逻辑 and。

# 第四大供应商

这是一个简单的功能接口，我们不需要输入，只需要得到我们想要的输出。这个函数接口经常使用“get”方法来获得函数的结果，而不需要输入，比如构造函数、获得对象实例的函数等等。让我们看看下面的例子是如何工作的。

主方法的输出:

![](img/e5952cf92aeeb7941f676d2a8eed15ce.png)

# 摘要

应用函数接口可以使我们的代码更加可读、干净和简单。上面的文章展示了 Java 中最常用的四个基本函数接口。希望这些内容对您有所帮助，并清楚地说明了如何将功能接口应用到您的实际项目中。谢谢大家！

*如果你喜欢这个故事，你也会喜欢:*

*   [*你必须知道的 Java 18: 4 特性*](/java-18-top-4-features-you-must-know-1f36ee23e2ab)
*   [*你必须知道的 Java 11: 8 特性*](https://medium.com/@techisbeautiful/new-features-you-must-know-in-java-11-and-examples-3fda2ad26def)
*   [*你必须知道的 Java 8 : 7 特性*](/java-8-seven-features-you-must-know-and-examples-1c3964ae7fe8)

*喜欢这篇文章？给我弄个* [*Ko-fi*](https://ko-fi.com/techisbeautiful) *。*

*爱我的文字？加入我的* [*邮箱列表*](https://medium.com/subscribe/@techisbeautiful) *。*

*爱读书？加入*[*Medium*](https://medium.com/@techisbeautiful/membership)*(如果你用这个链接，也是支持我，因为我有一点 Medium 的提成)。*