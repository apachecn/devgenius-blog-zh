# 为什么开发人员更喜欢添加代码而不是删除代码？

> 原文：<https://blog.devgenius.io/why-developers-like-adding-code-more-than-removing-it-18519952486a?source=collection_archive---------7----------------------->

## 添加代码比删除和简化代码更容易

![](img/75dfcc926881855355078e6301010d23.png)

[stux](https://pixabay.com/images/id-3155663/)

> 我最有效率的一天是扔掉了 1000 行代码。肯·汤普森

开发人员更愿意添加代码而不是删除代码，但是这种偏见增加了更多的错误和复杂性，这是为什么呢？

这篇文章[在解决问题时，加法比减法更受欢迎](https://www.nature.com/articles/d41586-021-00592-0)给人们解谜，并发现增加组件来解决问题比移除组件来解决问题有偏见。

人们会添加一个组件，即使如果他们删除一个组件，最终的解决方案会更简单、更有效。

> 亚当斯等人证明，他们的参与者提供如此少的减法解决方案的原因不是因为他们没有认识到这些解决方案的价值，而是因为他们没有考虑这些解决方案。事实上，当指令明确提到减法解决方案的可能性时，或者当参与者有更多的机会思考或实践时，提供减法解决方案的可能性就会增加。因此，人们似乎倾向于使用“我们可以在这里添加什么？”启发式(简化和加速决策的默认策略)。这种启发可以通过施加额外的认知努力来考虑其他不太直观的解决方案来克服。"

有趣的是，人们选择添加东西，即使删除会更简单，需要维护的项目更少。

# **代码少，问题少**

> “编写速度最快、从不中断、不需要维护的代码行是您永远不必编写的代码行。”史蒂夫·乔布斯

添加代码花费的精力更少，风险也更低。要更改和删除现有代码，您必须了解代码和系统中的任何相关代码。如果您添加代码，您需要对代码如何工作有一个粗略的概念，但要了解您的更改。如果它不起作用，您可以删除您的更改，让代码保持原样。

[最好的代码是根本没有代码](https://blog.codinghorror.com/the-best-code-is-no-code-at-all/)

# **切斯特顿之门**

开发人员同样偏向于添加代码，而不是删除代码或使代码更简单。如果您通过重构和删除不需要的代码来更改现有的代码，您必须理解这些代码是做什么的。当删除代码时，考虑[切斯特顿栅栏](https://fs.blog/2020/03/chestertons-fence/)。

> 在这种情况下，存在着某种制度或法律；为了简单起见，让我们说一个横跨马路的栅栏或大门。更现代的改革家兴高采烈地走上前去说，“我看不出这有什么用；让我们清除它。”对于这个问题，更聪明的改革家会很好地回答:“如果你看不到它的用处，我当然不会让你把它清理掉。走开想一想。然后，当你能回来告诉我你看到它的使用，我可能允许你摧毁它。”切斯特顿

你需要理解为什么有人写代码，在你删除它之前它是做什么的。我见过很多糟糕的代码被重构，后来发现代码被添加是为了修复一个 bug。

我们知道，一个完整的解决方案要复杂得多，开发人员在删除部分解决方案之前需要理解它。

# **评论**

开发人员可以通过做出改变并留下评论来解释来对冲他们的赌注。这是一个给切斯特顿的栅栏增加一个路标的尝试，这样人们就知道栅栏是用来把人挡在外面还是把动物关在里面。

这似乎是一个好主意，除了它增加了维护开销，因为现在注释和代码必须保持同步。代码或注释经常被更改，但并不总是两者都被更改。现在你有一个困惑的问题。

> 如果代码和注释不匹配，可能两者都不正确。诺姆·施莱尔

添加注释增加了复杂性，当阅读代码和注释时你需要决定

*   你理解评论吗？
*   你懂密码吗？
*   注释与代码匹配吗？如果不是，哪一个是正确的？

如果注释和代码不匹配，你必须找出它们不同步的原因。更好的解决方案是给代码命名，这样它做什么就很明显了。

[代码应该是真相的一个版本，不要加注释](https://medium.com/dev-genius/code-should-be-the-one-version-of-the-truth-dont-add-comments-b0bcd8631a9a)

# **简化**

> “简单是最复杂的”莱昂纳多·达·芬奇

删除代码并通过减法使代码更简单是有好处的。每一行代码都必须维护，并且有可能包含错误。您需要维护的代码越少，解决方案就越简单。

使用单元测试删除代码更容易，因为您可以确认没有破坏任何东西。当你删除代码时，你降低了复杂度——为什么代码复杂度很重要。修剪和精炼代码需要更多的时间，但是[简单的代码值得花时间去创建](https://thehosk.medium.com/good-code-is-like-underwear-e0a9697f8531)

> 有时候，周一呆在床上比花一周的时间调试周一的代码更划算。克里斯托弗·汤普森

每当你碰到一行代码，你可能就已经破坏了它。很多次我只是读了一行代码就破坏了它:-) [#HoskWisdom](https://twitter.com/hashtag/hoskwisdom?lang=en)

# **你可能喜欢的其他帖子**

*   [我们如何尝试加快 IT 项目的速度，为什么行不通](https://thehosk.medium.com/how-we-try-to-speed-up-it-projects-and-why-it-doesnt-work-ca3bdc5d7413)
*   [开发人员愚蠢的十大普遍法则](/the-10-universal-laws-of-developer-stupidity-ccda23e91ee7)
*   [不要只考快乐路径](/dont-just-test-the-happy-path-e3fd565bad53)