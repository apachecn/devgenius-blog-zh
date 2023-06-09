# 了解调试器提供的一切

> 原文：<https://blog.devgenius.io/learn-everything-your-debugger-offers-a7a38ca324bd?source=collection_archive---------13----------------------->

## 你利用了调试器给你的所有超能力了吗？

![](img/745fd7316d76a2b037e621f543341fe7.png)

照片由 [ETA+](https://unsplash.com/@etaplus?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

许多开发人员并不知道他们的调试器能做什么，而其他人并不使用它。

诚然，调试器有一个初始的学习曲线，对于某些平台和编程类型来说可能很难设置。这也很容易让人觉得你总是可以通过打印报表和日志来解决问题。你总能最终解决问题，对吗？

不要再拖延了。

## 花时间去学习和设置你的调试器。

节省的时间和压力将是巨大的。只有当你开始使用调试器时，你才会注意到它的价值。如果你和使用调试器的开发人员交谈，大多数人会说他们多么希望没有推迟它。

使用调试器是必不可少的，因为这是加快调试速度的最快方法之一。

## 它完全改变了调试代码的方式。

您不再需要停止运行代码、添加日志或打印语句来检查一个额外的值。调试器以一种比任何其他调试工具更容易理解的方式提供了更多的信息。他们还可以在请求过程中更改代码和数据，并执行其他工具很少能提供的其他操作。

学习如何使用你的调试器将提高你的调试水平。

# 了解如何使用调试器

我无法帮助您开始使用特定的调试器。

每个调试器的工作方式都完全不同于其他调试器。我可以向您介绍调试器在高层次上可以做什么，以及它们如何在您的调试之旅中提供帮助。最好的开始方式是查阅特定于您的语言和平台的文档和调试技巧。

找到或制作一份备忘单将有助于你使用调试器，即使是在那些令人紧张的紧急 bug 修复过程中。

# 使用断点

很有可能，即使你没有使用调试器，你也听说过断点。它甚至可能是您使用的调试器的一个特性。

断点将在不退出进程的情况下停止代码执行，使您能够在当前请求期间查看数据，或者在不关闭和重新启动的情况下更改内容。

## 暂停代码执行后，您可以像往常一样继续，或者逐行执行代码，直到下一个断点或程序退出。

断点通常设置在特定的代码行。一些调试器提供高级选项，如在鼠标光标处、调用特定函数时、数据更改时或从调用堆栈窗口设置断点。

了解断点的所有可用选项，因为这将是您使用最多的调试工具。

# 使用监视窗口

监视窗口提供了对存储在变量中的数据的深入了解，而无需悬停或手动检查值。它们是显示值的 log 或 print 语句的完美替代。

当您可以看到代码使用的确切数据时，解决棘手的逻辑错误就变得更容易了。

## 不同的调试器可能以其他名称调用观察器，或者以不同的方式对数据进行分组。

例如，一些将所有变量分组，而另一些将有窗口显示当前行的数据，另一个窗口显示局部范围，另一个窗口显示当前请求中的所有数据。大多数将提供检查当前范围内所有数据的方法。

一些调试器还为观察器提供了通知值是否改变的方法，轻松地一次显示多个值，将值固定到实际的代码行，以及其他高级功能。

# 使用步入、步出和跨过。

有时，您不知道放置断点的最佳位置，或者需要查看每行代码发生了什么。能够逐句通过代码在这里很有帮助。

最好的理解方式是，这就像一帧一帧地观看视频。

## 所有调试器都应该提供一种逐行调试代码的方法。

通常，这是通过设置断点或手动暂停代码开始的，然后使用调试器或 IDE 告诉该进程您希望如何继续。大多数调试器将提供以下三种类型的单步执行代码的步骤:

*   **进入** —进入下一行进入方法。
*   **步出** —步出一个方法到调用它的代码，同时仍然执行该方法的其余部分。
*   **单步执行** —在方法返回后立即单步执行代码，同时仍在函数内运行代码。

还可能有一个设置，您可以将其更改为只单步执行您的代码，或者单步执行系统和您的代码。

## 了解调试器的快捷键有助于加快调试速度，尤其是在逐句通过代码时。

备忘单不仅可以方便地帮助记忆快捷键，还可以帮助记忆调试器能做什么。

# 高级调试

到目前为止，我们讨论的所有内容都将帮助您使用调试器，尤其是如果您以前没有使用它的话。

但是许多调试器有许多更高级的特性来进一步提高调试水平。这些高级功能各不相同，从在代码运行时更改代码和值，到自定义调试器如何设置断点、单步执行代码以及一般工作方式。

# 使用条件断点

条件断点类似于将 if 语句应用到断点。

每次代码遇到那一行代码时，它不是不断地中断，而是在暂停代码之前，先检查某个条件是否为真。以下是断点可以使用的一些常见条件:

*   当变量等于特定值时
*   当代码被调用 X 次时
*   当变量或表达式改变时
*   当对象是对实例的特定引用时
*   当特定的机器、进程或线程到达代码时

您可能已经在考虑条件断点是如何有用的了。

它们非常适合于调试竞争或性能问题，即具有特定值的问题，尤其是当它位于包含数百个其他对象的数组中时，以及其他可能不会一直发生的问题。

# 在请求过程中进行更改

大多数调试器都提供了一种在请求过程中进行更改的方法。

什么可以改变，什么时候可以改变，取决于你的平台和它所允许的。许多调试器将允许改变值和代码本身。编译语言可能没有这个选项。

执行此操作通常依赖于热重装或使用脚本语言。

在请求过程中更改内容就像在调试时使用超高速。

取决于你想改变什么，如果你的调试器有一个即时窗口，那可能是一个更好的选择。

# 使用即时窗口

即时窗口是监视功能和更改代码的强大组合。

它将允许您与当前运行的代码进行交互，而无需更改实际的代码。可以在作用域内引用变量、调用方法以及编写其他逻辑代码，比如设置临时变量。有些即时窗口允许在不接触代码的情况下执行代码可以执行的所有操作。

最好将它视为当前调试会话的便签簿或拨弄器。

## 在使用即时窗口之前，请确保检查调试器的即时功能是否会产生副作用。

我的意思是，它是否允许在作用域内改变变量，调用可能改变当前代码执行的函数，等等。大多数调试器都允许副作用，但是我遇到过一些不让你做任何会引起副作用的事情，或者有一个阻止副作用的设置。

# 使用堆栈跟踪和调用堆栈窗口

堆栈跟踪或调用堆栈窗口与我们在异常发生时看到的堆栈跟踪几乎相同。不同的调试器将这称为堆栈跟踪或调用堆栈。堆栈跟踪按照被调用的顺序列出被调用的方法。

如果您不确定正在运行的确切代码，或者如果您想检查是否在不添加断点的情况下调用了特定的方法，堆栈跟踪会很有帮助。

一些调试器还允许直接在“调用堆栈”窗口中向方法调用添加断点。

# 检查线程

如果您正在处理一个多线程平台，您的调试器应该有一种与不同线程交互的方法。

可能有多种方法可以查看所有线程中的数据和调用，将您看到的内容限制在特定线程中，并在数据通过线程时对其进行监控。多线程系统的所有调试器都应该有附加、分离和重新附加到至少运行的不同线程和进程的选项。当调试由并行运行的代码引起的竞态条件和其他错误时，在调试期间与单个线程进行交互会很有帮助。

调试多线程应用程序而不查看线程上运行的确切代码和数据几乎是不可能的。

# 您需要知道如何使用调试器提供的一切。

即使使用了正确的工具，修复 bug 也会有足够的压力。不要因为没有使用最强大的工具之一而让自己更加困难。

# 资源

我关于调试的其他文章:

[](/how-to-find-a-bug-1ca218be3666) [## 如何找到 Bug

### 使用你不了解的代码就像趟过沼泽。你应该努力让自己过上稳定的生活…

blog.devgenius.io](/how-to-find-a-bug-1ca218be3666) [](/4-tips-to-make-production-debugging-easier-484d07a19afe) [## 简化生产调试的 4 个技巧

### 当用户尖叫的时候，你的老板的粗重的呼吸压在你的脖子上，你不想被吓到。

blog.devgenius.io](/4-tips-to-make-production-debugging-easier-484d07a19afe) 

感谢您的阅读。

```
**Want to Connect With the Author?**If you liked this and would like to see other tips, advice, and articles from me, you can find me on most social media under [@kevinhickssw](https://twitter.com/KevinHicksSW).
```