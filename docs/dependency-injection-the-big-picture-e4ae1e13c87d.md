# 依赖注入，大图

> 原文：<https://blog.devgenius.io/dependency-injection-the-big-picture-e4ae1e13c87d?source=collection_archive---------2----------------------->

![](img/9746e1a3880d80d8f399db5d56f9e505.png)

# **什么是依赖注入？**

关于依赖注入(DI)及其用例有很多定义。依赖注入是软件工程中的另一个难题，在许多 web 框架和应用程序中被广泛用作一种设计模式。

我喜欢将**依赖注入**定义为 ***设计模式*** ，以及实现 ***控制反转*** (IOC)的技术，借此一个对象接收它所依赖的其他对象。

这么多流行语，对吧？让我们得到一个更清晰的画面。😅

首先，将 ***设计模式*** 视为软件开发人员在软件开发过程中面临的一般问题的解决方案。

另一方面，控制反转(IOC)在软件工程中是一个非常宽泛的术语。简单来说，*就是控制组件和类的行为，因此，顾名思义，它是用来在面向对象设计中颠倒不同种类的控件来实现松耦合*。

反转控制有点棘手，你可以按照这篇 [**的文章**](https://martinfowler.com/articles/injection.html#InversionOfControl) 从马丁·福勒那里得到一个更清楚的例子。

现在，让我们回到我前面提到的定义中，它说 ***依赖注入*** 是一种实现**反转控制**的技术。使用依赖注入， ***实现通过构造器、服务查找、设置器等传递到对象*** 中，对象将“依赖”这些实现以正确地运行。

# 依赖注入的类型

依赖注入有三种类型，我们将会看到它是如何使用的。

**构造器注入:**这在依赖注入的实现中被广泛使用。在构造函数注入中，当创建类的实例时，注入器通过类的构造函数提供服务(依赖)。

**属性注入(Setter 注入):**在属性注入中，注入器通过类的一个公共属性来提供依赖。

**方法注入(接口注入):**在方法注入中，通过方法提供依赖关系。这个方法可以是类方法，也可以是接口方法。

## 构造函数注入

如前所述，依赖关系是通过客户端的类构造函数提供的。尽管这里的大部分例子都是用 C#编写的，但它是一种通用语言，并且根据**面向对象(OO)** 原则很容易理解。

让我们用一个真实世界的场景来更好地理解，让我们想象一个学校，基本上，学校是我们去获取知识的地方，通过学习涉及我们想要获取或获得更多理解的“那个”的东西。我们可以通过上课等方式来实现。

创建一个接口 **ISchool。**

***ISchool*** 接口有一个方法定义叫做 ***Learn。*** 创建一个类 ***School*** ，该类在其构造函数中将***is School***接口作为参数。

现在让我们添加两所热门大学(哈佛大学和牛津大学)，这两所大学显然都属于学校类别，并且必须从 ***ISchool*** 接口继承。

有了上面的类，让我们看看依赖注入的实际应用。😋

注意，对于 ***School*** 类的每个实例，我们也可以称之为容器类，我们正在传递我们需要的类的一个新实例，在本例中是*哈佛大学*和*牛津大学*。从而使**和*松耦合。***

> 这里需要注意的重要一点是，**学校类**接受**is School**接口作为其 ***构造函数*** 中 ***依赖关系的参数。***

```
private readonly ISchool _school;        
public School(ISchool school)    
{        
   this._school = school;    
}
```

## 资产注入

如前所述，注入器通过类的公共属性提供依赖关系。让我们看一个很好的例子，来自我们之前的代码样本。

***属性注入*** 可以和 ***构造函数注入一起实现，*** 通过设置默认为 ***构造函数注入*** 。回想一下在 ***School 类*** 中我们声明了一个属性 ***_school*** ，它的类型是 **ISchool 接口。**

```
private readonly ISchool _school;
```

现在，要完全实现 ***属性注入*** 这里，我们需要修改这个属性，我们可以把它改成一个公共方法，而且，它不应该是一个 ***只读的*** 类型。请参见下面的示例。

```
public ISchool _school { get; set; }
```

注意 ***get-set*** 方法。以前， ***_school*** 属性是一个 ***只读*** 类型，它只使用 ***get。***

另一种实现 ***属性注入的方式，*** 这是正常的方式，而在这种情况下，构造函数注入实际上并没有被设置为默认的注入模式。

因此，通过属性注入依赖项将如下所示

您可以看到 **School** 类的属性 **school** 现在可以分配给哈佛大学或牛津大学的不同实例，这正是注入发生的地方。

## 方法注入

依赖关系是通过方法提供的，方法是将依赖关系作为方法参数传递。这个方法可以是类方法，也可以是接口方法。

让我们看一个上面定义的简单例子。同样，使用我们之前的例子，让我们修改代码来进一步展示方法注入是如何发生的。

注意我们正在将 **ISchool** 接口作为参数传递给***attend class()***方法。

***方法注入*** 不同于其他类型的 DI 模式，注入不会发生在*组合根*中，而是在调用时动态进行。

**组合根**是应用程序中一个(最好是)唯一的位置，模块在这里组合在一起。

> 总结一下**依赖注入**的类型，我们可以说，一个学生需要一所学校， ***构造函数注入*** 为学生提供了一所大学的前期，他们无法改变。 ***属性注入*** 让某人不挑大学就成为学生，可以换大学，但大概不会经常换。 ***方法注入*** 让学生每次上课的时候选择自己要去的大学！。

在 C#中，使用现代 web 框架，如[**ASP.NET 核心**](https://docs.microsoft.com/en-us/aspnet/core/?view=aspnetcore-3.1) ，依赖注入是一个内置特性，它的支持不仅限于中间件，还包括框架的其他部分，如控制器、视图、模型等。

关于 ***依赖注入*** 如何在**Asp.Net 核心**中工作的更多细节需要注意的是，这可以通过使用 ***容器(IOC 容器)来实现。***

## 那么什么是 IoC 容器呢？

请记住， **IoC** 的要点是我们不应该需要手动连接我们的依赖，因此依赖注入实现了 **IoC。**

**IoC 容器**创建指定类的对象，并在运行时通过构造函数、属性或方法注入所有依赖对象，并在适当的时候释放它。这样做是为了让我们不必手动创建和管理对象。

所以在像***Asp.Net 核心*** 这样的框架中，我们注册我们称之为 ***的提供者*** 和 ***容器(Ioc 容器)*** 为我们做依赖注入。

# **依赖注入的优势**

依赖注入有很多优点，也有很多用例，但是让我们来看几个。

## **松散耦合架构**

松散耦合意味着对象应该只拥有完成其工作所需的依赖关系——并且依赖关系应该很少。此外，如果可能的话，对象的依赖应该在接口上，而不是在“具体的”对象上。

## 具有不同模拟实现的易测试代码

依赖注入增加了组件的可测试性。当依赖关系可以注入到组件中时，就有可能注入这些依赖关系的模拟实现。模拟对象用于测试，作为真实实现的替代。

## **更可读的代码**

更容易看出一个对象有什么依赖关系，或者你的用例是什么。使代码更具可读性。

# 参考

[*反转控制:马丁福勒*](https://martinfowler.com/articles/injection.html#InversionOfControl) *、* [*迪讲解:教程老师*](https://www.tutorialsteacher.com/ioc/dependency-injection)

## 摘要

这是我能想到的关于依赖注入的一些基本解释，我希望这能有所帮助。我尽可能用简单明了的步骤来解释，但是如果有任何问题，请让我知道。

另外，如果你觉得这有帮助，请留下掌声。😃

感谢 Lionell Park 彻底检查了代码示例。

[*(chibuikekenneth . github . io)*](http://chibuikekenneth.github.io/)， [*(github)*](https://github.com/Chibuikekenneth) ， [*(twitter)*](https://twitter.com/chibuikekenn) *💂*