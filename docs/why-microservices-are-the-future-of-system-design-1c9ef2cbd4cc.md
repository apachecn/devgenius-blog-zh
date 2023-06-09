# 为什么微服务架构仍然是软件开发的未来

> 原文：<https://blog.devgenius.io/why-microservices-are-the-future-of-system-design-1c9ef2cbd4cc?source=collection_archive---------4----------------------->

![](img/3cbe60c86db1807e4d6a68428d5e97f0.png)

科林斯·莱苏利在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

亨利·福特于 1908 年开始生产“福特 T 型车”。福特渴望找到一种方法，使其汽车成为受消费者欢迎的廉价选择；并意识到要实现这一目标，必须提高工厂的生产能力。

这个问题的解决方案来自福特的一位经理，他观察了当地屠宰场准备各种动物肉块的方法。经理印象深刻的是，每个工人只执行一个切割操作(从而专业化)。他告诉福特公司这一点，并建议他们在自己的生产线上效仿这一流程。经理提出了这样的想法，即每个工厂工人将专门从事一项具体的行动，这样工厂将达到最高效率。在福特公司，他们称之为“装配线”。

福特对这个想法充满热情，并围绕它建立了一个全新的 T 型车生产工厂。使用装配线来生产汽车，福特突然将 T 型车的生产时间从 12.5 小时减少到只有一个半小时！

![](img/5020dda74508dbc9f0688c49d8bafc76.png)

照片由[维多利亚博物馆](https://unsplash.com/@museumsvictoria?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 拍摄

微服务最近在软件世界引起了很多炒作，像亚马逊和网飞这样的大公司都提倡采用这种架构。但是这种炒作的原因是什么，为什么它比更传统的软件架构方法更可取，微服务的突然流行是否归功于福特 20 世纪工厂的装配线？

## **把一个大问题分成小块**

微服务架构是一种设计模式，其中每个微服务只是更大系统中的一小部分。每个微服务执行一个特定的和有限范围的任务，该任务对最终结果有贡献。微服务架构优于更多单片架构的原因之一是微服务更容易构建(因为它们的尺寸更小)。

在装配线出现之前，如果你要制造一辆新车，这个过程既缓慢又繁琐——每个零件都必须定制，并与其他零件连接。这个问题太大了。在旁观者看来，移动的装配线是一个由链条和链环组成的无止境的装置，它允许 T 型车的零件在装配过程的海洋中畅游。总的来说，汽车的制造可以分为 84 个步骤。

## **自主缩放**

让我们说，负责制造方向盘的部分比制造发动机的部分慢。因此，方向盘在我们的系统中产生了一个瓶颈。由于微服务架构(其中每个服务都与其他服务分离)，我们可以独立地扩展这些步骤；允许我们在制造方向盘的部分增加更多的工人，从而使整个过程更快。

微服务也保证了高可用性。假设方向盘站的一名工人患了流感，生产仍然可以继续，因为有更多的员工可以代替生病的工人。在一个单一的系统中，所有的工人都必须熟悉所有的制造过程，或者至少是其中的一大部分，这意味着不可能轻易地在一个特定的工位上增加一个新的工人。当我们雇佣一名新员工时，他的资源将会分散到所有的制造流程中。总的来说，传统的方法需要更多的工人，成本更高，并且没有实现系统的最大效率。

![](img/6fcdceb2bf3f98822997df1744c17083.png)

由 [Garett Mizunaka](https://unsplash.com/@garett3?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

## **松耦合**

松散耦合的概念是减少系统组件之间的相互依赖。耦合会影响您安全地进行更改的能力。系统中的耦合越多，变化就越有可能产生意想不到的效果。松散耦合意味着服务是独立的，因此一个服务中的变化不会影响任何其他服务，这增加了敏捷性，并允许您快速迭代一个小的、集中的功能(产生同样快速的结果)。

使用装配线制造方法，如果我们想改变汽车座椅的设计，我们只需要培训在座椅站工作的员工。只要新的设计仍然适合座椅轨道，并且座椅部件仍然使用机械化带被运送到车站(在微服务类比中，这意味着我们没有改变接口)，没有其他车站需要意识到某些事情已经改变。

这也意味着，如果我们想改变底盘中的螺钉和螺母的类型，使其更加坚固，我们不必到处更换，因为它们只在一个特定的工位上使用。这允许我们在实施微服务时使用不同的技术，这取决于我们的服务正在解决的问题。从而给予团队很大的自由和灵活性。

![](img/5ea410e66d38e0eb7f2b11115d00b320.png)

马库斯·斯皮斯克在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

**专家团队**

拥有一个绑定到特定领域的面向任务的团队会产生更好的结果，并且会让团队更加专注。正如每个工作站负责一项特定任务一样，微服务也是如此。所有团队都是各自职责范围内的专家，因此提高了效率、一致性和质量。

有什么诀窍？

尽管如此，微服务架构也并不完美。当将一个系统分布到更小的部分时，我们通过引入一种通信机制和在网络上分布事务来增加复杂性，这会产生一些我们以前不必面对的问题(剧透:它们将在我以后的文章中讨论)。

![](img/4828c8d435da193bafb1d70543f58f9c.png)

照片由 [Cookie 在](https://unsplash.com/@cookiethepom?utm_source=medium&utm_medium=referral) [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的 Pom 拍摄

**那么，您应该开始使用微服务架构构建您的系统吗？**

简而言之，如果你相信你正在建设的东西，并且相信它有潜力为很多客户服务，那么答案绝对是肯定的。许多基础良好的公司已经开始改变他们的架构，同时让他们的产品就位，这是一个昂贵而漫长的重构。为了预测未来会发生什么，我们应该了解过去发生了什么。所以在福特的故事中可以找到另一个原因。

由于采用了装配线方法，T 型车的生产立即发生了变化。这种汽车开始批量销售，价格是其他汽车的三分之一。其先进高效的生产线每 3 分钟就推出一款新车，这使其成为流水线生产方式效率的典范。许多工厂已经开始复制这些生产流程。今天，这种生产方法是工业中制造产品的唯一方法。

对许多人来说，亨利·福特发明的生产线是第二次工业革命。我相信微服务架构在云计算领域也在做同样的事情。