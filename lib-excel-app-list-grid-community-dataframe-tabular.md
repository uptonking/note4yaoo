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
# discuss
- ## 

- ## 

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