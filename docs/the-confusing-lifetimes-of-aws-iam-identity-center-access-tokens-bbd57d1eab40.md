# AWS IAM 身份中心访问令牌令人困惑的生存期

> 原文：<https://blog.devgenius.io/the-confusing-lifetimes-of-aws-iam-identity-center-access-tokens-bbd57d1eab40?source=collection_archive---------0----------------------->

每个星期，几乎毫无例外，我都会遇到一件让我困惑、娱乐或者最常见的激怒我的事情。我决定记录我的冒险经历。

我似乎陷入了#AWS #IAM Identity Center 内容的循环中。如果那不是你喜欢的，不要担心——我倾向于松鼠，我保证下周会有所不同。然而，本周我们将讨论 AWS 会话生存期以及为什么它们会令人困惑。

# 背景

AWS IAM Identity Center(以前的 AWS-SSO)提供#SSO 功能，支持 SAML、OIDC CLI 访问和 SCIM。随着最近[客户管理策略](https://aws.amazon.com/about-aws/whats-new/2022/07/aws-single-sign-on-aws-sso-aws-identity-access-management-iam-customer-managed-policies-cmps/)的加入，它确实成为 SSO 到 AWS 的唯一合理解决方案。

虽然 Identity Center 在后端有一个看似简单的前端，但它负责相当多的工作，尤其是与经典的 IAM SSO 相比。正如我所提到的，Identity Center 的主要优势之一是 OIDC 支持真正通过 CLI 修复 auth，这也可以由 [IDPs(如](https://support.okta.com/help/s/question/0D50Z00008C3jogSAB/saml-assertion-via-api?language=en_US) #Okta)修复，允许基于 OIDC 的 API 提供 SAML 断言(但我离题了)。Identity Center 的另一个强大功能是它可以被 AWS 组织识别。不幸的是，该服务需要建立在现有的 AWS 服务之上，例如 IAM，这些服务不支持组织，这将会引起一些问题。

请注意，为了发挥其魔力，Identity Center 为从属托管帐户提供了保留角色(和信任关系)。这意味着，当你通过用户界面或命令行界面选择一个帐户时，你会看到一个可用角色的列表，AWS 实际上向你展示了它神奇的保留角色——它对名称进行了一些清理，因此用户只能看到“权限集”名称，但这是发生什么的关键。

# 问题是

问题的核心是，为了保持现有的范例并使开发工作更加合理，只有少数 AWS API 端点可以使用访问令牌。有帮助的是，其中一个端点是[AssumeRoleWithWebIdentity](https://docs.aws.amazon.com/STS/latest/APIReference/API_AssumeRoleWithWebIdentity.html)，它接受一个访问令牌和角色名，并返回临时 AWS 凭证。但是，这有一个不幸的副作用，就是将 AWS Identity Center 访问控制与 IAM Classic 的现有访问控制机制混合在一起。虽然这两者之间的交互并不“脆弱”,但它们可能非常不直观。此外，违背 OIDC RFC 的建议也无助于这种非直觉性。

用户承担的 IAM 经典角色有一个最大会话持续时间。这个时间是可配置的，[最多](https://docs.amazonaws.cn/en_us/IAM/latest/UserGuide/id_roles_use.html)，12 小时。但是，在 Identity Center land 中，用于承担角色的访问令牌也有会话持续时间。此会话持续时间是不可配置的 8 小时。乍一看，这似乎没什么问题，但这实际上意味着用户能够在访问令牌的生命周期内承担多个有效角色。换句话说，在上面的例子中，在访问令牌发出后 7 小时 59 分钟，假设一个角色，用户将能够维持有效的 AWS 会话最多 20 小时。

显然，这种访问大大长于所需 AWS 角色的最大持续时间。此外，正如[上周](https://www.linkedin.com/pulse/aws-iam-identity-center-access-tokens-stored-clear-text-chaim-sanders/?trackingId=Lk8FLaP2tAJaq4%2BOm7fpiA%3D%3D)所发现的，这种 8 小时的默认设置[违背了 OIDC RFC](https://www.rfc-editor.org/rfc/rfc6750#section-5.3) 的规定，该 RFC 只推荐访问令牌的生命周期长度为 1 小时或更短。这个建议非常有趣，因为权限集和角色会话持续时间都只能设置为最少一个小时。

# 解决方案

那么，为什么 AWS 没有选择 1 小时的访问令牌到期时间呢？诚实的回答是我不知道，可能是礼仪。但是，正如我们上周所讨论的，留下这些访问令牌并不是一个特别明智的想法。

更正确的策略可能是在访问令牌用于承担角色后直接删除它。这种方法的问题是双重的。

1)用户可能希望使用访问令牌承担多个角色(实际上，我认为这可能需要重新认证)

2) AWS-CLI 将访问令牌的获取(“AWS 配置 sso”)与角色的假设分开。只有在执行活动(例如“aws s3 ls”)时，才会假定角色(并保留 AWS 凭证)。在承担角色之前和之后，访问令牌都保存在一个固定的位置(~/。AWS/SSO/cache/{ sha1 _ of _ start _ URL }。json)。这意味着，即使 AWS-CLI 删除了它认为是第一次使用的访问令牌，任何其他应用程序都可以在 AWS-CLI 使用之前利用这些凭据。

这里还有最后一个有趣的地方。权限集链接到角色，但不链接到角色的会话持续时间。权限集持续时间将覆盖神奇的“保留角色”的持续时间，权限集的持续时间将在 UI 中反映为 cookie 的到期时间，或在 CLI 时间中反映为~/中的到期时间。aws/cli/cache/*.json。

上述情况很奇怪，但这实际上并不构成问题，因为 AWS 管理员无法管理“保留角色”,因此永远无法修改信任关系以允许其他用户/角色承担这些特殊角色(身份服务 IDP 之外)。