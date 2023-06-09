# 堆栈溢出是为了什么？

> 原文：<https://blog.devgenius.io/what-is-stack-overflow-for-1960b794a471?source=collection_archive---------2----------------------->

## 给有抱负的软件工程师的建议

电动工具很有用，但要安全使用。

这篇博文描述了一些有抱负的软件工程师使用互联网的反模式。我的观察是我自己的，我很少努力将它们与科学研究联系起来。尽管如此，我希望它们对某人有所帮助。

# 互联网反模式

作为一名计算机工程教授，我教授并指导许多有抱负的软件工程师。这些原型工程师面临着一个诱惑，我在学生时代不必与之斗争:Stack Overflow 及其兄弟。

大多数以编程为主题的互联网帮助网站都是在我上大学的时候出现的，我和我的朋友们都取笑它们太局限了。时代变了。如今，似乎你可以用谷歌搜索来回答几乎所有的编程问题，在 Stack Overflow 和 Quora 这样的网站上，这些问题都有很高的投票率。

有时我看到这种便利将一个有抱负的软件工程师引入歧途。这是互联网的反模式:*通过反复求助于堆栈溢出进行编程，复制代码来解决每个错误，最终得到一个你并不完全理解的部分解决方案*。我的一些学生最终陷入了困境，并报告说花了很长时间——超过 10 个小时！—在不成功的堆栈溢出追踪中。

# 有效使用堆栈溢出的提示

## 花点时间思考一下

下一次你发现自己正前往 Stack Overflow 寻求帮助时，问自己几个问题:

1.  "*我是否有足够的专业知识来理解这个建议是否合理？*“如果你做到了，太好了。但如果不是，你的时间最好花在发展你的专业技能上。
2.  "*当这个代码片段不工作时，我能调试它吗？"大多数堆栈溢出帖子需要根据您的上下文来定制，许多帖子有细微的错误，因为它们只是为了举例说明。在不知道代码如何工作的情况下，你不应该从别人那里获取代码。*
3.  *“我完全理解这个问题及其解决方案有多重要？”*在工程工作中，有些知识很关键，有些知识不关键。大多数工程师不需要深入掌握日期时间格式或定义有效电子邮件地址的 RFC。互联网资源是找到适合此类任务的代码片段的好方法，然后您可以将其隐藏在实用程序库中一个友好的 API 中。但是如果你正在为关键的业务流程(或者你学校项目中的关键算法)编写代码，那就要小心了。
4.  “我寻找解决问题的方法有多长时间了？“就我个人而言，我使用一个“5 分钟”规则。如果我寻找解决方案的时间超过 5 分钟，这通常是一个信号，表明我的问题有问题。这意味着我应该转而研究和发展我对问题和我所使用的工具的理解。另一种解释是，我的问题非常模糊，我是第一批试图解决它的人之一——所以我最好专注于解决它！

## 磨快你的斧子

如果我可以选择(a)花 10 个小时调试我不太理解的错误，或者(b)花 9 个小时阅读技术手册，然后花 1 个小时应用我新学到的技能，我知道我会选择哪个。J. Strong 有一句老话:“*磨利斧头的时间可以省去挥舞斧头的时间。*“你应该寻求发展长期可重用的技能，而不仅仅是从一个快速解决方案到另一个快速解决方案。

在软件工程中，有成千上万的教程指导你编写你的第一个 Android 应用程序，建立你的第一个网站，甚至实现你的第一个 Linux 内核模块。这些资源是有价值的，但不要变得过于自信。如果你完成了这些教程中的一个，你现在已经知道足够多的知识去*开始*探索。不要停在那里！以下是我建议你接下来要做的:

1.  要有一种寻求掌握所学课题的态度。花时间讨论这个话题——无论是编程语言、框架、技术栈、查询语言、设计模式还是算法。你在学安卓吗？花半天时间通读 Android 开发者手册。你在学 C++吗？接受 Stroustrup 的建议。你在学习设计模式吗？在四人帮下学习。
2.  当你以精通为目标时，确保你学以致用！画一些 UML 图，自己尝试 TDD，写一些 map-reduce 查询。但不要在“活病人”身上做实验。在一个独立的程序中做一点练习就可以发现隐藏在程序内部的一个问题。然后你就可以把你学到的东西转移到你真正的项目中去了。

不要试图快速致富，不要在不投资专业知识的情况下寻求成为专家，不要误解精通的本质。专家之所以是专家，是因为他们明智地投入了时间。我想，你可以通过阅读足够多的堆栈溢出帖子来发展专业技能，但这是一条痛苦的道路。如果你认为你的专业知识缺乏，你的时间花在学习和实践上会比寻找和挣扎好得多。

# 我只是一个暴躁的老人吗？

如果我回避对学生时代接触过的“无用工具”的一些反思，那将是我的失职。个人笔记本电脑是主流，ide 正在成熟，Linux 发行版和虚拟机技术是消费者友好的(尽管驱动程序生态系统还没有完全到位)。这些技术本身就是一套“强大的工具”,超出了上一代计算机专业学生的想象。我曾与年长的技术人员交谈过，他们在 10 磅重的笔记本电脑上学习，在公共图书馆学习，在有穿孔卡的大型机中起步——每一代人似乎都认为，继任者可用的工具会让他们变得软弱。

然而，我确实想知道这里是否有范式的转变。尽管我的“编程爷爷奶奶”手工设计出他们的算法，并反复检查它们，因为将它们具体化为穿孔卡片太昂贵了，尽管我的“编程父母”不得不专程去图书馆编程，尽管我在舒适的宿舍里做作业，但在每一代中，我们主要依靠自己的专业知识，辅以朋友的知识和课本。我们的功能越来越强大的工具提高了我们的效率，但同时也完成了同样的任务:将我们自己的想法传达给我们的计算机。

当代人可用的信息动力工具是另一种类型的。它们实现了一种新的编程形式:程序员作为一个管道，将其他人的想法传达给计算机。成为一个有效的渠道需要实践，正确区分好的和坏的内容，并将其融入他们的计划框架。这对新手来说是一项艰巨的任务。

# 结束语

没有人需要深入理解代码库的每个方面。抽象出细节是构建复杂系统的关键，这在每个工程项目中都很常见。机械工程师不需要了解系统中的每一个齿轮，电气工程师也不需要了解电路中每一个电阻的用途。同样，软件工程师不需要了解他们系统的每一个细节。我们构建库，给它们起好名字，使用设计模式构建它们，并将它们集成到越来越抽象的 API 中。

但是“互联网反模式”恰恰发生在你*需要了解你的系统的某个部分的细节的时候。当你发现自己不确定的时候，你必须决定:我是应该找别人帮忙，还是应该寻求更深入的了解？每条道路在适当的时候都是有帮助的。*

*我无意阻止一个有抱负的软件工程师使用互联网上的资源。有这么多免费的精彩内容，还有很多好心的工程师想分享他们的专业知识。但这些资源是一种“强力工具”。如果你知道如何使用它们，它们会帮助你。如果不这样做，可能对自己弊大于利。*