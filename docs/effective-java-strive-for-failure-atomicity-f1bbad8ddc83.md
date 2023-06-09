# 有效的 Java:争取失败原子性

> 原文：<https://blog.devgenius.io/effective-java-strive-for-failure-atomicity-f1bbad8ddc83?source=collection_archive---------4----------------------->

![](img/93b3dda48fe587d7bf0ea50a1f660cf7.png)

照片由[丹·迈耶斯](https://unsplash.com/@dmey503?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 拍摄

即使在一个对象抛出异常之后，该对象仍然处于有效状态也是所期望和希望的。除非抛出的异常是一个致命的异常，否则应用程序将继续前进，从而使对象处于无效状态，这只是要求进一步的问题。既然如此，我们应该努力让对象保持有效状态，即使在抛出异常之后。

让我们考虑一些方法，使我们的对象处于有效状态。

第一个选项是创建不可变的对象。这极大地简化了保持状态有效，即使在异常之后，因为状态不能改变。除此之外，不可变对象还有许多好处。在这种情况下，我们不能总是使用不可变的对象，因此在处理可变对象时我们需要策略。

这些可变策略中的第一个是在进行任何状态更改之前，将所有可能导致异常的[参数检查](https://medium.com/geekculture/effective-java-check-parameters-for-validity-fba5d8579685)推到函数的开头。这个想法的核心是，一旦您通过了参数检查，就不会抛出异常。让我们考虑一个`Stack.pop`方法的例子:

```
public Object pop() {
  if (size == 0) {
    throw new EmptyStackException();
  }
  Object result = elements[--size];
  elements[size] = null;
  return result;
}
```

通过在开始时检查函数的前提条件，我们可以在对象处于不良状态之前抛出必要的异常。你可以想象，如果我们在处理之前不检查大小，我们不仅会抛出一个`ArrayIndexOutOfBoundsException`(这对于抽象来说是不合适的[)，还会让`size`变量为负，这不是一个有效值。](/effective-java-throw-exceptions-appropriate-to-the-abstraction-d085ca1ccba1)

对于可变对象，类似的方法是对函数的操作进行排序，使得可能失败的方法在任何状态改变之前执行。这导致了与前一个策略相同的想法，因为一旦我们到达可变动作，我们就保证成功。

另一种策略是在对象的临时副本上执行操作，一旦成功就替换当前状态。这确实需要一些额外的操作和更多的内存使用，但通常这是值得的。另一方面，有一些算法(比如一些排序算法)可以通过操作临时副本来提高性能。

最后一个策略是编写一个导致回滚的*恢复代码*。这可以通过数据库或文件系统存储来实现。这种方法不经常使用，但如果出现这种情况，这是一种很好的方法。

最后，任何规则都有例外。可能有些情况我们无法正常恢复，比如两个线程之间的并发修改。也可能出现这样的情况，即建设这种复原力的成本不值得。通常情况下，只要我们注意到实现原子性的愿望，并且已经熟悉了实现原子性的模式，那么这种原子性的代价就会很低。

我非常喜欢这些类型的思考练习。当我们能够使用代码组织使我们的系统对错误更有弹性时，它总是一个胜利。考虑和解决这些问题是我心目中的高级工程师的一个标志，技术领导可以在我们代码的港口升起所有的船。