# 斜率公式和斜率点公式

> 原文：<https://blog.devgenius.io/slope-formula-and-slop-point-formula-16f2496dbb86?source=collection_archive---------3----------------------->

## 带 Cinemachine 推车的移动电梯

![](img/c28cc0383e323c0e3a00119b6e1a638a.png)

为了使我的电梯适用于基于真实世界建筑的电梯，各楼层间隔均匀，我可以为每个楼层添加停靠点。我只需要第一个航点和最后一个航点在正确的地方。然后，我可以使用斜率和点斜率公式来获得地板在路径上的位置。

![](img/f83c1c6956d926144bfded326697bd88.png)

我必须确定我需要什么信息，以及如何将它可视化。我将使用 2D 图来形象化这一点。在这种情况下，Y 将是位置单位，我有 2 个必须转换的单位，归一化(0–1)和距离(0-距离的长度， *17.99999* )。

![](img/cb5b5a9a3286273d4a41e00c17f93ab5.png)

x 将会是你想要的楼层数。为了正确工作，点的数量需要与楼层的数量相同或更多，并且楼层应该均匀分布，路点不需要均匀分布。

![](img/b3ca6d73e49b3eb2bbd208de966ac002.png)

给定以下信息，我需要求解 y，因为这是我需要设置为期望位置的数字。

![](img/46316d353d5c2abf507301f537c962e5.png)

# 倾斜

为了使用点斜率，首先我需要得到斜率。这将根据我要使用的元素数量而变化。我的例子中唯一的常数是 0–1。

![](img/c4217193d13c85bd354eefb69931ee74.png)

把我的值放进公式里，我就能在两种情况下解出 M。

![](img/ea999e07178e3bdeffa3c472dd647361.png)

注意，不管 y1 和 x1 都是 0，我可以把它简化为 y 最大值除以 x 最大值。

![](img/249d782845e9d1666cedb22d10ad532c.png)

# 点斜率

![](img/805591b925aaf6d2fa5cb9ba28fad58c.png)

把我的值放入公式中，我现在可以求解这两种情况下的 y。

![](img/ddfdc56c9d0d61993c56bc27983cf38a.png)

请注意，无论 y1 和 x1 是 0，我都可以将其简化为 y = m *航路点索引。

![](img/6088bba8a1eb7eaa079cf16c4b81622c.png)

# 完成移动到地板方法

现在我需要做的就是使用斜率点来得到我想要的位置。对于 Y 最大值，我使用路径的最大值，使用选定的位置单位，对于 X 最大值，我使用路径的最大位置。对于最小值，我使用各自的最小值。

![](img/a8dfdce172f3db194fb792d9395f1c84.png)

使用距离，归一化的工作原理是一样的。

![](img/05ffe1b92dce65b900dab281468c7ebd.png)

这与路点的位置不一致。0°处的路点和最后一个路点是需要在正确位置经过的路点。

![](img/8d176e1143fa23851e962ece4ca9f3f6.png)

将第一个和最后一个路径点用在错误的位置。

![](img/bbf0d5b3ab335e2507d0f91851346a02.png)

## 使用仅具有起点和终点位置以及沿途多层的位置。

要有一个起点和一个终点，并且多个楼层间隔相等，我需要做的就是将 xMin 改为 1，将 xMax 改为楼层数。

![](img/4293ac8ffb93be5e25f36808cf75569b.png)

在 unity 使用 3 层楼进行测试。

![](img/bb49029054f20d5440f19f61b9fe45c8.png)

## 不同位置的多个楼层。

要添加多个楼层并停在它们的透视点，我需要将楼层号转换到与该楼层号对应的位置。传入的楼层号应对应一个航路点号，航路点从 0 开始，是路径单位。为了转换楼层数，我减去 1，得到正确的路点数。为了将它转换到正确的位置，我使用 Cinemachine 的内置方法 [**从路径本地单位**](https://docs.unity3d.com/Packages/com.unity.cinemachine@2.1/api/Cinemachine.CinemachinePathBase.html) **。**

![](img/9ab8e99d493d4b804adbf6f510002cd6.png)

然后，我添加一个检查，看看是否有 2 个以上的路点。如果没有，我就用斜率法来设定位置。

![](img/91ac6ad2389a776e1d30a9843dd2fee5.png)

现在我有了一部功能齐全的移动电梯，不管它是如何设置的，它都能正确地停在正确的楼层。

![](img/6223854506ae41148faec4fc668c3366.png)