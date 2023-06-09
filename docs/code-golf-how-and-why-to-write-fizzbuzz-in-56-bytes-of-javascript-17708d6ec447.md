# Code Golf:如何(以及为什么)用 56 字节的 JavaScript 编写“FizzBuzz”

> 原文：<https://blog.devgenius.io/code-golf-how-and-why-to-write-fizzbuzz-in-56-bytes-of-javascript-17708d6ec447?source=collection_archive---------2----------------------->

![](img/152bf3f383f464fc0470756e510d0b0d.png)

考特尼·库克在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

[代码高尔夫](https://code.golf)是一种游戏，程序员们竞相用尽可能少的字符编写算法。参赛者可以从几十种不同的语言和许多不同的问题中进行选择，每个组合都有一个排行榜，用于将他们的结果与社区中的其他人进行比较。

在本文中，我们将通过一个代码高尔夫游戏，用仅仅 56 个字符的用 **JavaScript 编写 *FizzBuzz* 。我们将从一个基本的、简单的解决方案开始，一步一步地努力达到 56 字节的顶级解决方案。当然有可能有一个更好的解决方案，但没有人发现，但有数百名球员在 56 分，这将是我们今天的目标。**

(以防你以前没有遇到过， *FizzBuzz* 是一个非常简单的算法，有时用于筛选面试——你可以在维基百科文章中阅读关于它的更多信息[。)](https://en.wikipedia.org/wiki/Fizz_buzz)

# …但首先，为什么？

好吧，公平的问题——我们为什么要这么做？不用说，为 Code Golf 编写的代码不是高度可读、高质量或通用的代码——它被编写得很小，在某些情况下利用语言技巧和怪癖来实现尽可能简洁的解决方案。但是我们仍然有很多理由玩这个游戏。

首先，我们可能会学到一些我们已经知道的语言的新东西。例如，在这种情况下，我们将使用 JavaScript 的一些类型转换技巧来简化代码。在这样做的时候，我不得不多次查阅 JavaScript 规范和文档，以了解变化会如何表现。

除了是磨练你已经使用的语言技能的好方法外， *Code Golf 还是学习一门新语言的速成班。*在解决 Code Golf 问题时，您可能会发现自己在查看一种语言的文档，以找出诸如“这种语言如何处理类型转换”、“支持哪种条件运算符”之类的问题。这是在浏览器中用语言解决简单问题的一种有趣的小方法。

但是除了教育方面，你应该打代码高尔夫，因为你认为它很有趣。即使从我的描述来看这听起来不好玩，我还是鼓励你试一试。一旦你进入其中，当你解决问题时，每一个小的单个字符的改进都会让你觉得很有价值。

# 56 个角色的 FizzBuzz 之路

好——让我们开始吧！我的出发点总是以最明显的方式编写代码。它不需要漂亮，不需要聪明，只需要管用。让我们快速写下一个简单的解决方案，让它发挥作用。

```
**// 147 characters**
for(i=1;i<101;i++) {
  if(i%3==0 && i%5==0) print("FizzBuzz")
  else if(i%3 == 0) print("Fizz")
  else if(i%5 == 0) print("Buzz")
  else print(i)
}
```

有了我们最初的工作解决方案，我注意到的第一件事就是所有的空白。让我们删除一部分内容，*但是我会在适当的位置留下足够多的空白来保留一些可读性*——我们将在稍后接近解决方案时删除其余的内容:

```
**// 133 characters**
for(i=1;i<101;i++){
 if(i%3==0&&i%5==0)print("FizzBuzz")
 else if(i%3==0)print("Fizz")
 else if(i%5==0)print("Buzz")
 else print(i)
}
```

一般的代码高尔夫策略之一，尤其是在问题的早期，是寻找明显的重复:在这里，我看到一些明显的重复在重复使用“打印”。让我们看看是否可以将我们打印的内容分解到一个变量中，以消除这种情况:

```
**// 122 characters**
for(i=1;i<101;i++){
 let j=i
 if(i%3==0&&i%5==0)j="FizzBuzz"
 else if(i%3==0)j="Fizz"
 else if(i%5==0)j="Buzz"
 **print(j)**
}
```

我注意到的下一件事是我们逻辑流的文本量，所有的“如果”和“其他”。我认为如果我们使用 JavaScript 的三元运算符，我们可以做得更好。让我们从一个简单的用法开始，看看它看起来像什么，看看它是否有帮助:

```
**// 119 characters**
for(i=1;i<101;i++){
 let j
 if(i%3==0&&i%5==0)j="FizzBuzz"
 else if(i%3==0)j="Fizz"
 else **j=i%5==0?"Buzz":i**
 print(j)
}
```

是啊！Ternaries 肯定有帮助。现在，如果我们将 ternaries 嵌套在一起，并将其直接放入打印语句中，我们的得分将得到迄今为止最大的提升。下面的代码看起来很不一样，但是逻辑是一样的:

```
**// 85 characters**
for(i=1;i<101;i++){
 print(i%3==0&&i%5==0?"FizzBuzz":i%3==0?"Fizz":i%5==0?"Buzz":i)
}
```

到目前为止，我们的逻辑实际上与我们开始时的简单 if/else 解决方案是一样的。我们只是简化和压缩了。下一步，我们将对逻辑本身进行第一次真正的更新:让我们看看是否可以减少“嘶嘶”和“嗡嗡”的重复。这将需要我们改变 4 个不同案例的流程。

我们可以通过使用字符串连接并提取“Fizz”逻辑来实现这种重构:始终打印“Fizz”if`i%3==0`，连接“Buzz”或数字或空字符串。我们可以在下面的伪代码中看到这个想法。我去掉了实际的条件句，只是为了了解这个想法:

`print ("Fizz" or-maybe "") + ("Buzz" or-maybe i or-maybe "")`

这种方法需要空白字符串，因为我们使用的是字符串连接。

```
**// 76 characters** for(i=1;i<101;i++){
 print(**(i%3==0?"Fizz":"")+**(i%5==0?"Buzz":i%3!=0?i:""))
}
```

好吧，接下来只是一个小改进，但从一开始就一直困扰着我——`i%n==0`可以少写一个字，我们做了几次。你明白了吗？因为我们使用了模数，我们知道结果将是正的，所以我们真的可以进行检查`i%n>0`或`i%n<0`:

```
**// 73 characters** for(i=1;i<101;i++){
 print((**i%3<1**?"Fizz":"")+(i%5<1?"Buzz":**i%3>0**?i:""))
}
```

这里仍然有一些重复。我们看到我们做了两次`i%3`，一次检查大于 0，一次检查小于 1。如果我们对第二个比较重新排序，我们可以将它们提取到一个变量捕获`i%3<1`！轻松取胜，对吗？

```
**// 74 characters** for(let i=1;i<101;i++){
 **j=i%3<1**
 print((j?"Fizz":"")+(i%5<1?"Buzz":j?"":i))
}
```

哎呀！我们无意中添加了一个角色！有时你看到一个重构的好主意，但结果比原来的更差。

尽管如此，有时尝试这些想法是值得的，因为它们通常会带来新的视角和其他探索途径。在这种情况下，是的——它确实引出了另一条思路。让我们进一步提取，将我们的“Fizz”字符串加入到`j`表达式中。为什么？因为这将让我们去掉上面多余的括号:

```
**// 73 characters**
for(i=1;i<101;i++){
 **j=i%3<1?"Fizz":""**
 print(i%5<1?j+”Buzz”:j==''?i:j)
}
```

所以我们回到了之前的 73，但新的结构会让我们有更多的改进。现在`j`要么是“Fizz ”,要么是一个空字符串:我们可以直接将它添加到我们的“Buzz”中，作为逻辑的一部分。

我们的下一个变化是这些 JavaScript 小惊喜之一。看到表情`j==''?i:j`了吗？令人惊讶的是，我们可以简化这一点，这一切都与 JavaScript 如何将字符串转换为布尔值有关。你能找到它吗？

*在 JavaScript 中，逻辑表达式中的空字符串被转换为 false，而非空字符串被转换为 true。*利用这个技巧，我们可以把`j==''?i:j` (9 个字符)改写成`j||i` (4 个字符):

```
**// 68 characters**
for(i=1;i<101;i++){
 j=i%3<1?"Fizz":""
 print(i%5<1?j+"Buzz":**j||i**)
}
```

精彩！既然我们已经了解了这一点，我们可以在三元运算符中利用另一种布尔转换。试着找到它。这与数字 0 如何被解释为布尔值有关:

```
**// 64 characters** for(i=1;i<101;i++){
 j=i%3?"":"Fizz"
 print(**i%5?j||i:j+"Buzz"**)
}
```

好的，我们越来越接近了，我们仍然有之前留下的空白。现在我们越来越接近了，让我们把它剥离出来，看看我们在哪里:

```
**// 60 characters**
for(i=1;i<101;i++){j=i%3?"":"Fizz";print(i%5?j||i:j+"Buzz")}
```

只差 4 个字符就解决了！

看起来不错，但你知道我在烦什么吗？那些花括号`{}`！我们能摆脱这些吗？如果我们能以某种方式将两行合并成一条语句，我们就可以去掉大括号…

事实证明我们可以——利用您在简化的 JavaScript 代码中经常看到的技巧:[JavaScript 逗号运算符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comma_Operator)允许您将多个表达式组合成一个表达式:

```
**// 58 characters**
for(i=1;i<101;i++)j=i%3?"":"Fizz",print(i%5?j||i:j+"Buzz")
```

我们如此接近，现在我们可以品尝它！我们需要做的最后一个优化是一个棘手的优化，但是这里有一个提示:一个典型的 JavaScript for-loop 可以写成`for(i=0;i<100;i++) ...`，但是没有理由它必须遵循这种格式。for 循环真正的意思是`for(initializer; condition; increment) ...`，这里的三个表达式实际上可以是*任何东西。*

没有什么强迫我们在我们的`increment`表达式中遵循`i++`的格式，即使这是最常见的事情。没有理由我们不能在其他地方执行我们的增量:我们可以把我们的`++`放在其他的`i`上。通过这样做，我们 1)为`I`本身去掉了一个字符，2)可以将我们的一个语句移到循环内部，并去掉逗号！

我们开始吧:

```
**// 56 characters - but oops!  Doesn't work!** for(i=1;i++<101;j=i%3?"":"Fizz")print(i%5?j||i:j+"Buzz")***unnamed:1: ReferenceError: j is not defined*** *for(i=1;i++<101;j=i%3?"":"Fizz")print(i%5?j||i:j+"Buzz")
                                          ^*
```

这是我首先尝试的——将`j`初始化移到迭代器中，但是它给出了一个错误！这是因为迭代器在每个循环的之后运行*，所以尽管这是违反直觉的，我们还是需要将*打印语句*放在迭代器中，然后进行`j`初始化！*

在移动了我们的代码之后，还有一个调整(从 0 开始计数，而不是从 1 到 100，因为我们现在是预递增的):

```
**// 56 characters - the solution!**
for(i=0;i++<100;print(i%5?j||i:j+"Buzz"))j=i%3?"":"Fizz"
```

所以，一步一步来，我们找到了解决方案。在这个过程中，我们利用了一些 JavaScript 的怪癖，甚至浏览了几次文档来学习新的东西。

# 试试看！

如果你觉得这个演练很有娱乐性或教育性，我鼓励你亲自尝试一下 [Code Golf](https://code.golf) 。有如此多的语言和问题组合可供选择，很容易找到合适的挑战水平。我用你最喜欢的语言推荐 [99 瓶啤酒](https://code.golf/rankings/holes/99-bottles-of-beer/all/bytes)，或者尝试用另一种语言的 [FizzBuzz](https://code.golf/rankings/holes/fizz-buzz/all/bytes) ，并使用本文中的一些技巧和技术来完成它。

*Jonathan 在大大小小的创业公司中拥有超过 20 年的工程领导经验。*