# 六边形架构的 Flask 博客教程(第 1 部分)

> 原文：<https://blog.devgenius.io/flask-blog-tutorial-with-hexagonal-architecture-part-1-6446e7e9aaaa?source=collection_archive---------4----------------------->

![](img/5688fb3df07e18fc85641b31358a5003.png)

图片来自:
[http://thinkmicroservices . com/blog/2019/hexagon-architecture . html](http://thinkmicroservices.com/blog/2019/hexagonal-architecture.html)

[该项目的 GitHub 回购](https://github.com/ShahriyarR/hexagonal-flask-blog-tutorial)

>[本系列第二部](https://rzayev-sehriyar.medium.com/flask-blog-tutorial-with-hexagonal-architecture-part-2-8930ca009c27)

>[本系列第三部](https://rzayev-sehriyar.medium.com/flask-blog-tutorial-with-hexagonal-architecture-part-3-9a265f0c4b95)

想法是借助依赖注入重写官方 [Flask 博客教程](https://flask.palletsprojects.com/en/2.2.x/tutorial/)，遵循六边形架构。

你可以从这里区分并查看原始代码库: [Flask 博客教程代码库](https://github.com/pallets/flask/tree/main/examples/tutorial/flaskr)

所有的静态数据和模板都是从最初的博客文章中抓取的。

这个项目应该给出一个我们如何使用 Python、Flask 和 DI 实现端口和适配器(六角形)架构的想法。

最终的项目结构如下所示:

# 关于六角形建筑

可以看原作者的:

[模式:端口和适配器](https://alistair.cockburn.us/hexagonal-architecture/)

# 关于项目相关性

该项目有两个主要依赖项:

[依赖注入器](https://github.com/ets-labs/python-dependency-injector)

[烧瓶](https://github.com/pallets/flask)

# 入门指南

现在，让我们深入了解我们所拥有的，以及如何将这个原始的 flask 博客教程代码转换成一个干净的、可维护的六边形架构。

从概念上讲，我们需要通过将领域模型置于应用程序的核心来将领域模型与外部世界分离开来。这意味着我们需要首先考虑我们的领域模型。同样不是关于数据库，不是关于 flask，也不是关于 docker 等等，想想你的应用程序的核心是什么。

最好是提出问题:

*   问:这到底是什么应用程序？—至于官方的 Flask 教程，这是一个博客应用程序，它需要两件事情来工作:用户登录和博客被写。
*   问:这个用户到底是谁？是什么让“某样东西”成为用户？——具有唯一 ID、用户名和密码的“某物”可以被视为我们的用户。
*   问:那么什么是博客文章呢？—博客文章将有作者 id、标题、正文，可能还有创建时间。带有该信息的“某些东西”将被视为博客帖子。

酷，我们已经定义了我们的模型，是时候实现它们了。

> 请记住，领域模型不是数据库模型，我们甚至不考虑数据库。数据库是一个细节。

# 实现领域模型

我们的领域模型将停留在:`/src/domain/model`路径。所以请创建这些文件夹。

然后创建`user.py`和`post.py`，分别代表用户和帖子。

请注意创建用户模型并将其返回的工厂方法。理想情况下，在这个工厂方法中应该有一个很好的验证步骤，但是我们已经省略了它，因为原始的 Flask 教程也默默地遮蔽了它:)

我们的帖子模型:

很简单，也很整洁。

# 关于端口的推理。

由于我们将遵循端口和适配器架构，我们需要首先考虑端口，因为这是 REST API 将要实现和使用的地方。

我将端口代码放在域端口文件夹`/src/domain/ports`中。

> *端口是由适配器实现的接口，你马上就会看到。*

问题:

*   问:我们如何持久化我们的用户和发布数据？—好的，我们可以有一个简单的存储库模式，它是一个接受数据库连接的接口或抽象类。

在端口内创建`repository.py`文件，并放入以下代码:

基本上，我们的 Repo 将执行 SQL 语句，然后调用 DB commit。我们在这里没有使用任何形式的 ORM，因为最初的 Flask 博客教程也只使用原始 SQL 和 SQLite。

问:外界(CLI，REST，任何东西)将如何注册和登录用户？—我们可以拥有有史以来最简单的命令或服务模式，姑且称之为`user_service.py`:

现在，请注意，`UserService`接受`RepositoryInterface`作为参数，作为依赖项。

使用`user_repo`它将保存实际的用户数据。

另外，请注意用户模型是如何在 create 方法中使用 user_factory 创建的，只有在此之后，用户数据才会被构造并插入到数据库中。

这就是我们如何颠倒存储机制的依赖性，我们的用户模型不依赖于数据库生存，但是数据库动作需要我们的用户做它的工作。

*   管理岗位怎么样？给你，`post_service.py`:

PostService 再次接受抽象存储库来保存 post 数据。但是我们这里有更有趣的东西。

让我来解释一下`CreatePostInputDto`、`UpdatePostInputDto`、`DeletePostInputDto`背后的想法。

同样的问题:

*   我们需要什么样的信息来创建一个 Post 域模型—基本上，post_factory()需要 author_id、body 和 title，创建时间会自动实例化。`CreatePostInputDto`(数据传输对象)只是封装并验证这些信息，post_factory 使用其数据创建 post，然后将其插入数据库。
*   我们需要什么样的信息来更新数据库中保存的帖子？— `UpdatePostInputDto`封装并再次验证帖子 id、标题和正文
*   从数据库中删除保存的帖子需要什么样的信息？—我们可以通过 id 找到帖子，然后删除它。`DeletePostInputDto`简单地为我们封装了 id。

但是，为什么我们需要这些 dto 呢？如果您从外部接受一些东西作为输入，如果您返回一些东西作为输出，那么限制、验证并赋予接受和返回的数据一些形状总是更好的。可以把它想象成 web 框架中的请求/响应模型。您接受一些数据作为请求对象的一部分，然后构造一些响应模型并将其返回给用户。

我将把这些 dto 放在`/src/domain/ports/__init__.py`中:

第一部分总结:

*   我们实现了简单的领域模型，没有任何领域事件或其他花哨的东西。
*   我们已经实现了六边形架构的所有端口。

> *我们也没有测试，因为最初的 Flask 博客教程残忍地将测试踢出了:D*