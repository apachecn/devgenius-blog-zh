# 如何使用状态管理库 Zustand

> 原文：<https://blog.devgenius.io/how-to-use-zustand-which-is-react-state-management-library-648f55a0455f?source=collection_archive---------1----------------------->

![](img/51520d8adee0b58f35d239ba911b2a2d.png)

图片来自[https://github.com/pmndrs/zustand](https://github.com/pmndrs/zustand)

# 目的

由于我在工作期间研究了 Zustand，关于这个库的例子并不多，所以我将它分享给你。

# Zustand 是什么？

Zustand 是 JS 中使用简化 flux 原理的状态管理库之一，在 github 上有 16.8k stars。您可以在 react 或任何其他 JS 框架(如 Angular 或 Vue)中使用这个库，甚至可以在 Vanilla JS 中使用。

如果你有使用 Redux 的经验，这个库很容易理解，因为它和 Redux 很相似。

# 利弊

## 赞成的意见

*   与 Redux 相比，代码更少

正如你可能知道的，redux 是一个非常有用的状态管理库，但是他们需要很多样板文件。因此，一般来说，Redux 非常适合相对较大的项目或应用程序，这些项目或应用程序应该有几个不同的状态，并且经常改变状态的状态。另一方面，Zustand 不需要太多样板文件，即使你不需要你的父母提供服务。

*   简单的文档

基本上，redux 有一个主要的方法来编写，其中包含代码示例和官方文档中的许多说明。这很好用，但是在一个小项目中可能用过头了。相反，Zustand 有基础教程，有中等量的代码示例作为菜谱，就这样。这对于简单项目是可搜索的。

*   灵活性

正如我提到的，这个库包含了大量的代码示例，这些示例包含了几种编写方法。你可以写得更简单，或者你可以集成一些中间件，比如 immer，以实现不变性，或者你甚至可以写你的代码，比如 redux way，它有 reducer，dispatch。redux 有一个大型全球商店，但 Zustand 允许您独立创建多个商店。当然，您可以创建一个全局商店，也可以将不同的商店创建为几个部分并进行组合。此外，这个库也支持 TypeScript。这个库非常灵活。

## 骗局

*   信息不多

没有太多关于 Zustand 的信息，因为国家管理系统存在几个。由于 redux 是最受欢迎的库之一，你可以很容易地在文档中甚至在堆栈溢出中找到解决方案，因为已经有很多人在为同样的问题或错误而奋斗。然而，那不是给 Zustand 的。你需要更多的尝试和失误来找到解决方案。

*   很多括号

在我看来，你需要有很多括号来节省代码量。特别是如果你想在没有任何其他库的情况下获取一些数据，你需要写更多的代码，因为你应该用括号写状态变化。这是一种个人偏好，因为至少你可以保存你的代码，避免滚动。

*   难以找到最佳实践

正如我提到的，这个库具有非常好的灵活性。另一方面，您需要选择如何编写代码来使用 Zustand 创建您的应用程序。换句话说，很容易“使用”Zustand，但是很难“高效使用”Zustand。在我看来，在实际项目中使用时，你需要“试错”。

这是足够的基本信息，让我们探索一些例子。

# 示例 1(计数器应用程序)

这是我在 src 目录下的文件夹结构(只包含必要的)。

```
src
├── App.css
├── App.js
├── app
│   └── store.js
├── features
│   └── counter
│       └── Counter.js
├── index.css
├── index.js
```

## 步伐

1.  创建一个基本的 react 应用程序

```
npx create-react-app zustand-counter(this name is app to you)
cd zustand-counter
```

2.安装 Zustand

```
npm install zustand
```

3.在 features/counter 文件夹中创建“Counter.js ”(创建文件夹是可选的)。我只是专注于意义。

4.在 App.js 中导入您的 Counter.js

5.在 app 文件夹内创建“store.js”(创建文件夹部分是可选的)。您需要导入 zustand，并将其用作 useStore。您应该创建 store，并设置像 count 这样的默认值，并且您可以通过使用 callback 来创建一些方法。您可以设置像 1 这样的实数值，或者您可以设置 payload 来更动态地使用。这个“有效载荷”的名称由你决定，因为官方文件在这部分写着“by”。然而，我对 redux 很熟悉，所以我把 payload 放在这里是有意义的。

6.将这个“useStore”导入 Counter.js，并使用它。你可以在 redux 中使用某种 useSelector，你需要用 useStore 选择(oldValue) => (newValue)。如果要使用 payload，需要注意回调，因为调用的时机问题。

7.就是这样！这是应用程序屏幕，它应该工作。您可以使用任何组件来注入状态，即使它们具有深度嵌套的文件夹结构。

![](img/70922fbca50fbe2e2767665e8bb43bba.png)

# 示例 2(获取信息应用程序)

这是我在 src 目录下的文件夹结构(仅包含必要的文件夹，类似于示例 1)。

```
src
├── App.css
├── App.js
├── app
│   └── store.js
├── features
│   └── fetchData
│       └── FetchDataZustand.js
├── index.css
├── index.js
```

## 步骤(1 和 2 与示例 1 相同)

1.  创建一个基本的 react 应用程序

```
npx create-react-app zustand-fetch-data(this name is app to you)
cd zustand-fetch-data
```

2.安装 Zustand 和 axios(使用 axios 获取数据)

```
npm install zustand axios
```

3.在 features/fetchData 文件夹中创建“FetchDataZustand.js”(创建文件夹是可选的)。

4.在 App.js 中导入“FetchDataZustand.js”

5.在 app 文件夹内创建“store.js”(创建文件夹部分是可选的)。你需要从“zustand”和 axios 导入 create，并使用它。比如 redux 例子，我准备了三种不同类型的 state 值，分别用来获取确切的数据、加载和获取错误(名字由你决定)。并创建一个带有回调的获取方法。您可以为数据提取的每个部分设置主导和错误状态。出于演示目的，我使用了 jsonplaceholder 的端点，但是您可以使用任何想要的端点。

6.将这个“useStore”导入到 FetchDataZutand.js，并使用它。与第一个例子相同，您可以使用“useStore”，如 redux“use selector”。“陈述本身”和“动作”都可以用。

7.就是这样。下面是实际屏幕，你可以看到加载状态。这个数据量很小，所以你几乎看不到加载状态，但是加载和数据读取状态是工作的。

![](img/35e666de93dcff777c5151f6042f6b43.png)

下面是我故意拼错端点错误版本。您可以清楚地看到加载和错误信息。

![](img/940d68d79aefd4d88c9910efb0092045.png)

# 结论

Zustand 是最有用的状态管理库之一，与 Redux 相比，它非常灵活且代码更少。如果你需要一些全局语句库，我推荐你考虑这个库。

# 参考

官方文件:[https://docs.pmnd.rs/zustand/introduction](https://docs.pmnd.rs/zustand/introduction)

切片示例:[https://github-wiki-see . page/m/pm ndrs/zustand/wiki/Splitting-the-store-into-separate-slices](https://github-wiki-see.page/m/pmndrs/zustand/wiki/Splitting-the-store-into-separate-slices)

Zustand 简单状态管理指南:[https://blog . bitsrc . io/zustands-Guide-to-Simple-State-Management-12c 654 c 69990](https://blog.bitsrc.io/zustands-guide-to-simple-state-management-12c654c69990)

Reactで状態管理 初心者でも簡単 Zustandの設定方法：[https://reffect.co.jp/react/zustand](https://reffect.co.jp/react/zustand)

感谢您的阅读！！