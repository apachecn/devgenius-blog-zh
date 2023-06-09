# 使用 Ruby Gems 进行认证和授权

> 原文：<https://blog.devgenius.io/authenticate-and-authorize-with-ruby-gems-a7f24bc62446?source=collection_archive---------10----------------------->

## 如何使用 JWT 和 BCrypt 宝石来保护您的全栈应用程序

![](img/a94b68144ea23ce8826433a831b15db3.png)

[iMattSmart](https://unsplash.com/@imattsmart?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

如果您计划让用户选择为您的应用程序创建帐户，您将实现身份验证和授权。身份验证检查登录的用户是否提供了正确的凭据(匹配用户名和密码)。授权在认证之后；一旦我们知道我们有一个特定的用户，我们决定他们可以访问什么。

我的应用程序在前端使用 React，在后端使用 Ruby on Rails。我们将在 React 前端从用户那里获取信息，但是我们将它发送到 Rails 后端进行身份验证和授权。BCrypt 是一个密码散列函数，它帮助我们进行身份验证。JWT 允许我们编码和解码令牌；这是授权的一部分。一旦我们将这两个 gem 添加到我们的 Gemfile 中，我们就可以开始使用它们的特性了。

[](https://github.com/codahale/bcrypt-ruby) [## codahale/bcrypt-ruby

### 保护用户密码安全的简单方法。如果您明文存储用户密码，那么窃取…

github.com](https://github.com/codahale/bcrypt-ruby) [](https://github.com/jwt/ruby-jwt) [## jwt/ruby-jwt

### RFC 7519 OAuth JSON Web Token (JWT)标准的 ruby 实现。如果您有更多关于…的问题

github.com](https://github.com/jwt/ruby-jwt) 

# 用 BCrypt 创建安全密码

BCrypt gem 非常棒，因为它在幕后为我们做了很多工作。只需将代码行`has_secure_password`添加到用户模型中，我们就可以调用 BCrypt 的所有功能。现在我们的用户控制器知道散列它创建的密码。控制器从前端接收某些参数，包括“密码”。当我们在 users#create 操作中创建新用户时，密码会自动散列。当需要使用散列密码对用户进行身份验证时，我们可以使用一个`.authenticate()`方法来检查通过 params 传递的密码是否与创建的密码匹配。

那么这些杂凑是怎么回事？我们散列密码，因为在数据库中存储明文密码是不安全的。人们可以访问数据库并恶意使用存储的密码。哈希算法使用一种无法复制的算法将密码转换成无法识别的东西。由于数据库存储了用户输入的密码无法识别的内容，您可能想知道我们如何知道他们何时为自己的帐户提供了正确的密码。

我在熨斗学校的老师杜克解释得很好。想象密码是一幅美丽的玻璃画。哈希拿起那幅玻璃画，按随机顺序把它打碎成一千个小块。它现在看起来一点也不像最初的玻璃画。然而，如果你提供一个玻璃画的精确副本，哈希将会以同样的方式粉碎它，这样你就可以比较粉碎的残骸。BCrypt 对密码进行哈希处理，并比较哈希结果，而不会保留敏感信息。

# JWT 代币

为了授权，我们使用代币。基本上，我们在浏览器上留下一个令牌，以便每个组件/页面都可以获取它，并检查后端以查看令牌包含什么信息。JWT 允许我们编码和解码这些令牌；编码和解码在这里是必要的，因为用户可以访问他们浏览器的令牌，我们不想给他们留下比他们应该得到的更多的信息。

## 登录和注册时创建令牌

每当我们对用户进行身份验证时，我们都会创建令牌。当用户创建帐户或登录他们的帐户时，我们会创建一个令牌用于以后的授权。

登录时，我们向后端 AuthController 发送一个获取请求。AuthController 是我们处理令牌业务的地方。在 auth#create 操作中，我们使用用户提供的用户名和密码参数，在对它们进行身份验证之后，用用户信息创建一个令牌。使用 JWT 创建令牌需要令牌持有的对象(`user.id`)、密钥(【chookey】)和 JWT 使用的算法(【HS256】)。我们将用户信息作为对象包含在内，稍后我们可以通过解码令牌来访问它。最后，我们必须将令牌发送回前端，并在本地存储中设置它。

![](img/16bc94d3a2525ce89fe8c7c2da060020.png)

为用户认证和创建令牌

注册时创建令牌看起来是一样的，只是没有身份验证。

## 创建一个高阶组件来授权其他组件

我们有多个组件需要借助令牌进行授权。这就是为什么创建一个能够使用 localStorage 中的令牌来授权节省重复代码的高阶组件。任何想要授权用户的组件现在都可以将自己包装在更高级的组件中。

[](https://reactjs.org/docs/higher-order-components.html) [## 高阶组件-反应

### 高阶组件(HOC)是 React 中重用组件逻辑的一种高级技术。hoc 不属于…

reactjs.org](https://reactjs.org/docs/higher-order-components.html) 

正是在这个高阶组件中，我们获取令牌并将其发送到后端进行授权。我们可以用代码行`const token = localStorage.getItem(‘token’);`从 localStorage 获取令牌。为了在获取请求中发送令牌，我们将其作为获取头的一部分。获取请求应该是这样的:

![](img/11cdbadd3f32902aa18795ed47260859.png)

我们的获取请求将我们带到 auth#show 操作。这里我们用代码行`token = request.headers[‘Authorization’].split(‘ ‘)[1]`从获取请求对象头中获取令牌。接下来，我们在 JWT `.decode()`方法的帮助下解码令牌，最后我们将令牌为我们隐藏的信息发送回用户。总之这个动作看起来是这样的:

![](img/1c37e22f1d51a510b2e809952bd9d579.png)

## 注销时删除令牌

最后一部分非常简单，不需要 JWT 的帮助。当用户注销时，应用程序应该不再授权该帐户。为了做到这一点，我们从 localStorage 中删除了令牌，因此我们不能再将它发送到后端进行授权。只需一行代码，我们用高阶组件包装的组件就会意识到它们没有授权用户。这一行代码是`localStorage.removeItem(‘token’);`。这结束了我们的令牌的漫长，美丽的旅程。