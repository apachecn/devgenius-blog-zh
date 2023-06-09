# 如何使用反应文件浏览器

> 原文：<https://blog.devgenius.io/how-to-use-react-file-previewer-da7427ec1715?source=collection_archive---------1----------------------->

![](img/626deac8d4e44c4adf5b446c01dfb660.png)

图片来自[https://github.com/plangrid/react-file-viewer](https://github.com/plangrid/react-file-viewer)

# 目的

虽然我探索了一些 react 文件查看器库来实现“文件查看功能”，可以在不安装的情况下查看任何文件。事实上，很难找到一个非常好的，即使我找到了几个图书馆，并探索了它。最后，我发现了一个很好的库，叫做“反应文件浏览器”，我将向你展示什么是反应文件浏览器，以及如何使用这个库来展示一个例子。

# 什么是反应文件浏览器？

正如我提到的，react 文件查看器是一个 npm 库，我们可以在没有任何安装的情况下查看文件。一方面，有很多库可以用来查看 pdf。另一方面，有一些库可以用来查看其他扩展名，如 png、docx、xlsx、csv。我知道现在最重要的文档类型是 PDF，因为这种文档类型基本上不允许我们编辑。这更安全，我们保护文档免受任何欺骗，但仍然需要查看任何其他扩展，因为有很多人使用 Microsoft office，以及一些图像。

# react-file-viewer 的优缺点是什么？

## 赞成的意见

*   支持不同的扩展

这个库支持不同的扩展名，如 png，docx，xlsx，csv。可能存在其他付费的浏览者，但是这个图书馆是免费的。这太神奇了！甚至支持视频(mp4，webm)和音频(mp3)。

*   使用方便

虽然我稍后会展示一个例子，但是这个库不需要很多代码。只需要文件和类型。这个例子有一些错误组件，这是推荐的，但它仍然是可选的(这并不花时间，所以我也建议您安装和使用错误组件)。

*   没有乱码文本

我试图使用几个文件浏览器，但我发现一些混乱的文本，以及一个错误的文本结构。

这个库没有任何乱码，下载的时候会出现“正在加载 0-100%”的文字。这是向用户显示当前情况的一个非常好的功能。

*   也支持功能组件

虽然官方的例子是由类组件编写的，但是这个库也可以在功能组件中工作。这是一个很好的特性，因为我们不需要准备一个类组件来使用这个库。

## 骗局

*   没有频繁更新

上次更新时间是 2 年前，也就是说这个库最近没有更新。这并不坏，但是当这个库停止开发并且我们不能再使用的时候，你需要找到一个不同的依赖。

*   不支持 ppt 扩展

那要看情况，不过这个库不支持 ppt，虽然支持 docx 和 xlsx。如果您对文件查看器的需求包括 ppt，那么这个库并不适合您。

*   不支持 react18(仅限 xlsx、csv)。

您可能知道，react 现在更新了不同的语法。大概就是因为这样，这个库不能再支持 xlsx，csv 了。如果我们降级到 react 17，xlsx 和 csv 就可以工作了(任何其他扩展在 react 18 中仍然可以工作)。

现在这还不是很糟糕，但是正如我已经提到的，这个库最近没有更新，这可能是几年后的大问题。

## 示例(循序渐进)

1.  安装依赖项并使用它。react-file-viewer 是必需的，但是 logging-library 和 custom-error 是可选的(推荐使用这些)。

```
npm install react-file-viewer logging-library custom-error
// logging-library and custom-error is optional.
```

2.导入一些方法并使用它。因为我想向您展示一个文件查看器，所以我使用 useState 设置了 view 按钮。您可以使用本地文件或 URL。我把我的文件放在公共文件夹中，只需要使用它，但是你不需要写公共文件夹的路径，你只需要写文件名。这很实用

3.这是我的屏幕。如果你点击“查看”按钮，你准备的文件就会出现。在这项事业中，我以我的简历 PDF 为例。

![](img/2a8554f1002608b4603d6f182b225278.png)

# 结论

react-file-viewer 并不是查看文件的完美库，但是使用起来很有用。

当您搜索文件查看器库时，值得一试。

# 参考

反应文件浏览器[https://www.npmjs.com/package/react-file-viewer](https://www.npmjs.com/package/react-file-viewer)

感谢您的阅读！！