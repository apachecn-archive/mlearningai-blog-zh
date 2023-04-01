# 用基于机器学习的方法输入缺失值

> 原文：<https://medium.com/mlearning-ai/imputing-missing-values-with-machine-learning-based-approaches-373219dba314?source=collection_archive---------2----------------------->

在我之前的博客文章中已经深入研究了数据准备(如果感兴趣，请查看[数据挖掘中实例选择的介绍](/@sabrinaherbst/an-introduction-to-instance-selection-in-data-mining-7b2ac94fb07))，我决定继续研究数据预处理中的另一个重要主题，即处理缺失值。

特别是，我想深入研究基于最大似然法的方法，例如使用 KNN 或 K 均值聚类来估算缺失值。除非另有说明，相关信息摘自 García 等人[1]的第 4 章。

![](img/334b0762ea78b7d8160a633599671ab6.png)

pixabay.com

# 缺失价值的分类

当考虑缺失值时，可以大致区分**随机缺失(MAR)** 和**非随机缺失(MNAR)** 变量。

让我们考虑将输入变量 *X* 分成观察部分和缺失部分。MAR 的一个相当简单明了的观点是，缺失变量可以(但不一定)依赖于可用数据，但独立于其他缺失属性。

MAR 的一个特例是**完全随机缺失(MCAR)** ，其中缺失数据既不依赖于观测值，也不依赖于缺失数据。

类似地，MNAR 被定义为依赖于观察到的变量以及缺失的变量。请注意，以下方法依赖于 MAR 假设。

# 使用 ML 技术估算数据

有许多不同的方法来处理缺失值。这些分类器的范围从相当简单的分类器(例如，删除缺失变量或根本不输入，这对于像朴素贝叶斯这样的 ML 模型是可能的)到复杂的统计分类器，依赖于找到/近似潜在的分布(例如，最大似然估计)。

使用最大似然模型估算数据的一个优点是不需要明确地估计潜在的分布。熟悉 ML 模型工作的数据科学家将会看到，输入数据的过程与构建预测 ML 模型的过程非常相似。

## k-最近邻插补

可能最直接的基于 ML 的数据插补策略之一是使用 K 近邻插补(KNNI)。顾名思义，它使用 KNN 模型来预测缺失值。

因此，重要的是:( 1)定义要考虑的多个邻居*k*,以及(2)选择最终预测值的策略。要考虑的相邻点数量取决于不同的数据集特征(例如，在处理小数据集时，我们将考虑较少数量的相邻点)，因此，必须针对每个数据集单独计算。

预测最终值的策略通常与 KNN 分类器相同。因此，对于连续变量，将选择平均值，而对于名义属性，将进行多数投票。

KNNI 的思想已经扩展到加权 K 近邻填充(WKNNI)。作为扩展，该算法考虑了相邻数据点到插补的相应数据点的距离(例如，最近的相邻数据点比第 k 个最近的相邻数据点“更”重要)[2]。

通常，欧几里得距离将被认为是一种距离度量。但是，请记住，当 KNN 计算数据点之间的距离时，变量的缩放会对分类器产生很大的影响。

## k-均值聚类插补(KMI)

在 K-Means 聚类中，输入数据被分成 *k* 个聚类。然后，通过聚类中所有元素的平均值来计算每个聚类的聚类质心。目标是在同一聚类中有相似的数据点，从而最小化*聚类内相异度*(聚类中的数据点和质心之间的差异总和)。

我们将数据集分为两部分，即一部分包含所有完整的数据点，另一部分包含具有缺失值的样本。当考虑一组完整的数据点时，KMI 首先声明 *k* 元素为质心。

之后，修改聚类以减少聚类内的不相似性，直到达到某个不相似性阈值或者不再进行改变。

然后，添加具有缺失值的元素的剩余数据分区，并将每个数据点分配给一个聚类。为了找到样本的插补值，可以选择任意最近邻算法。我们将同一簇中的所有元素定义为最近邻。

这种方法也被扩展到模糊 K 均值聚类，其中一个节点可以同时属于(至少部分属于)多个聚类。欲了解更多信息，请参考李等人[3]。

## 其他方法

还有许多其他基于最大似然法的数据插补方法，例如下面列出的方法。如果感兴趣，请参考各自的论文。

*   奇异值分解插补[2]
*   事件覆盖[4]
*   局部最小二乘插补[5]

数据插补领域的研究在不断发展，新论文的发表非常频繁，提出了对现有技术的改进。虽然不可能在一篇简短的博客文章中涵盖所有内容，但我希望这篇文章仍能让您对将来如何处理丢失的数据有所了解。

[1] García 等[数据挖掘中的数据预处理](https://link.springer.com/book/10.1007/978-3-319-10247-4)。*智能系统参考图书馆。* 2015 年。

[2] Troyanskaya 等[DNA 微阵列的缺失值估计方法](https://doi.org/10.1093/bioinformatics/17.6.520)。*生物信息学。17/6: 520–525.2001 年。*

[3]李等.【面向缺失数据填补:模糊 K-均值聚类方法研究】。*粗糙集与当前计算趋势。2004 年。*

[4] Wong 等[从不完全混合模式数据中综合统计知识。](http://doi.org/10.1109/tpami.1987.4767986) *IEEE 传输模式分析机器智能。9/6:796–805*。1987.

[5] Kim 等[DNA 微阵列基因表达数据的缺失值估计:局部最小二乘插补](https://doi.org/10.1093/bioinformatics/bth499)。*生物信息学。**21/2:187–198*。2005.

[](/mlearning-ai/mlearning-ai-submission-suggestions-b51e2b130bfb) [## Mlearning.ai 提交建议

### 如何成为 Mlearning.ai 上的作家

medium.com](/mlearning-ai/mlearning-ai-submission-suggestions-b51e2b130bfb)