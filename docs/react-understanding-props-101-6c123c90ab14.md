# 反应:理解道具-101

> 原文：<https://blog.devgenius.io/react-understanding-props-101-6c123c90ab14?source=collection_archive---------8----------------------->

![](img/7f350fed5ee7e0bd7d6e6a6a27d00c07.png)

[cruftlesscraft.com](https://www.google.com/url?sa=i&url=https%3A%2F%2Fcruftlesscraft.com%2Fpassing-data-from-twig-to-javascript&psig=AOvVaw3kHEF2I0fFdkZVoULce8xm&ust=1650465626266000&source=images&cd=vfe&ved=2ahUKEwju9prcraD3AhURxyoKHUcODOcQr4kDegUIARCCAQ)

不管你对 web 开发有什么看法，React 仍然是构建“动态”用户界面最快的库之一，除了状态的概念，PROPS 是你总能在每面写有 React 的墙上找到的小砖块之一。

为什么反应快？

简单！有了 react，浏览器不再需要重新呈现整个界面，而只需要显示一个数字的简单段落。它只需呈现发生变化的内容，仅此而已。这样想，想象你是一个艺术家，有画上面这幅图像的简单任务(*画任何东西都不简单..lol* 。为了保护环境，我们给了你一个数字板和一支数字笔。现在，想象一下，你花了 6 个小时试图在数字键盘上再现上面的图像，当你正要完成最后一笔时，一个像我一样的讨厌的家伙走到你面前说……啊！看，你用绿色代替了红色的胸标。(*虽然*我永远不会这么做)。

现在，你的数字键盘突然决定告诉你该做什么，而不是让你擦掉绿色并用红色代替，而是让你从头开始重新绘制整个图像！都是因为你想简单地改变颜色！(*我来破数字垫*)。

现在，在没有反应情况下，每当我们的用户通过改变聊天框的颜色这样简单的事情来改变我们网站 UI 的一部分时，浏览器必须经历这种折磨！(*等等！浏览器是如何在做出反应之前容忍所有这些的呢？！*)。他们做到了。也许这就是为什么它向脸书的内部团队抱怨，并要求他们提供一个使工作更容易的工具。

React 是 facebook 对浏览器请求的回应。

有了 React，浏览器只需绘制一次图像。无论发生了什么变化或者需要发生什么变化(比如用绿色替换红色)，都不需要重新绘制整个图像。React 使用名为 Virtual-DOM 的 DOM 的辅助副本来完成这项工作。(*如果你不能马上理解它也没关系，因为即使在写作中也是抽象的*)。

然而，道具是赋予 react 这种惊人力量的必要组成部分，理解它是我写这篇文章的目的。那么，没有进一步的啊做，让我们跳进它。

react 中的组件只是一个返回 jsx 表达式的函数——通过扩展，是一段 HTML 代码。这个返回的代码只是我们对浏览器的一个描述，说明我们希望界面在任何时间点的外观。因为这些是常规的 javascript 函数，所以它们可以接受在返回块中使用的参数。这些参数可以从一个函数传递到另一个函数，称为 props。

假设我有一个名为 App 的父组件。App 被称为父组件，因为它返回 3 个其他组件，分别称为 Header、Content 和 Total，并且因为它将它们作为父组件返回，所以 App 可以决定向它们传递一些它们各自需要发挥作用的属性。

首先，让我们定义我们的父应用组件:记住，它只是一个常规函数。

```
function App() {
const course = ‘Half Stack application development’
const part1 = ‘Fundamentals of React’
const exercises1 = 10
const part2 = ‘Using props to pass data’
const exercises2 = 7
const part3 = ‘State of a component’
const exercises3 = 14return (
<div className=”App”>
<Header name={course}/>
<Content part={part1} ex={exercises1}/>
<Content part={part2} ex={exercises2}/>
<Content part={part3} ex={exercises3}/>
<Total number={exercises1 + exercises2 + exercises3} />
</div>);}export default App;
```

我们的 App 函数中有一些用“const”关键字声明的变量。这些是父应用程序组件想要传递给子组件的信息，它正在返回块中呈现这些信息。例如，父组件决定将*课程*信息传递给标题组件，它给标题组件命名为*名称，*这意味着在标题组件中，课程信息可以作为*名称获得。*

但是，我们如何在我们的 Header 组件(子组件)中访问这个 *name* 信息呢？

让我们看看:

```
function Header(props) {return (<div><p>Course Title: {props.name}</p></div>)}
```

再次注意，我们的 header 组件也是一个函数。

现在，请注意，我们已经将名为 *props* 的参数传递给了这个头函数，并且在返回块中，我们已经使用 *props.name.* 访问了 name 的值

请记住，当在父应用程序组件的返回块中调用 Header 组件时，会将*名称*传递给它。关键字 *props* 只是*属性的缩写。*每当你把它看作一个函数调用的参数时，它的意思就是这个函数正在从一个父函数(比如 App)接收信息，这个父函数在它自己的返回块中呈现它。把道具想象成一个物体的名字。在这种情况下，我们的道具对象看起来像这样:

```
let props = {name: course,}
```

为了访问 name 键的值，我们将因此使用 *props.name* 并且因为 *props.name* 是一个 javascript 语法(记住在这些函数中返回的不是纯 HTML 或纯 JS，而是 JSX，即使它在幕后全部翻译成纯 JS-*Babel 有效地完成了这项工作*，我们将把它嵌入{}。

组件可以嵌入到组件中，并且这种嵌入可以根据需要进行。为了解释，假设我们的标题组件决定也成为标题组件的父组件。这个标题组件将是呈现标题的组件，而不是标题组件本身。

我们如何帮助新的标题父组件将从其应用程序父组件收到的信息传递给它自己的子标题组件？

首先，让我们定义标题组件。

```
function Title(props) {return (<div><p>{props.title}</p></div>)}
```

从上面可以看出，我们的 Title 组件将收到一个名为 *title* 的信息，该信息将从呈现它的 Header 组件传递给它。见下文

```
function Header(props) {return (<div><Title title={props.name}/></div>)}
```

请注意，标题组件传递给标题组件的信息也是从应用程序接收的，它所做的只是给它一个不同的名称，如*标题。*