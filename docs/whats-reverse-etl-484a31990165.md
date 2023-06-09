# 什么是逆向 ETL？

> 原文：<https://blog.devgenius.io/whats-reverse-etl-484a31990165?source=collection_archive---------13----------------------->

## 从仓库中取出数据？

# **TL；博士**

反向 ETL 是将数据从你的数据仓库同步到你的业务工具如 Salesforce 和 Hubspot 的过程。

*   数据团队花时间将数据组织到一个**集中仓库**
*   然而，像销售和营销这样的运营团队**需要在他们的日常 SaaS 工具中使用这些数据**
*   反向 ETL 是将数据从仓库转移到那些工具中的过程，因此运营团队可以对其采取行动
*   之所以称之为反向 ETL，是因为数据是 ***离开*仓库**

随着所谓的“现代数据堆栈”围绕着像 [Snowflake](https://www.snowflake.com/) 和 [BigQuery](https://cloud.google.com/bigquery) 这样的集中式云仓库进行整合，将数据反向 ETL 到 SaaS 工具中的过程变得更加容易，像 [Census](https://www.getcensus.com/) 这样的工具将其作为简单的 SaaS 服务提供。

# **仓库里是什么样的数据？**

逆向 ETL 的一个令人困惑的部分是理解数据仓库中的*到底是什么，以及它来自哪里。要复习什么是数据仓库，请点击这里查看最初的技术文章。每个仓库设置都不同，但您应该会看到以下几种情况的组合:*

*   **用户数据**

每个应用程序在它们的[生产数据库](https://technically.substack.com/p/the-details-production-databases)中都有一个`users`表，这通常构成了你在仓库中拥有的关于你的用户的那种数据的基础。常见属性包括用户注册的时间、他们的电子邮件地址、他们的姓名、他们工作的公司，有时还包括高级活动数据，如他们上次登录的时间。

*   **产品使用数据**

用户在您的工具中所做的是您可以捕捉到的一些最有价值的分析数据。团队倾向于根据**事件**来跟踪这一点。每当用户点击一个特定的按钮，导航到一个特定的页面，或者在产品中做任何值得注意的事情时，驱动你的应用程序的代码都会记录一个“事件”；这些事件随后被发送到数据仓库，以供将来分析。您可以汇总这些数据来回答一些问题，比如有多少用户尝试了某个特定的功能。

*   **营销和归属数据**

与产品活动一样，数据团队收集关于用户访问哪些网站页面的信息，是什么来源将他们推荐到该网站的(播客赞助？谷歌搜索？)，以及他们在注册前浏览营销材料的“旅程”。这有助于营销团队了解哪些渠道表现良好，以及如何分配支出。

*   **支付和计费数据**

关于用户和团队参与哪些计划的数据，以及他们每月支付多少费用，有助于团队了解收入来自哪里以及可能与哪些活动相关。其中一些来自你自己的系统，一些来自支付[API](https://technically.substack.com/p/whats-an-api)比如 [Stripe](https://technically.substack.com/p/what-does-stripe-do) 。

无论我们谈论的是什么样的数据，所有的数据都通过 ETL(或 ELT)进入仓库，这个过程在技术上已经在这里广泛讨论过了。数据团队花费时间获取源数据，对其建模以使其对分析有用，并将其存放在数据仓库中。将数据以有用的格式放入仓库是数据团队的主要职责之一！

但是**反向 ETL** 是相反的:将它*从仓库*中取出，并将*放入*您团队的 SaaS 工具中。

# **数据需要在上下文中**

公司的运营依赖于一些由 SaaS 工具拼凑而成的组合。每个团队使用不同的工具，但主题是相同的:他们都需要用户和活动数据是有用的。让我们从几个例子开始:

**→销售**

大多数销售团队使用 [Salesforce](https://www.salesforce.com/) 作为他们的记录系统和运营中心。Salesforce 跟踪您所有未完成的机会和客户，让您在不同阶段之间移动公司(例如，潜在客户→客户)，自动获取电子邮件数据，允许团队构建渠道报告…您可以在其中做很多事情。

**→营销**

营销团队也使用 CRM:通常是 Hubspot 或 T2 Marketo。这些工具允许团队跟踪他们的所有销售线索，将他们组织成组，并根据触发器在特定时间发送有针对性的电子邮件活动。如果你注册了一个产品并在一天后收到了一封欢迎邮件，那很可能是用这些工具之一发送的。

**→支持**

支持团队使用像 [Intercom](https://www.intercom.com/) 和 [Zendesk](https://www.zendesk.com/) 这样的工具来跟踪所有打开的票证和请求，以及通过电子邮件或聊天与客户沟通。这些工具允许团队对开放的票证进行分类和组织，使其处于不同的状态，与其他团队成员协作(例如，标记可能知道答案的同事)，以及发送 CSAT 调查等。

尽管所有这些工具都生成和管理自己的数据，但是当您可以从数据仓库中获取关于用户的外部数据时，它们会变得更加有用。回到我们的例子:

→ **销售** —产品使用数据

*   例如，用户在产品上花了多少时间？他们都用过哪些功能？有多少团队成员是活跃的？
*   帮助确认潜在客户，更有效地分配时间

→ **营销** —人口统计数据

*   这家公司有多少员工？当他们注册时，他们说他们要用这个产品做什么？
*   帮助建立有用的小组和目标信息/点滴活动

→ **支持** —支付数据

*   例如，该客户的计划是什么？他们付钱多久了？账户有多大？
*   帮助优先支持更关键的客户

这些都是说明性的:团队变得有创造力，你永远不知道什么样的数据在不同的环境中会有价值。重要的部分是数据需要在团队用来采取**行动**的工具中*。*

# **反向 ETL 如何工作**

现在，您已经知道仓库中通常存储的是什么类型的数据，并且知道将这些数据从仓库中取出并放入团队的可操作 SaaS 工具中是非常重要的。**反向 ETL** 就是实现这一点的过程。另一种思考方式是，反向 ETL 让您可以操作化您的数据，这只是一种奇特的方式，说明您实际上可以将您的数据用于日常操作和决策，而不是将其发送到一个几周后就会变得陈旧的仪表板中。

**→ SaaS 工具拥有您可以使用的数据库**

所有上述工具——sales force、Hubspot 等。—允许您向他们发送数据，他们将为您存储数据并显示在工具的用户界面中。他们通常通过一组[API](https://technically.substack.com/p/whats-an-api)来公开这一功能，比如来自 Salesforce 的[。一旦你获取了数据，当你使用这个工具时，你会在上下文中看到它。这是 Intercom 的一个示例，您会在与用户的支持对话旁边看到:](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/custom_fields.htm)

![](img/389ee9d4d48fc9c088a646a0fa627ab2.png)

不管是谁设置的，都是从公司的内部 ID、团队规模、每月支出(他们什么都没花！)，还有他们的网址，也是不为人知的。他们使用 Intercom 的 API 将这些数据输入 Intercom 的系统，现在他们可以将这些数据与工具一起使用。你在这里看到的数据是通过反向 ETL 得到的。

**→第一波:从零开始构建反向 ETL**

直到最近，最先进的技术是手工进行反向 ETL。要从逻辑上将数据从您的仓库导入 SaaS 工具，您需要设置某种循环作业，提取数据并使用 SaaS 工具的 API 将其导入他们的系统。API 将要求数据符合特定的格式，因此您可能需要在运行中转换它。您还需要设置报告和出错时的重试方案，因为错误是会发生的。

> **🔍更深层次看🔍**
> 
> 从零开始构建反向 ETL 管道的过程实际上非常类似于从零开始构建普通 ETL 管道的过程。这里加倍恼人的事情是，每个目的地——即您的 SaaS 工具的 APIs 需要稍微不同格式和配置的数据，这意味着每个管道都需要定制。
> 
> **🔍更深层次看🔍**

如果我的措辞没有使它变得明显，这是一种痛苦，特别是因为 API 和格式会随着时间的推移而变化。几年前，专门构建的工具开始出现，以使事情变得更容易。

**→第二波:为反向 ETL 专门构建的 SaaS**

今天，你可以使用类似于 [Census](https://www.getcensus.com/) 或 [Hightouch](https://hightouch.io/) 的东西来为你相当容易地进行反向 ETL 你只需要做一点预先配置。这些工具连接到您的**源**(数据仓库和其他)、您的**目的地** (Salesforce、Hubspot 等)。)并允许您使用 SQL 轻松地在它们之间移动数据。您还可以创建[模型](https://docs.getcensus.com/basics/core-concept#building-models)来组织您的数据，并为您的工具想要接收的格式做准备。

一个常见的用例可能是每天一次将营销属性数据从仓库同步到 Hubspot。Census 将允许您安排同步，如果需要，可以提前转换数据，并显示每次同步的历史记录:

![](img/999e01d46c81e0ab10d79d438f9a4b5f.png)

在幕后，他们负责对您的仓库运行查询，动态转换数据，并访问您的 SaaS 工具的 API，以定期插入和更新您想要的数据。

# 进一步阅读

人口普查的[关于反向 ETL 的解释者](https://blog.getcensus.com/what-is-reverse-etl/)

反向 ETL 工具综述

Benn Stancil 关于[仓库作为平台的帖子](https://benn.substack.com/p/entity-layer)

> 用简单的语言从技术上分解软件工程，这样你可以给你的老板留下深刻印象。加入 3 万多人的行列，获得更多技术知识:

[](https://technically.substack.com/embed) [## 技术上

### 用简单而吸引人的方式从技术上解释软件和硬件，这样你可以给你的老板留下深刻印象。点击阅读…

technically.substack.com](https://technically.substack.com/embed)