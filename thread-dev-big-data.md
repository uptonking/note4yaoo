---
title: thread-dev-big-data
tags: [big-data, thread]
created: 2023-04-19T07:30:03.445Z
modified: 2023-04-19T07:30:34.872Z
---

# thread-dev-big-data

# guide

# discuss-stars
- ## 

- ## 

- ## 🚀 [ClickHouse Keeper: A ZooKeeper alternative written in C++ | Hacker News _202309](https://news.ycombinator.com/item?id=37674967)
- 
- 
- 

- ## Hudi is considered as one of the open lakehouse table formats.
- https://twitter.com/Dipankartnt/status/1763400988210110667
- Hudi actually provides various "platform services" that extends Hudi's role from being just a table format to a comprehensive lakehouse platform.
- These services includes things like:
  - HudiStreamer for ingestion: ingest from different sources such as DFS or Kafka
  - Tools for snapshotting, exporting/importing Hudi tables
  - Commit notifications
  - Catalog support (Hive, Glue, BigQuery)
- If we break down the Hudi stack, this is what it looks like (bottom to top):
✅ Lake storage - cloud object stores (S3, ADLS, GCS)
✅ Open file format - Parquet, ORC & other data files that stores data
✅ Transactional database layer
  - Table format
  - Indexes
  - Concurrency control
  - Table services
  - Lake Cache, Metaserver (wip)
✅ Programming APIs - Writers, Readers
✅ User Interface
- Platform services - HudiStreamer (ingestion), catalog sync, admin CLI
- Query engine

- ## 🆚️ Spark was a short-lived anomaly. The future of data and analytics is very clearly Python and Rust.
- https://twitter.com/jdegoes/status/1762770034579931533
- Data scientists use Python. In the very uncommon cases when you need to extend Python, you can do so with C/C++ bindings, but that is not what data scientists do.
- mojo is in the Python bucket, to the extent it doesn't diverge.

- Check out Daft https://github.com/Eventual-Inc/Daft It’s a next gen Pyspark built in Rust!

- Wherever performance matters any JVM language is better than python. To speak about spark, it has come a long way. It is de facto standard for distributed parallel processing. I don’t think I need to explain well known pros of it.

- The end state for data is SQL(-like), the rest are SQL generating embedded DSLs. Projects converging to sql dsl: Spark, Kstreams, Flink, ...

- if you meant "spark will be replaced by another MapReduce library, with executors in Rust and apis for Python" - maybe
  - if you meant that Rust Data Engineer positions are going to become the norm - no. DE is built on cheap labor and Rust programmers aren't cheap

- rewriting should be easy considering that spark-core only has 18k lines of code, but it never happened. would you like give it a burl?

- ## 🎯 [2024 年，一个大数据从业者决定…… - 个人文章 - SegmentFault 思否_202401](https://zhuanlan.zhihu.com/p/675918720)
- 那会正是大数据如日中天的时代，我见到了很多用户例如招行、平安、微软等的如何使用大数据技术解决自己的业务问题；看到了 cloudera 和 hortonworks 两家hadoop 发行商是如何合并，以及大数据如何开始走向疲软的；
  - 也见证了云原生数仓时代 snowflake 的上市以其股价是如何逆天的。
  - 随后，clickhouse 如火如荼，mpp 技术又重新证明了自己，带动着数据库玩家们开始跑步进入大数据、数仓赛道。
  - 而 k8s 也逐渐成熟，云原生已然势不可挡，hadoop生态的大数据技术的正慢慢退潮
- 我将带着自己大数据多年的从业经验和围城外的视角，与大家复盘大数据的兴衰历史
- 💡 在我看来，大数据体系中最重要的的内容由四部分组成，分别是存储、计算、资源调度、数据目录 Catalog。后续我也会按照这个顺序一一探讨，今天的主角是存储技术。
- 在大数据领域，存储可以分为以下几类技术分别讨论：分布式文件系统/对象存储、存储格式、数据库/数据仓库、数据湖。
- 这 4 类技术彼此存在着密切的关系，通常要相互配合才能构建一个完整的存储系统：
  - 以 HDFS/S3 为代表的分布式存储作为大数据存储的基础架构，用于存储大规模的数据文件。
  - 列式存储格式（如 Parquet 和 ORC）用于对大规模数据进行高效的存储和查询
  - 数据库/数据仓库用于存储结构化和半结构化数据，是面向业务用户的接口，内部会视情况选择合适的存储格式和分布式存储。
  - 数据湖架构同样也是面向业务用户的接口，但与数据库不同，数据湖更强调开放的数据格式、灵活的数据访问，但交互式分析能力较弱。
- 其中分布式存储在其中扮演着核心的角色
  - 2007年，hadoop发布
  - 2010年，nosql兴起，云存储兴起
  - 2012年，hdfs和hbase成熟
  - 2015年，对象存储成为非结构化数据的理想选择
  - 2018年，大数据与ai结合
  - 2023年，hadoop退潮，s3成为云存储的事实标准
- 目前技术趋势已经统一在云存储、存算分离方向上，Hadoop 生态圈的一系列技术纷纷逃离 Hadoop、拥抱云原生，新兴的技术也在积极拥抱云原生，只是把 HDFS 作为一种 legacy 技术去做兼容

- Yahoo 内部的一拨人按照论文实现并开源了 Hadoop，Hadoop 的三驾马车 Yarn、MapReduce、HDFS。
  - 后来，资源管理的 Yarn 几乎被 k8s 取代了，分布式计算的 MapReduce 早就被 Spark 等技术淘汰了，只余下 HDFS 还在发挥着余热。
  - HDFS 的架构比较简单，是主从模式，早期版本通过多副本（一般是 3 副本）的方式实现了数据的高可用，后来加入了纠栅码能力节约存储资源。HDFS 还有一系列优势，例如高可靠、高容错、高吞吐、数据本地性等。然而，HDFS 还是没落了。
- 有这么几点原因：
- 第一，运维过于复杂。
  - 这不单单是 HDFS 的问题，是整个 Hadoop 体系的问题。
  - 举个例子：Hadoop 生态喜欢把配置文件分发到客户端，这就导致想要做配置变更、集群扩容、升级非常麻烦。
  - 此外，在搭建 HDFS 集群时，需要提前规划好集群的容量，否则后期扩容时会非常棘手。
- 第二，扩展性问题，尤其是 NameNode 的扩展性。
  - 由于 NameNode 是单点（虽然有主从模式保证高可用），而且整个文件系统的元数据都会存在 NameNode 的内存里，如果在集群搭建时给 NameNode 没有充足的内存资源，会使得整个集群文件量上限很低，也会严重影响 HDFS 的吞吐。
  - 而且 NameNode 作为集群的核心几乎不能出问题，否则整个文件系统会不可用，而 HDFS 是大数据生态的核心，一旦不可用，整个大数据系统就会停止工作。
- 第三，也是往往被人忽略的一个原因，那就是开发者的使用体验。开发者需要很懂 HDFS 的原理、配置，甚至早期只能使用 MapReduce 框架才能写出合格的程序，这非常劝退想把 HDFS 用好的开发者。

- 云存储是跟大数据同时代兴起的技术，云存储产品包含对象存储、文件存储、块存储等技术，但在大数据/数据库体系里被拿来替换 HDFS 的，就是以 S3 为代表的对象存储。
  - 从 2006 发布开始，S3 就以其低成本、可扩展性、高可用性、管理使用简单的特点吸引了很多应用开发者使用，用来存储图片、视频、文档等非机构化数据。
  - 随着 AWS 等云厂商的发力，开发了一系列软件包用来替换 HDFS，以及其真的能解决很多 HDFS 的痛点，尤其是随着存储成本进一步降低，存算分离的概念逐渐深入人心，像 HDFS 这类存算混合的方案渐渐没有了新引力。
  - 近几年很多新兴的云原生数据库、消息中间件直接就将对象存储作为了其存储介质，跨过了分布式文件系统这个过渡阶段。

- S3 也有其不可回避的各种问题：
  - 第一，查询延迟性能问题。由于要跨网络并且使用的是 Http 协议访问，很容易造成延迟过高。
  - 第二，早期版本的最终一致性问题。具体表现是写完一个文件后无法立刻查到，要等多久才能查到也是无法预期的，这造成了很多产品迟迟无法从 HDFS 生态迁移到 S3，在 2021 年时 S3 终于发布了新版本尝试了最终一致性的问题。
  - 第三，限流问题。S3本质上是一个 SaaS 云服务，出于自保护、成本、收费的考虑，有一系列限流的规则，可能会出现用着用着突然系统变慢了的情况。
  - 第四，不是一个完整的 POSIX 文件系统。当然，S3 在设计之初也没想过要支持完整的 POSIX 接口，只是大数据和数据库的开发者会不自觉地把之前的习惯带到云原生存储的使用上。习惯的力量是可怕的，像文件 rename、list 目录、获取目录大小这些在文件系统上轻量级的操作，使用 S3 之后会很慢。
  - 第五，各个云厂商的接口很割裂。虽然各个云厂商都有类似 AWS S3的对象存储接口，但是每个都有自己的特色，切换云厂商的时候势必要针对性的适配。
- 以上这些问题也都有相应的解决方案，例如 
  - JuiceFS 希望解决延迟、最终一致性、文件系统这类问题；
  - OpenDAL 想帮助开发者屏蔽各个云厂商的差异；
  - Alluxio 想帮助用户加速文件访问等。
- 现在回过头来看，S3 能战胜 HDFS 的原因有很多：存储价格下降、云厂商的大力推动、扩展性方面的原因，但最大的问题还是成本。
  - 保有一套 HDFS 系统不仅需要购买大量的物理机器，还要维护一个专业的运维团队，最终效果也不一定多好，对于很多公司来讲不是一个划算的事，相反按需购买、价格透明、可用性高达 11 个 9 的对象存储成为了更优的选择。

### [还在做 Hadoop 生态？那我祝你一帆风顺 - 知乎](https://zhuanlan.zhihu.com/p/677132057)

- 有了分布式存储解决了能不能存的问题之后，下一步就是怎么存的问题。使用哪种存储格式，取决于用户的使用场景
- 在早期大数据生态中，大家都是用纯文本例如 csv 存储数据，甚至有不少同学使用自己拼接的字符串存储。
  - 这就带来了很多显而易见的问题，例如存储效率不高，没有很好地使用压缩，读取时性能差，文件缺乏解释性很难复用。
  - 所以，2013年左右，当时两家著名的 Hadoop 发行商 Cloudera、Hortonworks 相继推出了自己的列式存储格式 parquet 和 orc
- 列式存储的优势现在看来也不是什么高科技的东西，但是在当时确实大大加速了分析效率。列存的优势是压缩率更高、查询时可以裁剪、支持灵活的 schema、对并行计算友好。
- 列存也不是全是优点，例如不适合频繁的更新、不支持随机访问、写入性能差等，这就让列存天然地适合分析场景，所以列存现在成了几乎所有 OLAP 数据库、数据湖的标配，但 OLTP 数据库几乎不会使用列存。

- 无论是文本格式的 csv 还是列存的 parquet，都是开放、标准的存储格式，有大量的生态兼容。
  - 但是大量的数据库、数据仓库出于性能、稳定性、兼容性等种种原因会使用自己独有的存储格式，这些文件只能通过对应的数据库读取，用户只能通过数据库的 API 访问数据。
  - 这也就是数据库和数据湖两类技术本质上的不同，一个更强调性能，一个更强调开放。

- HBase 是构建在 HDFS 之上的数据库，数据模型类似于 Google 的 Bigtable，旨在提供对大量结构化数据的快速随机访问。
  - Hadoop 生态有的问题像运维复杂、扩展困难、故障排查难等，HBase 一样不少，甚至 HBase 的存在会加重这些问题。
  - 但是，在 10 年代的前几年几乎没有更好的方案，能够同时满足高速查询、写入、海量数据、可扩展这些能力。
- HBase 既能满足高速的写入又能高速的查询，它用了什么格式。
  - 像 HBase 这类数据库一般会采用 KV 的存储格式，但又不是简单的 KV，而是自定义了一套 HFile 存储格式，并配套了一个存储引擎，包含索引、compaction、标记删除、内存表和磁盘数据管理等。
  - 虽然 HBase 技术逐渐式微，但它的设计理念深深的影响了其它分布式数据库，甚至现在还有几家云厂商把 HBase 魔改版本对外售卖。
- 与 HBase 同时代的还有 Cassandra，Cassandra 不在 Hadoop 体系内，是一个自成体系的数据库，实现了 Google BigTable 的论文。
  - 其最初由Facebook开发并开源，旨在解决大规模数据存储和处理的需求，具有高可用性、高性能和分布式的特点。
- 相比于 HBase 的主从结构，Cassandra 的设计受到了 Google 的 Bigtable 和亚马逊的 Dynamo 论文的启发，采用了分布式架构和基于列的数据模型。
  - Cassandra 使用了 P2P 的架构，整个集群没有 master 节点，基于 Gossip 协议实现的对等集群。
  - 这种设计的结果是放弃了强一致性，选择了可用性。此外, 如果客户端想读到最新的数据需要满足 W+R>N 的条件，这里 W 是写入的副本数，R 是读的副本数，N 是集群的节点数。
- 2012 年，Google 发布了 Spanner 论文，随后 NewSQL 这个品类开始进入技术圈的视野，先后有两款产品分别是 CockroachDB 和 TiDB，这些新产品完全跟 Hadoop 体系没有关系，尝试使用新的思路解决大数据中结构化数据的存储问题，同时 NewSQL 又再次把 SQL 带回了正轨，再次证明了 SQL 才是结构化数据的真爱。至此，大数据和数据库两个生态开始互相竞争又融合，SQL 也再次成为了数据接口的标准。

- AI 技术的持续火热，使得大量半结构、非结构化的数据亟待处理。
  - AI 的数据使用场景并不仅仅是简单的求和、最大最小值这类的数值计算，而是更复杂的神经网络、矩阵、向量计算，这类场景几乎不可能用 SQL 表达，一定是通过 Python 或其他语言的代码来实现。
  - 而且 AI 的计算往往不是使用 CPU 而是用 GPU
- 除了 AI 之外，分析领域也在快速发展，更灵活的数据使用方式需求量也越来越大，这就催生了数据湖技术。
- 数据湖技术从下到上依次是 对象存储 --> 存储格式 --> 开放的表格式 --> Catalog --> 计算引擎 和 存储引擎。
  - 目前主流的数据湖表格式有 3 个：Hudi、Iceberg、Delta Lake。三者各有优劣
- 无论哪项技术都对接了现有的 Spark、Flink、Doris、Clickhouse 等主流的计算引擎和 OLAP 数据库。
- 尽管开放的表格式(Open Table Format)相对于列式存储(Column based Data Format)，从技术视角只是多了一层元数据和基于时间戳的事务管理，这个小小的创新却带来了质的飞跃。
  - 在 Hive 的年代，数据库的元数据信息都存在 Hive 的 metastore 里，也就是存在 MySQL 里，可想而知随着数据表、分区、列、视图、用户等等这些元数据信息的爆炸，MySQL 就撑不住了。
  - 当访问元数据的并发量增加 MySQL 的单点瓶颈也会凸显。
  - 而开放的表结构优势是把元数据和数据放在一起，使得数据可以自解释，把元数据也视为一类大数据，这样大大扩展了系统的容量，元数据服务不再是瓶颈，开发者也可以更自由地访问。

- 对于一线的开发者而言该如何选择？
  - 云存储已经成为了事实标准，如果现在还有新人投入到 Hadoop 生态圈里，我只能送出真诚的祝福，并祝他一帆风顺。
  - 开放大于封闭，目前来看没有一个技术能完全解决所有用户的所有问题，那么无论是哪种技术、哪种方案都要把生态、集成作为重点考察的指标。
  - 分布式数据库和大数据融合，这两者的界限已经越来越模糊，机会还有很多。
  - 与 AI 结合的场景还有广阔的空间，结构化数据处理已经卷成红海，而AI更注重非结构化、半结构化数据的场景，还有很大的空白，向量数据库这一细分品类的出现就是很好的例子
  - 批流结合，大数据技术中批数据和流数据有时是两套架构，甚至两套技术栈，很割裂，现在已经有很多产品想将两者融合，给用户提供统一的使用体验。
# discuss-spark-alternatives
- ## 

- ## 

- ## 👣 @apple has replaced @ApacheSpark 's guts with @ApacheArrow DataFusion. And they're donating it.
- https://twitter.com/criccomini/status/1755012003503251890
  - This is an alternative to @MetaOpenSource 's Velox Spark implementation using cpp

- This is a great example of the composable data system concept that everyone seems to be talking about lately. In this case, using Spark's very mature planning and scheduling and delegating to DataFusion for native execution.
  - DataFusion is winning the OLAP query engine world... @andrewlamb1111 I think your vision is well on its way to become true

- I remember there was a project Gluten that was trying to make it all pluggable so you could swap out the native engine with velox or arrow based like datsfusion, wonder if this uses that or is separate. I guess if it's spark api compatible it doesn't matter from user perspective
  - This is an alternative to Gluten. Gluten is still an active project though. You are correct that it shouldn't really matter from the user's POV since these are all behind the Spark API.
- There are quite a few Spark accelerators now:
  - Databricks Photon
  - Spark RAPIDS
  - Gluten + Velox
  - DataFusion Comet
- Are you sure? This seems an alternative to Velox? Gluten had some stuff via substrait plans and stuff to generalize things so you could use Spark powered by Clickhouse, Velox, or Datsfusion, or RAPIDS/GPU. I don't think that's a goal of this project, right?
# discuss-hudi-iceberg-delta
- ## 

- ## 

- ## Apache Hudi’s WRITE operation - Under the Hood. 
- https://twitter.com/apachehudi/status/1764814812939202841
01. Deduplication:  Any duplicate record keys in the incoming batch are identified & addressed appropriately
02. Index Lookup: Next, an index lookup is performed to identify the file group an input record belongs to. For a new INSERT, this step returns no results
03. File Sizing: Then the file sizing algorithm will add sufficient records into a small file until it nearly reaches the configured maximum limit (via bin-packing)
04. Partitioning: Here the allocation of specific updates & inserts to existing or new file groups is determined
05. Write I/O: Actual writes happens here. Either the base file is created or an existing log file is appended to
06. Update Index: The Index is then updated to reflect the inclusion of new file groups, among other updates
07. Commit: Finally the changes are committed atomically
08. Clean: Following the commit, cleaning is initiated as required
09. Compaction: For MoR tables, compaction may run inline or be scheduled to execute asynchronously
10. Archival: Finally, an archival process is run, transferring old items from the timeline to an archive folder

# discuss
- ## 

- ## 

- ## Everything you ever wanted to know about data catalogs in @ApacheFlink SQL
- https://twitter.com/Decodableco/status/1759992559353430415
  - [Catalogs in Flink SQL—Hands On](https://www.decodable.co/blog/catalogs-in-flink-sql-hands-on)

- ## Voltron Data做了很多特别基础的活雷锋项目，像arrow, arrow flight, adbc, substrait之类的，都太基础了也没法在云上搞SaaS，
- https://twitter.com/niyue/status/1730253887356186951
  - 我一直没看懂他们怎么赚钱，现在出了一个GPU加速的引擎处理分析型和AI的计算负载，看起来是个直接和spark/presto竞争的分布式查询引擎，好像这个终于离养家糊口比较接近了

- ## TIL about Apache paimon a new table format for batch and streaming
- https://twitter.com/mim_djo/status/1726143809313198423
  - [Apache Paimon](https://paimon.apache.org/)

- ## TIL that a “data lake” is just an S3 bucket stuffed choke full o’ good ol’ csv files
- https://twitter.com/ChiefScientist/status/1724918222066159857
- And you put a table abstraction on top, that gets you a lakehouse
- It becomes a Data Ocean soon enough.
- Same with a data stream

- ## In ascending order of importance for Data Engineering:
- https://twitter.com/Ubunta/status/1718275186074730997
  01. Data Format
  02. Mutability (Mutable vs. Immutable Data)
  03. Logging Mechanisms
  04. Infrastructure Management
  05. Rapid Data Access with Governance
  - Each has become an industry in itself now

- ## nice talk about Umbra: A Disk-Based System with In-Memory Performance, 
- https://twitter.com/mim_djo/status/1657614372439744512
  - a perfect example for pure in-memory DB is #PowerBI vertipaq, very fast but very expensive too, 
- Was just thinking about this today while watching the LTT video about a 21 ssd (pcie g4 x2) carrier board. It gets competitive throughput with DRAM sticks...at about a $20k price tag, so way more than dram... The problem is that throughput matters a lot less than latency.

- ## 一段时间不见，clickhouse竟然有这么多重大特性
- https://twitter.com/li_taiyang/status/1648174437299265541
  - 理清了ast/query tree/plan/pipeline等阶段，支持连续join
- 初步集成三大数据湖：iceberg/delta-lake/hudi
