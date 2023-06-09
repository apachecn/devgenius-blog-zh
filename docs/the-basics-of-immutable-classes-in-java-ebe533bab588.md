# Java 中不可变类的基础知识

> 原文：<https://blog.devgenius.io/the-basics-of-immutable-classes-in-java-ebe533bab588?source=collection_archive---------2----------------------->

![](img/e4bae0e63a9532fa6eea1545361b2d03.png)

一只塞特犬睡在一个人类婴儿旁边。瑞安·斯通在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

你不应该写 setters。至少目前的普遍观点是这样说的。二十年前，当 Java Beans 模型被公式化的时候，常识并不是这么说的。

这并不是说今天的常识是错误的。只是常识通常无法解释这些声明背后的原因。或者解释简洁而隐晦。

在禁止 setter 的情况下，最初的程序员可能会被告知这是因为 setter 违反了不变性。这听起来可能像毫无意义的胡言乱语。

或者他们可能被告知类应该是不可变的。他们可能理解什么是不可变类，但是不理解为什么我们应该选择不可变类而不是可变类。

或者他们可能甚至不知道对于一个类来说不可变意味着什么。所以在这篇文章中，我的目的是解释在 Java 环境中一个类不可变意味着什么，以及为什么你通常更喜欢写不可变类而不是可变类。

不可变类就是状态不变的类。这似乎是显而易见的。在实例化时，构造函数设置所有字段，这些字段保持不变，直到对象被丢弃。

一个不可变的类可能有 getters，但是没有很好的理由让它有 setters，因为字段不能被改变。

Java 中最著名的类`String`，是不可变的。这意味着，正如您可能已经知道或已经明白的，一旦创建了一个`String`实例，就不能更改。当然，如果指针没有被标记为 final，那么它是可以改变的。

一个`String`实例上的任何计算结果几乎总是另一个`String`实例。例如，鉴于

```
String s = "Hello, World!";
s = s.toLowerCase();
System.out.println(s);
```

文本“你好，世界！”在`s`被重新分配指向“你好，世界！”后，很可能还会在系统中存在一段时间实例。如果我们有

```
String s = "Hello, World!";
s.toLowerCase(); **// Notice no "s = "**
System.out.println(s);
```

我们会看到“你好，世界！”而不是“你好，世界！”。您的集成开发环境(IDE)也可能建议您检查`toLowerCase()`的返回值。

假设小写计算仍然发生，但是我们的程序不能访问那个结果，因为`s`仍然指向初始化它的`String`实例。

下面是我们实现`toLowerCase()`的一种方式:

```
 public String toLowerCase() {
        char[] copy = (char[]) this.value.clone();
        for (int i = 0; i < copy.length; i++) {
            copy[i] = Character.toLowerCase(copy[i]);
        }
        **return new String(copy);**
    }
```

这可能会创建一个新的`String`实例，即使当前的`String`实例已经是小写的。

我还没有彻底测试过，它可能无法通过一些特定于地区的测试，也可能无法通过涉及高低代理的测试。但是这里重要的是它不会改变它被调用的实例。

您不能改变一个`String`实例，因为它的所有实例字段都被标记为 final。最重要的字段只是一个包私有的`char`数组(包是`java.lang`)。

因此，获得具有不同状态的`String`实例的唯一方法是构造一个新的`String`实例。这是不可变类的定义特征。

`String`类有大约二十个构造函数，有些是公共的，有些是包私有的，可能有些是完全私有的，这取决于你使用的 Java 开发工具包(JDK)的版本。

另一个著名的 Java 类`Graphics`肯定是可变的。JDK 中的许多类是可变的。给定一个`Graphics`实例，你的程序可以调用`setColor()`和`setFont()`以及其他几个实例。

理论上，`Graphics`可以作为一个不可变的类来实现。但是这实际上不会发生，因为今天仍在运行的许多 Java 软件都依赖于`Graphics`的可变性。

如果 Java 抽象窗口工具包(AWT)是今天发明的，`Graphics`可能仍然是一个可变类。但是更多的类，比如`Point`，将是不可变的。

不变性有很多好处。线程安全是一个经常被提到的好处，排在任何其他好处之前。

Setters 意味着参数验证。一旦 setter 参数被验证，可能需要一到两个时钟周期来更新所有的对象状态。

如果只有一个线程在访问一个对象，这不是问题。但是，即使只有两个不同的线程在访问同一个对象，当一个对象的状态不一致时，它也有可能被访问。这可能会导致意外的异常，例如对于不应该为空的空字段。

如果所有相关的对象都是由不可变的类定义的，那么当一个线程被中断而另一个线程访问同一个对象时，对象就不可能处于不一致的状态。

假设`obj`是一个名为`SomeClass`的不可变类的实例。线程`t`有指向`obj`的指针`a`，线程`u`有指向`obj`的指针`b`。

如果线程`u`需要改变`b`，那么`b`被改变指向`SomeClass`的一个新实例，或者指向`SomeClass`的一个不属于`obj`的现有实例。这不会以任何方式影响线程`t`，不管`a`是否仍然指向`obj`。

一个更普遍的好处是不可变类更容易测试和调试。如果你接受测试驱动的开发方法，你测试你的不可变类，但是你几乎不需要调试它们。

如果一个类是不可变的，那么就没有必要测试变化的状态。程序中更少的“活动部分”意味着测试程序时需要考虑的场景更少。

一般来说，getters 和 setters 意味着更多的工作。例如，测试 getters 和 setters。我知道常识也说不要测试 getters 和 setters。

关于测试 getters 和 setters，缺少的细微差别是，如果下列任一项为真，您应该实际测试它们:

*   您希望 getters 不会泄漏可用于更改对象内部状态的引用。
*   您希望 setters 执行任何验证。例如，如果参数中的数字被限制在特定的范围内。
*   这个类甚至只有一个显式定义的构造函数。构造函数越多，编写初始化时出错的可能性就越大。

例如，关于 getters，考虑这个函数，它说明了两个不同的问题:

```
public ArrayList<Transaction> getTransactions() {
    return this.transactions;
}
```

理论上，返回值可能被用来在没有必要的事务验证的情况下不恰当地添加或删除事务。所以现在你需要测试`getTransactions()`没有泄露那一点状态。额外加分:用`getTransactions()`识别其他潜在问题。

这个`getTransactions()`函数来自一个表示银行账户的抽象类。理论上，`Account`可能是一个不可变的类。每当账户上发生交易时，整个`Account`对象的交易列表将被复制到一个新的`Account`对象，新的交易将覆盖新的交易列表，否则新的交易列表只包含旧的交易。

也许这可以很快完成，因为只需要复制指向`Transaction`对象的指针，而不是一个接一个地复制每个`Transaction`对象。

大概`Transaction`及其子类(比如`Deposit`和`Withdrawal`)应该是不可变的。这仍然允许未决交易的概念:`Account`将保存一个已完成交易的列表，这些交易的金额加起来就是“官方”余额，以及一个未决交易的列表。待处理交易的总数将被添加到官方余额中，以给出可用余额。

毫无疑问，表示金额的类应该是不可变的，并且您应该使用专门设计来表示金额的类，而不是使用`BigDecimal`。为此使用浮点原语是一个非常糟糕的主意。

表示金额的类可能使用`java.util.Currency`来表示货币单位(例如，美元、欧元、法郎等)。).该类不仅是不可变的，而且是最终的，没有公共构造函数。

我认为有可能创建一个可变的枚举类型(用`enum`)。但这可能不是个好主意。枚举类型应该总是不可变的。

# 摘要

一个类是不可变的意味着它的内部状态在构造后不能改变。这样的类可以有 getters，但是不应该有 setters，因为那样的话它将是可变的而不是不可变的。

随着 Java 吸收 Scala 特性，它也吸收了标准库中对不变性的普遍偏好。然而，这不是必需的，Scala 的标准库自带可变类(也许还有可变特征)。

尽管我们应该更喜欢不可变的类，但是我们也应该认识到可变的类有它们的用途。如果你想成为一个绝对主义者，那么也许你应该用 Haskell 而不是 Java 编程。

最好让常识来决定一个新类什么时候应该是不可变的，什么时候应该是可变的，最好是不可变的类。

*更多内容尽在*[*blog . dev genius . io*](http://blog.devgenius.io)*。*