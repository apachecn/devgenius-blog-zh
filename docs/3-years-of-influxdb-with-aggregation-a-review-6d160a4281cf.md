# 3 年运行 InfluxDB 与聚合—回顾

> 原文：<https://blog.devgenius.io/3-years-of-influxdb-with-aggregation-a-review-6d160a4281cf?source=collection_archive---------0----------------------->

## InfluxDB |聚合|审查|成本效益|长期存储

## 压缩数据是获得可维护的、响应迅速的系统的关键——但是这值得努力吗？

![](img/66da59251cfdaa429fcf95f5c2a63925.png)

亚当·诺瓦克斯基在 [Unsplash](https://unsplash.com/s/photos/chart?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的照片

我已经运行我自己的小 InfluxDB 实例大约 3 年了。是时候回顾一下它的性能，并回顾一下我的聚合设置的影响了。

# 聚合值得努力吗？

设置一个全自动聚合的系统需要一些努力。值得关注的一个方面是成本效益主题:

*   如果我们没有汇总数据，会发生什么？
*   如果我们仅仅储存一年呢？
*   维护聚合设置花费了多少精力？
*   我们是否因为聚合而丢失了数据？
*   聚合消耗多少资源？或者换句话说，它对数据库造成了多大的负载？

## 设置工作

设置聚合到底需要多少努力？这是一个我们必须诚实地问自己的问题。在我的案例中，我花了很多精力来开发解决方案。不过，我的 ansible 角色的实际设置非常简单。当然，这需要几天才能完成，但这仅仅是因为测试和数据的实际迁移。因此，如果幸运的话，您可以在收集数据之前设置聚合，这样可以节省您迁移现有数据的所有精力(时间)。

对于我们这里的故事，让我们假设我花了 **5 天**来设置聚合。

## 如果你没有呢？

如果几年前，我没有决定汇总我的数据，现在的情况会是什么样？让我们看一看。

下面的屏幕显示了我的 InfluxDB 实例的每个数据库的**系列的演变。你很容易看到，2018 年底，数据库摄入的系列爆炸了。原因很简单，就是更多的主机和指标。当时，InfluxDB 没有为聚合而设置。**

![](img/3849cc89dfd59eec14681c758ddffb03.png)

“每个数据库一个系列”在 3 年中的演变

当我注意到系列的大幅增长时，我有几个选择:

*   防止获取临时指标(例如 docker 容器随机名称、拼写错误的指标等)。这将减少或减缓系列数量的增长，但它们仍将持续上升。此外，在摄取期间设置和维护指标的“过滤器”与定义聚合设置非常相似。
*   在 30 天、60 天、90 天之后删除数据，当然这也是一个选择，但是我想对数据有一个长远的看法，例如能够用真实的生活经历写一篇这样的文章。在一段时间后完全删除数据确实会在一定程度上限制您的数据，因为旧的、未使用的序列最终会被删除(逐出)。
*   选择我希望长期保留的数据，并专门为它们设置聚合。这意味着努力并有意识地决定我想保留什么，以什么样的粒度保留什么。

你可以猜到聚合最终是我的选择。在开发我的解决方案的过程中，我发现需要过滤来保持历史数据中没有不需要的指标。这给维护解决方案带来了额外的开销，并可能导致您忘记列入“白名单”的指标的长期数据丢失。但最终，我并不后悔这个决定，因为向长期存储中添加数据应该始终是一个有意识的决定，因为它会带来(存储/资源)成本。

## 所以，如果我没有呢？

简而言之:我的数据库在存储方面会爆炸，在性能方面也会下降。正如我在我的责任角色示例中写的[,](https://github.com/DrPsychick/ansible_influx_downsampling/tree/master/examples/full-5level-backfill-compact#my-setup)当时数据库大小超过 9GB。想象一下，随着时间的推移，上面屏幕中的蓝线会继续下去…到目前为止，我可能需要几百 GB 的存储空间以及一台多核机器来处理长期查询(6 个月、1 年、3 年视图)。

不是一个选项，至少对我来说。

## 对数据库的影响

聚集设置对数据库有影响吗？是的，当然，总会有的。但问题是，与在需要时查询原始数据相比，这个负载有多大？

常识会告诉您，将原始数据编译成一个精简视图，然后在需要时查询精简视图会更有效。我的数据清楚地证实了这一点。让我们看一看:

在下面的屏幕中，您可以看到在我设置了聚合之后，在我的 InfluxDB 上运行的连续查询。你可以看到有很多，只是因为我的设置聚合了多个级别，我的数据库中有大约 40 个测量值。(免责声明:该图的指标并没有一直被正确收集，但我可以说的是，目前数据库每天运行 16k 连续查询)

![](img/2afffdb413ec593f6f9ed96b9c5b5b0b.png)

InfluxDB 上每天连续查询的次数—可接受的负载

## 我们丢失数据了吗？

明确的答案是肯定的！什么真的？当我丢失数据时，为什么要设置聚合？

问那个问题是合乎逻辑的，或者说是意料之中的，但这是个不该问的问题。如上所述，决定长期保留哪些数据应该是一个有意识的决定。所以说实话:在我们建立聚合的时候，我们根本没有考虑过我们当前的情况，因为我们当时不知道我们现在知道什么。克服它，如果您还想长期使用它，就将缺失的数据添加到聚合中。

## 我们失去了什么？

我丢失了我的 InfluxDB 的 CPU/内存消耗历史记录。令人遗憾的是，我无法向您展示更多关于聚合设置对数据库负载的影响。除此之外，我没有丢失长期数据的任何问题。

关于负载影响，您必须相信我:我的仪表板也能快速加载长期查询，我对我的实例消耗的磁盘、RAM 和 CPU 数量非常满意，同时让我能够在几秒钟内访问 3 年范围内最重要的指标。

## 最后，维护聚集设置的工作。

老实说，在我的情况下，维护工作可以忽略不计。再说一遍，我没有添加大量的新指标。不过，一旦设置就绪，我可以在几分钟内添加一个带有聚合定义的新指标，然后运行我的 ansible 角色将其“部署”到 InfluxDB 数据库。Ansible 将会运行一段时间，因为这个角色是通用的，并且会检查所有的度量，但是如果这变成了一个问题，那么可以将设置分成多个单独的剧本/角色，以便只处理部分度量。

# InfluxDB 内部指标

让我们来看看 InfluxDB 在过去 3 年中的一些内部指标:

![](img/535d92ac1db0ce552d6ded3cd868fffe.png)

InfluxDB 三年来的内部指标

## 我们注意到的是:

*   随着聚合的进行，堆的使用显著增加。是的，但是:我认为这在合理的范围之内，而且这是合乎逻辑的:将多个数据库加载到内存中需要更多的 RAM。2018 年堆使用量的峰值是由现有数据的迁移引起的。
*   堆消耗稳定，级数稳定。**这是重要的部分。这就是我们想要的。**我们希望有一个或多或少稳定的数据库安装。我们希望存储和内存需求或多或少可以预测。
*   3y 数据库的系列计数“不断”上升。是的，这是意料之中的。数据库还没有“满”，因为还没有 3 年前的数据。预计一旦超过 3 年的数据从 3y 数据库中清除，该系列将保持与其他数据库一样的稳定性。
*   2020 年系列涨跌。当我们通过调整聚合设置`where`子句/过滤器来添加指标和/或清理时，就会发生这种情况。
*   最常被查询的数据库“telegraf ”(当前/最近的数据)保持在 10k 系列以下，这对查询性能有积极的影响。

# 关键外卖

## 聚集设置值得努力吗？

我通常会说是的。唯一的例外是当您有意只想将数据存储很短的一段时间，如 14 天、30 天、60 天。在这种情况下，您的 60 天查询可能仍然很慢，这取决于您的数据的基数(系列数)。这可能是一个可以接受的选择，例如，当您一个月只查询一次长期数据时。

但是你自己决定吧。以下是我的要点:

## 我付出了什么代价？

*   5 天设置聚合(不包括开发和测试 ansible 角色的无尽时间)。如果您有大量现有数据要迁移，这 5 天可能会持续两周或更长时间。此外，设置的“复杂性”将显著影响您完成这项工作所需的时间。
*   偶尔检查一下配置(一个`yaml`文件)并添加主机名、指标，有时还会添加聚合查询。让我们粗略地总结为 2 周——2 年的时间！
*   为了避免在聚合中丢失指标(丢失长期数据)，设置一个流程来确保新指标总是被添加到聚合设置中。

## 我得到了什么？

*   系列，因此存储和内存需求**保持稳定**。结果，服务本身(Grafana+InfluxDB)在 2 年的时间里保持稳定！
*   仪表板的设置需要更多的工作，但是查询总是非常快。**用户体验是一流的**，因为即使是 3 年的查询也只需要几秒钟。
*   毫无疑问，我当前设置的**成本**比我在不进行汇总的情况下长期保存所有数据所面临的成本要低得多，例如，满足“长期”需求而无需投入时间来设置汇总。
*   用户在“等待数据所花费的时间”方面的**成本** **节约** **很难衡量，但当用户探索长期数据时，这一点会立即显现出来。对我来说，这个标题最好是“令人沮丧的节省”，但在我看来，这仍然是一个经常被忽视的话题:用户体验。**

![](img/153452bbf9ec3b21dd8ed4650144b342.png)

演示:通过聚合查询长期数据的速度

## 感谢您的阅读！

我的职责如上所述:

[](https://github.com/DrPsychick/ansible_influx_downsampling) [## DrPsychick/ansi ble _ inflow _ down sampling

### InfluxDB 使用默认的保留策略，将数据永久保存在 7 天的碎片中——以原始格式(每 10 分钟数据点…

github.com](https://github.com/DrPsychick/ansible_influx_downsampling) 

如果您想了解有关聚合您的 InfluxDB 的更多信息:

[](https://medium.com/dev-genius/save-90-disk-space-by-compacting-your-influxdb-838366cfa133) [## 通过压缩您的 InfluxDB 节省 90%的磁盘空间

### 加快查询速度并降低存储需求。如何用 Grafana 监控 InfluxDB 本身？

medium.com](https://medium.com/dev-genius/save-90-disk-space-by-compacting-your-influxdb-838366cfa133)