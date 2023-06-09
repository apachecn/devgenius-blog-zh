# 在 Azure 批处理中运行您的应用程序

> 原文：<https://blog.devgenius.io/run-your-applications-in-azure-batch-4d5be5bf5a7d?source=collection_archive---------9----------------------->

了解如何在 Azure Batch 中运行代码，以及如何将应用程序包部署到计算节点

# 问题陈述

从内部部署到云的 SQL 迁移带来了迁移 SSIS 包方面的挑战，尤其是在考虑 PaaS 服务(如 Azure SQL 或 Azure 托管实例)时。之前，我在下面的文章中谈到了如何使用 Azure Data Factory (ADF)中的 SSIS 集成运行时来迁移您的 SSIS 包[使用 Azure SQL Server 托管实例运行您的 SSIS 包](/run-your-ssis-packages-using-azure-sql-server-managed-instance-d98f652b9e82)

然而，许多企业拥有在 SQL 代理作业中调用的**可执行文件**，作为其工作流步骤的一部分，这种情况也很普遍。这些可执行文件通常或传统上是用**编写的。Net** 平台上使用 Visual Basic (VB)或 C#开发。这带来了新的挑战，因为云 PaaS 服务不支持运行可执行文件，如**。exe** 里面。此外，这些可执行文件通常还会在虚拟机或裸机中从运行 SQL Server 的本地驱动器或网络共享中读取或写入数据，这带来了更多挑战，因为在 PaaS 服务中无法访问本地驱动器。这涉及到代码的重构，以使用 Azure Blob 存储。

更大的问题是，我们如何解决它？我们可以考虑两种主要的解决方案:

1.  天蓝色批料
2.  Azure 功能 App

在这篇文章中，我将谈论 Azure Batch 以及它如何解决这个场景并帮助您的 ETL 过程云本地化。

# 概观

Azure Batch 创建并管理计算节点(虚拟机)池，安装您想要运行的应用程序，并调度作业在节点上运行。批处理可以很好地处理本质上并行(也称为“令人尴尬的并行”)的工作负载。这些工作负载的应用程序可以独立运行，每个实例完成部分工作。

# Azure Batch 是如何工作的？

下图显示了常见批处理工作流中的步骤，其中客户端应用程序或托管服务使用批处理来运行并行工作负载。

![](img/3531f3362cb8ed394f6acee024280ee1.png)

[Azure Batch 在云中运行大型并行作业——Azure Batch | Microsoft Learn](https://learn.microsoft.com/en-us/azure/batch/batch-technical-overview)

值得注意的是，上面的图表显示了使用 Azure Batch 的一种方式，还有许多其他适合您的用例的方式来实现它。

# 体系结构

下图显示了该解决方案的高级架构。

![](img/a44ef1dcc565521f2a264a17318e861f.png)

1.  Azure 批处理池在虚拟网络(vNet)的子网中提供。还需要注意的是，vNet 必须与用于创建池的批处理帐户位于同一订阅和区域中。
2.  只要预先分配了足够的 IP 地址空间，就可以在同一个虚拟网络或子网中创建多个池。
3.  池中的计算节点可以与 Azure SQL 托管实例通信，因为它也在同一个 vNet 中配置。
4.  池中的计算节点可以通过连接到同一虚拟网络中的子网的专用端点访问存储 blob。

如需了解更多 Azure Batch 网络需求，请访问以下链接[在虚拟网络中调配池— Azure Batch | Microsoft Learn](https://learn.microsoft.com/en-us/azure/batch/batch-virtual-network)

# 部署 Azure 批处理

本文的剩余部分将涵盖部署 Azure Batch 的逐步指南。

## 创建 Azure 批处理帐户

创建池和作业需要批处理帐户。存储帐户还可以链接到批处理帐户，有助于部署应用程序和存储大多数工作负载的输入/输出数据。

在 Azure portal 中，查找批处理帐户并选择“创建”

![](img/2467a687918b12eb0a5654346b8fffbe.png)

## 创建一个计算节点池

创建批处理帐户后，创建一个 Windows 计算节点示例池。

在批处理帐户中，选择池→添加

![](img/350efd916bf81c9b8f35aca85683f1ba.png)

输入以下内容:

![](img/6fecd655eb0aa4abac3012f302950dc6.png)![](img/08d3f6496e4540f8d5900d9fa7588011.png)

向下滚动并添加节点大小和比例设置，如下所示。建议的节点大小提供了性能与成本的良好平衡。

![](img/1799c7e3fab8e332dac050adf9ac1e2a.png)

进一步向下滚动以输入虚拟网络信息。指定一个 vNet 并为 Azure batch 选择一个子网，如前面在架构图中提到的。确保没有其他工作负载或资源连接到该子网。

![](img/5351d55914d42fef6e2205c7a218c0cc.png)

单击“确定”创建池。

批处理池会立即创建。但是，分配和启动计算节点需要几分钟时间。在此期间，您可以在调整池大小时继续前进到创建作业和任务的下一步。几分钟后，分配状态将变为“稳定”,节点将启动。当节点状态为“空闲”时，它准备好运行任务。

## 创造一份工作

创建池后，我们可以创建一个作业在其中运行。批处理作业被分成一个或多个任务组。

1.  在批处理帐户视图中，选择作业→添加
2.  在作业 ID 中，提供一个名称，如“myjob ”,如下所示。
3.  在池中，选择您在前面的步骤中创建的池。
4.  其余设置保留默认值。
5.  单击“确定”

![](img/5c87462c1c19414a424d92c119c6d5cd.png)

## 添加新应用程序

在这一步中，我们将添加一个用 C#编写的应用程序。**样例应用程序代码及其开发步骤将在本文的后面部分进行概述。**

> 在进行到这一步之前，请确保您已经编译好应用程序…

使用应用程序包，您可以上传和管理任务运行的应用程序的多个版本，包括它们的支持文件。然后，您可以将这些应用程序中的一个或多个自动部署到您的池中的计算节点。

要使用应用程序包，将存储帐户链接到批处理帐户非常重要。您可以通过点击批量账户→存储账户来验证存储账户是否链接，如下图所示。

![](img/e0885beb3ed5c0eda1ebefd24c8ab6bd.png)

要创建应用程序，请执行以下操作。

1.  在批处理帐户中，单击应用程序→添加

![](img/b8a96c8a1a09f2ba6607cacdfc9bdecc.png)

2.提供应用程序 Id、版本，并将应用程序包上传到。zip 格式

![](img/d682cbeb8e43ccd4475add3c1a56caf2.png)

3.这将在链接的存储帐户中上传应用程序，如下所示。

![](img/9958507bff589738127f4fe92e986b3d.png)

添加应用程序后，您可以在批处理帐户的应用程序选项卡中验证它，如下所示。

![](img/e2b14a4efe051dabdc0b112ee36d4e4a.png)

## 创建任务

现在选择作业。要创建任务，请执行以下操作。

1.  批处理帐户→作业→添加

![](img/9f6bc1f25ef0b009508817f59edc1cf0.png)

2.输入任务 ID，如 task01，如下所示。在命令行中，输入以下命令。

```
cmd /c “%AZ_BATCH_APP_PACKAGE_demo02#1.0%\\demo02.1.0\demo02.exe”
```

![](img/500d84e99f9658709aecac60d65e6a36.png)

3.向下滚动并选择在前面步骤中上传的“应用程序包”。单击应用程序包，如下所示。

![](img/d0b85207b87d15680597d2bcc4a788a7.png)

4.选择要在任务中部署的应用程序及其版本号。

![](img/4416c178c78df2576792c01a48f02b7b.png)

# 确认

让我们验证一下是否一切都按我们预期的方式运行！！！

在验证过程中，请遵循以下步骤。

创建任务后，请访问批处理帐户→作业→任务

![](img/bfd76454f0245cbe7e6027be2a2e532a.png)

在这种情况下，单击 task01 等任务。任务提交后，进入“运行”阶段，然后“完成”，如下图所示。

![](img/e23b0dcd7f6289338d20010a0a241ccf.png)

一旦状态为“完成”，如下所示。单击左侧窗格中的“节点上的文件”。

![](img/f53e123e369c39599ee29f1a5d709fa7.png)

点击 stdout.txt 如下图。如果任务由于某种错误而失败，您可以看到 stderr.txt 文件。

![](img/b6ccc2f25b9468e1a02d21368d3dd8bc.png)

下面是在计算节点中作为任务运行的控制台应用程序的输出。

![](img/5b248967589f630d65dc3deb10ff22e7.png)

## RDP 到节点

如果您想进行更深入的故障排除，还可以对计算节点执行远程桌面。

单击任务选项卡中的节点，如下所示。

![](img/af60e474a1736cfe9a7c4c1f5047c7e8.png)

点击“连接”。您可以生成一个随机用户，如下所示。

![](img/0c2a9da463d0984ea6f0f3b63bf355c7.png)

一旦通过 RDP 进入节点，您也可以手动执行程序。

![](img/237c20d361402a90e326e5b9d66a344e.png)

C#代码也下载了。来自 Azure 存储帐户的 txt 文件。您还可以验证文件是否从 blob 下载到计算节点。

![](img/ea24556071e0d28525bc6d4d4dd1aa39.png)

## 验证 SQL MI 中的输出

C#代码从存储帐户下载文本文件，解析/转换它，然后将数据上传到 SQL MI 数据库表中。这可以通过运行如下所示的 SQL 查询来验证。

![](img/efbc7f1954776c99d5e1e099f3a27df7.png)

# 在 Visual Studio 中设计和开发应用程序

在本文中，我使用 visual studio 开发了一个非常简单的 c#应用程序。该应用的范围如下。

1.  下载。Azure 存储 blob 容器中的 txt 文件
2.  读取文本文件中的每一行，并将其转换为固定的字段变量。
3.  将每一行插入在 Azure SQL MI 中预先创建的 SQL 表中。

## 创建新项目

启动 Visual Studio 并创建一个新项目。在 C#中选择控制台应用程序，如下所示。

![](img/d2d31e3b3789b14629ee28bef12415f0.png)

配置您的项目。指定项目名称、位置和解决方案名称。

![](img/8754dcfaff9c507abbd4d7c1c36b29d3.png)

在附加信息中，选择。网络核心 3.1

![](img/931a0b5558cc558d2bce357715f0513a.png)

## C#代码

让我们开始编码…

本文中使用了以下代码。此应用程序将存储帐户和 SQL MI 的连接字符串信息存储在 App.config 文件中。但是，在生产级设置中，强烈建议使用 Azure Key Vault 和/或托管身份连接到存储帐户和 SQL MI。

编译、运行和测试代码。

> **注意:如果您对存储帐户使用私有端点，对 SQL MI 使用私有 IP，除非您通过 VPN 客户端连接到您的 VPN 网关，否则代码不会在本地成功执行。**

## 发布您的代码

一旦您运行了构建并且没有发现错误。您可以发布您的应用程序。右键单击项目，然后选择“发布”，如下所示。

![](img/844cc6f661ef0ee2f6b55e3293348679.png)

确保将部署模式选择为“自包含”。将您的应用程序发布为*自包含的*会生成一个包含。NET 运行库和库，以及您的应用程序及其依赖项。该应用程序的用户可以在没有的计算机上运行它。已安装. NET 运行时。

![](img/7948c7aa7d3d5d1c2ae28ebf047e90e4.png)

如果您的部署模式不是*自包含*，而是*依赖于框架*，那么当它在计算节点中运行时，您将看到以下错误。它将失败。Net 依赖项在计算节点中不可用

![](img/a761b2c14e70bbeb5036118c83e6fc2d.png)

最后，压缩您发布应用程序的文件夹，并将其上传到批处理帐户应用程序。

# 结论

批处理帐户是以云本地方式运行您的自定义代码的一种很好的方式。它为执行用。Net、python、java 等等。它允许您调配基于 Windows 和 Linux 的计算节点。批处理帐户可以在 Azure 数据工厂管道中使用批处理服务活动，其中自定义代码需要在编排的工作流中执行。