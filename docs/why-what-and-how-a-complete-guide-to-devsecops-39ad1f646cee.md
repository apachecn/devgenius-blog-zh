# 为什么、什么和如何:DEVSECOPS 完全指南

> 原文：<https://blog.devgenius.io/why-what-and-how-a-complete-guide-to-devsecops-39ad1f646cee?source=collection_archive---------4----------------------->

DevSecOps 是开发、安全和操作的缩写，是一个在软件开发周期的每个阶段集成安全性的过程，从最初的设计到集成、测试开发，最后是软件交付。DevSecOps 方法彻底改变了组织在其软件构建过程中实现安全性的方式。传统的安全方法让组织只在软件开发生命周期的末尾执行安全检查或测试。该方法的重点主要是应用程序开发和产品交付，而不是安全性。当测试人员或工程师检查软件的错误时，产品应该已经通过了开发的初始阶段，并且几乎完全开发出来了。在这么晚的阶段发现并纠正错误和安全威胁意味着从头开始重新编写代码，这是一个非常艰巨和耗时的过程。因此，打补丁成为解决漏洞和安全威胁的首选方案或修复方法。

网络犯罪的扩散导致了这种先进的方法。最初，软件更新或补丁每年只发布一次或两次。随着开发者致力于缩短软件开发周期，攻击的增加使得传统的附加方法变得无用。

**阅读:** [每个开发人员应该知道的关于威胁建模的事情](https://securetriad.io/what-every-developer-should-know-about-threat-modelling/)

# 为什么是 DEVSECOPS？

DevSecOps 是一个将安全性集成到软件开发工作流程的每个阶段的过程。这有助于在每个阶段发现问题时解决问题，而不是完全开发产品，然后在最后阶段解决安全问题。这样，修复威胁或缺陷就更容易、更快、更便宜、更省时。DevSecOps 是一种方法，它指出安全是开发、安全和运营团队的共同责任，而不是在一个竖井类型的结构中工作。这确保了快速和安全的产品交付，在 DevSecOps 方法出现之前，这在安全行业只是一个矛盾的说法。

# DEVSECOPS 的优势

DevSecOps 方法的主要目标是将安全性作为不同团队的共同责任，并确保快速和安全的代码交付，安全性是主要的组成部分。以下是好处:

**快速而经济的软件交付:**当软件在非 DevSecOps 环境中开发时，由于测试阶段是在产品完全开发完成后进行的，因此安全延迟和修复可能会导致巨大的时间延迟。这可能是一个昂贵的事情，以及代码需要返工和从头开发。DevSecOps 在每个阶段都集成了安全性，解决了每个阶段的安全问题，并且通过避免重复流程和程序节省了时间。这种集成的方法消除了返工、不必要的重建以及重复或多次审查，从而使其成为一种经济高效且快速的事情。

**更好的协作和改进的安全性:**由于安全性是从软件开发周期的开始就集成的，所以在每个阶段的结尾都要对安全代码进行检查、审计、扫描和安全缺陷测试。在引入和实现额外的或新的依赖项之前，立即处理或解决安全问题。开发、安全和运营团队共同承担安全责任，提高了组织对安全事故和错误的响应能力，从而减少了开发时间。

**加速安全补丁:**没有一个系统是故障安全的，当新的漏洞和威胁出现时，DevSecOps 方法可确保快速管理漏洞。这种方法及时地将漏洞扫描和修补集成到发布周期中，从而限制了攻击者在软件发布和修补程序发布之间的威胁和机会窗口。

自动化过程:如果一个组织为软件开发执行一个持续的集成管道过程，那么它可以将安全测试集成到一个自动化测试套件中。这种自动化生产过程依赖于开发的产品和组织目标。

**适应性强的流程:**随着组织的发展，他们的安全需求和流程也在发展。DevSecOps 是一个可重复且适应性强的流程，它集成了安全性并在新环境中一致地实施共享的安全模型，以满足新的需求和要求。一个完全成熟的 DevSecOps 实现具有可靠的自动化、强大的配置系统、稳定的编排和强大的基础设施环境。

**另请参阅:** [SQL 注入-攻击和预防](https://securetriad.io/sql-injection-attack/)

# DEVSECOPS 中的测试类型

在 DevSecOps 方法中有两种类型的测试过程

**连续测试:**这是作为软件交付管道的一部分，执行和实施连续的自动化测试流的过程，以便在每次实现代码变更时接收反馈。通过反馈和质量提高来改进是持续测试过程的主要目标

**功能测试:**这是一个过程或测试方法，确保一个部分或一个软件按照预先确定的要求正确运行。示例包括单元测试、回归测试、冒烟测试、生产测试和 API 测试。

# 在 DEVSECOPS 中哪里测试？

**IDE:** 集成开发环境是包含源代码编辑器、构建自动化工具和用于创建软件的调试器的应用程序。在 IDE 上进行测试有助于实现符合业务需求的内置安全特性，并创建健壮的软件。

**扫描工具:**自动扫描并检测每个阶段的漏洞和 bug。非常推荐应用程序源代码的静态代码分析。高度定制的扫描器在搜索或检测预定义的漏洞和错误方面非常有效。

**Pentesting:** 完全集成到 DevSecOps 环境中，为不同的团队带来价值。虽然它的缓慢和不灵活的本质是将其集成到 DevSecOps 方法中的一个挑战。它在发现连锁利用和业务逻辑问题的地方工作得最好。是一个强大的防御层，用于检测自动检查未能发现的漏洞。

**回归:**这是一个测试过程，测试以前开发或测试过的功能，以确保在实施变更后，新软件版本发布前，功能按照要求运行。

**手动代码审查:**这是通过与开发、安全和操作团队协作，通过逐行审查代码来检查错误和漏洞而完成的。虽然这种 f 型测试是安全的，并且增强了安全性，但是它需要大量的技能、耐心和时间。

*本文最初发表于 2021 年 10 月 26 日的*[https://securetriad . io/why-what-and-how-a-complete-guide-to-devsecops/](https://securetriad.io/why-what-and-how-a-complete-guide-to-devsecops/)