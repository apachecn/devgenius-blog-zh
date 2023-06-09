# 在 OpenGL 中完成游戏

> 原文：<https://blog.devgenius.io/completing-a-game-in-opengl-f4421f069fce?source=collection_archive---------23----------------------->

## 一个简单的滑动拼图教会了我如何编码。

![](img/70e0ba68cba8f2afb76a92c8a7e6abfc.png)

Youtube: [在 OpenGL 中完成一个游戏](https://youtu.be/I3Mqp311UOw)

这一切都是从一个假期开始的，在那里我应该放松一下。我刚刚为我的上级完成了一个困难的项目，我准备做的最后一件事是更多的工程。虽然，我从来不是那种能够长时间坐着放松的人。我总是给自己找些事情做，这个假期也不例外。我发现繁忙的工作只能到此为止。我很快发现自己很无聊，没有任何实质性的事情可做。它让我发疯。

然后我所有问题的解决方案出现了。一个简单但恼人的滑动难题。目标是什么？从 1 到 15 排列数字，什么也不做，只是通过一个整体缺口的滑块交换数字。这很烦人，但是我喜欢它所需要的技巧，我一天至少解决 15 次。我开始快速运行这个难题，以计算出我能解决它的最佳时间，达到远低于 2:30 的数字。假期结束时，我知道我要为下一个编码项目做什么。

我想挑战自己。在过去的几年里，我一直在使用 C++中的 OpenGL 来制作定制的游戏引擎——尽管，我当时非常新手，无法学习设计结构来拯救我的生活。我想用 OpenGL 做一些可以被认为是游戏的东西。为了让事情变得更难，我决定使用 C 语言可能是这个项目的一个有趣的组合。

我开始了我的旅程，很快找到了我想引入程序的每一个理念:除非必要，否则没有运行时分配，没有扩展数组，所有 C 程序员使用的甜蜜果酱。到第一天结束时，我对 C 感到沮丧，但我的努力工作有所表现。

在接下来的几天里，我更加努力地让我的解决方案运行起来，制作一个真正的游戏。我让纹理工作，并开始实现一个基于网格的点击算法。它花了一些时间来工作，直到今天，由于正交相机投影，它只能以 1:1 的纵横比工作，但我没有时间了，有更大的问题要担心。当我最终得到正确的纹理渲染和运动实现时，我添加了一个获胜条件。我终于在自己的引擎上完成了我的第一个游戏。

![](img/c627b1b256e9f3b2280398fd538a4aab.png)

完整的游戏

虽然我的游戏只有我希望实现的 10%的功能，但考虑到时间框架，它仍然给了我和原来的拼图一样的快乐。当你做了一个错误的交换时，笨拙的动作和失望和现实生活中的感觉是一样的。这是一项既有趣又锻炼大脑的活动。

对我来说重要的是，在多年的引擎创作之后，我能够制作一款游戏。如果我使用现成的引擎并在几分钟内完成这个“原型”，这个游戏对我来说就不会这么好了。从头看到尾，让我完全控制了整个系统。我再也不想回到发动机，因为我渴望它，这是不现实的。我建议每个人挑战自己的思维，如果你也负担得起，尽量不要使用引擎，你可能从来没有意识到一个预装的引擎会阻碍你多少。

代码:[十五](https://github.com/Untiied/Fifteen)