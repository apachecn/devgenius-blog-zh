# 如何为你的扑克应用创建一个 Rails API！

> 原文：<https://blog.devgenius.io/how-to-create-rails-api-for-your-poker-app-a68c1eb4327c?source=collection_archive---------10----------------------->

![](img/6b8888d61d1cb3cd9e5582bf4e57e90d.png)

口袋 a！

对于这篇博文，我想谈谈为玩扑克(德州扑克)创建一个 Rails API。

我一直在尝试创建一个 React/Rails 应用程序，允许人们实时聊天和玩扑克。我希望能为 poker 数据库找到一个 gem 或 GitHub repo，但是我找不到一个只支持 Rails 的 API，所以我自己创建了这个数据库。

分解扑克游戏的玩法既有挑战性又很有趣；下面是我如何将用户和游戏数据持久化到 Rails 数据库中的。

*   我发现[这个回购](https://github.com/dilshanraja/Texas-holdem)对扑克游戏的一些逻辑很有帮助。它类似于我正在尝试制作的应用程序。
*   [这里的](https://github.com/atribecalledarty/console-poker)是 GitHub 的完整项目。
*   [扑克规则的全部细节。](https://www.888poker.com/en/texas-holdem-poker-rules.pdf)
*   [Holdem gem](https://github.com/Jberczel/holdem) 比较扑克手牌。

# 首先是模型和属性。

我们有三种不同的模式:**游戏**、**回合、**和**用户**。

用户玩一个由许多回合组成的游戏。扑克的主要逻辑包含在回合模型中—回合模型负责处理游戏的状态。

关联:用户模型同时属于游戏和回合模型。游戏和回合模式都有很多用户。

*注:我将使用术语“* ***下注回合*** *”或“* ***阶段*** *”来指代一个阶段，即翻牌前、翻牌圈、转牌圈和河牌圈，而“回合”将用于指代整个扑克回合。*

以下是我们需要的用户模型和倒圆角模型的属性:

## 用户模型

*   **round_bet** = >这样我们就可以跟踪用户每轮下注(即翻牌前、翻牌圈、转牌圈、河牌圈)的当前下注金额
*   **筹码** = >用户拥有的总筹码
*   **玩** = >他们是在当前手牌还是已经盖牌？
*   **牌** = >用户的两张牌(孔牌)

## 圆形模型

*   **_ playing**=>一轮开始了还是结束了？
*   **状态** = >一个状态消息数组，这样我们就可以很容易地访问游戏的流程(例如“翻牌…，轮到玩家 1…，等等)。)= > *我在我的应用程序中使用这个属性来轻松地向客户端显示游戏状态。*
*   **small_blind_index** = >游戏的小盲注指数，用于确定每个下注阶段第一个下注的玩家。*(我希望能够指定每轮新扑克的开始玩家，这样我就可以轮流开始每场游戏的小盲注玩家)。*
*   **轮到谁了？**
*   **锅** = >当前锅
*   **highest _ bet _ for _ phase**=>跟踪当前一轮下注的赌注
*   **社区 _ 牌** = >社区牌(翻牌、转牌、河牌)
*   **all_in** = >有人全押了吗？— *我不想处理对分彩池，所以当有人全押时，就不允许再加注了。让我知道，如果你有一个雄辩的解决方案分裂锅。*
*   **no _ players _ for _ phase&turn _ count**=>(no _ players _ for _ phase 表示一个阶段的玩家人数)。我们使用这些来确保所有玩家都在给定的一轮下注中下注

# 创建游戏逻辑:

在我们开始运行扑克游戏之前，这里有一些关于德州扑克结构的信息。**扑克**共有四轮下注:前翻牌、**翻牌**、**转牌**和**河牌**。**在每轮下注中，行动从“小盲注，**”开始(在翻牌圈，盲注后面的人开始下注)。然后，**每个玩家走一步，直到每个玩家都有机会下注**。**在一轮下注结束之前，每位活跃玩家必须已经下了与该轮下注的最高赌注相等的赌注**。例如，如果最高赌注是 400 英镑，那么在一轮下注结束之前，每个没有弃牌的玩家都必须投入 400 英镑。

****一场扑克游戏只能以两种方式结束:所有下注回合都已结束，或者除了一名玩家之外所有玩家都弃牌**。因此，在每个玩家的回合之后，我们将检查这些条件中的任何一个。我们还会在每一轮结束后查看一个下注阶段是否结束，以开始下一个阶段。**

## **每个玩家回合后要检查的条件:**

1.  **除了一个玩家，其他玩家都弃牌了吗？= >给最后一名玩家奖金**
2.  **最后一轮下注结束了吗？= >执行摊牌=决定赢家并分配奖金**
3.  **当前一轮下注结束了吗？= >开始下一轮下注**

**这基本上是整个游戏流程的逻辑。我们只需开始游戏，发牌(我们稍后会讨论如何处理牌)，收集盲注，然后等待玩家的行动。每回合后，我们检查回合属性和玩家属性，以确定游戏的状态。**

# **圆形型号代码:**

## **常数:**

**阶段:0 = >翻牌圈，1 = >翻牌圈，2 = >转牌圈，3 = >河牌圈。**

**盲注被硬编码为 200 和 400。**

## **我们将需要的方法:**

*   ****轮到** = >轮到谁了？**
*   ****active_players** = >未折叠的用户数组(按 id 排序)**
*   ****access_community_cards**=>游戏开始时，所有的社区卡(五张)都会被分发，access _ community _ cards 用于确定当前阶段有哪些卡可用。(卡片将采用“`Ac 7d 4c Td Qc".`”格式)。**
*   ****阶段 _ 完成了？** = >要不要进入下一个投注阶段？
    由两个条件决定:
    1)回合数(turn _ count)>no _ players _ for _ phase(表示每个人都获得了下注的机会)
    2) **players_have_bet？** = >所有玩家的回合赌注等于当前赌注或最高 _bet_for_phase**

# **开始**

**当回合开始时:**

*   ****为用户设置所有相关属性**。
    *注意:在我的应用程序中，在一轮开始时，该轮将有权访问它的游戏，而游戏也有权访问它的玩家。当回合开始时，我需要抓取游戏的玩家，并将每个玩家的 round_id 设置为回合。***
*   **将 **is_playing** 设置为真。**
*   **然后，**摆牌**和**开始第一轮下注**。**

# **套装 _ 卡片**

*   **添加状态。**
*   ****发牌社区牌和发牌玩家牌**。我们使用格式' *Ns，'*来表示一张牌，其中 N =数字，s =小写字母。稍后，我们使用宝石“holdem”来决定使用这种形式的最佳手牌。参见[‘holdem’自述](https://github.com/Jberczel/holdem)查看手部构造和对比细节。**

# **开始 _ 下注 _ 回合**

**调用 start_betting_round()开始每一轮下注(翻牌前、翻牌圈、转牌圈和河牌)。**

*   **添加下注回合状态的案例陈述。**
*   **将活动用户的“ **round_bet** ”重置为 0。记住 round_bet 是用户对下注回合的下注。**
*   **设置 **no_players_for_phase** 。(该阶段的玩家人数)**
*   **重置当前下注(**最高 _ 下注 _ 相位**和**回合 _ 计数**)。**
*   **并设置**转位**。(每轮下注期间，small_blind_index 开始动作。)**
*   ****如果 phase == 0(翻牌前)，为前两名玩家下盲注。****

# **user . make _ move & round . make _ player _ move**

**在我的应用中，**“移动”是由轮到它的玩家做出的，而不是回合本身。我认为这个架构作为游戏的隐喻更有意义。**玩家在游戏中出招。******

****user.make_move('call')** 是我们向回合提交移动的方式。这将调用回合方法**make _ player _ move(‘call’)。****

**… make_player_move:**

****next_turn()** 通过递增 turn_index 和 turn_count 来设置下一轮。*注意:接受 blinds 布尔值，当 blinds = true 时，不会增加 turn_count。***

****make_player_move()** 带三个 arg，两个可选。**

**(1)命令名，(2)加注量，以及(3)加注 Blinds 布尔值。**

**例如 make_player_move('raise '，SMALL_BLINDS，true)
例如 make_player_move('fold ')**

***我们需要 blinds boolean，这样当前两名玩家在翻牌前自动加注盲注时，这些“移动”就不会算作回合。请记住，在翻牌前，“第一个”下注的人是盲注之后的人。***

**然后，我们对每种命令类型都有一个 if-else 语句。**

**最后，**这里是控制游戏流程的东西:**在每一个回合之后，我们检查(1)游戏是否结束了？或者(2)下注阶段结束了？**

1.  ****除了一个人都折了？** **如果有，end_game_by_fold。****
2.  ****投注回合结束？** **如果是，调用 initiate_next_phase** 。**

****initiate _ next _ phase()**=>如果有人全押，或者如果当前阶段是最后一个阶段，则进入“**摊牌**”，这是玩家手牌的对决，并决定赢家。否则，开始下一个投注阶段。**

**为了缩短这篇博文，我不会去实现每一种移动。**

**[*这里是*](https://gist.github.com/atribecalledarty/8b016826c07fac1b4a62ded2e200cbb4) *对每个命令的完整 make_player_move 方法。***

**有几件事要注意:**

*   ***当最后一个被索引的人弃牌时，我们需要将 turn_index 重置为 0。***
*   ***确保“叫牌”、“检查”和“加注”动作有效。***
*   *****确保所有玩家都能负担得起任何人可以加注的最高金额****——我们这样做是为了避免底池分裂。***
*   ***在“跟注”和“加注”期间，检查玩家是否全押(因为在下注阶段结束时，如果有人全押，我们就会摊牌。)***

# **摊牌**

## **1.确定获胜玩家:**

**为了确定获胜的玩家，我们需要一组最好的手牌和最好的玩家。**

**迭代剩余的玩家:**

1.  **使用玩家卡和社区卡创建一个 Holdem::PokerHand.new。
    **注意:包含在 Gemfile** `**gem ‘holdem’**` **和** `**run bundle install**`
    *构造器从字符串创建一手牌，例如“4c Kc 4h 5d 6s Kd Qs”
    你可以比较两个不同的手牌>、<或==。* [*查看文档*](https://github.com/Jberczel/holdem) *了解更多详情。***
2.  **如果该玩家是第一个玩家，则将他们和他们的手牌添加到最佳玩家和最佳手牌中。**
3.  **将每个人的手牌与当前的最佳手牌进行比较，并添加或重置最佳手牌&最佳玩家。**

**花点时间理解这里的逻辑。我们最终拥有一批最好的手牌和最好的玩家。**

## **2.分配奖金并结束游戏**

**用于添加状态消息的 if 语句。**向赢家支付底池奖金。**最后，**设置 is_playing = false。****

**最后，我们成功了！我们可以成功地玩完一整轮扑克，每个玩家的走法都保存在数据库中。**

**一个简单的用法示例:**

**我们并没有真正谈论状态信息，因为我想把注意力集中在游戏的结构上。在 round_instance.status 中跟踪状态消息使我们能够很容易地将游戏的流程传达给客户端。**

**关于扑克逻辑需要记住的一些事情:游戏只能以两种方式结束。摊牌(所有下注回合都已结束)或还剩一名玩家。当用户提交移动时，回合模型检查自身及其用户的属性，以确定游戏的状态。**

**这是我第一次想出的解决方案。我认为可以有一些改进:具体来说，减少圆形模型的属性。让我知道我是否能做任何改进！**

**你可以在[我的完整项目](https://github.com/atribecalledarty/console-poker)中查看模型和迁移。**