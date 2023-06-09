# 如何优化你的项目和团队

> 原文：<https://blog.devgenius.io/how-to-optimize-your-project-and-team-a5703fb2935a?source=collection_archive---------18----------------------->

![](img/273718433423748afa3e91f4262087e7.png)

# 目的

我最近分配的项目有许多问题，尽管我们的团队成员尽了最大努力，花了很多时间来解决这些问题。一个大问题是没有足够的时间来处理这个项目，因为我们的团队成员同时有几个项目(2 或 3 或更多)。然而，我认为如果我们优化我们的项目，我们可以避免花费大量的时间(甚至超过 8 小时)。此外，我猜几乎所有的项目都没有足够的资源。所以，我会和你分享我的反思点来优化你的项目。在我的例子中，我使用了 react，所以我特别关注 React 项目。但是，如果您不是 react 用户，这篇文章会很有帮助，因为有些反映点是一般性的。

# 我的思考点和如何改善一个项目管理。

*   在开始开发之前，确定“核心”设计并准备澄清文档。

实际上，当我分配这个项目时，“核心”设计还没有确定。是的，有很多文档，但几乎所有的都像垃圾一样，因为“核心”设计没有固定。一位项目经理说:“这个项目将是灵活的，因为我们为当前项目引入了‘敏捷方法’,所以我们不需要现在就修改设计，因为这个设计将通过与客户的讨论而改变。”

啊，我能理解他说的话。然而，这是完全错误的，因为“敏捷方法”并不意味着允许我们不做任何决定。至少我们需要在一开始就准备好固定的或理想的设计，以及基于这个固定的或理想的设计的固定设计。否则，我们需要一次又一次地修理，浪费时间。

*   从头添加分支管理。

一开始，我们只为一个人创建了一个分支机构(比如 dev-〇〇).这对于立即合并非常有用，但是有很多回归。当另一个成员合并一些代码时，我的代码意外地消失了。尽管有一些回归的原因，在我的例子中“我们可以立即合并，有时两个人同时合并”“当有人合并开发分支时，我们需要拉开发分支。但在我们的情况下，这不是强制性的”。当我们处理回归问题时，我们需要花费大量的时间来研究和浪费时间。所以一开始就需要“feature/…”“bugfix/…”这样的分支管理。这不仅有助于防止回归，还可以方便地检查过去的代码。如果我们不引入分支管理，我们需要阅读整个提交注释来检查过去的代码。然而，如果我们引入分支管理，我们只需要检查“分支名称”,这对节省我们的时间很有用。

*   花很多时间设计组件结构

正如我上面所说的，我们的项目是从“敏捷方法”开始的，并没有决定重要的设计。

此外，XD 设计不是合适的组件设计，因为所有的按钮设计都有点不同。

因此，我们没有仔细考虑组件设计就开始了我们的项目，但这是完全错误的。因为如果我们没有“公共”组件，我们需要在许多具有相似结构的组件中更改大量代码。这需要很长时间来实现。因此，我们需要创建一个完整的组件，并对此进行讨论。

*   花大量时间选择图书馆

对于 react 或者 Js 框架，有很多库。这是非常有用的，但是如果我们有很多需求，我们不应该从易于实现的角度来决定一些库。起初，这个决定节省了我们的时间，但是如果我们想要添加一些新的需求，而我们使用的一些库没有道具来实现这些新的需求，我们需要自己创建这些特性。事实上，这是不可避免的，但我们需要更多的时间来讨论我们应该使用哪些库。此外，如果我们使用一些库并发现一些错误，这些错误有时很难修复，因为基本上这些库有许多彼此相关的代码。有时候我们可以找到一些讨论来修复这些 bug，但这并不是每次。

*   更深入地了解客户需求

我现在的项目经理经常说“一个客户希望我们实现‘基本’功能和设计”。他说的听起来是显而易见的，但什么是“基本特征”呢？我们不需要实现任何 css 吗？哪个特征或点更重要？虽然我问他，他没有任何明确的答案，但我需要一次又一次地问他，因为时间有限。

基本上，应用程序一开始并不完美，所以我们需要决定“在这个服务或项目中，应用程序的重要点是什么？”

*   不要创建大量文档

如果我们创建许多文档，这看起来不错，但那是完全错误的。因为如果有很多文件，包含不同的信息，这是非常混乱的，每次都要花时间检查。理想情况下，我们只有一个文档，并在一个文档中安排所有信息。

# 结论

正如我已经说过的，几乎所有的项目都没有足够的团队成员和时间，所以我们需要在一开始就决定什么应该做，什么不应该做。我认为“准备”是最重要的，因为一旦我们开始，就很难停下来安排我们的项目或组件设计。

这些思考点对我很有帮助，但我希望对你也有帮助。

# 感谢您的阅读！！