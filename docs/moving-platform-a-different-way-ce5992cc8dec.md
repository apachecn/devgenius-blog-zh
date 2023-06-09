# 以不同的方式移动平台

> 原文：<https://blog.devgenius.io/moving-platform-a-different-way-ce5992cc8dec?source=collection_archive---------5----------------------->

## 创建一个模块化的移动平台，并把它变成一个预制组件

![](img/53da13735ca3433b01d05cbf2537bdfd.png)

为了创建这个平台，我将使用 Cinemachine Smooth Path 作为我的路径点，就像我在本文中所做的一样。

[](/moving-platform-part-2-71b3addbc462) [## 移动平台第 2 部分

### 使用 Cinemachine 平滑路径

blog.devgenius.io](/moving-platform-part-2-71b3addbc462) 

为此，我不会使用推车，因为我不想改变平台的旋转，而是使用 [**Vector3。像我在这篇文章中所做的那样，用变换向**](https://docs.unity3d.com/2021.1/Documentation/ScriptReference/Vector3.MoveTowards.html) 移动。

[](/moving-platforms-in-unity-4d7299b2d013) [## 在 Unity 中移动平台

### 在两个变换之间移动

blog.devgenius.io](/moving-platforms-in-unity-4d7299b2d013) 

融合了两者的优点。

我创建了一个空的游戏对象来放置我的移动平台。我把我的平台预制添加进去。我通过打开可抓取的壁架并关闭普通壁架，使两个壁架都是可抓取的 **e** 。然后我添加了一个

![](img/0f52cc90491e32a23652d7208d28ba3b.png)

我从让它动起来所需的基础开始。

![](img/c8ab7fb807ec5611172d1e052cfe5122.png)

我填写更新方法。

![](img/a13cc606ac9cb1c4896e435c9f6cd4c8.png)

然后我填写下一个位置方法。为了得到下一个位置，我使用 Cinemachine 基本路径评估单位位置方法。此方法返回由给定位置单位确定的给定位置处的向量 3。

![](img/ed995e054177f04bb52d7e922a5e6719.png)

我将可移动平台作为一个组件添加到移动平台，并在检查器中设置值，然后将它变成一个预置。

![](img/c15b8fa375fe1d24919e1f6abf723022.png)

现在我已经有了一个预制品，我把可移动的平台设置到我想要的位置，并为它创建路径。

![](img/bcf819a2fc2741df790a9e409d126393.png)

现在，我通过在玩家进入平台时将玩家的父代设置为平台，并在玩家退出平台时将玩家的父代设置为 null，修复了玩家不随平台移动的问题。

![](img/d43a5c473fbf68e4c3a09635e07969bf.png)

由于触发器在平台上，而不是移动平台主对象上，我需要给移动平台添加一个刚体，这样触发器碰撞就会发生。此外，我应该使用固定更新而不是更新，我需要设置玩家的父母平台转换。

![](img/1602e41d8aae1eb7b8e78745daf5b0a1.png)![](img/f925b0d32b46a99261cadd42e401a99f.png)

同样，当玩家抓住一个壁架时，当前设置会关闭角色控制器，这意味着玩家退出碰撞器，不再随平台移动。

![](img/767a893e960b12d7f184ddb5c60ca76a.png)

要解决这个问题很简单，在把它的父对象设置为空之前，先检查一下玩家是否在抓壁架。

![](img/cae87ab6a79b204dc3b292f79b53c699.png)

将壁架抓取脚本对象添加到移动平台预设

![](img/a5d8a68370128ae971c15b3acb065980.png)

我还不得不改变平台上的箱子碰撞器触发器，它在 Z 轴上不够大，以至于在抓取壁架时与玩家发生碰撞。

![](img/c16865ab6b466dc73e364d6ca4eabe07.png)

现在我有了一个玩家可以抓住的移动平台。

![](img/eca1c9b4ddac292233f90058c11a299e.png)

我必须考虑的一件事是，玩家在抓壁架时不使用物理系统，所以我必须确保任何移动的平台都不能以玩家可能会撞到什么东西的方式移动。