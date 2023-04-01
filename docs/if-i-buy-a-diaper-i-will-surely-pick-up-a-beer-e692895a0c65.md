# 如果我买尿布，我一定会买一瓶啤酒！

> 原文：<https://medium.com/mlearning-ai/if-i-buy-a-diaper-i-will-surely-pick-up-a-beer-e692895a0c65?source=collection_archive---------8----------------------->

使用 Python 进行购物篮分析/关联规则挖掘

![](img/4bd90ea5622e3bc2164bca5f3829e25a.png)

Photo by [Kenny Eliason](https://unsplash.com/@neonbrand?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

关联规则挖掘是数据挖掘的一个分支，对于零售和其他在线业务非常有用。你可能有过这样的经历，当你在网上买东西时，一些相关的商品会作为建议显示给你，这增加了任何组织的销售额。线下零售店的情况也是如此，店主总是试图将相关的商品放在一起，以便用户可以方便地拿走。比如把 DVD 放在 DVD 播放机旁边。关联规则挖掘可以发现许多我们想都不敢想的不可能的关联，比如著名的[啤酒尿布关联](https://tdwi.org/articles/2016/11/15/beer-and-diapers-impossible-correlation.aspx)。

随着过去十年中收集的数据的增加，关联规则挖掘再次流行起来，并成功地产生类似的推荐。在这篇博客中，我们将学习一些基础知识和一种算法，使用这种算法我们可以对收集的任何数据集执行关联规则挖掘。

# 输入数据集

关联规则挖掘又称购物篮分析是在包含用户执行的交易记录的交易数据集上进行的。我为这个博客考虑了两个数据集，分别是**在线零售**和**电影镜头数据集。**两个数据集如下所示:

![](img/d83199100f5909ec63064cbc0fed4229.png)

Online Retail Dataset [Source: Author]

![](img/fbc176e12113254310506086990a03f7.png)

Online Movie Lens Dataset [Source: Author]

如上图所示，这两个数据集都是正常的事务性数据集。在线零售数据集具有唯一的发票号，其中每一行显示在一个发票号下购买的单个商品。另一方面，电影镜头数据集具有电影所属的不同类型，由特殊字符(|)分隔。通常，我们会在不同的组织中收集这两种类型的事务性数据集。需要记住的一点是，我们需要决定需要对哪一列进行关联规则挖掘。例如，在电影镜头数据集中，我们不关心电影的名称或年份，我们只是希望知道类型之间的关系。如果一部电影是喜剧，那么它也可能是惊悚片。

# 数据预处理

在本节中，我们假设数据集是正确的，并且不包含缺失值、拼写错误或任何其他错误。我们将学习如何将一个精炼的数据集转换成一种格式，以便我们可以执行关联规则挖掘。

## 在线零售数据集

我们已经使用发票号对库存代码进行了分组，并通过应用 list 函数创建了一个项目列表。如果需要，我们还可以对产品名称进行分组。下图显示了使用上述代码创建的数据集的一部分的快照。

![](img/6e1c051b996a69ecdf78193b34f1a96c.png)

[Source: Author]

## 电影镜头数据集

在这个数据集中，我们使用字符(|)拆分了流派的单词，并将一个事务的所有流派存储为一个列表值。第一个列表包含以下数据:

![](img/ed38bf1e627eacc02b34ff4dd4541208.png)

[Source: Author]

## 为关联规则挖掘准备数据集

上一节中的细化数据集也与关联规则挖掘不兼容。准确的关联挖掘数据集应该将所有项目作为列，并且每个交易应该将列表中可用的产品显示为真，所有其他产品应该为假，就像我们在创建 hot encoder 时所做的那样。根据我们在挖掘过程中使用的语言和框架，True 和 False 可以替换为 1 和 0。幸运的是，python 有一个名为 **mlxtend(机器学习扩展)**的专用包，可以用来将任何事务性数据集转换成热编码器。用于进行这种转换的函数叫做 **TransactionEncoder** ，这个包使用 fit 和 transform 方法进行转换。参见下面的代码，两个数据集的事务数据用于将其转换为 hot 编码器，然后以 pandas 数据帧的形式存储。下图显示了在线零售和电影镜头数据集的数据框片段。

![](img/09c0acd890439ec5c1c6eb0c05c9bb0a.png)

Online Retail dataset after conversion to Hot Encoder [Source: Author]

![](img/afea269f34cf7c8c5d948c1c9f82e933.png)

Movie Lens Dataset after conversion to Hot Encoder [Source: Author]

# 关联规则挖掘度量

我们有各种各样的关联规则度量标准，可以用来选择和拒绝关联规则，所有的度量标准都会在这个博客中一一讨论。

## 支持

支持度量查找包含一个项目或多个项目的组合的事务的比率，可以通过以下方式编写:

![](img/39cea4e83ffe5d943389ccc630b0bff4.png)

让我们计算两个数据集中每一项的支持度，我们只需找到每一列的平均值即可。具有 True 的值将被相加并除以作为支持值的事务数量。也可以计算两个组合项的支持，如下面代码的第 8 行所示。

![](img/3e962cdf7af29816afd08407f6433abe.png)

Support of Online Retail Dataset [Source: Author]

![](img/aa248c2671865ff5151a7eeb9f323c1d.png)

Support of all Genre of Movie Lens Dataset [Source: Author]

## 信心

当一个项目在交易中受欢迎时，支持度量可能会产生误导。我们可以在与另一个项目相关的项目中找到信心，这将使我们对特定规则更有信心。它将给出有两个项目的交易数量与有一个项目的交易数量的比率。置信度越高，规则越好，置信度为:

![](img/9f01cfb5e71b630555c19d098e2d4f10.png)

上面的代码显示了置信度函数，它接受关联规则的前因和后果，并返回置信度值。例如，**剧- >喜剧**的置信度只有 **0.19** ，这是一个不太好的规则。

## 电梯

提升是另一个度量，它通过发现前件的置信度与后件的支持度的比率来提升置信度的值。从字面上来说，就是在知道前因的情况下拥有结果与支持结果的比例。升力的方程式是:

![](img/4a9b88077b0ec5e2d22fc4e1f19da0c7.png)

比如 lift(喜剧->戏剧)就是在我们知道是喜剧的情况下，一部电影成为戏剧的概率与一部电影成为戏剧的概率之比。这种提升胜过支持和信心两者。下面的代码计算升力，对于一个好的规则，升力的值应该大于 1。

## 杠杆作用

Lift 的范围从 0 到无穷大，因此很难确定与规则相关联的范围。杠杆指标生成-1 到+1 范围内的输出，这解决了提升指标的问题。它可以代替电梯使用，提供更好的信息。杠杆可以计算为

![](img/9ca1aee09c551aec9b8e517e56b5c9d4.png)

## 张度规

上面讨论的所有指标都给出了一个规则的关联程度，而没有提到解除关联的程度。就像两个物体在天平上是如何分离的。张在 2000 年提出了一个新的度量标准，它不仅可以计算先行词和结果词之间的关联，还可以计算它们之间的分离程度。该指标通过生成从-1 到+1 范围内的输出值来实现这一点。所有负值表示分离的程度，正值表示关联。张的度量是这样计算的:

![](img/915ed2e057def1d731af58d191c0086c.png)

如果仔细展开，这个等式可以写成:

![](img/e30209a2579733b0a88d17b3676df69c.png)

下面的代码显示了张指标的实现:

## 一个数据框架中的所有指标

让我们根据一对一规则找出所有这些指标的值，并使用这些值创建一个数据框。这可用于多标准关联规则挖掘。

![](img/6e8d71ab2a59dff09a986a5862288358.png)

[Source: Author]

上图显示了数据帧的头部，对于一对一项目规则，每个指标都有一列。

# 多准则关联规则挖掘

我们可以使用多个指标来识别有用的规则。参见下面的代码

随着数据集中项目数量的增加，多标准关联规则挖掘方法变得难以执行和实现。对于大项目规模的数据集，我们有 Apriori/FP growth 这样的标准算法。然而，这些度量的知识对于那些高级算法的实现是重要的。

# Apriori 算法

这个博客作为一个单独的博客已经足够长了，所以我不会详细讨论 Apriori 算法的工作原理。apriori 的基本思想是，任何包含不频繁项的项集也是不频繁的。它消除了多个项集的组合，见下图。如果蜡烛线不频繁(支持度小于阈值)，则包含蜡烛线的所有项目集也不频繁，并且不会被考虑用于关联规则生成。

![](img/9769b54bab60a2aab78f272da1a979bc.png)

Apriori 算法的一个重要因素是它用于消除非频繁项集，它不创建任何关联规则。我们必须使用另一种方法从频繁项集中发现规则。apriori 见下面的代码，下面会一步步解释。

第 1 到 3 行从 mlxtend 导入了所需的包。第 5 行使用 apriori 算法来修剪规则，并找到最小支持度为 0.005 且最大项目集长度为 4 的规则。该数据集中频繁项集的长度为 **532。**参见下面的频繁项集:

![](img/7251a55fd544e9a7416df5e5cbfafad5.png)

[Source: Author]

第 10 行使用了 **association_rule** 函数，通过使用最小值为 0.001 的 **support** 度量从频繁项目集中发现规则。我们可以使用我们在博客中讨论过的任何指标，比如**提升**、**信心等等。**(见第 13 至 15 行)。association_rule 函数打印大部分指标值，见下图(第 11 行)。

![](img/a2d8bd21605a8a522867c0dc85491c36.png)

[Source: Author]

此外，我们还可以对这些规则使用多标准关联规则挖掘，并生成满足各种条件的规则(参见第 17 行)。请看下图，我们使用各种条件生成了 10 条规则。

![](img/4f1c3a0d6bf7280d089f0d3736eed0b3.png)

[Source: Author]

# 结论

购物篮分析(也称为关联规则挖掘)是一种重要的方法，可用于各种组织和企业。使用这些方法也可以改进特定于用户的推荐生成。这个研究领域非常广阔，这个博客将让你从基本的代码和方法开始。

这些方法可以与推荐系统结合使用，从而产生更好的推荐。

[](/mlearning-ai/mlearning-ai-submission-suggestions-b51e2b130bfb) [## Mlearning.ai 提交建议

### 如何成为 Mlearning.ai 上的作家

medium.com](/mlearning-ai/mlearning-ai-submission-suggestions-b51e2b130bfb)