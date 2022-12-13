---
title: lib-olap-duckdb-community
tags: [community, duckdb, olap]
created: 2022-12-05T16:01:07.929Z
modified: 2022-12-05T16:01:25.243Z
---

# lib-olap-duckdb-community

# guide

# discuss
- ## 

- ## 

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
- Sorry for this beginner question, is this only the case for DuckDB WASM, or DuckDB itself as well?I‘m just trying to explore possibilities for the fastest possible query results for users, I could also execute the queries in Lambda function instead.
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
