---
title: lib-olap-duckdb-community
tags: [community, duckdb, olap]
created: 2022-12-05T16:01:07.929Z
modified: 2022-12-05T16:01:25.243Z
---

# lib-olap-duckdb-community

# guide

- Icecap would be an alternative implementation of Iceberg tables using the native DuckDB file format and Redis.
  - https://github.com/sutoiku/puffin/blob/main/docs/Icecap.md

- [Epilogue: Our lessons learned building analytics startup Whywhywhy： use _202301](https://www.whywhywhy.com/what-we-learned/)
  - This is what we learned from building Whywhywhy over the past two years. 
  - We hope it will be useful to founders who are considering tackling problems in the analytics/BI space.
    - we built around two amazing core technologies: DuckDB (a very fast embedded analytics database) and Apache Arrow (a universal format for tabular data). 
    - The combination makes it easy to crunch millions of rows of data in memory at near instant speeds. 
    - WebAssembly has made the browser much more powerful.
    - document formats like Notion, Coda, and Google Workspace getting richer, we think analytics results will be consumed in context with narrative and visuals, rather than being trapped in BI siloes.
  - Whywhywhy let you quickly create interactive charts and share them with your team in communication tools like Slack, Notion, or Google Slides. 
  - Our vision was to enable anyone to answer questions using data.
  - Assumption 1: Target business users, not the data team
  - Assumption 2: Create an accessible data analysis and storytelling format
    - Dashboards work well for monitoring, but are bad for storytelling. 
    - Spreadsheets are great but don’t work well with big, live, data. 
    - The format that most inspired us was the computational notebook.
    - We got excited about taking the form of notebooks but making it accessible for people who don’t code.
    - Eventually, we moved focus from the no-code notebook to narrow sharing use cases for analysts, but still, it wasn’t sticking. What was the problem?
    - BI is a mature and broad category. It might feel like it should be ripe for unbundling given how many jobs that single piece of software does (and dbt has shown that it’s possible for the modeling part). But visualization and reporting is BI’s bread and butter and it’s not obvious to us how you wedge yourself in from that angle.
  - Assumption 3: Go to market through bottom-up adoption
# discuss
- ## 

- ## 

- ## 

- ## 

- ## Hot take: once @DuckDB 's native file format becomes stable, it will be on its path to becoming the new CSV.
- https://twitter.com/ghalimi/status/1620641265955270657
  - Why? Because DuckDB will be so ubiquitous that any data practitioner will have at least one DuckDB client at their disposal. Therefore, they'll be able to read and write DuckDB files as easily as CSV. But because these files will be 10 times smaller, they'll prefer them to CSV.
- Why DuckDB's file format over Parquet? Parquet already serves as the new CSV in a lot of places
- I think it might replace parquet but not csv. People store things in csv so it is human readable.
  - For small data, I agree with you. But data is getting bigger and bigger...
- Fwiw I suspect a lot of data vendors actually use CSV to pretend the data they are selling is "big". You might know the ones I'm talking about


- Wouldn't it be better if there was a format where row, vector, and human-readable were all interchangeable without loss of information?
  - I'm not sure that I understand what you mean. If you want human-readable, you can't compress. In that case, CSV is probably the way to go. But if you want compression, you really want a columnar format. Can you elaborate your thinking? I might be missing something here.
- Check out zed! [Zed Formats | Zed](https://zed.brimdata.io/docs/formats)
  - I did. It's interesting work, but with different objectives. We're very focused on high performance and do not want to create any new query language. Nothing beats SQL and the relational algebra. And there are plenty of languages like Malloy or @prql_lang that you can add on top
  - Also, the whole point of @PuffinDB 's Icecap is to take advantage of @DuckDB 's rapid adoption. 2M this past month. Before you know it, it will cross the 100M users mark (like GitHub just did). There are tectonic forces at play here...

- ## Seems like people use duckdb to manipulate pandas dataframes using SQL queries...? 
- https://twitter.com/__AlexMonahan__/status/1602449507870191616
  - I like SQL a lot but the biggest reason for me to switch to pandas/python is for stuff that's difficult in SQL!
- SQL on Pandas/Arrow are key use cases and DuckDB is much faster than Pandas (multicore+query optimizer). 
  - You can also read parquet files locally or over the internet from S3, and even in browser with WASM! It's also a good engine for SQL anywhere
- Plus, since it is in process, data transfer is super fast... You can read Pandas/Arrow usually without even copying it since you share the same memory space. 
  - The SQL dialect is also nice: the standard of Postgres syntax, but with more forgiveness and extra features too!
- You can also directly read SQLite or Postgres for super simple and open source HTAP! Another interesting use case is the Modern Data Stack in a Box... No cloud data warehouse needed, just 1 Docker image with @duckdb, @meltanodata, @getdbt, parquet, and @evidence_dev!

- ## [[Question] Wondering about serial HTTP range requests · duckdb/duckdb-wasm](https://github.com/duckdb/duckdb-wasm/issues/381)
- I wanted to play around a bit in the shell, and I uploaded a parquet file (a common one, a subset of the NYC taxi ride dataset, about 500MB in total) to a public S3 bucket and set the CORS so that it could be read by shell.duckdb.org. Then, I went to try out a few queries on the remote data file
  - First of all, I want to say again this is just amazing -- it pulled less then 30MB to answer an analytical query like this on a 500MB dataset, just blows my mind
- But secondly -- it's kinda slow! That query took over a minute to come back, most of it seeming to be network. To confirm, I opened up the devtools and checked the network, and saw a whole bunch of tiny sequential range requests that seemed to be making sure we couldn't get too much work done at once
  - I'm guessing they can't "just" be fully parallelized
- Yes, we're facing a couple of problems here.
  - The most important one is, that we're (not yet) fully async during I/O. This has a few far reaching requirements for the query execution model that haven't been been tackled yet.
  - Right now, we're always sitting in a C++ callstack when doing I/O which restricts us to single blocking http reads (via XHR).
  - Threads would offer an escape hatch here but they're immediately bringing up the problems with SharedArrayBuffers and cross-origin-isolation.
- I'd love to implement the web filesystem using multiple concurrent fetches but that's not quite possible today.
- So what we're doing right now is the following:
We're tracking 10 read heads per file and increase the read(ahead) size whenever we request sequential ranges.
  - But this leaves us with a few knobs that we have to tune ourselves, most importantly the readahead acceleration.
  - If you look at your screenshot, you can actually see that the requested byte ranges are growing roughly with a factor of 1.5.
  - We could totally increase that to 2 or more to reduce the number of roundtrips.
- Closing this for now with the readahead acceleration and the caching bug fix for Benjamin. We can track the user-configurable readahead acceleration in a dedicated issue.

- ## upon my current experiments with DuckDB WASM, it looks like querying partitioned Parquet files in S3 is done in sequential steps. Couldn't this be parallelized? 
- https://twitter.com/TobiM/status/1601981788758609920
- Here are some details about what is going on behind the scenes!
  - 👉🏻 Essentially we are in C++/WASM land and using synchronous IO. 
  - In the long run, DuckDB core plans to move to async IO, but that is not a small change!
- Sorry for this beginner question, is this only the case for DuckDB WASM, or DuckDB itself as well? I‘m just trying to explore possibilities for the fastest possible query results for users, I could also execute the queries in Lambda function instead.
  - DuckDB core is multi threaded (but synchronous per thread) I believe, so you should see parallelism in the other clients! (Node, Python, etc)

- ## DuckDB can query parquet data that's hosted on GitHub without needing to fully download the files! Presumably using HTTP range headers?
- https://twitter.com/simonw/status/1571140256052969482
- Indeed we use Range requests to surgically read Parquet metadata first, then only the row groups / columns relevant to the query
- Correct! And it works in DuckDB WASM as well - you can query anything on GitHub just by heading to the shell (on a non-mobile browser)! https://shell.duckdb.org/
- Oh! Is DuckDB WASM able to do glob expansion on remote http files?
  - Not yet I don't think!
  - Nice! In the Python world, it should be possible with the HTTP filesystem abstraction and Arrow.
- Any reason mobile browsers don't work with that? My iPhone runs WASM quite happily
- Bandwidth is magnitude cheaper than storage.
