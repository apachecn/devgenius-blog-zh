# 贝尔曼-福特算法直观解释

> 原文：<https://blog.devgenius.io/bellman-ford-algorithm-visually-explained-e940b6edb00a?source=collection_archive---------4----------------------->

![](img/860e9fc51dbfed1fddbbc5968079f020.png)

贝尔曼-福特算法寻找从源顶点到有向图中每个顶点的最短路径。与 Dijkstra 的算法不同，Bellman-Ford 可以有负边缘。

![](img/35f9182d305883a82703efd02f586049.png)

首先，所有出站边都按字母顺序记录在一个表中。

![](img/c6a30667af98fea938b95e7637ad7567.png)

像 Dijkstra 的算法一样，创建一个记录到每个顶点的距离和每个顶点的前身的表。除了源顶点之外，每个顶点的距离都被初始化为无穷大。距离用变量 d 表示，前任用变量π表示。

![](img/acf9c9d3cf64595825388e32168b77f6.png)

贝尔曼-福特算法将遍历每条边。因为有 9 条边，所以最多有 9 次迭代。在每次迭代过程中，放松特定的边。在第一次迭代中，从 A 到顶点 C 的代价是-3。从源到 A 的当前距离是无穷大。当-3 加到无穷大时，结果是无穷大，所以 C 的值保持无穷大。类似地，从 A 到 E，成本是 2，然而，由于到 A 的距离是无穷大，E 的值保持无穷大。看看边 B-F，C-B，C-H，F-G，G-B 和 H-D，我们可以看到它们都产生相同的结果，无穷大。最后一条边 S-A 产生了不同的结果。边 S-A 的权重是 5。目前到 S 的距离是 0，所以 S 到 A 的距离是 0 + 5 = 5。A 的前任设置为 s，第一次迭代后，贝尔曼-福特找到了从 s 到 A 的路径。

![](img/a8d1cf7fe294a9eb44f5c9a87885fb8d.png)

因为所有的边都被放松了，贝尔曼-福特开始第二次迭代。尽管每条边都是松弛的，但唯一重要的边是来自 S 和 A 的边，因为到这些顶点的距离是已知的。到所有其他顶点的距离是无穷大。查看包含边的表，我们从放松边 A-C 开始。

![](img/96fe211fe01e167896cab741fa6aee98.png)

边 A-C 的权重是-3。通过边 S-A 到顶点 A 的当前距离是 5，所以到顶点 C 的距离是 5 + (-3) = 2。C 的前身是 A，边 A-E 的权重是 2。通过边 S-A 到 E 的距离是 5+2 = 7。E 的前身更新为 a。边 B-F 还不能放松。

![](img/76e10043a95304ff19d106efccee247f.png)

边 C-B 可以放松，因为我们知道到 C 的距离。到 B 的距离是
2 + 7 = 9，顶点 B 的前身是 C。边 C-H 可以放松，因为我们知道到 C 的距离。到 H 的距离是 2 + (-3) = -1，顶点 H 的前身是顶点 C

![](img/b9bea5cb05f6bf6f6e256b830fe1b7e7.png)

边缘 F-G 还不能放松。边缘 G-B 不能放松。边 H-D 可以放松，因为我们知道到顶点 H 的距离是-1。到顶点 D 的距离是-1 + 1 = 0，到顶点 D 的前任是顶点 h。

![](img/f2089086155792697fb43ba223275f01.png)

从边 S-A 到 A 的距离已经是 5，因此不需要更新。这结束了迭代 2。

![](img/971d272db9e5c5ce4fd22973af466b1c.png)![](img/a75859f54e016c2eb90db029008286aa.png)

在第三次迭代中，贝尔曼-福特算法再次检查所有的边。边 A-C 和 A-E 产生相同的结果。边缘 B-F 现在可以放松了。到 B 的距离是 9，所以到顶点 F 的距离是 9 + (-5) = 4。F 的前身是 b。

![](img/66cdb87aabe6f5c18b29b5c11e43a4ad.png)

边 C-B 和 C-H 产生相同的结果，因此表保持不变。边缘 F-G 现在可以放松了。到顶点 F 的距离是 4，所以到顶点 G 的距离是 4 + 2 = 6。G 的前身是 f。

![](img/ab6758a05feaa060aed835caf960d743.png)

边缘 G-B 现在可以放松了。到顶点 G 的距离是 6，所以到 B 的距离是 6 + 4 = 10。因为通过边 C-B 可以用更短的距离到达顶点 B，所以表保持不变。

![](img/fdb46c80671e078de8c1e6fb2158e016.png)![](img/17f6801c68984f668213ac47a920621f.png)

在第四次迭代中，检查所有的边。该算法发现没有变化，因此该算法在第四次迭代时结束。

如果这个图有一个负循环，在迭代重复 n-1 次后，理论上贝尔曼-福特算法应该已经找到了到所有顶点的最短路径。在第 n 次迭代期间，其中 n 代表顶点的数量，如果存在负循环，到至少一个顶点的距离将改变。让我们看一个简单的例子。

![](img/ddd3966eb5261bfb79891ebfbed72199.png)![](img/77bf976972453a4822d8c17027baffcf.png)

构建具有距离和前辈的表。顶点 A、B 和 c 的距离被初始化为无穷大。到 S 的距离为 0。

![](img/e5afad4653ef817e2b31ae0f85f91bd5.png)

看第一条边，A-B 还不能放松，边 B-C 和边 C-A 也不能放松，边 S-A 可以放松。到 S 的距离是 0，所以到 A 的距离是 0 + 3 = 3。A 的前身是 s。

![](img/9b0e3b1587b3db728345233ac24fd560.png)

Edge S-B 也可以放宽。到顶点 B 的距离是 0 + 6 = 6。顶点 B 的前身是 s。

![](img/6b82c414db8e07fdea29ec13ed6de79a.png)![](img/e882193902f57d12b8c66b914f16f56b.png)

第一次迭代完成。在第二次迭代中，再次检查所有的边。

![](img/f25a8fd32b74cdf47d78e3e1f7e873b2.png)

边缘 A-B 可以在第二次迭代中放松。到 A 的距离是 3，所以到顶点 B 的距离是 3 + 5 = 8。因为到 B 的距离已经小于新值，所以保留 B 的值。6 + 2 = 8 可以达到边 B-C。顶点 C 的前身是顶点 b。

![](img/c855940482eaeaad7336eb61497a173b.png)![](img/a604e88ea5e2ca752caa70b6b7837ea8.png)

接下来检查边 C-A。到 C 的距离是 8 个单位，所以到 A 的过孔边缘 B-C 的距离是 8 + (-10) = -2。因为到通孔边缘 C-A 的距离小于到通孔 S-A 的距离，所以到 A 的距离被更新。

![](img/30cf4ba687beeb3fea8d1ed9a30e5d88.png)![](img/78a25015770b221a75e9f484431e7a17.png)

边 S-A 和 S-B 不会产生更好的结果，因此第二次迭代完成。第三次迭代开始。

![](img/2d5d5142b45b5502a650f321a3d6ce66.png)

边缘 A-B 是放松的。到 A 的距离目前是-2，因此通过边 A-B 到 B 的距离是-2 + 5 = 3。由于通过 A-B 到 B 的距离小于到 S-B 的距离，因此距离更新为 3。顶点 B 的前身更新为顶点 a。

![](img/4ce747095262ac7f6dd5d33541d73561.png)

接下来放松边缘 B-C。当前到 B 的距离是 3，所以到 C 的距离是
3 + 2 = 5。到 C 的距离更新为 5。

![](img/f9c1506bb352ce54354bdd000b7fa942.png)

边缘 C-A 是放松的。到 C 的距离是 5 + (-10) = -5。到顶点 A 的距离更新为-5 个单位。

![](img/07333144b423746fefc15e2bcec6cc35.png)

边 S-A 和 S-B 不会产生更好的结果。此时，应该已经找到了所有最短路径。如果我们检查另一个迭代，应该没有变化。

![](img/a604b3c794b95b88397d6afaad5ac30c.png)

边缘 A-B 是放松的。到 A 的距离是-5，所以到 B 的距离是-5 + 5 = 0。到 B 的距离更新为 0。因为值在第 n 次迭代时改变，所以值也将在第 n+1 次迭代时改变；价值观将继续无限变化。如果我们仔细观察这个图，我们可以看到 A-B-C 产生了一个负值:5 + 2 + (-10) = -3。

如果你喜欢你所读的，看看我的书，[](https://www.amazon.com/Illustrative-Introduction-Algorithms-Dino-Cajic-ebook-dp-B07WG48NV7/dp/B07WG48NV7/ref=mt_kindle?_encoding=UTF8&me=&qid=1586643862)**算法的说明性介绍。**

*![](img/d3a9f579317fbdafd4992518ca12a4b7.png)*

*Dino Cajic 目前是 [LSBio(寿命生物科学公司)](https://www.lsbio.com/)、[绝对抗体](https://absoluteantibody.com/)、 [Kerafast](https://www.kerafast.com/) 、 [Everest BioTech](https://everestbiotech.com/) 、 [Nordic MUbio](https://www.nordicmubio.com/) 和 [Exalpha](https://www.exalpha.com/) 的 IT 负责人。他还是我的自动系统公司的首席执行官。他有十多年的软件工程经验。他拥有计算机科学学士学位，辅修生物学。他的背景包括创建企业级电子商务应用程序、执行基于研究的软件开发，以及通过写作促进知识的传播。*

*你可以在 [LinkedIn](https://www.linkedin.com/in/dinocajic/) 上联系他，在 [Instagram](https://instagram.com/think.dino) 上关注他，或者[订阅他的媒体出版物](https://dinocajic.medium.com/subscribe)。*

*阅读 Dino Cajic(以及 Medium 上成千上万的其他作家)的每一个故事。你的会员费直接支持迪诺·卡吉克和你阅读的其他作家。你也可以在媒体上看到所有的故事。*