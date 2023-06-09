# 您可能希望切换到 NoSQL 数据库的 3 个原因

> 原文：<https://blog.devgenius.io/3-reasons-you-might-want-to-switch-to-a-nosql-database-1b0f19f5119?source=collection_archive---------1----------------------->

![](img/aba9ec8239e39f6d186a498faf309a04.png)

大多数开发人员都熟悉关系数据库管理系统，如 SQL Server、MySQL 和 PostgreSQL，这主要是因为它们已经成为行业标准几十年了，拥有相对良好的记录和较大的市场份额。

在我们数字时代的大部分时间里，存储成本都被限制在较高的水平。你不能只是一时兴起储存 10 亿张唱片，然后抱最好的希望。关系数据库通过减少重复数据和构建限制内容大小的严格模型来帮助减少这一开支。至少在标准化良好的数据库上是这样。

但现在是 2021 年，我们(大多数人)不再需要担心这些事情。GB 的价格便宜，带宽充足，所以我们现在可以选择替代的存储机制，这实际上可能比旧的方式更有益。

# 我为什么要换

我目前在一个共享服务器上运行我的博客(【www.thatsoftwaredude.com】T2)，我的大部分数据存储在一个关系数据库中。这是我在学校学到的，也是我的大多数雇主多年来一直使用的。因此，通常情况下，建立一个模式并编写一些代码来连接所有东西是一件很容易的事情，而我现在可以相对快速地完成它。

但是有一些问题。老实说，总有一些问题我只是简单地解决或者忽略，因为我无能为力。但是最近，当我的网站在一天中的大部分时间里关闭，我坐在那里一遍又一遍地重启应用程序池时，我意识到我需要改变。有什么问题？

嗯，是数据库。更具体地说，我开始达到服务器允许的大小限制。我还没到那一步，但已经很接近了。太接近了，以至于数据库崩溃了，所有东西都跟着崩溃了。我备份了我的数据，基本上只是删除了我能找到的最不重要的记录。但是，我不能批量删除，因为事务日志已经满了。所以我慢慢地坐在那里，一大块一大块地删除我网站上的神经元，直到它恢复到足以恢复生机。

我可能已经解决了这个问题(今天)，但它会回来。在这一点上，我是在拖延时间。因此，我开始寻找存储数据的替代方法，而不是以更高的成本寻找存储容量稍大的升级服务器。

这就是为什么 NoSQL 现在对我有意义。

# 3.提供灵活性

我的关系数据库面临的最大挑战是它不完整。我的博客大约有 7 年历史了，并且是一个持续发展的作品。我一直在添加、删除和更新内容，这意味着曾经设置为 200 个字符的列现在需要超过 1000 个字符，甚至设置为 max 以消除任何限制。

一旦我更新了数据库，我通常需要更新我的代码。数据模型和 DAL(数据访问层)需要与新的模式相匹配。所以从资源和时间的角度来看，它是昂贵的。如果我使用的是像 Entity 框架这样的对象关系映射框架，那么默认情况下，大部分工作都是为我处理的。除了我不是，因为许多原因将在未来的帖子中讨论。

不过，通常情况下，如果不删除整个数据库表并重新构建它，我就无法进行模式更新。我甚至可能需要 DBA(数据库管理员)来进行我认为简单的数据库更新。这将取决于权限和数据库中当前的数据。

因为 NoSQL 数据库不依赖于预先确定的模式来保存数据，所以我不必担心这一点。我可以简单地存储带有新属性的新对象，并在知道数据保存得很好的情况下继续我的工作。然后，我可以编写适当的代码来适应这种新的数据模型，从而将责任转移给程序，我实际上发现这样更自由。

这也意味着我不再需要像现在这样处理截断错误。7 年前当我建立数据库时，我犯了错误。我将列大小设置得太小，没有考虑任何类型的增长。这些错误现在是一个问题，因为用户的联系信息经常会达到一定的文本限制，中途被切断。

如今，灵活性正变得越来越重要。

# 2.对程序员来说更容易

我首先要说的是，建立一个 SQL Server 数据库，创建列，创建外键，创建索引，然后创建 DAL(数据访问层)是一项重复的枯燥任务，但是必须完成。

通常，在关系数据库中，必须首先开发模式(如上所述)。一旦达成一致，开发阶段就开始了，在这种情况下，你要尽可能地按照数据库模型编写类、对象等代码。这个阶段容易出错。通常，数据库中的数据类型与您正在使用的编程语言并不完全匹配。在测试和调试方面，开发人员需要做更多的工作来确保数据的完整性。

以像 MongoDB 这样的文档风格的 NoSQL 数据库为例，它将数据存储在 JSON 风格的对象中。因为数据已经是一种程序员友好的格式(JSON)，所以您不必构建任何形式的中间件层来将数据库数据转换为客户端数据，而对于关系数据库，我往往必须这样做。这通常被称为数据访问层(DAL ),在我作为软件开发人员的大部分职业生涯中，维护这些代码是很重要的一部分。

例如，如果我的数据像下面这样存储在 NoSQL 数据库中:

```
{fname: 'Bob', lname: 'Smith', ID: 2342}
```

响应一到达客户端，我就可以开始使用数据了。我不必转换数据类型来匹配我的代码。例如，在 SQL Server 中，您可以将一个值存储为一个*位*，这实际上意味着 1 或 0。然而，在 C#中，*位*的默认转换是布尔值(真或假)。我知道这一点，因为我用 C#工作了多年。但是一个新接触这门语言的人可能很难弄清楚他们的*位*去了哪里。

NoSQL 数据库拉近了数据库和代码之间的距离，这实际上意味着更少的错误代码和更高的可靠性。

# 1.可量测性

使用 NoSQL 数据库的最大好处之一是，它们本质上是为向外扩展而不是向上扩展而设计的。我这么说是什么意思？以传统的 SQL Server 数据库为例，基于服务器本身，您会受到资源的限制。例如，在特定服务器上运行的数据库可能只有 10GB 的存储空间，当达到极限时，通常会出现问题，我的博客就是这种情况。

然而，使用文档风格的 NoSQL 方法，您可以根据需要扩展存储，而不必重新配置服务器。想想你电脑上的文件。你可以创建文件并将其存储在硬盘上，如果你需要更多空间，你可以简单地在云上扩展存储或使用拇指驱动器。您将不必重启机器或更新操作系统或任何其他破坏性任务。

随着我的流量逐年增加，这对我来说变得越来越重要。任何形式的停机通常都不是什么好事。但是几个小时的停机时间和一天内数千次的页面浏览，可能会造成。这在共享服务器上尤其明显，在共享服务器上，其他应用程序同时运行，共享有限的资源。我不能简单地剥离一个新的数据库，然后从我停止的地方继续下去。

看起来 NoSQL 足够灵活，可以为我减少或完全消除这个问题。至少，这是希望。为了实现转变，我还有很多工作要做。首先，我必须将我的数据转换成适当的格式，然后将其迁移到新家。如果进展顺利，我就必须构建一个新的 DAL，这样我的服务器端代码就可以访问数据，最后重新创建几年的查询。

不用说，是工作。但是我在这里列出的每一个好处都将为我节省时间和精力。老实说，我不知道实际的好处是否会像我在这里所说的那样明显。但如果我从不尝试，我怎么会真正知道。

最后，我想说 SQL 数据库在软件工程中仍然很重要。他们有几十年的工作经验，还有成千上万的开发人员和他们一起工作过，比如我自己。但随着技术的快速变化和创新，有替代品可以填补它的不足是一个巨大的好处。