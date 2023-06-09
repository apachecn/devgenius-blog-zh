# CI/CD 管道的简单定义

> 原文：<https://blog.devgenius.io/a-simple-definition-of-the-ci-cd-pipeline-8a48169be938?source=collection_archive---------6----------------------->

🚀 [**打造分层微服务**](https://learnbackend.dev/books/build-layered-microservices) 这本书出来了！现在就在 [learnbackend.dev](https://learnbackend.dev/books/build-layered-microservices) 购买你自己的副本。

![](img/89705072cd0531af4cf52367fd402b79.png)

*持续集成/交付/部署*是一种通过将自动化引入软件开发阶段，向最终用户交付更快更新的方法。

在过去，负责一个特性的开发人员通常会孤立地工作几个星期——如果不是几个月的话——然后将他们完成的工作合并和集成到主分支中，并最终将其部署到生产中。

当他们试图集成他们的代码时，他们最初工作所基于的分支代码已经发生了很大的变化，以至于合并这些新的变化经常被证明是非常具有挑战性和耗时的，结果就是有时被称为“合并地狱”的东西。

这将最终导致代码冲突和 bug 累积很长一段时间而得不到纠正，从而几乎不可能快速交付产品更新。

为了解决这个问题，开发人员提出了一个自动化的软件发布管道，它结合了持续集成、交付和部署，通常缩写为 *CI/CD* 。

# 连续累计

这个发布管道的第一步叫做*持续集成*。

*持续集成*，是将来自多个开发人员的频繁代码变更自动集成到一个像 Git 这样的中央存储库中的实践，在那里运行构建和测试，以便在集成之前断言新代码的正确性。

由于持续集成旨在与自动化测试结合使用，它通常与一个叫做[测试驱动开发](/a-simple-approach-to-test-driven-development-68fde989157c)的软件开发过程相结合。

现在，这里是*持续集成*工作流在实践中的样子:

*   在将代码变更提交到中央存储库之前，开发人员在他们自己的工作站上的本地环境中构建、运行和测试代码。
*   每次提交新代码时，CI 服务都会选取更改并自动构建项目。
*   如果构建成功，就运行单元测试和集成测试，以立即发现任何错误。
*   最后，向团队发送一份详细的报告，包括成功构建的数量、运行的测试的数量等等。

现在让我们进入发布管道的下一个阶段，称为持续交付或部署。

# 持续交付与部署

尽管*连续交付*和*连续部署*听起来非常相似，都是缩写的 CD，并且旨在实现相同的目标，但它们有一点不同。

## 连续交货

*持续交付*扩展了*持续集成*，因为它的目标是将经过测试的代码打包成一个工件——也称为构建——可以在任何时候通过手动发布进行部署——换句话说，按下一个按钮——无论是在试运行环境还是生产环境中，通常都是按照这个顺序。

在这里， *deployment* 简单地说就是:通过将软件版本转移到公共服务器或另一种分发机制，比如应用商店，来分发软件版本。

为什么是这个顺序？因为*单元测试*或*集成测试*很少足以断言一个版本工作正常。

最后，在发布给最终用户之前，它们通常由团队的质量保证成员在试运行环境中执行手动冒烟测试或验收测试来完成，这种配置通常是产品配置的副本，或者至少尽可能接近。

## 持续部署

相比之下，*连续部署*更进一步，如果之前的测试都没有失败，那么向最终用户发布构建是自动的，因此不需要人工干预。

这可能是加速与客户的反馈循环和减轻团队压力的一个很好的方式，因为不再需要发布日期，因为代码一准备好就会自动部署。

然而，只有当您的团队已经通过仔细设置管道的每个阶段完成了繁重的开发工作时，这种全自动的发布过程才是可能的。

因此我们可以说*连续部署*需要*连续交付*。

# 结论

总之， *CI/CD* 管道是构建、测试和部署代码的自动化工具的强大组合，极大地提高了代码的质量，并使新功能的集成速度极快。

# 下一步是什么？

不要忘记👏🏻如果你喜欢读我的作品！

👉你喜欢这种内容？查看 https://learnbackend.dev 上的书籍[**Build Layered micro services**](https://learnbackend.dev/books/build-layered-microservices)了解如何使用 Express framework 构建生产就绪的分层认证微服务，从第一行代码到最后一行文档，该服务在开发实践和软件架构方面符合行业标准。