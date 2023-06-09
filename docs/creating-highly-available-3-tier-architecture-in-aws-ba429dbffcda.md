# 在 AWS 中创建高度可用的 3 层架构

> 原文：<https://blog.devgenius.io/creating-highly-available-3-tier-architecture-in-aws-ba429dbffcda?source=collection_archive---------3----------------------->

![](img/315b9b7dea5a87bffd6a94a53393a846.png)

## 什么是三层架构？

它是一种客户机-服务器体系结构，将体系结构分为三层:数据层、应用层和表示层。

1.  **表示层** —这一层向浏览器发送 HTML、JS 和 CSS。它可能使用 React、Angular、Ember、Aurora 等框架。
2.  **应用** —为应用处理业务逻辑。它可能是用 C#、Java、C++、Python、Ruby 等语言编写的。
3.  **数据库** —这一层通过数据库管理系统提供对应用数据的访问。这可能是 MSSQL、MySQL 或 PostgreSQL 等。

假设您正试图使用一个 web 应用程序来查找您所在地区的电影时间，作为三层架构的一个示例。在表示层，您会看到一个包含输入信息字段的网页。例如，你的邮政编码和你想看电影的日期。然后将信息传递给应用层，应用层格式化查询并将其发送给数据库。

数据库系统运行查询并将结果(您所在地理区域内的可用电影列表)返回给应用层，应用层将结果格式化为网页。之后，页面被发送回浏览器，浏览器使用表示层在笔记本电脑或其他设备上显示页面。

## 利益

*   您可以更新应用程序技术堆栈的一个层，而不会影响其他方面。
*   不同的开发团队可以专注于不同的专业领域。今天的开发人员更有可能在一个领域拥有深厚的能力，比如前端编码，而不是在整个堆栈上工作。
*   可伸缩的应用程序允许您部署到多个数据库并添加额外的 web 服务器，而不是局限于一种特定的技术。例如，单独的后端层允许您部署到多个数据库。
*   通过分离表示代码和业务逻辑，它简化了代码库的维护，例如，对业务逻辑的更改不会影响表示代码。

## 目标

*   创造一个 VPC
*   创建 Web 层
*   创建应用层
*   创建数据库层

# 步骤 1:创建 VPC

在此步骤中，我们将为 VPC 总共创建 6 个子网。两个公共子网用于面向 Web 的服务器，四个私有子网。应用层和数据库层各两个。这将跨两个可用性区域进行配置，以确保高可用性。

我们的 VPC 将包括一个 NAT 网关，用于私有子网中的主机，以确保它们能够连接到互联网进行更新等。将配置公共和私有路由表。

导航到控制台中的 ***VPC 仪表盘*** ，点击 ***创建 VPC*** 。

我们将利用 AWS 的 ***VPC 体验*** 向导来自动创建我们的 VPC 资源。这将为我们创建 internet 网关、子网、NAT 网关和路由表。

输入您的项目名称并选中自动生成框。选择 2 个公共子网和 4 个私有子网。到目前为止，您的设置应该是这样的。

![](img/2120b8c4886d1e291cf335b0049fad59.png)

选择选项以选择在 1 AZ 中创建 NAT 网关。将 VPC 端点选项改为 ***【无】*** 。点击 ***创建 VPC*** 。

![](img/4fded310c3a243eb6fb8a39ecc352f9b.png)

现在我们的网络 VPC 图应该是这样的。

![](img/857c4c011ba87eff96fa4ce924da6114.png)

向导将为每个专用子网创建一个路由表。在我们的情况下，这是不需要的，我们可以修改其中一个私有路由表，使其包含我们所有的私有子网，以便于管理。

![](img/b0098d93277e30daba14c06c7f077b07.png)

让我们修改其中一个路由表，使其包含所有私有子网。我将导航到 VPC >路由表，并将其中一个私有路由表的名称更改为“***tier 3 project-rt b-private***”。

![](img/5e3317fadabab1b27cf09e0ba6256291.png)

显示路由表

点击 ***路由表*** > ***子网关联*** 选项卡然后点击 ***编辑关联*** 内 ***显式子网关联***

![](img/9846ff40d14db652620c600f0e2c3d64.png)

选中所有私有子网的复选框，然后单击 ***保存关联*** 。

![](img/e8282d38c02e5bcd822a9e41ddf3552d.png)

现在我们可以删除其它私有路由表了。勾选子网的复选框，然后从 ***动作*** 下拉菜单中点击 ***删除路由表*** 。

![](img/4be6345f7f0d46bf604f6d28564375ae.png)

确认删除，我们已经创建了我们的 VPC。

![](img/7307a2e82dd10095aaf015417fdae88e.png)

# 步骤 2:创建 Web 层

让我们用应用程序负载平衡器为我们的 web 层创建一个自动扩展组。

导航到自动缩放组并点击 ***创建*** 。

![](img/00e5f0b7a1517b56644cdf0bcd5fce47.png)

我将我的名字命名为 ***WebTier-ASG*** ，然后点击创建一个 ***启动模板*** 。

![](img/8cefb6784923a006a5c2369b15113d2b.png)

在新窗口中，配置模板的名称，并选择一个带有 t2.micro 实例类型的自由层 Amazon AMI，然后关联一个密钥对。

![](img/76a905abae9a3ab946d8c670a19201df.png)![](img/19ce781cee4739f60e073ae88fcc1727.png)

创建一个新的安全组，给定一个名称，并允许来自任何来源的 HTTP 流量。添加一个规则，理想情况下只允许从您的 IP 使用 SSH。出于演示目的，我将允许它来自任何地方。选择我们创建的 VPC。

![](img/16de010d92f5cff159502fec7ff676d4.png)

在 ***高级网络配置下*** 添加网络接口 ***启用*** 自动分配公网 IP。

![](img/a8cbc0e0ab4e8a38d8f98668de387184.png)

现在将引导映像来安装和运行 apache。展开 ***高级详情*** ，在 ***用户数据*** 字段输入以下代码。

```
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<html><body><h1>My Custom Tier 3 Application!</h1></body></html>" > /var/www/html/index.html
```

点击 ***创建启动模板*** 完成。

![](img/76a12e46aed7ac9882d3be55e26f8473.png)

现在回到自动缩放组向导，从下拉菜单中选择我们刚刚创建的模板，然后点击 ***下一个*** 。

![](img/7bda81dd13e3604fc88ce01dcd151a59.png)

选择我们的 VPC，并从下拉列表中选择我们的两个专用子网，然后单击下一步。

![](img/53dac8c036d98f2d6487283b457bb239.png)

选择 ***连接新的负载平衡器*** 和 ***面向互联网。*** 选择 ***创建目标组 t*** 然后保留所有默认值。点击**下一步*。***

![](img/3aa5cf9023ebb39ea989717b7fd4c1c1.png)

我们希望任何时候都至少有两台机器处于运行状态。将设置更改为以下内容。然后点击 ***跳过查看。***

![](img/12cc0eedbe676c9e59c554514cba36f6.png)

点击 ***创建自动缩放组。***

![](img/45493234d8cee756168f1f866cdeb997.png)

现在我们已经创建了 ASG，我们需要更改应用程序负载平衡器的安全组，以允许 internet 流量通过。导航到 ***EC2 >负载平衡器*** 并选择我们的***WebTier-ASG-1***负载平衡器。

![](img/c064658484a74f067a977f128cad42fa.png)

转到 ***操作*** >编辑 ***安全组*** 然后点击 ***创建新的安全组*** 。

给它一个名字，并选择我们的 VPC。允许来自任何来源的 HTTP 流量。

![](img/6c4c711f9e7df02ced9359e123c17c96.png)

现在将安全组与负载平衡器关联起来。

![](img/4ed0b44c6013d3619b01d8a39afcdaaf.png)![](img/5d7b4d07a85b82e8bac4b165a4be0b73.png)

现在，让我们通过将负载平衡器的 DNS 名称复制到 web 浏览器中来进行测试。

![](img/b2587647bb49f5df0b4b2fa97d61ec96.png)

显示默认网页

太好了！第一层已经完成，我们可以查看我们的前端服务器。

# 步骤 3:创建应用层

现在我们将创建应用层。这将非常类似于我们的 web 层。我们将把我们的自动伸缩组放在两个私有子网中来托管我们的 EC2 实例。

像之前一样创建另一个 ASG 这次把它叫做 ***AppTier-ASG*** 并选择 ***创建*** ***启动模板。选择与 web 层相同的 AMI 和实例类型。***

创建新的安全组。这次将 NSG 配置为只允许来自我们的 ***WebTier-NSG*** 的流量。

![](img/51e60a30a47b2690aee46ee65c1caaa8.png)

不需要启用公共 IP 分配，因为这些实例将保留在我们的专用子网中。我们不会向用户数据字段添加任何代码。

现在回到我们的 ASG 向导，选择我们刚刚创建的启动模板，然后单击 ***下一步*** 。选择适当的 VPC 和两个私有子网。

![](img/76ba1d5ac81979bfe04f2b01ccc2f0d2.png)

添加一个新的 ALB，这次选择 ***内部*** 为负载均衡方案。

![](img/08cfcdb147ef69510be329de16322f3c.png)

使用我们对 web 层所做的配置来完成向导。我们现在有两个 ASG 和两个 EC2 实例。

![](img/c30257a9d45a8b7c918699b451d8efff.png)

展示 ASG

![](img/e6e35f9a1e26e0ff42410f9322643693.png)

显示 EC2 实例

现在让我们验证一下，我们可以从 Web 层访问位于我们私有子网中的第 2 层 EC2 实例。连接到一个 web 层实例，并通过私有 IP ping 我们的第 2 层子网中的一个 EC2 实例。

![](img/07712dc55deb55d09c2490e2bc4e4cb4.png)

显示成功回复

我们的 ping 操作成功，并且我们已经正确配置了 NSG。第二层完成了。

# 步骤 4:添加数据库层

现在我们将添加我们的数据库。我们将利用免费层选项，并在我们的一个 az 中创建一个 MySQL 数据库。

创建新的安全组。选择我们的 VPC 并创建一个入站规则，只允许来自我们的 ***AppTier-NSG*** 的 ***TCP 端口 3306*** 的流量。

![](img/081fac1548ad5c0dd4a79dd34eda6ef2.png)

展示 NSG

在控制台内导航到 ***RDS >数据库*** 和选择 ***创建数据库***

![](img/f0911b20533b965a0745e3d2da831f0d.png)

选择 ***标准创建*** 和 ***MySQL*** 。选择 ***自由层*** 并保留默认值。填写密码字段。

![](img/5d2b1daf72da66fd45e7faff83c4d23c.png)![](img/cdbbffa762daff4b2daa5616f38209ae.png)

在 ***连接*** 部分选择我们的 VPC 和我们的 NSG 为 ***VPC 安全组*** 。选择 ***us-west-2a*** 作为可用区域。

![](img/86b237f91f33cdadd47e123a91bb5b42.png)

点击 ***创建数据库***

![](img/369533a084648c4ba22565d0a3e06d81.png)

数据库已经创建，我们完成了本教程。保重！