# 数据网格体系结构的原则

> 原文：<https://blog.devgenius.io/the-principles-of-the-data-mesh-architecture-ca65efa826bb?source=collection_archive---------10----------------------->

## 引用

## *摘自* [*行动中的数据网*](https://www.manning.com/books/data-mesh-in-action?utm_source=medium&utm_medium=referral&utm_campaign=book_siwiak_data_12_29_21) *作者:亚采克·马奇扎克、斯文·巴尔诺扬和玛丽安·西维亚克*

*本节选探讨了数据网格作为一个概念的四个原则。*

如果你有兴趣了解什么是数据网格以及如何使用它，请阅读这篇文章。

Zhamak Dehghani 首先将数据网格概念的当前化身描述为一组四个原则:域所有权、域数据作为产品、联邦计算治理和自助式数据平台。然而，从我们的角度来看，数据网格实现成功的关键在于理解它是一种社会技术架构，而不是技术解决方案。在本文中，我们将介绍 Dehghani 的 4 个原则，并解释对于理解数据网格体系结构至关重要的社会技术方面。

## **面向领域的分散数据所有权和架构**

第一个原则是*数据及其相关组件应该由最接近它的人拥有、维护和开发，即数据领域内的人*。这需要将领域和有界上下文的概念应用到数据世界中。这也意味着所有权和架构的去中心化应用。

其思想是领域内部工程师负责开发数据接口，允许其他用户(例如数据科学家、自助 BI 用户、数据工程师和系统开发人员)使用领域数据。数据产品的数据工程师应该是某个领域的专家，这样可以减少沟通问题和对数据的误解。

数据应该有明确的所有权，它不应该在组织的集中层次上；我们应该把这个责任交给最亲近的人。在面向源的数据集的情况下，这可能是领域团队，或者对于从其他数据集创建的新数据集，这可能是数据工程团队、分析工程团队或数据科学团队。如果我们的数据集是一个非常面向消费者的数据集，它也可以是使用数据的组织单位。

领域是我们业务的一个领域或一部分。是对公司进行切片分解的一种方式。通常，我们的组织结构类似于业务领域。

在任何给定的业务中，您都可以找到像内容分发、内容生产和营销以及品牌开发这样的领域。

![](img/e6502b7247f05007f659a7c29d612cff.png)

图一。来自一家名为 Messflix LLC 的虚构企业的简化业务领域草图。

领域所有权原则表明，拥有这些领域的每个团队或单位也应该拥有在这些领域中创建的数据。因此，开发支持内容生产的软件的团队也要对内容生产数据负责。但是对数据负责意味着什么呢？

对数据负责意味着为组织的其他部分(即其他域)托管和提供数据集。所有权不仅涵盖数据；该团队还应该负责管道、软件、清理、重复数据删除和丰富数据。

与敏捷原则和敏捷团队一样，如果没有自主权，所有权本身就没有多大意义。这就是团队应该能够自主发布和部署操作和分析数据系统的原因。

每个企业都包含许多领域。这些域中的每一个通常都可以进一步划分为子域。通过应用这一原理，我们将得到一个互连的域数据节点的网格。网格的节点可以甚至应该被连接。需要时，数据可以在域之间移动、复制和改变形状。例如，数据通常会从面向源的数据域(操作系统的输出)转移到更加面向消费者的数据域，在这些数据域中，原始数据通常会被聚合并转换为更加消费者友好的形状和格式。

在这样一个由互连的域和子域组成的网格中，只有接近数据的人才足够了解数据，能够真正使用它。举一个图 1 中的例子:单词“content”在这三个领域中的意思是一样的吗？希望不会，因为在“生产内容”领域，我们既有正在创建的内容的“草稿版本和想法”,也有将成为真正生产内容的内容。然而，在“分发内容”领域，这将意味着生产化的最终内容。

想象一个来自“分发内容”领域的开发人员，他应该从“生产内容”领域编辑一个“内容片段”列表。他可能会产生一个产生的内容片段的列表。然而，这没有抓住要点。该需求可能会要求一个所有内容片段的列表，包括想法、仍在生产中的东西以及被取消的片段。此外，还应该包括这些内容块的状态。

然而，这个领域之外的人甚至不知道这些是重要的数据。因此，域内的人是唯一真正能够处理这种数据的人。

**源数据域**通常提供代表业务事实的数据和信息。数据应该向其他领域公开，以服务于操作目的(如 REST API)和分析目的。源数据域应该公开域事件和随时间聚合的历史快照。对于后者，我们应该确保底层存储针对大数据分析消费进行了优化(如数据湖)。在前面的示例中，当“生产内容”域公开生产内容片段的列表时，它就变成了源数据域。这是由创建内容的业务流程创建的原始数据。

**消费者数据领域**与消费密切相关。这种领域的一个很好的例子是管理报告和预测。在 Messflix LLC 的情况下，它可能是内容推荐域，这可能是内容分发的子域。如果现在营销团队拿出制作内容的清单，用相关的营销材料、用于推广的推文等丰富它。，那么新列表将进入消费者数据域。

数据域之间的部分数据可以复制。尽管如此，因为它服务于不同的目的，它也将被不同地建模；这意味着域边界通常也是数据模型边界。因为我们希望给予团队尽可能多的自主权，所以我们并不试图为整个组织创建一个单一的规范模型。我们给予他们自由，以他们需要的方式对数据建模。除了源和消费者一致的域之外，我们还可能遇到跨组织使用的核心数据域，并且通常表示关键的实体或对象。

当我们在整个组织中分担数据的责任时，我们获得了巨大的可伸缩性和可维护性。例如，当我们想要向网格添加新的数据集时，我们将添加一个新的自治节点。与此同时，拥有数据集的团队将处于非常舒适的境地。他们只会拥有自己真正理解的数据。

## **作为产品的数据**

第二个原则是*数据必须被视为产品*。这需要引入产品思维，集成到数据管理中。

通常，当我们谈论数据时，我们首先想到的不是文件就是数据库中的表。当我们想到数据时，我们经常会看到一个电子表格或文件中一系列带有命名列的行。从这个角度来看，很容易将数据简化为技术细节。但是，更重要的问题是:从组织的角度来看，是什么赋予了数据价值？或者反过来问这个问题:是什么阻止了我们将数据转化为有价值的决策？

如果没有一组适当的描述，即使是准备得最好的数据集也找不到，因此无法从中提取任何价值。在需要这些属性的情况下，缺少关于数据的新近性或完整性的信息可能会使它完全无用。这就是为什么值得将数据视为一种产品，即最终构成用户使用体验的更大整体。

数据团队提供的数据应遵循典型的产品特征，如:

*   *可行的质量* —由专业领域专家确保。
*   *预测用户需求* —向外界提供数据的团队应该了解企业的业务环境，例如，以现有数据管道易于消化的格式呈现数据，以确保所提供数据的可用性和易用性。
*   *安全可用性* —确保产品的可用性，以满足用户随时随地的需求。
*   *关注用户目标* —关注一个领域并不意味着数据团队缺乏与其他用户的沟通；相反，寻求协同作用和共享工具集应该为更好地了解彼此的需求创造机会。
*   *Findable* —任何数据产品都应该可以通过简单的方式被发现，这是数据库中的随机表所缺乏的。
*   *可互操作* —不同的数据产品应该能够以增加其价值的方式进行组合。

## 什么时候我们可以称数据为产品？

在日常生活中，我们与许多产品打交道。一般来说，产品可以被定义为“有意识行为的结果”如果我们以一条牛仔裤为例，我们确信它满足某些预定的条件。一件产品要被称为一条牛仔裤，它必须有合适的形式和形状，并由某种材料制成。此外，它应该有其独特的名称(特别是如果制造商提供了许多特定类型的产品)，因为我们购买的是特定的型号，而不是一般的牛仔裤。

它还应该满足一些标准，以确保一条牛仔裤在使用几个小时后不会坏掉。除此之外，还有人对该产品、其质量以及在公认的、未言明的使用条款内使用该产品的后果负责。我们可以用这种思维去思考数据。

把数据当成一个产品，会意味着有人有意识地设计了这个产品，然后创造并发布了它，对它负责，主要对它的质量负责。在数据网格环境中，这将是数据产品所有者(设计数据产品的人)和实现它的数据产品开发人员的责任。就像商店货架上的产品一样，数据产品有其独特的名称和既定的特征，包括:

*   质量水平
*   可用性级别
*   安全规则
*   更新频率
*   特定内容

当我们考虑产品时，仅仅暴露数据是不够的。我们还需要确保为最终用户最大化其可用性。在这种情况下，数据产品所有者的角色至关重要，因为他或她负责数据的最终用户体验。

参考前面提到的 Messflix 示例，我们可以想象一下生产内容领域中的一些示例性数据产品:

*   成本表
*   剧本
*   铸造
*   电影流行度
*   电影趋势

将数据视为一种产品让我们直接进入产品思维方式；从您的客户希望解决什么问题开始，并以此推动数据产品设计流程。然后，作为数据产品所有者，您应该基于预定义的成功标准交付解决这些问题的数据产品。

作为产品的数据还意味着一定程度的标准化，允许将单个元素整合到更大的数据网格生态系统中。要将一组给定的数据称为数据产品，它应该是:

*   **自描述的和可发现的** —数据应该被描述，并且这种描述应该是数据产品的一个组成部分。数据产品应该能够在数据网格生态系统中注册自己，因此应该是可发现的。
*   **可寻址** —它应该有一个唯一的地址(例如以 URI 地址的形式)，这样它就可以被引用，并且可以创建数据产品之间的关系。
*   **可互操作** —数据产品应根据预定义的标准制作，涉及数据共享形式、标准化格式、词汇、术语或标识符、安全和可信。数据产品应该满足已建立和声明的 SLA，并支持受控访问，从两个角度确保数据安全:知识产权和 GDPR 式法规。

## 作为自主组件的数据产品

在满足先前确定的条件的同时，数据产品应同时构成一个自主的组成部分，以便负责某一数据产品的团队能够独立开发该产品。从技术解决方案的角度来看，我们可以将数据产品视为数据世界中微服务的模拟。除了使数据可用之外，数据产品还嵌入了与数据转换、清理或协调相关的代码。它还公开了与数据网格环境和平台自动集成的接口，除其他外，它还提供:

*   **输入逻辑和输出端口** —用于从源获取数据并向消费者公开数据的形式和协议。
*   **运营指标** —用户数量、吞吐量、提取的数据量等。
*   **数据质量报告** —不完整数据的数量、格式不兼容、异常值的统计测量等。
*   **元数据** —数据模式、领域描述、业务所有权等的规范和描述。
*   **配置端点** —指在运行时配置数据产品，如设置安全规则。

这些是作为技术组件构成数据产品的几个例子。

## **联邦计算治理**

第三个原则是在数据网格的所有参与者之间联合和自动化数据治理。它旨在为基本独立的数据产品生态系统提供一个统一的框架和互操作性。它的目的是让自主数据产品在一个实际的数据*网格*中工作，而不仅仅是作为独立的产品。

联合计算治理需要两个不可分割的元素:治理机构和实施手段。

总体规则和法规应由一个由数据产品所有者、自助式数据基础架构平台团队、安全专家以及 CDO/首席信息官/首席技术官代表组成的机构达成一致。该机构还将作为一个讨论场所，讨论新数据产品的开发与向现有数据产品添加新数据集、吸收新外部数据源的方法、中央平台开发的优先事项等。

有效的数据治理至关重要，数据安全是各行各业各种规模公司的首席数据官/首席信息官主要关注的问题之一。此外，大多数大型企业需要引入由政府或商业法规(如 GDPR、HIPAA、PCI DSS 或 SoX)强制实施的数据安全和治理控制。

## 数据治理的联邦化

乍一看，数据网格给已经很大的数据治理范围增加了新的复杂性，因为它现在还需要解决将责任转移到数据产品的问题。反过来，每个数据产品都需要配备允许安全有效地处理所拥有的基础设施、代码和数据(以及元数据)的流程。此外，数据治理流程需要平衡公司范围内的数据解决方案的一致性，通常通过标准化与提供给数据产品团队的自治驱动的灵活性和创造性来实现。

必须明白，没有平衡中央治理和地方自治的灵丹妙药！这将始终取决于您组织的具体情况。例如，您的数据产品所有者的需求和成熟度是什么？组织的数据相关风险偏好是什么？您的中央数据治理团队的专业知识水平如何？您正在处理的数据有多敏感？在你能够设置中央和地方团队的职权范围之前，你需要回答这些和更多的问题。

需要另一套策略来确保数据产品的互操作性和数据消费者随时将它们连接在一起的能力。最后，这些程序需要提供不同数据产品的兼容性，而不需要明确实施一个总体数据模型，因为这种方法已被证明会造成数据操作的瓶颈。

数据网格试图通过数据治理的联邦化来满足这一需求。在这种情况下，联邦化意味着治理结构在中央和地方这两个不同层次上平等运作。由数据治理委员会执行的中央治理级别将决定确保数据产品安全可靠的可发现性和互操作性所需的一组最少的全球规则。

由数据产品所有者领导的数据产品团队负责高度自主地开发其产品，决定其职权范围内(在企业技术堆栈的边界内)的所有技术和程序问题。

对于责任的精确划分、数据治理委员会的结构以及治理数据世界的确切规则，没有灵丹妙药。相反，每个业务都有自己的一套全局规则，让领域团队对他们的数据产品有不同级别的控制。

## 数据治理的计算元素

联邦计算治理这个名字是由扎马克·达格哈尼在她的*事实上的*[数据网宣言](https://martinfowler.com/articles/data-mesh-principles.html)博客文章中创造的。然而，由于计算治理在其他任何地方都没有定义，我们将假设该术语与数据治理自动化的元素相关，通过作为连接不同数据产品的媒介的中央平台的存在来实现。

可以自动化并嵌入数据平台的数据治理元素包括但不限于:

*   [计]元数据
*   目录、参考和主数据
*   血统和出处
*   验证和确认
*   存储和操作
*   安全性和隐私

同样，没有什么灵丹妙药可以决定哪些应该自动化。这需要您的团队努力工作来识别哪些数据治理任务在您的组织中造成了数据网格开发的瓶颈，并使它们自动化。然而，它会有回报的。首先，它将为数据产品所有者提供解决方案，使他们能够无摩擦地连接他们的数据产品。其次，它将使用户能够有效地利用公开的数据。

当我们讨论自助式数据基础架构即平台的细节时，您将了解更多关于数据治理自动化元素的信息。

## **自助式数据基础设施平台**

第四个原则是将数据网格的重复工作提取到一个平台中。它要求将“平台思维”应用于数据环境。平台思维意味着在整个公司范围内更大程度上重复的工作也可以打包到一个“平台”中，因此只做一次，但作为一种“服务”提供给其他人。

就像任何人都可以在一家主要的云提供商那里租赁云资源，并根据自己的需求进行定制，从而减少维护自己的云的工作量一样，他的想法可以缩减为公司内部的工作。

构建和维护数据产品是资源密集型的，需要一系列非常专业的技能(从计算环境管理到安全性)。所需工作乘以数据产品的数量会危及整个数据网格想法的可行性。中央平台背后的想法是将可重复的和可概括的行为集中到必要的程度(同样取决于公司的环境！)并提供一套抽象专业技能的工具。这将减少数据产品开发者和数据产品消费者的进入和进入壁垒。

您可以从您的第一个数据产品所有者的需求开始，迭代地构建设置以满足您的组织的需求。

基础设施支持可以在本地计算能力或云中提供，具体取决于企业政策。其元素可在 IaaS、PaaS、SaaS 或其混合模型中获得。数据网格平台可以支持:

*   **可治理性** —所有与数据治理流程相关的数据计算都需要整合到连接到数据基础架构的每个数据产品中，并在其上自动执行。
*   **安全** —基础设施解决方案应确保所有数据产品为用户提供操作自由，用户的访问允许他们满足其信息需求，并确保安全，防止未经授权的访问。为了做到这一点，数据产品的创造者和用户应能够使用一套现成的流程、工具和程序。
*   **灵活性、适应性和弹性** —基础设施需要支持多种类型的业务领域数据。这意味着启用不同的数据存储解决方案、ETL 和查询操作、部署、数据处理引擎和管道。所有这些都需要具有可伸缩性，以满足不断出现的业务需求。
*   **弹性** —数据驱动型业务的平稳运营需要数据的高可用性。因此，他们在每个基础设施元素的设计级别确保冗余和灾难恢复协议。
*   **流程自动化** —从数据产品注册处的数据元数据注入到确保访问控制，通过中央基础设施的数据流需要完全自动化，可能使用机器学习和人工智能来确保高效的数据处理、质量和监控。

现在，您已经很好地掌握了四个关键的数据网格原则，让我们来谈谈作为一种社会技术架构的数据网格。

## **社会技术架构**

数据网格不是数据问题的技术解决方案。数据网格使用社会技术架构或社会技术系统设计来解决这些问题。我们认为这是数据网格作为一种范式的最大优势，我们认为您应该将社会技术架构视为数据网格实现的基础。你需要有意识地应用社会技术架构来使它成功。

但在此之前，我们需要了解一些背景信息。为此，我们研究康威定律，以理解为什么我们不能独自改变技术，然后研究团队拓扑结构框架，这在本质上是关于社会技术架构的。最后，我们将认知负荷作为团队拓扑框架所利用的主要思想之一。

## **康威定律**

> “任何设计系统(广义定义)的组织都将产生一个设计，其结构是该组织通信结构的副本。”
> 
> -康威定律

梅尔文·康威(Melvin Conway)在 1967 年做出了这一观察，就在第一种广泛使用的高级语言 FORTRAN 发布后十年。没过多久，我们就看到了这种强大的、几乎是引力的力量在实践中的运用。这股“力量”迟早会改变我们的架构，让它看起来像我们的组织结构。作为架构师，我们需要充分意识到隐含的后果。

我们应该以称为合气道的武术为例。“合气道”指的是武术原理或战术，即与攻击者的动作相结合，以最小的努力控制他们的行动。合气道的大师们教你，不要以武会师。相反，你应该利用对手施加的力量。同理，我们也要警惕，利用康威定律。

## **示例:*中央数据仓库***

康威定律很好地解释了为什么人们说“中央数据仓库”，但指的是“由中央数据团队运营的中央数据仓库”。这是因为通常当你发现一个中央数据仓库时，它是由一个中央数据团队建立的。

康威定律只是告诉我们要兼顾事物的组织层面和技术层面。仅仅改变技术上的东西是不会产生影响的。该组织将扭曲或误用事物的技术方面。

## **团队拓扑**

顾名思义，在社会技术架构方法中，我们试图同时合作设计社会和技术架构元素。这样，我们可以提前考虑所有的约束和顾虑。

## **不完善的例子:*构建团队拓扑***

试着想想建造摩天大楼的过程。这在结构上不同于村民集体为他们社区的一个成员建造谷仓。摩天大楼是由高度专业化的团队建造的，有些团队是“前线”，有些团队是“支持”角色。你不会派电工去安装窗户(一语双关)。在给定时间、给定地点使用的技术要求定义了执行任务的团队。

这一部分是关于一种主要的架构方法，这种方法目前在数据网格社区中被用来做好社会技术架构。

> "*团队拓扑是一种清晰、易于遵循的现代软件交付方法，强调优化团队交互以实现流程。*
> 
> (来源:teamtopologies.com)

Matthew Skelton 和 Manuel Pais 创建了团队拓扑，由于其简单和直接的应用，它们开始在社区中受到一些关注。团队拓扑是一种帮助你不陷入康威定律陷阱的方法。团队拓扑结构框架旨在优化公司内部的团队，以实现最佳流程。它很大程度上依赖于认知负荷的概念，以便在这个流程中正确地划分工作负荷，并将团队分成几个团队，并将交互模式分成旨在最小化认知负荷的模式。

由于团队拓扑关注公司的最佳流程，它将帮助我们优化公司内部的数据价值流。

## **认知负荷**

认知负荷(Cognitive Load)是认知负荷理论中的一个术语，它指的是一个人使用的精神资源(工作记忆)的数量。这一理论首先应用于教学领域，它影响了我们如何编写说明书，以便读者可以轻松地消化它们。但之后被用在越来越多的领域，喜欢。

认知负荷有三种类型:

*   内在:构建产品所需的技能和知识(如编程语言、框架和模式)。
*   无关的活动不是产品开发的一部分，但却是发布产品所需要的(比如基础设施、部署和监控)。
*   密切相关:业务和问题领域的知识(比如，如果你是 Messflix LLC 的开发者，你需要了解电影的类型)。

作为社会技术架构师，我们应该塑造我们的团队，以便限制总的认知负荷。它和道路交通很像，你把道路的每一平方米都塞满了车，也不会让车流量最大化；当车与车之间有足够的空间让车辆接近速度限制时，交通以最快的方式行驶。球队也是如此。

那么，我们能做些什么来使数据网格团队高效呢？因此，首先，我们应该简单地规划我们的技术堆栈，以限制内在负载。其次，我们应该接受平台思想，不要强迫团队每次都使用另一个监控和日志记录解决方案来限制额外的负载。做到这两点将允许团队完全专注于本质的东西:密切相关的负载，也就是业务领域。但是密切相关的负载也应该受到限制，我们将通过将解决方案分解成更小的面向领域的数据产品来做到这一点。

所有的原则都受到社会技术思维方式的影响。

**面向领域的分散数据所有权和架构**通过分散对领域和相应数据的责任来减少密切相关的负载。

**数据即产品**通过使数据可查找、可访问、可互操作和可重用，减少了团队之间访问数据的协作；它通过公开预期和已知格式的数据以及消费团队的端口来限制额外的负载。

**自助式数据基础架构平台**通过提供自助式平台减少额外负载。

**联合计算治理**通过实施通用标准和模式，使得团队之间的协作更加容易；它通过减少公司内部可能的技术堆栈来实现团队成员的转移。

正如你所看到的，在每个原则的核心，我们找到了社会技术的思考方式。由于这种范式转变的社会技术性质，清楚这种转变可能带来的好处是很重要的。

虽然数据网格是许多问题的社会技术解决方案，但也有一些与之相关的重大挑战。

目前就这些。感谢阅读。