# Tableau 中的交换图表

> 原文：<https://blog.devgenius.io/swap-charts-in-tableau-cfaa842f8293?source=collection_archive---------10----------------------->

教程创建下拉菜单并选择特定图表。

![](img/e4e368027519a59e9e8bc7842ea1d23b.png)

# 目录

> [简介](#76ee)
> 
> [创建图表](#59a2)
> 
> [创建仪表板](#a324)
> 
> [创建参数](#21a3)
> 
> [创建计算字段](#dfad)
> 
> [饼状图的问题](#0b22)
> 
> [饼状图解决方案](#6f06)
> 
> [结论](#8540)
> 
> [视频教程](#a283)

# 介绍

一个好的视觉效果应该为用户提供方便，交换图表是一个选择。在本教程中，我将讲述如何创建一个下拉菜单。

网上有很多文章可以用来交换 Tableau 中的图表。然而，他们中的大多数人从来没有展示出全貌。让我们从 Tableau 中的**交换图开始**

# 创建图表

让我们创建一些图表进行演示。

![](img/3eb03d93c5312b10af40206eaaf48419.png)![](img/7bcc7a04005b1c6287dc7b55fe22f442.png)![](img/1264dc3df1fc3469e6074e9fa3f7aa0c.png)

# 创建仪表板

让我们创建一个仪表板来保存这些图表。

![](img/e91acd3fa5c1fef5d807d2f1b3d279a8.png)

> 我们拖进来一个:
> 
> 1.仪表板标题的文本容器
> 
> 2.容纳图表的垂直容器

然后，将图表放入容器中。

![](img/2b01eab4f7e05d9fce9cf1f9e185f80e.png)

*   *注意:在这里调整图表高度很有诱惑力。请不要触摸大小，否则你会固定图表的高度，这个技巧不会起作用。如果您不小心调整了高度，请取消选中图表中的固定高度选项。

![](img/f637cc2dbb7533bf8c9cb1d9ef9a5723.png)

# 创建参数

接下来，让我们创建一个参数来创建一个交换图表下拉列表。

![](img/d100e88bf37226e2242be986f2586d74.png)![](img/17550b735c321f4ea7a87415e1af1544.png)

按照红框配置参数设置。

![](img/1ea2907a6007dce9e38302d7656dd108.png)

选中显示参数选项以显示下拉列表。

# 创建计算字段

创建计算字段来存储参数。

![](img/be013c1af1e6e710f80666026ee8941c.png)![](img/2a416ffdb457b4fd119d28124bf28a8a.png)

将参数拖到计算字段中。

![](img/8b8509e07d2e856541f9a1c52d2e3cf7.png)

然后将其拖入过滤器。

![](img/7c760b378777fa6f826e6334f87b737a.png)

我们希望手动将过滤器选项添加到过滤器中。因此，我们手动将选项键入过滤器，然后按 Ctrl + Enter。请注意，我们希望对所有图表的图表名称重复这一操作。也就是说，我们为条形图键入 All & Bar Chart，为折线图键入 All & Line Chart，为饼图键入 All & Pie Chart。

![](img/ce0781fc9ba1caa0d225ea0779c43e5d.png)

然后，让我们转到我们的控制面板，显示交换图表下拉列表。只要您取消选择固定高度选项，这应该可以工作。

# 饼状图的问题是

这个问题不仅仅适用于饼状图。这也适用于行/列架中没有药丸的所有图表。

![](img/aa6a3fb175a06201f02a94edd27400ef.png)

让我们重复这些步骤，将图表切换到包含两个饼图的仪表板。

![](img/8265b5b66d9f30ff1bc49e2d43f113c4.png)![](img/db9e64a2fb21e71df5fca64eac129ea0.png)![](img/18410cf94d7c3ceae5b2a1e4cad69467.png)

当选择饼图 2 时，将会有空白空间，饼图 1 不会填满该空间。

# 饼图解决方案

![](img/4173b2e3900c75cfbeb88d4933cc6540.png)![](img/7d9a74996e38186de5ec3689867d8694.png)

对于这两个饼图，我们在行/列架中创建一个虚拟字段。然后取消选中“显示标题”选项。

> * *双击 Rows shelf 并键入“”，然后按 Enter 键。

只要您对两个饼图都做了这一步，交换图下拉列表就应该工作得很好。

![](img/2a8658b4f2184645d93d0a63cc6de624.png)

# 结论

创建交换图表下拉列表时需要注意的两个重要事项。

> 确保容器中的所有图表取消选中“固定高度”选项。
> 
> 确保容器中的所有图表在行/列架中至少有一个药丸，即使您必须创建一个虚拟字段。

好了，今天的文章就到这里。如果你觉得有帮助，请与你的朋友/同事分享。下一篇文章再见。

如果你喜欢视频教程，可以在我的 YouTube 频道上看看这个视频。考虑订阅我的频道和媒体来获得更多这样的教程。干杯！

# 视频教程