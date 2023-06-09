# 使用序列作为 ORM

> 原文：<https://blog.devgenius.io/using-sequelize-as-orm-a70455153028?source=collection_archive---------33----------------------->

![](img/2e86ee4fd81bd84b74fb1e579832b3fa.png)

[活动发起人](https://unsplash.com/@campaign_creators?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

*免责声明:这是我自己的经验，所以这是一篇主观的文章，人们可能不同意或有更客观的观点。*

Sequelize 是我从使用 Node.JS 迁移到代码以来使用的最有用的包之一，我以前使用过 Java，并使用 MyBatis 作为工具来帮助我查询复杂的搜索。然后我切换到 Node。我辞去第一份工作，加入第二家公司的那一天。我必须选择一个 ORM 来查询数据库，因为我不想使用编写自己的查询的冗长方式，用我想要插入的变量替换所有变量。因为我选择 Express 作为我的 Rest API 框架，所以我选择使用 Sequelize 作为 ORM。

这是我第一次使用 ORM，所以我真的不知道它的结构以及如何正确使用它。然后我谷歌了一下(当然)使用 Sequelize 的最佳方式，并发现了一个巧妙之处。这就是 Sequelize 的巧妙之处

## 1.Sequelize 有一个 CLI

Sequelize 有一个 CLI(命令行界面),在那里我不需要手动创建文件夹，比如模型、种子、迁移和配置。它是一个独立的 npm 包，带有核心的 Sequelize 包，所以直到我阅读了他们文档的底部，我才真正注意到它。你要做的就是

```
$ npm install sequelize --save
$ npm install sequelize-cli -g --save
$ sequelize init
```

Sequelize 然后创建模型、迁移、种子和配置文件夹。默认情况下，它将创建在项目的根目录下。如果我想设置文件夹的位置，我只需要在项目的根目录下创建一个. sequelizerc 文件。我们还可以生成并运行数据库的播种和迁移。在我看来很方便。

## 2.Sequelize 仅适用于 ORM

与 Waterline (Sails JS)或 Loopback 等一些 ORM 不同，Sequelize 只有一个主要用途，那就是帮助进行数据库查询和管理。我以前使用过 Sails JS Waterline，它只非常好地支持基本查询(从版本 1 开始),但很难用于我可以在 Sequelize 中进行的更复杂的查询，可能是因为它更关注整个框架。我还没有尝试过其他的 ORM，但是对我个人来说，如果你不真的使用任何包含自己的 ORM 的框架，比如 express，Sequelize 是一个很好的 ORM。它支持大多数主流 SQL 数据库(Mysql、Postgresql、SQLite)。

## 3.非常灵活，但简单

我还喜欢 Sequelize 的一点是，它可以执行更复杂的查询，而无需我为它创建原始查询。尽管有些复杂查询并不那么直接，但许多查询都很简单，比如 upsert、find 和 count、基于连接表的排序等等。数据库配置也很简单，我可以根据运行它的环境来创建数据库。

## 4.一个大社区

Sequelize 有一个很大的社区，当我需要做一些事情，但似乎找不到正确的方法时，它给了我很大的帮助。近两年来，它一直是我的救星，我问谷歌的任何奇怪问题似乎都可以在 Stackoverflow 或他们的 github 回购问题中找到答案。我必须说这是一个成熟的 ORM(到目前为止是稳定的版本 5 ),并且有很好的文档记录可以开始使用。

![](img/f2241d740113e39094bc97920f470566.png)

蒂姆·马歇尔在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

# 结论

Sequelize 对我个人来说是一个非常简单的 ORM，使用它对我来说是一种乐趣，尽管它也有缺陷。这是一个成熟的 ORM，有一个很大的社区。这真的是一个很好的 ORM，对于任何选择在你的 Node JS 项目中使用什么 ORM 的人来说，我建议你考虑使用 Sequelize 作为一个 ORM。谢谢:)

干杯！

![](img/1a99e621fa7d1c131970b9d20ac6e601.png)

照片由 [Zan](https://unsplash.com/@zanilic?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)