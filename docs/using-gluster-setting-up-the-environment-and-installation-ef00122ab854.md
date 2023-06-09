# 使用 Gluster:设置环境和安装。

> 原文：<https://blog.devgenius.io/using-gluster-setting-up-the-environment-and-installation-ef00122ab854?source=collection_archive---------15----------------------->

这是给那些想开始使用 Gluster 的人的一个指南，g luster 是一个免费的开源可扩展网络文件系统。(有各种各样的官方文档可以使用，这些文档将采用一种通用的方法，这更多的是对我开始使用 gluster 时所采用的方法的描述。)

![](img/5d00c95dec9006994e36aec1c5e768e0.png)

在开始安装 Gluster 和其他操作之前(我们将在下面的故事中介绍)..)，我们必须解决基本环境和依赖关系。

Gluster 是一个集群网络文件系统，这意味着我们可能需要设置集群的底层机器来进行测试。现在，人们不需要多台机器就可以尝试 gluster 的基本功能。

答案是用 VM 托管多台机器，给这些 VM 附加磁盘，然后玩 gluster。

现在，我使用基于 nix 的操作系统，具体来说，fedora 32。Linux 内核有一种叫做[内核虚拟化](https://en.wikipedia.org/wiki/Kernel-based_Virtual_Machine)的东西。使用这个特性，只需安装一个虚拟管理器。我正在使用[虚拟管理器](https://virt-manager.org/)。我认为可以查找 virt-manager 所需的依赖项和安装步骤。(另外，一定要了解使用 virt-manager 的基础知识。目前，我不会添加关于如何使用 virt-manager 的额外信息。虽然我应该在未来增加一个。)

一旦安装了您选择的虚拟化管理器，您就可以尝试如何创建 VM、修改其网络设置、存储等。

现在，一旦您熟悉了虚拟机的创建、网络设置和磁盘分配，我会建议您创建一个带有 Fedora32 的虚拟机，比如说，如果可能的话，20GB 存储、2 GB RAM 和 2 个 CPU，还要将一个大约 10 GB 的磁盘连接到该虚拟机作为存储。在这个虚拟机上完成所有安装后，我们可以稍后克隆它，这样就不必为每个虚拟机单独设置环境。

接下来，我们将安装 gluster 的依赖项。现在，您可以选择源代码安装，甚至是软件包安装。RPM 和 DEB 包可用于 gluster，人们可以通过查找来获得它们。也可以克隆存储库并安装 gluster 的源代码。

在本指南中，我将继续进行 gluster 的源代码安装，只是为了展示它所具有的依赖性，同时也有助于了解我们正在处理的内容。

1.  转到[https://github.com/gluster/glusterfs](https://github.com/gluster/glusterfs)。
2.  将存储库克隆到您已设置的虚拟机。
3.  现在，即使我们有源代码，我们也不能运行安装，因为我们肯定会出错。要制作和编译 gluster，需要一些基本的构建工具，如 autogen、auto-conf 等。
4.  正在安装依赖项。人们可以简单地复制下面的命令

正在为 gluster 安装依赖项。

现在，如果有人对运行测试用例或者甚至创建新的测试用例来添加到存储库中感兴趣，那么需要安装某些包，

为测试设置安装依赖项

5.一旦安装完成，就可以继续进行 glusterfs 的源代码构建了。按照以下命令构建 glusterfs

从源头构建 glusterfs

6.一旦 gluster 安装成功，就必须启动 glusterd 守护进程。这个守护进程是 glusterfs 工作的核心。使用命令，

```
$ systemctl daemon-reload
$ systemctl start glusterd
```

还需要一个配置，即打开节点之间以及节点与客户端之间的通信端口。现在，这通常取决于所使用的网络协议，tcp、nfs 还是 samba。因此，我会建议参考相同的文件。

现在，只需要克隆这个 VM，然后开始试验 glusterfs 的特性。如前所述，本文关注的是在安装之前设置 gluster 并解决依赖关系。

如果您面临任何问题，请发表评论…