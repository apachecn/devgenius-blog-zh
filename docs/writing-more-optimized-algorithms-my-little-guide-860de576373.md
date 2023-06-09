# 编写更优化的算法:我的小指南…

> 原文：<https://blog.devgenius.io/writing-more-optimized-algorithms-my-little-guide-860de576373?source=collection_archive---------5----------------------->

> 千里之行始于足下。

凭借 5 年多构建现实世界软件的经验，我逐渐意识到有很多方法可以达到预期的结果。然而，即使是这种情况，也不是所有的方法和模式都能提供可靠(或有效)的结果。也就是说，这是一个不争的事实，那就是不仅要找出实现某件事的方法，而且要找出在任何情况下实现它的最佳方法。

![](img/c4680dd795f6c50be9feba5d83a54860.png)

图片来源:https://swiss-ipg.com

这不仅适用于软件开发，也适用于任何涉及逻辑决策的情况。

在这个小指南中，我将指出两种情况，人们必须开发简单的程序来执行基本任务。值得一提的是，这些并不是应用这些方法的唯一情况。

> 别说了，直接开始吧。是的，我知道！

在你写任何软件之前，你应该考虑很多因素，比如安全性、性能、用户体验、代码整洁、可伸缩性等等。如果没有前面提到的平衡，你的软件很可能不符合最佳实践，就软件开发而言，这是不可以的。

我现在要向你提出的两个问题是簿记和金融环境中经常遇到的问题，为了便于说明，我将分享 Python 中的代码片段，所以请耐心等待，小心谨慎！

简单列举一下不会有什么问题:

**问题 A:** 从按字母顺序升序排列的名字列表中搜索一个名字。

**问题 B:** 从一个用户的钱包中扣款，并增加另一个用户的钱包。

对于提供给您的每个问题，您应该能够遵循以下步骤:

*   理解问题。
*   确定你有什么工具来处理这个问题。
*   挑出问题中涉及的元素(参数)。
*   逐一处理每个组件。
*   合并解决方案以给出最终结果。

# **先说问题 A；**

在这个场景中，给定一个名字“Henry Garrick ”,使用一个简单的程序从按字母升序排列的名字列表中进行搜索，其中“Henry Garrick”是一个字符串，要查询的目标名字表示一个字符串(名字)列表。

![](img/1e5ad8490c44e70d0d907fbc334f5996.png)

看着这个问题，我们可以推导出以下参数:

*   列表总是按字母顺序排列。
*   我们知道数据结构的数据类型。
*   我们要找到一个完全匹配的，而不是相似的名字。
*   我们不局限于任何发展模式。

用 Python 编写代码的最快方法很可能是这样做:

![](img/64803f92b5db65bfffa16affc4e0bfcf.png)

从上面的代码片段中，我们注意到我们从列表的开头到结尾执行了一个循环。这种方法非常好，但是你不认为有一种方法可以让它更快，因为我们有这么多的细节可以处理？

是的，有。不过，我对它有一点了解。

想到什么了吗？好吧，你有足够的时间:)

> 我们为什么不检查一下我们要查询的名字的首字母的位置，然后根据字符在字母表中的位置从上到下进行搜索，反之亦然？

这工作得非常好，并且在大数据集的情况下肯定会减少查询时间，因此值得一试。

![](img/0fb890580f4ebd427b7d6f20d8dd4c43.png)

看一下上面的代码片段，它看起来比前面显示的代码长得多，但是可以证明它在性能方面更高效。有时，用开发复杂性换取性能是值得的，因为这是任何成功产品的必要条件。

在这种情况下，它获取查询字符串的首字符，使用字母表字母的一个子集进行邻近性检查。如果它离起点更近，它就从上到下搜索，反之亦然。

例如，诸如“Zack Lynx”的名字将导致从上到下的反向循环(Z -> A)，而诸如“Beth Finn”的名字将导致从上到下的循环(A -> Z)。在以大数据为目标的情况下，这使得搜索更加优化。

# 我们转到问题 B。

毫无疑问，今天世界上有如此多的金融科技解决方案，而且还有更多。

转移交易的基本思想包括通过授权实体的同意(在合法情况下)启动，使用数学运算改变两个或多个数据存储点中的数值。

在本例中，我们将处理最基本的操作，即从钱包 A(发送方)到钱包 B(接收方)的转账，这涉及从钱包 A 中扣除一个数值，并在钱包 B 中增加相同的值(考虑到在转账交易中没有其他操作要执行)。

为了做到这一点，典型的检查包括检查未决交易并对其进行对账，然后检查可提取余额是否足以启动转账(以避免负余额)。

假设我们有一个名为“users”的表，其中“id”、“user_id”和“balance”为字段，发送者的用户 id 为“0002”，接收者的 ID 为“0004”，他们的余额分别为 4000 和 2000。并且汇款人发起 1000 英镑的转账。

通常会执行一个查询来检查用户余额，如果用户余额小于转账发起请求的金额，就会向用户返回一个错误，否则会执行另一个查询来扣除用户余额，然后执行另一个查询来增加收款人的余额。

总共有三个查询。

*   检查余额
*   扣除汇款人的余额
*   增加收款人余额

下图表明:

![](img/ac6240bfa430e4dbd52eac698aff3847.png)

> 在这个小例子中，我们不考虑 SQL 注入袭击。不要惊慌。Lol。

查询应该是这样的:

> 从用户中选择余额，其中 user_id = "0002 "
> 
> 更新用户设置 balance = balance -1000，其中 user_id = "0002 "
> 
> 更新用户设置余额=余额+ 1000，其中 user_id = "0004 "

不管怎么说，这并不是一件坏事，但是竞争条件可能会导致多项扣除(负余额),并且完成这些操作所花费的时间将远远超过在两个查询或更少查询中完成的情况。

我们可以将查询总结成两个，并在一个地方进行多次阻塞检查。

> 一石二鸟是个不错的主意。

我们实际上应该把“1000”变成一个变量:)，比如说“数量”

我们可以这样查询:

> 更新用户设置 balance = balance -{amount}，其中 balance > {amount}和{amount} > 0

这使得两个查询汇总在一个地方，并防止出现负平衡情况。此外，如果处理得好，它可以帮助您防止竞态条件。请参见下图:

![](img/d0f5a5a9fecd004c92f88a569ccd59d9.png)

如果你想了解竞争条件意味着什么，你可以访问这个链接:[对竞争条件的解释](https://www.techtarget.com/searchstorage/definition/race-condition)。这解释了什么是竞争条件和可能导致竞争的条件，以及预防措施。

总之，许多问题可以用多种方法来解决，但是尝试提出一种更优的方法是值得的，即使它有时会导致更复杂的解决方案。

感谢阅读💚

干杯！