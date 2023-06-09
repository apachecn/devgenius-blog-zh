# Elm 中的样板代码(Rant)

> 原文：<https://blog.devgenius.io/boilerplate-code-in-elm-rant-ec22c50b58bd?source=collection_archive---------3----------------------->

![](img/d2e720f11a1592584a9d1ab9d12e6821.png)

马库斯·斯皮斯克在 [Unsplash](https://unsplash.com/s/photos/functional-programming?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的照片

虽然我喜欢用 Elm 编程，但它并不是真正的完美语言。其中一个问题是样板代码。我会在这里写下我是如何陷入现在的困境的。

作为免责声明，我还是喜欢 Elm 的，我会继续用它做我的一些副业项目。只是在某些方面本可以做得更好。

我决定在 Elm 中实现一个私人项目的前端，这样我就可以在这个过程中学习一门新的语言。我已经很熟悉 Haskell 了，我想我也会喜欢 Elm 的。事实证明这是真的，我真的很喜欢 Elm，我从来没有想到在函数式编程中编写前端代码会如此有趣。说了这么多，Elm 还是有让我很困扰的东西。

我正在从事的项目的(过于简化的)特征。

*   认证(注册/登录/注销)。其他所有功能只允许登录用户使用。
*   用户可以添加、编辑、删除和读取条目。
*   条目可能包含标签(类似于 tweets，但用户通常会为所有条目添加大约 20 个相同的标签)。
*   条目只对拥有它们的用户可见，这不是一个社交网络。
*   在标签上自动完成(最好以某种方式在本地存储所有标签)

我做了我在学习一门新语言时通常做的事情。观看一个快速视频教程，浏览文档，然后研究什么库正被用于类似的项目。

我首先看了一下 [elm-spa-example](https://github.com/rtfeldman/elm-spa-example) ，但是在实现了一些页面之后，我觉得在页面和全局状态以及消息之间有很多依赖关系。

因此，我没有试图解决这个问题，而是找到了 elm-spa。这是创建 Spa 应用程序的一个很好的工具，并且有很好的文档记录。所以我用这个工具创建了一个新的应用程序，并复制了我在上一个应用程序中完成的一些功能。

一切都很顺利，直到我开始遇到 elm-ui 的问题。对于我需要的用户界面来说，它的限制太多了。由于 elm-spa 默认使用 elm-ui，现在对我来说转移到 elm-css 很难也没有意义。

我放弃了使用代码生成工具，开始了一个新项目。我复制了到目前为止我所做的可重复使用的代码片段，并开始创建我自己的结构。我从实现功能到重构整个代码库经历了很多次，直到我想出一个我现在所在的结构。

此时，我将我的项目分成了四个目录:页面、组件、元素、实用工具和类型。Elements、Util 和 Types 中的每个文件都与其他所有文件分离。它们是独立的，如果需要的话，我可以把它们转移到新的库中。组件依赖于元素、实用工具和类型，而页面依赖于组件、实用工具和类型。每个组件和每个页面都是独立的，它们对其他组件/页面一无所知。例如，如果我想让两个页面一起对话，我需要在 global (Main.elm)中这样做，类似于同步两个输入字段以获得相同的值。

最后我谈到了主要问题。样板代码。此时，项目一半的代码都是样板文件。

这在榆树似乎是不可避免的。每次添加页面时，我都需要在全局模型中添加一个字段来保存它的状态。在全局消息中添加一个子类型，并调用它的更新函数来处理这种情况，创建它的自适应函数，这些函数基本上是从其他类型的每个函数复制而来的。

我目前最大的问题是，我仍然必须重构这么多代码来为系统添加新的功能。现在，您可以从页面发出 HttpRequests 并存储到 LocalStorage，但是我想添加 IndexedDB 功能，我需要再次重构整个代码库。现在有太多的代码，这将花费很多时间。

我将不得不为这些在未来建立一些代码生成器，但即使它将解决这个项目的问题，它将很难被重用。类似于 elm-spa 工具。在 Haskell 中，使用类可以很容易地解决这个问题。

如果我有意愿这样做，我会再重写一次代码来处理 IndexedDB，这一次如果我想添加类似的功能，就可以很容易地添加“插件/插件”。我怀疑这将是一个通用的解决方案，但其他问题将在未来出现，需要实现与我现在拥有的不同的流程，这将需要重新重写整个事情。我只是希望到那时 Elm 能够提供类或者其他类型的泛型。