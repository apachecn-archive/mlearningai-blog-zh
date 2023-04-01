# Python 库及其用途

> 原文：<https://medium.com/mlearning-ai/starting-to-artificial-intelligence-3bc06bbfe911?source=collection_archive---------1----------------------->

*Python 库人工智能入门指南*

![](img/169516132f3d28c6d2823986c494ac06.png)

Photo by [Alex Knight](https://unsplash.com/@agk42?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# **为什么是 Python？**

**电池包括**现有经典数值方法、绘图或数据处理工具的丰富集合。我们不想重新编程绘制曲线，傅立叶变换或拟合算法。不要多此一举！

*   大多数科学家不像程序员那样拿工资，也没有接受过这样的培训。他们需要能够在几分钟内画出曲线，平滑信号，进行傅立叶变换。
*   为了让代码在实验室或公司内保持活力，它应该像书一样容易被合作者、学生或者客户阅读。Python 语法很简单，避免了奇怪的符号或冗长的例行规范，这些会转移读者对代码的数学或科学理解。
*   **高效代码** Python 数值模块计算效率高。但是不用说，如果花太多时间去写，一个非常快的代码会变得毫无用处。Python 的目标是快速开发和快速执行。
*   通用 Python 是一种用于许多不同问题的语言。学习 Python 避免了为每个新问题学习一个新软件。

# ***Numpy***

NumPy 是 Python 中科学计算的基础包。这是一个 Python 库，它提供了一个多维数组对象、各种派生对象(如掩码数组和矩阵)以及一系列对数组进行快速操作的例程，包括数学、逻辑、形状操作、排序、选择、I/O、离散傅立叶变换、基本线性代数、基本统计操作、随机模拟等等。

NumPy 包的核心是 ndarray 对象。这封装了同构数据类型的 n 维数组，为了提高性能，许多操作都在编译后的代码中执行。NumPy 数组和标准 Python 序列之间有几个重要的区别:

*   NumPy 数组在创建时具有固定的大小，不像 Python 列表(可以动态增长)。更改 ndarray 的大小将创建一个新数组并删除原始数组。
*   NumPy 数组中的元素都需要具有相同的数据类型，因此在内存中的大小也相同。例外:可以有(Python，包括 NumPy)对象的数组，从而允许不同大小元素的数组。
*   NumPy 数组有助于对大量数据进行高级数学和其他类型的运算。通常，与使用 Python 的内置序列相比，这种操作的执行效率更高，代码更少。
*   越来越多的基于 Python 的科学和数学包正在使用 NumPy 数组；虽然这些通常支持 Python 序列输入，但是它们在处理之前将这种输入转换为 NumPy 数组，并且它们经常输出 NumPy 数组。换句话说，为了有效地使用当今许多(甚至可能是大多数)基于 Python 的科学/数学软件，仅仅知道如何使用 Python 的内置序列类型是不够的——还需要知道如何使用 NumPy 数组。

# ***熊猫***

pandas 是一个 Python 包，它提供了快速、灵活、富于表现力的数据结构，旨在使处理“关系”或“标签”数据变得既简单又直观。它的目标是成为用 Python 进行实际的、**真实世界**数据分析的基础高级构建块。此外，它还有一个更广泛的目标，那就是成为任何语言中最强大、最灵活的开源数据分析/操作工具。它已经在朝着这个目标前进。

pandas 非常适合许多不同类型的数据:

*   具有不同类型列的表格数据，如在 SQL 表或 Excel 电子表格中
*   有序和无序(不一定是固定频率)时间序列数据。
*   带有行和列标签的任意矩阵数据(同类或异类)
*   任何其他形式的观察/统计数据集。数据根本不需要标记就可以放入 pandas 数据结构中

以下是熊猫擅长的几件事:

*   轻松处理浮点和非浮点数据中的缺失数据(表示为 NaN)
*   大小可变性:可以在数据帧和高维对象中插入和删除列
*   自动和明确的数据对齐:对象可以明确地与一组标签对齐，或者用户可以简单地忽略标签，让系列、数据框等。在计算中自动调整数据
*   强大、灵活的分组功能，可对数据集执行拆分-应用-组合操作，用于聚合和转换数据
*   轻松将其他 Python 和 NumPy 数据结构中不规则的不同索引数据转换为 DataFrame 对象智能的基于标签的切片、花式索引和大型数据集的子集化
*   直观的合并和连接数据集
*   数据集的灵活整形和旋转
*   轴的分层标签(每个刻度可能有多个标签)
*   强大的 IO 工具，用于从平面文件(CSV 和带分隔符文件)、Excel 文件、数据库加载数据，以及从超快速 HDF5 格式保存/加载数据
*   特定于时间序列的功能:日期范围生成和频率转换、移动窗口统计、日期移动和滞后。

# ***张量流***

TensorFlow 是一个软件库或框架，由谷歌团队设计，以最简单的方式实现机器学习和深度学习概念。它结合了优化技术的计算代数，便于许多数学表达式的计算。

TensorFlow 是有据可查的，包括大量的机器学习库。它为此提供了一些重要的功能和方法。TensorFlow 也被称为“谷歌”产品。它包括各种机器学习和深度学习算法。TensorFlow 可以训练和运行深度神经网络，用于手写数字分类、图像识别、单词嵌入和各种序列模型的创建。

现在让我们考虑张量流的以下重要特征:

*   它包括的一个功能，可以借助称为张量的多维数组轻松定义、优化和计算数学表达式。
*   它包括深度神经网络和机器学习技术的编程支持。
*   它包括对各种数据集的高度可扩展的计算特性。TensorFlow 使用 GPU 计算，实现管理自动化。
*   它还包括优化相同内存和所用数据的独特功能。

*Keras 利用各种优化技术使高级神经网络 API 更容易和更高效。它支持以下功能*

*   *一致、简单且可扩展的 API。*
*   *最小结构——无需任何装饰即可轻松实现目标。*
*   *它支持多种平台和后端。*
*   *这是一个用户友好的框架，可以在 CPU 和 GPU 上运行。*
*   *计算的高度可扩展性。*

*Keras 是一个非常强大的动态框架，具有以下优势*

*   *更大的社区支持。*
*   *容易测试。*
*   *Keras 神经网络是用 Python 编写的，这使得事情变得更简单。*
*   *Keras 支持卷积和递归网络。*
*   *深度学习模型是离散的组件，因此，您可以以多种方式进行组合。*

# ****PyTorch****

*PyTorch 被定义为 Python 的开源机器学习库。它用于自然语言处理等应用。它最初是由脸书人工智能研究小组和基于它的优步概率编程软件 Pyro 开发的。*

*最初，PyTorch 是由 Hugh Perkins 开发的，作为基于 Torch 框架的 LusJIT 的 Python 包装器。PyTorch 有两种变体。*

*PyTorch 在 Python 中重新设计并实现了 Torch，同时为后端代码共享相同的核心 C 库。PyTorch 开发人员调整了这些后端代码，以便高效地运行 Python。他们还保留了基于 GPU 的硬件加速以及使基于 Lua 的 Torch 具有可扩展性的特性。*

## *PyTorch 的优势*

*PyTorch 的优势如下:*

*   *代码很容易调试和理解。*
*   *它包括许多层，如火炬。*
*   *它可以被认为是对 GPU 的 NumPy 扩展。*
*   *它允许建立其结构依赖于计算本身的网络。*

# ****Scikit-Learn****

*Scikit-learn (Sklearn)是 Python 中最有用、最健壮的机器学习库。它通过 Python 中的一致性接口，为机器学习和统计建模提供了一系列有效的工具，包括分类、回归、聚类和降维。这个库主要是用 Python 编写的，构建在 NumPy、SciPy 和 Matplotlib 之上。*

*Scikit-learn library 专注于数据建模，而不是专注于加载、操作和汇总数据。Sklearn 提供的最受欢迎的几组模型如下:*

***监督学习算法**:几乎所有流行的监督学习算法，如线性回归、支持向量机(SVM)、决策树等。，是 scikit-learn 的一部分。*

***无监督学习算法**:另一方面，它还拥有从聚类、因子分析、PCA(主成分分析)到无监督神经网络的所有流行的无监督学习算法。*

***聚类**:该模型用于对未标记的数据进行分组。*

***交叉验证**:用于检查监督模型对不可见数据的准确性。*

***降维**:用于减少数据中可进一步用于汇总、可视化和特征选择的属性数量。*

***集成方法**:顾名思义，用于组合多个监督模型的预测。*

***特征提取**:用于从数据中提取特征，定义图像和文本数据中的属性。*

***特征选择**:用于识别有用的属性，创建监督模型。*

*开源:这是一个开源库，在 BSD 许可下也可以商业使用*

*[](/mlearning-ai/mlearning-ai-submission-suggestions-b51e2b130bfb) [## Mlearning.ai 提交建议

### 如何成为 Mlearning.ai 上的作家

medium.com](/mlearning-ai/mlearning-ai-submission-suggestions-b51e2b130bfb) 

🔵 [**成为作家**](/mlearning-ai/mlearning-ai-submission-suggestions-b51e2b130bfb)*