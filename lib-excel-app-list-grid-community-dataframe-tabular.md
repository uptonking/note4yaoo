---
title: lib-excel-app-list-grid-community-dataframe-tabular
tags: [community, csv, dataframe, excel, tabular]
created: 2023-11-14T06:31:05.667Z
modified: 2023-11-14T06:31:35.103Z
---

# lib-excel-app-list-grid-community-dataframe-tabular

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## We present the first detailed, empirical evaluation of three popular and increasingly-adopted formats and evaluate their suitability to be used as a native format in a DBMS
- https://twitter.com/gunnarmorling/status/1731776497197756545
  - @ApacheArrow , @ApacheParquet , @apacheorc compared, by Chunwei Liu et al.

# discuss-toolchain
- ## 

- ## 

- ## 

- ## [Polars vs Pandas in 2025 — have you fully migrated yet? : r/Python _202601](https://www.reddit.com/r/Python/comments/1qbrioj/polars_vs_pandas_in_2025_have_you_fully_migrated/)
- ecosystem compatibility is still a pain point
  - Last time I tried (which means could be updated by now) some ML libraries only accepted and/or returned pandas dataframes, and was kinda annoying having to convert the data back and forth.

- Need geopolars to be fully fleshed out still.

- The only feature of Pandas for which I haven't found a Polars substitute is the pivot table, which is the only situation I've encountered where multiindexes make a problem simpler.
  - If I could, I would use only Polars in all situations, however I am also maintaining a Python data science package that needs to support both Pandas and Polars and so I need to deal with Pandas.

- Performance matters more if you are deploying pipelines. If you're doing EDA for example that latency doesn't matter so much. At that point the question is which is easier and I'm used to pandas.
  - Fair point. For EDA, the "I already know Pandas" factor is huge — context switching has a real cost.
  - Though I'd argue Polars' syntax is actually cleaner once you get past the initial hump. Method chaining without all the .copy() paranoia is nice.

- Anytime I am stepping into EDA, I write on pandas without a second thought (6 years of that workflow). However the past year saw me switch to utilizing polars for some larger scale data acquisition+ingestion processes. What would take ~8 minutes of processing with pandas takes maybe ~20 seconds.

- I have fully migrated a bit before polars 1.0. The speed improvement is not always noticeable especially for small data, but the API was the biggest reason for me. I am very experienced in pandas and have always hated its API. I picked up polars API fairly quickly and it's just natural now.
  - It's rare that I stumble into compatibility issues, but when I do, I just .to_pandas() or pl.from_pandas() it and move on.

- Fully migrated. Was attracted by the speed but stayed for the beautiful API. But it‘s natural that you have more tutorials for pandas since most tutorials are from a time where polars wasn‘t widely known yet.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## [Show HN: Turn your Pandas dataframe into a Tableau-style UI for visual analysis | Hacker News _202302](https://news.ycombinator.com/item?id=34869244)
- The Tableau algorithm is patented. In particular, the algorithm that chooses the type of the chart depending on the properties of the data. It was developed under the name Polaris at MIT (?).
  - This is based on graphic-walker which is based on vega as far as I see. It would be interesting to see if vega is different enough from Polaris/Tableau.

- Superset doesn't run in a Jupyter Notebook. So they are used differently. This seems very easily embeddable for instance. Or otherwise really practical.

- 
- 

- ## [Comparison of Data Lake Table Formats | Dremio Blog_202204](https://www.dremio.com/blog/comparison-of-data-lake-table-formats-apache-iceberg-apache-hudi-and-delta-lake/)

- ## @apachehudi brings the concept of 2 table types:
- https://twitter.com/Dipankartnt/status/1729304456439767105
  - ✅ Copy-on-Write (CoW)
  - ✅ Merge-on-Read (MoR)
  - Each of these table types has its trade-offs and allows users to deal between read and write latency. 
  - [Table & Query Types | Apache Hudi](https://hudi.apache.org/docs/table_types/)
- CoW:
  - data is stored exclusively using columnar file formats such as #parquet
  - every new update produces a new version of the base file by rewriting the file
  - handled on the write-side
  - higher write amplification (good for OLAP use cases)
- MoR:
  - data is stored using a combination of columnar (base) + row-based formats (log)
  - the base columnar file stores the main data & the row-based log file stores the updates
  - these updates are later compacted to produce new versions of columnar files (synchronous/async)

- ## [Why isn’t there a decent file format for tabular data? | Hacker News_202205](https://news.ycombinator.com/item?id=31220841)
- several high quality and well-developed formats
  - csv/tsv -- Simple for simple use cases, text-based, however many edge cases, feature lacking etc
  - xlsx -- Works in excel, ubiquitous format with a standard, however complicated and missing scientific features
  - sqlite -- Designed for relational data, somewhat ubiquitous, types defined but not enforced
  - parquet / hdf5 / apache feather / etc -- Designed for scientific use cases, robust, efficient, less ubiquitous
  - capn proto, prototype buffers, avro, thrift -- Has specific features for data communication between systems
  - xml -- Useful if you are programming in early 2000s
  - GDBM, Kyoto Cabinet, etc -- Useful if you are programming in late 1990s

- The latest version of SQLite has a STRICT command to enforce the data types. 
  - This option is set per table, but **even in a STRICT table you can specify the type of some columns as ANY** if you want to allow any type of data in that column (this is not the same meaning of ANY in non-strict tables).

- One major limitation with quoted values that can this contain record delimiters (as opposed to escaping the delimiters) is that it stops systems from being able to load records in parallel.
  - Some systems ban embedded record delimiters, for this reason.

- Parquet is a wonderful file format and is a dream to work with compared to CSV. 
  - Parquet embeds the schema in the footer metadata, so the query engines don't need to guess what the column names / data types are.
- Parquet is still relatively poorly supported in the JVM world 
- The other problem with Parquet is that it's overly flexible/supports application-specific metadata. 
  - It's all fine when you use a single tool/library for reading and writing files but cross-platform is problematic. 
  - Saving a Pandas dataframe to parquet, for example, will include a bunch of Pandas-specific metadata which is ignored or skipped by other libraries.
- I've been pretty impressed with parquet lately. One thing I've missed is a way to group tables. Is there a standard for that? While parquet is generally column oriented it has support for metadata about tables of multiple columns. However, I'm not aware of any format that groups the tables, short of just zipping a bunch of files.

- It's it possible to diff a parquet file?
  - Its possible but you can't just diff the file bytes. Because you will get spurious differences due to metadata, etc.

- There is a decent file format for tabular data, and the author dismisses it: parquet.
