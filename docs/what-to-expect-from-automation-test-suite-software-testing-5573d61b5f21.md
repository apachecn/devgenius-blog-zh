# 自动化测试套件——软件测试会带来什么

> 原文：<https://blog.devgenius.io/what-to-expect-from-automation-test-suite-software-testing-5573d61b5f21?source=collection_archive---------15----------------------->

1913 年，福特在制造业引入了生产自动化，这是提高制造业和汽车生产生产率的标志性过程之一。渐渐地，其他行业也开始采用同样的方法，现在你可以在任何地方看到自动化。这里我们将关注软件测试中的自动化。

![](img/79260c1ceddf2c4474653551973f42d8.png)

在软件测试中，我们使用不同的工具和过程来确保我们的软件按照预期和标准交付。软件测试自动化就是这些工具之一，它帮助我们缩短产品交付周期。不同的涉众对自动化套件有不同的期望，这些期望必须由测试开发人员来解决。提供了不同的库和工具来满足他们的大部分期望。然而，如果期望没有得到满足，那么我们都知道，需要是发明之母。但是创新是昂贵的，它们可能需要大量的时间和迭代，这在我看来是完全公平的。

所以，现在我们明白没有什么是不可实现的，但是在有限的时间框架内，自动化工具/框架必须能够按照我的理解解决什么期望。

**框架的简单性**

该框架必须尽可能简单，以便任何人都可以用最少的知识开始工作。尽量只使用标准做法。例如，遵循关于您正在使用的工具或编程语言的标准约定。尝试为测试/方法或类使用详细的名称，而不是使用快捷的名称。如果你正在写代码，尽量不要使用太多的包装器。对于包装器来说，资源必须适应项目，当您将它们移动到不同的项目时，它们会失去编写代码的实际方式的上下文。

**商务人士层**

无论您使用什么工具或框架，您都不能期望每个人都理解所有的东西。你将有一群非技术人员、业务所有者和其他利益相关者，他们对你使用的工具最不感兴趣。他们会对你讲述的场景更感兴趣。因此，您需要以一种简化的方式拥有一个包含测试细节的层，以便业务用户也可以在需要时理解测试场景。

**变更请求**

这里的期望应该是变更请求应该很容易被合并。产品的大变化应该不能强迫你改变自动化的核心。尽管对于框架中的小改进，您必须有一点灵活性。

此外，如果业务逻辑发生变化，自动化将不会自动修复。为什么我在这里写到现在，因为人们已经进入了一个阶段，机器学习被用来修复框架故障或与应用程序相关的变化，但目前为止程度有限。如果业务逻辑发生变化，您也必须改变自动化流程。因此，必须处理变更请求。花点时间了解变化，分析影响并提供估计。永远为未知留一个缓冲。在这里，你需要理解项目管理的概念，并相应地应用它们。不要简单地说，将修复更改。这可能会让你付出很大代价。

变更请求必须与开发变更一起接收。被动的方法是完全不合适的，在这种方法中，测试失败了，然后团队知道这是由于开发/产品流程或功能中的一些变化。

**一切都要经过**——错误的期望

当任何人运行自动化套件时，他们不应该期望所有的测试用例都必须通过。这种做法是不正确的。更好的方法是，执行的自动化测试用例应该通过，如果有任何失败，寻找失败的原因。您可以遵循以下步骤—

1.  如果测试失败，查找任何一个案例并按照步骤操作
2.  我们有一些失败的截图吗？—如果没有，请转到第 5 步，请求提供故障截图作为增强功能。如果是，请执行下一步。
3.  截图是否清楚地告诉我们测试失败的步骤和原因——如果是——解决了问题
4.  如果屏幕截图没有清楚地说明查找日志、测试失败的位置和原因(如果是),请解决该问题
5.  如果日志不清楚—要求更新日志作为改进，然后重新运行测试并进行同样的监控—如果您能找出原因—如果是—解决问题
6.  如果重新执行和监控没有帮助，手动尝试测试步骤并找到根本原因——如果对于失败的用例，测试用例按预期手动工作，向测试开发人员提出问题。如果您手动发现问题，请向产品开发人员/各自的利益相关者报告错误。
7.  所有情况下的故障看起来相似还是不同

**报道**

报道是这里的关键。报告必须涵盖成功、失败、完成状态和相关数字等要点。保持报告简明扼要。该报告必须可供所有主要利益相关方共享/访问。

总的来说，这里的想法是保持事情简单，积极主动地交流变化，并轻松地融入变化。这将有助于你接受其他项目。