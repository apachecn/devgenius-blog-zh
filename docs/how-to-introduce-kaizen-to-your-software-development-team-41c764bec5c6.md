# 如何向你的软件开发团队介绍改善

> 原文：<https://blog.devgenius.io/how-to-introduce-kaizen-to-your-software-development-team-41c764bec5c6?source=collection_archive---------4----------------------->

![](img/f2c0ce505a88bd39480d0200a127aca1.png)

Jukan Tateisi 在 [Unsplash](https://unsplash.com/s/photos/step?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄的照片

我第一次听到“改善”这个词是在一本流行书籍 [*凤凰计划*](https://www.amazon.com/Phoenix-Project-DevOps-Helping-Business/dp/0988262592) 中。在这本书里，我们了解了一个最近被提升的 IT 经理是如何试图解决他的组织中的所有问题的。这些问题似乎很难解决，但他仍然坚持不懈。

对这种性格最大的体会之一就是，没有持续的改进，事情就会恶化。熵定律永远是赢家。此外，书中的人物意识到，一个人不能仅仅命令改变，改变会在一夜之间发生。他意识到，大爆炸式的重写、团队间的指责或“自上而下”的命令都不能解决他的 IT 问题。

相反，从长远来看，微小的、持续的、日常的改善会带来更好的结果。随着时间的推移，变化会一点一点地发生。他的团队需要不断地识别和解决问题、错误和缺点。

一个团队如何去完成它？这样做的有用框架是什么？

## 进入改善

Kaizen 是一个日语单词，概括了“持续改进”的概念形式上，它的实际定义仅仅是“改进”。在丰田将这一想法作为改善生产线的一种方式后，它成为了一种商业概念。你可以在这里阅读所有关于历史的内容。

在本文中，我不想重新定义改善，也不想深入探讨它的所有好处。已经有很多为此而写的[书](https://www.amazon.com/Phoenix-Project-DevOps-Helping-Business/dp/0988262592)和[文章](https://simpleprogrammer.com/kaizen-developers/)。

相反，我想帮你想出一个计划，把这些想法介绍给你的团队。特别是，如何着手引入一个识别和解决问题的框架，就像我们书中的 IT 经理所做的那样。你不需要一个完美的路线图或一个大的演示。你只需要从几件事情开始。

## 去源头

当问题出现时，很容易从别人那里听到。昨晚一个部署出了问题，但是没人知道是谁出了问题，出了什么问题。主管问经理，经理问团队领导，团队领导问开发人员最终找到相关人员。一路走来，大家在往下走的路上稍微改一下问题。答案在上升的过程中略有不同。

相反，你需要找到问题的根源。部署出错了吗？与进行部署的工程师交谈。业绩受影响吗？你的衡量标准是什么？一个团队发展的时间太长了吗？询问团队是什么让他们慢了下来。具有讽刺意味的是，我敢打赌，在许多组织中，团队甚至不知道他们很慢——但他们的经理可能知道。

为了解决这个问题，团队需要两样东西:**可见性**和**反射**。

首先，团队需要了解正在发生的事情，以便每个人都在同一页上。需要监控和安排部署。应用程序需要日志和指标监控。流程需要透明的跟踪——并且需要团队中的每个人都可以访问。你的第一个问题可能只是，“我们不知道这里出了什么问题。”

第二，一旦发现问题，团队要定期反思和评估他们遇到的问题。敏捷团队倾向于在与他们典型的开发步调一致的回顾中这样做。其他团队每周同步讨论问题。

开始这个过程的一个很好的方法是引入回顾。从每月一次开始，因为这通常有足够的时间让团队在每次会议之间实施和跟踪变更。如果你从未举办过回顾展，我建议你看看这篇[的文章](https://www.thoughtworks.com/insights/blog/5-things-you-need-know-facilitate-retrospective)(评论中有很大的讨论！).

## 确定解决方案

一旦你确定了你的问题并对问题进行了评估，你需要头脑风暴如何解决它。有些会有很好很简单的解决方案；其他人可能需要大量的批判性思维。

你可能需要和你的团队进行一次头脑风暴，或者你可能只需要写下一个想法并寻求反馈。这取决于你的团队的动态。

对于需要更广泛的解决方案的大问题，首先要为你想去的地方制定一个愿景。不要满足于“变得更好”如果您的团队目前根本没有监控，也许像下面这样的一个“愿景句子”会有所帮助:

> 我们希望有主动的监控和警报，以便我们的团队在其他团队意识到问题之前得到通知。我们希望这些警报能够清楚地显示出哪里出了问题。

我发现有帮助的是总是想出至少一个想法来呈现给你的团队。这可以让你避免分析瘫痪，并给你的团队一些具体的东西来评估。

![](img/f73b5e7049e59cf9886e53ed05ec7b06.png)

照片由 [Lefteris kallergis](https://unsplash.com/@lefterisk?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 在 [Unsplash](https://unsplash.com/s/photos/step?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 拍摄

## 确定最小的有意义的改进步骤

现在，您已经确定了一个需要解决的问题，并且心中有了解决方案。太好了！现在是困难的部分:确定朝着解决方案前进的最小的有意义的一步。

你的大部分问题都无法快速、一步到位地解决。例如，如果您试图改进您的团队部署软件的方式，要实现您的解决方案，有许多许多事情要做。你需要做的是回溯你的解决方案，问“我们需要做什么？”不断重复，直到你认识到下一步该从你现在的位置开始。

理想情况下，这是你可以立即采取的步骤**。在 GitHub 中创建小组或团队；撰写文档；创建邮递员集合等。这里的要点是，如果你现在就能采取行动，那么你的团队现在也在进步。**

## **再次转到源**

**从这里开始，你重复这些步骤。去源头找问题。集体讨论这些问题的解决方案，为实现它们勾画出远景。确定实现愿景的最小的有意义的下一步，并采取行动。**

**你会发现你原来的视野会改变——这很好！当你继续回到源头，如果你正在改进，问题本身会稍微转移。**

**我喜欢把这想象成清理一个凌乱的房间。你可能会先找出一堆你需要收拾的衣服，然后着手处理，你的目标是把所有的衣服都收拾干净。然而，你发现在衣服堆下面，有人不小心打翻了一株植物，满地都是灰尘。污垢现在可能是最需要解决的问题。**

**Kaizen 是一个强大的精神框架，是如何提高团队的指导。我在这里仅仅触及了皮毛，但是我希望它能够帮助您理解如何在您的团队中开始使用它。**

**编码快乐！**