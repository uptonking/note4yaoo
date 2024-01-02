---
title: lib-db-olap-community
tags: [community, olap]
created: 2022-12-05T19:10:03.490Z
modified: 2023-12-15T18:01:43.992Z
---

# lib-db-olap-community

# guide

# discuss-stars
- ## 

- ## 

- ## The One Billion Row Challenge
- https://twitter.com/gunnarmorling/status/1741839724933751238
  - How fast can YOU aggregate 1B rows using modern #Java? Grab your threads, flex your SIMD, and kick off 2024 true coder style by joining this friendly little competition
  - Submissions must be written in #Java (see FAQ: https://github.com/gunnarmorling/1brc#faq), so JNI won't work as you'd need some C glue code. But there might be more modern alternatives which may let you do what you're after

# discuss
- ## 

- ## 

- ## 

- ## [The Rise and Fall of the OLAP Cube (2020) | Hacker News_202107](https://news.ycombinator.com/item?id=27736713)
- Modern data warehouses don't need to build cubes for performance reasons. 
  - Low latency data warehouses like ClickHouse or Druid can aggregate directly off source data. 
  - The biggest driver for modeling is allowing non-coders to access data and perform their own analyses. 
  - I don't see that problem ever going away. Cube modeling with dimensions and measures solves it well.

- OLAP Cube is not dead, as long as you use some form of:
  1. GROUP BY multiple fields (your dimensions), or
  2. partition/shuffle/reduceByKey
  - and materializing/caching the result of this query for later reuse, you are rolling your own OLAP Cube with whatever data processing ecosystem you have on hands.
  - The technology itself has clear use cases and incredible business value on a daily basis, only implementation details differ depending on surroinding ecosystem

- I'm a bit opinionated on data modelling, so a couple points.
1. "OLAP Cubes" arguably belong to Microsoft and refer to SQL Server cubes that require MDX queries. It's a solution given to us by Microsoft that comes with well understood features.
2. OLAP Cubes started to decrease in population in 2015 (I'd argue).
3. Any solution to fixing "OLAP" that comes from a commercial vendor is suspicious. As painful as Kimbal & Inmon are, they are ideas that don't require vendor lock in.
4. At my current company, we recently wrapped up a process where we set out to define the future of our DW. The end result looks eerily close to Kimball but with our own naming conventions.
5. Columnar databases are so pervasive(无处不在的) these days that you should no longer need to worry about a lack of options when choosing the right storage engine for your OLAP db.
6. More and more data marts are being defined by BI Teams w/little modeling/CS skills. To that end, I think it's important to educate your BI teams as a means to minimize the fallout, and be accommodating in your DW as means to work efficiently with your BI teams. This is to say settle on a set of data modelling principles that work for you, but may not work for someone else.

- Snowflake is the cubeless column store.
- The OLAP cube needs to come back, as an optimization of a data-warehouse-centric workflow

- A data warehouse is always “OLAP” but it isn’t often a “cube”.
- The difference as I understand it is that a cube specifically is the multidimensional schema definition of your data set. So for instance typically in an OLTP system you’d have customer data, product data, sales data, performance data, etc. Usually that data is in separate tables.
  - OLAP is the combined methods that allow you to analyze the data, roll it up, aggregate it, combine it across dimensions etc. Usually by using a star schema.
  - A OLAP Cube, then, is the full multidimensional schema and relations of all the data. Typically a cube lets you define how each type of field is aggregated, whether it’s summing count fields, averaging dollar fields, or special rules for date fields etc. In addition you specify hierarchies of the data

- I never liked OLAP cubes because they discouraged ad-hoc data exploration since if there wasn't already a cube that modeled the data a certain way you couldn't do it. You had to develop it, or hope a DBA had time to develop it sometime in the next two months. They were fine if you already knew the questions you needed answered, but they probably contributed to some companies focussing on the wrong things because they couldn't easily explore data for new insights.
  - This is why sometimes you end up with BOTH a traditional ETL data warehouse, for common, structured reporting and analytics and also an unstructured data lake(s) that pull raw data in from many sources to allow for ad-hoc exploration.
- I think OLAP cubes are falling out of fashion because traditional BI and reporting in general is falling out of fashion. With self-service BI tools like looker and other tools, Business folks are running more adhoc queries than traditionally piped data through ETL processes.

- 👉🏻 We still use MDX. Did some testing with DAX, but I don't believe its step in the right direction. As for tools, we mostly use in-house tools build either on Mondrian or connecting to MS Analysis Services trough XMLA - depending on the use case.

- i think the article misses a big point parametric queries
  - cubes whether tabular (columnar database) or multidimensional provide a language mdx or dax, that basically allows parametric measures (or queries)
  - which is essential in data analysis
  - sql for now, doesnt allow parametric functions or queries in the same way dax or mdx does

- ## do you think in the long term for OLAP DB, native storage format will basically disappear and will be replace by OSS Table format like #DeltaTable and #Apacheiceberg etc
- https://twitter.com/mim_djo/status/1715544800840269854
- Why not an open source OLAP-optimized native format?
  - I thought that is Delta table raison

- ## I've been advocating to add measures (columns whose value is evaluated as a context-sensitive expression) to SQL's data model. 
- https://twitter.com/julianhyde/status/1674128899977154562
  - Is there a similar concept in the data frames world (R, Pandas, Spark, ...)?
- Isn’t it what “the semantic layer” is trying to address as an additional layer
  -  remain to be convinced that the "semantic layer" is anything but a few bits of fluff
- [Power BI: Custom Column Vs Calculated Column | Power BI](https://devoworx.net/custom-column-vs-calculated-column-power-bi/)

- ## @StarRocksLabs just released version 3, Big change, from sharing nothing to shared disk
- https://twitter.com/mim_djo/status/1658675242930442241

- ## 💡 Why Analytical Tools don't speak native SQL ? that's the Mother of all questions.
- https://twitter.com/mim_djo/status/1656450400051171329
  - [Cubing and Metrics in SQL, Oh My! - YouTube](https://www.youtube.com/watch?v=oo1uwJ3qHwE)

- BI tools implement their own language on top of SQL. Why not SQL?

- SQL vs BI
  - semantic model
  - define reusable calculations
  - pre-join tables
  - control presentation / viz
  - governance
  - ask complex question in a concise way

- semantic models vs databases
- a semantic model
  - is the place to share data and calculations
  - needs a good query language
  - doesnot become a database just because it speaks sql
  - should do more things like permissions/transform

- use semantic model to avoid being tied to one vendor db

- I have the conservative view that it is a solution searching for a problem, we will always have another layer that generate SQL, but SQL will not take over BI

- and to share @cwebb_bi cynical view, if SQL was such a good thing for measures, we would have a good solution by now
- so we have three camps 
  - 1- SQL with extension @julianhyde (MDX)
  - 2- DSL that generate SQL (Malloy, dbt, Tableau etc) @lloydtabb
  - 3- Microsoft, nope, you don't need SQL, we build our own Calculation Engine :) @jwang_pbi
- Obviously you have another camp, the SQL fanatics like @felipehoffa @teej_m @pdrmnvd , you don't need a model at all, you write everything by hand 🤡

- Back in the day, camps 2 and 3 used to be called ROLAP and MOLAP

- ## We've been working on, Malloy, a new experimental data language.  If you work in SQL, we'd love your feedback._202110
- https://twitter.com/lloydtabb/status/1450538694130110464
- it seems to me it trying to solve the same problems as something like MDX, is this a fair statement ?
  - No, not MDX.  We're focused on the things you would do with a SQL. 
- this is the logical sequel to LookML. 
  - No, the focus is different :)  Malloy entirely language based and our goal is to use Malloy all the places you would write a SQL SELECT.

- I have some questions. 
  - Is intermediate data stored in memory?
  - Is it lazy eval like Spark?
  - Does it supports static typechecking?
- No intermediates, every Malloy query turns into a single SQL query.
- It leverages the database for evaluation, so yes, lazy eval.
- It is type checked.

- ## Seems like @ClickHouseDB adding Clickhouse local is a direct reaction to @duckdb. #data
- https://twitter.com/AstasiaMyers/status/1611432837202448384
  - Tech goes through waves of being server-oriented and client-oriented. Seems like we are moving into a phase when people are more interested in the #edge and client.
- clickhouse-local was available in 2016, DuckDB first preview release is in 2019. Strange causality.
  - MonetDBLite (by the same folks who built DuckDB!) was also from 2016.
- If so, I’d say their approach is interesting. They basically turned themselves into a clickhouse railway
  - https://railway.app/
  - clickhouse’s approach is not edge/client at all! 
  - They basically just opened up a request/response API to a server, where the heavy lifting is happening.

- ## [ClickBench: A benchmark for analytical databases (Snowflake, Druid, Redshift) | Hacker News_202207](https://news.ycombinator.com/item?id=32084571)
- As a database author myself (I work on Apache Druid) I have really mixed feelings about publishing benchmarks. 
  - They're fun, especially when you win. 
  - But I always want to caution people not to put too much stock in them. 
  - We published one a few months ago showing Druid being faster than Clickhouse on a different workload
  - [Druid Nails Cost Efficiency Challenge Against ClickHouse & Rockset - Imply](https://imply.io/blog/druid-nails-cost-efficiency-challenge-against-clickhouse-and-rockset/)
  - It just seems wrong to take them too seriously.

- There are several existing benchmarks that test query optimisers with a lot of joins. It does not show performance of query engine, but more likely how good is your optimiser was tailored for this queries.

- It's possible the Druid configuration is suboptimal in some way. 
  - It appears that the ClickHouse tests were done using a local table, which there isn't an equivalent of in Druid. 
  - Druid treats every table like what ClickHouse would call a "distributed" table. 

- ## Metrics and benchmarks matter.
- https://twitter.com/ting_sun_cn/status/1600104343818031104
  - 李飞飞搞个ImageNet，Emery Berger搞个csrankings，一下子就对整个领域有了举足轻重的力量
- 确实，你看 clickbench 才上线多久，大家都已经开始在上面搞事情了
- 但是很多人搞过benchmark，最终也是消失在茫茫文献里
  - 说明设计合理的benchmark并推广它并不容易，比如ImageNet就是这样，不冲突

- ## 非常好懂的一篇文章。作者发现在CloudNative的OLAP数据库中，实际上存在Push查询到存储（如S3）和Cache两种实现存储和计算分离的方法。
- https://twitter.com/ant_sz/status/1436346537718652935
  - 更进一步，Cache往往速度更快但是受限于计算节点的空间，Pushdown受到网络、存储格式、查询类型的影响性能表现会有差别。因此想要结合两种方法
  - 原理也很简单，就是将适合Pushdown的部分Pushdown，其他的部分Cache起来。FPDB总是Cache源表而不是中间结果，主要贡献在于发现并提出了这个优化的点以及决定是否Cache的启发式算法和Cache管理算法，实验表明提升还是很大的
