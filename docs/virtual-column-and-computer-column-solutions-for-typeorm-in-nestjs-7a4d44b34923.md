# Nestjs 中 TypeORM 的虚拟列和计算列解决方案

> 原文：<https://blog.devgenius.io/virtual-column-and-computer-column-solutions-for-typeorm-in-nestjs-7a4d44b34923?source=collection_archive---------0----------------------->

![](img/b543332bdfa692264e51a97603b112bd.png)

如果你完全欣赏前端的 ***计算属性*** 的技术，那么你肯定也想在后端实现它。在大多数情况下，您有足够的信息来计算要显示的项目，所以您不想增加保存这种数据的难度。

例如，您手上已经有了名字和姓氏，您不需要浪费一个字节来保存全名，或者您已经有了关于长度和宽度的数据，您不喜欢将区域数据放在您的数据库中。

我确信*虚拟列*或*计算列*术语应该会出现在您的脑海中。如果我错了请纠正我，这个要求到目前为止还没有正式实现。

因此，让我们来谈谈来自开发人员世界的提示和技巧，我知道有一位开发人员写了一篇关于这个主题的文章，谢谢 Adrian Pietrzak，他激励我们更好地解决这个问题。

有些开发者使用*非可选列*、 *getRaw()方法*、*订阅者方法*和*loadRelationCountAndMap()*等。对于实现，我想在这里介绍两个与 decorator 相关的食谱，因为我是 decorator 的忠实粉丝:)。

# I .装饰方法

我真的很喜欢使用装饰者来保持我的代码整洁，以一种更符合逻辑和更有表现力的方式可读。坦率地说，Java Spring Boot 的注释用法给了我很大的启发。

在 Nestjs 中，您可以在几秒钟内轻松构建自己的装饰器，如果我们在模型中声明一个内置的`**@VirtualColumn()**`装饰器，并且当我们使用`**.addSelect()**`时，结果将被分配给那个键，这将是非常理想的。所以我们来编程吧。

让我们从创建一个装饰器开始:

现在我们可以将它导入到我们的实体中，并将其分配给一个新的字段:

装饰者只为我们添加了元数据，但我们仍然需要编写逻辑来告诉 TypeORM 我们需要为这些元数据做什么，所以现在我们需要以一种体面的方式覆盖核心 TypeORM 函数`**.getOne()**`和`**.getMany()**`。我们想把这个逻辑添加到一个名为 ***的文件中***

您需要在正确的位置实现我们的代码以便编译，只需在***app . module . ts***中导入 ***pollyfill***

```
**import './polyfill';**
```

我扩展了用户服务，添加了一个返回多个用户的额外方法，并添加了`**.addSelect()**`函数:

我创建了一个额外的控制器来运行我的功能:

现在，当我添加`**.addSelect()**`并将结果分配给虚拟列名时，应用程序将执行以下 SQL 操作:

它将返回`**.getOne()**`和`**.getMany()**`函数的映射模型，就像你一直想要的那样。

形式上，这个食谱已经达到了目的，如果你喜欢 QueryBuilder 的话。不幸的是，我对此不太感兴趣，您可能已经注意到了，并准备张嘴大喊:*如果我使用存储库或活动记录，我该怎么办？*或者不使用`**.getOne()**`和`**.getMany()**` 功能如何生存。例如，您正在使用`**.getManyAndCount()**`，那么您必须在 pollyfill.ts 中覆盖更多的函数，如下所示:

有没有一种方法可以更简单，适用于大多数场景？让我们回到订阅者选项，订阅者解决方案是开发人员最常选择的。它使用订阅者`**.AfterLoad()**`将每次给定的结果添加到加载的模型中。但是缺点是显而易见的，您的业务逻辑现在将在您每次尝试加载实体时被执行。

# 二。订户装饰者

让我们从第一个配方中的所有修改回滚，我们只需要修改 user.entity.ts，如下所示:

瞧啊。结束了。我只是在实体中定义了一个具有任意名称的方法(在本例中为`**generateFullname()**`)并用`**.AfterLoad()**`、`**.AfterInsert()**`和`**.AfterUpdate()**`标记它，TypeORM 将在每次使用 QueryBuilder 或 repository/manager find 方法加载实体时调用它。我想这个食谱会让我的生活更轻松。

# 结论

没有什么是完美的，没有什么是不完美的。完美和不完美存在于你的用例中。第一种方法为大量的关联搜索提供了高效率，但是为每个虚拟列编写逻辑并覆盖几个类型方法并不容易。第二种更简单，基本上适合不复杂的用例，但是它会影响你的效率。

你也可以在我的[medium.com](https://medium.com/@joosepwong)上看到这篇文章，在那里我分享了我在软件工程师职业生涯中遇到的问题的解决方案。

如果您还有其他问题，请随时通过 [LinkedIn](https://www.linkedin.com/in/joosepwong/) 联系我。

科图米塞尼！