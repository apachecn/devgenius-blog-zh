# 内存仓库:一个被遗忘的设计工具

> 原文：<https://blog.devgenius.io/in-memory-repositories-a-forgotten-design-tool-1613151b8491?source=collection_archive---------5----------------------->

![](img/cece88c56e24860a71a9e4516c4e8511.png)

在 [Unsplash](https://unsplash.com/s/photos/ram?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上[栾卓卡](https://unsplash.com/@luangjokaj?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)拍摄的照片

# 前言

这些年来，我已经用许多不同的方式接触了设计和开发。当我第一次开始开发时，我通常会从我认为最关键的方面开始。在大多数情况下，这就是数据建模。但不是类设计，我会从 SQL 模型开始。我将预先确定我需要的所有列、大小要求和连接。数据存储的地方，似乎是最合理的起点。然后，我会将堆栈向上扩展到软件数据模型，然后是我需要的服务，最后是用户界面部分，无论是 API 控制器(或 WCF SOAP)还是实际视图(ASP。网)。

像开发世界中的任何事情一样，这并不一定是错误的，但是随着时间的推移，我了解到以这种方式工作的困难。当我使用这个流程时，会不断发生一些事情:

1.  用户似乎总是只关心系统的 UI /界面部分，而不是后端的任何东西。所以本质上所有的数据工作并没有真正在早期产生影响。
2.  他们似乎几乎每天都在改变他们需要的东西(当我幸运的时候是每周一次)。这将导致数据元素不断变化，包括大小、结构和表设计。
3.  每次需要更改时，我都必须通过 3 或 4 层来为他们提供任何价值，即使我们还没有上线(只是为了显示进度)。这需要大量的 DTO、接口和对象来改变整个堆栈。
4.  业务逻辑的自动化测试总是花费更长的时间，尤其是当我试图测试 SQL 设计和业务逻辑的时候。

这非常令人沮丧。我处理这件事的方式从来都不“正确”。客户们也觉得所有的事情都要“永远”进行下去。

请记住，已经建立的项目不会像以这种方式运作的绿地项目那样受到严重影响。但是当工作在全新的事物上时，提供价值的时间感觉被拉长了。

# 我的新方法

随着时间的推移，我意识到需求会发生很大的变化，尤其是在新的应用程序中(业务规则和数据元素变更是最常见的)。因此，我决定从纯粹的数据存储转移到逻辑和数据设计上，然后再考虑表结构。事实上，在我职业生涯的这个阶段，我会等到最后一刻才开始整理储物件。

我实现这一点的方法是在项目早期建立一个可靠的界面。然后，当使用测试驱动的设计/开发(TDD)方法时，我开始构建存储库和服务的内存模型。

从这里开始有几个巨大的优势。

1.  早期不需要基础设施。这意味着在项目开始时，不需要对技术做出任何决定(例如，MongoDB、SQL Server 或原始文件)。您可以稍后再做这个架构决策(我也理解在许多情况下这可能已经为您准备好了，但是仍然…)。
2.  您有一个内置的测试实现，当进行自动化测试时，它将更恰当地表示您的逻辑，避免任何对模仿或伪造的大量需求。
3.  在早期建立所有业务规则，这些规则可以很容易地翻译成 SQL 或任何其他语言，通过同时集中所有的努力来降低认知负荷。我的意思是，你可以一次设计整个数据库结构，而不是为了一个更统一的结构而在整个项目中零碎地设计。
4.  避免了引入新功能的多个步骤的费用，这意味着不必首先运行脚本，或者需要在开发环境中本地运行脚本。打戏是小事。

自从我开始朝这个方向发展，我就再也没有回到从数据基础设施开始。但是我必须承认，我发现开发人员和 10 年前一样，首先从 SQL 脚本开始。我明白了。因此，为了展示一种更简单的方法，接下来我将通过一个例子来说明。

# 示例概述

在这个例子中，我将只关注存储库接口的一个功能。具体来说，它将是一个产品存储库。很简单。但是，我将通过 TDD 过程(正如我所看到的)来展示它的好处。

> 注意:无论如何我都不是 TDD 纯粹主义者。我天生持务实的观点，但试图留住许多房客。

虽然这主要是在 C#中完成的，但我坚信我们可以在任何面向对象语言中应用它。

让我们跳进来。

# 接口定义

正如我之前提到的，我将从界面开始。我很少让 TDD 定义我的接口(尽管我确实允许 TDD 改变它)。通常，这是因为接口是需要遵守的契约。这是我目前的设计:

这是一个非常简单的 CRUD 接口。基本我知道，但足够普遍，它仍将是有用的。我们将重点关注`AddAsync`方法。

# 步骤 0:准备 TDD

我本人偏爱[xUnit.net](https://xunit.net/)，所以我将把它用于测试框架。在这种特定的情况下，我通常会跳过几个 TDD 步骤，建立一个基线实现，如下所示:

一旦有了这个，我就可以为我的测试创建 xUnit 类了。通常，它会像下面这样开始:

此时，是时候开始构建我的实现了。

# 步骤 1:构建内存中的实现

我将用一些背对背的代码示例来展示这种方法，其中我建立了一个测试，然后介绍它是如何实现的(通过测试)。如果你想看成品，就直接跳到最后。

> 给定有效的产品对象，当添加时，返回非零整数

> 给定两个唯一的产品对象，当将两者相加时，返回值是唯一的并且不等于零

> 给定添加的产品，当按 Id 获取时，则返回具有相同详细信息的产品

在下一篇文章中，是时候开始对设计施加一点压力了(再次强调实用的 TDD)。所以我需要为`GetAsync`调用做一个基本的实现，这样我就可以开始执行其他类型的测试。

您还会注意到，我开始执行一些重构来使测试变得更小。

> 给定无效的产品名称，添加时会引发异常

> 给定添加的产品，当添加同名的新产品时，会引发异常

您将在这里看到，我继续对代码进行重构，以减轻测试负担。重构测试应该像在生产代码中一样工作(依我拙见)。

> 给定的空乘积在添加时会引发异常

这是一个显而易见的…

> 添加了给定的空描述，检索时，描述为空字符串

> 给定名称太大，添加时会引发异常
> 
> 给定的描述太大，添加时会引发异常

# 代码摘要

最终的测试和实现代码如下:

在`GetAsync`的一点帮助下，我们几乎完全专注于`AddAsync`。使用内存中的实现，这并不太复杂。您可以立即看到好处:

1.  我们已经想好了先决条件。
2.  我们现在可以将这个实现用于将来可能需要一个`IProductRepository`实例的测试。
3.  这些测试运行速度很快！

但是这样做的目的是提供一种创建数据库结构的方法。让我们接下来做那件事。

# 步骤 2: SQL 实现

我偏爱微软 SQL Server(我最了解的)和利用 [Dapper (micro-ORM)](https://github.com/DapperLib/Dapper) 。因此，让我们展示一个表的快速设计，以及带有我们刚刚建立的规则的部分 SQL Server 实现。

你可以在设计的表格中看到，我用`64`作为名称的最大长度，用`256`作为描述，这是通过测试确定的。我也把它们都做了`NOT NULL`。自然，主键是一个与我们的模型相关的`INT`。

现在实现向表中添加一个产品。

> 如果你还没有看到我对`ISqlExecutor`的用法，请参阅文章 [C#提示:SQL Executor 服务](https://justin-coulston.medium.com/c-problem-sql-executor-service-deb459132a50)了解我的方法。

您会注意到一些事情:

1.  前提条件逻辑是相同的。虽然我没有把它抽象出来，但是您可以很容易地将这种逻辑分离出来，以便在这些类型的实现中重用。
2.  我以与对象完全相同的方式命名列。对于任何 ORM，这只是更容易处理。然而，我承认情况不会总是这样。
3.  我们没有在对象本身上设置产品标识符。这样，内存中实现的工作方式与 SQL Server 版本不同。但是，您可以根据自己的判断执行此操作(这可能是您最好的选择)。

这是一个非常简单的实现。然而，我发现当我们进行更复杂的查询时，比如聚合查询、计数器、复杂连接等等，这个值会放大更多。

# 结论

在本文中，我介绍了从测试到 SQL Server 实现开发一个实现(单一方法)的整个过程。在现实环境中，逻辑可能会变得更加复杂，尤其是当您冒险关闭服务(而不是简单的 CRUD 存储库)时。但这同样适用于这些服务。

这种方法的好处是能够在对数据库结构做太多工作之前定义逻辑。它还为未来的单元/集成测试提供了巨大的好处。在更高层次的服务中使用具有与 SQL 版本相同的核心逻辑和条件的真实实现的能力允许衍生出更好的测试。尽管我看到了模拟服务的价值，但是您确实丢失了重要的业务逻辑和检查(除非您为每个测试明确地做了这些。为什么不使用一个真实的实现呢？).

最后，我喜欢这种方法，因为它有助于尽早测试你的界面设计。在 CRUD 服务中，这不是一个大问题，但是在设计业务服务或集合存储库时，优势更加明显。

我知道这是一个非常简单的技巧，但是我发现它对我作为开发人员的工作效率有极大的影响。我希望你也觉得它有用。

直到下一次！