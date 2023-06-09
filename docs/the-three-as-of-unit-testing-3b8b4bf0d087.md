# 单元测试的三个 A

> 原文：<https://blog.devgenius.io/the-three-as-of-unit-testing-3b8b4bf0d087?source=collection_archive---------2----------------------->

解释安排，行动，断言模式使用茉莉花。

![](img/46842795864dbabea402c3a22fbad8f4.png)

由[费伦茨·阿尔马西](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 拍摄的照片

测试是构建软件的重要部分。当涉及到生产就绪的应用程序时，我们需要有尽可能少的错误的可靠的和经过良好测试的代码。有许多方法可以用来测试你的代码。在本文中，我将介绍最流行的方法之一，单元测试。单元测试包括测试应用程序中的特定模块或代码片段。编写测试时，您可能希望遵循某种模式来编写结构良好、可读性强的测试。这就是 AAA 模式的由来。AAA 代表安排、行动和断言。这是一个很好的方法来确保我们覆盖了测试代码模块的所有方面。

**A** 调整数据的状态，为测试做准备。

**一个** ct 通过某种方法对数据执行一个动作。

一个断言，对数据采取行动的结果就是我们期望的结果。

这是在任何测试框架中使用 AAA 模式的基本流程。为了使用一个代码示例来分解这些，我们将使用 Javascript 的 [Jasmine](https://en.wikipedia.org/wiki/Jasmine_(JavaScript_testing_framework)) 测试框架。如果您以前没有听说过 Jasmine，它类似于您可能熟悉的其他测试框架，如 RSpec 和 JSpec。现在让我们写一些测试！

# 实现 AAA 模式

对于我们的例子，我们将用 Javascript 测试一个用户模型。我们的用户类构造函数将接收一个全名对象来设置它的名、中间名和姓属性。

我们的用户类包含一个方法`getFullName()`，它应该返回用户的全名。那么我们如何检查这个方法是否如它所说的那样呢？我们可以编写一个单元测试来确保我们得到正确的值。下面的代码就是这么做的！

所以我们测试套件的第一部分是`describe`方法。`describe`只是将我们正在测试的代码组合在一起。然后我们测试的`it`部分是说这段特定的代码实际上应该做什么。在这种情况下，它应该返回全名。在`it`的主体内部，我们实现了安排、操作和断言，赋予每个部分特定的职责。当 act 使用我们正在测试的`getFullName()`方法执行动作时，arrange 正在创建一个`User`类的新实例。然后 Assert 向我们保证，调用用户的`getFullName()`得到的评估结果是否正是我们想要的结果。

# 结论

AAA 模式为我们测试代码提供了简单而有效的步骤。这个模式的每一步都有自己的工作要做。arrange 步骤设置我们的数据，而 act 步骤执行测试数据所需的操作，assert 将确定对数据进行操作的结果是否是我们所期望的。