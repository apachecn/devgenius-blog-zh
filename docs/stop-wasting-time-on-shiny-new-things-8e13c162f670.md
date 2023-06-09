# 不要在闪亮的新事物上浪费时间

> 原文：<https://blog.devgenius.io/stop-wasting-time-on-shiny-new-things-8e13c162f670?source=collection_archive---------17----------------------->

## 当解决方案变成新问题时

为一个项目挑选技术是困难的，当每天都有新技术突然出现时，这就更难了。这些技术中有很多非常有用和强大，但是它们也给了你足够的绳索来上吊。我知道，我知道，另一个关于现代网络框架的邪恶的故事，或者通过科技行业发现的[猖獗的货物买卖](https://hackernoon.com/the-cargo-cult-school-of-software-development-78469084961d)。区别在于:我并不反对使用我将要描述的技术。事实上，我经常使用并推荐它们！我在这里想做的是解释好的技术和好的 ***在*** 的情况下的区别。这里我用几个例子来说明区别。

![](img/541335af4fe97f0d09d27cd6efd27e9a.png)

闪闪发光并不能让东西变得有用

## 我说反应的部分

所以我想在这一点上称 React 为“新”有点不合适，但它仍然是我称之为“开发过度杀伤”的最大元凶之一。React 是一个强大的框架，允许您轻松地创建复杂的 web 应用程序，具有足够的开箱即用功能，让您感觉几乎不用自己做任何事情。在企业环境中，它允许在应用程序和团队之间共享资源，从而带来美妙的开发体验。最重要的是，有一个成熟的生态系统和一个维护它的大公司，难怪 React 成为企业网站开发的首选。那么问题出在哪里？

React 适用于交互式用户界面和复杂的应用程序。这是脸书为脸书设计的。如果您正在创建一个需要这种能力的应用程序，那么我会 100%推荐 React。然而，如果你只是在制作一个静态网页，或者一个早期的模型，甚至是一个简单的时事通讯的注册页面，为什么要使用这么强大的东西呢？你不需要对这样的事情做出反应，就像你不需要喷火器来点燃蜡烛一样。

让我们看一个时事通讯的注册页面的例子。用普通的 Javascript、HTML 和 CSS 创建表单并设计其样式相当简单。大多数 web 开发人员可能已经在某个时候将此作为练习。那么 React 给这个过程增加了什么呢？首先，你要么使用像 [create-react-app](https://github.com/facebook/create-react-app) 这样的工具为你创建一个 react 项目(有比你需要的更多的依赖项和复杂的结构),要么你需要自己配置 Babel 和 Webpack。React 要求浏览器使用 Babel，因为它是用 JSX 编写的，这就像 Javascript 和 HTML 受到了杰夫·高布伦的“苍蝇”待遇。一旦您配置好项目，您将很快意识到您并没有真正使用 React 的许多优秀特性。取而代之的是，你几乎只是在编写你用普通 Javascript 和 HTML 会做的东西，但是用不同的方式组织一切，用稍微不同的语法。React 没有以任何方式使应用程序变得更糟，但它也没有帮助，并且可能增加了额外的开发时间。

## gRPC 很棒

我最近做了一个后端项目，在服务之间的通信中使用了 [gRPC](https://grpc.io/docs/what-is-grpc/introduction/) 而不是 REST。我非常喜欢它。开发体验非常棒，性能比 REST 和 JSON 提供的要好得多(在延迟和序列化大小方面)。我真的很喜欢在 gRPC 项目上工作。我也不会把它用于个人项目。

像 React 一样，gRPC 是一种为大型复杂项目提供最大好处的技术。它基本上允许您跨应用程序边界共享数据模型，因此您可以在一个位置声明您的模型和 api，并在多个应用程序中使用它们。模型和 api 是用一种叫做协议缓冲区的技术编写的，这种技术可以翻译成几种语言。它允许你编写一次 api 接口并在多个应用程序中使用，每个应用程序可以使用不同的语言。这一切使得跨团队工作变得容易，并减少了开发时间。那么有什么问题呢？

除了企业级的服务堆栈之外，我不使用 gRPC 的主要原因有两个。首先，它的工具仍然是新的，随之而来的是不稳定的特性和错误。例如，我的团队花了 4 周时间修复了一个跟踪问题，这个问题是在我们尝试切换用来将协议缓冲区转换为 Kotlin 的库时引入的。没有什么比试图向你的老板解释为什么你的发布会比计划晚了 4 周更有趣的了，而且你也不知道如何或何时会准备好。第二，只有当你在多个服务和多个团队中使用 gRPC 时，gRPC 的开发优势才能完全实现。如果我创建一个具有一个前端和一个后端的应用程序，我不会从创建协议缓冲 api 中获得任何好处，因为我不会在多个地方使用接口和模型。正确设置 api 和工具所需的工作完全抵消了您从中获得的任何好处。当然有性能上的好处，但是大多数个人项目不会因为性能问题而陷入困境。

## 把你的头从云里拿出来

云技术是炒作和流行词汇的完美风暴。公司喜欢这样的事实，即他们可以通过没有专用服务器来节省资金，像 AWS 和 Azure 这样的服务提供自己的支持和有保证的正常运行时间。我认为我见过的传播最广的技术是 Kubernetes，但人们仍然不了解它，所以这是我在这里要挑选的。

Kubernetes 使容器管理变得简单和容易。由于自动伸缩、健康检查和负载平衡等功能，它还可以提高复杂应用程序的稳定性。对于一个复杂的系统，Kubernetes 比使用 AWS 计算实例或其容器服务 ECS 需要更多的配置，但它可以节省成本并提高弹性。对于较小的系统，Kubernetes 会导致浪费时间和增加成本。Kubernetes 比管理较少的部署方法需要更多的配置，这意味着需要更多的开发时间。此外，由于 Kubernetes 需要基线量的资源专门用于管理您的 pod，小型系统的成本可能会更高。Kubernetes 的好处才真正开始大规模显现。注意到一个模式？

## 当它值得的时候

那么，什么时候应该使用新的、被大肆宣传的技术呢？很高兴你问了，想象中的对话伙伴！这一切都归结于收益是否超过使用成本。老实说，这不是一个简单的任务，我还在努力。然而，我认为一个好的捷径是看看你实际上会使用什么功能。构建一个需要身份验证、路由和复杂用户交互的 web 应用程序？React 大概是值得用的。您是否部署了多个具有高正常运行时间和高负载要求的应用程序，并使用 CI/CD 管道？Kubernetes 可能是完美的。当你能够利用这些技术的主要特性时，它们会带来巨大的好处。

## /咆哮

如果你从中吸取了什么，我希望是仔细评估技术选择的重要性。如果你从中得不到任何好处，不要浪费时间去学习新的东西并把它整合到一个项目中。