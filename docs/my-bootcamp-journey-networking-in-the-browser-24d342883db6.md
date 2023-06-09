# 我的训练营之旅:浏览器中的网络

> 原文：<https://blog.devgenius.io/my-bootcamp-journey-networking-in-the-browser-24d342883db6?source=collection_archive---------16----------------------->

## 了解 XHRequest、Fetch API 和 CORS

![](img/760e98b187c40315525724005fe58a42.png)

泰勒·维克在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

在我以前的文章中，我谈到了错误和错误处理。你可以[在这里](https://medium.com/dev-genius/my-bootcamp-journey-errors-and-error-handling-40b2b28b5b45)找到那篇文章。今天的主题是浏览器中的网络，所以让我们开始吧。

# 概观

浏览器包含许多网络组件，可以帮助你建立网络。第一个是 XHR，代表 XMLHttpRequest。它是一个在客户端和服务器之间传输数据的 API。XHR 的伟大之处在于，当你从服务器请求一些数据时，它不会刷新整个页面，它只是更新需要更新的部分，而不会干扰用户正在做的事情。随着时间的推移，一种新的网络 API 出现了，它比 Fetch API 好得多，并得到了现代浏览器的推荐。

# XHR (XMLHttpRequest)

![](img/bd7f203232dd16295911b04e751363f2.png)

让我们看看这里发生了什么。

1.  我们在第一行代码中创建了一个新的 XHR 请求。
2.  我们在 onReadyStateChange 属性上调用一个函数来监听请求的 readyState。4 表示响应下载完成。
3.  我们检查请求状态，如果是 200，这意味着我们做了所有的事情，数据成功返回。
4.  用 open 方法初始化请求，并传入我们想要发出的请求类型(GET、POST、DELETE 等)。)在我们的例子中，GET。在第二个参数中，我们说我们想要请求什么 URL。
5.  最后，XHR.send()将请求发送到服务器。

这就是使用 XHR 进行基本请求的要点。👍

# 获取 API(基本)

Fetch API 是发出请求的现代方式。Fetch API 返回一个承诺，这使得我们更容易使用 async-await。让我们看看典型的获取请求是什么样子的

![](img/429a362c04f5c624717d45cc6574d5ed.png)

让我们看看这是怎么回事。

从第 2–6 行开始。我创建了一个 IIFE 函数(一个在声明后立即被调用的函数)并使其异步。我使用 fetch API 向 URL(在我们的例子中是 JSON 占位符)发出一个`get`请求。我们附加了`await`关键字，因为它返回一个我们需要等待的承诺，然后它会自动存储在变量`fetchRequest`中。在 fetch 中，我们需要手动将数据转换成 JSON，我们在第 4 行完成了这一操作。这也返回了一个我们需要等待的承诺(因此有了`await`关键字)。一旦我们有了响应变量(它有我们的实际数据),我们就可以做我们想做的任何事情，在我们的例子中，我们在我们的`displayResult`函数中传递它，这样我们就可以循环通过它和`console.log`待办事项标题。

然而，在执行异步任务时可能会出错，所以如果我们有办法捕捉这些可能的错误，那就最好了。这就是`try-catch`块的用武之地😃

![](img/a8c8360beba8df347fc5a05fc3bb882e.png)

这是相同的函数，但是使用了`try catch`来捕捉任何错误。在我们的例子中，我故意在我们的获取请求中键入了错误的 URL(拼写为 todos error ),这样它就会在我们的`catch`块中发送我们的错误，我们的`console.log`。

让我们更深入地研究一下 Fetch API，这样您就可以从整体上看到它。

# 获取 API(发布)

一个简单的 post 请求(向服务器发送数据)如下所示

![](img/4bb937d01dc366c3ae954cace3edf401.png)

具体来说，我们做的和以前一样，但是这里唯一的不同是我们向 JSON 占位符 API 发出了一个`post`请求。从第 6–13 行开始，我们向 fetch 请求传递一些额外的选项，这里我们告诉服务器`method`属性是 post 而不是`get`请求。`headers`属性告诉服务器我们发布什么类型的内容，在我们的例子中是`application/json`。`body`属性是我们需要指定向服务器传递什么数据的主要属性。在我们的例子中，`body`属性是一个 JSON 字符串(object ),包含我们给它的数据，数据结构需要与你发布的 API 的结构相匹配。

我们仍然像以前一样做所有正常的到 JSON 的数据转换，最后我们`console.log`。这是发送到 JSON 占位符 API 的实际数据。

# 获取 API(响应对象)

现在，让我们仔细看看响应对象。为了澄清，响应对象是关于当我们进行 API 调用时返回给我们的响应的信息。

![](img/470752f7521ed81b8cdb2c1d02610542.png)

这是我们在响应对象(`headers`、`status`、`URL`)上访问的信息，这里是`console.log`。我们可以有很多头，这就是为什么我们调用`get`函数来指定我们想要哪个头。

# 获取 API(请求对象)

现在，让我们仔细看看请求对象。澄清一下，我们可以访问我们请求的信息。为了做到这一点，我们需要像这样使用`Request`构造函数创建一个新的请求。

![](img/7e108efad157fe147b9e1142415ea3f8.png)

我们可以访问几个只读属性，如`method`、`URL`、`headers`、`cache`等。

# 什么是 Cors？

CORS 代表**跨源资源共享**和当 CORS 设置为允许`**Access-Control-Allow-Origin: ***` 时，这意味着任何源/域都可以向服务器发出请求。然而，当你试图从服务器获取数据时，有时你会得到一个 CORS 错误，这是因为有时服务器不允许来自不同来源的请求(获取、发布、删除等)。例如，如果我们试图获取 Google，我们会得到一个 cors 错误，因为 Google 不允许来自任何随机域/源的请求。

![](img/74075452075eb32c5350c7f66a7e62f8.png)

谷歌将不得不设置 CORS，允许我们的域名向他们的服务器发出请求。

所以，万一你遇到这种类型的错误，这就是它的意思👍

这就是本文的全部内容，我希望这能帮助人们更好地理解浏览器中的网络。😃

尽情享受吧！👍

附注(阿诺德·施瓦辛格的声音)我会回来的😎

~ ***爱活着，活着要代号***