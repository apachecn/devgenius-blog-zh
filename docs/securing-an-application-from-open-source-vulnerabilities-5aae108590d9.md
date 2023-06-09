# 保护应用程序免受开源漏洞的影响

> 原文：<https://blog.devgenius.io/securing-an-application-from-open-source-vulnerabilities-5aae108590d9?source=collection_archive---------15----------------------->

![](img/43e0ef24bc205b171f374eb016084396.png)

沙哈达特·拉赫曼在 [Unsplash](https://unsplash.com/s/photos/open-source?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄的照片

随着开源解决方案使用的增加和第三方库在大多数应用程序中的接受。越来越重要的是，不仅要保护我们的应用程序免受我们的代码可能引入的漏洞的影响，还要保护它免受我们添加到应用程序中的开源库代码所诱发的漏洞的影响。

最近，当一个包中报告了严重的漏洞时，整个行业都感到震惊，该包用于大多数 java 应用程序的日志记录，即 log4j。由于更广泛的使用，影响是广泛的，甚至由于活跃的社区和软件包维护者，漏洞的修复也是尽快可用的。

在这种情况下，漏洞在被报告之前不为任何人所知。但是我们确实有这样的情况，应用程序使用的依赖版本已经报告了严重的漏洞。

在这种情况下，保护 web 应用程序取决于多种因素。

首先要为您的项目选择合适的依赖项，这取决于以下因素:-

1.  选择下载次数多的依赖项。

为了解决一个问题，可以有多个库可用。当选择一个库时，有多少用户在使用一个特定的库应该是我们在应用程序中选择使用哪个库的一个考虑因素。

2.贡献者人数

社区越大，获得 bug 和安全补丁支持的机会就越大。因此，在选择一个包时，需要注意的一个关键因素是包的贡献者和维护者的数量。

3.释放模式

很有可能一个包非常有名，但是在很长一段时间内，围绕这个包没有最新的发布。我们可能会注意到一个非常大的软件包社区，因为它在过去被广泛使用。因此，检查这个包在最近是否仍然有发布将增加选择这个包的保证。

4.检查您选择的版本是否存在漏洞

你已经选择了一个最新版本的包，因为基于以上几点，这是最好的选择。但是，您仍然可以检查该版本是否有一些已经报告的漏洞。在这里，您需要浏览报告此类漏洞的安全咨询页面。例如:-

[](https://github.com/advisories) [## GitHub 咨询数据库

### 包含 CVEs 和 GitHub 的安全漏洞数据库源自开放世界的安全建议…

github.com](https://github.com/advisories)  [## CVE 安全漏洞数据库。安全漏洞、利用、参考等

### 在 6.8.1.0 之前的 Malwarebytes Binisoft Windows 防火墙控制中，从工具选项卡执行的程序可用于…

www.cvedetails.com](https://www.cvedetails.com/vulnerability-list/) 

这种咨询可以帮助您寻找已经报告的漏洞。

> 基于以上几点选择依赖关系是非常重要的，因为如果正确遵循以上几点。如果您正在使用的任何软件包将来报告了漏洞，这是一个很好的机会。你将尽快解决这个问题。

现在，您根据以上几点选择了一个依赖项。在添加它的时候，所选择的依赖项和版本没有任何报告的漏洞。但是随着时间的推移，我们需要确保我们在添加时所做的调查仍然适用于当前的场景。

有很多事情可以解决这个问题。

1.  定期审核您的应用程序。

许多依赖项管理解决方案现在都带有内置的漏洞扫描器，用于在项目中添加依赖项。这种扫描器基本上检查所有添加到咨询库的包，就像我上面分享的那些。例如，使用 **npm** ，您可以运行以下命令来了解此类漏洞

> npm 审计

你可以在这里阅读更多关于 npm 审计的内容

[](https://blog.npmjs.org/post/173719309445/npm-audit-identify-and-fix-insecure.html) [## npm 博客存档:“npm 审计”:识别并修复不安全的依赖关系

### 上个月，我们发布了 npm@6，它包含了一个保护代码安全的强大的新工具，npm audit…

blog.npmjs.org](https://blog.npmjs.org/post/173719309445/npm-audit-identify-and-fix-insecure.html) 

2.DevSecops

您可以将审计作为构建管道的一部分。像 Jenkins 这样的工具带有插件，您可以将这些插件添加到您的管道中，对您的应用程序进行深度扫描，并让您了解当前的漏洞。如果报告的漏洞超过设置的阈值，可以设置不同的阈值来使构建基本上失败。

3.及时的依赖关系更新

尽可能依赖最新版本是至关重要的。因为最新版本通常带有错误修复和安全修复。在这种升级中，依赖关系通常也会升级它们正在使用的内部软件包。因此，如果可能的话，我们应该尽可能将我们正在使用的依赖项保持在最新版本。

> **在这种情况下，比方说在获得一个软件包的审计报告后，你觉得正在使用的软件包现在没有得到积极的维护，并且获得漏洞修复的机会非常小。然后，是时候按照我们上面已经讨论过的要点寻找一个替代包了。**

这样做可能不会成为对付未知漏洞的灵丹妙药，但肯定会帮助我们避免公开的、为更多人所知的漏洞。因为公开存在的漏洞更有可能被更广泛的怀有恶意的受众尝试和利用。

> 我已经试着涵盖了我所能想到的观点，如果在这篇文章的评论中找到一个有效的观点，我会添加进来。不断阅读，不断学习，不断成长。