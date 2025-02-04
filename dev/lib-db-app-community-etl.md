---
title: lib-db-app-community-etl
tags: [community, database, etl]
created: 2023-09-17T18:10:19.845Z
modified: 2023-09-17T18:10:33.050Z
---

# lib-db-app-community-etl

> about data sources and integration

# guide

# discuss-stars
- ## 

- ## [有人解答下datax、talend、etlcloud各自的不同吗？ - 知乎](https://www.zhihu.com/question/603875795)
- datax是elt工具没有web界面，性能也一般
  - talend是商用etl工具也有社区版本是c/s结构的，国内用户群体比较少出了问题不知道找谁
  - etlcloud应该是国内最好的一款etl工具了，全web界面功能也很强大，还有cdc实时数据处理能力

- ## 🆚️ [Otter, Canal, DataX这几个开源的数据同步工具差别在哪? 究竟该用哪个? - 知乎](https://www.zhihu.com/question/392983860)
- cannal、otter都是阿里巴巴旗下开源的产品，其中canal是只有数据增量订阅的功能, 不能实现数据同步，otter是内嵌了canal的，利用其增量订阅，来进行源数据库和目标数据库的绑定，支持双向绑定和单向绑定，这两个该用哪个就看需求了，datax没用过不做评价

- Otter、Canal联合起来使用，用于两个mysql数据库的实时同步，简单通俗地说就是，源mysql一旦有变更动作（也就是操作日志），就传递给Canal，Canal再传递给Otter，Otter再在目标mysql里重做该动作，由于双方做了相同动作，双方就一致。这种传递-重做的过程一直在进行，双方就一直相同。
  - DataX则不同，它是直接读取源库的数据，并写入目标库，从而使双方一致。这种动作执行完成后，程序就退出了，如果以后需要再同步，需要再执行一次。

- ## 🆚️ How are you propagating changes from your operational database to your data warehouse / analytics system?
- https://twitter.com/gunnarmorling/status/1718681535803449394
  - batch vs streaming  =  0.52: 0.48  /145votes
- It is a tough question. A lot of factor should be considered. Such as how the change impacts reports, is there any realtime report got impacted … if all is “yes”, you will need realtime pipeline, else, batch processing is preferable.
- Streaming is much higher than expected and seen in the wild in this poll.  I suspect it’s influenced by your audience.
- Both!

# discuss
- ## 

- ## 

- ## Why is it that there's so little code reuse in the data transformation layer/ETL?
- https://x.com/mistercrunch/status/1841875802092405059
- I've been involved in several data interoperability standards committees over the years. In my experience (which is admittedly outdated) only power ($, legislation, etc..) drives adoption (e.g. medicare, walmart)

- ## 📥 Question for data people, how do you track files ingested, do you create a specific table or just a simple log like CSV etc ?
- https://twitter.com/mim_djo/status/1755004742005387534
- Snowflake automatically create a metadata table for that purpose—no need for any manual stuff. Back in the good old Hadoop days, we created a simple table with the date that has been ingested.
- but how do you make sure only 1 file is copied?
  - I think the uniqueness is the combination of filename, checksum and modified date

- In the @dagster , it is given out-of-box with the sensors whereby the run_key is unique and not run two times. You leverage metadata in the background
  -  we write the checkpoint next to the source folder in the same structure and write files that it was processed

- Normally, I have a table in the database where I log the pipeline ingestion and also track errors in the data processing that could be helpful for troubleshooting later

- We create a lineage table with a row per file or group of files, then this becomes a key on every row in every table within staging, any integration tables and final star schema. In Fabric we also stamp filename on table, if a single notebook loaded multiple files in one go.

- ## If you fix your Data, you have solved half of your problems. And using SQL Constraints is the perfect way to start.
- https://twitter.com/RaulJuncoV/status/1735285206179860639
  - PRIMARY Key Constraint
  - FOREIGN Key Constraint
  - UNIQUE Constraint
  - CHECK Constraint
  - NOT NULL Constraint
  - DEFAULT Constraint: useful when you want to provide a default value instead of leaving it NULL.

- ## DuckDB don't support RAM cache when querying Parquet files(to be fair none of the OSS engine support it), 
- https://twitter.com/mim_djo/status/1725848821681541295
  - current workaround is to load the whole tables into Memory, this is basically what #PowerBI did with import mode, at least before 2021
  - [Announcing on-demand loading capabilities for large models in Power BI_202112](https://powerbi.microsoft.com/en-us/blog/announcing-on-demand-loading-capabilities-for-large-models-in-power-bi/)
- so in a sense the biggest innovation of #Fabric direct lake is the capability to load and transcode from Parquet to the in-memory format that PowerBI understand, that's none trivial at all 

- ## Do you want a #database that can:
- https://twitter.com/OnlyXuanwo/status/1725494564755325036
  - SELECT * FROM 'gdrive://*.csv'
  - COPY FROM 'dropbox://*.xlsx' INTO table
- It seems that @duckdb supports both features. It may not support `gdrive://` or `dropbox://` scheme, but with the help of fuse i think it is possible to perform IO directly over these webdrivers
  - Yep, many databases support load data from services like s3. As known as data lake house 
- Taking a look at the popularity of projects like dsq, clickhouse-local, duckdb, sqlite-utils, datafusion-cli, etc.
- TiDB does support importing data from S3/GCS, but I agree GDrive/Dropbox sounds much cooler for personal usage. 

- ## 🔥 [Show HN: Stein – Use Google Sheets as a No-Setup Database | Hacker News_201907](https://news.ycombinator.com/item?id=20426682)
- 
- 
- 

- ## [SQL should be the default choice for data transformation logic | Hacker News_202301](https://news.ycombinator.com/item?id=34578324)

> 技术选型要根据使用场景，数据类操作和计算大多用python

- To me, data pipelines are about moving data from one place to another. and that's not really covered by the SQL spec. The article doesn't specify what constitutes a "data engineering pipeline", but for me there's three components to it:
  - orchestration, or what happens when
  - data manipulation, aka the T in ETL
  - data movement, getting data from A to B
- Orchestration? Please do not use dynamic SQL, you're digging a hole you'll never get out of. Moreover, SQL has zero support for time-based triggers so you'll need a secondary system anyway.
- Manipulating the data? Sure, use SQL, as long as you're operating on data from one database. Trying to collate(收集, 整理; 校对, 核对 ) data from multiple databases may have unpredictable performance issues even in the engines that support it.
- Moving data? There are much better options. And the same caveat as for orchestration applies here: every RDBMS vendor has its own idea of what external query's should look like (openrowset, external tables, linked servers) with their own performance considerations.
- Even on the manipulation side I tend to disfavor sql.
  - Even though it’s improved a lot the testing situation in sql is still not where a more traditional programming language is, modularity comes either in the form of ever nested cte, stored procs or dbt style templates. And **sql types are wholly dependent on the sql engine, which can lead to wacky transforms**.
  - Sql is great for adhoc analysis. If something isn’t adhoc, there is almost always a better tool.

- How do you test some SQL logic in isolation?
  - I do this using sql
  1. Extracting an 'ephemeral model' to different model file
  2. Mock out this model in upstream model in unit tests https://github.com/EqualExperts/dbt-unit-testing
  3. Write unit tests for this model.
  - This is not different than regular software development in a language like java.
  - I would argue its even better better because unit tests are always in tabular format and pretty easy to understand. Java unit tests on other hand are never read by devs in practice.

- As someone who works with 10s to 100s of TB of data from SQL and SQL-like DBs on a daily basis, writes lots of analytical code, I can say, emphatically, BS. Unless your analyses are trivial (column mean, max, etc.), chances are you need a real programming language behind you. 
  - And when you are working with dataframes that are 300+ million rows (glances over to his work machine, yup, that's a smaller analysis I need to run), you need a compiled and fast language for this, which can run in parallel on multiple threads and machines. 
  - You aren't using SQL for this. You aren't likely using pandas for this, or pyspark.

- I'm fine with this, but SQL has some lingering(继续存在的) shortcomings:
  - Inability to express recursive/nested datasets directly (tree-like).
  - General inability to express structural sharing and graphs directly.
  - Inability to express associative (map-like) relationships directly.
  - Some of these are solved in the SQL standard, but not universally adopted. Others are solved by particular databases, but also not universally adopted. For the rest, of course you can solve it if we add the condition "some assembly required" when you get the data.
  - But if you have to assemble and disassemble the data at every step, it stops being a viable pipeline choice. It's as good as serializing into CSV, JSON, or whatever. In fact, JSON at least can nest.

- I would strongly recommend reconsidering the suggestion that SQL serve as a data engineering pipeline default. We use SQL heavily at our organization, and use it for broad, significant ELT workloads. 
  - In essence, we use SQL, largely via DBT, where appropriate.
  - However, everywhere else, which comprises(包含；构成；组成) a significant collection of data pipeline services, uniform where possible but definitely heterogenous, we default to Clojure; we also utilize Python where more appropriate. Of these 3 languages **SQL clearly has the least generality, least testability, least API integration capability**, and definitely the most awkward data processing capability. I feel it is naive to suggest it could serve as a default language for data engineering pipelines, particularly given the need to interact with cloud services and third parties.

- I’ve found that sql pipelines end up depending heavily on a specific database (ssis packages for sqlserver) so really suck when you don’t want to use that database any more, or still need something to coordinate and run all the sql.

- Most SQL centric projects I've touched had a severe lack of automated tests.
  - Most projects I've touched had a severe lack of automated tests.

- SQL is fine. But as an engineer, I much prefer getting a notebook over a 1000-line plate of SQL spaghetti.

- I learnt this when I worked at www.carto.com. In Geo Analysis, you start with Raw data and then apply a series of transformations to it. The idea that all these transformations could be summarized in chain of SQL commands fascinated me.

- 
- 
- 

- ## dbt (data build tool) enables analytics engineers to transform data in their warehouses by simply writing select statements. 
  - dbt handles turning these select statements into tables and views.
  - dbt does the T in ELT (Extract, Load, Transform) processes – it doesn’t extract or load data
  - A dbt project is a directory of .sql and .yml files. 
