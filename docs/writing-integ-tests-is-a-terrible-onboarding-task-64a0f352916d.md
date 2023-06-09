# 编写集成测试是一项可怕的入职任务

> 原文：<https://blog.devgenius.io/writing-integ-tests-is-a-terrible-onboarding-task-64a0f352916d?source=collection_archive---------12----------------------->

*免责声明:所有观点都是我自己的*

![](img/2bfc6f1c3d26a5bcea559efcb90b51ba.png)

[照片](https://www.pexels.com/photo/person-writing-while-using-phone-239548/)Pew Nguyen 来自 Pexels

在我的职业生涯中，我见过几十个团队中的工程师，他们会问:“我们应该让他们做的第一个任务是什么？”对话播放了多次。因此，答案常常是“他们能改进我们的集成测试吗？”

从表面上看，这似乎是一个很棒的选择，对团队和新工程师来说是双赢。团队讨论的好处包括

*   这将帮助他们更加熟悉代码库
*   这将为团队提供更可靠的产品
*   打断是一件容易的事
*   这将是低压力，所以他们不会感到沮丧，如果他们不能取得进展

这样的例子不胜枚举。但今天我想告诉你一些原因，为什么这是一个工程师的可怕的第一个任务。

# 需要领域知识

通常，集成测试关注的是应用程序的行为。目的是验证对您的客户重要的行为，并确保关键用例按预期工作。

但这意味着编写 integ 测试的工程师也必须对应用程序有深入的领域知识。你会努力去验证一些你不懂的东西。

# 它通常需要脚手架

你的软件中为你赚钱的部分通常都有他们需要的脚手架。Nginx 和一个负载平衡器来引入 web 流量、一个已建立的数据库或一台运行批处理的机器。

但是，如果您没有投资 integ 测试，通常需要进行大量设置来运行它。新工程师必须弄清楚如何为测试运行提供场所，研究作为管道的一部分触发测试的不同方法，弄清楚如果测试失败如何使管道失败，等等。

这些步骤通常特定于您的公司，可能并不直观。

# Integ 测试看似维护繁重

您编写和运行的所有代码都需要某种程度的维护。

Integ 测试也不例外。如果您将它们作为质量关放入您的部署过程，对它们的维护突然变得非常重要。如果 integ 测试失败(可能会有假阳性失败)会阻止新功能的推出，这可能是一个令人惊讶的强制维护。

新工程师并不总是能够以长期可维护的方式编写 integ 测试。

# 这是孤独的工作

如果团队到那时还没有优先考虑 integ 测试，那是因为他们不认为它们很重要。如果你给他们安排一个新的工程师，他们很难获得合作或帮助解决问题。

这会让编写 integ 测试变成一种非常孤立的体验。

所以，在你指派新的团队成员编写 integ 测试之前，请三思而行。或者至少尽可能多地用它们来完成测试。

测试愉快！