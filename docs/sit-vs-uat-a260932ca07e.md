# 锡特对 UAT

> 原文：<https://blog.devgenius.io/sit-vs-uat-a260932ca07e?source=collection_archive---------0----------------------->

SIT(系统集成测试)和 UAT(用户验收测试)是测试过程的一部分，SIT 负责测试组件之间的接口以及与系统各部分的交互，如硬件、软件(操作系统和文件系统)和系统之间的接口。

![](img/7842d74e906a2967f36658cfb14deb1a.png)

相反，UAT (User Acceptance Testing)是一种从用户端执行的验证测试，检查用户需求和业务相关流程，以确定系统是否可以被接受。

# UAT:用户验收测试最佳实践

用户验收测试是系统被运行用户接受之前的最后一个测试阶段。最终用户根据用户需求规范执行 UAT，以确认应用程序是否满足需求。

当产品准备交付时，UAT(用户验收测试)在整个测试过程的末尾进行。软件开发的主要目的是开发能够满足用户需求的软件，而不仅仅是满足系统规格。

UAT 是在产品准备交付时进行的，也是在整个测试过程结束时进行的。UAT 用于验证系统是否可接受。

UAT 证实:

*   所开发的系统满足系统需求规格
*   系统已达到系统需求声明中记录的性能。
*   它可以根据合同中的定义而变化。

**UAT 的种类:**

有两种主要的用户接受度测试:Alpha 测试和 Beta 测试。

1.  **Alpha 测试** : Alpha 测试由客户在开发人员的站点进行。测试在开发人员的控制下进行。一旦系统测试完成，就进行 Alpha 测试。
2.  **Beta 测试** : Beta 测试由软件的最终用户在一个或多个客户处进行。对于一个应用程序的 beta 测试，它被交给一个可信任的客户。在这里，测试不受开发人员的控制。只有在 alpha 测试完成后，才会执行 Beta 测试。

## 验收准则

验收标准被定义为退出标准，系统必须满足该标准才能被最终用户接受。三个验收标准如下所示:

*   **产品验收** —规定当产品要求改变时，验收标准也必须根据需要进行修改和定义。
*   **程序验收** —可根据交付遵循的程序定义验收标准。
*   **服务水平协议** —服务水平协议只是客户和产品组织签署的合同的一部分，有助于作为验收测试的一部分验证软件。

# SIT:系统集成测试最佳实践

执行系统集成测试是为了确认单独测试的模块是否可以一起工作来提供所需的功能。单独测试的模块可能运行良好，但是当它们集成在一起时，可能会出现一些问题。执行系统集成测试是为了通过将数据从一个模块传输到另一个模块来测试模块之间的依赖性。

为了更好地理解什么是 SIT first，我们必须了解什么是系统集成？因此，正如其名称所暗示的，系统集成指的是一组阶段，其中各种组件被合并到一个单元中，这些单元进行集成测试，组件之间的交互组被称为集成和测试，这些交互和模块交互被称为集成测试。

从另一个角度来看，SIT(系统集成测试)被认为是集成测试和系统测试的结合。至此，我们知道了什么是集成测试。现在，我们需要了解什么是系统测试？对绝对集成产品进行测试，以检查系统是否符合功能和非功能元素的规定要求，这种测试称为系统测试。

SIT 也被认为是集成测试和系统测试的结合。

系统集成始于模块级，在模块级，各个单元集成在一起，形成一个子系统，最终形成一个系统。

## SIT 的类型:

有两种主要的系统集成测试方法:自顶向下的集成方法和自底向上的集成方法。

1.  **自上而下的集成方法**:模块通过在层级中向下移动来集成，其中主模块位于顶部。在自上而下的方法中，如果较低的模块没有准备好，则使用称为存根的虚拟模块进行测试。在测试过程中，存根充当模块。存根具有测试“上述”模块时需要使用的最小功能。
2.  **自底向上的集成方法**:在这里，模块被组合起来，并在非常低的层次上开始测试。如果顶层模块没有准备好，则使用驱动程序进行测试。驱动程序是专门用于测试的程序。

## 接口的类型

有两种接口——内部接口和外部接口。

*   **内部接口**促进了项目内部的两个模块之间的交互。
*   **外部接口**对于第三方开发者来说是产品之外的有形事物。

# UAT 与 SIT 的比较:

**SIT-系统集成测试**

*   模块间的测试接口
*   测试的目的是看接口
*   由开发人员和测试人员执行。
*   问题将与数据流，控制流。

**UAT-用户验收测试**

*   根据用户要求进行测试
*   目的是从最终用户的角度测试功能。
*   由客户和最终用户执行。
*   不符合用户要求。

# SIT 和 UAT 的主要区别

1.  SIT(系统集成测试)的目的是在集成所有系统组件后，测试系统的整体功能。另一方面，UAT(用户验收测试)负责从用户的角度测试系统。
2.  要进行 SIT 测试，需要专门的开发人员和测试人员。与此相反，UAT 是由购买软件产品的产品客户或组织执行的。
3.  系统集成测试在用户验收测试之前进行。
4.  SIT 中检测到的缺陷将与控制流、数据流等相关。相反，在 UAT，产生的问题是与用户需求不匹配的功能。

对于刚刚推出新网站或新应用程序的公司，我们为您提供了优惠。如果您不确定您的网站/移动应用程序是否安全无故障，我们可以为您提供免费的基础设施测试审计。

所以你可以知道你的应用程序是否让你的潜在客户感到沮丧。要申请免费审计，请发送电子邮件至 [StackedQA](http://stackedqa@gmail.com/) 并填写您的主题“免费测试审计”

在社交媒体上关注我们:

[脸书](https://www.facebook.com/StackedQA)，[推特](https://twitter.com/stackedqa)， [Instagram](https://instagram.com/stackedqa) ，&Linkedin

[](https://husseinbaashen.medium.com/membership) [## 通过我的推荐链接加入媒体-侯赛因巴申

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

husseinbaashen.medium.com](https://husseinbaashen.medium.com/membership)