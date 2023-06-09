# 如何制作抖音克隆或短视频 YouTube Flutter App

> 原文：<https://blog.devgenius.io/how-to-make-tiktok-clone-or-short-video-youtube-flutter-app-a38dff79789e?source=collection_archive---------4----------------------->

![](img/ac557d1e66fb509eb38ea39fa688d056.png)

# 介绍

抖音是中国公司字节跳动旗下的视频分享社交网络服务。社交媒体平台用于制作各种短片，包括舞蹈、喜剧和教育等类型，时长从 15 秒到 1 分钟不等(一些用户为 3 分钟)。自 2016 年推出以来，抖音在东亚、南亚、东南亚、美国、土耳其、俄国和世界其他地区迅速受到欢迎。

现在视频分享已经成为一种趋势。就连脸书的母公司 Meta 也表示，人们在脸书和 Instagram 上观看其短片视频的时间增加了 30%以上。你有没有想过在你的平台上加入像抖音、YouTube、脸书或 Instagram 这样的视频分享功能？你可能会认为将视频文件存储在云中很昂贵，而且可能会消耗大量带宽。此外，您可能会认为，如果许多人同时加载您的视频，很难实现视频流以及如何处理流量。在本文中，我将向您展示如何免费(在某种程度上)使用 Flutter 和 Firebase 存储创建抖音克隆应用程序或短视频 Youtube 克隆应用程序。为了让你更容易理解、形象化和学习，特别是对于初学者，我在这篇文章中附上了许多截图。现在让我们把手弄脏。

# 先决条件

*   下载并安装 Visual Studio 代码 IDE
*   下载并安装 Flutter SDK
*   Firebase 云存储

# 涉及的成本

我们将使用的唯一云解决方案是 Firebase 云存储。因此，让我们研究一下 Firebase 的免费版本能提供什么。Firebase 中有两个计划:

a)星火计划(免费版)

b)火焰计划(付费版)

![](img/a26ebb58799f6c542366d5df89a03141.png)

有了星火计划，你可以在云中免费存储高达 5 GB 的视频文件。假设一个视频文件是 20MB，你可以免费存储多达 250 个视频文件。请注意，这 5GB 的可用存储空间仅适用于默认存储桶。如果您添加了新的存储桶，您在新存储桶中的存储使用将根据 Blaze 计划收费。这就是“每个项目多个桶”的含义。

带宽方面，每天免费获得 1 GB。假设一个视频文件是 20MB，你每天可以免费服务 50 个用户。

如果您的使用量超过限制，那么您将根据 Blaze 计划收费，云存储费用为 0.026 美元/ GB，带宽费用为 0.12 美元/ GB。

当你刚刚启动的时候，通常你没有很多用户。所以很可能你不需要支付任何费用，直到你得到越来越多的用户。到那时，你应该能够将你的产品货币化来支付云计算。

# 视频流与视频下载

视频流是指设备不断接收数据以观看视频，而无需获取整个物理媒体文件。而视频下载会制作媒体文件的副本，并在您开始观看视频之前将其保存在本地设备上。就用户体验而言，实现视频流会更好，因为视频一旦被观看就立即播放，尤其是对于长格式的视频。然而，你需要为这种流媒体服务付费，而且通常并不便宜。为了最大限度地降低我们的成本，甚至达到零成本的极端，我们将坚持视频下载。因此，视频的持续时间必须很短，视频的大小必须尽可能小，以便可以更快地下载视频文件。因此，我们将把视频时长限制在 60 秒，并且我们必须在上传到 Firebase 云存储之前压缩视频。

# 设置开发环境

首先，您需要下载并安装一个 IDE。我选择 Visual Studio 代码是因为它是轻量级的。此外，还有许多扩展和工具可以安装到 IDE 中，使您的工作更容易。它绝对是初学者的最佳 IDE，或者是专业程序员的高效工具。现在让我们开始在您的机器上设置环境。

1.  前往[https://code.visualstudio.com](https://code.visualstudio.com/)，下载并安装适用于您的操作系统(OS)的 Visual Studio 代码。

![](img/6e8593b14fe10f15eea42253c08c6dea.png)

2.前往 https://docs.flutter.dev/get-started/install为您的操作系统(OS)下载并安装 Flutter SDK。您需要按照那里的说明为 Android 和 iOS 平台设置您的开发环境。

![](img/9956edca03f38a970c845f86a14894c7.png)

# 设置 Firebase 云存储

3.去 https://console.firebase.google.com/[创建一个新项目。请注意，您首先需要有一个谷歌帐户。](https://console.firebase.google.com/)

![](img/81cf09dd415e75aea5c926513667a203.png)

4.为您的项目命名(例如抖音克隆)，然后单击继续继续。

![](img/e850e6d1bf7dbf68e6753777962b5e25.png)

5.将所有内容保留为默认值，然后单击“继续”继续。

![](img/3407c1eb6f51cc485b8529c3033090a2.png)

6.将所有内容保留为默认值，然后单击“创建项目”按钮继续。

![](img/7094416e7a587556974069b7094dcfc7.png)

7.等待一段时间，让 Firebase 创建您的新项目。之后，您应该能够看到如下所示的屏幕。

![](img/a6c86a7689dc2d54e7264d1941d4b6f3.png)

8.展开“构建”菜单，然后单击“存储”。之后，点击开始按钮。

![](img/a051017891cebbfea748cae00333f7c3.png)

9.如果您选择在生产模式下启动，默认情况下，您的 flutter 应用程序将无法访问云存储中的文件。因此，让我们选择在测试模式下启动。该测试模式的安全规则允许您在接下来的 30 天内从您的 flutter 应用程序访问该文件。请注意，如果您愿意，以后仍然可以更改此安全规则。

![](img/e84592573a9a71d1c47f83b2a2017124.png)

10.现在，您需要为您的云存储选择一个位置。这是您的云服务器将被托管的地方。

![](img/33e73e3e920a5490adef5b2a1c286657.png)

11.最后，Firebase 将为您创建一个默认的 bucket，对于我的案例来说是[GS://tiktokclone 1234 . appspot . com](https://console.firebase.google.com/project/tiktokclone1234/storage/tiktokclone1234.appspot.com/files)。请注意，通过将文件存储在此默认存储桶中，您将只能获得 5GB 的可用存储空间。

![](img/a549c3b2ace447d16c80f678ff2c004f.png)

12.现在，让我们通过点击 Project Overview > Project settings，将您稍后将要创建的 Flutter 应用程序注册到 Firebase 项目中。之后，点击 Android 或 iOS 图标。

![](img/bca11f7a4ed97ed623a860c8730edf5c.png)

13.对于 Android，为应用程序指定一个包名，然后单击注册应用程序。之后，下载 google-services.json 文件，并将其放入您的 Android 应用程序模块根目录。这个 json 文件包含访问 Firebase 云存储的凭证。注册 iOS 应用程序的过程也是一样的。你可以按照 Firebase 控制台中给出的说明进行操作。

![](img/3a2d4ac1c85487a0d521fdbc11185c06.png)

# 创建颤振应用程序

14.启动刚才安装的 Visual Studio 代码，打开一个新的终端。

![](img/a06c0d484c165045c7f2a8bf2c558abd.png)

15.导航到你的开发文件夹，输入“flutter create-org<domain>T3”，用默认模板创建一个新的 flutter 应用。下面的命令将创建一个名为 com.tiktokclone 的 Flutter 应用程序。</domain>

![](img/db807fd10e2fb576e7212f5159d3afce.png)

16.点击左侧面板的“Explorer”图标，然后点击“Open Folder”打开刚才创建的 flutter app 开发文件夹。

![](img/28e9e3cf5f3eb4d30464221a2360ff4a.png)

17.如果一切正常，您应该会看到如下所示的 Flutter 默认模板的源代码。

![](img/9c28e7f1e8f869ca560bea66fb9e6523.png)

18.现在让我们安装一个名为 image_picker 的第三方插件。这个插件可以用来捕捉照片或视频，或者从图库中选择照片或视频。所以我们要用这个插件来启动一个录像机，然后捕捉一个视频。

![](img/a44ff5d41638aa7e740eeffc8dfc54a9.png)

19.flutter 默认模板在右下角有一个浮动的动作按钮。让我们改变按钮的功能。不要递增计数器，让它启动录像机。由于我们使用视频下载而不是视频流，我们需要将最长视频录制时间限制为 60 秒。在这里，ImageSource 是启动录像机的 camera，您可以将其更改为 gallery，以便从 gallery 中选择现有的视频。

20.现在让我们安装另一个名为 firebase_storage 的插件，从 firebase 云存储中上传或下载视频。您还需要安装 firebase_core 插件来初始化 firebase 插件。此外，您还需要将 google 服务添加到两个 Android 的 build.gradle 文件中。

![](img/0ec1d819ad91e2a634d3a5ede1ace175.png)![](img/621a5ff317f853af21b0ab4d8a02d4ac.png)![](img/a8cd1f958396b46134cabdab10266b93.png)![](img/5120dfacd9b1315c8092ed98321f7688.png)

21.我们需要安装视频压缩插件来压缩视频文件，然后上传到 Firebase 云存储。这可以使上传过程更快，也消耗更少的存储空间。在这里，您需要再次将视频剪切到 60 秒，以防视频文件是从图库中选择的，而不是录制新的视频。

![](img/22d47ee89ddf0c192d75fa57121fc00a.png)

22.之后，我们会将 mp4 视频上传到 Firebase 云存储。

23.构建项目时可能会出错。这是由于视频压缩插件需要更高的 Android SDK 版本 18。您需要将 minSdkVersion 设置为 18 at../android/app/build.gradle。

![](img/6bce573d4e89dd7b8fcbf71da258a457.png)

24.您可能需要在启用 multidex../android/app/build.gradle，如果您得到如下所示的错误。

![](img/c6a946c7c83df9b4d0f7ffc80aeff1da.png)![](img/93a66c02e87fa2b32891b22b7ac9df62.png)

25.现在让我们再安装三个插件:

*   抖音式滚动器
*   缓存视频播放器。
*   能见度探测器

类似抖音的 scroller 插件是显示视频列表的主用户界面，你可以通过上下滑动切换到下一个视频。对于缓存视频播放器，我们使用缓存版本的视频播放器来节省下载带宽。如果你以前看过视频，它会从你的设备缓存中检索视频文件，而不是一次又一次地从 Firebase 云存储中下载视频文件。这可以减少 Firebase 云存储的带宽使用。对于可见性检测器，当视频页面可见时，它将自动播放视频。

![](img/71fef83b8fade154610967ed558c349c.png)![](img/ec470f8c468c99b00f845a383af97744.png)![](img/8f1bc154b343b5c16985245f657529ee.png)

26.当应用程序启动时，从 Firebase 云存储的视频桶中获取所有视频 URL。

27.之后，加载并显示抖音式滚动条上的所有视频。video.dart 是为每个视频页面自动播放的视频 UI 类。

28.现在让我们构建源代码并测试您的 Flutter 应用程序。要将你的源代码编译成 APK 安装在你的 Android 手机上，你可以在你的终端中输入“flutter build apk”。然后，您可以从以下网址获得您的 APK 文件../build/app/outputs/flutter-apk/app-release . apk。如果出现如下所示的错误，您需要在您的../android/app/build.gradle 文件。现在让我们再次建设，你应该能够建立你的 APK 成功。

![](img/f4627b7cdd48b312af246a10de844431.png)![](img/14eb8fa7d530535af99222ce073fcc7a.png)

29.你可以点击下面的视频链接，看看这个 Flutter 应用程序是如何工作的，我已经上传了 3 个视频到我的 Firebase 云存储中。

[](https://youtube.com/shorts/AD8TUjJhD9s?feature=share) [## 如何创建抖音克隆或短视频 YouTube Flutter App

### 你有没有想过在你的平台上加入像抖音、YouTube、脸书或 Instagram 这样的视频分享功能？你…

youtube.com](https://youtube.com/shorts/AD8TUjJhD9s?feature=share) 

30.既然你已经知道了如何在 Android 平台上用 Flutter 创建一个抖音克隆应用或者短视频 Youtube 应用。你可以挑战自己，在 iOS 平台甚至网络上做同样的事情。由于 Flutter 是一个跨平台的框架，你的源代码应该已经支持 iOS 了。也许你只需要在 MacOS 中构建你的源代码。

# 结论

在本文中，您学习了如何使用 Flutter 和 Firebase 云存储创建抖音克隆或短视频 Youtube 克隆应用程序。然而，它只是向您展示了短视频共享功能的最基本功能。您可以挑战自己，添加更多附加功能，例如:

*   打开或关闭视频声音
*   下拉以刷新
*   从图库中选择并上传现有视频
*   从 Firebase 云存储中批量获取视频
*   Firebase 用户认证
*   过滤或阻止不良视频内容
*   等等

如果你想看看这个短视频分享功能的真实例子，你可以在 GroundWorm.com[访问我的应用的网页版](https://groundworm.com)，或者在 [Play Store](https://play.google.com/store/apps/details?id=com.groundworm.android) 下载安卓版。这款应用的 UI 设计更像是一款短视频 Youtube 应用，而不是抖音。GroundWorm 是一个基于位置的社区社交平台，在这里你可以分享照片和视频。欢迎你在那里创建一个视频帖子。

你可以在 [GitHub](https://github.com/koosoftware/tiktok-clone-flutter-app) 找到上述 Flutter 应用的完整源代码。

如果你觉得这个教程有用，请留下你的评论。如果你没有时间，请至少给我一个掌声，或者更好的是，按住你的鼠标按钮给更多的掌声，这是免费的！你的支持是我写越来越多内容的动力。谢谢你。