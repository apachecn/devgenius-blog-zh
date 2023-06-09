# [May Update]Wasp——开发全栈 JS 应用程序的语言，没有样板文件

> 原文：<https://blog.devgenius.io/may-update-wasp-language-for-developing-full-stack-js-apps-with-no-boilerplate-cf3541cc925b?source=collection_archive---------7----------------------->

Wasp 是一种配置语言(DSL ),用于使用更少的代码和最佳实践构建全栈 web 应用程序，与 React 和 Node.js 一起工作。我们的使命是简化 web 应用程序开发，同时使开发人员能够继续使用代码和他们喜爱的工具。我们得到了 Y Combinator 和来自 Airbnb、脸书和 Lyft 的工程师的支持。这是我们的社区更新！

[**我们在阿尔法(试用)！**](https://e44cy1h4s0q.typeform.com/to/ycUzQa5A) → [**加入我们的社区**](https://discord.gg/rzdnErX) → [**与我们一起工作**](https://wasp-lang.notion.site/Founding-Engineer-at-Wasp-402274568afa4d7eb7f428f8fa2c0816)

怎么跳，同胞们？🐰 🐝欢迎访问我们的 5 月更新—这是又一个开发和发布新功能的繁忙月份，所以让我们深入了解一下新功能:

# 社区亮点——加入我们的讨论吧！

![](img/c24e39c43022838d8a34847823085135.png)

我们的一位了不起的贡献者和用户， [cursorial](https://github.com/cursorial) ，给整个团队做了一个关于**他如何使用 Wasp 为他当时工作的公司开发和部署一个内部工具**！下一步是把它变成一个独立的 SaaS 服务，当然，他再次使用 Wasp！

![](img/6041a3c8ef926f9a14b59610560a8882.png)

🤯🤯

![](img/9698596ce765e5c6a79da709569d35e7.png)

[加入我们的纷争！](https://discord.gg/rzdnErX)来自我们 Alpha 测试计划的反馈——滚动下方以了解更多信息并加入！

# 🐝成为黄蜂阿尔法测试+获得阿乐黄蜂阿尔法 t 恤！👕

![](img/a3f99af37e7b790a68fa672dc8a5dab1.png)

[想看看兔子洞有多深？服用红色药丸，卢克](https://wasp-lang.notion.site/Wasp-Alpha-Testing-Program-Admissions-dca25649d63849cb8dfc55881e4f6f82)。

我们的 Alpha 测试项目正在全面展开，我们已经得到了一些很好的反馈，但是我们也[需要你加入](https://wasp-lang.notion.site/Wasp-Alpha-Testing-Program-Admissions-dca25649d63849cb8dfc55881e4f6f82)！

这是你体验 Wasp 的机会，与团队建立联系，并赢得永远吹嘘的权利(+一件 t 恤衫来证明)[当 Wasp 还在 Alpha 阶段](https://wasp-lang.notion.site/Wasp-Alpha-Testing-Program-Admissions-dca25649d63849cb8dfc55881e4f6f82)时，你就测试了它，并通过你的反馈几乎单枪匹马地将它从不可避免的厄运中拯救出来！

![](img/e6b8378a6b1695f8c8b009a006dbf610.png)

**加入为:**

*   黄蜂社区官方认可(牛逼 nick color in Discord +限量版 t 恤！)
*   直接联系 Wasp 团队(通过专用渠道)
*   成为第一个了解新功能并直接影响它们的人！

如何加入？在此申请，我们将很快与您联系！

为了证明 t 恤衫不是谎言，这里有一张我们藏货的照片:

![](img/35621f5c2a1527a93f21a63cc4bf6e48.png)

这也是我们创造的最新迷因(由我们的首席技术官马丁创造，他对此非常自豪，所以我必须把它包括进来):

![](img/9530d23b675d4a2afb3fa20bf8e7ed2c.png)

我们第一批测试人员的录制镜头(我们保证，现在更好了！！😅)

# 🚀直接从 Wasp 运行异步作业！🏗

![](img/ee5444e17e819d1dccf6ca7c5372590d.png)

如果您有一个想要以异步方式运行的服务器任务(例如，发送一封电子邮件，通过第三方 API 操作上传的图像，一夜之间生成一个冗长的报告……)，Wasp 可以满足您！

**你只需要提供一个你想要执行的函数，定义它是否是 cron 任务，Wasp 会完成剩下的工作:**

*   执行它
*   不断重试以防失败
*   将进度存储在数据库中，以便在服务器重启时不会丢失
*   →所有你不想操心的重活！

查看带有示例的[功能公告帖子，也可以在这里](https://wasp-lang.dev/blog/2022/06/15/jobs-feature-announcement)找到文档[。](https://wasp-lang.dev/docs/language/features#jobs)

# ❓Easily 配置反应-查询客户端⚙️

![](img/b00b5d10eb8870d586d6e387b5c70b2a.png)

Wasp *useQuery* 挂钩由引擎盖下的 [react-query](https://react-query.tanstack.com/) 供电。它已经有了相当合理的默认选项，所以你通常不需要接触它，但如果你现在接触它，你就可以了！您可以通过客户端设置功能(如下图)中的 *configureQueryClient* (如上图)进行设置:

![](img/dcb89a437ff8022f06cb944186e704d6.png)

有关更多细节和示例，请查看文档。

# 🚧即将推出🚧乐观的用户界面更新没有麻烦！🧘‍♂️

![](img/641393b326c6c2203c4dd5098ca22b99.png)

在我们将 react-query 更新到最新的稳定版本并使其可配置之后，现在是时候处理房间里的大象了——乐观的 UI 更新！这是一个许多开发人员竭尽全力的模式，这使得它非常适合用 Wasp 进行精简！

# 🚧即将推出🚧改进了对 Wasp 的 IDE 支持📟

![](img/b89450b504c3c19988b40b3ddf92daa9.png)

你自找的——你得到了！构建一门语言有很多好处，比如几乎无限的灵活性来为你设计尽可能好的 DX，但是它也需要更多的工作来让围绕它的所有工具如你所期望的那样工作。

Wasp 已经有了一个通过 VS 代码扩展的基于正则表达式的语法高亮，但是现在我们更进一步— **我们正在构建我们自己的 LSP！这意味着所有常见的好东西都将得到支持——自动完成、语法高亮、跳转到定义、…** (我们不再认为它们是理所当然的了！😅)

# 🎉欢迎菲利普——创始工程师！🎊

[看看这篇文章！](https://wasp-lang.dev/blog/2022/05/31/filip-intro)

![](img/0d9ecb0b9477d7f298fbb14e50ffefb6.png)

又一个了不起的工程师加入了这个团队！Filip 是一个死硬的开源用户和贡献者(他最喜欢的消遣是配置他的 archlinux 设置)，Wasp 不是他工作过的第一种编程语言。

要了解更多关于他的信息以及他为什么加入 Wasp of the places，请查看他的[介绍采访](https://wasp-lang.dev/blog/2022/05/31/filip-intro)。

# 🕹️:我们正在招聘 wasp 的德弗雷尔！💾

在看到与你们所有人互动、谈论代码以及写这些电子邮件是多么有趣之后，我们决定不能自私地把这些藏在心里——这就是为什么我们决定[为 Wasp](https://wasp-lang.notion.site/DevRel-at-Wasp-dd53d9b3a8b54960b2cb93f9bdad2944) 雇佣一个 DevRel！

![](img/ea6bec60d8d778643c342bbb2047e479.png)

如果你申请 Wasp 的 DevRel 职位，这就是我们将要跳舞的方式——你真的想把它从我们这里拿走吗(也许你应该这么做)？

如果你喜欢编码，但也喜欢写作和与其他开发人员交谈，我们很乐意见到你！更多详情[请看这里](https://wasp-lang.notion.site/DevRel-at-Wasp-dd53d9b3a8b54960b2cb93f9bdad2944)，请直接回复此邮件。如果这不是你的东西，但你知道有人是谁的，请随意转发给他们。我们迫不及待地想听到你的消息！

# Wasp Github 明星成长——我们在 Github 上成为潮流！

Wasp 正在 GitHub 上的“Haskell”类别中流行——请确保[开始回购](https://github.com/wasp-lang/wasp)并让我们成功登顶！

![](img/fb6ab8a03a4c5e6e44959f27affa7606.png)

总明星数:1706——我们着火了🔥🔥！一如既往，非常感谢我们所有的[贡献者](https://github.com/wasp-lang/wasp/graphs/contributors)和[观星者](https://github.com/wasp-lang/wasp/stargazers)。

![](img/c4570087ceb60dcb7c15f00bdac6d06b.png)

**如果你还没有**，[请在 Github](https://github.com/wasp-lang/wasp) 上给我们上星吧！是的，我们是无耻的明星乞丐，但如果你相信这个项目并想支持它，这是最好的方式之一(下一步是用 Wasp 实际建造一些东西——[也去做吧](https://wasp-lang.dev/docs)！:D)。不要为我们，为莱斯利·诺普:

![](img/c2db9d8de88a8b0d63554d43fd798bb5.png)

甚至罗恩也会在 GitHub 上出演 Wasp。

[Wasp 在推特上](https://twitter.com/WaspLang) [-](https://twitter.com/WaspLang)-) 我们加强了我们的游戏，现在每天都在推特上(至少我们尝试着)！我们分享迷因、代码示例，并宣布黑客马拉松和赠品— [关注我们，了解最新动态](https://twitter.com/WaspLang)！

![](img/eae93bb9af7f28e49a9c129634ddfe64.png)

蛋糕是个谎言！(或者是🎂？)

# 开发者生活💻⌨️💽

这是我们这个月遇到的很酷的东西:

[采样器——任何 shell 命令的可视化](https://github.com/sqshq/sampler) —如果我们曾经见过很酷的 CLI 工具，这就是它。直接从终端对任何动态过程进行采样，并且在这样做的时候看起来像一个真正的 h4x0r！这实际上是接近黄蜂阿尔法测试程序的酷。

![](img/b1c0eeaa6b4a6875fbdf990300070627.png)

[fly cut——干净简单的 Mac 剪贴板](https://github.com/TermiT/Flycut) —如果你需要一遍又一遍地复制/粘贴一堆东西，你应该知道从剪贴板中丢失前一个项目是多么令人烦恼。嗯，再也不会了——有了这个保存剪贴板历史的漂亮工具，你将提高你的生产力，也成为一个更好的人(因为你会更少咒骂)。

![](img/02961c9db5535836ac8cefc78fbff66d.png)

通过按 Shift + Cmd + V，您可以在剪贴板历史中切换

[机械表——机械装置可视化](https://ciechanow.ski/mechanical-watch/)——HN 上有一个“发布互联网上最酷的页面”的话题，它确实没有让人失望。与编程本身无关，但它是下一个最好的工程。机械表内部运作的惊人互动 3d 可视化！

![](img/712f8ec9a415458ca9e331f3fe894f47.png)

你有什么建议给我们吗(音乐、装备、有用的应用/插件等等)？通过在推特上[给我们加标签让我们知道，我们会在下一次更新中包括它(当然要有适当的信用)。](https://twitter.com/WaspLang)

![](img/ec0ddbdca1ef737a431c54e05af99a51.png)

我现在必须离开，完成我的使命(制造更多的迷因)

这个月到此为止！感谢您阅读和支持我们——如果您有任何反馈或想法，或者只是想分享您最新的 swag 想法(例如[黄蜂天线头带和蜂巢眼镜](https://www.amazon.com/Antenna-Headband-Ladybug-Accessories-Halloween/dp/B09YQ52CPN/ref=sr_1_9?keywords=bee%2Baccessories&qid=1655816371&sr=8-9&th=1)？)[加入我们的不和](https://discord.gg/rzdnErX)或者点击回复本邮件！

自由飞翔，用你的触角感受风！🐝🐝
黄蜂队