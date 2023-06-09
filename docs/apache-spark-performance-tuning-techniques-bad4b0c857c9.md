# Apache Spark:调试和提高性能的方法

> 原文：<https://medium.com/mlearning-ai/apache-spark-performance-tuning-techniques-bad4b0c857c9?source=collection_archive---------3----------------------->

![](img/86dd129c0b086d8831866dac3d91c17f.png)

Photo by [Kristopher Roller](https://unsplash.com/@krisroller?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 介绍

Apache Spark 是一个快速的内存数据处理引擎，支持批处理和流处理。它被设计成可伸缩和灵活的，允许您在一个机器集群上运行大规模的数据处理应用程序。

尽管 spark 可以处理大规模数据处理，但也存在 spark 作业因内存问题而出错的情况。以下是 spark 作业中的一些常见错误。

## **Spark 常见错误**

1.  **内存不足**:如果 Spark 试图处理一个大于 worker 节点上可用内存的数据集，就会出现 OOM 错误。这可能是由大型输入数据集或需要大量内存来执行的复杂转换造成的。
2.  **内存泄漏**:如果 Spark 应用程序中存在内存泄漏，也会发生 OOM 错误，内存被分配但没有被正确释放。这可能导致可用内存量随着时间的推移逐渐减少，最终导致 OOM 错误。
3.  **配置不正确**:如果配置不正确，Spark 应用程序也会遇到 OOM 错误。例如，如果 Spark 执行器或驱动程序的内存分配设置得太低，可能不足以处理数据。
4.  **资源争用**:如果工作节点上存在对 CPU 或磁盘 IO 等资源的争用，也会发生 OOM 错误，这会导致 Spark 在等待这些资源变得可用时耗尽内存。

## 调试和改进 Spark 作业的方法

要对 Spark 中的错误进行故障排除，首先要确定问题的**根本原因，然后实施适当的措施来解决它，例如增加内存分配、优化 Spark 作业以使用更少的内存，或者确定并修复任何内存泄漏。**

## **1。适当的资源分配**:

为 Spark 分配适量的资源，比如内存和 CPU，有助于确保应用程序有足够的资源来高效地处理数据。您可以使用`spark.executor.memory`和`spark.executor.cores`配置来控制 Spark 执行器的资源分配。

## **2。数据分区**:

Spark 中的数据分区是将大型数据集划分为可以并行处理的较小分区的过程，从而提高 Spark 作业的性能和可伸缩性。

对数据进行正确的分区有助于确保数据均匀地分布在工作节点上，这可以提高涉及在节点之间转移数据的 Spark 操作(如连接和聚合)的性能。

以下是 spark 中不同的分区类型。

1.  **散列分区:**散列分区是一种使用散列函数来确定记录应该被分配到哪个分区的技术。这确保了具有相同哈希值的记录被分配到相同的分区。散列分区有助于在分区之间均匀分布记录，并确保记录被一致地分配给同一个分区。
2.  **范围分区**:范围分区是一种根据某些关键字段的值将记录分配给分区的技术。这有助于确保将具有相似键值的记录分配到同一个分区，从而提高按这些键值进行筛选或分组的查询和聚合的性能。
3.  **自定义分区:**自定义分区是一种允许用户定义自己的分区函数的技术，使他们能够指定如何将记录分配给分区。这有助于实现更复杂的分区方案，而这对于散列或范围分区是不可能的。

## **3。数据持久性**:

通过避免重复从磁盘读取数据的开销，将数据保存在内存中有助于提高 Spark 应用程序的性能。您可以使用`cache()`和`persist()`功能将数据存储在内存中，使用`unpersist()`功能将不再需要的数据从内存中删除。

Spark 提供一系列存储级别可供选择，包括:

*   **MEMORY_ONLY** :数据存储在内存中，但不持久存储到磁盘。这是最快的存储级别，但在内存使用方面也是最昂贵的。
*   **MEMORY_AND_DISK** :数据存储在内存中，但是如果数据量超过可用内存，就会溢出到磁盘。这种存储级别在性能和成本之间提供了良好的平衡，因为它允许您将内存用作缓存，同时仍然能够在磁盘上存储大量数据。
*   **DISK_ONLY** :数据只存储在磁盘上，不保存在内存中。这是最慢的存储级别，因为每次访问数据时都必须从磁盘中读取。不过从内存使用上来说是性价比最高的。
*   **MEMORY_ONLY_SER** :数据以序列化的形式存储在内存中，比原始数据占用的空间少，但访问速度较慢。当您需要在内存中存储大量数据，但没有足够的空间以原始形式存储数据时，此存储级别非常有用。
*   **MEMORY_AND_DISK_SER** :数据以序列化的形式存储在内存中，如果数据量超过可用内存，则以序列化的形式溢出到磁盘。这种存储级别类似于 MEMORY_AND_DISK，但使用的内存更少，代价是访问速度更慢。

## **4。数据偏斜**:

数据不对称，即数据集的某些分区明显大于其他分区，会导致 Spark 中的性能瓶颈。要解决这个问题，您可以使用数据采样、数据重新平衡或自定义分区等技术，将数据均匀地分布在工作节点上。

我在这里创建了一个关于数据偏斜[的独立帖子。](/@dishanka/data-skew-101-e5a7bda36f76)

## **5。优化 Spark SQL** :

您可以使用谓词下推、列修剪和分区修剪等技术来优化 Spark SQL 查询的性能。您还可以使用`EXPLAIN`命令来获得查询执行计划的详细分解，并识别任何潜在的优化机会。

1.  数据过滤—尽早过滤数据
2.  数据分布—将数据均匀分布在所有节点上
3.  连接顺序-连接表的顺序
4.  连接类型—为用例使用正确的连接类型。分类合并，散列和广播。默认为排序合并。
5.  避免笛卡尔连接
6.  尽可能避免按顺序排列
7.  使用高效的函数、数据结构

## 重要的火花配置

*   `spark.driver.memory`:该配置指定驱动程序进程应该使用的内存量。适当地设置这个值很重要，因为它会影响 Spark 应用程序的性能。
*   `spark.executor.memory`:这个配置指定了每个执行器应该使用的内存量。适当地设置这个值很重要，因为它会影响 Spark 应用程序的性能。
*   `spark.executor.cores`:这个配置指定了每个执行器应该使用的内核数量。通过增加内核数量，您可以提高 Spark 应用程序的并行性。
*   `spark.sql.shuffle.partitions`:该配置指定在 Spark SQL 查询中混排数据时使用的分区数量。增加该值可以让 Spark 更快地处理数据，但也会增加应用程序的内存和 CPU 使用率。
*   `spark.default.parallelism`:该配置指定运行 Spark 操作时应使用的默认并行度。它可以用来控制 Spark 创建的任务数量，并且可以根据内核数量和您正在处理的数据大小进行设置。
*   `spark.serializer`:该配置指定了应该用于序列化数据以便存储和传输的序列化库。默认的序列化库是 Java 序列化，但是您也可以使用其他库，比如 Kryo 序列化，它在某些情况下会更快更有效。
*   `spark.shuffle.service.enabled`:该配置指定是否启用用于管理数据混洗的混洗服务。启用 shuffle 服务可以通过减少网络流量来提高 Spark 应用程序的性能
*   `spark.memory.fraction`:这个配置指定了 Spark 中用于执行和存储的可用内存的比例。它表示为 0 到 1 之间的十进制值，可以用来控制 Spark 中执行和存储之间的平衡

# 结论

只要以正确的方式处理配置和资源，Apache spark 可以有效地处理大规模数据。小的改变可以带来大的不同。

感谢阅读！

[](/mlearning-ai/mlearning-ai-submission-suggestions-b51e2b130bfb) [## Mlearning.ai 提交建议

### 如何成为 Mlearning.ai 上的作家

medium.com](/mlearning-ai/mlearning-ai-submission-suggestions-b51e2b130bfb)