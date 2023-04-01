# 使用 ML 模型的贷款预测系统

> 原文：<https://medium.com/mlearning-ai/loan-prediction-system-using-ml-models-b7410c5280ba?source=collection_archive---------8----------------------->

![](img/a3f925e87a11d91a79c25f1a5851e2fb.png)

# 问题陈述

我们有住房金融公司，并希望根据填写在线申请表时提供的客户详细信息，自动完成贷款资格流程。

# 关于数据集

**贷款标识:**唯一的贷款标识

**性别:**男/女

**已婚:**申请人已婚(Y/N)

**家属:**家属数量

**学历:**申请人学历(研究生/本科生)

**自由职业者:**自由职业者(是/否)

**申请收入:**申请人收入

**共同申请人收入:**共同申请人收入

**贷款金额:**贷款金额，单位:千

**贷款 _ 金额 _ 期限:**贷款期限(月)

信用记录:信用记录符合规定

**房产 _ 面积:**市区/半市区/郊区

**贷款 _ 状态:**(输出变量)贷款批准(是/否)

# 导入所需的库

![](img/9673312176ff5a025c92dc1ebfc6afb0.png)

# 加载并验证数据的形状

![](img/46ae0b4e729c6a7b652c11070d95f5b6.png)

# 数据预处理

# 1.1 分类自变量与目标变量的分析

![](img/3be86a601d521fe535a9dca8df31a987.png)![](img/8937500a8433b4bbcb1e3bf9651ce9d4.png)

1.  对于已批准的贷款，已婚申请人的比例更高。
2.  有 1 个或 3 个以上受抚养人的申请人在两种贷款状态类别中的分布相似。
3.  从自营职业者与贷款者的对比图中，我们无法推断出任何有意义的东西。
4.  看起来信用记录为 1 的人更有可能获得贷款批准。
5.  与农村或城市地区相比，半城市地区获得批准的贷款比例更高。

# 1.2 去除无关紧要的变量

Loan_ID 列包含申请人的序列号，这对于进一步的分析是多余的。因此，我们删除该列。

![](img/e64b5512f7e700415306a784d82e8d87.png)

# 1.3 缺失值处理

![](img/26187127f9cacb9579479cdb041c4351.png)

我们在一些变量中有空值。我们将看到变量的值计数，并决定填充空值的更好方法。

![](img/65cfd74599fe2567c71eef8b022b4818.png)

通过查看变量 Loan_Amount_Term，它是一个数字变量，值 360 是重复最多的。因此，我们将使用该变量的模式替换该变量中缺少的值

![](img/a8ed282543098a6d52ce4ddac6f3ccc6.png)

通过查看可变贷款额，我们将使用中位数来填充空值，因为我们看到贷款额有异常值，所以平均值将不是正确的方法，因为它受异常值的影响很大。

![](img/15b05e3cd219aa2f06d106d57af7b1fe.png)

# 1.4 异常值处理

![](img/7638f1da06a3e265ca5cfa90ec41d414.png)![](img/31b094d839d5a544a7ea844937a04de5.png)![](img/7e4bcab91ef3ba99f0bc481741f8e901.png)![](img/0cd057de2e8ac7710ea76a450e7e3fd9.png)

变量不是正态分布的

由于这些异常值，贷款金额中的大部分数据位于左侧，右尾较长。这叫做右偏度。消除偏斜的一种方法是进行对数变换。当我们进行对数变换时，它不会对较小的值产生太大的影响，但会减少较大的值。所以，我们得到一个类似于正态分布的分布。我们来形象化一下 log 变换的效果。

我假设有些人收入很低，但是有很强的共同收入，所以一个好主意是把他们放在一个总收入栏里。并删除 coapplicantIncome 变量

![](img/f65e10d9c3ddb38792e808ca2634adae.png)![](img/0441534801da8db83ac14dcf9d66b8d2.png)![](img/489b81f5f9d2372d29d8b136da011a28.png)

# 1.5 对分类变量进行编码

![](img/6697fca1261a87329b2bc8a1a76bd4cb.png)

# 1.6 所有数值变量之间的相关性

![](img/9472f740830be11177cf8b6dcadf20b3.png)

我们看到最相关的变量是申请收入—贷款金额和信用记录—贷款状态。

# 创建一个广义函数来绘制测试集的 roc 曲线。

![](img/3ae7cf106f68150e3fec73e557b4bdc7.png)

# **创建输入和目标变量**

![](img/f6ef65fec0da035cdb0050648a15d2f2.png)

# 1.7 因变量的分布

![](img/d43d89879d356fa9e5221a15c0064870.png)

从图中我们可以看出，数据是不平衡的。我们将使用 SMOTE 进行过采样。

# 平衡数据的 SMOTE

![](img/5c674b561c140e317aa5d29f7c5674fc.png)![](img/9b04363a8c0fcf9bad0eae618b69e640.png)![](img/b7e49aca674b6afc3bfde8f3a3a5414f.png)

# 列车测试分离

![](img/2f2c595a81cf33e903171e76ef86972e.png)

# 逻辑回归

## 在训练数据集上构建完整的逻辑模型

![](img/c94aca21dc430b3ad026a14e670bf34a.png)![](img/9ecae12f20cd13860732f4a411f82411.png)![](img/b14154b966349fce61cf08a802a16d8e.png)

**解读:**使用逻辑回归，我们得到了 72%的准确率。

# k 最近邻(KNN)

## 使用欧氏距离在训练数据集上构建 knn 模型

![](img/8175b7a4fbb6317464799e618e5975c7.png)![](img/ad67f679e6b969c8f6285a50eb73954c.png)![](img/6b630881989ee62037823001d7aa49e8.png)![](img/b17ae348b5a27ef3cf1a5bef0d78d6c1.png)![](img/eabdb615be17d9b221efbedee8e48ffd.png)

**解释:**使用逻辑回归，我们得到了 78%的准确率。

# 结论

![](img/5453ded8e5a7955da1f48855bca6de8a.png)

**解释:**从结果中我们可以看出，与其他模型相比，KNN 模型给出了更好的准确性和 AUC 分数。我们可以利用 KNN 进行部署。