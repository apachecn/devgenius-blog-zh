# 我太老了，受不了这些垃圾了…

> 原文：<https://blog.devgenius.io/im-getting-too-old-for-this-crud-dff71455edc3?source=collection_archive---------7----------------------->

如果这个标题听起来有点熟悉，不要担心，因为这个引用确实是有意的。虽然在谷歌上简单搜索一下就能发现，20 世纪最后 30 年有几部电影可以引用这句话的某些变体，但《致命武器》系列是我个人的灵感来源。非常有趣和娱乐性的电影，如果你有心情沉迷于一些不需要太多脑力的动作和喜剧，我强烈推荐。我跑题了…

“CRUD”这个缩写词除了是引用众所周知的电影台词的一种 PG 友好方式之外，本质上与访问数据有关。

c:创建
R:读取
U:更新
D:删除

那么，这到底意味着什么呢？就个人而言，当有例子时，我倾向于更好地理解概念，所以让我们在这里放一个“例子”。比方说，如果你正在使用一个 web 应用程序来查询你所在地区的天气，或者因为你想吃墨西哥卷饼而寻找附近的墨西哥餐馆，你将从一个数据库中访问信息。上传你自己的照片到网上相册*创造了*一个新的附加物，它(有希望)在未来持续几天、几个月或几年。浏览记录片列表是可能的，因为代码是*读取*该信息并将其呈现在你面前。改变你的关系状态意味着你在*更新*你在“那个叫什么的”欺骗你之前保存的先前状态。决定*删除*前一天晚上拍摄的你拍摄身体照片的快照会将证据从之前储存的地方移走…某种程度上。让我们面对现实吧，无论你是否点击了方便的垃圾桶图标，你都有办法访问你在网上发布的任何东西。

作为开发人员，这些数据要么在应用程序的后端处理，要么通过第三方访问。无论哪种方式，都可以通过应用程序编程接口(API)进行通信，从那里，我们可以利用这些信息做的事情几乎是无限的。在 React 中工作时，需要考虑的下一件事是如何在数据返回时存储数据。这可以通过利用 Redux(一个状态管理工具)或本地的*状态*来完成。我将在这篇文章中讨论后者。

你能想出一次你点击一个链接，一篇文章或一个视频，你短暂地发现某种类型的指示器显示内容正在加载吗？这是有目的的，使用了*状态*。在这种情况下，它向用户显示他们的请求正在被处理，并且不要气馁(虽然当这样说时，我回到了拨号上网的日子，天哪，这是你的一些观点)。为了提供一个视觉效果，我将根据我出色的项目合作伙伴提出的主题编写一些代码，作为我们本周提交的主题。以下所有片段的主题都是令人讨厌的可爱小猫。不客气

正如我前面提到的，无论您对数据做什么，都需要首先将它存储在本地 state 中进行处理。暂时忽略“useEffect”。我们很快会回到这个话题。

![](img/45f15c1fc46dddc1bc133c04710c62c0.png)

比方说，我想在页面上呈现一些组胺的可爱球的照片。在适当组件的函数中，我需要做的第一件事是为数据声明一个状态。如果我获取一个对象数组，每个对象中有一只猫的图像，可能是这样的:

![](img/fde69cb00968f2e47a10a63725cac257.png)

我们将初始状态设置为空数组，为数组中的元素做好准备。在继续之前要记住的是，在 React 中，我们应该利用 *useEffect* 钩子在我们的组件中执行一个副作用。在本例中，我想获取 cat 数据，并最终将其呈现在页面上。

![](img/2e1540f6cc3d5c9dbfb6a3d6e6e6bb4e.png)

在我非常有限的编码经验中，方法的名字并不总是与它们的用途一致。 *Fetch* 是一个完美的例子。事实上，我们正在从存储数据的任何地方获取数据。这个步骤后面有几个不同的方法，但是它默认为 *GET* ，这正是我们在这个例子中想要的，因此我不需要指定一个方法( [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch) 有一篇很棒的文章介绍了这一点以及更多)。

在上面的代码片段中，最终结果是使用一个 setter 函数，实际上，*将我们之前指定的“猫”的状态设置为从 fetch 中获取的数据。接下来，我们将把数据传递给负责呈现图像集合的组件。*

![](img/44e0b0d4728e7618d6c1790b269b0773.png)

然后，在该组件中，我们将它传递给负责渲染画廊中每只猫的子组件。除了个人偏好之外，实现这一点的方式还取决于数据结构本身。在这种情况下，我使用。map 迭代数组中的元素，并将 cat prop 传递给 card 组件。

![](img/7fa43a5922331b500c4a9741156e120a.png)

接下来，只需决定如何显示数据。带上道具，渲染你所关注的特定数据。

![](img/5d14ccca5fba1a560b2082462fe7e0a3.png)

由于我要演示的内容，我在上面的例子中没有使用 *alt* ,但是请尽量在你的代码中包含它，并详细解释图像所显示的内容，以便任何访问该页面的视障人士能够理解所显示的内容。例如，下面图像的 alt 文本将清楚地显示为“草地上一只诱发糖尿病的可爱的小印花布小猫，正如她公正的母亲所宣称的那样”。

![](img/7553aa366a357665bf5840227536c917.png)

这仅仅包括了*阅读*获取的数据，一个开始这次冒险的缩写字母。这只是对 CRUD 的一个方面的简单介绍，但是我觉得掌握它对于着手更复杂的工作是必不可少的。如果你能理解这背后的逻辑，那么你就成功了。当然，这里需要记住语法和额外的参数，或者改变方法，但是我个人认为获取数据的核心在于遵循这个基本流程。

这个总结也提醒了我自己，在试图冲刺到地平线之前，先走一步。我最终会到达那里，最好穿上鞋，最好涂上一点防晒霜。