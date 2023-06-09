# 雪花雪景:炒作还是真实交易？

> 原文：<https://blog.devgenius.io/snowflake-snowsight-a-hype-or-a-real-deal-1342578abf7d?source=collection_archive---------2----------------------->

![](img/f9a3624f75836ed6fc316839bd13a0c2.png)

Snowsight 是 SQL 工作表的替代品，旨在支持数据分析师的活动。Snowsight 在新的雪花网络界面中可用。这仍在预览中。

# SQL 工作表与 Snowsight

SQL 工作表紧密集成在雪花 Web UI 中。这是一个用于雪花 DML 和 DDL 查询的文本编辑器和执行环境。下面的屏幕截图是 classic 控制台中的工作表。

![](img/9917e84550c9722ec0e949835ad22cfd.png)

单个工作表就像 web 浏览器中的选项卡一样被分隔开。顶部中间是 SQL 查询编辑器，下面是结果窗格。在左手边，有一个对象查看器。文本编辑器的右上角包含切换上下文的选项(即数据库、角色、仓库、模式)。

Snowsight 是雪花工作表经典控制台的视觉增强版本，带有快速图表。要打开 Snowsight，我们必须从功能区菜单角色中点击“预览应用程序”,如下所示。

![](img/7702630b7015c188c3641abf2f372b10.png)

**雪景方位(来源雪花)**

![](img/c43d3c9d4eed88183c3b66a1ef71a0af.png)

1.  在打开的工作表上执行操作:

*   将工作表移动到新的或现有的文件夹或仪表板。
*   复制工作表。
*   对工作表中的查询应用标准 SQL 格式。
*   删除工作表。

此外，您可以打开一个显示支持的键盘快捷键的对话框。

2.选择会话上下文(即用户会话的当前角色、仓库和数据库)。

3.在查询编辑器中编写和编辑查询。

4.在活动之间切换:浏览查询结果、创建图表和浏览模式。

5.创建新工作表、共享当前工作表或在当前工作表中执行查询。

6.打开以前版本的工作表。

# 演示

# **Snowsight Vs BI 工具**(来源:雪花)

**什么时候使用 Snowsight？**

对于熟悉 SQL 的人，在加载探索性查询的过程中进行数据验证。团队分享和探索的快速图表。

**什么时候使用 BI 工具？**

机构报告、业务用户探索、复杂仪表板、嵌入式 BI 应用程序。

# Snowsight 模式元数据刷新

Snowsight 中的模式元数据每 24 小时自动刷新一次。如果创建新表或向表中插入数据，或者在数据库中创建任何对象，模式浏览器不会立即刷新元数据。要手动刷新模式的元数据，请在模式浏览器中单击 **…** (选项)**刷新模式**。Snowsight 会快速刷新元数据，以便列出新对象并进行搜索。

![](img/c6c16d3aa04be217ff0bbed74b67f2e8.png)

# 调整大小或暂停虚拟仓库

在 Snowsight 中，我们能够直接从 Snowsight UI 中调整、暂停和修改仓库的缩放策略。

![](img/b81e3e8b1cf20a74f55d47192cc109d3.png)

# SQL 智能自动完成

与经典工作表相比，Snowsight 最吸引人的特性之一是它支持上下文相关的自动完成。

![](img/2cd952cf2025e3a125770ae0e54486a7.png)

# 自定义过滤器

帐户管理员(即具有帐户管理员角色的用户)必须授予每个角色 ***，包括帐户管理员角色本身*** ，创建自定义过滤器的能力。

**如何添加新的自定义过滤器？**

管理设置过滤器。

**如何在查询中使用过滤器？**

![](img/16c9fcb540d89ad4c7281f6decd115fc.png)

# 通过图表实现数据可视化

Snowsight 支持快速图表，帮助创建仪表板。您还可以与您的同事共享仪表板。

![](img/4eff4001d27c3158216beb146072e28f.png)

# 结论

我认为仪表盘很方便，也很酷。结合对 SQL 和领域专业知识的深入了解，用户无需使用外部 BI 可视化工具就能获得大量洞察力。

此外，您可以与同事共享您的仪表板。仓库大小调整，智能自动完成，自定义过滤器是自定义工作表顶部的一些非常好的增强功能，使 Snowsight 成为一笔好交易。

希望这个博客能帮助你了解雪景。如果你对此有任何疑问，欢迎在评论区提问。如果你喜欢这个博客，请鼓掌。保持联系，看到更多这样的酷东西。谢谢你的支持。

**你看了我下面的博客了吗:**

[SNOWPRO 自我评估工具](https://rajivgupta780184.medium.com/snowpro-self-assessment-tool-163e2a9805bd)

[从零到雪花中的英雄(2-3 周内获得 SNOWPRO 认证)](https://rajivgupta780184.medium.com/zero-to-hero-in-snowflake-snowpro-certified-in-2-week-8ec62cd89674)

**你可以找我:**

**跟我上媒:**[https://rajivgupta780184.medium.com/](https://rajivgupta780184.medium.com/)

**在推特上关注我:【https://twitter.com/RAJIVGUPTA780】T22**

**在 LinkedIn 跟我连线:**[https://www.linkedin.com/in/rajiv-gupta-618b0228/](https://www.linkedin.com/in/rajiv-gupta-618b0228/)

**订阅我的 YouTube 频道:**[https://www.youtube.com/channel/UC8Fwkdf2d6-hnNvcrzovktg](https://www.youtube.com/channel/UC8Fwkdf2d6-hnNvcrzovktg)

![](img/f5d39a229aefd3f4eb42587270bf2094.png)

#坚持学习#坚持分享#每天学习。

# 参考资料:-

*   [https://www.snowflake.com/](https://www.snowflake.com/)