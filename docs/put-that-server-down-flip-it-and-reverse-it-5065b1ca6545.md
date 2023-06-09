# 把那个服务器放下，翻转过来，再反过来

> 原文：<https://blog.devgenius.io/put-that-server-down-flip-it-and-reverse-it-5065b1ca6545?source=collection_archive---------9----------------------->

![](img/ed2b582a4b8a8664fb676adfcc9003e3.png)

# 对托管设置进行反向工程

在我的职业生涯中，我在这个地方着陆过很多次。我最终负责支持或解决一些不是我建立的东西的地方。一些很少或没有文档的东西，我没有以前的开发资源。但是我现在有管理员权限或根凭证，被告知要解决这个问题。我需要找到一种气味。我需要探探地面，看看建造这东西的人以前经常去哪里。

通常，我喜欢从给我权限的客户/团体生成一个问题列表开始。他们可能认为自己什么都不知道。但是，如果他们能给你一个常见问题的想法，架构选择，它的东西，它可能会节省你很多时间。如果你第一次问了一大堆问题，而他们没有答案，那就重新措辞，再试一次。人们知道的总是比他们想象的多。你只需要用一种帮助他们记忆的方式问他们。

# 重要的事情先来。

为客户提出这些问题。问问你自己，写下你可能有的每一个问题。以下是一些帮助您开始的示例:

*   代码库是什么？
*   代码库在源代码控制中吗？(好家伙，这有时是一个有趣的问题)。

> 客户:“什么是源代码管理？”
> 
> 我:“……”

*   什么样的服务器？
*   你能提供任何关于事物如何被建造的文件或来回的谈话吗？吉拉任务，基本架构图，部署步骤，操作文档，任何东西？

> 如果没有，或者他们没有给你提供任何有价值的东西，你需要设定现实的期望。你不能做任何承诺。“这将是一次战略性的采矿行动；我们需要一次做一大块。”

*   有多少人用这个东西？
*   如果坏了可以吗？
*   这个站点/应用程序/程序有过任何问题吗？定期保养？

> 也许某个特定的部分经常需要处理:数据库变满，日志变满，磁盘空间耗尽，缓慢恼人的内存泄漏在几个月后成为问题。

*   如果它倒下了。它能舒服地躺多久？

> 这可能是一个糟糕的问题，但它让你知道你的调查需要多么认真和仔细，或者支持它将是什么样的。可能的答案:人会死；我们经常安排停机时间，但它需要在所有工作时间都可用；没什么大不了的。我们有一个客户，他们只在星期一使用它。如果它在周一被打破了。只要给我们提个醒，没什么大不了的。实际上没人用这个。我们已经失去了所有的希望。备份它，并打破它。

*   您有多个环境吗？
*   你的管道情况怎么样？
*   与你正在做的东西的所有者确认:这个东西是做什么的？
*   我能接触到创作这个的原创者吗？

> 如果没有，应该设定更多的期望值。如果有许多移动部件，这可能需要很长时间。

![](img/c563d16c08fac76469c887d857dbbcdd.png)

# 深入研究并创建文档

开始挖掘，掌握一切。试着回答尽可能多的你在钻研系统或架构图(清晰图表、Vizio、写字板)时最初产生的问题。不管它们看起来多么简单，它们都是有用的。绘制出你所知道的片段，以及它们之间的联系。每当你发现一个你不知道的新组件时，用一个占位符把它扔在图上，这样它就在你大脑的架子上，直到你发现它的作用(如果它确实有作用的话)。

如果你在某一点上卡住了，不知道事情是如何工作的，或者它是如何产生的——用尽可能多的信息淹没你自己。然后让它腌制。走开。睡觉。再次压倒自己。我该如何面对这些情况呢？…如果我完全理解了这一点——我真的很棒……必须。保持。希望)。在某一点上，您要么已经达到了您的目标，并且已经完全拥有、理解和控制了系统，要么您可能已经确定有些事情无法解决，因为原始的源代码控制已经丢失并且无法从 dll 进行逆向工程。无论如何，**记录下**你产生的所有问题及其答案，你的不同运动部分的图表，以及你在斗争中的所有笔记。把他们打包，确保他们活下去，这样下一个幸运的人就不用受苦了。并且有一个坚实的起点来从你停止的地方开始。

## **——安迪·海宁格，AWH**的开发工程师。我们正在帮助企业通过技术推动增长。