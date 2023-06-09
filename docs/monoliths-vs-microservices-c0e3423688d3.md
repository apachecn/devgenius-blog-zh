# 单片 vs 微服务

> 原文：<https://blog.devgenius.io/monoliths-vs-microservices-c0e3423688d3?source=collection_archive---------4----------------------->

## 了解哪种架构设置最适合您。

单片和微服务有什么区别，

当涉及到设计你的系统时，你会选择哪一种呢？

让我们开始吧。

![](img/58f97a68efa3041c12814495b53ae3b2.png)

把所有东西放在一起还是全部分开？这是个问题。[图像来源](https://dev.to/alex_barashkov/microservices-vs-monolith-architecture-4l1m)

# 主要亮点

1.  **什么是整体-** 每一个软件解决方案都有多个组件，需要这些组件来使其工作。在整体式架构中，所有组件将一起构建和维护。这意味着当你改变一个元素时，你必须重新构建整个代码。
2.  **什么是微服务-** 在微服务中，系统的不同部分是独立部署和维护的。一般来说，不同的微服务被分配到不同的团队，微服务本身通过 API 调用/网络中继进行交互。
3.  **独石的优点**——一句话——简单。尽管有时名声不好，但 monoliths 是处理小范围项目的一种干净有效的方式。在高度耦合的应用程序中，部署前的测试也变得更加容易，因为在运行测试时，您将能够看到您的新更改是否会破坏您的应用程序。相比之下，对微服务的意外更改通常只有在部署后才可见(尤其是在设计不当的情况下)，导致您的应用程序在运行时中断。
4.  **微服务的优势-** 简单来说，这种系统允许很大的可伸缩性和灵活性。由于每个服务都将被解耦，因此您可以根据需要对资源分配进行微调。更改和部署也会快得多(假设做得对)。[IBM 的这个视频很好地概括了微服务的整体优势](https://youtu.be/CdBtNQZH8a4)。
5.  **结论**——微服务很酷，将带来可伸缩性的提升。然而，它们很难建立，需要更仔细的计划。很多人认为巨石柱很无聊，但它们通常是安全的选择。它们更容易设计，开销也更低(不同的独立服务听起来很酷，直到你不得不挖掘用多种语言、框架和风格编写的代码库)。但是如果你在大型团队中工作，独立服务，并且非常强调规模，那么微服务可能是你的障碍。

对于我的视觉学习者，看看下面的视频。它以一种超级吸引人的方式报道了这场辩论。我也喜欢 Dave 将他的分析与选择一个特定的设置将如何改变你与版本控制的交互联系起来。又增加了一层思考。他还演示了在设置微服务时最常见的失败之一，它首先破坏了这种架构的好处。

如果你想了解技术领袖们对这个话题的想法，可以看看《重构》的这篇文章。它充满了各种专家对该主题的评论和见解。我也非常喜欢他的结尾分析，其中 Luca 展示了不同的团队结构将如何受益于不同的架构选择。

[](https://refactoring.fm/p/monoliths-vs-microservices?utm_source=substack&utm_campaign=post_embed&utm_medium=web) [## 单片 vs 微服务🗿

### 每周我都会根据自己的经验、研究和案例，写一些如何成为更好的工程领导者的建议…

refactoring.fm](https://refactoring.fm/p/monoliths-vs-microservices?utm_source=substack&utm_campaign=post_embed&utm_medium=web) 

最后，如果你有这些方面的经验，我很乐意听听。您可以回复此电子邮件、发表评论或使用我的社交媒体链接来联系我们。

![](img/90b96e67e59f7c9502f4088d37f790f4.png)

如果你喜欢这篇文章，你会喜欢我的每日电子邮件简讯[技术使之变得简单](https://codinginterviewsmadesimple.substack.com/)。它涵盖了算法设计、数学、人工智能、数据科学、最近的技术事件、软件工程等主题，让你成为更好的开发人员。 [**我目前正在进行全年八折优惠，所以一定要去看看。**](https://codinginterviewsmadesimple.substack.com/subscribe?coupon=1e0532f2) 使用此折扣会降低价格-

***每月 800 印度卢比(10 美元)→ 533 印度卢比(8 美元)***

***每年 8000 印度卢比(100 美元)→6400 印度卢比(80 美元)***

[你可以在这里了解更多关于时事通讯的信息](https://codinginterviewsmadesimple.substack.com/about)

![](img/a2eaa6df237c295714fe7109048a13ef.png)

# 向我伸出手

使用下面的链接查看我的其他内容，了解更多关于辅导的信息，或者只是打个招呼。另外，查看免费的罗宾汉推荐链接。我们都得到一个免费的股票(你不用放任何钱)，对你没有任何风险。**所以不使用它只是失去免费的钱。**

为了帮助我了解你[填写这份调查(匿名)](https://forms.gle/7MfQmKhEhyBTMDUD7)

查看我在 Medium 上的其他文章。https://rb.gy/zn1aiu

我的 YouTube:[https://rb.gy/88iwdd](https://rb.gy/88iwdd)

在 LinkedIn 上联系我。我们来连线:[https://rb.gy/m5ok2y](https://rb.gy/f7ltuj)

我的 insta gram:【https://rb.gy/gmvuy9 

我的推特:【https://twitter.com/Machine01776819 

如果你想在科技领域发展事业:[https://codinginterviewsmadesimple.substack.com/](https://codinginterviewsmadesimple.substack.com/)

获得罗宾汉的免费股票:[https://join.robinhood.com/fnud75](https://join.robinhood.com/fnud75/)