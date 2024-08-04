---
title: spec-format-csv
tags: [csv, format]
created: 2019-12-24T12:58:14.083Z
modified: 2020-12-08T13:52:12.853Z
---

# spec-format-csv

# guide

# spec

- 

# faq
- 如何解决在单元格位置的内容中也含有逗号的问题
# summary

- 

# dev

- 

# discuss
- ## 

- ## 

- ## 

- ## Reading large csv files in parallel chunks is tricky because you can’t be sure a line end isn’t in a quoted field. 
- https://x.com/fredine/status/1817261497200021846
  - But I found a paper showing how to make a good guess that works most of the time!
- Write a state machine and use overlapping windows. Not sure why this warrants a paper.

- 💡 Alternative approach is to make the serial record/quote finding really fast and parallelize the rest through a work queue. My last experiment did that at 8-16GB/s. With AVX-512 I'm sure that can be improved upon.
  - I think that’s the two pass approach described in the paper.
- Similar, but not same. I had master process read into a ringbuffer, identify record boundaries and stick them into work queue, workers grab records from the queue/ringbuffer and process. Ringbuffer access will likely be cache-to-cache. Synchronization is tricky though.

- @duckdb has it, and it’s really, really fast too.
- I think @holanda_pe has done something like this for DuckDB
  - Yes - I was poking around and noted that DuckDB and polars support parallel reading. But no general support in the Rust csv eco system, Rust arrow or data fusion… might decide to do something about that…
- Polars csv reader is available in Rust.
