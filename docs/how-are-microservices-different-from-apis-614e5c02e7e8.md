# 微服务和 API 有什么不同

> 原文：<https://blog.devgenius.io/how-are-microservices-different-from-apis-614e5c02e7e8?source=collection_archive---------4----------------------->

![](img/9a624ee83db7d7a371e5a3964c8e6b8b.png)

照片由 [Mailchimp](https://unsplash.com/es/@mailchimp?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

# 什么是微服务？

微服务是一种架构风格，由单独的独立服务组成。现代应用依赖微服务架构来加快部署。微服务在[受欢迎的主要原因是一步一步开发应用程序的单个功能很容易。较大的组织利用微服务在独立的团队中工作，他们之间没有任何复杂的通信。亚马逊网络服务将微服务描述为:](https://www.simform.com/blog/what-are-microservices/)

微服务将一个较大的团队细分为独立的小型运营团队，这些团队完全拥有自己的服务。团队协同工作，相互授权以缩短周期时间。

# 微服务的特征

*   每个服务都有自己独立的代码库、数据库层和 CI/CD 工具包。
*   保存数据是微服务的责任
*   每个服务都可以独立部署和测试，而不依赖于任何其他服务。
*   服务之间的内部通信通过定义良好的 API 或任何轻量级通信协议进行。
*   每个微服务决定最适合其用例的技术堆栈、库和框架。
*   如果出现网络或系统故障，服务应该实现重试功能。

# 什么是 API？

应用程序编程接口或 API 是允许开发人员与应用程序交互的入口。交互允许开发人员完成两件事:访问应用程序的数据或使用应用程序的功能。比如使用社交媒体帐户在网站上进行身份验证，从单独的应用程序访问谷歌地图，触发物联网设备等。，全靠 API。

API 通常是为第三方用户创建的。它们通常是公开的。随着微服务的日益普及，越来越多的私有 API 应运而生。组织利用 API 作为单个微服务相互通信的轻量级解决方案。

用技术术语来说，API 通过 HTTP 请求发送数据。关于这一点，API 以 JSON 的形式返回文本响应，开发人员可以根据他们的可行性来使用。存在多种类型的 API，例如 REST、SOAP、GraphQL、gRPC 等等。

# 微服务和 API 的区别

在深入讨论细节之前，让我们快速回顾一下:

*   API 是微服务之间进行通信的东西。软件 API 定义了什么是可接受的请求以及如何响应请求。
*   微服务是一种架构方法，用于将应用程序的功能构建到离散的、模块化的、自包含的程序中。它允许开发人员通过分解功能来轻松创建和维护应用程序。

微服务和 API 经常结合在一起，尽管它们是两个不同的实体。微服务中的服务利用私有 API 相互通信。微服务的一个组件使用私有 API 来访问同一微服务的另一个组件。这种思想类似于使用公共 API 作为应用程序之间的接口。

务必记住，没有两个微服务是相同的，它们都以不同的方式使用 API。有些人会将许多 API 分配给一个服务，而有些人会利用一个 API 来访问多个服务。另一方面，API 超越了微服务。它们可以在没有微服务实现的情况下在内部使用。

# 结论

API 和微服务对于任何现代应用程序的开发都至关重要。虽然它们在性质上有所不同，但有时由于非常接近，两者之间可能会出现混淆。根据我的经验，我试图解决人们在详细讨论他们时所面临的这个问题。如果你有任何特别的例子可以更彻底地澄清疑问，请在下面的评论中告诉我。