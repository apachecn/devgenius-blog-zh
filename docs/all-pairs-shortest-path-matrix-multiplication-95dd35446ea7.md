# 所有对最短路径矩阵乘法

> 原文：<https://blog.devgenius.io/all-pairs-shortest-path-matrix-multiplication-95dd35446ea7?source=collection_archive---------3----------------------->

![](img/fc8a7af0f2fb7087a3e27764a7d7cf57.png)

你将看到一个图表，你的目标是使用动态规划找到所有的最短路径对。

![](img/25c38af45f7d1a961bb70463662d23e4.png)

第一步是创建一个矩阵，其中行数和列数等于顶点数，然后用初始数据填充它。对于一跳可到达的每个顶点，您将用边权重填充它。如果一个顶点不能一跳到达，你将用无穷大填充它，如果一个顶点试图到达它自己，你将用零填充它。让我们通过算法来填充初始矩阵。

![](img/70119983a65e59cf223c06c3faa1170f.png)

我们将从填充所有的零开始。零会在对角线的下方。为什么？查看 A *1* (1，1)的第一个条目，您正试图从顶点 1 到顶点 1。那东西有多重？零。对于(2，2)，(3，3)和(4，4)也是如此。

![](img/b8a43828940e0c5a2f2c5b8d0ce71399.png)

接下来让我们来检查一个 *1* (1，2)。一跳就可以从顶点 1 到 2。边权重为 10。

![](img/7b152d42b1776d38f6c0122739256215.png)

接下来，我们来看看 A *1* (1，3)。因为你不能从顶点 1 一跳到达顶点 3，所以你输入无穷大。

![](img/de3f207cbcf788f8bed669d70c41ea95.png)

让我们填写其余的字段。

![](img/36e50409cb82979db9718ca757cac018.png)

*   从 1 到 4，A *0* (1，4) = 5
*   从 2 到 1，A *0* (2，1) = ∞
*   从 2 到 3，A *0* (2，3) = ∞
*   从 2 到 4，A *0* (2，4) = 9
*   从 3 到 1，A *0* (3，1) = -2
*   从 3 到 2，A *0* (3，2) = 4
*   从 3 到 4，A *0* (3，4) = ∞
*   从 4 到 1，A *0* (4，1) = ∞
*   从 4 到 2，A *0* (4，2) = -3
*   从 4 到 3，A *0* (4，3) = 1

![](img/84ee2170ccc8a269a8c76fbcf15ea36d.png)

接下来，让我们从编程和可视化的角度来看这个算法。

![](img/8a56116dfd31eee517a0e0f72d8249fc.png)

我们首先尝试获取 A *0* (1，1)的值。如果我们遵循 for 循环，k 将等于 1，然后 2，然后 3，最后 4，而 I 和 j 的值不变。

![](img/c14caf296d9192042e403499f34c9a22.png)

接下来，插入这些条目的值。

![](img/77efde4b9aedc596e25674cf43f23d3f.png)

最小值为 0。因此，我们取零值，并将其插入到一个 *1* (1，1)中

![](img/fed10eee166881af0c18ae03d0987fc3.png)

接下来，我们将检查 A1(1，2)，但这次我们将直观地进行检查。我们在前面的例子中所做的是遍历与条目对应的行和列。因为我们查看了条目(1，1)，所以我们将第一行和第一列的值相加，然后得到这些条目的最小值。让我们从突出显示第一行和第二列开始，因为我们正在处理 entry (1，2)。

![](img/84100ae20a9e4dbff439890dad323de0.png)

如果我们遍历该算法，我们将(1，1)加到(1，2)、(1，2)加到(2，2)、(1，3)加到(3，2)和(1，4)加到(4，2)。

![](img/f4ca52c8bf9776455ef79f4eda8f9b28.png)![](img/cfd6b73a30e38ebdf660f4b0587c88e3.png)

最小值是 2，所以我们用 2 来更新 A *2* (1，2)。

![](img/9974bdc213c81107ada8e8bee45b093a.png)

让我们也为第一行可视化地填写其余的单元格。接下来是 A2(1，3)。

![](img/f0d32685da6c3fa030cb70ff849c080f.png)![](img/0fb801e07ede62509eb59e3f9e79ec5a.png)

最小值是 6，所以我们用 6 来更新 A *2* (1，3)。接下来是 A *2* (1，4)。

![](img/803a545253ff8ad3537657d6ea68c354.png)![](img/429994d80f80adecd1db94bafa1a96ca.png)

最小值是 5，所以我们用 5 来更新 A *2* (1，4)。接下来是一个 *2* (2，1)。

![](img/27bab3b358fc5f48d329a71ef4aab6dc.png)

值仍然是无穷大，所以我们用∞更新 A *2* (2，1)。接下来是一个 *2* (2，2)。

![](img/a8aec93eeefbc18af70ec56f7c760b48.png)

对于构建一个 *2* 的迭代的剩余部分，我将列出项目，您可以通过矩阵 A *1* 来验证它们。

![](img/a149323045f50452cba71ad128a46390.png)![](img/e1bbf93b708450c40b7bc938722ddaad.png)

最终产品如下所示:

![](img/dbceb88802b3bf5e70e6ea135c9ac058.png)

我们不断重复这个过程，直到我们能够观察到两种情况之一:

*   从先前矩阵到当前矩阵的条目不会改变
*   对角线上有一个负值。这表示一个负循环，数值将无限下降。

A *2* 矩阵到底是什么？它是两个 A *1* 矩阵的修正矩阵乘法的结果。要查找的下一个矩阵是一个 *4* 。这将通过两个 A *2* 矩阵相乘来实现。让我们来看一下整个过程。

![](img/316adecfec8bb3cc2f991bc64fa20b01.png)![](img/f7d8ed0eae056bdfc1a8d2553f9c5c7a.png)

由于矩阵与之前的版本不同，我们还没有完成。移动到 A *8* 的时间到了。

![](img/f4e9d91fcce20d165e11422406230f02.png)![](img/43d009654661cd848410566df0bf880f.png)

因为 A4 和 A8 之间没有变化，所以不需要进一步的操作。

*如果你喜欢你所读的，看看我的书，* [*算法说明*](https://www.amazon.com/Illustrative-Introduction-Algorithms-Dino-Cajic-ebook-dp-B07WG48NV7/dp/B07WG48NV7/ref=mt_kindle?_encoding=UTF8&me=&qid=1586643862) *。*

![](img/5e38f6820278def014d5c1c3b24b094c.png)

迪诺·卡希奇目前是 [LSBio(寿命生物科学公司)](https://www.lsbio.com/)、[绝对抗体](https://absoluteantibody.com/)、 [Kerafast](https://www.kerafast.com/) 、[珠穆朗玛生物科技](https://everestbiotech.com/)、[北欧 MUbio](https://www.nordicmubio.com/) 和 [Exalpha](https://www.exalpha.com/) 的 IT 负责人。他还担任我的自动系统的首席执行官。他有十多年的软件工程经验。他拥有计算机科学学士学位，辅修生物学。他的背景包括创建企业级电子商务应用程序、执行基于研究的软件开发，以及通过写作促进知识的传播。

你可以在 [LinkedIn](https://www.linkedin.com/in/dinocajic/) 上联系他，在 [Instagram](https://instagram.com/think.dino) 上关注他，或者[订阅他的媒体出版物](https://dinocajic.medium.com/subscribe)。

阅读迪诺·卡吉克(以及媒体上成千上万的其他作家)的每一个故事。你的会员费直接支持迪诺·卡吉克和你阅读的其他作家。你也可以在媒体上看到所有的故事。