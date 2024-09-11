---
title: toc-lib-data-processing
tags: [data-processing, lib, toc]
created: 2020-12-31T15:33:05.382Z
modified: 2021-05-13T16:14:15.415Z
---

# toc-lib-data-processing

# guide

# popular
- https://github.com/jinyus/related_post_gen
  - Data Processing benchmark featuring Rust, Go, Swift, Zig etc.
  - Given a list of posts, compute the top 5 related posts for each post based on the number of shared tags.
# data-model
- https://github.com/apache/arrow
  - https://github.com/apache/arrow/tree/master/js /ts
   - Apache Arrow is a columnar memory layout specification for encoding vectors and table-like containers of flat and nested data. 
  - The Arrow spec aligns columnar data in memory to minimize cache misses and take advantage of the latest SIMD (Single input multiple data) and GPU operations on modern processors.
  - 👉🏻 Apache Arrow is the emerging standard for large in-memory columnar data (Spark, Pandas, Drill, Graphistry, ...). 
    - By standardizing on a common binary interchange format, big data systems can reduce the costs and friction associated with cross-system communication.

- https://github.com/onetable-io/onetable /apache2/202311/java
  - https://github.com/onetable-io/onetable
  - OneTable is an omni-directional converter for table formats that facilitates interoperability across data processing systems and query engines. 
  - Currently, OneTable supports widely adopted open-source table formats such as Apache Hudi, Apache Iceberg, and Delta Lake.
# data-tools
- https://github.com/malloydata/malloy
  - https://www.malloydata.dev/
  - Malloy is an experimental language for describing data relationships and transformations.
  - Each query you write in Malloy is a building block for the next level of understanding. 
  - https://djouallah.github.io/composer/

- https://github.com/dbt-labs/dbt-core /python
  - https://getdbt.com/
  - dbt enables data analysts and engineers to transform their data using the same practices that software engineers use to build applications.
  - Analysts using dbt can transform their data by simply writing select statements, while dbt handles turning these statements into tables and views in a data warehouse.
  - dbt makes it easy to manage relationships between models(select statements), and visualize these relationships

- https://github.com/uwdata/arquero
  - https://uwdata.github.io/arquero
  - /438Star/BSD/202105/js
  - a JavaScript library for query processing and transformation of array-backed data tables. 
  - Following the relational algebra and inspired by the design of dplyr, Arquero provides a fluent API for manipulating column-oriented data frames.
  - Arquero supports a range of data transformation tasks, including filter, sample, aggregation, window, join, and reshaping operations.
  - query over arrays, typed arrays, array-like objects, or Apache Arrow columns.

- https://github.com/yifanwu/diel
  - a declarative framework for scaling up your interactive visualizations with... SQL! (and some timesteps)
# data-wasm
- https://github.com/pyodide/pyodide /12kStar/MPLv2/202409/python/c/ts
  - https://pyodide.org/en/stable/
  - Pyodide is a Python distribution for the browser and Node.js based on WebAssembly
  - Pyodide is a port of CPython to WebAssembly/Emscripten.
  - Pyodide makes it possible to install and run Python packages in the browser with micropip. Any pure Python package with a wheel available on PyPi is supported. 
  - Pyodide comes with a robust Javascript ⟺ Python foreign function interface so that you can freely mix these two languages in your code with minimal friction
  - [Related Projects](https://github.com/pyodide/pyodide/blob/main/docs/project/related-projects.md)
    - https://github.com/jupyterlite/jupyterlite
    - https://github.com/gzuidhof/starboard-notebook
    - https://github.com/iodide-project/iodide

- https://github.com/pyscript/pyscript
  - https://pyscript.net/
  - PyScript is a framework that allows users to create rich Python applications in the browser using HTML's interface and the power of Pyodide, WASM, and modern web technologies.

- https://github.com/finos/perspective
  - A data visualization and analytics component, especially well-suited for large and/or streaming datasets.
# ref
- [Apache Arrow简介](https://zhuanlan.zhihu.com/p/339132159)
  - 由于历史原因，Snowflake一直使用了JSON作为结果集（ResultSet）的序列化方式，引起了许多问题。
    - 首先，JSON的序列化/反序列化的成本实在是太高了：
      - 许多cpu cycle都被浪费在了字符串和其他数据类型之间的转换。
      - 不仅仅是cpu，内存的消耗也是十分巨大的，尤其像是Java这样的语言，对内存的压力非常大。
    - 其次，使用JSON进行序列化，会导致某些数据类型（浮点数）的精度丢失。
  - 经过研究，我们最终决定采用Apache Arrow作为我们新的结果集序列化方式
  - Apache Arrow定义了一种在内存中表示tabular data的格式。
    - 这种格式特别为数据分析型操作（analytical operation）进行了优化。
    - 比如说列式格式（columnar format），能充分利用现代cpu的优势，进行向量化计算（vectorization）。
    - 不仅如此，Arrow还定义了IPC格式，序列化内存中的数据，进行网络传输，或者把数据以文件的方式持久化。
  - Arrow定义的格式是与语言无关的，所以任何语言都能实现Arrow定义的格式。
    - arrow项目为几乎所有的主流编程语言提供了SDK
  - arrow其实和protobuf很像，可是两者的使用场景却很不一样。
    - protobuf是为了structured data提供内存表示方式和序列化方案。
    - protobuf主要是序列化structured data，有很多的键值对和非常深的nested structure。
    - arrow序列化的对象主要还是表格状数据。
  - arrow在内存中表示数据的最基本单元是array，它代表了一连串长度已知、类型相同的数据。
    - 而多个长度相同、类型相同或者不同的array就可以用来表示结果集（或者一部分的结果集）
    - arrow限制了array的最大长度，当结果集（或者表）的大小超过了array的最大长度，就需要把结果集水平切分成多个有序集合。
  - 多个长度相同的array组成的有序集合可以用来表示结果集的子集（或者部分的表），arrow称这个有序集合为Record Batch
    - Record Batch也是序列化的基本单元。
    - arrow定义了一个传输协议，能把多个record batch序列化成一个二进制的字节流，并且把这些字节流反序列化成record batch，从让数据能在不同的进程之间进行交换。
  - 在传统的编程世界中，数据只存放与oltp database中（比如说MySQL），application通过JDBC或者ODBC等标准接口和数据库进行交互。
  - 现在数据的使用场景也越来越复杂，arrow适用的场景可能有一下几个：
    - 同一个系统，多个节点：
      - 由于云计算的普及，数据库上云也得到了越来越多的关注。
      - 在一个分布式数据库的实现中，可能会有许多的query executor节点并行产生结果集。
      - arrow的格式可以让客户端并行读取各个节点产生的结果集。
    - 多个系统可能会同时读取同一份数据：
      - 企业可能会需要data warehouse生成报表，需要spark做一些机器学习。
      - 为了能让不同的系统之间进行数据的交互，企业经常把数据以文件的形式存放于一些分布式的文件系统（AWS S3）之上。

- [什么是内存内计算 (In-Memory Computing)，这是未来高效计算的趋势吗？](https://www.zhihu.com/question/24519772/answers/updated)
  - 从Hadoop到Spark；从HDFS到Alluxio；
    - 再到现在Arrow的出现，可以让不同计算引擎、计算库共享内存中的数据结构。
  - 从一级缓存取一个block的数据只要0.5纳秒，而从内存取一个block则需要100纳秒

- [2019年大数据的发展趋势](https://zhuanlan.zhihu.com/p/81946004)
  - **趋势1：Apache Arrow和Arrow Flight的崛起**
  - Arrow定义了用于处理数据的内存列存储格式以及对应的低级别操作库，
    - 如针对特定运行时环境进行高度优化的sorts, filters, and projections操作。这些操作的资源利用率更高更快。
  - Arrow用于许多类型的应用程序，包括SQL引擎（如Dremio的Sabot），数据框架（例如，Python pandas），分布式处理（例如Spark），数据库（例如InfluxDB），机器学习环境（例如RAPIDS）和一些可视化系统。
  - 这些软件应用程序使用Arrow 的驱动，不仅来自于速度和效率的提升，还可以使得多个使用Arrow的系统间自由进行数据交换。
    - 当两个系统都实现Arrow时，可以在不对数据进行序列化和反序列化的情况下进行数据交换，且避免了不必要的复制，从而释放CPU，GPU和内存资源
  - Arrow Flight，这是应用程序与Arrow交互的新方式。
    - 你可以将Flight视为ODBC/JDBC的替代方案，用于内存分析。
    - 现在我们已经建立了一种在内存中表示数据的方法，Flight则定义了一种在系统之间交换数据的标准化方法。
  - 一旦 Arrow Flight 普遍可用，实现 Arrow 的应用程序可以直接使用 Arrow 缓冲区。
    - 在我们的内部测试中，我们观察到与 ODBC\/JDBC 接口相比，这种方法的效率提高了10倍-100倍。
  - **趋势2：数据即服务**
  - 数据目录（Data catalog）：全面的数据资产清单，数据使用者可以轻松地跨不同系统和来源查找数据，以及按对业务有意义的方式描述数据。
  - 数据管理（Data curation）：用于过滤，整合和转换数据的工具。将可重用数据集添加到数据目录中以供其他用户使用。某些部署可以使用虚拟数据集实现数据管理，将数据副本降到最少。
  - 数据血缘（Data lineage）：在从不同系统访问数据集并创建新数据集时，跟踪数据集的出处和血缘的能力。
  - 数据加速（Data acceleration）：数据加速让用户可以快速、交互式访问大型数据集。如果查询需要几分钟才能处理，则用户无法有效地执行其工作。

  数据虚拟化（Data virtualization）：企业数据存在于许多不同的系统中，包括数据仓库，数据湖和操作系统。它提供了一种统一的原位访问数据的方法，用户无需将所有数据复制到新的孤岛中。

  - SQL执行（SQL execution）： SQL仍然是数据分析的事实标准。每个BI工具和每个数据科学平台都支持SQL作为从不同来源访问数据的主要方法。数据即服务提供SQL作为这些工具和系统的接口。
  - **趋势3：云数据湖**
  - 每个供应商都为数据仓库和数据集市提供了替代方案：AWS上的Redshift，Azure上的SQL数据仓库和Google上的BigQuery。还有独立产品，如Snowflake，支持多个云平台。
  - 云数据湖将作为基础设施：
    - 数据首先以原始形式存在，包括旧应用程序和流式数据（Stream Data）
    - 根据不同需求对数据进行转换，丰富和整合
    - 数据用于数据科学场景
    - 数据被加载到云数据仓库中
  - 企业正在利用多种技术构建云数据湖：AWS上的S3，Azure上的ADLS和用于存储数据的Google云存储。
    - 对于数据处理，企业使用多种选项，包括Spark，Hive，AWS Glue，Azure Data Factory和Google Cloud Dataflow。
    - 其他功能将继续出现，例如与Kafka等流式平台以及数据目录和数据准备工具更紧密的集成。
    - 即使是最基本的形式，对于将迁移到云的企业而言，云数据湖也将成为基础系统。
