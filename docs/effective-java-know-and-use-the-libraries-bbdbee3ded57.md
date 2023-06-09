# 有效的 Java:了解并使用库

> 原文：<https://blog.devgenius.io/effective-java-know-and-use-the-libraries-bbdbee3ded57?source=collection_archive---------7----------------------->

![](img/22f3508582d1cf751e47ad7abac90a00.png)

照片由[阿尔方斯·莫拉莱斯](https://unsplash.com/@alfonsmc10?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

这一章深入探讨了一个问题，许多开发人员会发现自己不时会陷入这个问题，那就是重新发明轮子。作为开发人员，我们经常想了解一些事情的细节，而不是学习如何使用别人的代码。也就是说，采取这种立场，我们经常给自己带来伤害。

让我们看一个例子。让我们考虑下面的代码。这段代码的工作是在给定的限制内选择一个随机数:

```
static Random rnd = new Random();static int random(int upperLimit) {
  return Math.abs(rnd.nextInt()) % n;
}
```

乍一看，这段代码可能看起来合理，它似乎以简洁的方式完成了工作。即使经过一些快速测试，它似乎做的工作。目前还不明显的是，这段代码有许多问题:

*   价值的分配是不平等的。这显示的方式将取决于`n`是否是 2 的幂，但是由于二进制算术和数论，分布将不相等。
*   在极少数情况下(当`rnd.nextInt()`返回`Integer.MIN_VALUE`时)，代码会通过调用`Math.abs`试图使值为正，在这种特殊情况下，T3 仍将返回`Integer.MIN_VALUE`。这可能会导致返回一个负数，这可能是代码没有准备好的。这也将是极其难以测试的。

那么我们如何解决这些问题呢？我们干脆用:`Random.nextInt(int)`怎么样？虽然这可能不是你想要的有趣的答案，但事实几乎总是如此。Java 中的内置库函数是由专家编写的，在无数的应用程序中使用过，并且被仔细检查过。这并不是对你的编码技能的侮辱，而仅仅是在每种情况下开发的软件类型的事实。你会从中获得一些好处。

*   您甚至不需要考虑如何完成任务，只需调用函数并继续前进。
*   很可能这些功能的性能会优于你自己的。虽然您可以为您的特定用例编写一个更高性能的函数，但是您能够找到一个比其经过实战检验的版本更快的通用解决方案的可能性很低。
*   当您升级时，您还将从免费改进中受益。即使你什么都不做，你也能看到这些好处。

那么为什么没有人使用这些内置函数呢？我认为最常见的原因可能是缺乏熟悉。毫无疑问，Java 的 API 服务是相当庞大的。认为任何人都可以在大脑中有效地容纳所有的 API 空间是愚蠢的。也就是说，有几个过程可以帮助你:

*   熟悉几个核心包:`java.lang`、`java.util`、`java.io`、`java.streams`等。
*   花点时间阅读每个 Java 版本的发行说明。有了 Java 新的更快的发布周期，这些发行说明可以更容易使用。
*   希望不用说，但是在发明你自己的版本之前，也在互联网上搜索你的问题的解决方案。这通常足以让您熟悉内置函数。

即使 Java 语言中有大量的内置函数，仍然会有一些东西不能在核心语言中实现。尽管如此，还是有一些很棒的通用库，你仍然可以利用它们来解决你的问题。像:`Guava`、`Apache Commons`等库。虽然您不会完全获得内置函数的所有好处，但您会在较小的程度上获得一些好处。

虽然从头实现一个解决方案很有趣，但它很少是正确的解决方案。在实现感觉不独特的功能之前，考虑在核心库中查找，并通过快速互联网搜索来找到现有的、经过审查的解决方案。