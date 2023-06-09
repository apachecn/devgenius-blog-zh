# 来自数据安全英雄的智慧

> 原文：<https://blog.devgenius.io/wisdom-from-a-data-security-hero-16d4bf9dcc8c?source=collection_archive---------35----------------------->

我经常提到我在 2017 年碰撞大会上的首次亮相，这是我职业生涯迄今为止的一个亮点，也是有充分理由的。尽管与风投和其他网络建立了有价值的联系，我还是参加了与 EFF 执行董事辛迪·科恩的私人小组讨论。

在科技界，她绝对是我心目中的英雄之一。她参与了[乌布里切特诉美国](https://www.scotusblog.com/case-files/cases/ulbricht-v-united-states/)、[赫平廷诉 AT & T](https://www.scotusblog.com/case-files/cases/hepting-v-att-corp/) 和 [OPG 诉迪堡](https://en.wikipedia.org/wiki/Online_Policy_Group_v._Diebold,_Inc.)等案件，这只是她参与的几个知名度较高的案件。这是我有史以来关于技术的最好的对话之一，我认为这是我开始大数据技术之旅时值得重温的宝贵记忆。

![](img/f53d21ce5367897e244c57362b62cc8f.png)

今天，像 [Ban.jo](https://ban.jo) 、 [HiQ](https://hiq.com) 和 [Clearview.ai](https://clearview.ai) 这样的公司试图削弱第四修正案权利(以及其他权利)，并为此提供[可疑的理由。在 Ban.jo 的首席执行官 Damien Patton 被揭露为 1990 年三 k 党枪击犹太教堂事件的同谋的背景下，这一点变得更加令人担忧。](https://jolt.law.harvard.edu/digest/clearview-ai-responds-to-cease-and-desist-letters-by-claiming-first-amendment-right-to-publicly-available-data)

在人工智能领域，我们比以往任何时候都更需要关注我们工作的道德和存在意义。这就是为什么我在这里谈论我学到的关于防止国家窃取你的用户数据。其中一些观点是通过我自己的研究阐述的，但我肯定应该感谢辛迪将我的研究转向这个方向。

# 要点

**要求搜查令**

这个应该很明显，但是你的公司有公民自由。从地方治安官到中央情报局的警察机构必须使用授权系统才能在没有你明确许可的情况下访问你的数据。如果政府试图强迫你，请律师。

**传播你的数据**

作为 Tor 项目的董事会成员，辛迪对“数字安全”略知一二。使用时。洋葱网络对大多数企业来说有点过头了，对于那些开发分布式数据架构的企业来说，可以从中吸取教训。

例如，如果你把你的用户数据放在俄罗斯或日本等国家的美国用户那里，引渡命令和外国搜索请求很难执行，你就为窥探设置了一个巨大的路障。

如果你的后端支持它，将用户数据的碎片分布在不同大洲的服务器上，将使任何一个政府都几乎不可能窥探用户数据。就像超级富豪如何利用外国银行来规避美国的限制和税收。

如果你真的想走极端，为你的每一个服务器银行在其各自的司法管辖区申请一个公司，并确保每个地点都有利于你的法律。如果他们不得不处理伊利诺伊州、瑞士、冰岛和日本的隐私法，只是为了收集你的用户数据的不同元素，他们可能会减少损失，不再插手。

**加密一切**

如果你从研究[苹果与 FBI](https://en.wikipedia.org/wiki/FBI%E2%80%93Apple_encryption_dispute) 的历史中学不到什么，那应该是你不应该被要求在自己的产品中引入安全缺陷来支持国家监控。你的加密越强，你的论点就越有力，所以投资一个高质量的数据安全基础设施。

**用户条款和条件至关重要**

LegalZoom 模板很棒……当你刚开始的时候。一旦你的用户群大到足以引起注意，你就值得考虑写一些强有力的条款来保护你的用户免受像 Clearview 这样的第三方的攻击。

如果你在美国运营，伊利诺伊州生物识别信息隐私法是你的朋友，因为它自动给你至少一个针对抓取者的索赔，所以引用它的条款会有所帮助。尤其是如果你的公司或你的应用部门是在伊利诺伊州注册的，因为这让你能够声称伊利诺伊州是合同的管辖法律。

# **展望未来**

未经我们同意收集我们的数据对大多数美国人来说已经够可怕的了。不幸的是，当谈到人工智能的[伦理含义时，这只是冰山一角。](https://www.weforum.org/agenda/2016/10/top-10-ethical-issues-in-artificial-intelligence/)

我最大的担心之一是，国防部会采用类似 Clearview 的东西，然后添加一些“如果”语句和一些硬件接口到类似 [this](https://taskandpurpose.com/analysis/ai-weapons-artificial-intelligence) 的东西。如果你在想“该死，这就像一个字面上的天网”，你是对的。作为一个未来学家，当我们走向[奇点](https://www.newscientist.com/article/mg22930661-800-vision-of-singularity-questions-ai-intellect/)的时候，我不禁把它看作是[机器末日](https://www.youtube.com/watch?v=jHd22kMa0_w)的一个貌似合理的前兆。

幸运的是这还没有发生，如果我们作为计算机程序员一起工作，这就不会发生。如果你喜欢这篇文章，我强烈推荐你尽你所能支持像关注科学家联盟这样的组织。更重要的是，永远不要推送你知道是不道德的代码。如果你的技术领导要求你，就像斯诺登一样揭发他。