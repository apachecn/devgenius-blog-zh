# 2021 年我仍在使用 ASP.NET 网络表单的 5 个原因

> 原文：<https://blog.devgenius.io/5-reasons-why-im-still-using-asp-net-web-forms-in-2021-a7db6934b915?source=collection_archive---------1----------------------->

![](img/7cb332867351598f80d9cee063ffed88.png)

按照软件工程的标准，ASP.NET 的 Web 表单可以被认为是老派的。也许这句话让我变老了，但这是真的。从软件的角度来看，即使 10 年也开始显示出它的年龄。在微软 2003 年推出 Web 表单的第二年，我开始使用 Web 表单。

我大学的大部分时间都是在 Web 表单中度过的，我职业生涯的 80%也是围绕着它们展开的。不用说，我有前科。我很享受其中的大部分。这不是我通常所说的框架。我也大量使用 ASP.NET MVC 5，但是我不能说我喜欢这样做。我也使用过 React，它完成了工作，但是，我不能说我喜欢使用它。但是 Web 表单是不同的。

这就像今天有人驾驶电动汽车，仍然可以欣赏 1969 年谢尔比发动机的声音。这是因为它构建得很好，非常强大，并且给软件开发带来了某种程度的怀旧情绪。但是也有更多值得喜欢的东西。

# 5.服务器控件

对于那些不知情的人来说，服务器控件是预构建的 web 组件，具有大量现成的功能，可以编译成兼容的现代 HTML。想想按钮、链接和图像，除了它们可以由服务器直接处理而不需要任何额外的工作。这些控件可以附加服务器端事件处理程序，如按钮单击或更改事件。Visual Studio 通常只需轻击一个键就可以为您处理大部分事件绑定。

尽管在 AJAX 大行其道的时代，服务器控件可能开始显示出它们的年龄。主要是因为如今整版回发越来越难得到了。因此，在 2021 年，将服务器端的“更改”事件绑定到下拉菜单可能是不太可能的。

幸运的是，Microsoft 也考虑到了这一点，并引入了 UpdatePanel 控件，该控件允许在无需执行整页回发事件的情况下呈现内容。本质上，它是一个为服务器控件创建适当的 AJAX 请求功能的控件。再一次，您只需将控件拖动到面板上就可以完成所有工作。

我真正喜欢的是整个事情的简单性。

# 4.用户控件

用户控件本质上是服务器控件(如上所述)，只是它们是自定义的。您可以用您认为合适的任何功能和属性来定义您自己的可重用组件。

这允许您非常容易地将这些组件包含到任何 web 表单中，并通过它们各自的属性对它们进行单独配置。不过，真正的好处是，当您开始利用其他组织多年来开发的第三方自定义用户控件时。

我见过从完全响应的图表编辑器到作为定制用户控件开发的复杂文字处理器的一切。您还可以开发能够在任何 ASP.NET web 应用程序中运行的通用控件。对于像我这样的人来说，这是一个巨大的福音，因为我有大量的 Web 表单项目已经发布或者即将发布。

如果您熟悉 React，那么最接近用户控件的应该是组件系统。本质上，独立模块可以与其父级或其他控件共享数据。

# 3.页面生命周期

ASP.NET·佩奇的生命周期就像字母表一样嵌入了我的潜意识。这是因为在 2000 年中期，这是我一次又一次收到的最受欢迎的面试问题之一。

因为这很重要。至少，如果您正在处理 Web 表单，这可能是很重要的。不需要太多的技术细节，页面生命周期就是每个页面为了呈现而经历的一系列步骤。

作为参考，这些包括启动、初始化、加载、渲染和卸载。最棒的是，您可以访问每个事件处理程序。这意味着，如果您需要在页面加载之前或者甚至在页面加载之后进行配置或设置，那么您可以自由地这样做。

我还没有使用过任何其他框架，它给了我对页面呈现顺序如此精细的控制。虽然不是最常用的特性，但有时预处理控件或模块是必须的。

# 2.代码隐藏

对我个人来说，使用 Web 表单时最突出的特点是客户端逻辑和服务器端逻辑的清晰分离。ASP.NET 通过将每个网页分别分割成两个独立的文件来解决这个问题。一个严格用于客户端代码(包括服务器控件)，另一个用于存放服务器端事件处理程序，比如按钮点击或页面加载事件。

两个页面可以通过多种方式相互通信。服务器页面可以修改 DOM 和服务器控件，客户端页面可以包含在页面加载之前呈现的服务器端标记。

最后，在这一部分，您可以选择以某种方式编译项目，以便更新客户端页面时不需要重新编译整个项目。只有对代码隐藏服务器的更新需要这样做。如果你处在一个前端大规模开发的位置，小的变化是不断的，这是巨大的。

对我个人来说，这种客户机-服务器的代码分离清晰而简洁。每个项目开发人员都知道按钮点击事件处理程序的位置。他们不必搜索定制的项目或目录结构来寻找隐藏的逻辑，这是我在使用其他框架时经常发现的。

# 1.忠诚

随便问。如果他们愿意转换，我敢打赌绝大多数人会嗤之以鼻。至少，一个很了解 Web Forms *的. NET 开发者*。那些已经深入并发现了最模糊的错误的人，只是为了挖掘一些更伟大的开发人员的集体良知并找到一个更模糊的解决方案。

我一次又一次地发现自己处于那种情况。盯着最优秀的人的肚子，不确定我在做的事情是否可能。当希望几乎破灭时，编译器会抛出一条成功消息，一切都好了。这种感觉很棒。

这就是我忠于框架的原因。我做得很好，到目前为止，我没有发现什么是不可能的。我希望微软(阅读这篇文章)通过继续支持它，承认成千上万的开发人员花费了职业生涯来学习驾驭这个环境。

然而，从表面上看，微软确实在其网站的不同部分声明开发者应该考虑使用 Razor 网页来代替 Web 表单。也没有计划把它移植到。NET Core，但它确实提出了一个问题，即这项技术还能存在多久。

直到它不再被支持的那一天，我会很高兴地继续使用它，并把它推广给那些愿意听一个家伙在它发布近 20 年后对 ASP.NET Web Forms 大发牢骚的人。