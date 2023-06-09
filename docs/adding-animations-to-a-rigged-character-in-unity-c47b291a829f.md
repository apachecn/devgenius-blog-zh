# 在 Unity 中给一个被操纵的角色添加动画

> 原文：<https://blog.devgenius.io/adding-animations-to-a-rigged-character-in-unity-c47b291a829f?source=collection_archive---------0----------------------->

## 使用 Mixamo 动画

![](img/3c10f2f51387244fa912a9fa345b3897.png)

Mixamo 是一个为你的游戏获取角色和动画的好地方。他们已经准备好使用角色，你可以上传一个模型，让它自动装配。他们也有运动捕捉动画，你可以使用任何人形装备的角色，最好是装备设置与他们的装备相同。

 [## 米夏莫

### 编辑描述

www.mixamo.com](https://www.mixamo.com/#/) 

我已经有一个角色可以使用 Mixamo 的动画。所以我不需要角色。目前他们有 3 页的字符。

![](img/6827ea4a4cea763316356b90355fb53f.png)

# 获取动画

他们有接近 2500 个动画，你可以从中选择，缩小范围的最好方法是使用搜索栏来搜索。

![](img/650020f9bf492fd48ad57a1afd806714.png)

我建议通过单词包搜索，得到一个符合你需求的动画包。你可以在左边的窗口预览。我想我会选择动作冒险套装，因为我喜欢跳跃/坠落的动画

![](img/2870b35aefa40b555a8c8a6336f5503f.png)

一旦你有了你想要的动画，就下载它。有几种不同的选择。我不需要一个角色，所以我把姿势设置为无角色(使用 T 型姿势或皮肤以获得更好的效果)，对于格式，我将使用统一的 FBX。

![](img/5b263800f5976d3d0adc9099ea87f810.png)![](img/7d117409a0d470765f6dcc9e31d7c442.png)

下载完成后，我将 zip 文件解压到我的项目文件夹中。

![](img/f40e0fef817ee7c64fb612b540b8b747.png)

接下来在 Unity 中，我确保将动画类型设置为人形。为了预览动画，我把我的角色拖到预览面板上。

![](img/10ebbeefa358af6b8e7bce3329ed8303.png)

# 使用动画

我需要创建一个可以在我的播放器上使用的控制器。

![](img/dc3610d9a55893d189858e63c70374c8.png)

现在我需要做的就是把我的动画拖到控制器上。

![](img/576be7301f59f6ae01f4192e43e54c9f.png)

角色空闲，但动画播放一次。为了解决这个问题，我需要编辑动画循环的时间。

![](img/5163491dc55afc0a52db7712985c60df.png)

# 根运动

动画带有根部运动。当我将动画速度设置为 1 时，玩家开始奔跑。

![](img/8b5f7b404d87b165a913b5d78a24d034.png)

如果我想让动画控制玩家角色的运动，这是很棒的，很多角色控制器都是这样做的。

![](img/d3618bd78244f8c6df1aea74fb1004bd.png)

这不是我想要的行为。我希望从行为中控制一切。动画师将只用于显示动画。

要解决这个问题，我有两个选择。一种选择是回到 Maximo，通过选择“就位”选项下载我想要使用的动画。下载包时，此选项不可用。

![](img/fe7a8aad119bc6cafc6ef2e737a430c0.png)

通过这个动画

![](img/b9cab23e0d1919a8612052dcc6df96ab.png)

当然，我必须将装备设置为人形，动画设置为循环。

![](img/21a69eb20eaf4cac53bd94d341cb2afc.png)

另一个选项是设置动画不应用根运动。现在，即使动画中有根部运动，它也不会影响我的角色。这就是我想要的。即使我选择下载没有应用根运动的单个动画，我也可能有一些带有根运动的动画，比如空闲动画。另外，我不必下载每一个单独的议案。

![](img/94077536ae9307c8cf87054c0b7db9a6.png)

# 控制动画师

现在我需要做的就是在玩家移动的时候把这个信息传递给动画师。为此，我将为动画和 [**脚本对象变量**](/script-communication-in-unity-using-scriptable-objects-ad2ef0d99c59) 使用单独的行为。我使用包管理器 安装了我的 [**核心框架**](/creating-custom-packages-for-use-in-unity-7dfbaa49e4b4)

我将玩家动画组件添加到玩家模型中。

![](img/1addb78bf4c813f0fdffe3d89dfddccf.png)

我需要一个给动画师的参考来传递需要的信息。

现在我的动画器中唯一的参数是速度浮动，当我添加更多的动画时，我会添加更多的参数。我必须使用 ScriptableObject 引用的值来设置动画师的速度浮动。

![](img/6f4ed76f0fe8228ddd30ca98137e6f1b.png)

我创建了我的播放器速度变量，并将其添加到播放器动画组件中。

![](img/5f89ee3621b2af23c2ea0d9c085af613.png)

现在，更改变量的值会使动画师播放正确的动画。

![](img/b9fc4209d45794ed0cffa0a0a104c229.png)

现在我需要在玩家行为中设置这个值。我将它设置为移动方向的绝对值，因为动画师正在寻找一个大于 0.1 的值来切换到正在运行的动画，并且输入被设置为-1，0，0r 1。

![](img/305ef221fa9163cd5f77e81e71ef2c96.png)

在检查器中设置参数后，当我移动时，我的播放器现在播放正确的动画。

![](img/a60c26740be0f88e9485356eb130bb0e.png)

# 跑步、跳跃和空闲的动画

我完成了控制器。如果跳转为真，它将从任何状态跳转到运行状态。I 跳跃时根据速度切换回怠速或运行为假。

![](img/e802c511d360fce370b501ceb1b8164d.png)

## 这些行为

在玩家动画行为中，我添加了设置:如果跳转引用的值改变，动画师会跳转。

![](img/b8606e80ec117273d5b919e531c09e69.png)

在玩家行为中，如果控制器接地，我将 Bool 引用设置为 false，如果玩家跳跃，我将它设置为 true。

![](img/9c5896e348d3e197b6c9f8c8e87f9bb7.png)

现在我的玩家可以在游戏中正确地跑和跳了。

![](img/bd43e41f5234d05fda4b91501c8c69ee.png)