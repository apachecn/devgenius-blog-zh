# 我们来建吧！

> 原文：<https://blog.devgenius.io/builder-pattern-fd0fed6002ff?source=collection_archive---------4----------------------->

![](img/985f89a8efbc6242cded0c16a0473b68.png)

Photo by [贝莉儿 DANIST](https://unsplash.com/@danist07?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

假设你拥有一个网站，人们可以在那里买卖汽车。不用说，您必须有一个搜索页面，用户可以在其中指定大量的搜索条件。类似下面的页面来自[cars.com](https://www.cars.com/for-sale/advanced-search/):

![](img/45b3d2215ac49301ae223e70cf7a157e.png)

你如何对这个需求建模？

嗯，我想到的第一个想法是创建并填充一个搜索条件实例，并将其传递给一个方法，该方法将根据该条件返回结果。大概是这样的:

这种方法的一些问题:

1.  这里最明显的问题是参数的数量。根据 [Susan Weinschenk 博士](https://twitter.com/thebrainlady)的研究，将你提供给人们的信息限制在四条以内几乎是最佳的。任何超过这一点的事情，作为人类，我们都容易忘记，或者至少会对此感到紧张/不舒服。这一点以及她出色的书[中的更多内容，每个设计师都需要知道的关于人的 100 件事](https://www.amazon.com/Things-Designer-People-Voices-Matter/dp/0321767535)，我强烈推荐给每个软件开发人员。毕竟，我们——软件开发人员是设计师。
2.  具有长参数列表的方法的另一个问题是，您可能很容易忘记哪个值是什么。在上面的例子中，当你看到第 8 个参数为零时，你可能很容易弄不清楚这个值是什么。是一个最小里程数，一个最低价格，甚至是一个二进制值来指定汽车是否有天窗。**如果你作为一名开发人员看着代码感到困惑，这意味着它没有被正确设计**。一个设计良好的产品是不含糊的，因为它是不言自明的或直观的，给人一种愉快的体验，而且非常漂亮。
3.  如果用户只指定车身样式，并希望列出轿车车身样式的所有汽车，该怎么办？我们该怎么办？我们只需填充第一个参数，并将所有内容设置为默认值，如下所示:

我敢肯定，你们大多数人都会同意，这是相当丑陋的。一堆没有附加值，有很多问号的代码。**没有附加值的代码不仅无用，而且有害；它需要灭亡**。

对于这种情况，我不打算解释为什么我们不应该创建然后调用一个新的构造函数；我认为这不是一个好主意的原因是显而易见的。

4.最后，但同样重要的是，我将引用罗伯特·c·马丁的必读书籍《干净的代码》中的一句名言:

*   函数的理想参数数是零(niladic)。
*   *接下来是一(一元)，紧接着是二(二元)。*
*   *在可能的情况下，应该避免三个论点。*
*   超过三个(多元的)需要非常特殊的理由——而且无论如何都不应该使用。

尽管一开始他似乎强调了参数的数量，但也许这里更重要的问题是关于软件测试的。如果您曾经编写过任何单元测试，或者对它略有所知，那么您一定知道，随着参数总数的增加，方法中每个新引入的参数都需要您创建越来越多的测试用例。一个方法的变量越多，它的业务逻辑就越复杂。

那么，我们如何解决所有这些问题，同时保持一切干净简单呢？嗯，每个决定都有取舍。修改代码会耗费我们宝贵的时间和精力，但从长远来看，这是值得的。无论是就你正在开发的产品还是你的个人职业生涯/进步而言。

现在比较这些:

后者看起来像是某个[关心](https://www.goodreads.com/quotes/7630389-clean-code-always-looks-like-it-was-written-by-someone)的人写的。关心他正在开发的产品。关心他工作的公司。关心队友。关心她/他自己的名誉。最后，他开始关心那些他永远也不会认识的人——在他去世后很久仍在从事代码工作的程序员同事。

请注意，我们以流畅的方式一个接一个地链接方法(如果你好奇，可以谷歌“方法链接”、“流畅接口”、“流畅 API”)。我相信你已经知道这种技术是 LINQ 中的[方法语法。](https://www.geeksforgeeks.org/linq-method-syntax/)

我可以听到我懒惰的内心声音在抱怨:当我们可以简单地只设置所需的属性时，为什么要费心编写所有额外的代码呢？

好吧，很公平。:)我建议你不要仅仅因为你可能错过一些[捷径](https://www.goodreads.com/quotes/568877-i-choose-a-lazy-person-to-do-a-hard-job)而忽视你懒惰的内心声音，它甚至可能[让你成功](https://www.telegraph.co.uk/money/consumer-affairs/lazy-procrastinating-could-make-wildly-successful/)。有时候最好的解决方案是最直接的。

然而，我恐怕要告诉你，这次不是。提议的惰性解决方案会带来以下问题:

*   我们需要尽可能避免将所有字段都公开为公共可设置属性，而更喜欢具有只读属性的构造函数。
*   [所有输入数据都是邪恶的](https://www.codemag.com/Article/0705061/All-Input-Data-is-Evil-So-Make-Sure-You-Handle-It-Correctly-and-with-Due-Care)，需要验证。如果我们没有任何限制/验证，对象可能会转换到无效状态。举个例子，假设有两个属性，分别是 MinYear 和 MaxYear。当我们将 MinYear 设置为 2019，将 MaxYear 设置为 2018 时，对象会切换到无效状态，使用此搜索条件实例进行搜索变得毫无意义。当然，您可以在实际进行搜索的方法中添加一些验证，但是我坚信对象首先不应该处于错误的状态。

您可能已经从构建器模式代码示例中注意到，在末尾有一个 Build()方法。该方法是方法链中的最后一环，是添加一些规则的最佳位置，例如:

*   最小年份不能大于最大年份。
*   一对夫妇必须总是正好有两扇门。
*   一辆汽车的汽缸数量必须在 1 到 12 之间。

我不想用很长的代码块让你窒息，所以我会留下一个链接，你可以在这里 下载所有的源代码 [**。**](https://github.com/anar-khalilov/builder-pattern)

总而言之，当我们需要以简单、干净和可持续的方式创建高度可配置的对象时，我们使用构建器模式。