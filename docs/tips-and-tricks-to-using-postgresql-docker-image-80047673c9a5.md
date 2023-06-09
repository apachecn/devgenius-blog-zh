# 使用 PostgreSQL Docker 映像的提示和技巧

> 原文：<https://blog.devgenius.io/tips-and-tricks-to-using-postgresql-docker-image-80047673c9a5?source=collection_archive---------4----------------------->

## 第二部分:用 Flyway 编写 Docker

![](img/2ec8ca79725d363d07f3ff78b1763a48.png)

本文是系列文章的第二部分

*   在这里找到第一部分:[使用初始化脚本](/tips-and-tricks-to-using-postgresql-docker-image-1c799e4ee3b8)

本文分享了一些使用 [Docker Compose](https://docs.docker.com/compose/) 和 [Flyway](https://flywaydb.org/documentation/) 设置您的 [PostgreSQL](https://www.postgresql.org/) 数据库的技巧和代码示例。

## 何时使用 Docker 撰写

当您希望在一个应用程序后面运行多个 Docker 容器时，Docker Compose 非常有用。例如，在一个容器上运行的 Node.js API 与另一个容器上的 PostgreSQL 数据库进行通信。Docker Compose 简化了多容器应用程序的设置。它还使您能够用一个命令运行整个应用程序。

## 何时使用 Flyway

Flyway 有助于管理不断发展的数据库。本质上，这是一种记录数据库变化的方法。这包括像新表、新列和删除的表(仅举几个例子)这样的更改。版本历史使您能够

*   从头开始重新创建数据库
*   对数据库状态有清晰的历史记录
*   增强对数据库版本间迁移的控制

考虑将数据库迁移工具用于生产应用程序是一个好主意。

## 设置 Docker 合成文件

docker 合成文件是配置应用程序 Docker 映像的地方。

下面是一个运行 PostgreSQL 和 Flyway 容器的 Docker 合成文件示例。默认情况下，合成文件应该位于`./docker-compose.yml`

下面是我的一个应用程序中的 docker-compose.yml 文件示例。

docker-compose.yml 配置文件示例

让我们一行一行地分解这个文件来理解每一部分。

## 顶级属性

**版本**(可选)—该值仅供参考，从 [1.27.0](https://github.com/docker/compose/releases/tag/1.27.0) 版本开始不再需要。它指示预期的 docker-compose 版本。

**服务**(必需)—此属性包含此应用程序的每个容器的配置。每个服务代表一个组件，可以独立于其他组件进行扩展或替换。

**卷**(可选)—用于保存 Docker 容器生成的数据。顶级密钥可以为空，在这种情况下，它使用默认配置。

## 服务属性

上面的 docker-compose.yml 文件配置了两个服务，Postgres 和 Flyway。下面我们来深究一下这两种配置。

以下是 Postgres 服务的摘录，这样你可以避免过多的滚动。

Postgis 摘录自完整的 docker-compose.yml

**image —** 指示使用哪个 Docker 图像作为该服务的基础。Docker Hub 图像库拥有成千上万张图像。值(`postgres`)针对[官方 Postgres 镜像](https://hub.docker.com/_/postgres)。

**容器名称—** 可用于指定自定义容器名称。如果您不提供名称，Docker 将生成一个随机名称(以 UUID 的形式)。把这个想象成一个变量名；这只是在提到容器时添加含义的一种方式。

**环境—** 添加环境变量的地方。某些图像，如官方 Postgres 图像，将在指定的环境变量中寻找值。例如，参见处的[部分的“环境变量”。](https://hub.docker.com/_/postgres)

**端口—** 公开容器内部端口，供外部客户端连接。公开的端口不需要与实际的容器端口相匹配。上面的 docker-compose.yml 文件使用了格式，`HOST:CONTAINER`。

**卷** —用于装载主机或命名卷上的路径。请记住，卷是用来保存数据的。在上面的 docker-compose.yml 文件中，一个初始化脚本被挂载到容器中，供 Postgres 映像使用。关于初始化脚本的更多信息，请参见本系列的第一部分。

线`pg_data:var/lib/postgresql`是一个命名卷(`pg_data`)，安装在`var/lib/postgresql`的集装箱上。

**重启** —设置容器的[重启策略](https://docs.docker.com/config/containers/start-containers-automatically/#use-a-restart-policy)。如果未指定，默认情况下永远不重新启动。指定`always`意味着容器将在停止时重新启动。

以下是 Flyway 服务的摘录

Flyway 摘录自完整 docker-compose.yml

**命令** —这个特殊的命令值需要一些额外的解释。当您运行 Docker 容器时，它通过连接`entrypoint`和`command`来构建一个命令行。飞行路线基础图像定义了一个`entrypoint`。见[此处](https://github.com/flyway/flyway-docker/blob/master/alpine/Dockerfile#L22)。因此，docker-compose.yml 文件只需要为 Flyway `entrypoint`命令提供参数。

**链接**(遗留特性)——表示到另一个服务中的容器的链接。链接还表达了服务之间的依赖关系，它告诉 Docker 应该先启动哪些服务。关于构建新容器时的建议方式，请参见 Compose 中的[联网。](https://docs.docker.com/compose/networking/)

**使用 Flyway 的版本化迁移**

Flyway 最常见的用途是“版本化迁移”。“迁移”是 Flyway 对数据库的任何更改使用的名称。迁移可以包括对表(创建、修改、删除)、索引、键和数据类型的更改。

Flyway 希望这些文件遵循特定的命名约定。此处详细定义了命名约定[。例如，我的一个项目的迁移文件被命名为:](https://flywaydb.org/documentation/concepts/migrations.html#naming)

*   V1 _ _ initial _ setup _ create _ event . SQL
*   V2 _ _ 添加日期 _ 创建日期 _ unix _ 至 _ 面包屑. sql
*   V3 _ _ 添加时间戳至面包屑 ds.sql

根据上面的卷定义，迁移文件应该存储在主机上的`./migration/sql`下。注意在`volumes`下，该路径安装在容器上:

Flyway 将自动运行尚未应用到数据库的任何迁移。因此，要更改数据库，请将 SQL 命令添加到主机上的新迁移文件中。

例如，文件 V1 _ _ initial _ setup _ create _ events . SQL 包含:

要获得更完整的使用 Flyway 和 PostgreSQL 与 Docker Compose 的示例，请查看我的后端应用程序， [Breadcrumbs](https://github.com/tonyOreglia/breadcrumbs) (这里用 UI [演示了它](https://tonycodes.com/breadcrumbs))。它包括 Flyway 版本化迁移、初始化脚本、docker-compose 和 docker 文件。Flyway 版本化迁移文件可以在[这里](https://github.com/tonyOreglia/breadcrumbs/tree/master/migration/sql)找到。

希望这篇参考有帮助。如果你有任何问题，请留言，我会很乐意回答。

# 资源

*   卷键上的合成规范:[https://github . com/compose-spec/compose-spec/blob/master/spec . MD # volumes-top-level-element](https://github.com/compose-spec/compose-spec/blob/master/spec.md#volumes-top-level-element)
*   使用卷的 Docker 文档:【https://docs.docker.com/storage/volumes/ 
*   码头枢纽:【https://hub.docker.com/ 
*   docker-compose.yml 文件参考:[https://docs . docker . com/compose/compose-file/compose-file-v3/](https://docs.docker.com/compose/compose-file/compose-file-v3/)
*   Flyway 版本化迁移:[https://flyway db . org/documentation/concepts/Migrations . html #版本化迁移](https://flywaydb.org/documentation/concepts/migrations.html#versioned-migrations)