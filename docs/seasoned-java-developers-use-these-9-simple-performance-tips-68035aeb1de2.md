# 经验丰富的 Java 开发人员使用这 9 个简单的性能技巧

> 原文：<https://blog.devgenius.io/seasoned-java-developers-use-these-9-simple-performance-tips-68035aeb1de2?source=collection_archive---------1----------------------->

## 如何用 9 个简单的技巧优化你的 Java 代码

![](img/d10f45282c48d5e79bee5d9f4835eea5.png)

[由亚娜拉·www.freepik.com 创作的商业照片](https://www.freepik.com/photos/business)

Java 开发人员不关心性能或维护成本。

大部分复制了 StackOverflow 的东西。如果代码有效，就不要碰代码。有经验的开发人员不会放过这一点。

下面是编写更高性能的 Java 代码的方法。

# 1.偏好组合而非继承

合成有更多的好处，因为它不需要 vtable lookup。因为你没有很多子类，你将避免虚拟调用。

没有子类方法的方法的单调用点是单态的。它们只有一种形态，一种形状，因此被称为单形。他们有更好的表现。

一个方法的许多调用点，许多覆盖该方法的子类，都是多态的。它们有许多形状，因此得名。因为它们需要 vtable 查找，所以性能会受到影响。

最多三次覆盖不会影响性能。三次覆盖以上的所有操作都会影响性能。

考虑到 is-a 和 has-a 的关系。不要盲目地遵循这个提示，而是要把它考虑进去。

# 2.保持你的兰姆达斯短

***一天没有λ。***

保持你的兰姆达斯短。 参数越多——捕获成本越大。函数类型是在运行时生成的，它们需要捕获参数。本质上，保持做空以获得收益。

***不指非静态成员。*** 来自外部类的参数会导致一些性能损失。尽管命中率可以忽略不计，但最好不要使用非静态成员。

# 3.使用未绑定的方法引用

用这些`Class::method`代替`this::method`。后者的表现会更差。如果你喜欢静态方法引用来降低捕获成本。

# 4.根除大方法

***创造小而热的方法。避免大方法。***

***编译器内嵌小方法。*** 你要尽量给他喂小的。这符合干净代码的原则，所以这是一个双赢的局面。

*如何找到改进的方法？使用 [jarScan](https://github.com/AdoptOpenJDK/jitwatch/blob/master/jarScan.sh) 并将限制设置为 325 字节。极限指出大方法。*

# 5.首选枚举集

这是一个在`Set`中存储`Enum`值并获得更好性能的结构。

你应该更喜欢`EnumSet`而不是`HashSet`。*为什么？* `EnumSet`，由于密钥事先已知，可以用 bitset 来存储值。这使得`EnumSet`占用的空间更少，所有操作都是按位的。

# 6.学习等号和 hashCode 关系

对这些方法的无知会浪费你宝贵的时间。每次面试都会问到这些问题，所以这可能会让你丢掉一份工作。

这里有一些关于这些的提示。

***不应该有常量 hashCode。***

这将影响性能，并消除哈希的优势。假设您使用 constant 作为 hashCode。每次访问类似散列的结构都会导致冲突。这将把常数访问时间降低到线性时间复杂度。

对于 hashCode，你应该只使用不可变的字段。

不要使用可变字段来生成 hashCode。这可能会适得其反，导致奇怪的错误。你可以看看这个例子，看看记录是如何产生这些错误的。

# 7.你不应该对常量使用接口

只有常量的接口是一种反模式。 不创建接口来存储常量。或者创建内部接口来存储常数。

***用*** `***EnumSets***` ***。这些将容纳多达 64 个常数，给你更快的访问，和一个存储常数的惯用方法。***

因为接口不是密封的，所以你可以实现这个只有常量的接口。至少布洛赫是这么说的。你在实践中永远看不到这一点。但是你可以添加越来越多的常量，扩大界面。

# 8.按照预期使用断言错误

***断言错误就是错误。*** 错误应该发生。错误不是例外。

这里很好的解释了什么时候用哪个。

[来源](https://github.com/google/guava/wiki/ConditionalFailuresExplained#summary)

***抛出异常和断言错误不一样。正确对待这个问题会增加你作为开发者的价值。***

这两者之间的明显区别可以提高你的表现。你将确切地知道什么是错误，什么是异常。

# 9.不要迭代枚举值

在 Java 枚举中你会经常看到这种情况。当你出于某种原因需要所有的值时，你求助于`Enum.values()`。

你应该尝试使用`EnumSet`或`EnumMap`。如前所述，这些将有助于你与枚举。它们将比其他解决方案更具性能。

如果需要使用值，缓存它们。[基准测试显示](https://richardstartin.github.io/posts/5-java-mundane-performance-tricks#dont-iterate-over-enumvalues)对于更大的 Enums 有很大的改进。

# 外卖食品

这些都是可以有所作为的微优化。你不应该扔掉你当前的代码，而是把它们留在你的脑海里。