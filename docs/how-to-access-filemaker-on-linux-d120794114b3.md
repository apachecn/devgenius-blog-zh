# 如何在 Linux 上访问 FileMaker

> 原文：<https://blog.devgenius.io/how-to-access-filemaker-on-linux-d120794114b3?source=collection_archive---------8----------------------->

![](img/478195db05be8bf46ff127cf52981651.png)

你可能听说过克拉丽丝女团推出了一个 Linux 版本的文件服务器。随着克拉丽丝女团新 Linux 版 FileMaker 服务器及其基于命令行的环境的推出，许多人想知道如何访问他们的备份和其他相关文件。嗯，这并不像许多人想象的那么难。但是首先，在我们开始之前，我们需要回顾一些关于云服务的基础知识。

# 一切都在计划之中

我们将使用一个基于 Azure 的云实例，但 AWS 和其他提供商将是类似的。当我们设置第一个虚拟机(VM)时，我们的提供商可能会问我们希望如何对其进行身份验证。

![](img/ce9b2468a9e8b5747f92c7f665a7492f.png)

在大多数情况下，我们希望选择私钥选项，因为这是一种非常安全的方式来验证和加密我们与虚拟机之间的连接。一旦我们下载了密钥，请把它放在一个安全的地方，因为我们不会有第二次机会访问它…一次下载是我们得到的全部。我们可能会发现，在使用它之前，我们必须通过发出以下命令来更改权限:

![](img/1bb6a44bb2612f0a584798a000827669.png)

接下来我们需要的是服务器的地址。我们必须找到它，因为没有它我们就不知道该连接到哪里。如果我们在服务器上安装了自定义 SSL 证书(为了安全和无故障运行，我们应该这样做)，那么我们可以使用该地址。我们也可以使用证书颁发给的完全合格的域名(FQDN)，例如 fms.mydomian.com。否则，我们可以使用分配给虚拟机的 IP 地址。使用 FQDN 通常更好，因为大多数提供商对静态 IP 地址收取额外费用。现在让我们使用我们选择的文件传输协议(FTP)客户端。在这种情况下，我们使用的是跨平台应用 Cyberduck。我们创建了一个新的连接，并将类型指定为安全文件传输协议(SFTP)，用户名为“azureuser ”,因为我们在 Azure 上建立了虚拟机，这是我们的默认选择。

![](img/4c314b377bc244a251a28d01e86d5573.png)

创建连接后，我们只需双击列表中的链接即可打开它。系统可能会提醒我们，我们正在连接一个具有“未知指纹”的服务器我们收到这个通知是因为我们之前没有保存这个服务器的连接信息，所以它是未知的。

![](img/e17891d85b710addb89c295ba3f96f73.png)

在我们点击“允许”之前，请确保选中“总是”选项，这样我们就不会再次收到这种可怕的警告。我们现在应该会看到一个窗口，显示“/home/azureuser”文件夹中的所有文件。这个目录是用户的主文件夹，所以如果我们想上传一些东西到服务器，我们可以把它拖放到这里，然后使用命令行把它移到 FileMaker 服务器文件夹。

但是，我们正在尝试访问 FileMaker 备份文件夹，默认路径是“/opt/FileMaker/FileMaker Server/Data/Backups/”Cyberduck，以及大多数 GUI 驱动的 FTP 客户端，工作起来很像 MacOS Finder 或 Windows 文件资源管理器，所以我们应该感觉像在家里一样上下移动文件夹树。

![](img/e8b4fbfc12b22f3c15d4dfc933086256.png)

现在我们已经到达了服务器的备份文件夹，我们可以继续将我们想要的任何备份拖放到我们的桌面计算机上，下载将自动开始。

如您所见，如果我们知道该做什么，访问基于 Linux 的 FileMaker 服务器的备份文件夹的过程就非常简单了。在下一篇文章中，我们将讨论如何通过几个简单的命令在云驱动器上保存备份副本。[敬请期待](https://blog.supportgroup.com/browsemode-subscription?utm_source=BlogPost-2021-01-21&utm_medium=Medium&utm_campaign=traffic)。

如果您错过了，请了解如何优化 [FileMaker 服务器性能](https://blog.supportgroup.com/optimize-filemaker-server-performance?utm_source=BlogPost-2021-01-21&utm_medium=Medium&utm_campaign=traffic)的更多信息。

*原载于 2021 年 1 月 21 日 https://blog.supportgroup.com*[](https://blog.supportgroup.com/how-to-access-filemaker-on-linux?hs_preview=ncqTUjwl-40711239217)**。**