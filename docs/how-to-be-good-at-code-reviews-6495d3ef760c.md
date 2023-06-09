# 如何擅长代码评审

> 原文：<https://blog.devgenius.io/how-to-be-good-at-code-reviews-6495d3ef760c?source=collection_archive---------4----------------------->

![](img/20d41795da1bb57da33fa8f810991f7f.png)

查尔斯·德鲁维奥在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

在我作为开发人员的时间里，我已经进行了数百次代码审查。这是我学会非常享受的事情，因为它给了我其他人对我们代码库的看法。大多数时候，我从中学到一些新东西。在这篇文章中，我想介绍一些如何做好它们，尤其是如何享受它们的技巧。

# 良好的管道

大多数团队都有某种代码风格的规则和关于如何统一他们的代码库的建议。无论您做什么，不要强迫代码审查者检查拉请求是否符合那些规则。有工具可以做到这一点。这些工具应该作为你公关渠道的一部分。

SonarQube 是其中一个工具，它将改善团队中每个人的代码评审。它可以发现风格问题，但可以做得更多。通过他们的代码分析，他们可以发现你在代码中最常见的错误。你从未关闭你的资源？声纳会让你知道。就我个人而言，在 Sonar 完成它的工作之前，我从不做代码审查。

你需要有一个具体的流程，每当有人创建一个公关或在那里推出新的变化时，这个流程就会运行。步骤可以是这样的。

*   编译代码
*   运行测试
*   运行林挺
*   运行 SonarQube
*   执行手动审查流程
*   合并到主代码库

# 立交桥

像第一件事一样，在我的回顾中，我将对所有更改的文件做一个快速的概述。我通常在拉请求 UI 中这样做。在这个阶段，我只关注几件事。

首先是代码的可读性。阅读体验如何？正在做的事情很明显吗？好的代码应该一眼就能表达出它的目的。然后我试图弄清楚这个变更是否是相应的变更请求所要求的。我将通读票证，并尝试匹配拉取请求中的所有要求。

在这个阶段，我不会深入研究实现细节。我为后面的阶段确定这些。

此阶段传达的可能要点:

*   变化不太可读
*   变更不包括要求，或者变更请求单没有随着要求的变更而变更
*   缺失测试

# 做深

在简短的代码飞越之后，我有一个需要深入研究的已更改文件列表。我通常在 IDE 中这样做，这样我可以更好地看到文件之间的连接，但是对于大多数更改，在 pull 请求的 web UI 中这样做是可以的。

我首先问自己如何解决这个问题，然后从那里开始。我们的代码库中是否有一段代码做类似(或相同)的事情？有没有一个库(我们目前使用的)可以用来做这件事？如果有一个我们目前不使用的库，是否值得添加来解决这个问题？

# 测试回顾

不要忘记复习考试。所有案例都有效吗？那些测试有可能发现什么吗？断言可读吗？有测试吗？

如果作为评审者，你觉得有可能添加测试来改进代码库，不要害怕反击添加更多的测试。

# 做好人，有教养

无论你做什么，不要傲慢、刻薄，听起来像个万事通。如果建议的解决方案是有效的，但你会以不同的方式来做，你可以这样说，但也批准请求。你可以留下教育评论，但是太多的教育评论是有害的。考虑什么感觉重要。不要为小事争论，人各有不同，各有各的看法。

# 同意

审批要快，不完美也可以。

这是你应该遵守的黄金法则。

更多类似的建议，你可以在 Twitter 上关注我。

*原载于 2021 年 5 月 5 日*[*https://dev . to*](https://dev.to/pavel_polivka/how-to-be-good-at-code-reviews-2lpl)*。*