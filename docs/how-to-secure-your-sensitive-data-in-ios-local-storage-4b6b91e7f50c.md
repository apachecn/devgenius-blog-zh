# 如何保护 iOS 本地存储中的敏感数据

> 原文：<https://blog.devgenius.io/how-to-secure-your-sensitive-data-in-ios-local-storage-4b6b91e7f50c?source=collection_archive---------2----------------------->

![](img/77b89f30d0f1f5306791839db07d65fb.png)

布雷特·乔丹在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

每个项目中存储应用数据的方式可能会有所不同。虽然一些应用程序将数据存储在 iCloud 中，但其他应用程序使用设备本身的本地存储来保存不应离开设备的用户特定信息。无论你把应用程序的数据放在哪里，你都应该确保它被安全可靠地存储，这样没有人可以在你不知道和不允许的情况下访问它。以下是如何保护 iOS 本地存储中的敏感数据的四个技巧。

## 使用钥匙串代替 NSUserDefaults

钥匙串储存加密在设备上的敏感数据，如密码、信用卡号码和安全备忘录。Keychain 内建在 iOS 中，可通过 UserDefaults(即 NSUserDefaults)访问，但直接使用 Keychain 有两大好处:

*   你不用担心 NSUserDefaults 有没有备份或者和 iCloud 同步(其实没有)；
*   您还可以在钥匙串项目中储存除纯字符串以外的对象。

然而，存储敏感数据不是免费的。使用 Keychain 需要更多的工作，因为它需要您自己编写大量代码。但是，如果安全性是你的应用程序的重中之重，那么花时间学习如何正确使用它可能是值得的。例如，如果您想要在 Keychain 中存储一个对象，首先确定该类符合 NSCoding。然后创建一个 SecItem 实例，并传入一个包含要保存的每个属性的信息的 SecItemAttribute 数组；这些属性包括诸如值是否应该加密之类的内容。最后，调用 SecItemAdd()。如果您需要帮助来开始使用 Keychain，请查阅 Apple 的文档来了解如何安全地使用它。

## 使用资产目录而不是 NSDictionary

从版本 6 开始，Apple 不再支持使用 NSDictionary 对象存储数据。相反，您应该使用资产目录。这一点很重要，因为资产目录让你的应用程序可以访问一些字典无法访问的关键功能。例如，使用资产目录，您可以轻松地为图像设置参考，以便高效、自动地加载它们。资源目录还允许您将本地化描述与每个文件相关联，允许您在用户从资源库或项目浏览器中选择图像时显示描述性文本。使用 NSDictionary，没有简单的方法来做这些事情；有了资产目录，事情就简单多了。简而言之，如果您以前将敏感信息存储在 NSDictionary 对象中，请切换到使用资产目录。

## 选择苹果框架而不是本土解决方案

几乎每个开发人员都知道 NSUserDefaults 以及它是如何存储键值对的。大多数开发人员也知道备份文件可以很容易地从/Library/Application Support 中检索到。如果您需要储存敏感信息，请改用“钥匙串”。好消息是，苹果提供了两个框架——钥匙链和文件保护——可以帮助你保护设备上的数据。这些框架很方便，因为它们内置在 Xcode 中，所以您所要做的就是链接它们，这使得开发比从头开始编写自己的实现要容易得多。当然，本土解决方案可能更直接；例如，如果您需要的只是一个简单的键值存储系统，根本没有授权或加密特性。但是如果你需要更高级的东西，利用苹果已经提供的东西。

## 利用 iOS CloudKit

苹果让开发者从他们的应用程序中保存和检索信息变得更加容易。您可以使用 iCloud 或 CloudKit 作为一种简单、安全的方式来存储用户的数据，尤其是社会保险号、信用卡信息、地址或用户 id 等敏感信息，并在用户登录的所有设备上访问这些数据。这两个平台可以无缝协作，因此您不必担心在不同的服务或服务器之间切换。为了保证用户敏感信息的安全(至少尽可能地)，CloudKit 是任何需要存储本地内容的应用程序的绝佳选择。有关如何本地和远程设置 CloudKit 的更多信息，请查看苹果的文档。如果您想更深入地了解安全措施，我建议您查看 Swift by Tutorials，它提供了一整章专门用于保护您的应用的内容。

## 不要在用户首选项中存储机密

尽管很诱人，但不要在用户偏好中存储敏感数据。UserDefaults 的文档清楚地声明:不要在用户默认值中存储敏感的应用程序数据。换句话说，你的应用程序所使用的任何数据都应该安全而私密地存储在你的应用程序代码中或远程服务器上。用户偏好适用于存储少量非敏感信息，如球员姓名或 Twitter 账号。如果您绝对必须存储敏感数据，您可以在将它存储在用户首选项中之前对其进行加密。可以使用 NSUserDefaultsSecurelySaveString()进行加密，使用 NSUserDefaultsSecurelyRetrieveString()进行解密。如果您希望确保从 App Store 下载更新后，只有经过身份验证的用户才能访问您的安全数据，您也可以考虑使用 nsfilepointcompleteuntilfirstusertauthentication。有关这些 API 如何工作的更多信息，请阅读 Apple 的安全编程指南介绍。

## 查看应用商店中的应用

如果你正在开发应用程序，看看人们已经在做什么——然后做得更好。你可以从其他应用程序中获得灵感，即使它们不属于你的领域。浏览 Google Play 或 iTunes 上一些排名靠前的应用，找出人们喜欢它们的原因。寻找常见的可用性问题(如加载时间长)，您可以通过使用不同的技术堆栈或简单地重新设计一些小东西(如您的注册页面)来解决这些问题。还要留意糟糕的设计决策；对于日常用户来说，这些可能不会影响交易，但有经验的设计师每次看到它们都会退缩。例如，如果有两种方法来完成一项任务，其中一种是否比另一种更直观？如果有，那就改！这种想法也适用于你所有的营销努力:看看什么对别人有用，并把这些经验应用到你自己的生意中。

## 在本地存储数据之前对其进行加密

最佳做法是在将应用程序发送的任何数据保存到存储之前对其进行加密。这可以通过使用加密工具来完成，例如 nsfilepointcompleteuntilfirstuser authentic ation 或使用 nsfilepointcompleteuntilfirstuser authentic ation 来保护敏感用户数据。这两种工具都利用硬件支持的加密，并保护您的文件，直到用户使用其 iCloud 或本地帐户凭据登录到他们的设备并解锁它们。有关这些机制的更多信息可以在 NSFileProtection 类参考和使用硬件支持的保护来保护用户数据中找到。

> 不要使用文件保护机制，如。lockedFullScreenPhoto，。锁定文档，。appdata 和。app-extension 如果您正在处理敏感数据！

[](https://medium.com/@rashadsh/why-you-should-use-xcode-instruments-in-your-ios-apps-305f83338508) [## 为什么应该在 iOS 应用程序中使用 Xcode 乐器

### Xcode 的内建开发工具是强大的工具，允许您调试和调整您的 iOS 应用程序，而无需…

medium.com](https://medium.com/@rashadsh/why-you-should-use-xcode-instruments-in-your-ios-apps-305f83338508) [](https://medium.com/@rashadsh/frame-vs-bound-in-ios-whats-the-difference-8dcb927620bf) [## IOS 中的框架 vs 绑定:有什么区别？

### 在 iOS 开发的世界中，您可能以前遇到过框架和绑定这两个术语。你可能用过它们…

medium.com](https://medium.com/@rashadsh/frame-vs-bound-in-ios-whats-the-difference-8dcb927620bf) [](https://medium.com/@rashadsh/map-compactmap-flatmap-e88f936ec9bf) [## 地图，压缩地图，平面地图

### 比较这些函数

medium.com](https://medium.com/@rashadsh/map-compactmap-flatmap-e88f936ec9bf) 

**感谢**

我写软件开发，咖啡和一般的话题。非常感谢你关注我和我的故事。很高兴有你在这里，并希望它值得你的时间。

[](https://medium.com/@rashadsh/membership) [## 通过我的推荐链接加入媒体- Rashad Shirizada

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

medium.com](https://medium.com/@rashadsh/membership)