# 从 Ruby 转换到 JavaScript

> 原文：<https://blog.devgenius.io/making-the-switch-from-ruby-to-javascript-cc5f0d94b792?source=collection_archive---------6----------------------->

![](img/300490a634352585787bcd2cb7ef1660.png)

约书亚·富勒在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

作为一名初学程序员，在我的编码之旅中，我并没有太多偏好从哪种语言开始。诚然，在选择我想参加哪个训练营以及每个训练营教授哪种语言之前，我已经做了大量的研究，但我要说的是，我对他们中的任何一个都没有感情上的联系。我希望能够解决 web 开发问题，这就是我所知道的全部。

Flatiron 的前两个 mod 集中在 Ruby 和 Rails 上，这是一个简单的、结构化的、面向对象的程序，现在我非常想念它，因为我已经在 JavaScript 的道路上走了几个星期了。我认为我对 Ruby 的热爱，以及我在学习 Ruby 时在大脑中形成的联系，可能阻碍了我最初接受 JavaScript 的能力，所以我想在这两者之间进行描述，从世俗到概念，以启发那些一直在为之奋斗的人。

让我们把编程语言想象成人。如果说 Ruby 是一个五岁的小女孩，试图让程序员喜欢她，享受和她在一起的时光，那么 JavaScript 就是一个急躁的少年。Ruby 理解简单性，理解对象的本质，并简单地将所有东西放入这些盒子中。JavaScript，或者他所谓的 JS，很前卫，他喜欢用他的方式做事，不管是在语法上还是其他方面。他足够聪明，能够异步地做事情，以最大化他的生产力，并处理更抽象的概念。

# **语言目的**

显然，Ruby 和 JavaScript 在 web 开发领域有着完全不同的目的。到目前为止，在我们的训练营中，Ruby 已经被用来制作 API 和更基本的服务器端应用。另一方面，JavaScript 与 HTML 和 CSS 交互来构建交互式网页。

这两种语言背后的核心理念有着根本的不同，这使得一种语言比另一种语言更容易完成某些任务。Ruby 的创造者专注于编程给人的感觉，这反过来强调生产力和简单性，而不是无限的可能性。JavaScript 从一开始就是为了让网页活起来而创建的，这意味着它允许程序员用更少的结构和更多的语法来做一百万件事情。

Ruby 的流程是由 MVC 范式定义的:模型、视图和控制器来控制应用程序的不同方面。模型存储信息，视图显示信息，控制器在两者之间工作以控制信息。另一方面，JavaScript 是一种事件驱动的语言，这意味着与 API/数据库和 DOM 的交互不是在各个部分之间描述的，而是并存于事件侦听器、函数和其他代码中。

JS 要求我们的代码在一个文档中更有条理。对我有效的方法是从所有变量声明开始，然后是函数声明，然后是事件侦听器。这样，我们在调试时可以更容易地找到信息。

# **在**周围传递信息

在 Rails 应用程序中编写代码时，我们使用控制器中的实例变量来访问来自模型的信息，以发送我们希望在. html.erb 文件中显示的信息。当然，我们不能在控制器方法之间访问实例变量，但是我们利用了*会话*和*参数*的帮助来存储和查找信息。

当用 JavaScript 写代码时，我们不这样做；这意味着访问一个变量并改变它比我们想要的要困难得多。一直在使用的解决方法是将信息存储在 DOM 元素的 dataset 属性中。虽然不像在 Ruby 中那样容易访问，但我想冒险猜测一下，我们会找到一种方法使它在我们的课程中变得更容易。

# **隐式与显式返回**

Ruby 函数有一个隐式的 return，这意味着不需要使用 return 关键字从函数中检索信息；自动返回最后执行的行。JavaScript 函数要求为每个定义的函数或方法显式返回。

这又回到了 Ruby 和 JS 对待对象的方式；在 Ruby 中，几乎所有东西都是对象，而 JS 是一种面向对象的语言，它基本上是在现有的原型基础上扩展的。所以在 Ruby 中发生的事情是，一切都是在一个类/模型范围内定义的，通常很少使用全局变量，并且通常很少有独立的代码。在 JavaScript 中，并不是所有的东西都是对象，这意味着我们可以在任何我们想要的地方定义函数，这些函数可以做各种各样的事情，从作用于一个对象，到只是做一个动作。JS 需要一个显式的返回结果是有道理的。

# **回调和匿名函数**

在 Ruby 中，所有的函数都是命名的，所以没有所谓的匿名函数。在 def 关键字之后，所有东西都必须被命名。这很直观，因为作为人类，我们喜欢命名我们所有的行为，从吃饭和睡觉，到假设和推理。如果我们不知道一件事叫什么，我们怎么称呼它呢？

在 JavaScript 中，情况并非如此。信息不像 Ruby MVC 结构那样存储在模型中，函数可以在类之外定义。函数或方法的目的只是将重复的代码组合在一起，而不是主要定义对象行为。因此，JS 允许将代码行组合在一起，而不用给它们起名字。

此外，在 JS 中，函数是一级公民和对象，这意味着它们可以作为参数传递给其他函数。基本上，这意味着你可以定义一个函数，将另一个函数作为参数。虽然这起初对我来说似乎毫无意义，但一旦我们开始讨论语言的底层结构和异步编程的概念，这就变得有意义了。

```
function print(callback) {  
    callback();
}
```

由于处理代码的方式，Ruby 被认为比 JavaScript 慢 200 倍左右。令人震惊，我知道。但是 JavaScript 能够更快地处理代码，因为它采用了异步编程；这允许事件驱动或基于时间的功能(例如，事件监听器、setTimeout、setInterval 等)。)

对于事件驱动或基于时间的函数(也称为高阶函数)，需要能够将一个函数作为参数传递给另一个函数；人们基本上可以在高阶函数的代码块末尾调用该函数，但是将回调作为参数传入是一种语法上的好处，可以减轻这样做的需要。

```
setTimeout(message, 3000);const message = function() {  
    console.log("This message is shown after 3 seconds");
}
```

上例中的“message”函数是从 setTimeout 内部调用的；setTimeout 是高阶函数，“message”是回调函数。

请注意，在引用回调函数时，不会调用任何()。您只需要编写命名函数或匿名函数的代码。

# **语法(简单的东西)**

**功能/方法**

Ruby 方法定义:

```
def sayHi
    puts "Hello!"
end
```

JavaScript 方法定义:

```
function sayHi(){
    console.log("Hello!")
}
```

**识别对象类型**

在 Ruby 中，我们写。类来弄清楚它是什么类型的东西。在 JS 中，我们使用 typeof。

**到整数**

在 Ruby 中将字符串更改为整数包括。to _ I . JavaScript 中同样需要 parseInt()。

**递增快捷键**

*在 Ruby 中:* x+=1
*在 JavaScript 中:* x++

**JavaScript 中什么时候用括号和圆括号？？？**

JavaScript 中的圆括号`()`用于函数调用，包围条件语句，或者用于分组以执行操作顺序。

```
function myFunc() {
  if (condition1) { }
  if ( (1 + 2) * 3) {
    // very different from (1 + 2 * 3)
  }
}
```

大括号`{}`在声明对象文字时使用，或者用来括住代码块(函数定义、条件块、循环等)。

```
var objLit = {
  a: "I am an Object Literal."
}; 
```

希望这有助于减轻 Ruby 和 JavaScript 的一些困惑。我确信随着我的编程之旅的继续，我将会有更多的东西添加到本文中。

来源:[JavaScript 回调](https://www.freecodecamp.org/news/javascript-callback-functions-what-are-callbacks-in-js-and-how-to-use-them/)，[何时使用括号](https://stackoverflow.com/questions/23225375/when-to-use-parentheses-brackets-and-curly-braces-in-javascript-and-jquery)