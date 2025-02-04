---
title: lib-db-app-blog-arch-kappa
tags: [blog, database, kappa-architecture]
created: 2023-12-03T07:14:06.903Z
modified: 2023-12-03T07:21:27.015Z
---

# lib-db-app-blog-arch-kappa

# guide

# blogs-streaming

## [From Samza to Flink: A Decade of Stream Processing _202402](https://materializedview.io/p/from-samza-to-flink-a-decade-of-stream)

- 👥 https://twitter.com/criccomini/status/1759958636024181091
  - Why Samza failed, how it led to Kafka Streams and Kafka Connect, and why I'm skeptical of Apache Flink.
- Agree 100% that Flink is suffering from feature bloating. And a sad part is that some core fundamentals don't always work , especially on large-scale jobs. I would prefer much less features, but having rock solid base functionality.
- I think if you can have Flink capabilities without having to deal with its complexities, it is a win
# blogs
- [三张图讲清楚大数据基础设施Hadoop、Lambda、kappa架构 - 知乎](https://zhuanlan.zhihu.com/p/337520151)
  - 第一代基础设施：以Hadoop为代表的离线数据处理。
    - 底层以HDFS分布式文件系统做数据存储，所有的数据都通过MapReduce计算模型进行处理
  - 第二代基础设施：以Lambda为代表的流批数据处理。
    - 通过把数据分解为ServingLayer、SpeedLayer、BatchLayer三层来解决在不同数据集的数据需求。
    - 优点是将流处理和批处理分开，很好的结合了实时计算和流计算的优点，架构稳定，实时计算成本可控，提高了整个系统的容错性、降低了复杂性。
    - 缺点是离线数据和实时数据很难保障数据的一致性，开发人员需要维护两套系统。
  - 第三代基础设施：以Kappa为代表的集成流批数据处理。
    - Lambda架构的流批分离解决了数据一致性问题，也提高了效率，但对应的也增加了系统的复杂性。
    - Kappa架构利用流计算的分布式特征，增加流计算的并发性，加大流数据的时间窗口，统一批处理和流处理数据。
    - Kappa架构在Lambda架构的基础上删除了Batch层，所有的数据都是流处理实时计算，计算好了之后可以直接给到业务层使用，也可以放在数据湖中，需要进行离线分析时使用。
    - Kappa架构的优点是开发人员只需要维护实时处理模块，不需要离线实时数据合并，
    - 缺点是在实时处理时可能会存在信息丢失情况。

- [Flink architecture and execution engine - Practical Real-time Data Processing and Analytics [Book]](https://www.oreilly.com/library/view/practical-real-time-data/9781787281202/e1aa468d-c22d-4dc3-afce-498a084c1ee3.xhtml)
  - The core of Flink is a streaming dataflow engine. 
  - Flink is based on Kappa architecture. 
  - Kappa architecture was introduced in 2014 by Jay Kreps

- [Apache Flink 101: Understanding the Architecture](https://techlake.dev/apache-flink-101-understanding-the-architecture)
  - In Kappa architecture, batch processing is a special case of stream processing hence it is able to perform both batch and real-time processing, especially for analytics, with a single technology stack.
  - Apache Flink is built on Kappa architecture hence it excels at processing unbounded and bounded data sets.

- [实时数仓之 Kappa 架构与 Lambda 架构 - 知乎](https://zhuanlan.zhihu.com/p/584255261)

- [Kappa Architecture 1:1 - How to Build a Modern Streaming Data Architecture?](https://nexocode.com/blog/posts/kappa-architecture/)

## [Using Kappa Architecture to Reduce Data Integration Costs - Striim](https://www.striim.com/blog/using-kappa-architecture-to-reduce-data-integration-costs/)

- 🐛 Drawbacks of kappa architecture
- The complexity of setting up and maintaining a kappa architecture can be very high, requiring specialized engineers to ensure that all components are properly configured and functioning correctly. 
  - Additionally, without a centralized system for managing data, it can be difficult for businesses to maintain data governance across their organization. 
  - This lack of centralization also means that each component must be independently managed, leading to higher costs in terms of additional computing resources.
- Another limitation of kappa architecture is scalability. 
  - As more data is processed through the system, it will require more computing resources in order to remain efficient and effective. 
  - This makes scaling the architecture complex and costly, as businesses will need to invest in additional hardware or cloud computing services in order to handle larger volumes of data processing.
- kappa architectures are not suitable for all types of data processing tasks. 
  - While they are well suited for near-real-time analytics applications, they may not be the best choice for batch processing jobs or those that require intensive computation or machine learning algorithms. 
  - It’s important for businesses to assess their individual needs before deciding if kappa architectures are the right choice for reducing their data integration costs.
# blogs-usecase

# more
