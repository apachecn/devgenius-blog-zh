# 有效的 Java:Java 序列化的首选替代方案

> 原文：<https://blog.devgenius.io/effective-java-prefer-alternatives-to-java-serialization-3cf14eee190?source=collection_archive---------1----------------------->

![](img/fe28ce41ab5a8c302dc6b5872ce1e1fd.png)

由[米凯尔·西根](https://unsplash.com/@mikael_seegen?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

从 1997 年开始，Java 的内置序列化就已经成为该语言的一部分，仅仅是在它诞生两年之后。甚至从它作为语言的一部分诞生之初，它就被认为是危险的。虽然目标是善意的，即不费吹灰之力地分发对象，但事后看来，人们普遍认为在正确性、性能、安全性和维护方面的成本是不值得的。

在 Java 语言的历史中，有无数的例子表明 Java 的内置序列化带来了问题。一个这样的例子是 2016 年对旧金山大都会运输署市政铁路的勒索软件攻击，该攻击使整个收费系统关闭了两天。

Java 序列化的一个核心问题是它的目标太广，以至于攻击面非常大。对象图由`ObjectInputStream`类上的`readObject`方法反序列化。这有效地充当了一个神奇的构造函数，可以实例化基本上任何类型的对象，只要它实现了`Serializable`接口。

基本上没有不属于序列化攻击面的类。JVM 类、第三方类和应用程序本身的类都是可能的目标。即使您的代码没有显式使用 Java 序列化，它也可能在幕后使用序列化。这是因为 Java 平台的主要部分，如 RMI(远程方法调用)、JMX (Java 管理扩展)和 JMS (Java 消息传递系统)都是建立在 Java 提供的序列化之上的。通过这些系统对不可信来源进行反序列化会导致远程代码执行、拒绝服务攻击和其他问题。

攻击者和安全研究人员总是在寻找他们可以通过序列化利用的新类。很多时候，实际的攻击是通过这些攻击的链接进行的。这正是上文提到的铁路系统所发生的情况。

即使没有这些攻击链，我们也可能会遇到序列化问题，即使是基本的代码。攻击者通常会寻找一些方法，他们可以提供少量的代码并执行大量的计算来寻找拒绝服务攻击。这通常被称为*反序列化炸弹*。让我们看一个例子:

```
static byte[] bomb() {
  Set<Object> root = new HashSet<>();
  Set<Object> s1 = root;
  Set<Object> s2 = new HashSet<>();
  for (int i=0; i<100; i++) {
    Set<Object> t1 = new HashSet<>();
    Set<Object> t2 = new HashSet<>();
    t1.add("foo");
    s1.add(t1);
    s1.add(t2);
    s2.add(t1);
    s2.add(t2);
    s1 = t1;
    s2 = t2;
  } return serialize(root);
}
```

这段代码创建了 201 个`HashSet`实例的对象图，每个实例有 3 个或更少的对象引用。整个图形仅占用 5744 字节，但无法反序列化。这是因为反序列化一个`HashSet`需要计算其所有元素的散列码。根`HashSet`的两个元素本身在 100 层之下还有两个散列集。这使得`hashCode`函数被称为 2^100 时间。令人沮丧的是，除了代码没有完成之外，没有任何问题的迹象。

所以我认为我们已经充分证明了 Java 的内置序列化有很多缺陷。我们该怎么办？解决这个问题的最好方法是完全避免它。没有充分的理由在您今天编写的任何新代码中使用 Java 序列化。相反，您应该使用其他形式的数据传输。这些系统具有跨平台的优势。这些表示的好处是比 Java 序列化简单得多，范围也小得多。这使得 it 更加安全，因为他们通常只关注数据。这些格式的一些例子是 JSON、协议缓冲区(Protobuf)和 Avro。虽然协议缓冲区和 Avro 也可以促进模式验证，并具有远程过程调用系统(RPC)的扩展，但在简单传输状态时，它们仍然比 Java 序列化简单得多。

但是，如果您正在使用序列化的遗留系统上工作，您仍然可以做一些事情来降低风险。首先是只反序列化可信数据。Java 的官方安全编码指南用红色粗体字写道“不可信数据的反序列化本质上是危险的，应该避免”。这是唯一的指导方针，所以我们不应该忽视它。您可以使用的另一个工具是 Java 9 中添加的`java.io.ObjectInputFilter`类(也是后端口的)。这允许更多地控制什么类型的对象可以和不可以在我们的系统中被反序列化。您可以选择只接受某些类型(允许列表)或不接受某些类型(不允许列表)。如果可能的话，你应该使用一个允许列表，因为这样可以最大程度地控制什么是可以接受的。不允许列表虽然仍然有用，但它只能保护您免受已知问题的影响，而不能防止新发现的问题。

今天仍然有很多使用序列化的 Java 代码在使用。既然如此，我们应该理解它可能带来的复杂性和问题。我们还应该利用我们所拥有的任何工具来限制我们对这些问题的暴露程度以及它们的影响范围。一般来说，如果可以避免 Java 序列化，就避免它。在新系统中根本不引入 Java 序列化。相反，使用现代数据交换格式来跨系统传输数据。