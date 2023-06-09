# 自动化测试技巧

> 原文：<https://blog.devgenius.io/automation-testing-tips-2b61bc44490e?source=collection_archive---------11----------------------->

![](img/6b7f2dd718a9aed4dd96bb2e11a9c4fd.png)

彻底的测试对软件产品的成功至关重要。如果你的软件不能正常工作，大多数人很可能不会购买或使用它…至少不会很久。但是通过测试来发现缺陷或错误是耗时、昂贵、经常重复的，并且容易出现人为错误。自动化测试，其中质量保证团队使用软件工具来自动运行详细的、重复的和数据密集型的测试，帮助团队提高软件质量并充分利用他们总是有限的测试资源。

使用这些顶级技巧来确保您的软件测试成功，并获得最大的投资回报(ROI):

1.  决定要自动化的测试用例
2.  尽早测试，经常测试
3.  选择正确的自动化测试工具
4.  划分你的自动化测试工作
5.  创建好的、高质量的测试数据
6.  创建能够抵抗 UI 变化的自动化测试

# 决定要自动化的测试用例

自动化所有的测试是不可能的，所以确定哪些测试用例应该首先被自动化是很重要的。

自动化测试的好处与给定测试可以重复多少次有关。只执行几次的测试最好留给手工测试。好的自动化测试用例是那些频繁运行并需要大量数据来执行相同操作的测试用例。

通过自动化，您可以从您的自动化测试工作中获得最大的收益:

*   为多个构建运行的重复测试。
*   容易导致人为错误的测试。
*   需要多个数据集的测试。
*   引入高风险条件的常用功能。
*   无法手动执行的测试。
*   在几种不同的硬件或软件平台和配置上运行的测试。
*   手动测试时需要花费大量精力和时间的测试。

测试自动化的成功需要仔细的计划和设计工作。从创建自动化计划开始。这允许您确定要自动化的初始测试集，并作为未来测试的指南。首先，您应该定义自动化测试的目标，并确定要自动化的测试类型。有几种不同类型的测试，每一种在测试过程中都有它的位置。例如，单元测试用于测试预期应用程序的一小部分。要测试应用程序 UI 的某个部分，您可以使用功能测试或 GUI 测试。

在确定了您的目标和要自动化的测试类型之后，您应该决定您的自动化测试将执行什么操作。不要只创建测试步骤，一次测试应用程序行为的各个方面。大型、复杂的自动化测试很难编辑和调试。最好将您的测试分成几个更小的逻辑测试。它使您的测试环境更加一致和可管理，并允许您共享测试代码、测试数据和过程。您将获得更多的机会来更新您的自动化测试，仅仅通过添加解决新功能的小测试。在添加应用程序时测试其功能，而不是等到整个功能实现后再测试。

当创建测试时，尽量保持小规模并集中在一个目标上。例如，单独的只读测试和读/写测试。这允许您重复使用这些单独的测试，而不需要将它们包含在每个自动化测试中。

一旦您创建了几个简单的自动化测试，您就可以将您的测试组合成一个更大的自动化测试。您可以通过应用程序的功能区域、应用程序中的主要/次要部分、公共功能或者一组基本的测试数据来组织自动化测试。如果一个自动化测试引用了其他测试，您可能需要创建一个测试树，您可以在其中以特定的顺序运行测试。

# 尽早测试，经常测试

为了从自动化测试中获得最大的收益，测试应该尽可能早地开始，并且根据需要经常运行。测试人员越早参与项目的生命周期越好，测试越多，发现的 bug 就越多。自动化单元测试可以在第一天实现，然后你可以逐步构建你的自动化测试套件。早期发现的错误比后来在生产或部署中发现的要便宜得多。

随着左移运动，开发人员和高级测试人员现在能够构建和运行测试。工具允许用户在他们喜欢的 ide 中运行 web 和桌面应用程序的功能 UI 测试。有了对 Visual Studio 和 Java IDEs(如 IntelliJ 和 Eclipse)的支持，开发人员再也不必离开他们舒适的生态系统来验证应用程序质量，这意味着团队可以快速轻松地转移到更快地交付软件。

# 选择正确的自动化测试工具

选择一个自动化测试工具对于测试自动化是至关重要的。市场上有很多自动化测试工具，选择最适合您的总体需求的自动化测试工具非常重要。

在选择自动化测试工具时，请考虑以下要点:

*   支持您的平台和技术。你在测试。Net、C#或 WPF 应用程序，以及在什么操作系统上运行？你打算测试 web 应用程序吗？你需要移动应用测试的支持吗？你是用安卓还是 iOS，还是两个操作系统都用？
*   所有技能水平的测试人员的灵活性。你的 QA 部门可以编写自动化测试脚本吗？或者有必要进行关键字测试吗？
*   功能丰富但易于创建自动化测试。自动化测试工具是否支持记录和回放测试创建以及自动化测试的手动创建；它是否包括实现检查点来验证值、数据库或应用程序的关键功能的特性？
*   创建可重用的、可维护的、抗应用程序 UI 变化的自动化测试。如果我的 UI 改变了，我的自动化测试会中断吗？

有关为自动化测试选择自动化测试工具的详细信息，请参见选择自动化测试工具。

# 划分你的自动化测试工作

通常，不同测试的创建是基于 QA 工程师的技能水平。确定每个团队成员的经验和技能水平，并相应地划分自动化测试工作是很重要的。例如，编写自动化测试脚本需要脚本语言的专业知识。因此，为了执行这些任务，您应该让 QA 工程师了解自动化测试工具提供的脚本语言。

一些团队成员可能不精通编写自动化测试脚本。这些 QA 工程师可能更擅长编写测试用例。如果自动化测试工具能够创建不需要深入了解脚本语言的自动化测试，那就更好了。

你也应该在你的自动化测试项目中与你部门中的其他 QA 工程师合作。由团队执行的测试对于发现缺陷更有效，并且正确的自动化测试工具允许您与几个测试人员共享您的项目。

# 创建好的、高质量的测试数据

好的测试数据对于数据驱动测试非常有用。在自动化测试过程中应该输入到输入字段中的数据通常存储在一个外部文件中。这些数据可以从数据库或任何其他数据源读取，如文本或 XML 文件、Excel 表和数据库表。一个好的自动化测试工具实际上理解数据文件的内容，并在自动化测试中迭代这些内容。使用外部数据使得您的自动化测试可重用并且更容易维护。为了添加不同的测试场景，可以很容易地用新数据扩展数据文件，而不需要编辑实际的自动化测试。

通常，您手动创建测试数据，然后将其保存到所需的数据存储中。但是，您会发现一些工具为您提供了数据生成器，帮助您创建存储测试数据的表格变量和 Excel 文件。这种方法允许您生成所需类型的数据(整数、字符串、布尔值等)，并将这些数据自动保存到指定的变量或文件中。使用这个特性，您可以减少为数据驱动测试准备测试数据所花费的时间。

为自动化测试创建测试数据很乏味，但您应该投入时间和精力来创建结构良好的数据。有了良好的可用测试数据，编写自动化测试就会变得容易得多。越早创建高质量的数据，就越容易随着应用程序的开发来扩展现有的自动化测试。

# 创建对 UI 中的更改具有抵抗力的自动化测试

使用脚本或关键字测试创建的自动化测试取决于被测试的应用程序。应用程序的用户界面可能会在内部版本之间更改，尤其是在早期阶段。这些更改可能会影响测试结果，或者您的自动化测试可能不再适用于应用程序的未来版本。问题在于自动化测试工具使用一系列属性来识别和定位对象。有时，测试工具依赖于位置坐标来寻找对象。例如，如果控制项标题或其位置已变更，则自动测试在执行时将无法再找到物件，而且会失败。要成功运行自动化测试，您可能需要在对应用程序的新版本运行测试之前，用整个项目中的新名称替换旧名称。但是，如果为控件提供唯一的名称，则会使自动化测试抵抗这些 UI 更改，并确保自动化测试可以工作，而不必对文本本身进行更改。这也消除了自动化测试工具依赖于位置坐标来寻找控制，其不太稳定并且容易破坏。

# 结论

这些天有吨的软件产品和工具让它更容易为你但可悲的是没有人给你免费。所以当你在等待我们做出最好的自动化工具/软件的时候，这是目前正在开发的。我们建议您尝试首先在设备中将其设置好。

然后试着为你构建的每个自动化框架选择一种语言。然后，随着您对它的熟悉程度的提高，您将尝试改进您的框架，使其要么在时间上更快，要么能够同时测试多个模块。

如果您正在寻找我们的服务，请点击下面的网站:

[StackedQA 网站](https://www.stackedqa.com/)

看看我们的社交媒体:

[脸书](https://www.facebook.com/StackedQA)、 [Twitter](https://twitter.com/stackedqa) 、 [Instagram](https://instagram.com/stackedqa) 、&Linkedin