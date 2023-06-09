# 什么是调用顺序，如何在 React App 中正确使用钩子？

> 原文：<https://blog.devgenius.io/what-is-call-order-in-hooks-and-how-to-use-hooks-correctly-in-react-app-dbe96c0c766a?source=collection_archive---------3----------------------->

![](img/56065e18119b23497a663857582a55e3.png)

钩子是 React 必不可少的一部分，有时可能会很复杂，我们如何克服这个问题，使使用它们变得简单而不会从控制台得到错误？通过学习 React hook 规则的每个细节，答案是显而易见的。我今天会用我的文章清楚地覆盖这个话题，最后你不会对钩子有任何疑问。

有两个规则我们必须记住，所以每当我们使用钩子时，我们都会基于这两个规则来使用它们，以确保我们的 React 应用程序不会出现任何问题，并且会顺利运行。

**简单说明一下**,**调用顺序**是钩子正常工作的**要素**，我们将基于该逻辑解释规则。

**挂钩规则**

**1-)只调用顶层**的钩子(use state&use effect)

这意味着，不要在循环、条件或嵌套函数中调用钩子，总是在 React 函数的顶层使用钩子。因此，根据这条规则，我们必须确保每次组件渲染时钩子都以相同的顺序被调用。这将允许 React 在 useState/useEffect 调用之间正确地保留钩子的状态。

**坏例子一**

下面我们看到一个**错误挂钩调用**的例子，它破坏了调用顺序，我们为每个使用状态和使用效果分配一个调用顺序，在**调用顺序 4 中，**它有时会被跳过，这会破坏调用顺序，我们会得到一个错误。下面的例子是**不可预测的**，所以这违反了我们的规则。

简单说明一下，**调用顺序**必须保持一致和可预测**因此**需要遵循**规则。**

**如何修复不好的例子一**

我们将如何解决上面的例子，检查下面的例子。

**坏例子二**

下面我们看到一个**错误挂钩调用**的例子，它破坏了调用顺序，我们将调用顺序分配给每个 useState 和 useEffect，在**调用顺序 5 中，**我们在这里有一个 useEffect，它有一个条件，必须放在里面。如果没有，它有时会被跳过，这将打破调用顺序，我们会得到一个错误。下面的例子是**不可预测的**，所以这违反了我们的规则。

**如何修复不好的例子二**

我们将如何修复顶部的示例，我们只需将条件放入 useEffect 中，现在调用顺序是可预测的并且运行良好。

**坏例子三**

下面我们看到一个**错误钩子调用**的例子，它破坏了调用顺序，我们给每个 useState 和 useEffect 分配调用顺序，在**调用顺序 5 中，**我们在这里有一个 useEffect，它在顶层有一个嵌套函数，这个嵌套函数可以在 use 中使用。如果没有，它有时会被跳过，这将打破调用顺序，我们会得到一个错误。下面的例子是**不可预测**，所以这打破了我们的规则。

**如何修复不好的例子三**

我们将如何修复顶部的示例，我们只需将嵌套函数放在 useEffect 中，并在其中调用函数，嵌套函数的作用域只在 useEffect 中，但示例将会工作，因为调用顺序将会很好。

**解释**，在我们在顶部解释的三个例子中，我们在坏例子中的共同点是，我们没有在顶层调用挂钩，以及我们如何修复它们，简单来说，我们只是在顶层获得挂钩，因此我们将正确使用调用顺序，React 应用程序将顺利工作。

**2-)不要从常规 JS 函数中调用钩子。**

这意味着，不要从你在代码中创建的函数中调用钩子，假设你有一个函数，当你按下一个按钮时，它会触发，每次你点击那个按钮，它都会增加数字，如果你在那个函数中调用钩子，你会得到一个错误，所以避免在你的自定义 Javascript 函数中使用钩子。

仅调用 React FC 的钩子

只调用你创建的自定义钩子中的钩子。

**坏例子**

我们在这里使用了 React FC 中的钩子，这符合规则 **a** 但是我们在我们创建的函数中使用了钩子，这违反了规则，我们将得到一个错误。

**如何解决不好的例子**

我们将如何修复顶部的示例，我们只需将 javascript 自定义函数放入 useEffect 中，只需去掉自定义函数，并在顶部放置挂钩**即可解决问题。**

我们将在这里结束，如果你有任何问题，就在帖子上发表评论，如果帖子帮助你解决了你的问题，请鼓掌，分享或给我一个关注。

我的链接在下面

[AKIN KARAYUN | LinkedIn](https://www.linkedin.com/in/akin-karayun-ab3239bb/)