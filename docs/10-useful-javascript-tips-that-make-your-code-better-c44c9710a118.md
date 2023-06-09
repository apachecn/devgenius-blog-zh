# 让你的代码更好的 10 个有用的 Javascript 技巧

> 原文：<https://blog.devgenius.io/10-useful-javascript-tips-that-make-your-code-better-c44c9710a118?source=collection_archive---------2----------------------->

## 最佳实践的一些提示

![](img/ea847151be6630f4002e24927f547690.png)

奥斯卡·伊尔迪兹在 Unsplash[上的照片](https://unsplash.com?utm_source=medium&utm_medium=referral)

或多或少每个人都写代码，但不是每个人都知道如何让代码看起来更好。
每个程序员都梦想能够用更少的精力和时间写出更好的代码。这只有在使用一些使代码简单的技巧时才有可能。在这里，我将讨论一些你可能会喜欢的技巧。

# 1.自调用功能

在 javascript 中，自调用函数也称为自创建函数。
函数表达式如果后跟表达式()，将自动生效。您不能自行请求活动的声明。

这是一个创建后自动执行的功能。看看下面-

# **2。创建一个对象构造器**

构造函数是一个函数，它创建一个类的例子，通常称为“对象”。当您想要创建多个具有相同属性和方法的相似对象时，构造函数非常有用。代码创建对象而不是它们。看看下面的例子-

# 3.使用分号来结束行

使用分号来结束一行是一个好习惯。如果你忘记了它，你不会得到警告，因为在大多数情况下，它会被一个 JavaScript 解析器插入。

## 例子

```
var burger
var cheese
```

会是这个

```
var burger;
var cheese;
```

# 4.使用循环

在循环中，语句只需编写一次，循环将执行多次，如下图所示。循环是一系列重复的指令，直到达到某个条件。

# 5.扩展运算符的用法

我们可以在迭代中使用 spread 操作符，比如字符串或数组，它将迭代器的内容放入单独的元素中。

```
let greet = ['Hello', 'World']; console.log(greet); *// Without spread operator* console.log(...greet); *// Using spread operator*
```

如果我们运行这段代码，我们会看到

```
['Hello', 'World'] Hello World
```

您一定已经注意到，在第二种情况下(包括 spread 操作符)，问候列表的内容被扩展并从数组中删除。

# 6.逗号运算符的用法

逗号计算运算符(，)的每个运算，并返回最后一个操作数的值。逗号也分隔键值对。

# 7.将字符串转换为数组

JavaScript 字符串可以被拆分()并使用数组转换成字符数组。()来自函数。

```
let string = "Hello"
let arr = [...string] 

// arr -> ["H", "e", "l", "l", "o"]
```

# **8。避免数组中的负索引**

使用多个数组作为真正的多数组(数组的数组)的语言不能有负索引。确保在`splice`中传递的参数不是负数。

# 9.清空数组

空数组意味着数组长度为零。它没有元素。当您创建空的零数组而没有为它们的元素指定值时，对于整数数组，它们默认为像零- 0 这样的值。

```
var myArray = [12 , 222 , 1000 ];  
myArray.length = 0; // myArray will be equal to [].
```

# 10.**使用逻辑 AND/ OR for 条件**

逻辑运算符:

**& &** 表示和
**||** 表示或

逻辑 OR 函数可用于设置参数的默认值。这些通常与布尔(逻辑)值一起使用。

# 结论

我希望你从这篇文章中学到了一些东西，找到一些有用的东西。祝你愉快。

谢谢你。