---
title: spec-format-parquet
tags: [columnar, format, parquet, spec]
created: 2023-01-13T14:52:09.370Z
modified: 2023-01-13T14:53:08.503Z
---

# spec-format-parquet

# guide

# dev

# discuss

- ## 

- ## 

- ## 

- ## 

- ## Bulk open data is best served as statically-hosted parquet files, with csv equivalents.
- https://twitter.com/RobinLinacre/status/1612414425948098560
  - It's faster, easier to use and cheaper to host than alternatives such as custom APIs.
  - [Why parquet files are my preferred API for bulk open data_201301](https://www.robinlinacre.com/parquet_api/)

- Completely agree - it's so frustrating having to learn some bespoke API to extract tiny amounts of data from a dataset.
  - Parquet files on an S3 or ADLS2 is far easier.
  - Delta format extends parquet to allow for ACID transactions and easier data management if data still changing.
- Exactly.  Or the other option which is just as bad:  having to navigate an often-horrible website to find a csv url (maybe hidden behind javascript) which lacks a naming convention (so you have to visit the website again for every update).

- This is what's needed to make this a total game changer:
  - [[C++] Implement HTTP and FTP file systems · apache/arrow](https://github.com/apache/arrow/issues/23849)

- Python, R, the CLI, DuckDB WASM, and maybe other clients should all be able to read and write files over the network, even to S3!

- Yes, but in that blog post I'm specifically talking about open data i.e. data that's supposed to be public access.   Nonetheless, if I was consuming private data, I'd still like it to be in parquet format!  I believe e.g. AWS S3 supports token based access

- Great post. I completely agree: APIs are the wrong tool for data analysis/bulk data transport. It was always confusing why data vendors would build them. I am a Snowflake fan precisely because their data-sharing/marketplace feature is similar but in the warehouse.

- I tend to find the biggest problems in open data are accessibility, data standards, metadata, and discoverability.
  - Parquet files may be neat but I don’t they particularly address any of these, and in terms of accessibility I think they add complexity (though agree with csv)

- I absolutely agree! However, I still believe that many non-technical data consumers still won’t have heard of Parquet files, and support for them in desktop software is almost non-existent. I still recommend also publishing in e.g. ODS to ensure non-technical accessibility.
