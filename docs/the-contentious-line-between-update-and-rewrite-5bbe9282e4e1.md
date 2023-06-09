# 更新和重写之间有争议的界限

> 原文：<https://blog.devgenius.io/the-contentious-line-between-update-and-rewrite-5bbe9282e4e1?source=collection_archive---------3----------------------->

困扰工程师几十年的软件问题。

![](img/1c392e49b663058929fb377602008a7e.png)

照片由来自[佩克斯](https://www.pexels.com/photo/man-in-white-shirt-using-macbook-pro-52608/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)的[蒂姆·高](https://www.pexels.com/@punttim?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)拍摄

# 代码中的一行

当谈到遗留产品时，在软件工程的世界里有两种类型的人——那些准备重写的人和那些不准备重写的人。

有时候，人们，在这种情况下通常是经理，只想坚持到底，直到可能发生的事情发生，并继续修补，直到他们剩下的软件相当于忒修斯的[船](https://en.wikipedia.org/wiki/Ship_of_Theseus)。

让我们简单地谈谈重写的利弊，并理解为什么“渐进式重写”从来都不是一个好主意。

# 年龄和经历

老化的软件通常缺乏文档和开发经验，这通常是由于文档实践不充分以及随着时间的推移不同代的开发人员在产品上工作的结果。

我可以写一整部小说来描述文档如何以及为什么经常跟不上软件开发，但是根据我自己的经验，这通常可以归咎于分配给这个过程的时间不够。这主要是由省钱的短期收益驱动的，而长期的代价是没有人知道它最终是如何结合和运作的。

另一个常见的问题是，确实存在的文档通常很少被审查，一个开发人员可能认为是全面且易读的摘要对另一个开发人员来说可能是完全的天书。

通常，在技术经验方面具有不同背景的开发人员，以及不同的口语，将随着时间的推移从事一个产品的工作，并且产生的文档将反映这一点。一些最令人困惑的方面可能是模糊性和对先前领域知识的假设。

项目计划时间不足也可能是一个主要因素，特别是在匆忙进行 MVP 和一些最近的软件开发“方法论”所提倡的快速而有些杂乱的增量开发过程中，比如敏捷。

> 事实上，我还没有看到任何敏捷驱动的项目将合适的“文档时间”纳入他们的时间表。
> 我们不要过多地抨击敏捷，它太容易成为目标。

不充分的规划和轻率的分割开发会导致平台和技术的错误选择。不仅仅是因为不充分和迅速过时的文档而丢失了细节，而且技术债务的负担会呈指数增长，直到项目最终慢慢停止。

# 引爆点

在大多数软件产品的生命周期中(如果它们存在足够长的时间，这就是我们正在讨论的)，将会有一段时间，与持续更新的软件相关的知识会丢失，同样，底层平台和技术已经发展到产品感觉陈旧、缓慢和过时的程度。

正是在这一点上，人们开始提出关于更新现有代码库的问题，以迎合新的底层平台、后端系统或更现代的软件技术和实践。

最终有三种方法可供选择，

*   尝试按原样更新现有软件
*   将现有的软件分解成更小的独立(读取、解耦)模块，并尝试渐进式重写
*   从头开始重写整件事

在这一点上，项目经理和以上级别的人会因为宁滨的“工作”软件产品的建议而陷入恐慌，并且一提到“重写”这个词就浑身发抖。(我甚至大胆猜测，在他们眼前会出现舞动的美元|欧元|英镑的小符号！)

需要慎重考虑的是以下几点。当你考虑下一步该做什么，或者关键时刻你站在哪一边时，问自己以下问题。

有人知道它是如何工作的吗？

现有的开发人员知道软件是如何工作的吗——他们花了足够的时间来真正理解正在发生的事情吗？是否有任何文档，它处于什么状态，需要多长时间才能让它进入可以被正确理解的可用状态？

如果要更新，那么需要由既有知识又有能力的人来进行更改，并且并行编写新的评审文档以供将来使用。

**有人知道语言/平台/框架吗？**

有没有开发人员掌握当前实现的技术——如果没有，是否值得让新成员加入或培训团队中的现有成员？

> 如果是 Fortran⁴，但不是绝对必须，也许你可以迁移到 python——不是因为它主要是现代的，而是因为它目前在社区中有更多的支持和知识。

**当前的语言/平台/框架还有用吗？**

时代变了，新的需求出现了，新的技术出现了。如果产品以陈旧的语言和过时的方法进行编码，不知什么原因，在这里我会想起 Java ，以及它在抽象方面常见的令人痛苦的过度工程化，是值得[对本质上已经是一匹死马的](https://idioms.thefreedictionary.com/Flogging+a+Dead+Horse)进行鞭笞，还是该彻底放弃它将不可避免地带来的所有潜在好处了？

例如，考虑十年前的 [JSON](https://en.wikipedia.org/wiki/JSON) 解析库或基于网络的 API，以及现代实现可能干净和高效得多。现成的就拿一个，经过验证和测试，不需要[重新发明](https://idioms.thefreedictionary.com/reinvent+the+wheel)。可能是因为许多促使我们考虑重写的问题都源于陈旧过时的库，而这些库已经不再适用。

另一个例子可能是从过时的遗留抽象重语言(如 Java)转向现代的严格类型化的圆滑语言(如 [Swift](https://swift.org) (抱歉，忍不住了，我会试着停下来)。这将带来更好的实现便利性、更广泛的开发人员人才库，以及许多内置的可防止大量运行时错误的编译检查。

# 敲竹杠，摘水果

考虑到前面的几点，通常会建议一种“渐进重写”的策略，以尝试保留尽可能多的原始产品，并且仅更新被认为会引起问题或者可以以最小的努力提供最大增强的部分。

在管理层发言中，他们称之为“大赚一笔”或“尝试一下低调的 fruit⁵'”——但从未考虑到了解产品的运作过程中所付出的努力，而这种努力足以做出最初被认为是简单的改变。

以我个人的经验来看，过时的软件产品往往要么是原始代码的铁板一块，要么是直接从⁶'.的一本关于“[模式”](https://en.wikipedia.org/wiki/Software_design_pattern)的教科书中抽象出来的高度耦合的老鼠窝

> 对这些规范进行修改需要高度的理解，这有点像在世界杯决赛点球大战中拆除一颗未爆炸的二战炸弹，这颗炸弹牢牢地嵌入了一个已爆满的足球场的地基中。

这就是权衡取舍的地方——理解代码和随后尝试安全解耦(以及测试它是否仍然工作)所花费的时间当然，我们都要测试，对吗？)甚至在做出改变变得有价值之前？

如果这样做了，并且成功了，那么还需要多长时间才能做出进一步的改变，直到不可理解的东西出现或者技术的限制(如我上面提到的平台、语言、框架)成为可扩展性的硬限制？

在几乎所有的情况下，我都会投票反对渐进式重写，除非由于诸如遗留的不可替代的硬件等小环境的限制，这是绝对不可能的。即便如此，迟早，这颗[子弹还是要被咬](https://idioms.thefreedictionary.com/bite+the+bullet)。

# 一个勇敢的新世界

对重写的反对通常是基于成本，反对者通常是管理层，但有时开发人员也会保持沉默——尽管我认为这是因为他们不愿意相信自己的能力，而不是其他能力。

至少在我看来，没有一个软件是不可替代的，也没有一个软件系统会无限期地工作。

重写优于更新和渐进重写的优点可以总结如下。

**彻底决裂**

这是一个用最美妙的天赋，后见之明，从限制技术中继续前进的机会。从当前的实现中吸取教训，如果不容易加入变化和特性，那么就转移到更好的、更现代的技术上去。

**吸取的教训**

从原来的、现在已经过时的、笨重的产品中获得的经验是一个很好的礼物，可以构建一个新产品来解决其缺点并确保其未来的可扩展性。

原始的、不再相关的需求可以被抛弃。为了长期维护和更新，可以适当地记录、设计和实现新的需求。

**文件 FTW**

一个适当的、清晰的、明确的和易于遵循的文档计划可以着手进行，使得将来完全重写的需要变得不太可能。

将为足够的细节分配时间，并将对其进行审查，以便团队和其他不直接参与项目的开发人员都可以理解。我真的不明白为什么这不是主流。

**解耦！**

正如我前面提到的，遗留代码库和产品倾向于高度耦合，不仅在它们自身内部，而且与相关的实体，比如数据库，高度耦合。

![](img/565182427e850cc3bf7f0f63d9b5f433.png)

照片由来自 [Pexels](https://www.pexels.com/photo/white-gallon-ship-746645/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) 的 [GEORGE DESIPRIS](https://www.pexels.com/@george-desipris?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) 拍摄

为此，可以构建一个更加模块化和分离的系统，其中组件可以通过设计而不是通过需求来换入换出。

定义一个严格的、可扩展的、版本化的 API，并坚持使用它。

一艘现代的忒修斯号[船，如果你愿意，但不是一艘由于疲劳和低效而不断更新的船——一艘可以不断更新以不断提高效率和性能的船。一艘能够快速巡航，胜利作战，最重要的是当它驶出干船坞时不会沉没的船。](https://en.wikipedia.org/wiki/Ship_of_Theseus)

# 为正义而战

经理们经常说，开发人员只是对最新的技术或最酷的语言感兴趣，这通常是为了阻止开发人员对软件重写的傲慢态度。

我会反驳说，我们对新奇事物的兴趣是极其重要的，因为这是任何有足够能力、经验丰富和现实的开发人员的工作，以他们详细的知识推动变化。

为改变而改变对我们没有好处，如果你的团队中有开发人员一直这样做，那么你需要重新审视你的招聘流程。

我们喜欢写软件，但是我们喜欢制作伟大的软件——这就是我们参与游戏的原因。

让我们做我们的工作，你会惊讶的。

[1]:我不是在谈论制表符对空格或者 [vim](https://www.vim.org) 对 [emacs](http://www.gnu.org/software/emacs/) ，让我们现在不要去那里。嗯，每个人都知道 spaces 和 vim 是任何有效的软件工程师的最佳途径，对吗？
【2】:至少在侦探工作上没有重大投入。
【3】:我不是粉丝，你也知道。与其说是因为核心方法本身，不如说是因为它确实有一些优点，但主要是因为围绕它为追随者建立的整个不必要的寄生生态系统。
[4]:就我个人而言，我不会从 Fortran 迁移到 Python，因为我真的很喜欢 Fortran，而且它确实如我所言——但我觉得对于年轻一代来说，这是一个他们会欣赏的好例子。
【5】:我从来没有真正理解过“低挂水果”,因为我认为它们不是最美味、最容易拿到的，而是最有可能是其他人(和所有动物)已经啃过的，所以实际上有点脏，因此是二手的。
【6】:模式，这样一个有争议的问题。我的意思是，我们都在使用它们，却不知道你会不会故意按照一种模式编码。看看在 Java 中发生了什么？啊，我又做了。抱歉。