# Docker:PHP/PDO + MySQL..如何？

> 原文：<https://blog.devgenius.io/docker-php-pdo-mysql-how-to-8c0aee437539?source=collection_archive---------2----------------------->

![](img/1c04cc46557b2d3db082eb5a6c947eb2.png)

照片由[法比奥](https://unsplash.com/@fabioha?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

**上下文**:一个 PHP 服务器和一个 MySQL 数据库。这是一个非常常见的设置。你必须创建一个与数据库交互 PHP 脚本，但是你不能访问服务器，因为由于防火墙安全限制，只有来自本地主机的脚本才能工作。

**问题:**要测试您的脚本，您必须打开一个 FTP 客户端，上传。php 脚本到服务器并测试它。每次 php 文件改变时，你都必须重复这个过程，不考虑在生产中尝试是一个非常糟糕的做法。

> **解决方案:Docker** 可以帮助开发人员在几个步骤中创建一个类似于生产环境的环境。这甚至允许开发人员在本地环境中测试他们代码，而不用担心犯错误！

有现成的容器用于 PHP 和 MySQL，许多教程和在线资源告诉我们如何在有和没有 docker-compose 的情况下将它们放在一起。我发现[这个](https://alysivji.github.io/php-mysql-docker-containers.html)使用 docker-compose 非常有用，而[这个](https://severalnines.com/database-blog/mysql-docker-containers-understanding-basics)没有使用它，但是**我努力尝试使用 PHP+PDO 来简单地打开一个与我的 MySQL 数据库的连接，只阅读这些文章**。我使用 PDO 的原因是 MySQLi 扩展已经被否决了，正如 W3C 所说的。

**环境配置问题(我写这篇文章的原因):**从主机到 MySQL 容器的通信正常，但是从 PHP 容器到 MySQL 容器的通信不正常。

> docker-compose 和适当的变量赋值。php 文件是解决这个问题的关键

这是我的 docker-compose:

我们可以看到 db image 保持原样(mysql:5.7)，但 web image 没有，因为我们必须将 PDO 扩展安装到基本 PHP 映像中。请注意，这两个容器都通过端口 8100(对于 PHP 容器)和 9906(对于 MySQL 数据库)向主机公开:这样，我们可以从主机终端使用类似下面的命令通过 [mysql-cli](https://dev.mysql.com/doc/refman/8.0/en/mysql.html) 连接到它:

其中-P 代表“端口”,必须与 docker-compose 中定义的 hots-exposed 相匹配。-p 代表“密码”，-u 代表“用户”。

在文档下面

最后一行安装所需的扩展。

最后，这是我的 MySQL PHP 连接脚本:

请注意两件重要的事情:

*   $servername 被设置为 docker-compose.yml 中的 *mysql 服务名*，因为 docker-compose 允许在 *docker-compose.yml* 中声明的容器通过服务名相互通信。不用担心 IP 地址
*   $port 设置为网络内端口，其中“网络内”是由“docker-compose up”运行时由 docker-compose 自动创建的端口
*   浏览 http://localhost:8100 ，你会看到消息:“连接成功”

![](img/d07395083f11856012cd785baae91ff3.png)

[韦斯利·埃兰](https://unsplash.com/@wesleyeland?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

# 感谢阅读:)