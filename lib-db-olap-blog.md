---
title: lib-db-olap-blog
tags: [blog, olap]
created: 2022-12-05T19:09:50.507Z
modified: 2023-12-15T17:59:59.688Z
---

# lib-db-olap-blog

# guide
- https://github.com/kangkaisen/olap-performance
  - https://perf.bcmeng.com/
  - 《OLAP 数据库性能优化指南》
  - 2025年将是我进入数据库领域的第十年，希望把自己十年内关于性能优化的经验总结分享下
  - 我和我的团队从零打造了 StarRocks 向量化执行器，CBO 优化器，Pipeline 并发引擎，打造出了一个全球领先的数据库查询引擎，希望把 StarRocks 性能优化的工程经验分享下
# blogs

## [Glaredb Storage Format_202309](https://datamonkeysite.com/2023/09/24/glaredb-storage-format/)

- I was messing around with GlareDB which is one of the new wave of OLAP DB system (With DuckDB, Datafusion and Databend) it is open source and based on Datafusion
  - Instead of building a new storage system from scratch, they just used Delta Table, basically they assembled a database using just existing components, apparently all glued together using Apache Arrow

- 🤔 So DB Vendors should stop innovating in Storage Format? 
  - I have to admit I changed my mind about this subject, I used to think Query Engines Developers  should design the best format that serve their Engine, after using Fabric for a couple of Months, open table format is just too convenient, my current thinking, the cold storage table format  make a lot of of sense **when using a standard format (Databricks-Delta, Iceberg, Hudi etc), the optimization can be done downstream**, for example tables statistics, In-Memory representations of the data, there are plenty of areas where DB vendor can differentiate their offering, but cold storage is really the common denominator(平均水平或标准).
  - One thing though I like about Delta is the relative Path. You can move around the folder and data keeps just working. Iceberg is a bit tricky as it does not support relative paths yet.

## [A Tale of Three Real-Time OLAP Databases: Apache Pinot, Apache Druid, and ClickHouse__202304](https://startree.ai/blog/a-tale-of-three-real-time-olap-databases)

## [Comparison of the Open Source OLAP Systems for Big Data: ClickHouse, Druid, and Pinot | by Roman Leventov__201802](https://leventov.medium.com/comparison-of-the-open-source-olap-systems-for-big-data-clickhouse-druid-and-pinot-8e042a5ed1c7)

# olap-model

## [Comparing Analysis Services tabular and multidimensional models | Microsoft Learn](https://learn.microsoft.com/en-us/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas?view=asallproducts-allversions)

- SQL Server Analysis Services (SSAS) provides several approaches, or modes, for creating business intelligence semantic models: Tabular and Multidimensional.

- Multidimensional mode is only available with SQL Server Analysis Services.
  - Multidimensional models will not be supported in Azure Analysis Services or Power BI Premium datasets. 

- This article is meant to provide a high-level comparison of multidimensional and tabular model constructs entirely in context of SQL Server Analysis Services.

- In SQL Server Analysis Services, having more than one approach enables a modeling experience tailored to different business and user requirements. 
  - 👉🏻 Multidimensional is a mature technology built on open standards, embraced by numerous vendors of BI software, but can be challenging to implement. 
  - 👉🏻 Tabular offers a relational modeling approach that many developers find more intuitive. 
  - In the long run, **tabular models are easier to develop and easier to manage**. 
  - While multidimensional models are still prevalent in many BI solutions, tabular models are now more widely accepted as the standard enterprise-grade BI semantic modeling solution on Microsoft platforms.

- Model features

- Data Considerations
- Compression
  - Both tabular and multidimensional solutions use data compression that reduces the size of the Analysis Services database relative to the data warehouse from which you are importing data.
  - An estimate used by many Analysis Services developers is that primary storage of a multidimensional database will be about one third size of the original data. 
  - Tabular databases can sometimes get greater amounts of compression, about one tenth the size, especially if most of the data is imported from fact tables.
- Size of the model and resource bias (in-memory or disk)
  - Tabular databases run either in-memory or in DirectQuery mode that offloads query execution to an external database. 
    - For tabular in-memory analytics, the database is stored entirely in memory, which means you must have sufficient memory to not only load all the data, but also additional data structures created to support queries.
  - Historically, the largest databases in production are multidimensional, with processing and query workloads running independently on dedicated hardware, each one optimized for its respective use. 
  - Tabular databases are catching up quickly, and new advancements in DirectQuery will help close the gap even further.
  - For multidimensional offloading data storage and query execution is available via ROLAP. On a query server, rowsets can be cached, and stale ones paged out. Efficient and balanced use of memory and disk resources often guide customers to multidimensional solutions.

- Query and scripting language support
  - Analysis Services includes MDX, DMX, DAX, XML/A, ASSL, and TMSL.
  - Tabular model databases support DAX calculations, DAX queries, and MDX queries. 
  - Multidimensional model databases support MDX calculations, MDX queries, DAX queries, and ASSL.
  - All databases support XMLA.

## [olap基础扫盲 - 知乎](https://zhuanlan.zhihu.com/p/400981139)

- 多维分析是一种数据分析过程，在此过程中，将数据分成两类：维度（dimensions)和度量(metrics/measurements)。
- 维度和度量的概念都出自于图论(graph theory)，维度指能够描述某个空间中所有点的最少坐标(coordinate)数，即空间基数；度量指的是无向图中顶点(vertices)间的距离。
- 在多维分析领域，维度一般包括字段值为字符类或者字段基数值较少且作为约束条件的离散数值类型；而度量一般包括基数值较大且可以参与运算的数值类字段，一般也称为指标。
- OLAP cube可以简单描述为“多维数据集”。cube，我们可以想象为数据指标根据多维度封装成的一个立方体结构（以三维空间为例，如果维度数超过3，我们则称为“Hypercube”）。
- 维度模型的概念出自于数据仓库领域，是数据仓库建设中的一种数据建模方法。维度模型主要由事实表和维度表这两个基本要素构成。
- 事实表是维度模型的基本表，用于存放大度量值，术语“事实”代表了一个度量值
- 事实表有两个或者两个以上的外关键字，外关键字用于连接到维度表的主关键字
- 维度表是事实表不可分割的部分。维度表包含有业务的文字描述。
  - 在一个设计合理的维度模型中，维度表会包含许多列或者属性，我们称之为维度属性
  - 维度表倾向于将行数做得相当少(通常少于100万行)，而将列数做得特别大。每个维度用单一的主关键字进行定义，主关键字是确保同一与之相连的任何事实表之间存在引用完整性的基础。
- 维度表是进入事实表的入口。
- 最后简单说明下维度表和事实表的融合。
  - 二者的融合也就是“维度模型”，“维度模型”一般采用“星型模式”或者“雪花模式”，
  - 而“雪花模式”可以看作是“星型模式”的拓展，表现为在维度表中，某个维度属性可能还存在更细粒度的属性描述，即维度表的层级关系。

- 常见的OLAP系统可以分为以下三类：关系型联机实时分析系统(Relational-OLAP，ROLAP)，多维联机实时分析系统(Multidimensional-OLAP，MOLAP)，混合型联机实时分析系统(Hybrid-OLAP，HOLAP)。

- ROLAP
  - ROLAP的核心依赖于关系型数据库，允许用户使用维度模型进行数据分析，将维度值存储在维度表中，将度量值存储在事实表中，通过关系型数据库访问数据，使用SQL进行查询分析。
  - ROLAP的一般使用模式概括如下：根据用户的需求，对不同维度进行分析后，将分析数据导入到另一张数据库表中。
- ROLAP的优势：
  - 处理高基数列具有更好的扩展性；
  - 擅长处理非聚合类的原始数据，生态圈内用于原始数据入库的ETL工具众多，同时比MOLAP入库速率更高；
  - 由于数据存储在关系型数据库中，所以支持标准SQL接口，查询便捷；
- ROLAP的劣势：
  - 工业界普遍认为ROLAP的性能要低于MOLAP。
  - 处理已聚合的数据，需要使用定制的ETL工具，开发量大且不具有通用性；如果采用原始数据入库，将非常影响查询性能，如果想要提升查询性能，需要将已入库的原始数据重新聚合后再导入到新的表中进行查询分析；
  - ROLAP的性能很大程度上依赖于使用的关系型数据库的查询与缓存性能；同时对于所有分析操作，都依赖于SQL语句，对于重计算类的分析模型，转换后的SQL就会变得复杂，对分析者的SQL语句的调优要求较高，而在某些无法使用SQL的场景下，ROLAP类产品则变得无能为力。

- MOLAP
  - MOLAP是OLAP的经典使用模式，所以经常用MOLAP来指代OLAP。
  - MOLAP和ROLAP具有一定的相似性，二者都可以使用维度模型进行数据分析，
  - 但是MOLAP并不将数据存储在维度表或者事实表中，而是对原始数据进行预计算（比如聚合操作），将计算结果存储在OLAP cube中。
- MOLAP的优势：
  - 由于MOLAP不采用关系型数据库进行数据存储，所以必须采用特殊的存储手段，例如：压缩存储、索引（例如位图索引）以及缓存技术等，查询速率更快；
- MOLAP的劣势：
  - 数据导入较慢，需要使用定制的ETL入库工具；
  - 由于没有维度表和事实表，所以对于更新操作以及明细查询，效率要比ROLAP低很多。

- HOLAP
  - HOLAP充分利用了ROLAP与MOLAP的各自优势，
  - 从纵向角度，既允许用户将部分数据（比如聚合类数据）使用MOLAP进行存储，从而获得更快的查询性能；又允许部分数据（比如原始数据）使用ROLAP进行存储，使用户能够查看细粒度数据。
  - 从横向角度，使用MOLAP存储最近较热的数据，从而提升查询性能；而使用ROLAP存储历史较冷的数据。

- 目前，商业类的OLAP产品更偏向于HOLAP，因为大厂既不想丢弃一直使用的关系型数据库，又想在数据分析能力上获得进一步提升，所以HOLAP类产品近几年也是百花齐放。

- OLAP的基本操作
- OLAP的操作是以查询——也就是数据库的SELECT操作为主，但是查询可以很复杂，比如基于关系数据库的查询可以多表关联，可以使用COUNT、SUM、AVG等聚合函数。
- OLAP正是基于多维模型定义了一些常见的面向分析的操作类型是这些操作显得更加直观。
- 钻取（Drill-down）：
  - 在维的不同层次间的变化，从上层降到下一层，或者说是将汇总数据拆分到更细节的数据，比如通过对2010年第二季度的总销售数据进行钻取来查看2010年第二季度4、5、6每个月的消费数据
- 上卷（Roll-up）：
  - 钻取的逆操作，即从细粒度数据向高层的聚合
- 切片（Slice）：
  - 选择维中特定的值进行分析，比如只选择电子产品的销售数据，或者2010年第二季度的数据。
- 切块（Dice）：
  - 选择维中特定区间的数据或者某批特定值进行分析，比如选择2010年第一季度到2010年第二季度的销售数据，或者是电子产品和日用品的销售数据。
- 旋转（Pivot）：
  - 即维的位置的互换，就像是二维表的行列转换，如图中通过旋转实现产品维和地域维的互换。

## [OLAP入门问答-进阶篇 - 知乎](https://zhuanlan.zhihu.com/p/147344996)

## [数据仓库系列：星型模型和雪花型模型 - 知乎](https://zhuanlan.zhihu.com/p/139656253)

- 星型模型：是一种多维的数据关系，它由一个事实表（Fact Table）和一组维表（Dimension Table）组成。
  - 每个维表都有一个维作为主键，所有这些维的主键组合成事实表的主键。
  - 事实表的非主键属性称为事实（Fact），它们一般都是数值或其他可以进行计算的数据
  - 多维数据集的每一个维度都直接与事实表相连接，所以数据有一定的冗余

- 雪花模型：当有一个或多个维表没有直接连接到事实表上，而是通过其他维表连接到事实表上时，其图解就像多个雪花连接在一起，故称雪花模型。
  - 雪花模型是对星型模型的扩展。它对星型模型的维表进一步层次化，原有的各维表可能被扩展为小的事实表，形成一些局部的 "层次 " 区域，这些被分解的表都连接到主维度表而不是事实表。
  - 通过最大限度地减少数据存储量以及联合较小的维表来改善查询性能。雪花型结构去除了数据冗余。

- 1、查询性能角度来看
  - 在OLTP-DW环节，由于雪花型要做多个表联接，性能会低于星型架构；
  - 但从DW-OLAP环节，由于雪花型架构更有利于度量值的聚合，因此性能要高于星型架构。
- 2、模型复杂度角度
  - 星型架构更简单方便处理
- 3、层次结构角度
  - 雪花型架构更加贴近OLTP系统的结构，比较符合业务逻辑，层次比较清晰。
- 3、层次结构角度
  - 雪花型架构更加贴近OLTP系统的结构，比较符合业务逻辑，层次比较清晰。

- 根据项目经验，一般建议使用星型模型。因为在实际项目中，往往最关注的是查询性能问题，至于磁盘空间一般都不是问题。
  - 当然，在维度表数据量极大，需要节省存储空间的情况下，或者是业务逻辑比较复杂、必须要体现清晰的层次概念情况下，可以使用雪花型模型。

## [数据仓库中的两大经典模型 - 知乎](https://zhuanlan.zhihu.com/p/449842419)

- 星型模型由一个事实表和一组维表组成，是一种多维的数据关系。
  - 里面的每个维表都有一个维作为主键，所有这些维的主键组合成事实表的主键。
  - 强调的是对维度进行预处理，将多个维度集合到一个事实表，形成一个宽表。所以在使用hive时，经常会看到一些大宽表的原因。
  - 大宽表属于事实表，包含了维度关联的主键和度量信息，而维度表则是事实表里面维度的具体信息，使用时候一般通过join来组合数据，相对来说对OLAP的分析比较方便。

- 当在星型模型中，有一个或多个维表没有直接连接到事实表上时，而是通过其他维表连接到事实表上时，其图解就像多个雪花连接在一起，故称雪花模型。
  - 雪花模型是对星型模型的扩展。也是对星型模型的维表进一步层次化，原有的各维表可能被扩展为小的事实表，形成一些局部的 "层次 " 区域，这些被分解的表都连接到主维度表而不是事实表。
  - 雪花模型更加符合数据库范式，减少数据冗余，但是在分析数据的时候，操作比较复杂，需要join的表比较多所以其性能并不一定比星型模型高。

- 星型模型的设计方式主要带来的好处是能够提升查询效率。因为生成的事实表已经经过预处理，主要的数据都在事实表里面，所以只要扫描实时表就能够进行大量的查询，而不必进行大量的join，其次维表数据一般比较少，在join可直接放入内存进行join以提升效率，除此之外，星型模型的事实表可读性比较好，不用关联多个表就能获取大部分核心信息，设计维护相对比较简答。
  - 雪花模型的设计方式是比较符合数据库范式的理念，设计方式比较正规，数据冗余少，但在查询的时候可能需要join多张表从而导致查询效率下降，此外规范化操作在后期维护比较复杂。
# query-language-mdx/dax

## [DAX for multidimensional models in SQL Server Analysis Services](https://learn.microsoft.com/en-us/analysis-services/multidimensional-models/dax-for-multidimensional-models?view=asallproducts-allversions)

- This article describes how Power BI uses DAX (Data Analysis Expressions) queries to report against multidimensional models in SQL Server Analysis Services.

- Historically, reporting applications use MDX (Multidimensional Expressions) as a query language against multidimensional databases. 
- MDX is optimized for common visual patterns like PivotTables in Excel and other reporting applications that target multidimensional business semantics. 
  - Beginning with SQL Server 2012 SP1, Analysis Services supports using both DAX and MDX against multidimensional and tabular models. 
- DAX, however, was originally designed for tabular data models. 
  - While DAX is considered easier to use, it's also more focused on simpler data visualizations like tables, charts, and maps in reports and dashboards. 
  - Power BI uses DAX to query both tabular and multidimensional models.

- Because DAX is primarily designed for tabular models, there are some interesting and useful mappings, and constraints, that must be understood when using DAX against multidimensional models.

- DAX is not a subset of MDX. 
  - DAX was initially designed to be similar to the Excel formula language. 
  - In tabular models, DAX is used against a relational data store comprised of tables and relationships. 
  - DAX is also used to create custom measures, calculated columns, and row-level security rules.
- In addition to being a calculation language, DAX can also be used to execute queries. 
  - This article describes how DAX queries work against a multidimensional model.

- DAX expressions are supported only within tabular models. You cannot use measures created by a DAX expression in a multidimensional model.

- Analysis Services provides a tabular model metadata representation of a multidimensional model. 
  - Objects in a multidimensional models are then represented as tabular objects in Power BI.

## [Comparing tabular model DAX with multi-dimensional MDX](https://www.wiseowl.co.uk/blog/s1450/dax-versus-mdx.htm)

- Suppose that we want to show the total value of transactions in a pivot table (that is, we want to sum Price * Quantity)

```shell
#  typical DAX expression, giving total price * quantity.
Total value:=sumx('Transaction', [Price]*[Quantity])

# A measure in MDX to create the expression for summing.

create member currentcube.measures.[Amount] as [Measures].[Price] * [Measures].[Quantity]
```

## [DAX vs MDX — Is there any difference? | by Muhammad Asif | Medium](https://medium.com/@masifsharif/dax-vs-mdx-is-there-any-difference-9d2d9f199df9)

- Will DAX Kill MDX?
  - Actually, NO. DAX might be termed as the future, but MDX isn’t going away anywhere in the least foreseeable future.
  - Imagine DAX as an extension of the Excel formulas that can be used to calculate against a PowerPivot dataset.
  - DAX also supports many MDX functions like TotalYTD, ParallelPeriod, to name a couple.

## [BI: Multidimensional vs In-Memory (MDX vs DAX)](https://www.tickboxsystems.com/bi-analytics/bi-mdx-vs-dax/)

- Microsoft technology provide both traditional OLAP using the standard SQL-like language MDX, as well as in-memory BI using their proprietary language DAX
- From 2014, DAX caught up and then overtook MDX, especially under Business & Industrial
# more-blog
- [Vectorization in OLAP Databases — tech ramblings](https://aneesh.mataroa.blog/blog/vectorization-in-olap-databases/)
