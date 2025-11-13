---
title: lib-db-app-community-etl-dbt
tags: [community, dbt, etl]
created: 2023-05-11T07:31:54.848Z
modified: 2023-12-15T18:03:33.503Z
---

# lib-db-app-community-etl-dbt

# guide

# blogs-dbt
- [How dbt succeeds - by Benn Stancil - benn.substack](https://benn.substack.com/p/how-dbt-succeeds)
# discuss-stars
- ## 

- ## 💥 [Best way to read 100k rows from DB and write it to Excel/CSV file? : r/golang](https://www.reddit.com/r/golang/comments/1ovoj9l/best_way_to_read_100k_rows_from_db_and_write_it/)
- Fetch query results in batches (1k or more, needs benchmarks).
  - Write each batch to CSV (use streaming).
  - Don't forget to compress CSV file (compression streaming is also a good idea).
  - Compressed file may be uploaded into online storage part by part.

- Read a row from the db.
  - Write a row to the csv.
  - Make sure I/o operations are buffered.
  - Profit.

- This is a simple producer-consumer problem that concurrency will handle nicely in Go. You can just use one goroutine to essentially be a generator for reading the DB results, then another goroutine can read from the channel and do the writes. In that case, it wouldn't matter how many rows you had to read and write.
- There are huge benefits in multiple go routines because they are waiting for different things on the outside world eg DB access on one side and writing to a file on the other side. This is especially true if it's not a simple read /write but actually a read / process (eg formatting) / write. In those situations you may want multiple threads running. Does the CSV data have to be in a certain order if not then you can really increase throughput.

- Yes. Don’t read everything in the memory first, write into the file as you read from the db. This alone should be enough. You can even gzip it on the fly.

- ## Today dbt announced column level lineage... but it's not open source and only available for paying cloud users. _202402
- https://twitter.com/Captaintobs/status/1757601463852023876
  - dbt is using SQLGlot (an open source SQL framework that my company @TobikoData maintains)  to power this newly gated feature.
- But there's an open source alternative to dbt cloud... @SQLMesh , where column level lineage is free and open source for everyone to use.
  - SQLMesh is backwards compatible with existing dbt projects, so you can gain all of its benefits without rewriting your project.

# discuss
- ## 

- ## 

- ## At this point in time, I’d recommend sqlmesh over dbt and it’s not even close.
- https://twitter.com/neelesh_salian/status/1783585925093830733
- I think it's similar to Airflow vs. Dagster. One brings more to the table but not enough "yet" to warrant an expensive migration for most companies.
  - However one difference here is that dbt Labs practically gave up on the open-source project, unlike Astronomer + Airflow community.
- our dbt adapter is pretty good which means you can run your dbt project on sqlmesh without having to do an expensive migration. we’re always looking to improve it to reduce the friction.

- ## 最近在计划一个全新的 #OpenDAL 子项目：oay，OpenDAL Gateway，允许用户使用最熟悉的 API 来访问不同的存储后端。
- https://twitter.com/AFutureD/status/1648685933330599936
- 事实上就是有不少给etcd加zookeeper API，给rocksdb加redis API 之类的项目。我觉得场景不是为了完全获得另一个系统的能力，而是为了不改代码获得一些好处。比如给redis上OSS API可能单纯就是小文件加速，不会去用scan

- 项目自己的定位和用户对项目的使用之间可能还有出入，而且很难说怎么去对齐一下
  - 这就是要贴近用户去思考了，OpenDAL 也过类似的故事。过去 OpenDAL 提供了 Object 的抽象，预期的是用户会重用同一个 Object 去做操作，但是 review 所有用户的代码后发现没人是这样用的，大家每次都在创建新的 Object，于是我直接把这层抽象拆掉了

- ## [A sequel to SQL? An intro to Malloy | Hacker News](https://news.ycombinator.com/item?id=32738874)
- It is the first thing I try to teach CS graduates: DRY ( re-usability) is not applicable in the SQL world. Trying to re-use code, as proposed in Malloy generally results in poor performing queries. Malloy also seems needlessly complex compared to highly successful tools like DBT.
  - One other reason that DBT is successful is the low threshold to migrate your existing codebase.
- DBT shines, not because of the language/templating, but because it handles a lot of the scut work of building out a data warehouse. Write the select statements you want to populate the model, write tests to constrain the model, and build.
