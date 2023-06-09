# 用 Ktor 开发 web 应用程序

> 原文：<https://blog.devgenius.io/series-developing-a-web-application-with-ktor-9d43af28cc?source=collection_archive---------6----------------------->

![](img/b335e56674b3c561e14ddb8538faf56d.png)

在我以前的文章中，我主要介绍了 Kotlin 生态系统中的几个框架，使用了非常基本的例子。这个例子只涵盖了相应框架提供的一小部分功能。为了展示这些框架如何在更真实的应用程序中协同工作，我构建了一个更复杂的示例，它涵盖了所用框架的不同特性，还包括一些特殊情况。

在这一系列文章中，我将展示如何开发一个 web 应用程序，它由一个服务器后端和一个 web 客户端组成。该应用程序的基础是由 Kotlin 生态系统的其他几个框架扩展的 **Ktor** 框架。

应用程序开发是以增量方式完成的，还包含在后续步骤中恢复/更新的中间步骤。我也会定期进行重构，只要我觉得代码越来越差，需要改进。我并不打算从一开始就展示一个完美的最终解决方案，而是在并行撰写本系列文章的同时逐步开发。为了保持简短，本文中没有显示所有步骤，但是在包含应用程序代码的 Github 存储库的提交历史中是可见的。

这些文章将涵盖以下主题:

*   需求规格
*   申请的结构
*   服务器后端应用程序—设置
*   服务器后端应用程序—持久性
*   服务器后端应用程序—业务逻辑
*   服务器后端应用程序— API 接口
*   服务器后端应用程序—身份验证+安全性+用户角色
*   前端 web 客户端—设置+用户界面
*   前端 web 客户端—API 连接+身份验证
*   文档+应用交付
*   结论

因为我在开发过程中写文章，还没有完成最终版本，所以这个系列有多少文章还不确定。这些要求是最终的，我也有一个想法如何实现它们，但细节和缺点直到现在还不清楚。大约在 7 点到 8 点之间。我不喜欢太大的文章，因此我会在一个需求被实现并且文章有大约 8-10 分钟的长度时，将文章拆分。

我会一篇接一篇地发表这些文章(不是一次全部)，并尝试每隔两到三周发表一篇。

# **需求规格**

在第一部分中，我描述了应用程序应该解决的需求，并概述了计划的应用程序的结构。

在接下来的文章中，这些需求是指导方针，也是我在逐步开发过程中唯一需要解决的部分。

要开发的应用程序是一个简单的**银行应用程序**，它支持如下一般功能

*   创建/更新/删除用户
*   为用户添加/更新/删除帐户
*   在两个用户帐户之间创建交易
*   为管理员显示所有帐户的历史记录
*   管理员删除交易

应用程序有**一般**要求:

*   使用 Kotlin 原生框架(如果可能的话)。 **Ktor** 是应用程序的基础框架。
*   该应用程序应该可用于浏览器和 REST API 客户端。
*   对于浏览器和 API 客户端的用户应该有一个认证机制。不经过验证就执行请求应该是不可能的。
*   有两种可用的应用程序用户角色:用户和管理员
*   前端应用程序和后端应用程序之间的通信应该使用 REST 来完成。
*   应该记录所有请求。
*   应用程序应该作为 docker 图像交付。
*   API 端点使用 OpenAPI 规范进行记录。

此外，应用程序还应涵盖以下**用例**:

# 用户角色:

**用户**

*   用户由以下属性组成: *userId* (唯一)*名*，*姓*，*生日*，*创建日期*，*最后更新*。
*   用户必须年满 18 岁。
*   只能创建一个名*名*、*姓*和*生日*相同的用户。
*   应该可以创建新用户。
*   应该可以删除一个现有的用户。
*   应该可以编辑除*用户 Id* 之外的所有用户数据。
*   用户正在创建过程中设置初始密码。
*   密码至少需要 16 个字符，包含数字、小写和大写字母以及特殊字符。
*   用户密码可以更改。
*   一个用户可以有多个帐户。

**账户:**

*   账户由以下属性组成:*名称*(每个用户唯一)*账户 id* (唯一)*余额*，*显示*，*限额*，*创建日期*，*最后更新*。
*   应该可以为现有用户创建帐户。创建一个没有用户的帐户应该是不可能的。
*   一个帐户只能由一个用户拥有。
*   应该可以删除现有账户(用户-账户关系被删除，但账户仍然存在，以保证交易历史)。
*   应该可以编辑除*账户 id* 和*余额*之外的账户数据。
*   一个帐户可以有多个交易(作为源或作为目标部分)。

**交易**:

*   该交易由以下属性组成:*交易 id* (唯一)、*发起账户*、*目标账户*、*金额*、*创建日期*。
*   一个交易只能持有一个正数。
*   应该可以创建两个帐户之间的交易。
*   应该不可能更新或删除交易。
*   仅当两个帐户的更新余额成功时，才创建交易。

# 管理员角色

*   管理员可以通过 API 或浏览器使用该应用程序。
*   对于管理员，存在预定义的数据集(不可能创建新的管理员)。
*   管理员可以重置每个用户的密码。
*   管理员对所有帐户的所有交易都有一个概览。
*   管理员可以删除交易(这将更新源帐户和目标帐户的余额)。

# 申请的结构

该应用程序包含两个部分——后端 **Ktor** 服务器应用程序和前端 web 客户端应用程序。前端与服务器后端分离，以便于交换。

下面是对用于两个应用部分的框架/工具的概述。

**科技栈**

后端:

*   格拉德勒
*   科特林
*   Ktor
*   柯因
*   暴露的
*   光
*   氘
*   液态碱

前端:

*   格拉德勒
*   科特林/JS
*   反应
*   引导程序

有了这个概述，我的系列的第一部分就完成了，是时候开始开发了。在下一篇文章中，我将从后端 **Ktor** 服务器应用程序开始。