# “注意(&这篇文章)是你所需要的”:在 7 分钟的阅读中理解变压器论文的关键点。

> 原文：<https://blog.devgenius.io/attention-this-post-is-all-you-need-understand-key-points-of-the-transformer-paper-in-a-7-677d75b49353?source=collection_archive---------5----------------------->

在这篇文章中，我将带你了解注意力的概念，并解释 Transformer 架构，正如“注意力是你所需要的一切”一文中所介绍的那样。我们开始吧，好吗？

> ***先决条件:*** *熟悉神经网络+对编码器-解码器架构有大致了解。*

**从重现到关注的转变:*是什么激发了变形金刚*？**

很长一段时间，RNNs 和 CNN 是每一个表演[转导模型](https://aicorespot.io/an-intro-to-transduction-within-machine-learning/)的核心。通常，它们被用来构建一个编码器-解码器架构，其中两个部分通过一个注意机制连接在一起。然而，尽管这些体系结构性能良好，但由于其固有的顺序性，在培训方面成本很高。我会在下面的段落中解释原因。

递归模型为输入和输出序列中的每个标记分配位置。对于每个这样的位置和计算的每个时间步长 t，使用时间 t 的输入和来自前一时间步长的隐藏状态来生成隐藏状态 hₜ。

rnn 的这种顺序工作提出了一个问题，因为它使得在同一训练示例中并行化是不可能的。对于非常长的序列，由于这些模型的执行需要存储所有时间步长的一系列隐藏状态，因此会出现内存问题。

基于以上原因，《注意力是你所需要的全部》的作者介绍了 Transformer: *一种完全依赖注意力而不需要递归或卷积的架构。*

如果你想了解更多关于《变形金刚》的历史背景，Vinithavn 在她的文章[中讲述了一个引人入胜的故事。](https://medium.com/geekculture/transformers-231c4a430746)

**介绍著名变压器:其架构&组件:**

如果转换者有一个脸书帐户，下图将是他们的个人资料图片。乍一看当然不是最讨人喜欢的数字，但我马上会给你分析一下！

![](img/b0cb95a87237677b71568bcb9485c5e5.png)

变压器架构——来自“你只需要关注”

现在，让我们大胆地看一下架构，并确定我们可以从中提取哪些组件。

> 首先，该架构是一个*(由灰色方框表示)编码器-解码器的架构，其中使用了两种类型的层: ***前馈层*** (蓝色)和 ***注意层*** (橙色)。第二，输入和输出除了使用 ***位置编码*** 外，还表示为 ***嵌入*** 。一个 ***softmax*** 图层(绿色)用于获得输出。*

*下面，我将解释上面强调的每个组件。*

# *注意:*

*从技术上讲，注意力不过是一种功能；连接一个序列的不同部分的东西。实际上，键-值对和查询之间的函数映射*(键、值和查询是向量)。**

*关键字、查询和值的含义类似于它们在检索系统中的用法 *:**

*   *查询 Q 是您计算关注度的向量。*
*   *K 键是你计算注意力的向量。*
*   *值 V 类似于根据您的查询得到的最佳匹配结果。*

*![](img/c73288d7577de1066a25bdca414e524f.png)*

*成比例的点积注意力与多头注意力——来自“你只需要注意力”*

*自我注意是指当注意机制被用于*“关联来自相同序列的不同位置，以便计算序列的表示”*。也就是说，Q、V 和 K 来自相同的位置/输入序列。*

****点积注意****

*有两种常用的注意力类型:加法和乘法/逐点法。由转换器实现的乘法注意力的计算如下:*

*![](img/1afcbdb92cfa0e0692a057478c178381.png)*

*其中:*

*   *Sqrt(dk)用于缩放:怀疑 dk(Q 和 K 的维数)的值越大，点积越大。因此，后者落在 softmax 曲线的梯度接近于零的区域。*
*   *Softmax 的用途是获得 0 和 1 之间的值，以便后者可以用作权重。*

****多头注意****

*Vaswani 等人发现，与其使用单个点积注意力计算，不如使用多个头部，对相同的查询、键和值的不同线性投影执行相同的操作。*

*换句话说，本文建议使用多个这样的值，而不是为键、值和查询使用一组值。*

*多头注意力的工作方式如下:*

> *h *头部堆叠在一起。它们的输出被连接并被投影:**

*![](img/cdc50e8d78a7219e643ce614993054e3.png)*

> *头部采用的 K、Q 和 V 值稍有不同，并且首先经过一些变换。k、Q 和 V 在被馈送到每个头之前被“用不同的学习线性投影进行线性投影”*。**

*![](img/5a34f2317de64a03b65d369a39fb46d4.png)*

****为什么要多头关注？****

*上面解释的变换背后的思想是，模型将"*关注来自不同位置的不同表示子空间的信息"。*换句话说，每个人头都会得到不同版本的 Q、V、k。*

*本文[详细解释了多头注意力背后的直觉和数学原理。](https://theaisummer.com/self-attention/)*

# *编码器-解码器堆栈:*

*编码器-解码器架构是大多数竞争转导模型的核心。*

*还记得变形金刚 FB 简介图吗？编码器是该图左侧的灰色方框。*

*   *每层由两个子层组成:一个前馈网络+一个多头自关注机制。*
*   *Nx 是构成转换器编码器部分的相同层数。*
*   *使用剩余连接和层标准化。*

*除了以下修改之外，解码器层(右侧的灰色框)与编码器层相似:*

*   *解码器层有一个额外的子层:一个多头注意力子层(橙色的第二个框)，负责编码器堆栈的输出。*
*   *掩蔽被添加到自关注层(解码器底部的橙色框)，以确保解码器只关注先前的位置，而不关注后续的位置。*

# *位置编码:*

*因为没有递归或卷积，所以需要一种不同的方法来说明序列的顺序。为此，使用这些位置编码，并将其与编码器和解码器输入相加。*

*实际上，这些编码可以学习或固定。在本文中，后者是使用正弦和余弦函数实现的:*

*![](img/4779cced58a97ddb82fd2aaa262004a2.png)*

*其中:*

*   **位置*是输入的位置。*
*   **i* 是每个维度对应一个正弦曲线的维度。*

*这种位置编码选择背后的直觉是基于这样的假设，即使用正弦函数，模型将:*

*   **“轻松学会按相对位置参加”。**
*   **“推断序列长度长于训练期间遇到的长度”。**

# *嵌入、Softmax 和前馈层:*

****嵌入****

*神经网络处理数字。当处理转导模型时，嵌入是必须的，以便将输入和输出令牌转换成它们的维度向量表示 *dmodel* 。*

***soft max***

*需要 softmax 函数将解码器输出转换为概率。后者用于在给定先前建立的词汇表的情况下解释解码器的输出。*

****前馈层****

*完全连接的前馈层与 ReLU 激活功能一起使用。*

# *在变压器中使用多头注意力的 3 种不同方式:*

***编解码注意***

*查询来自解码器层，而键和值来自编码器输出，如解码器中中间的橙色框所示。这允许解码器中的每个位置关注输入序列中的所有位置。*

***编码器中的自我关注***

*这种关注由编码器中的橙色方框表示。查询、键和值都来自同一个地方，在这种情况下，是前一个编码器层的输出。*

***解码器中的自我关注***

*类似于编码器中的自我关注，查询、键和值都来自前面的解码器层。解码器底部的橙色方框代表这种类型的注意力。目标是每个解码器位置关注自身和先前的位置。*

*至此，您可以放心，您已经对“注意力是您所需要的全部”一文中介绍的重要概念有了一个总体的了解。*

*新概念的坚持可能需要一些重复(和大量的耐心)。祝你好运&学习愉快！*

*如有建议或意见，欢迎联系 [Linkedin](https://www.linkedin.com/in/imane-boudr%C3%A2-50a3a5163/) 或 [Medium](https://medium.com/@boudra.imane1) 。*

# *参考:*

*瓦斯瓦尼等人(2017 年)。 [*注意力是你所需要的一切*](https://arxiv.org/pdf/1706.03762.pdf) *。**