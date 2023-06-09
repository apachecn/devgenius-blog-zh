# How 1 更改将 CI/CD 管道上的克隆时间减少了 90%

> 原文：<https://blog.devgenius.io/how-1-change-decreased-clone-times-on-ci-cd-pipelines-by-90-464a42f680dd?source=collection_archive---------4----------------------->

## 这使我们的管道构建时间平均减少了 1 分钟

![](img/2f45037360ef91254a79308df85f84c2.png)

Bitrise 工作流

## CI/CD 简介

CI/CD pipeline 帮助您自动化软件交付过程中的步骤，例如启动代码构建、运行自动化测试以及部署到试运行或生产环境。自动化管道消除了人工错误，提供了标准化的开发反馈循环，并实现了快速的产品迭代。

CI/CD 管道提高了现有流程的效率，并有助于通过每周或每两周发布一次的方式更快地迭代产品，其优势如下:

*   它有助于开发人员专注于编写代码
*   所有利益攸关方都可以方便地获得该系统的最新版本。
*   产品更新压力不大。
*   所有代码变更、测试和部署的日志随时可供检查。
*   出现问题时回滚到以前的版本是一个常规操作。
*   快速的反馈循环有助于建立一种学习和责任的组织文化。

## 问题

一般来说，您希望 CI/CD 管道很快，因为每个发出的 pull 请求都有一个完整的过程在运行，用于验证构建没有被 PR 上运行的关键测试用例破坏。

缓慢的构建时间增加了每个 PR 的合并时间，这在内部降低了开发人员的生产力。

我们希望减少 CI/CD 管道上的开发人员合并已经审核的 PR 的等待时间。

## 解决办法

我们用于 CI/CD 的工具是 Bitrise，对于静态分析，我们使用 Github 操作，在 Bitrise 中，我们定义了自己的工作流，其中包含各种步骤，如 Git 克隆、静态分析、UI 测试以及将构建推送到 hockey。类似地，我们有一个 Github 动作的工作流，它执行 lint 检查和其他任务，比如单元测试和生成各种报告。

每个组织都有多个 Bitrise 工作流来运行各种用例，这些用例可以在每个 PR 或每夜构建中运行，或者将构建推送到 Play/App store。

我们审查每一步平均需要多少时间，以及是否有任何可以改进的地方。

有一天，我偶然在 GitHub action 上查看 git 克隆时间，大约是**10-15 秒**。

因为我知道我们在 Bitrise 工作流程中也有 git 克隆步骤，因为任何 CI/CD 管道的运行都必须签出代码，所以我很惊讶地看到 Git 克隆时间大约为**平均每个构建**1.4 分钟**。**

然后我意识到 GitHub action 在做浅层克隆，Bitrise 在做深层克隆，通过阅读他们用来检查代码的脚本，理解他们之间的区别，你就能理解[浅层克隆](https://github.blog/2020-12-21-get-up-to-speed-with-partial-clone-and-shallow-clone/)是如何工作的。

为了不深入克隆的概念，Github action 所做的基本事情是深度为 1 的浅层克隆，这意味着:

> [创建一个“浅层”克隆，其历史被截断到指定的修订次数。](https://stackoverflow.com/questions/6941889/is-it-safe-to-shallow-clone-with-depth-1-create-commits-and-pull-updates-aga)

这让我检查了 Bitrise 上的 [Git 克隆是如何工作的，它没有指定任何深度，这意味着它是深度克隆，所以我们能够通过 Bitrise 平台找到一种方法来指定提交的深度，这有助于回购的浅层克隆。](https://www.bitrise.io/integrations/steps/git-clone)

![](img/39490de8b07161b2e78c411732b01b72.png)

我们将深度设为 1，然后我们的克隆时间减少了 **90%(1.4 分钟— > 16 秒)**，构建时间减少了 **1 分钟**。

# 学习

有时候你需要的只是一行代码来节省团队中每个人的时间，并改善开发者的日常体验。