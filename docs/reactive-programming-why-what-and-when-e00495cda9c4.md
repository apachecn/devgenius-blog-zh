# 反应式编程:为什么，什么和什么时候？

> 原文：<https://blog.devgenius.io/reactive-programming-why-what-and-when-e00495cda9c4?source=collection_archive---------5----------------------->

![](img/be7123b061bdaa2eb835bc8308ba81bf.png)

互动编程(eactive Programming)是一个流行词，已经伴随我们很长时间了(准确地说是从 20 世纪 60 年代开始)。因此，在这篇文章中，我将尝试回答这三个关于反应式编程的重要问题:为什么要使用反应式编程，它是什么，什么时候应该使用它？我在这里的目的是为那些想了解反应式编程的人解释一下，而不去深究技术细节。

因此，没有任何进一步的麻烦，让我们开始吧！

# ***为什么要使用无功编程？***

> 一句话——**并发**！现代系统必须以快速和稳定的方式处理多用户和海量数据，这通常通过并发性来解决，而 RP 正是这样做的。

***反应式编程对于面向对象的 Java 尤为重要，尤其是在异步经常导致代码难以理解和维护的情况下。*** 我知道你一定在想，我们已经有了*未来*和 *CompletableFuture* ，那为什么？答案是它们不够强大。例如，与 Java 8 的流不同，RxJava(网飞大学创建的一个完整的 Java 反应式编程库)也有一个反压机制，允许它处理处理管道的不同部分在不同线程中以不同速率运行的情况。为了更好地进行整体比较，请阅读下面的 [*stackoverflow 帖子*](https://stackoverflow.com/questions/35329845/difference-between-completablefuture-future-and-rxjavas-observable) *。*

# 什么是反应式编程？

根据 [*维基百科*](https://en.wikipedia.org/wiki/Reactive_programming) ，

> 在计算领域，**反应式编程**是一种声明式编程范例，关注数据流和变化的传播。利用这种范例，可以容易地表达静态(例如，数组)或动态(例如，事件发射器)*数据流*，并且还传达相关联的*执行模型*内存在推断的依赖性，这有助于改变的数据流的自动传播。

简单来说，反应式编程可以用以下方式表示:

> ***RP =可观测+观测+调度***

对上述表示的进一步解释:

1.  ***可观测的*** *最简单的解释:基本上就是数据流*。Observable 允许您用与数组等数据项集合相同的简单可组合操作来处理异步事件流。它将你从错综复杂的回调网络中解放出来，从而使你的代码可读性更好，更不容易出错。
2.  ***观察者*** *他们基本上是消费者。*观察者消费被观察者发出的数据流，该数据流是观察者事先订阅的。
3.  ***调度器*** *两个字:线程管理。既然我们在谈论异步编程，那么线程管理对我们来说就变得微不足道了。因此，调度器告诉可观察对象和观察者哪些线程要运行。*

# 何时使用反应式编程？

> 现在我们知道为什么首先需要反应式编程，它是什么，但是我们仍然不知道我们的用例是否需要使用反应式编程。使用 RP 最常见的一个**用例是当你需要处理异步数据流的时候。然而，这是一个很难回答的问题，因为用例中的微小差异都可能成为我们选择的决定性因素。因此，我将提到一些目前正在使用反应式编程的真实应用。**

1.  **使用反应式编程开发移动应用**
    我们经常需要在任务中间或任务结束时从后台线程更新主线程上的 UI，因此我们在我们的服务器上做繁重的工作和复杂的计算，因为移动设备不是非常强大来做繁重的工作。所以我们需要异步工作来进行网络操作，这就是我们使用 RP 的地方。
2.  **使用 RxJava 在网飞 API 中进行反应式编程** 需要服务器端并发来有效减少网络聊天。如果服务器上没有并发执行，单个“繁重”的客户端请求可能不会比许多“轻松”的请求好多少，因为来自设备的每个网络请求自然会与其他网络请求并行执行。如果服务器端对一个折叠的“重”请求的执行没有达到类似级别的并行执行，那么即使考虑到节省的网络延迟，它也可能比多个“轻”请求慢。关于详细的解释，请看这篇网飞强烈推荐的 [*中帖。*](https://netflixtechblog.com/reactive-programming-in-the-netflix-api-with-rxjava-7811c3a1496a)
3.  **对于特定类型的高负载或多用户应用程序，被动提供了一种优雅的解决方案:**

*   社交网络，聊天
*   比赛
*   音频和视频应用(流媒体应用更是如此)

说了这么多，最后我还想指出的是，在没有实际需求的情况下轻率地使用反应式方法只会以不必要的复杂性毁掉一个应用程序。

为了理解用 Java 实现 RP 的 ***【如何】*** 你可以从以下流行的 Java 反应库中选择: [RxJava 2](https://github.com/ReactiveX/RxJava/wiki/Reactive-Streams) 、 [Akka Streams](http://doc.akka.io/docs/akka-stream-and-http-experimental/1.0-M2/stream-design.html) 和 [Vertx](http://vertx.io/) 。如果你能给我一些其他语言的反应库，让我在这里提到，那就太好了。

# 引文

*   [*Java 中反应式编程的精髓— Vladimir Sinkevich*](https://www.scnsoft.com/blog/java-reactive-programming)
*   [*什么是无功编程？——凯夫尔·帕特尔*](https://medium.com/@kevalpatel2106/what-is-reactive-programming-da37c1611382)
*   [*react vex:简介*](http://reactivex.io/intro.html)