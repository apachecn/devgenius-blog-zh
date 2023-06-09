# 正则表达式组的高级用法

> 原文：<https://blog.devgenius.io/advanced-use-of-regex-groups-147ebfcbb139?source=collection_archive---------1----------------------->

正则表达式是一个很有用的学习工具。本质上，它们是一个解析文本的工具。

![](img/84d4d00171249bedaed0ce94479705c9.png)

正则表达式是 Python 的基础

它们存在于几乎每一种语言中，尽管有些差异。因此，正则表达式是可以在不同技术之间转移的知识。本文将关注 Python 版本的 Regex。

我是在我读过的阿菲尼亚·德查尔特和 T2 的萨德拉赫·皮耶博士的文章的基础上写的。相应文章的链接在底部。

它们可以在没有任何协议的情况下应用于解析数据结构。JSON 或 XML 等格式通常都有自定义的解析器。然而，有时您可能会遇到不熟悉的格式，在这种情况下，只有正则表达式可以拯救您。此外，正则表达式对于解析日志非常有用。

今天我将试着介绍群的高级用法。这些用于从字符串中获取信息。它们被括在括号()中。

```
m=re.search("(Trump)","Trump will win the election")
m.groups()
```

> (‘川普’，)

这是一个在字符串中查找单词的简单例子。括号内的名称表示要捕获的名称。

## 向前和向后正则表达式断言

我们正在转向更高级的组的使用。假设您想要查找前面有一系列字符的内容，但是您不希望将它们包含在组中。这种情况需要后视和前瞻断言。

```
txt=”Date: 03/07/20 We saw him on 04/05/20"
m=re.search(“(?<=Date: )(\d{2}/\d{2}/\d{2})”,txt)
```

> (‘03/07/20’,)

在这个例子中，我们试图捕获字符串开头的日期。具体来说，我们正在寻找“日期:”一词后面的日期。在上面的模式中，这是由“？< = "开头。如你所见，文本中有两个日期(即，txt)，由于后视断言，我们的搜索只捕获第一个。这种表达也可以用“？”来否定。

## 非捕获正则表达式组

我们还知道所谓的非捕获组，它们需要在模式匹配的字符串中，但是它们没有被捕获。您可能认为这看起来类似于后视和前瞻断言。您的想法是正确的，因为您可以执行大多数任务，否则您会使用断言。

```
txt=”Date: 03/07/20 We saw him on 04/05/20"
m=re.search(“(?:Date: )(\d{2}/\d{2}/\d{2})”,txt)
```

> (‘03/07/20’,)

非捕获组，而不是后视断言，否则示例和结果都是一样的。

然而，使用其他功能时会有一些不同。也就是说，当使用 match 和 sub 时，它们的行为是不同的。sub 函数用于用新的字符串替换找到的模式。

```
m1=re.sub(“(?:Date: )(\d{2}/\d{2}/\d{2})”,”02/02/20”,txt)
m2=re.sub(“(?<=Date: )(\d{2}/\d{2}/\d{2})”,”02/02/20”,txt)
print(m1)
print(m2)
```

> 我们在 04/05/20 见到了他

正如你所看到的，sub 方法是有区别的。即，非捕获组包括替换中的非捕获材料。因此，当你想交换前面有指定符号的东西时，最好使用后视断言。

match 函数总是在字符串的开头寻找模式，因此，如果在字符串的开头包含一个后视断言，就不会有匹配。

小组也可以捕捉替代方案。“|”表示左边或右边的表达式。断言的一个令人讨厌的特性是替代项必须等长，这迫使您在某些场景中使用非捕获组。例如，我们假设在一些文本中，除了使用序列“日期:”的其他文本之外，我们正在寻找的日期前面是序列“开始:”的。

```
 m=re.search(“(?<=Date: |Start: )(\d{2}/\d{2}/\d{2})”,txt)
```

> raise 错误("后视需要固定宽度模式")
> re.error:后视需要固定宽度模式

由于后视断言需要固定宽度的模式，因此返回一个错误。因此，我们应该在这里使用非捕获组。

## 结论

我们看了一下正则表达式中两个有用的概念。我们将继续这个系列的一篇文章，重点关注命名组。

[](https://medium.com/madhash/the-basics-of-regular-expressions-explained-simply-c65fff886608) [## 正则表达式的基础——简单解释

### 帮你弄清楚这一切意味着什么

medium.com](https://medium.com/madhash/the-basics-of-regular-expressions-explained-simply-c65fff886608) [](https://towardsdatascience.com/regular-expressions-in-python-7c991daab100) [## Python 中的正则表达式

### 数据科学的正则表达式

towardsdatascience.com](https://towardsdatascience.com/regular-expressions-in-python-7c991daab100)