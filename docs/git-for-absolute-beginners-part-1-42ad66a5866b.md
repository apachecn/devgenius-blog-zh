# 绝对初学者的 Git:第 1 部分

> 原文：<https://blog.devgenius.io/git-for-absolute-beginners-part-1-42ad66a5866b?source=collection_archive---------24----------------------->

![](img/59afeeb6a92b956987a7755e85cdfe11.png)

[潘卡杰·帕特尔](https://unsplash.com/@pankajpatel?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

我的表弟最近开始制作一个令人印象深刻的 2D 游戏，在交谈中我意识到，尽管他以惊人的速度轻松完成了 GDScript，但他没有一个解决方案来版本化他的代码并在线备份。我决定向他介绍 Git，这是最常用的版本控制系统之一，并且在某个时候意识到没有任何好的资源可以缓解 Git 到底是做什么的概念。我回顾了我刚开始学习 Python 时，对如何使用 Git 只有模糊的想法，并意识到有抱负的开发人员可以使用一些帮助和高级解释(即开发人员行话中的 *simple* )。

# 流行语

如果你是一个刚刚涉足软件开发领域的人，你可能已经听说过 Git(T8)作为一个流行词汇，坦率地说，当你用 Java 编写你的第一批 Python 脚本或第一个小应用程序时，你将很难理解这有什么大惊小怪的。为了给你一个视角，现在想象你自己，两年、三年、五年、十年后，作为一个久经沙场的软件开发人员。

首先想象你正在秘密地独自创作你的巨著。煞费苦心地将一点一滴的代码组合在一起，这些代码将自动创建无人机，让你接管世界。唉，您意识到您刚刚更改的其中一个文件之前包含了一大块您只想压缩和优化的关键代码，但是现在您甚至不知道如何弄清楚原始代码块做了什么。原始文件将永远丢失。

时光倒流不是很棒吗？使用 Git 你可以…

但是现在想象一下，现在，你意识到你不能全靠自己。工作太多了，你需要有人帮忙。你和一个朋友合作，事情是这样的:

1.  你和你的朋友做一个安排，让我们称他为约翰，每天下午 3 点你们将把改变的文件的拷贝发送给对方，并且你们将想出如何整合这些改变。
2.  在工作的第一天，John 通过添加一个占用数百行代码的函数`take_over_world`来修改`very_important_script.py`。
3.  第二天，你发现这个函数写得相当糟糕，一些变量名可以被改变以使内容更具可读性，你还发现你可以只用一个而不是三个嵌套循环，这样可以节省计算时间。您根据自己的喜好更改`take_over_world`，并将文件的副本发送给 John。
4.  约翰打电话给你，询问文件:*我的三重循环在哪里？我在这个循环中引入了 300 条额外的线路，让我们可以在一周内接管世界！*你很困惑。很明显，你的解决方案在计算时间上更好，但是 John 声称他可以让这段代码比你的代码更快地达到你的共同目标。你让步，让他使用他的副本。
5.  第二天你从约翰那里得到文件，你意识到你改变了你的`semi_important_script.py`来反映你对`take_over_world`函数所做的改变。你想回到两天前的前一个版本，但是你没有办法做到。您忘记制作一份*以防万一*副本。您最终会从头开始编写与两天前相同的代码，这一次引入了几个讨厌的 bug。
6.  你和约翰之间的这种来回发送文件和长时间电话讨论变化的情况持续了几个星期。有一天你醒来，发现自己又回到了起点。还是你？你不确定。没有你可以查看的历史，没有发生的事情的记录，没有代码中谁写了哪个片段的标记。
7.  你接管世界的无人机自动化项目惨败。你还得为约翰的工作付钱。

看到了吗？在一个团队中工作会变得非常困难，即使只有你和你的朋友在没有合适工具的情况下努力工作。像 Git 这样的工具。

# 什么和为什么？

Git 是一个潜在的工具，可以让你减轻前面提到的大部分头痛。它是一个**版本控制系统**工具，可以让您:

1.  准确跟踪项目的变更和历史
2.  简化团队工作(记录谁写了什么，谁修改了什么)
3.  当你破坏了无法修复的东西时，恢复到旧版本的文件
4.  为你的工作创建不同的分支(分支和分叉，我们稍后会谈到，虽然不是很详细)
5.  可能的话，把你的代码备份到相关的服务器上，比如 GitHub(想象一下，如果你把你的巨著存储在你的驱动器上，而你的磁盘被擦除了，会发生什么…)

当然，还有其他工具可以进行版本控制。git 的一些替代品包括 Subversion 和 Mercurial。我鼓励你仔细阅读这些，看看你最喜欢哪一个，但是要知道，很多公司和开源项目都在使用 Git。

# 基础知识

首先也是最重要的:Git 背后的高层思想是什么？当您开始一个新项目或者已经有了一个想要用 Git 跟踪的项目时，您可以在那个项目的目录中运行`git init`命令。这将添加一个特殊的隐藏文件夹`.git`, Git 将在其中存储它的文件，允许它正常工作。

维护完整文件副本的无限链没有什么意义。有时这些文件会变得非常大，想象一下，当您必须将每次增量更改的每个副本保存到一个文件中时会发生什么。这就是为什么 Git 使用`diff` s 的原因，它只精确记录每个文件中相对于前一版本发生变化的部分。

默认情况下，Git 不会跟踪项目文件夹中的所有文件。你应该告诉它哪些人的历史应该被记录下来。您不希望在 Git 中包含自动生成的文件，也不希望包含对代码正常工作不重要的任何大型二进制文件。所以 Git 在默认情况下希望您明确地告诉它添加要跟踪的文件。这是如何工作的？看一眼:

![](img/3581930a5cb21869f2cdaabd6b625be8.png)

# `git add`

运行完`git init`之后，你通常会想要做`git add`来将特定的文件添加到所谓的**暂存区**或**索引**(这些名称可以互换使用)。这是 Git 中的一种状态，文件中的更改与工作目录中的更改是分开的。那是什么意思？想象你已经达到了指标，并且继续工作。如果您对`semi_important_script.py`引入任何额外的更改，除非您在这些更改之后再次运行`git add`，Git 将只关注那些已经被移动到索引中的内容。

# `git commit`

上述命令通常与下一个命令密切相关。虽然`git add`让您专门选择要跟踪的文件，但是`git commit`实际上从索引中取出所有文件，并告诉 Git: *这些是这些文件中的更改，将其添加到项目历史记录中*。你通常会这样做:`git commit -m "feature: added semi_important_script.py"`。在`-m`标志之后会出现一条消息，描述您所做的更改，这条消息将被添加到存储库的历史中。

现在，需要注意一件重要的事情，提交是 Git 的*单元*。每次提交东西时，Git 都会把它当作历史中的单步修改，所以一般建议尽量少提交，经常提交。不要像我们故事中的约翰那样写 300 行然后提交。写几个修改程序的小部分，然后立即提交。

# `git push`

“保存历史”路径中最后但同样重要的是`git push`命令。这个命令可以让你把你的代码发送到一个*远程仓库*，这是一个存在于某个服务器上的项目副本的花哨名字，通常为开发者提供良好的管理工具，比如 GitHub。`git push`将只发送以前提交过的文件/更改。因此，如果你独自工作，你通常应该把这个添加、提交、推送作为一个重复的循环。

# `git pull`

图中有两个额外的命令。先来说说`pull`。当您与团队一起工作时，或者只需将服务器上的更改同步到另一台计算机上的项目副本时，这将非常方便。`git pull`检索服务器上可能出现的任何可能的更改，并尝试将它们集成到您自己计算机上的项目副本中。

# `git clone`

该命令用于从服务器获取项目的全新完整副本，其形式如下:`git clone https://example.com/my_repo/`。与`pull`不同的是，这创建了项目的一个单独的副本，并且当你邀请其他人在你的库上工作或者当你想要编辑其他人的代码时，或者当你切换到一台新的计算机而不是用闪存驱动器复制你的项目时，你可以只`git clone`如果你在服务器上的库是最新的。

# 协力

![](img/2c44c039c513a142134a57669bbdfe4b.png)

我将在这里描述最基本的场景，因为团队中的人越多，你将不断学习新的东西。

1.  首先，假设:上图假设 Alice 没有项目的现有副本，而 Bob 有。因此爱丽丝不得不`git clone`储存库。
2.  接下来，Alice 介绍了一些更改，并希望将其交给 Bob。她执行通常的`git add`、`git commit`和`git push`操作，将它发送到存储库服务器。如果第三个人想要加入这个团队，他们现在可以`git clone`访问这个存储库，并且他们可以使用 Alice 所做的更改。
3.  鲍勃需要做`git pull`才能开始他的工作，以获得爱丽丝所做的所有更改。
4.  Bob 完成后，他还将他更改的文件添加到索引中，提交更改并将它们推送到存储库服务器。

# 冲突

现在，想象 Alice 和 Bob 都在修改`semi_important_script.py`中相同的代码。鲍勃住在夏威夷，爱丽丝住在俄亥俄州，所以他们并不直接知道他们每个人在做什么。

当他们都修改了同一段代码，但以不同的方式修改时，会发生什么呢？假设这个脚本包含一个简单的函数，他们都在自己的机器上修改了这个函数:

```
# Bob's variant
def add_two_strings(string1, string2):
    return str(string1) + str(string2)# Alice's variant
def add_two_strings(string1, string2):
		return int(string1) + int(string2)
```

这两个函数的行为完全不同:

1.  第一个*连接两个字符串*。如果你用`"1"`和`"2"`呼叫它，你将得到`"12"`。它只是把两根线混合在一起。
2.  第二个首先*将*每个字符串转换成一个整数，然后将这些整数相加。按照上面的例子，事情是这样的:

*   拿`"1"`拿`"2"`。
*   将`"1"`转换为`1`并将`"2"`转换为`2`。
*   这些现在是数字，所以它们将在数学意义上相加:`1 + 2`等于`3`。
*   返回`3`。注意是`3`而不是`"3"`，所以这次函数返回一个数字而不是一个字符串。

顺便提一下:如果你已经用 Python 编写了一些代码，你肯定会理解为什么这两个函数都很糟糕:例如，注意，当你将`"a"`和`"b"`作为参数传递给第二个函数时，将会抛出一个错误(想想:如何将字母转换成整数，这没有多大意义)。但是出于演示的目的，假设这两个是合法的，让我们考虑冲突的解决。

当两个变更不能被 Git 明确地合并时，冲突就是我们最终的结果。注意，当第一个函数将传递的值包装到一个`str`中时，第二个函数使用了`int`。在你告诉它之前，Git 不会知道实际上应该保留哪个变量。Git 会告诉你发生了冲突，在 Alice 和 Bob 的情况下，如果他们中的任何一个试图将更改推送到服务器并在那里遇到另一个变体，Git 会相应地修改文件以帮助你解决冲突。假设 Bob 先推，Alice 试图推她的版本。然后，`semi_important_script.py`会有这样的东西:

```
def add_two_strings(string1, string2):
<<<<<<< HEAD
	return int(string1) + int(string2)
=======
	return str(string1) + str(string2)
>>>>>>> master
```

看着吓人？再看一眼！`HEAD`指的是爱丽丝在她机器上的*最新*变化。整个块基本上说的是`master`分支上的变化(之前由 Bob 推动)与`HEAD`中的变化相冲突。

那么你如何解决这样的冲突呢？在理想的情况下，Alice 应该尝试与 Bob 交流，询问使用`str`的意图是什么，或者至少调查提交的历史，看看 Bob 是否在某个地方留下了他为什么使用这种方法的消息。实际上，为了消除冲突，Alice 有三个选择:

*   保留她的版本并覆盖鲍勃写的版本:

```
# Alice deletes the commented-out lines in this scenario def add_two_strings(string1, string2): 
# <<<<<<< HEAD
   return int(string1) + int(string2)
# ======= 
#   return str(string1) + str(string2) 
# >>>>>>> master
```

*   保留鲍勃的版本，放弃她自己写的版本:

```
# Alice deletes the commented-out lines in this scenario def add_two_strings(string1, string2): 
# <<<<<<< HEAD 
#   return int(string1) + int(string2) 
# =======
   return str(string1) + str(string2) 
# >>>>>>> master
```

*   保留两个更改(这通常需要一些适当的重构，例如保留两个函数，但更改其中一个函数的名称):

```
# Alice modifies the code, for example like this: def int_add_two_strings(string1, string2):
   return int(string1) + int(string2) def str_add_two_strings(string1, string2):
   return str(string1) + str(string2)
```

在最后一个场景中，如果函数被重命名，需要做更多的工作。在函数调用发生的任何地方，也需要使用正确的名称。但有时保留两种变体是有意义的。Alice 可以编写一个函数闭包，她可以与 Bob 联系，看看是否可以将其压缩成一个使用类型检查并具有一致行为的函数…这里真的有很多很多选择。

# 离别留言

希望这篇小文章能让您看到在日常的新手程序员生活中使用 Git 的强大之处。我还希望，随着您越来越深入地研究版本控制，您可能会感到的轻微威胁会逐渐消失。我在这篇文章中使用了许多简化方法，虽然实际情况最终可能会变得更加复杂，但是作为一个初学者，你应该会发现这些技巧中的大部分对你来说已经足够了，但是我希望听到一些反馈！可能有你觉得应该出现在这篇文章里而你没有发现的话题。也许你觉得这篇文章的分量一下子太重了，那就随便指出来吧。对我来说，可能很难为初学者提出最终的建议，因为我是一名专业的软件开发人员，可能会低估或高估某些元素的重要性。这篇文章本质上是几年前我还是个菜鸟时就想听的事情的产物，也是我表弟 Philip 在我给他上第一堂 Git 课时指出的有点令人困惑的事情的产物。因为没有人是一成不变的，所以我希望看到你们认为应该为完全的 Git 初学者撰写的一系列文章。我认为不能低估这样一个事实，了解 Git 只会让软件更加一致和结构化。