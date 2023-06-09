# 在 Heroku 上部署——如何托管您的第一个 Javascript / Ruby 应用

> 原文：<https://blog.devgenius.io/deploy-on-heroku-how-to-get-your-first-javascript-ruby-app-hosted-b45b29542661?source=collection_archive---------8----------------------->

![](img/1e50682ba6b9ee8a5261885b08e9a555.png)

约翰·施诺布里奇在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

那么，你准备好托管你的第一个 web 应用程序了吗？恭喜你！作为一名 web 开发人员，这是成长过程中非常激动人心的一步。不幸的是，在部署您的第一个 web 应用程序时，可能会出现一些小问题，并且可能需要花费数小时来扫描解决这些问题。本文旨在强调并解决我在部署第一个 React / Rails 应用程序时遇到的错误，这样您就不必花费我花费的时间来寻找答案。

让我们从你认为你的应用程序在 localhost 上完全按照你想要的方式运行的那一刻开始，你已经准备好让全世界看到它了。Heroku 是一个免费托管 web 应用程序的好地方，但你不能简单地上传你的应用程序，然后就此收工。你必须先配置它。

很有可能，您的前端正在调用您的后端，并且被硬编码为 localhost:3000 或类似的东西。当然，当你的应用被托管时，这是行不通的。一旦托管后，您的后端将位于 Heroku 创建的 URL 下，因此您需要在提取到后端时引用该 URL。这意味着我们需要首先托管您的后端。去 [Heroku](http://heroku.com) 创建一个账户。登录后，创建一个新应用。随便你怎么命名，但是你可能要考虑为你的前端保存一个最合适的名字，并在这个应用的名字后面加上“后端”。

创建后，您可以选择连接应用程序的方式。因为我有最新的 Github，我发现这是最简单的。您可以搜索您的 Github repo 并简单地连接和部署它。不幸的是，你还没有完成。如果你的后端或前端使用了对 Github 隐藏的变量，你需要把它们添加到 Heroku 上，这样它们就可以被访问了。进入“设置->配置变量->显示配置变量”并添加每个变量。您还需要按照说明安装 Heroku CLI 它快速、简单，是目前为止调试出现的部署问题的最佳工具。

太好了！现在，您应该已经在 Heroku 上托管了后端，配置了变量，并且安装了 Heroku CLI。现在，您必须通过 Heroku CLI 迁移和播种后端，方法是访问后端的正确目录，并在终端中输入以下命令

```
heroku rake db:migrate --app=*enter-your-heroku-app-name-here*
heroku rake db:seed --app=*enter-your-heroku-app-name-here*
```

如果这工作正常，你的后端应该是好的。如果没有，您可以通过输入以下命令在访问后端应用程序上的不同路径时查看 Heroku 日志来检查错误。

```
heroku logs --app=*enter-your-heroku-app-name-here*
```

我发现在连接一个使用 Postgres 的 app 并通过 Heroku 进行迁移和播种时会出现错误，可以通过运行以下命令修复。

```
heroku pg:reset DATABASE_URL --app=*enter-your-heroku-app-name-here*
```

到目前为止，您应该已经完成了后端工作，并准备好继续部署前端。首先，您必须用新的 Heroku 后端 url 替换对后端 localhost 的每个调用。接下来，我们来谈谈两个常见的 bug。如果您使用的是 React 应用程序，那么您可能有一个 package.json 文件。如果 Github 给了你 dependabot 警报，而你合并了它们，它很可能也在你的应用程序中安装了 yarn.lock 文件。我的研究建议 Heroku 不允许两者，所以你需要配置所有的东西到一个 package.json 文件中，或者删除 dependabot 的修改。另一个常见的错误是，如果您在 returns 或 renders 中有任何注释掉的代码，它可能会通过 Heroku 导致错误，即使它在 localhost 上没有。确保移动或移除这些区域中任何被注释掉的代码。Heroku 也可能以 localhost 没有的方式包含 CSS 文件，所以如果您注意到了风格上的差异，请注意。

希望您的前端现在已经完全配置好了。一定要提交并推送到 Github，这样就可以把这个版本链接到 Heroku。接下来，再次按照步骤在 Heroku 上创建一个新的应用程序，并给它一个唯一的名称。如果您使用 React 作为前端，您可能需要添加一个包来允许正确的集成。转到此应用程序的设置，为您的前端添加配置变量，就像您为后端所做的那样，并在“构建包”下单击“添加构建包”并粘贴以下 URL。

```
[https://github.com/mars/create-react-app-buildpack.git](https://github.com/mars/create-react-app-buildpack.git)
```

现在您可以部署您的前端并进行测试了！如果某些东西不能正常工作，您需要确定问题是出在前端还是后端，并运行 Heroku CLI 命令再次打印日志，这将有助于您进行调试。如果你对你的代码做了任何修改，一定要把它们推送到 Github，必要的话重新部署你的应用！

我希望这能帮助你成功部署你的第一个 Heroku 应用。恭喜你！

![](img/8990b637af9dee0d7a72321f567bf27c.png)

达米亚诺·林戈里在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片