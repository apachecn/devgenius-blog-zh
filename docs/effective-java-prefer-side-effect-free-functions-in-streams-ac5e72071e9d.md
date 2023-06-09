# 有效的 Java！更喜欢流中无副作用的函数

> 原文：<https://blog.devgenius.io/effective-java-prefer-side-effect-free-functions-in-streams-ac5e72071e9d?source=collection_archive---------8----------------------->

正如在前面章节回顾中所讨论的，流可以大大缩短我们的代码，使之成为非常简洁的表达式。这个硬币有两面。简化代码有切中要点的一面，也有代码的密集性。许多开发人员，尤其是那些没有函数式编程背景的开发人员，会发现自己在涉及到流时处于晦涩难懂的一方。如果这解释了你对溪流的感觉，坚持信念，迟早你会找到模式。今天的主题将有助于以预期的方式使用流，从而不必与它们对抗。

如前所述，流是一个处理管道，当使用正确时，这是一个强大的概念，当使用错误时，它会使使用更加混乱和难以推理，甚至隐藏错误。那么使用流的正确方法是什么呢？这在很大程度上归结于使用流的纯函数 T4。一个*纯函数*是一个简单地操作它的输入并提供一个输出的函数，它不使用来自函数外部的任何数据，也不影响函数外部的任何东西。

像我们通常的模式一样，让我们来看一个违背这个建议的例子。在这种情况下，程序从一个文件中建立一个词频表。

```
Map<String, Long> frequency = new HashMap<>();
try (Stream<String> words = new Scanner(file).tokens()) {
  words.forEach(word -> frequency.merge(word.toLowerCase(), 1L, Long::sum));
}
```

这段代码很简单，很简洁，而且它完成了工作，那么问题是什么呢？这不是流代码。这是使用流 API 的迭代代码。简而言之，我们从 stream API 这里得到的只是混乱。以这种方式使用 streams API 时，对于以前使用过迭代代码的开发人员来说,`forEach`函数会感觉非常舒服。现在让我们看看如何将流 API 用于流处理代码:

```
Map<String, Long> frequency;
try(Stream<String> words = new Scanner(file).tokens()) {
  frequency = words.collect(groupingBy(String::toLowerCase, counting());
}
```

那么这里有什么显著的区别呢？代码最终变得更短，但也更清晰，定义了应该发生什么，而不是应该如何去做。在这种情况下，按照单词的小写版本收集单词，并将值设置为计数。与`forEach`版本相比，该版本本质上是迭代的，不适合流水线和并行处理，`foreach`函数应该简单地用于报告流水线处理的结果，而不是进行实际的业务逻辑处理。

你会发现自己在以不同的方式使用`collect`终端功能，我们不能在这篇博文中一一列举，但是在某些时候浏览一下它们会很有用，可以知道什么是可能的。就像功能接口一样，你可能无法记住所有的功能，但是知道这些功能的类型将有助于你记住在需要的时候使用什么功能。有很多方法可以创建各种类型的集合，从列表到地图，到集合，以及介于两者之间的任何东西。基本上所有这些功能都有专门化，如果你也需要的话，可以给你更多的控制。

虽然本章关注的是流中的终端节点，但这并不是我们需要担心无副作用操作的唯一地方。例如，我以前见过这样的代码，它获取 JPA 实体流，然后将它们作为流的一部分进行更新。虽然这段代码看起来非常好，看起来非常干净，但它的效率非常低，因为它是打开和关闭连接，一次处理一行，而不是像在 SQL 系统中最有效的那样处理集合。

习惯于以适当的管道处理方式处理流需要一些练习，但是随着您学习这种模式，它提供的功能以及使用这种模式可以完成的任务将变得很清楚。