# Git 教程:5 分钟学会 Git 分支

> 原文：<https://blog.devgenius.io/git-tutorial-learn-git-branching-in-5-minutes-cf2c01f63a5?source=collection_archive---------2----------------------->

![](img/1ef2c4253a95b69303779ffb16b8093f.png)

Git 是使用最广泛的版本控制系统之一，是每个开发人员都应该知道的重要工具。Git 最大的好处之一是它的分支能力。Git 分支是版本控制工作流的一个基本方面。今天，我们将讨论如何创建、删除、合并和重置 Git 分支。之后，我们将介绍您可以采取的进一步发展 Git 知识的后续步骤。

**我们将介绍**:

*   什么是分支？
*   创建分支
*   删除分支
*   合并分支
*   重建树枝基
*   接下来要学习的 Git 概念

# 什么是分支？

想象一下，你正在和你的团队一起做一个项目，你正在创建一个需要对代码库进行大量修改的新特性。在这个过程中，您发现了一个需要修复的 bug。这个 bug 与你的新特性有关，你不想影响你的代码。这种情况可能会变得复杂。你将在哪里存储你一直在工作的代码？

这就是 Git 分支出现的原因。分支是源代码控制的一个核心概念，它允许你将你的工作分成不同的*分支*，这样你就可以自由地处理你的源代码，而不会影响其他人的工作或者主分支中的实际代码。

使用 Git，您从一个名为 *main* 的主分支开始。Git 允许您创建任意多的分支。

> ***注意*** *:你不必总是从主分支创建分支。您可以从任何其他分支创建新分支。*

在你独立的分支中，你能够在不直接影响你的源代码的情况下进行实验和测试。分支**允许你和你的团队在上下文之间切换，而不用担心影响不同的分支**。对于团队来说，这是一个很好的工具，因为它使协作更加容易、方便和灵活。

> ***注*** *: Git 分行与 SVN 分行不同。Git 分支在您的日常工作流程中非常有用，而 SVN 分支则用于大规模开发工作中。*

# 创建分支

**本地分支机构只能在您的物理设备上访问**。在将分支推送到远程存储库之前，您需要首先创建一个本地分支。

如果你已经有一个本地分支，你可以使用`git checkout`:

```
git checkout <name>
```

如果您还没有所需的分支，可以像这样创建一个新分支:

```
git checkout -b <name>
```

现在我们知道了如何创建一个新的本地分支，让我们来看看如何创建一个远程分支。

# 创建远程分支

**您可以将本地分行推送到远程回购，它将成为远程分行**。当一个分支是远程分支时，这意味着任何可以访问远程存储库的人现在都可以访问远程分支。

如果您想将本地分支推送到远程回购，您可以使用`git push`:

```
git push -u origin <name>
```

# 删除分支

现在我们知道了如何创建本地分支和远程分支，让我们学习如何删除它们。我们将从使用`-d`标志删除一个本地分支开始:

```
git branch -d <name>
```

有时，Git 拒绝删除您的本地分支。当您的分支有尚未合并到其他分支或推送到远程存储库的提交时，就会发生这种情况。这种拒绝是为了防止您意外丢失数据。

如果你确定要删除你的分支，你可以使用`-D`标志。此标志强制删除。

```
git branch -D <name>
```

# 删除远程分支

要删除一个远程分支，您可以使用`git push`命令:

```
git push origin --delete <name>
```

# 合并分支

Git 合并是分支的一个基本功能。合并**允许你通过提交**加入两个或更多的分支。只有目标分支被改变。在我们的例子中，这将是主分支。**特征分支的历史被保留**。

让我们回想一下你和你的团队正在开发的功能。您的整个团队都可以访问您上传到远程存储库的主分支。您正在对特性进行小的修改，并且您不希望您的工作影响主要分支。

您可以创建自己的分支来试验和测试您的更改。一旦完成并测试，您可以将该分支合并到主分支中，这样每个人都可以访问它。

在我们的场景中，假设您想要将名为`myfeature`的实验分支合并到主分支中。在合并之前，您应该做一个`git fetch`来收集关于远程存储库的最新信息。

```
git fetch --all
```

然后，进入您想要合并变更的分支，执行`git checkout`。

```
git checkout main
```

现在，你可以将`myfeature`合并到主分支中。

```
git merge myfeature
```

您可以在存储库中检查项目的提交历史来验证合并。如果您的合并是成功的，并且您在`myfeature`上的工作已经完成，那么您可以删除那个实验分支，因为所有的变更现在都已经集成到主分支中了。

# 重建树枝基

Git rebase 是 Git 中的一个高级概念。这可能看起来有点复杂，但我们会复习基本知识。重置基础和合并非常相似。两个选项**都从一个分支获取提交，并将它们放到另一个分支**。

重定基础和合并的主要区别在于**重定基础将工作从特征分支转移到主分支**后，会删除特征分支的历史。一些开发人员更喜欢这种方法，因为它确保了一个简单的审查过程。

下面是如何使用 rebase:

```
git checkout myfeature
git rebase main
```

# 接下来要学习的 Git 概念

祝贺您迈出了 Git 分支的第一步！许多团队使用 Git，所以很好地掌握控制系统及其特性是很重要的。关于 Git 还有很多需要学习的地方。接下来推荐的一些概念包括:

*   樱桃采摘
*   高级 git 存储库操作
*   拉取请求
*   Git 命令

*快乐学习！*