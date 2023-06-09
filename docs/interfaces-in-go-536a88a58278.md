# Go 界面

> 原文：<https://blog.devgenius.io/interfaces-in-go-536a88a58278?source=collection_archive---------6----------------------->

Go 中的接口类型有点像*定义*。它定义并描述了*和其他类型*必须拥有的确切方法。

有时候你并不关心值的具体类型。你不关心它是什么。你只需要知道它将能够做某些事情。你可以在上面调用某些方法。你不在乎你有钢笔还是铅笔，你只需要一个有绘制方法的东西。你不在乎你是有车还是有船，你只需要有转向方法的东西。

接口允许你指定行为。它们是关于做，而不是存在。接口还允许您抽象代码，使其更具可重用性、可扩展性和可测试性。

与其他编程语言中的接口不同，Go 中的接口是隐式满足的。Go 并没有提供实现接口的关键字，所以如果你已经使用过其他编程语言的接口，但还不熟悉 Go，这种想法可能会令人困惑。

作为函数的一个例子可能如下:

```
**func** PerformAtVenue(m Musician) {
    m.Perform()
}
```

PerformAtVenue 函数将音乐家作为参数，并对音乐家调用 Perform 方法。音乐家类型是一个具体的类型。

```
**type** Musician **struct** {
    Name **string**
}**func** (m Musician) Perform() {
    fmt.Println(m.Name, "is singing")
}
```

当我们将一个音乐家传递给 PerformAtVenue 函数时，我们的代码进行编译，并得到预期的输出。

```
**func** main() {
    m := Musician{Name: "Kurt"}
    PerformAtVenue(m)
}
```

因为 PerformAtVenue 函数将一个具体类型的音乐家作为参数，所以我们被限制在谁可以在场地上表演。例如，如果我们试图将一个诗人传递给 PerformAtVenue 函数，我们将在下面的代码中得到一个编译错误。

```
**type** Poet **struct** {
    Name **string**
}**func** (p Poet) Perform() {
    fmt.Println(p.Name, "is reading poetry")
}**func** main() {
    m := Musician{Name: "Kurt"}
    PerformAtVenue(m) p := Poet{Name: "Janis"}
    PerformAtVenue(p)
}
// cannot use p (variable of type Poet) as type Musician in
// argument to PerformAtVenue
```

接口允许您通过指定 PerformAtVenue 函数所需的一组公共方法来解决这个问题。我们引入了一个执行者接口。此接口指定需要 Perform 方法来实现 Performer 接口。

```
**type** Performer **interface** {
    Perform()
}
```

音乐家和诗人都有演奏方法。因此，我们可以在这两种类型上实现 Performer 接口。通过更新 performat enue 函数以将表演者作为参数，我们现在能够将音乐家或诗人传递给 performat enue 函数。

```
**func** PerformAtVenue(p Performer) {
    p.Perform()
}
```

通过使用接口，而不是具体的类型，我们能够抽象代码，使其更加灵活和可扩展。

![](img/a6f8e4b386b195633eb7fb5e35f23b4f.png)

在下面的例子中，声明了 Writer 接口，我们有两个结构体，它们的方法分别带有一个值接收器和一个指针接收器，都工作得很好，只是要小心，当一个变量被声明为值类型，然后指向 address 时，表达式&m 取地址 m，其中&是一个取地址值的运算符，这是一个错误。

**{空口界面}**

空接口是没有方法集和行为的接口。空接口不指定任何方法。如果你用零个方法声明一个接口，那么系统中的每个类型都被认为实现了它。

```
// generic empty interface:
**interface**{} 
// aliased to "any" in Go v1.18// a named empty interface:
**type** foo **interface**{}
```

例如，一个 **int** 没有方法，正因为如此，一个 int 匹配一个没有方法的接口。

关于您在开始 Go 开发时可能会遇到的异常错误。

但是我们会更进一步:如果我们尝试创建一个*Man 类型的空变量，并将其转换为接口，会怎么样？

我们来了解一下为什么会出现这种情况。Go 中的接口包含两个字段，关于具体类型的**标签**和**数据**，其中有一个到数据本身的链接。而现在，根据 Go 的规则，只有这两个字段都没有定义，接口才能等于 nil。
让我们看看当我们将 man 变量转换成一个接口时会得到什么:

```
// https://golang.org/src/runtime/runtime2.go **type** iface **struct** {     
  tab  *itab     
  data unsafe.Pointer 
}
```

因此，我们有一个填充了 tab 字段的接口，检查是否与 nil 相等将总是返回 false。即使变量在与 nil 比较时最初返回 true。

我们的 gopher 文档中描述了这种行为吗？—不是。不完全是。这在语言规范中没有描述，但是在语言 FAQ 中有:[https://golang.org/doc/faq#nil_error](https://golang.org/doc/faq#nil_error)。在这里，考虑了与接口的这种行为相关的一个常见错误:当我们从一个函数返回对自定义错误的对象的引用时。如果函数中没有出现错误，则该引用可能为零。并且，当我们的自定义错误对象被转换为错误接口时，这个新转换的对象将不再等于 nil，并且 all if err！= nil {}检查将不再正常工作。
我将给出一个比常见问题解答更详细的例子:

[](https://www.alexedwards.net/blog/interfaces-explained) [## 戈朗接口解释道——亚历克斯·爱德华兹

### 在过去的几个月里，我一直在进行一项调查，询问人们在学习围棋时发现什么困难…

www.alexedwards.net](https://www.alexedwards.net/blog/interfaces-explained)  [## Go 界面

### 三本新书，Go 优化 101，Go 细节与技巧 101 和 Go 泛型 101 现在出版了。这是最…

go101.org](https://go101.org/article/interface.html)