# SPA 与 MPA:适合工作的工具

> 原文：<https://blog.devgenius.io/spa-vs-mpa-the-right-tool-for-the-job-8c4cca9d2cd0?source=collection_archive---------12----------------------->

大家好，感谢加入！

今天，我想看看单页应用程序和多页应用程序在使用正确的工具完成正确的工作方面的区别。

![](img/b632f548806830e174f1e5bd9cf81d7e.png)

我们中有多少人在为一个网站使用 React、Vue 或 Svelte 等框架，而最终却没有充分利用这个框架/库？

有时我们只是习惯于使用熟悉的工具…有时以前的开发人员选择了一个对工作来说可能有点大材小用的工具。

无论哪种方式，让我们对水疗中心和海洋保护区进行一次高水平的审视吧！它们各有利弊，这可能有助于您为下一个项目选择工具。

为了检验 SPA 模型和 MPA 模型，我们将把网站数据传递给用户的过程可视化。我们的堆栈将由一个 API、一个数据库和一个用户界面(客户端)组成。

# 单页应用流程

## 最初的请求

经过漫长的一天，约翰尼坐下来去他最喜欢的网站，碰巧是一个单页应用程序。他在浏览器中输入 URL，初始请求就发出了！

![](img/3a814717ea07530a03e5455c0141e252.png)

## 有效载荷

服务器收到请求后，有一项重要的工作:

> 来提供用户界面。

SPA 本身被设计为将包含用户界面的“大型”有效载荷发送回用户。

![](img/717455027f21404f3224a3270f6b8270.png)

Johnny 收到有效载荷，并可以查看网站的大约`every`页！

## 硬件

接下来，约翰尼的计算机开始将有效载荷转换成 HTML。换句话说，他的计算机正在制作它，以便他可以查看用户界面并与之交互。

![](img/acc4e14684b7d567a509548dcb09efa6.png)

需要注意的是，计算机执行这样的操作并不容易。另一方面，如果需要，可以利用外部处理能力！

## 模板

创建的 HTML 可以查看，但它只是一个模板。它丢失了数据。

```
<h1>Hello {{first_name}}</h1>
```

这些数据实际上位于托管数据库的另一台服务器上。也就是说，Johnny 计算机上的客户端应用程序已经准备好了，并且知道如何请求缺失的数据。

它被编程为向 API 发送额外的网络请求，以便从数据库中获取所需的数据。在此之前，用户必须观看加载屏幕！

![](img/18fc8a155cffec58f5cfa9e2fc2e1a27.png)

## 装载时间

到目前为止，Johnny 一直在观察他的计算机上的加载屏幕。

1.  他一直在等待他的浏览器下载“巨大的”初始有效载荷。
2.  他一直在等他的电脑把它转换成可见的 HTML
3.  他现在正在等待 API 发回他需要填充模板的数据。

一旦所有数据到达，Johnny 就可以开始使用这个单页应用程序了。

# 多页应用流程

## 最初的请求

这一次，Johnny 将发送访问多页应用程序的请求。这个请求的发送方式和以前一样，但是随后的事件顺序会有所不同。

## 有效载荷

同样，服务器的工作是交付用户界面。这一次，我们看到服务器没有向用户发回这么大的有效载荷。

相反，我们收到的是一个包含最少客户端 JavaScript 的小 HTML 文件。

![](img/3e8b009547d88e0e89c01bc59d9a03f8.png)

Johnny 收到了他请求的单个页面，而不是收到应用程序提供的每个页面。

## 硬件

这一次，约翰尼的计算机不必如此努力地工作，因为有效载荷已经包含成品！

他的电脑只显示 HTML，约翰尼正在使用该网站。

```
<h1>Hello Johnny</h1>
```

## 模板

MPA 的 HTML 模板不需要基于 JavaScript 创建。在这种情况下，HTML 模板已经创建好了，可以填充了。

服务器托管 HTML 模板，并在将成品发送给用户之前填充变量。

## 装载时间

对于多页面应用程序，需要处理的逻辑和网络请求明显减少，从而导致 web 应用程序的加载速度加快。

1.  Johnny 等待服务器填充 HTML 模板。
2.  他等待小的 HTML 文件被发送到他的计算机。

一旦 Johnny 收到完成的 HTML 文件，他就可以开始使用 web 应用程序了。

# 哪个更好？

嗯，两个选项都不是更好！这完全取决于用例场景。

以下是基本情况。

*   高度 **动态**的应用程序可能更适合 SPA，而更加面向数据的应用程序可能会从 MPA 方法中受益。高度动态的应用程序可以是像 Figma 或 Google Docs 这样的网站，而数据驱动的应用程序可以是托管您最喜欢的在线购物商店的网站。
*   SPA 上的交互时间(TTI)最初可能会更长，而页面之间的加载时间可能会更快。多页面应用程序上的 TTI 可能会更快，但每个后续页面加载都需要一个新的网络请求。

## 适合这项工作的工具

当考虑下一步时，考虑应用程序的未来是很重要的。

1.  你需要更快的“互动时间”吗？
2.  用户界面的动态性如何？
3.  您的用户拥有支持您的应用程序的硬件吗？
4.  您想购买硬件来支持您的应用吗？

## 看 MPA 经历？

我也是！查看我一直在关注的几个框架…

*   [Astro](https://astro.build/) :提供最少的客户端代码，同时支持你喜欢的框架，比如 React、Vue 和 Svelte。
*   Sane :轻松连接到一个 Mongo 实例，并开始用 Sane 的方式创建一个快速的 MPA。

你最喜欢的 MPA 框架是什么？你目前的项目需要水疗吗？

一如既往，感谢您的加入，迫不及待地想演示下一个 MPA 框架！

—尼克