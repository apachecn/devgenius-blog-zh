# REST 实现模式

> 原文：<https://blog.devgenius.io/rest-implementation-patterns-2d460ea21cda?source=collection_archive---------6----------------------->

![](img/3a547ce7e69999a8433bb6fa97d63316.png)

有很多文章将 REST 描述为一种哲学，或者描述一个特定的库或另一个使用 REST APIs 的库，但是我想花一些时间来谈谈我在使用 ASP.Net 构建 REST 服务时看到和使用过的实现模式。在我们开始之前，让我们至少花一些时间来定义 REST 服务的基本术语。

# 什么是休息来着？

REST 代表“代表性状态转移”。这个短语早在 2000 年就被罗伊·菲尔丁创造出来了，虽然这个名字本身并不能传达太多信息，但这个想法其实很简单。这是一种将数据想象和描述为无状态“资源”的方式，我们使用标准的 HTTP 动词来访问这些数据。每个资源都有自己唯一的地址，并且可以通过这个地址以各种方式进行操作。HTTP 动词描述了我们希望对这些资源采取的操作，服务器使用标准的 HTTP 响应代码来指示这些操作的成功或失败。当然，还有更多的东西，但从高层次上来说，这就是我们所追求的，一种可预测的组织和公开 API 的方式，这样消费者就可以知道在哪里可以根据惯例找到东西。

# 积垢和休息

基本的 CRUD(创建、检索、更新、删除)操作分别很好地映射到基本的 HTTP 动词 POST、GET、PUT 和 Delete。我们使用资源的路由和 HTTP 动词的组合来定义构成 API 支持的操作的端点。与其将有效负载发送到某个任意的端点，如[http://your service/accounts/update person，](http://yourservice/accounts/updateperson,)不如定义一个简单的路由到**资源**，称为“person”，然后在那里实现适当的代码。在这个更新的例子中，我们将为 PUT 或 PATCH 动词实现一个端点，这取决于我们希望调用者如何使用它。让我们看看您可能在 REST API 实现中找到的动词。

**GET —** 在给定的路线上检索资源。REST APIs 通常为每个路由支持两个不同的 GET 端点，一个不接受额外的路由参数并返回资源列表，另一个接受标识符作为路由的一部分并返回关于单个资源的信息。请注意，我在这里特别提到了“路由参数”。我们非常欢迎您在查询字符串的末尾添加参数，以提供搜索标准或控制分页等功能，但是通常每个资源类型只有这两个 GET 路径。例如，调用[http://your service/person](http://yourservice/person)将检索系统中的人员列表，而[http://your service/person/1](http://yourservice/person/1)将检索单个人的详细信息。寻呼参数可以以 http://yourservice/person？start=0 & length=10，过滤信息可能以 [http://yourservice/person/1？includeAddress=true。](http://yourservice/person/1?includeAddress=true.)

**POST —** 从头开始创建新资源。这是一个插入操作，而不是更新操作，所以对[http://your service/person](http://yourservice/person)的 POST 应该会创建一个 person 对象，即使您发送的 person 记录在各方面都与现有记录相同。一般来说，后端系统会忽略您提供的任何 Id 值。

**放置—** 替换已识别的资源。你可以从字面上理解为“把这个放在那里”。可以认为这是一个“插入或更新”(upsert)操作，根据需要创建新的资源或更新现有的资源。预计任何现有数据都将被完全覆盖。

**PATCH —** 对现有资源进行更改，而不必像使用 PUT 那样再次发送整个资源。这可能有点难以实现，需要一些规划。通常，您会希望只发送您想要更新的详细信息。例如，如果我们用一个补丁调用来更新一个人，而这个调用只指定了这个人的惟一 Id 和名字，我们会期望它保留这个人的所有其他属性，比如姓氏。

**DELETE —** 执行您预期的操作，从后端系统中删除已识别的资源。

**不常用动词**

这些不是唯一的 HTTP 动词，RESTful 服务可能希望实现其他动词，如 OPTIONS 和 HEAD，但它们超出了本文的范围。很多时候，你只需要上面基本的四五个动词，就可以完成你需要的一切。

![](img/f1d760e442ace56a7cf6132832b3c8ea.png)

# 路线是任意的

在 ASP.Net 中，路由遵循基于控制器类名称和方法名称的特定约定，但是这些约定可以被实现类或方法上的属性覆盖，这意味着您可以独立于实现路由的代码的组织方式来安排和公开路由。正如大多数开发人员所期望的那样，我可以在 PersonController 中处理 route[http://your service/person](http://yourservice/person)，或者我可以在 UserController 或 AccountController 类中处理它。完全取决于开发商。

这提供了很大的灵活性，并允许您为您的公共 API 提供与底层数据不同的“形状”,但这也可能导致开发人员在调试时产生一些困惑，因为他们会搜索代码以找到有问题的端点在哪里实现。对于大多数项目来说，开发人员倾向于保持路线和它的实现尽可能的相似。如果路由以“person”结尾，那么它们在 PersonController 类上实现它的各种方法。

作为一名开发人员，你需要花很多心思来决定如何安排你的代码，如何安排你的路线，这两个概念有多相似，以及哪一个驱动另一个。当您添加一个新的端点时，如何决定它应该放在哪里？没有单一的答案。就像发展世界中的其他事情一样，这要视情况而定。让我们来看看解决这个问题的两种不同方法。

# 按主题组织

我见过的最常见的模式是按主题将 API 端点分组在一起，比如将所有与人员相关的操作放在一个 PersonController 中。然后使用描述性的方法名来提高可发现性并避免冲突。例如，获取某人最近订单的端点可能是这样实现的。

```
```csharp
[ApiController]
[Route("person")]
public class PersonController : ControllerBase
{
    [HttpGet("{id}/orders/recent")]
    public ActionResult<List<Order>> GetRecentOrders(int id)
    {
        var results = People.FirstOrDefault(x => x.Id == id)
            .Orders
            .OrderByDescending(x => x.OrderDate)
            .Take(10);

        return results;
    }
}
```
```

正如您所看到的，Route 属性已经为这个端点定义了公共路由(…/person/1/orders/recent)，而方法名(GetRecentOrders)对开发人员更友好。一个外部消费者会向[http://your service/person/1/orders/recent，](http://yourservice/person/1/orders/recent,)发出一个 GET 请求，这个方法会处理这个调用。请注意，该方法可以简单地称为“RecentOrders”或“Recent”，甚至可以简单地称为“Get”，因为到目前为止，该控制器上没有其他方法。这个方法的名字**没有**来匹配它的路径。

这一开始非常简单容易，但是遵循这个约定意味着所有与人相关的东西最终都在这个控制器类中实现。对于您的 API 的高流量区域，这可能会导致一些非常大的控制器类有几十个方法，使其难以导航，并导致合并冲突，因为多个团队成员经常发现他们自己在同一时间处理同一个文件。

您也可以提出一个论点，上面例子中的“资源”实际上是订单，而人仅仅是一个查询参数。这就是 API 设计变得有创造性的地方。您需要决定如何以对您的 API 消费者最有意义的方式组织事物。“/order/recent/{personId}”是否更有意义？它或多或少能被发现吗？也许团队决定外部路径是好的，但是该方法确实属于 OrderController 类，因为它与订单的关系比与人的关系更大，但是他们不想破坏现有的 API 消费者。要进行这种更改，我们只需移动 GetRecentOrders 方法，修改 Route 属性，开发团队以外的任何人都不会知道有任何更改。

如果团队决定路线本身需要改变，那么现有的 API 用户会发生什么呢？如果改变路线，不就断了现有用户吗？幸运的是，没有。一个端点可以有多个路由，所以我们可以保留旧路由，同时建立一个新路由，然后温和地鼓励人们在可能的时候转移到新路由。最终，当没有人使用旧路线时，我们可以删除它。

这种灵活性既是优点也是缺点。外部 API 独立于其实现而变化的能力使我们可以在不破坏现有用户的情况下按照我们想要的方式重新排列代码，但这也意味着开发人员可能需要搜索更长的时间才能找到他们想要的东西，因为它几乎可能在任何地方。即使我们很努力，在这个标准范围内仍然有很大的变化空间。

![](img/7b48901f6f2722bbb43c4d32ba0c6294.png)

# 按路线组织

您也可以选择严格按照资源将方法映射到控制器上，这由它们的路由决定，并直接根据它们处理的 HTTP 谓词命名。按照惯例，这是 ASP.Net 真正想要你做的事情。如果您足够严格地遵循约定，您几乎可以完全取消路由属性。在开箱即用中，PersonController 类上的一个名为“GET”或“GetAsync”的方法将被自动连接起来，以处理对“/person”路由的 Get 请求，这是按路由组织的关键。在这里，您可以看到两个控制器，每个控制器都有一个名为“Get”的方法。

```
```csharp
[ApiController]
[Route("person")]
public class PersonController : ControllerBase
{
    [HttpGet("{id}")]
    public ActionResult<Person> Get(int id)
    {
        return People.FirstOrDefault(x => x.Id == id);
    }
}

[ApiController]
[Route("order")]
public class OrderController : ControllerBase
{
    [HttpGet("{id}")]
    public ActionResult<Order> Get(int id)
    {
        return Orders.FirstOrDefault(x => x.Id == id);
    }
}
```
```

在任何给定的类中，只能有一个带有给定签名的方法。试图添加具有相同名称和参数的第二个方法将导致编译时错误。代码根本无法构建。您也可以只有一个方法来处理给定的路由和动词组合，否则您会得到一个运行时错误。这两个概念非常一致。由此产生的约定迫使您用大量更小的控制器替换少量非常大的控制器，每个控制器只包含几个方法，每个方法对应于该路由支持的一个 HTTP 动词。

这种方法使得实现任何给定路由的核心的位置是可预测的。开发人员将知道在哪里可以找到任何给定路由/动词组合的实现。像这样将代码分散到更多的文件中有一个有益的副作用，那就是减少与其他团队成员的合并冲突，减少摩擦，提高团队的整体生产力。让我们看一个例子。

如果我们有一个路由，比如 http://your service/person/1/order，，我们可以在一个名为“PersonOrderController”的控制器上实现一个名为“Get”(或“GetAsync”)的方法。

```
```csharp
[ApiController]
public class PersonOrderController : ControllerBase
{
    [HttpGet("person/{personId}/order")]
    public ActionResult<List<Order>> Get(int personId)
    {
        return People.FirstOrDefault(x => x.Id == id).Orders.ToList();
    }
}
```
```

要想出这个名字，我们只需连接路由中所有非参数的单词。在这个例子中，应该是“person”和“order ”,因为“1”是一个参数，表示我们应该检索哪个人的订单。最后，我们在末尾加上“控制器”来跟随 ASP。Net 自己的控制器命名约定，我们都准备好了。

什么是路线的一部分和什么是参数之间的区别有时很明显。其他时候，更多的是判断。假设我们想要实现两个新的端点:http://your service/person/1/order/recent 和 http://your service/person/1/order/open。首先，我们需要确定哪些单词标识了资源类型，哪些仅仅是参数。很明显,“1”代表我们想要检索其订单的人的 Id 号，但是“最近”和“未完成”呢？最近的订单是否被视为与未结订单完全不同的资源类型？如果是这样的话，那么您可以提出一个强有力的论点，将它们作为路由的一部分，从而产生 PersonOrderRecentController 和 PersonOrderOpenController 类，每个类都有一个 Get 方法。

```
```csharp
[ApiController]
public class PersonOrderRecentController : ControllerBase
{
    [HttpGet("person/{personId}/order/recent")]
    public ActionResult<List<Order>> Get(int personId)
    {
        return People.FirstOrDefault(x => x.Id == id).Orders
            .OrderByDescending(x => x.OrderDate)
            .Take(10)
            .ToList();
    }
}

[ApiController]
public class PersonOrderOpenController : ControllerBase
{
    [HttpGet("person/{personId}/order/open")]
    public ActionResult<List<Order>> Get(int personId)
    {
        return People.FirstOrDefault(x => x.Id == id).Orders
            .Where(x => x.Status == "open")
            .ToList();
    }
}
```
```

这是一个好的设计吗？直观吗？开发者会在他们期望的地方找到东西吗？在这种情况下，答案是“大概不会”。这些名字很笨拙，感觉有些“不对劲”。当有疑问时，问自己以下问题。这些端点接受并返回不同的类型吗？这些控制器中的任何一个会有自己的其他方法吗？如果是这样，那么它们有资格作为独特的新路线/资源。然而在这个例子中，两个问题的答案都是否定的。这两种方法都不接受该端点特有的任何类型的参数，并且很可能返回相同类型的数据，可能是订单汇总类。此外，您永远不会向这些新路由中的任何一个发布、放置、修补或删除任何内容。给定这些答案，似乎“最近”和“开放”没有定义新的资源。它们只是同一个 GET 端点的参数([http://your service/person/{ personId }/order/{ category }](http://yourservice/person/%7bpersonId%7d/order/%7bcategory%7d))。

```
```csharp
[HttpGet("person/{personId}/order/{category}")]
public ActionResult<List<Order>> Get(int personId, string category)
{
    switch (category)
    {
        case "open":
            return People.FirstOrDefault(x => x.Id == personId).Orders
                .Where(x => x.Status == "open")
                .ToList();
        case "recent":
            return People.FirstOrDefault(x => x.Id == personId).Orders
                .OrderByDescending(x => x.OrderDate)
                .Take(10)
                .ToList();
        default:
            return null;
    }
}
```
```

# 结论

如果您想将您的服务称为 RESTful，那么 HTTP 动词必须是您的路由实现的一个组成部分。仅仅说您有 REST 服务是不够的，因为您通过 HTTP 公开了功能。您需要使用相同路由和不同动词的组合来表示对相同数据的不同操作。如果您有以“GetOrders”或“UpdateOrder”结尾的路径，那么您的服务可能是 REST 式的，但它们不是真正 RESTful 的。您可以手动指定您的路线，公开一个 RESTful API，并且在您的控制器中仍然有一个杂乱无章的混乱。根据它们处理的路径组织控制器和方法解决了许多开发问题，我不知道为什么你会用其他方式组织你的代码。这是一个惯例，鼓励你保持代码有组织，保持你的类小。当你试图做其他事情时，它会推你一把，帮助你发现更好的解决方案，而这些就是最好的约定。

## -梅尔·格拉布，AWH 软件开发团队负责人