# 水桶上有个洞

> 原文：<https://blog.devgenius.io/theres-a-hole-in-the-bucket-8c75fea1a8a6?source=collection_archive---------18----------------------->

今天早些时候，我遇到了这个问题。我鼓励你停下来仔细阅读这个问题。完成后，请回来继续学习解决此类问题所需的解决方案。

这个问题是硬币兑换问题的一个变种。基本上，你被给予多个不同的情况，在那里你被给予一个桶大小的面额(硬币)和你需要填充的数量 M(需要找零)。这是在每次输入多个案例的过程中完成的。这个问题要求你输出最少的桶满数来装满这个桶，但是如果不可能，你输出-1。

现在进入算法的本质。我们将首先从一个我们可以分析的随机样本案例开始。让我们举这个例子:

```
17 4
1
2
4
5
```

在这种情况下，我们有 4 个大小为 1、2、4 和 5 的桶，我们需要得到 17 的容量。可以证明，最佳答案是 3 个大小为 5 的桶和 1 个大小为 2 的桶，这给出了预期的输出 4。然而，我们如何编程来做到这一点呢？嗯，有两种方式，都涉及 DP。我将使用自底向上的方法，而不是递归解决方案，因为递归解决方案使用堆栈空间，并且更受限制。首先，您需要用(M+1)个值初始化一个大小为(M+1)的数组。这意味着对于这个例子，我们需要一个用 18 初始化的大小为 18 的数组。但是，我们将从将 DP 数组中位置 0 的元素设置为 0 开始。然后，您需要遍历这个数组和桶大小数组([1，2，4，5])。这是背包问题的一个变种。在这个问题中，数组的大小是您可以“达到”的容量，也就是说在给定的最少量的桶中可以填充多少。则数组的值是使用可能的桶在 DP 数组的当前索引处获得卷所需的桶数。在我开始和你们一起研究这个算法之前，我将向你们展示一下 DP 阵列目前应该是什么样子。

```
[0, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18]
```

简而言之，这是算法的伪代码:

```
Iterate the DP array
   Iterate the buckets array
      if the current bucket is less than the current index in the DP array
         set the element in the DP array at the current index to the minimum value of the current index and the value in DP at the current index minus the current bucket size and add one. 
Then return the last index
```

让我们看一下这个数组的算法。我们将从 DP 数组的第二个元素开始迭代。

我们在第一个索引处(i = 1)，桶列表中唯一小于或等于当前迭代的桶是第一个桶(大小为 1)。这意味着我们将取 DP 数组的当前元素的最小值(DP[1] = 18)和 DP 数组的当前元素减去桶大小，然后加 1(DP[1–1]= 0+1)。这意味着当前元素现在是 1。这意味着 DP 阵列看起来像这样:

```
[0, 1, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18]
```

现在，我们将继续进行第二次迭代。因为这次我们有两个小于迭代器的桶，所以我们有多种可能性。在桶列表的第一个元素中，我们有一个大小为 1 的桶。这意味着 DP 数组当前的元素将是 2(使用上面的逻辑)。那么第二个桶的大小为 2。这意味着 DP 数组的当前迭代中的元素将是 1。(使用上面的逻辑)。这意味着我们当前的 DP 阵列如下所示:

```
[0, 1, 1, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18]
```

接下来，在第三次迭代中，它发生了变化。由于当前迭代是 3，桶列表([1，2，4，5])中小于当前迭代的唯一桶是 1 和 2。从 1 开始，DP[3–1]= 1+1 小于 DP 数组中的当前元素(18)。这意味着 DP 数组中的当前元素将是 2。接下来，对于大小为 2 的桶，DP[3–2]= 1+1，它与 DP 数组中的当前元素大小相同，因此它将保持不变。所以综上，DP[3] = 2。

最后一次迭代需要另一个回合，但是这是我将演练的最后一次迭代，因为它是一个简单的算法，你应该能够掌握。我们目前正在进行第四次迭代，其中 DP 数组中的元素是 18。浏览桶列表，我们看到可以按顺序使用的元素是 1、2 和 4。我们将从 1 开始，因为 DP[4–1]= 2 的最小值，加上 1，在 DP 数组的当前迭代中的新元素是 3。然后，对于大小为 2 的桶，DP[4–2]= 1+1，这小于 3，DP[4]现在将是 2。然而，当我们做 4 DP[4]大小的桶时，它会改变。由于 DP[4–4]= 0+1，DP[4]现在将为 4。这是因为尺寸为 4 的桶仅用一个桶就能装满总体积为 4 的桶。

遵循这个测试用例的算法将会生成下面的 DP 数组。

```
[0, 1, 1, 2, 1, 1, 2, 2, 2, 2, 2, 3, 3, 3, 3, 3, 4, 4]
```

现在，让我们用代码实现这个算法。请记住，我们有多个“案例”要处理，我们将稍微修改代码，并在函数中使用该算法。下面是我描述并用来解决这个问题的算法/代码的实现:

如果该解决方案帮助您更好地理解了这类问题，请留下赞。请随意评论我接下来应该攻击什么问题。