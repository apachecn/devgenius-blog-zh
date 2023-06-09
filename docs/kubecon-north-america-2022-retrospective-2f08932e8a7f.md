# KubeCon 北美 2022 回顾展

> 原文：<https://blog.devgenius.io/kubecon-north-america-2022-retrospective-2f08932e8a7f?source=collection_archive---------3----------------------->

![](img/665b7bbfebd0a77f30609fc73f237888.png)

底特律。Adri Villela 的照片。

***同*** [***阿娜玛格麦地那***](https://www.linkedin.com/in/anammedina/)

各位库伯内特书呆子好！🤓KubeCon North America 现在已经落后了，所以是时候进行会议回顾了！现在，你们一定在想，“啊，不会又是一个吧！啊，但这不仅仅是一个 KubeCon 总结，因为我和 Ana 将分享我们的观点，我们很棒，你们都喜欢我们。阿米利特？我当然是。事不宜迟…

# 阿德里亚娜的观点

如果有任何会议在我的会议清单上，那肯定是 KubeCon。我对 Kubernetes 又爱又恨(我们不都是这样吗？)，和[花了几个小时试图理解它的狡猾方式](https://adri-v.medium.com/list/kubernetes-090db256e52b)，并在又一次 [CrashLoopBackOff](https://stackoverflow.com/questions/41604499/my-kubernetes-pods-keep-crashing-with-crashloopbackoff-but-i-cant-find-any-lo) 中诅咒我的终端。所以去 KubeCon 和书呆子在 Kubernetes 听起来很棒。

我终于有机会参加了在密歇根州底特律举行的 2022 年 KubeCon 北美大会(T21)。

![](img/5dca99c91e1418ae5096d9c3e8843e92.png)

底特律市中心的拼贴画。Adri Villela 拍摄的照片。

我非常兴奋能参加这次会议，原因有几个。

1.  这将是我第一次见到我的 Lightstep DevRel 团队，看看我是不是这群人中最矮的。剧透:安娜和我是最矮的，大约 5 英尺 3 英寸(我的身高是 161 厘米)。拉丁基因。我随波逐流。
2.  这是我作为开发者的会议记录。各位，这是我的第一个 DevRel 角色，如果你们能相信的话——6 个月了，我很喜欢！
3.  上一次参加会议是 2018 年多伦多 DevOps Days。最精彩的是让[妮可·福斯格伦](https://nicolefv.com)博士和[杰斯·亨布尔](https://research.google/people/106958)(两人都因[朵拉](https://www.devops-research.com/research.html)成名)在他们的书《T8 加速的硬拷贝上签名，这样就不会太寒酸了。PS:拿书。额外收获:如果你拿到有声读物，它是由妮可朗读的。

所以，废话少说。这是我的 KubeCon 总结，新手版！

作为一名对 COVID 持谨慎态度的女性，我很高兴地看到 [CNCF](https://www.cncf.io) 采取了各种 COVID 预防措施，包括疫苗要求或阴性 COVID 测试以挑选您的徽章，并且要求并强制执行掩蔽。各种 COVID 预防措施到位。首先，你需要疫苗接种证明或阴性 COVID 测试证明才能领取徽章。在场馆内，掩蔽是必需的，而且是强制性的。我总是在室内戴口罩(没有例外)，所以我在人群中肯定感觉更自在，因为知道我们有这些保护措施。我非常感激的另一件事是，CNCF 提供免费的[快速 COVID 测试](https://www.globalpointofcare.abbott/en/product-details/navica-binaxnow-covid-19-us.html)通过 [eMed](https://www.emed.com) 监督，所以我能够在那里每天测试，以获得额外的安心。

虽然 KubeCon 本身直到 10 月 26 日星期三才开始，但我在星期天晚上飞过来，以便能赶上星期一的[开放观测日](https://events.linuxfoundation.org/open-observability-day-north-america/program/schedule)，以及星期二的 [OTel 不插电](https://www.eventbrite.com/e/otel-unplugged-kubeconcloudnativecon-detroit-2022-tickets-427595037267)。

## 第一天:开放观察日

我在[开放观察日](https://events.linuxfoundation.org/open-observability-day-north-america/program/schedule)匆匆进出，在我听到的演讲中，有两个演讲我非常喜欢。一个是丹尼尔·金和李斯·李的《T2 教我如何建立一个可观测的数据管道》。尽管我已经熟悉了内容，但我真的很欣赏丹尼尔和里斯超级充满活力的演示风格。这绝对是一种受欢迎的提神饮料，有助于对抗午餐后的食物昏迷。另一个我很喜欢的演讲是【eBPF 能为现代的可观测性做些什么？作者 Ori Shussman 。在这篇文章中，他谈到了 eBPF 如何让我们看到原本看不到的数据。例如，eBPF 有助于提供对 gRPC[调用的更深入的了解，这是众所周知的难以观察的。🤯我还想对利比·梅伦的《打开可观察性之门》一书特别欢呼。虽然我错过了这次演讲，但这个话题对我来说非常近，因为在我以前的角色中，我不得不花大量的时间来尝试以正确的方式进行可观察性。](https://grpc.io)

有兴趣看看其他的演讲吗？你们可以在这里查看他们的视频。

![](img/34d947a6173f0c969d48f0996561b23e.png)

在开放观察日的演讲。Adri Villela 拍摄的照片。

那天下午晚些时候，我在现实生活中见到了我的 Lightstep DevRel fam，这太棒了！可惜我们从来没有集体自拍过。😿

## 第二天:OTel 不插电

我在[殖民地俱乐部](https://www.weddingwire.com/biz/colony-club-detroit-detroit/68e394fe233e346c.html)度过了第二天，去参加 [OTel 不插电](https://www.eventbrite.com/e/otel-unplugged-kubeconcloudnativecon-detroit-2022-tickets-427595037267)。本次活动由[轻步](https://lightstep.com)、[蜂巢](https://honeycomb.io)、[新遗迹](https://newrelic.com)、 [Splunk](https://www.splunk.com) 、 [Dynatrace](https://www.dynatrace.com) 、 [Crowdstrike](https://www.crowdstrike.com) 、 [NGINX](https://www.nginx.com) 赞助。我参加活动时不知道会发生什么。当我和不认识的人在一起时，我有时会闭嘴，但因为我在帮助活动签到，我不得不和一些与会者打招呼，这有助于打破僵局。事实证明，我在 OTel 社区的工作中认识了很多名字，与之前只在 Slack 或 Zoom 上见过面的人面对面交流也很不错。

![](img/fbcee5bb1f78f41a7cf58d7431422c44.png)

不插电的 OTel 照片拼贴。Adri Villela 拍摄的照片。

PS:大呼到会场，很华丽，工作人员超级友好。

## 第三天:KubeCon！

最后，重头戏！周一我去了会议中心拿我的徽章，但那天的人流量甚至比不上周三的繁忙程度。这是一个旋风般的一天，我花了一些时间在 Lightstep 展台。Lightstep 的工作人员做了 OTel 演示应用程序的演示，以说明[可观察性-景观-代码在起作用](https://lightstep.com/blog/observability-as-code-with-kubernetes-and-lightstep)，这[和](https://twitter.com/Ana_M_Medina)我倾注了我们的鲜血、恐怖、恐惧、汗水和(快乐？)在 KubeCon 之前泪入其中。这是一个很棒的小演示，如果我自己这么说的话，我绝对推荐你去看看。(不要脸的塞，我知道。抱歉不抱歉。)

![](img/ece11cf1d18314a167bd6d990d09abad.png)

KubeCon 的 Lightstep 展台照片拼贴。

在我们的摊位上，真人大小的叠人龙游戏非常吸引人，有很多喜欢冒险的人都尝试过。下面我和安娜的照片显示了这座塔有多高。你没看到的是，在照片拍摄后不久，我们中的一个人推倒了这座塔。哎呀。😳

我们的团队还特别为这次活动制作了 KubeCon-Detroit 主题的贴纸。安娜把事情发展到了一个新的水平，她做了指甲，以配合我们的贴纸。我不知道你是否能在下面的照片中看到它，但她也戴着 Kubernetes 主题的耳环。她很特别，我喜欢！这些贴纸是寻宝游戏的一部分，该游戏揭示了周四晚上由 Lightstep 主办的披萨派对的地点。

安娜和我还花了一些时间在参展商区闲逛，拿了一些可爱的东西(我买了一件可爱的 OTel t 恤和最可爱的小[tracestest](https://tracetest.io)plus HIE，我给它取名为 Tracey)，结识了新的有趣的人，并在现实生活中见到了一些熟悉的面孔。(嗨[艾比](https://twitter.com/a_bangser)！！)啊，一个 DevRel 的生活。所以。很多。好玩。💜💜💜

![](img/6d342f57dfbfacdcbaa1f8c105a9ccf1.png)

KubeCon 的照片拼贴

不幸的是，我没能参加完整的会议，但从我的经历来看，这很有趣。这绝对不会是我的最后一个 KubeCon，我绝对不能等待下一个 KubeCon！带上它！

![](img/aefab620a80f34656f9cbeeaad8fda3f.png)

图片来源[此处](https://media.self.com/photos/57d8a21b46d0cb351c8c558e/master/pass/bring-it-gabrielle-union.gif)。

# 安娜的观点

我是安娜。我想提供我过去参加过四次 KubeCons 的观点。这是我第二次通过 COVID 参加 KubeCon，我很感激 CNCF 在他们的活动中执行 COVID 协议。作为在 KubeCon EU València 期间感染 COVID 的人，我这次格外小心，每天都进行测试。我还在测试，COVID 阴性，所以谢谢你，CNCF！

周一，我被安排去参加贡献者峰会，但我在一周前的周四失去了声音，到周一早上我仍然没有恢复。🥲:在接下来的一周里，我有很多讲座和展位工作，所以我做了一些更轻松的事情，我只是帮助我的同事们为 KubeCon 做准备，并对我的幻灯片做最后的润色。

今年真正困难的一件事是有太多(或者我觉得太多)的同地/第 0 天活动。很高兴看到生态系统继续增长，但这无疑使我们很难决定参加哪些活动，以获得向社区学习的机会。我知道我在这方面很挣扎，所以我真的希望下次我们能更好地统一话题。

周二，我在混乱日(T0)、T2 社区日(T3)和同时举行的活动的走廊轨道之间分配时间。在过去 4 年多的混沌工程社区工作中，我喜欢看到[云原生混沌工程社区的成长](https://twitter.com/Ana_M_Medina/status/1584958979767402496)，我也喜欢与人们谈论 [Keptn](https://keptn.sh) 的未来，并就如何通过这个 CNCF 沙盒项目和其他 OSS 工具实现更高的可靠性发表演讲。

随着周三的开始，感觉到人们如此渴望学习和联系的兴奋和激动真是太好了。从第一天的主题演讲中，我很欣赏这一提醒，即受益于 Kubernetes 和 CNCF 生态系统的公司应该参与进来，回馈社会，并指导他人。生态系统中有很多对维护者和贡献者的爱，作为 Kubernetes v1.25 和 v1.26 的 [Kubernetes 发布团队](https://github.com/kubernetes/sig-release)中的一员，看到我和团队的其他成员一起出现在那里是一种巨大的荣誉！💙

![](img/8b964955a864657b23fd72dabb5ac233.png)

Kubernetes 贡献者。Ana Margarita Medina[摄影。](https://www.linkedin.com/in/anammedina/)

我还花了一些时间逛了逛展厅，买了一些 CNCF 的赠品，也查看了一下供应商的赠品。

周四又是忙碌的一天，与社区一起四处奔波。我还用西班牙语录制了一些原生的云内容，还有一些其他的拉丁语内容。除此之外，Lightstep 还举办了两次活动，其中一次是我们的秘密披萨派对。接管底特律著名的小巷 [The Belt](https://www.thebelt.org/about-the-belt) ，闲逛并谈论 SRE 是一件有趣的事情。感谢所有路过的人！#底特律🤘

![](img/90be073b4c40c207021c9ac1c3a7881f.png)

Lightstep KubeCon 披萨活动照片拼贴。

我在 KubeCon NA 呆了很长时间的另一个地方是 CNCF 项目馆。我很高兴看到它比我们在 KubeCon EU 期间的面积大了一点，但我仍然希望它能更大一些，不要那么藏在角落里。一周以来，许多摊位都在展示他们的项目，主持问答时间，并赠送礼品。如果你仍然试图了解云原生生态系统，你可以看看这张[非常广泛的地图](https://landscape.cncf.io)CNCF 下的景观和项目，其中一些比其他的更先进。当然，我有偏见，但我真的为 [Keptn](https://keptn.sh) 在帮助开发者更好地控制他们的应用程序生命周期方面所做的工作感到兴奋。我也非常期待看到[后台](https://backstage.io)的走向以及其他 CNCF 项目如何与他们的服务目录相结合。

周五，我有机会和我的社区朋友一起出去玩，并和我们的朋友在 Dynatrace 做了一个关于 Keptn 未来的演讲。我非常兴奋地看到这个项目的进展，以及我们继续用 OpenTelemetry 做什么工作，以便更容易地观察我们的部署及其可靠性。

![](img/cb8d8d844289d472a9c623ad6cc8bf92.png)

在 KubeCon 继续谈。照片由[安娜玛格丽塔麦地那](https://www.linkedin.com/in/anammedina/)拍摄。

# 最后的想法

啊…就这样结束了！KubeCon 对我和 Ana 来说都是一大乐趣。我们喜欢第一次与 Lightstep DevRel 团队面对面，我们喜欢与我们的各个 CNCF 社区、Lightstep 客户联系，看到所有酷的技术非常有趣。无论你是像我一样的 KubeCon 新手，还是像 Ana 一样的 KubeCon 老手，很高兴看到 CNCF 社区继续团结、发展和繁荣。我们绝对期待 2023 年的 KubeCon EU！

现在，请欣赏这张阿德里亚娜的老鼠菲比的照片，她在做她的 KubeCon 费用报告时陪伴着她。

![](img/82fd38462d9478721bd28fc011d1cc7e.png)

菲比这只老鼠在我的笔记本电脑旁闲逛，而我却在做 KubeCon 的开销。Adri Villela 拍摄的照片。

和平、爱和准则。🦄 🌈 💫

对可观察性有疑问吗？告诉我们！请随时通过[电子邮件](mailto:devrel@lightstep.com)与我们联系，或者:

*   在 [Twitter](https://twitter.com/adrianamvillela) 或 [LinkedIn](https://www.linkedin.com/in/adrianavillela) 上与 Adriana 联系
*   在 [Twitter](https://twitter.com/Ana_M_Medina) 或 [LinkedIn](https://www.linkedin.com/in/anammedina) 上与安娜联系。

希望收到你们的来信！

【https://lightstep.com】最初发表于[](https://lightstep.com/blog/kubecon-north-america-2022-a-retrospective)**。**