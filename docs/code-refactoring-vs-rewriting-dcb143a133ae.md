# 代码重构与重写

> 原文：<https://blog.devgenius.io/code-refactoring-vs-rewriting-dcb143a133ae?source=collection_archive---------4----------------------->

> 永远不要假设，永远要衡量。

![](img/e0b611e08bd15ccfa708e97d2a4989fc.png)

阿诺·弗朗西斯卡在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

> 遗留代码可能很难维护。

作为开发商，当你走到了封闭的街道，无路可退的时候，这是一个非常艰难的决定。我的意思是应用程序代码库是有问题的，有问题意味着它很难维护，需要在你的应用程序中添加新功能，如果程序员想继续下去，他们必须重构或重写应用程序。

[🎥](https://emojipedia.org/movie-camera/) **重构:**是“以不改变/改变外部行为的方式改变软件系统(代码)的过程，通过微小的改变来清理代码。或者用简单的话来说，你可以说这是一种重构现有代码的技术，但要记住它不会改变应用程序的现有行为。

[🎬](https://emojipedia.org/clapper-board/)**重写:是程序员扔掉所有代码，重新开始代码编写的过程。**

**客户总是希望在应用程序中嵌入新的特性/功能，例如**

**👈如果软件代码不够好，不足以解决/处理新的需求，那么就很难维护软件，你应该重新考虑软件设计(架构)。如果你说让我们重写应用程序，这是一种极端的正确，但如果你重写应用程序，这是一种非常激进的方法。你将会有很大的影响，因为突然之间，所有的遗产都将消失，你可以重写所有的东西，但另一方面，你必须做很多工作。你不仅要重写应用程序中所有有问题的部分，还要重写应用程序中没有问题的部分，比如你的登录流程，设置，关于屏幕等等...**

**因此，当选择从头重写代码时，用**重写代码**你会把大量的精力放在你并不真正关注的工作上，也不会增加多少用户价值，你会用你的新风格做大约 50%以上的重复工作，而且重写是一个非常危险的任务，因为你要启动一个全新的重写应用程序，就像一个核☢️按钮开关，并把它一次性放在应用程序上。**

****👉**在光谱的另一端，我们有**再分解**，这实际上是相同但风险更低的方法。您将采取非常小的增量步骤来使您的代码变得更好。通过使用这种技术，您的大多数问题或错误可以通过简单地添加小的更改来修复。开发某人的代码通常很困难，但这并不意味着不可能。重构代码通常会花费更多的时间，但是它可以帮助你检查并让你的用户期待升级，它减少了用户的失望率。但是对于开发者来说，这实际上是很不满意的，因为你改进了一些应用程序/代码，并且在一天结束的时候，你可能觉得你没有真正完成任何事情，所以这是一个缓慢而渐进的方法，但是这表明失去用户的风险很低。它还可以帮助你获得反馈，并逐步改进。**

**让我们总结一下。[🙅‍♂️](https://emojipedia.org/man-gesturing-no/) 首先要记住，要专业🤔保持你的代码整洁，遵循众所周知的架构，不要用一种新的模式来制作你的每个模块/特性，但是如果没有其他方法来解决你的问题，试着适当地记录文档，这样新的 bees 可以很容易地理解你的写作。也不要用瞎眼睛重写整个狗屎，除非一些主要的拦截击中。尝试重新分解、采纳和适应。使用这种技术，您和产品所有者可以摆脱软件在启动时已经面临的许多问题。**

**现在轮到你了！如果你学到了至少一件事&如果你觉得内容值得分享。😊提供反馈、评论或开始讨论。 [✍️](https://emojipedia.org/writing-hand/) 随时纠正错误。[🐛](https://emojipedia.org/bug/)**

# **[😀](https://emojipedia.org/grinning-face/)干杯！！**