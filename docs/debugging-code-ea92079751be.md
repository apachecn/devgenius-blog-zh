# 调试代码

> 原文：<https://blog.devgenius.io/debugging-code-ea92079751be?source=collection_archive---------19----------------------->

![](img/5d579b6c9f6fb3ce8d8c2c5022734173.png)

蒂莫西·戴克斯在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 拍摄的照片

调试被定义为在代码库中定位和纠正错误的过程。

通常，我们会从考虑所有可能的原因开始，然后测试每一个假设(从最有可能的开始)，直到发现最终的根本原因。然后我们修复它，并确保它不会再次发生。没有快速修复 bug 的方法。这通常需要结合使用谷歌搜索、记录我们的代码、交叉引用我们的逻辑和实际发生的事情。

虽然有许多工具可以帮助调试，但是使用它们并不总是最困难的部分。困难的是真正理解你遇到的错误并理解对它们的最佳解决方案。

> **“调试比一开始写代码难两倍。**因此，如果你尽可能聪明地编写代码，从定义上来说，你没有足够的聪明去调试它。”
> 
> ——布莱恩·w

# 调试心态

当考虑一个优秀的程序员需要具备哪些品质时，一个词浮现在脑海中:气质。如果说调试是编程的关键，那么拥有耐心和逻辑气质就是调试的关键。想想《星际迷航》里的斯波克。有些人天生就有这种气质，在学习编程的时候会很有用。有的人没有，要学会培养这种气质。天生聪明是有利的，但大多数人有足够的智力成为应用程序开发人员；他们需要改进的是在面对问题时培养一种系统的、耐心的气质。

# 读取错误消息

当你遇到一个错误时，你最有可能面对的是一大堆看起来不连贯的废话。这面胡言乱语的墙被称为堆栈跟踪，它对于确定从哪里开始调试至关重要。您必须习惯的第一件事是仔细阅读错误堆栈跟踪。错误消息嵌入在堆栈跟踪中。错误消息中会包含第一个提示，提示在哪里查找。这可能看起来是一个愚蠢的建议，但是你会惊讶有多少程序员没有仔细阅读错误消息，而是用脑海中出现的第一个想法对错误做出反应。

秘诀是训练你的眼睛寻找堆栈跟踪的相关部分，随着时间的推移，你将能够越来越快地发现错误。每种语言和库都有一个独特的堆栈跟踪模式，所以你使用一种语言或库越多，它就会变得越容易。如果第一次看到大量堆栈跟踪，不要气馁。仔细检查，尽量提取相关信息。

# 调试资源

*   谷歌——如果你不理解错误信息或者不知道为什么会出现错误信息，最好的第一步是谷歌一下。编码的许多令人惊奇的方面之一是庞大的在线社区。几乎可以肯定的是，有很多人遇到了和你一样的错误，他们已经解决并解释了这个问题，这样其他人就不必这么做了。
*   文档——当学习新东西或处理错误时，首先要检查的应该是官方文档。对于任何给定的工具，官方文档通常是最全面和最新的信息来源。浏览如此多的技术信息有时会令人厌烦或不知所措，但从长远来看，这可以节省时间。
*   Stack Overflow——Stack Overflow 是一个程序员可以提问和回答问题的网站。这是堆栈交换网络的旗舰网站。在 Google 中搜索时，经常会出现栈溢出的答案，但是如果其他答案都丢失了，你可以直接在栈溢出上提问。

# 调试步骤

每个人最终都会开发出自己的调试风格，但是要开始调试，您可以遵循下面概述的一般步骤:

1.  重现错误——找到可靠地重现问题的方法，这很有帮助，因为这意味着你可以与他人分享这个问题，并希望从他们那里获得一些有用的反馈。同样，在重现错误的过程中，您可能首先会发现为什么会发生这种情况。
2.  缩小问题范围——随着代码库规模的增长，分析每一行代码来寻找 bug 将变得很困难。因此，分而治之是个好主意，从最有可能产生问题的领域开始搜索。我们试图修改数据或代码，以确定错误的范围和问题的界限。这将使我们更好地了解问题，并实施更好的解决方案。大多数问题可以通过多种方式解决，你对问题理解得越透彻，你的解决方案就越全面。
3.  实施修复——一旦我们确定了错误的来源，并利用我们对问题的新认识，我们就可以实施修复，希望能阐明问题。要记住的一个关键点是一次只解决一个问题。在实施修复时，发现新的边缘情况或问题是很常见的。抵制同时解决多个问题的冲动。
4.  测试修复——唯一比解决一个困难的 bug 更令人沮丧的事情是修复了它却发现 bug 仍然存在。更糟糕的是,“解决方案”可能会在您的代码中引入额外的错误。测试代码以避免这种情况非常重要。如果你能用自动化的单元测试来做就更好了。理想情况下，代码库的每个部分都应该有自己的测试集。每当代码库发生变化时，都应该运行这些测试。这样，如果测试写得正确，我们可以在新的 bug 出现时就检测出来。当然，这使得识别和解决问题变得更加容易。

# 调试方法

## 逐行

你的耐心是你最好的调试工具，这也是我们在本文中首先提到气质的原因。代码中的大多数错误都是由于忽略了一个细节，而不是完全误解了一个概念。

作为一名程序员，你最强大的能力是谨慎、耐心，并养成逐行、逐词、逐字符阅读代码的习惯。如果你天生缺乏耐心或者喜欢掩饰细节，你必须训练自己在编程时表现得与众不同。如果你不注重细节，再多的调试建议或工具也帮不了你。

## 橡皮鸭

处理这个问题的一个好方法是一行一行地检查你的代码，边读边解释。橡皮鸭技术是一种流行的方法；这个名字来源于向一只橡皮鸭解释你的代码的实践。

目标是强迫你自己阅读你的代码，而不是假设你知道它做什么。这允许您将您头脑中的逻辑与代码中实际发生的事情进行比较。对我们来说，做出假设而不密切关注每一行代码只是人类的天性。这是一种让我们节省能源、更快完成工作的机制。但是，在调试的时候，一定要强迫大脑配合，尽可能的出现在每一行代码上。

## 休息一下

很多时候，在找到解决方案之前，您必须与错误斗争几个小时(或几天)。在我看来，在这些场合注意你的精神状态是至关重要的。编程主要是一种脑力活动。所以你的大脑在给定时间的工作方式，或者你的感受，将会直接影响你的代码外观和你有效解决问题的能力。如果你花几个小时阅读、大声重复相同的代码行、搜索、检查堆栈溢出问题，而你的代码仍然失败，你会变得沮丧，并开始给自己施加压力。当你尝试不同的解决方案并反复失败时，你对细节的关注可能会减弱，你会开始跳到不同的想法并同时尝试许多事情。

当你达到这一点时，最好去散步或干脆不去管它，直到第二天。专注、充分休息和放松是编写好代码和有效修复 bug 的关键。努力工作和耗尽精力之间的界限很模糊，但我们必须注意这一点，并在需要的时候休息一下。

# 结论

调试过程需要极大的耐心和冷静的头脑。但是，通过系统地分析问题，我们最终可以找到错误的根源，并加以纠正。这是对调试概念的介绍，并不详尽。掌握调试基础知识后的下一步是学习使用成熟的调试工具(例如 pry for Ruby ),但这是另一篇文章的主题。