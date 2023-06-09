# 在你的 Next.js 博客中添加阅读时间统计

> 原文：<https://blog.devgenius.io/adding-reading-time-stat-in-your-next-js-blog-b1ed5108a41c?source=collection_archive---------5----------------------->

![](img/316ad79c2bd0e0d3cc84b37346c9fa8c.png)

我最近开始了提高我的前端/javascript 技能的旅程。所以显而易见的方法是在我的博客上增加一些新功能。

我最新添加的是这篇文章需要你读多长时间的信息。几乎每个博客平台上都有这个，我一直想要它。

这个数字背后的理论是，人们平均每分钟阅读大约 225 个单词。所以我们需要统计文章的字数，除以 225。

所以基本代码应该是这样的:

现在我们需要统计单词。我一开始天真地用空格分割并计数。我对这个结果不太满意，因为我的文章中有很多代码，而且它把很多语法算作单词。

所以我决定按空白分割，并检查每个标记是否是一个单词。这是通过检查它是否包含一些字母数字标记来完成的。

我的实现:

我对自己的成绩很满意。我在 Medium 上交叉发布了我的大部分文章，我的结果时间和他们的结果差不多。在某些情况下，我有微小的差异，但我可以忍受。

如果你喜欢这篇文章，你可以在 Twitter 上关注我。

*最初发表于*[T5【https://ppolivka.com】](https://ppolivka.com/posts/reading-time-stat-in-nextjs-blog)*。*