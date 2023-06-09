# BDD:行为驱动开发

> 原文：<https://blog.devgenius.io/bdd-behavior-driven-development-2c0e18d97c16?source=collection_archive---------2----------------------->

![](img/98e2da60077ee032b3c11804b5efb99a.png)

DDD、BDD 和 TDD 是开发软件的三种方法，旨在使过程更好、更有效。每种方法都有自己的一套规则和方法。根据项目的需要，它们可以一起使用，也可以单独使用。在这篇文章中，我们将看看 DDD、BDD 和 TDD 之间的主要区别，以及它们是如何在软件开发项目中使用的。在那之后，我们将更详细地讨论 BDD。

> 这将是一篇理论性的文章，所以给自己拿一杯热腾腾的咖啡，让我们一起来挖掘❤️吧

# 💎DDD、BDD 和 TDD 简介

DD，或领域驱动设计，是一种软件开发方法，强调创建业务领域的模型，或产品设计服务的专业领域。DDD 的目标是生产一个软件系统，准确地代表业务领域，使其更容易为利益相关者理解和使用。

BDD，或行为驱动开发，是一种强调使用场景或例子定义系统行为的软件开发方法。BDD 需要开发人员、业务分析师和测试人员合作，以便定义系统的行为，并为每个场景生成可接受的标准。

TDD，或测试驱动开发，是一种软件开发方法，在这种方法中，测试在实际代码之前开发。TDD 旨在确保代码按计划满足定义的需求和功能。在测试驱动开发(TDD)中，开发人员编写定义代码预期行为的测试，然后构建代码以通过测试。

# DDD 和 BDD 之间的🧐差异

DDD、BDD 和 TDD 之间有几个显著的区别。
DDD 专注于开发业务领域的模型，而 BDD 专注于定义系统的基于场景的行为。
TDD 关注于测试和确保代码符合定义的需求。

DDD 有助于确保软件系统恰当地反映业务领域，使涉众更容易理解和使用。BDD 还可以改善团队沟通和协作，因为它需要开发人员、业务分析师和测试人员之间的协作。TDD 有助于确保代码的高质量，因为它要求开发人员在编写代码之前编写测试，这有助于在开发过程的早期识别问题。

# 😆现在，让我们跳到 BDD

行为驱动开发(BDD)是一种软件开发技术，它使用场景或例子来定义系统的行为。BDD 要求开发人员、业务分析师和测试人员一起工作来定义系统的行为，并为每个场景提供可接受的标准。BDD 旨在建立系统行为的共享知识，并确保它符合用户的需求。
BDD 的基本概念之一是它必须由业务需求和利益相关者的利益驱动。这表明开发过程应该基于业务目标和最终用户的需求，而不是系统的技术方面。这有助于确保系统对组织及其用户有益。
另一个重要的 BDD 原则是协作。BDD 需要几个团队之间的合作，包括开发人员、业务分析师和测试人员，以保证所有的观点都被考虑，并且系统满足所有涉众的需求。这可以改善开发团队内部的沟通和协作，并建立对系统行为的共同认识。

BDD 还需要使用例子或情况来定义系统的行为。这些示例用于为每个特性或需求开发验收标准，确保系统按预期运行并满足其用户的需求。这些例子可以用自然语言风格提供，比如英语，使它们对于非技术涉众来说更容易理解和实现。
BDD 可以改善开发团队内部和团队之间的沟通和协作，这是它的主要优势之一。BDD 可以帮助生成系统行为的共享知识，并通过在开发过程中集成几个利益相关者并利用例子来定义系统行为来确保系统满足其用户的需求。BDD 还有助于提高系统的质量，因为它使开发人员能够为每个特性创建验收标准，并根据这些标准测试系统。行为驱动的开发过程

# 😍行为驱动的开发方法

## 测试优先方法

测试优先的方法集中于在适当的时候测试产品，以保证实时的效率。它需要开发、测试和项目团队的敏捷性，以及在不同项目开发阶段使用的技术过程、原则和方法的清晰性。测试优先的方法消除了典型的开发和测试约束，在这些约束中，许多缺陷或瑕疵是在产品发布后才被发现的。因此，测试优先技术被认为是行为驱动开发中最重要的方法之一。
测试优先技术要求开发人员首先构建解释软件预期行为的自动化验收测试。这些测试是用自然语言语法构建的，以便非技术利益相关者能够理解它们。因为尚未编写实现代码，所以随后会执行测试来检查它们是否失败。

然后，开发人员编写特性或用户故事实现代码。然后，重新运行验收测试，以检查实现的特性或用户故事是否按预期执行。如果测试通过，开发人员可以确信特性或用户描述功能正常。如果测试失败，开发人员将能够发现并纠正实现代码中的任何问题。

## 敏捷测试方法

行为驱动开发和其他传统开发方法之间的一个关键区别是它独特的测试策略。它关注的是敏捷测试，而不是典型的构建、测试和修复错误的方法。敏捷测试建立在众所周知的迭代开发和测试技术之上，关注客户和团队的交流。

在敏捷测试策略下，测试经常被集成到开发过程中，作为开发团队日常工作的一部分。这有助于确保程序在创建时得到定期测试。为了确保产品满足最终用户的需求，敏捷测试方法强调开发人员、测试人员和利益相关者之间的协作和交流。

敏捷测试方法经常与行为驱动开发(BDD)结合使用。BDD 通过例子和场景帮助定义程序行为，并且自动化验收测试被用来确保软件按照预期执行。这有助于开发既可靠又可维护的软件，并对不断变化的需求做出响应。

## 内在质量方法

行为驱动的开发遵循内置的质量方法，这确保了最终产品具有所有必要的特性和解决方案，并且是市场现成的。仅仅收集功能和解决方案是不够的；它还必须以市场为导向，以客户为中心。行为驱动的开发通过确保满足所有终端用户需求的有竞争力的产品创造来解决这个问题。

# 🥰:那么每个阶段是如何运作的呢？

## 发现

接受标准在行为驱动开发的发现阶段被探索和选择。一般来说，产品经理积极地参与行为驱动开发的发现阶段。在这一阶段，根据产品类型、基本特征、目标受众、当前市场和其他变量制定验收标准。其他团队成员，如项目经理、开发人员、测试人员或操作团队，提供反馈。总的来说，在行为驱动开发的发现阶段，验收标准必须由团队成员合作开发。

## 配方阶段

制定阶段在发现阶段之后、实施阶段开始之前开始。当一个待定项即将被执行时，制定阶段尤其重要。此阶段的主要目标是保证验收标准已经过检查，并且适合实时使用。该要素通过验收测试在制定阶段实施
验收测试用于实施质量保证方法，以评估应用或产品是否符合规范。它根据最终用户的要求和认可决定了您可以接受产品的程度。因此，制定阶段的重点是将基本的验收标准转化为更稳定的版本，减少模糊性或缺陷。

## 自动化阶段

自动化阶段，顾名思义，自动化验收测试过程。它最大限度地减少了所需的时间和资源，同时保证获得所需的输出和标准。验收测试是自动化的，并在 BDD 的这个阶段持续执行，以验证和保证新的模式或行为与系统兼容。

# 🎶让我们看一个例子

> 让我们看看我们应该做什么..

## 定义业务目标

为了确保后端系统满足期望的规范，理解最终用户的业务目标和需求是很重要的。

定义业务目标和最终用户的需求是行为驱动开发(BDD)过程中的重要一步。这一步有助于确保正在开发的系统符合期望的规范，并且对企业及其用户有用和有价值，我们可以使用以下内容来定义它们:

1.  进行用户研究:这可能包括与最终用户交谈或进行调查，以了解他们的需求和目标。
2.  定义用户故事:用户故事是从最终用户的角度对系统的期望行为或功能的简短描述。这些故事可以用来定义最终用户的业务目标和需求。
3.  定义验收标准:验收标准是系统为了被认为是完整的而必须满足的特定条件。这些标准可以基于业务目标和最终用户的需求。
4.  使用客户反馈:客户可以对业务目标和最终用户的需求提供有价值的见解。通过使用客户反馈，开发人员可以确保系统符合预期的规范。

## 定义测试场景，用例子或场景来描述系统的预期行为

测试场景可以用来从最终用户的角度定义系统的预期行为。这些测试场景可以用自然语言格式编写，比如英语，这使得非技术的涉众更容易理解和使用。

根据示例或场景定义描述系统预期行为的测试场景是行为驱动开发(BDD)过程中的一个重要步骤。测试场景可用于从最终用户的角度定义系统的预期行为，并为每个功能或需求创建验收标准，我们可以通过以下方式定义测试场景:

1.  使用用户故事:用户故事是从最终用户的角度对系统的期望行为或功能的简短、简明的描述。这些故事可以用来定义描述系统预期行为的测试场景。
2.  定义验收标准:验收标准是系统为了被认为是完整的而必须满足的特定条件。这些标准可以基于业务目标和最终用户的需求。
3.  使用例子:例子可以用来以一种更加具体和明确的方式描述系统的预期行为。例如，如果系统是一个在线购物车，一个示例测试场景可能是:“作为一个客户，我希望能够将商品添加到我的购物车，并查看我的购物车的内容，以便我可以购买我选择的商品。”
4.  使用自然语言格式:测试场景可以用自然语言格式编写，比如英语，这可以让非技术涉众更容易理解和使用。

## 设计和构建后端系统，以满足测试场景中定义的预期

基于测试场景和验收标准，开发人员可以设计和构建后端系统来满足预期的行为和功能。

一旦在行为驱动开发(BDD)过程中定义了测试场景和验收标准，下一步就是设计和构建后端系统，以满足测试场景中定义的期望，我们可以设计一些方法:

1.  使用测试场景确定系统的关键特性和功能:测试场景可用于确定后端系统需要的关键特性和功能，以满足最终用户的期望。
2.  使用验收标准来指导系统的设计:验收标准可用于确保后端系统满足所需的规范，并按预期运行。
3.  使用模块化设计:模块化设计可以使后端系统的测试和维护更加容易。通过将系统分成更小的独立模块，开发人员可以单独测试和调试每个模块，这可以提高开发过程的效率。
4.  使用测试驱动方法:测试驱动方法包括在编写代码之前为一段代码编写测试。这有助于确保代码是正确的，并且符合所需的规范。

## 根据测试场景测试后端系统

构建后端系统后，开发人员可以根据测试场景测试系统，以确保它满足预期的行为和功能。

一旦在行为驱动开发(BDD)过程中设计并构建了后端系统，下一步就是根据测试场景测试系统，以确保它满足预期的行为和功能，测试我们可以使用的场景:

1.  使用自动化测试工具:有许多自动化测试工具可以用来执行测试场景和检查后端系统的行为。这些工具可以节省时间并提高测试过程的效率。
2.  使用测试驱动方法:测试驱动方法包括在编写代码之前为一段代码编写测试。这有助于确保代码是正确的，并且符合所需的规范。
3.  使用手动测试:在某些情况下，可能有必要根据测试场景手动测试后端系统。这对于测试复杂或难以自动化的场景非常有用。
4.  使用持续集成和交付:持续集成和交付(CI/CD)是一种软件开发实践，包括自动构建、测试和部署代码变更。通过使用 CI/CD，开发人员可以确保后端系统在每次代码更改时都得到自动测试。

# 🎃结论

最后，BDD 是一种软件开发方法，它专注于根据场景或实例定义系统的行为。BDD 需要团队合作和使用实例来开发每个项目的验收标准。BDD 的目的是建立系统行为的共享知识，并确保系统满足用户的需求。BDD 可以帮助增加开发团队内部的沟通和协作，以及系统质量。DDD、BDD 和 TDD 是软件开发的三种方法，可以用来提高过程的质量和效率。DDD 专注于业务领域的建模，BDD 专注于根据场景定义系统行为，TDD 专注于测试和确保代码与定义的需求相匹配。每种方法都有自己的一套思路和步骤，可以根据项目的需求一起使用，也可以单独使用。

> 希望你觉得这篇文章有趣🤩