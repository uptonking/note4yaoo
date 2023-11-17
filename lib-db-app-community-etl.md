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

- ## 

- ## 

- ## 🆚️ How are you propagating changes from your operational database to your data warehouse / analytics system?
- https://twitter.com/gunnarmorling/status/1718681535803449394
  - batch vs streaming  =  0.52: 0.48  /145votes
- It is a tough question. A lot of factor should be considered. Such as how the change impacts reports, is there any realtime report got impacted … if all is “yes”, you will need realtime pipeline, else, batch processing is preferable.
- Streaming is much higher than expected and seen in the wild in this poll.  I suspect it’s influenced by your audience.
- Both!

# discuss
- ## 

- ## 

- ## 

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
