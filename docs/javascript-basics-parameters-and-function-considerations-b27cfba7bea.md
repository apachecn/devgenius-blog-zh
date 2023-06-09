# JavaScript 基础—参数和函数考虑事项

> 原文：<https://blog.devgenius.io/javascript-basics-parameters-and-function-considerations-b27cfba7bea?source=collection_archive---------45----------------------->

![](img/0477ae070c63244d747593f37c4ded45.png)

由[阿曼达·卡里拉](https://unsplash.com/@amandakariella?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

JavaScript 是世界上最流行的编程语言之一。为了有效地使用它，我们必须了解它的基本知识。

在本文中，我们将研究函数参数、闭包、副作用和递归。

# 默认参数

如果我们有带参数的函数，但我们调用它们时没有足够的参数来填充参数，那么它们将被设置为`undefined`。

为了使函数调用更安全，我们可以为参数设置默认值。

例如，我们可以写:

```
const add = (a = 0, b = 0) => {
  return a + b;
}
```

我们将`a`和`b`都设置为默认值 0。

`=`表示当没有值传入时，我们给参数分配一个默认值。

所以我们可以这样称呼它:

```
const sum = add();
```

而`sum`得 0。

或者我们可以写:

```
const sum = add(1);
```

因为`a`是 1 而`b`是 0。

# 关闭

因为我们可以使用 JavaScript 函数作为值，所以我们可以将它们嵌套在函数中。

这让我们可以返回能够访问函数内部变量的函数，而这些变量从外部是不可用的。

例如，我们可以写:

```
const foo = () => {
  let x = 1;
  return () => x;
}
```

我们有一个函数，它返回一个只在`foo`函数中可用的`x`变量。

每个函数调用都会创建局部变量，所以不同的函数调用不会互相践踏变量。

能够引用封闭范围的局部变量的特定实例的能力称为闭包。

这样，我们就可以在本地访问变量，而不会暴露在外部。

我们可以这样称呼它:

```
const bar = foo()();
```

那么`bar`就是 1。

# 递归

函数可以调用它自己，只要我们不调用它太多次以至于溢出调用堆栈。

调用自身的函数称为递归函数。

例如，我们可以写:

```
const factorial = x => {
  if (x === 1) {
    return 1;
  }
  return x * factorial(x - 1);
}
```

上面的代码有一个带参数`x`的`factorial`函数。

如果`x`是 1，那么我们返回 1。

否则，我们返回`x`乘以用`x — 1`调用的`factorial`的返回结果。

每次我们调用`factorial`时，参数都会下降，直到 1。

这样就不会永远调用它，溢出调用栈。

# 增长函数

我们创建一个新函数有几个原因。

我们可能已经多次编写了一段代码。为了防止这种情况，我们将所有重复的代码放入一个函数中。

我们引入函数的另一个原因是为了添加我们还没有编写的功能，这些功能应该有自己的函数。

我们命名函数并编写函数体。

当我们想在函数创建后添加更多的功能时，我们会在函数体中添加更多的代码。

我们不断增加它，直到它变成一个怪物。

这样不好，因为很难阅读和理解。

因此，我们不应该有增长的功能。相反，我们应该把它们分成小块。

如果我们有更多的功能，那么创建一个新的功能，而不是添加到现有的功能。

![](img/e25f8258fac7da6806849bb9a22d2c83.png)

照片由[梅多·玛丽](https://unsplash.com/@meadowmariee?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

# 副作用

副作用是函数体中的代码，除了用于计算返回值之外，它还执行其他操作。

例如，如果我们将一些东西记录到控制台，那么这就是副作用。

返回值的函数比不产生副作用的函数更容易组合。

纯函数是一种没有副作用的特定的返回值函数。

而且它们也不依赖于其他代码的副作用。

这将使测试更容易，因为我们可以替换返回值，而不是调用函数本身。

这减少了对模拟副作用的脚手架的需求。

# 结论

JavaScript 函数可以有默认参数。我们可以利用这一点来降低没有传递参数的风险。

闭包让函数中的函数访问外部函数中的变量。

增长失控的功能应该被分解成更小的功能。

如果我们能避免副作用，就不应该犯。