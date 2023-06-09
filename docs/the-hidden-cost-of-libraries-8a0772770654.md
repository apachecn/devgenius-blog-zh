# 图书馆的隐性成本

> 原文：<https://blog.devgenius.io/the-hidden-cost-of-libraries-8a0772770654?source=collection_archive---------5----------------------->

开发者认为图书馆就像积木，但大多数时候就像器官(难以移植)。

![](img/27f178daf5d3e2400b7dd6dbf529b412.png)

图片由[史蒂夫·布西尼](https://pixabay.com/users/stevepb-282134/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=674828)拍摄

> 一个组件:
> 有一个简单的、定义良好的接口
> ■是一个对象，这意味着数据和方法被组合成一个单元
> ■展示了一定程度的功能专门化(通常通过配置获得)，具有适当范围的生命周期方法来支持所需的功能
> ■被设计为具有重用的预期，尽管重用上下文是不可预测的
> [https://martinfowler.com/ieeeSoftware/componentChaos.pdf](https://martinfowler.com/ieeeSoftware/componentChaos.pdf)(丽贝卡·帕森斯)

人们很自然地认为库是组件，但这并不完全正确。无论如何，我想说两者都有上面解释的原则。重用是[干](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)(不要重复自己)原则的结果。在同一个代码库中干是容易的，但是在不同的产品之间事情就复杂多了。

库是避免产品间代码重复的一种方式。这是重要的部分，如果我们没有代码重复，我们不应该创建一个库。因为拥有一个库比没有库更复杂，维护一个库是昂贵的，如果我们不需要它(没有代码重复)就不要创建它。我们需要应用 [YAGNI](https://en.wikipedia.org/wiki/You_aren%27t_gonna_need_it) 原则，不要仅仅因为“我们将来会用到”就把一个库变得更复杂。
库也必须是[内聚的](https://en.wikipedia.org/wiki/Cohesion_(computer_science))，它们必须解决不超过一个问题，因为否则它们将很难维护。它们必须易于使用，因为它们将被其他人使用，而不是库的创建者。

## 通用与可用

创建一个库要考虑的第一件事是，泛型是可用的反义词。例如，处理自然数的库不能用于分数(分数更通用)，但是分数库迫使我们总是传递“1”作为分母来计算自然数的运算(分数库不太适合处理自然数)。创建过于通用的库可能会导致人们不喜欢使用它们，因为它们很难集成，而且在我们找到稳定的 api 之前，它们会有很多突破性的变化。

这就是通用解决方案的集成比定制解决方案更难的原因。

## 分裂

当我们创建一个库时，我们希望重用它，所以我们需要通过一个依赖管理系统(maven、gradle、yarn、sbt 等)为我们的库设置一个名称和一个版本。假设我们的库很棒，并且组织中有很多产品在使用它:

*   产品 A: v1
*   产品 B: v1
*   产品 C: v1

几个月后，这种情况将会改变，这将会自然发生:

*   产品 A: v1
*   产品 B: v2
*   产品 v1.5 版

现在让我们假设产品 C 发现了 v1 的一个问题，这个问题也影响到了 v1.5，但没有影响到 v2。你可以说没问题，我们可以在产品 B 中使用 v2，但是等等，v2 包含了突破性的变化，而产品 B 有一个很难实现的最后期限。怎么办？。

![](img/30b0860cbea2d19d65624d6f199b9a90.png)

[https://pixabay.com/photos/fragmented-glass-broken-717138/](https://pixabay.com/photos/fragmented-glass-broken-717138/)

作为库的创建者，我们可以在 1.5 版中修复该问题，此时我们已经开始维护同一个库的多个版本。那很难，想象一下我们有 20 个版本要维护。

我们有几种选择来减少或解决这个问题:

*   为旧版本创建日落过程。在这里我们会看到软件的真正问题，人。很多人使用图书馆，所以在日落过程中更难认同他们。
*   在系统中创建服务，使本库工作。一个服务不能有多个版本，即已部署的版本，因此没有碎片。但是这带来了新的风险，如延迟、带宽等。总的来说，网络不是免费的。在这种情况下，我们的服务 API 必须使用向后兼容性进行更改，直到所有客户端都迁移到新的 API。

我说的不是微服务，因为库通常是高度耦合的，同等的服务在你的系统中也是高度耦合的。而耦合是针对微服务的。

## 向后兼容性

另一个解决碎片问题的方法是向后兼容。如果你不创建突破性的改变，那么你的库的所有用户将总是容易地升级到最新版本。

如果你的接口有一定的成熟度，这种方法可以很好地工作，但是会在库中产生技术债务。

向后兼容性对于平稳过渡到下一个重大变更非常重要。如果您将库转移到平台内部的服务，这应该是第一个解决方案。

## 传递依赖性

这是依赖关系最糟糕的部分，一旦你认为你的库没有问题了，就会出现这个问题。假设我们正在开发的产品 P 依赖于:

*   依赖于库 **B v1** 的库 A v1。
*   图书馆 **B v2** 。

通常我们的依赖关系管理系统会尝试为库 B 选择最接近的定义的依赖关系版本。在我们的例子中，库 B 是 V2，但这是一件棘手的事情，库 A 希望库 B 是 v1，而不是 v2。这些问题通常是在 qa、生产中发现的，会产生奇怪的错误。

[***单库***](https://en.wikipedia.org/wiki/Monorepo) 是一个与库共享代码但避免传递依赖、碎片和向后兼容问题的答案。但是它们很难维护，并且需要特定的工具在团队中与它们一起工作。

所以，图书馆不是免费的。它们是有成本的，如果你不需要在两个产品之间重用代码或者重用的代码过于通用，就不要创建库。如果你正在解决的问题能够支持库的隐藏成本，就创建库。