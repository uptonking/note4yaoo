---
title: note-mapreduce-dev
tags: [mapreduce]
created: '2020-09-27T03:53:35.087Z'
modified: '2020-09-27T03:58:20.682Z'
---

# note-mapreduce-dev

## pieces

- MapReduce框架其实包含5个步骤：Map、Sort、Combine、Shuffle、Reduce
  - 这5个步骤中最重要的就是Map和Reduce，这也是Spark中非常重要的两步
    - Map步骤是在不同机器上独立且同步运行的，它的主要目的是将数据转换为 key-value 的形式；
    - Reduce步骤是做聚合运算，它也是在不同机器上独立且同步运行的。
    - Map和Reduce 间夹杂着一步数据移动，也就是 shuffle，这步操作会涉及数量巨大的网络传输（network I/O），需要耗费大量的时间。 
    - 由于MapReduce的框架限制，一个MapReduce任务只能包含一次Map和一次Reduce，计算完成之后，MapReduce会将运算结果写回到磁盘中（更准确地说是分布式存储系统）供下次计算使用。
    - 如果所做的运算涉及大量循环，那么整个计算过程会不断重复地往磁盘里读写中间结果。这样的读写数据会引起大量的网络传输以及磁盘读写，极其耗时，而且它们都是没什么实际价值的废操作。因为上一次循环的结果会立马被下一次使用，完全没必要将其写入磁盘。
    - 整个算法的瓶颈是不必要的数据读写，而Spark主要改进的就是这一点
  - Spark延续了MapReduce的设计思路：对数据的计算也分为Map和Reduce两类。
    - 但不同的是，一个Spark任务并不止包含一个Map和一个Reduce，而是由一系列的Map、Reduce构成。
    - 这样，计算的中间结果可以高效地转给下一个计算步骤，提高算法性能。
    - 虽然Spark的改进看似很小，但实验结果显示，它的算法性能相比MapReduce提高了10～100 倍。

- MapReduce vs Spark
  - MapReduce通常需要将计算的中间结果写入磁盘，然后还要读取磁盘，从而导致了频繁的磁盘IO。
  - Spark则不需要将计算的中间结果写入磁盘，这得益于Spark的RDD（弹性分布式数据集，很强大）和DAG（有向无环图），
    - 其中DAG记录了job的stage以及在job执行过程中父RDD和子RDD之间的依赖关系。
    - 中间结果能够以RDD的形式存放在内存中，且能够从DAG中恢复，大大减少了磁盘IO。
  - ref
    - [为什么Spark比MapReduce快？](https://www.zhihu.com/question/31930662)

- Photon Powered Delta Engine是一个100%与Apache Spark兼容的矢量化查询引擎，旨在利用现代CPU架构实现极快的数据并行处理。
  - 该引擎使用C++从头开始编写，以利用现代硬件并利用数据级和CPU指令级并行性，优化了文本处理和正则表达式，以实现对真实数据和应用程序的快速性能。
  - 它与 Apache Spark™API 完全兼容，确保工作负载在不更改代码的情况下无缝运行。
  - 微软研究人员运行了30TB TPC Benchmark DS(TPC-DS)，行业标准基准测试来测量处理速度，发现Photon Powered Delta引擎比Spark 2.4快20倍。
  - Native Execution Engine (Photon): 
    - 100% Apache Spark-compatible vectorized query engine designed to take advantage of modern CPU architecture for extremely fast parallel processing of data
