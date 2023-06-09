# React 中的类别与功能组件

> 原文：<https://blog.devgenius.io/class-vs-functional-components-in-react-8a72807e4fbe?source=collection_archive---------11----------------------->

![](img/0db1ff40d4197a50389b10c1eb1128bb.png)

[Zan](https://unsplash.com/@zanilic?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 在 [Unsplash](https://unsplash.com/s/photos/typing?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的照片

组件构成了 React 应用程序的结构。应用程序越大越复杂，您拥有的组件就越多。组件可以分为类组件或功能组件，由 JavaScript 和 JSX 元素混合组成，可以接受称为 props 的输入，这是 properties 的缩写。所有 React 组件都有一个内置的状态对象，可以根据需要对其进行操作和渲染。组件是否需要自己的状态可能是决定在应用程序中使用哪种组件的决定性因素。

**类组件**

类组件，也称为有状态或容器组件，是具有 React 库功能的常规 ES6 类。为了让这些组件工作，它们必须有一个 render()方法，无论您在其中返回什么。它们被称为“有状态的”，因为它们可以使用 this.state 和 this.setState()创建和更改自己的状态。除此之外，类组件可以使用生命周期方法，这些方法是在组件安装、卸载等不同阶段使用的方法。

**功能组件**

功能组件是无状态的，并且是设置组件的最快方式，因为它们只是 JavaScript 函数。它们有时被称为表示组件，因为它们只是接受和返回要在 DOM 中呈现的数据。与类组件不同，它们不持有自己的状态对象，所以所有呈现的信息都需要从父组件作为道具传递给功能组件。在这些函数中，没有 render()，因为没有状态，所以无法使用生命周期方法。然而，从 React 的一个更高版本开始，功能组件现在可以使用钩子方法来访问生命周期事件。

**差异**

您会立即注意到这些组件之间的第一个区别是语法。类组件，除了我上面提到的使用 render()之外，还必须扩展 React。组件来使用 React 库。功能组件通常是首选，因为它们最终会更小，代码更少。这使得阅读和测试更容易，因为副作用更少。

基本上，当需要使用状态和生命周期方法时，应该使用类组件，而功能组件应该用于其他所有事情。尽量少用类组件，以最大限度地减少副作用和可能导致应用程序错误的状态问题。