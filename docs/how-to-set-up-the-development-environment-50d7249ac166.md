# 如何设置开发环境

> 原文：<https://blog.devgenius.io/how-to-set-up-the-development-environment-50d7249ac166?source=collection_archive---------5----------------------->

> **如何准备开发电脑**

所以，现在是 2019 年 2 月，我在研究生院的第二个学期；我想把工作和学习结合起来，以获得更多的实践经验，并在工作场所测试我的知识。我开始了新的工作岗位；从事各种云迁移(AWS)、移动应用和 web 开发、物联网试点项目等项目。所以我真的很兴奋，这是一个获得经验和学习更多东西的好机会。

![](img/d357c84ee08db05f652e38c1a517b323.png)

如果你刚刚开始一个新的 IT 职位，涉及软件开发或任何与编写代码相关的事情，那么需要做一些事情来为开发做好准备；让您的计算机为开发做好准备。在本文中，我将与大家分享我在准备电脑时完成的几项任务，以及如何设置开发环境。

# **IDE 集成开发环境**

您可能想做的第一件事就是安装最适合您将要从事的项目的 ide。集成开发环境(ide)是一种软件平台，它为程序员和开发人员在单一产品中进行软件开发提供了一套全面的工具。ide 是为与特定的应用程序平台一起工作而构建的，它消除了软件开发生命周期中的障碍。

![](img/98a9b4cd41f445b6e4c04b23249fdc46.png)

Atom IDE 截图

ide 在开发团队中用于构建新的软件、应用程序、网页和服务，它们通过提供一个具有所有功能的工具来提供帮助，并且消除了集成的需要。

ide 用于为一个或多个特定平台编写代码，并具有集成的功能，这些功能知道平台如何工作，以及如何通过编译代码、调试代码或智能地自动完成代码来使用平台的功能。

> **一些流行的免费 ide:**[**Visual Studio**](https://www.g2crowd.com/products/visual-studio/reviews)**，** [**Atom**](https://atom.io/) **，**[**py charm**](https://www.g2crowd.com/products/pycharm/reviews)**，**[**Eclipse**](https://www.g2crowd.com/products/eclipse/reviews)**，**[**IntelliJ IDEA**](https://www.g2crowd.com/products/intellij-idea/reviews)**，** [**Xcode 有关 IDE 的更多信息，请查看 g2crowd.com**上发布的](https://www.g2crowd.com/products/xcode/reviews) [**最佳集成开发环境**](https://www.g2crowd.com/categories/integrated-development-environment-ide) **(IDE)软件**

# 包装管理系统

一个**软件包管理器**或**软件包管理系统**是一个**软件**工具的集合，它们以一致的方式自动执行安装、升级、配置和删除计算机操作系统的计算机程序的过程。(来源:维基百科)

![](img/5c318b08cdd1996d4b793ef258c9f6c9.png)

它们肯定是你将要从事的许多项目需要安装的各种软件。软件包管理系统简化了软件在计算机中的安装，使安装过程不那么复杂。

> 一些流行的软件包管理系统:npm，APT，yum，Homebrew，pip，Chocolatey，NuGet，Anaconda，ProGet 等。

## **自制**

[**Homebrew**](https://brew.sh/) 是一款免费开源的软件包管理系统，简化了软件在苹果 macOS 操作系统和 Linux 上的安装。我强烈推荐 mac 用户使用自制软件。

## 节点 Js & NPM

**节点**。 **js** 是一个基于 Chrome 的 JavaScript 运行时构建的平台，用于轻松构建快速且可扩展的网络应用。**节点**。js 使用事件驱动的非阻塞 I/O 模型，这使得它轻量级且高效，非常适合跨分布式设备运行的数据密集型实时应用。(来源: [TutorialPoint](https://www.tutorialspoint.com/nodejs/nodejs_introduction.htm) )。

![](img/89c07e412af854ef5cc1714afd3ed1a1.png)

> **Node.js 和 npm 是用于许多框架平台的现代软件和 web 开发的基础。节点程序包管理器(npm)广泛用于安装软件、库依赖项、软件更新和其他相关任务。如果您的计算机上没有安装这些软件，请立即获取。**

# 调试工具

**调试**是检测和消除软件代码中现有的和潜在的错误(也称为“bug”)的**过程**，这些错误会导致软件代码意外运行或崩溃。为了防止软件或系统的错误操作，使用**调试**来发现并解决错误或缺陷。

> **Chrome 开发者工具**

Chrome DevTools 是一套直接内置在谷歌 Chrome T21 浏览器中的网络开发工具。DevTools 可以帮助你即时编辑页面并快速诊断问题，最终帮助你更快地建立更好的网站。使用 DevTools，您可以查看和更改任何页面。更多细节请看 [**Chrome DevTools 教程**](https://developers.google.com/web/tools/chrome-devtools/) 。

我还建议修改 HTTP 状态码。有几件事对你的调试能力至关重要。谈到调试，您需要:

*   理解错误代码或消息的含义(例如什么是 CORS 错误)
*   它来自哪里(服务器端、本地计算机、语法错误等)
*   知道在哪里可以找到关于修复这些错误的信息(谷歌或者利用其他资源:StackOverflow，tutorial 等等。)

# Bash_profile | Mac 用户

在 Mac 的用户目录中有一个名为的隐藏文件。 **bash_profile** 。你更有可能做一些文件设置来运行一些包或者在你的 Mac 上安装软件。这个文件，。 **bash_profile** 针对登录 shells 执行，而。bashrc 是为交互式非登录 shells 执行的。

**。bash_profile 是在 Terminal 加载您的 shell 环境之前加载的，它包含您的命令行界面的所有启动配置和首选项。当您通过控制台登录(键入用户名和密码)时，无论是坐在机器上还是通过 ssh 远程登录:。 **bash_profile** 在初始命令提示符之前被执行来配置您的 shell。**

这是我如何组织我的？我的 **Mac** 上的 bash_profile:

> 如果你喜欢这个故事，你可能也会喜欢“ [**编码面试:问题解决技巧**](https://medium.com/coinmonks/coding-interview-problem-solving-techniques-ae6a82d98dbb) ”
> 
> 请给它几个掌声支持！

> 干杯！！！