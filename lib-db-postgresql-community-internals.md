---
title: lib-db-postgresql-community-internals
tags: [codebase, community, database, internals, postgresql]
created: 2023-10-28T13:45:28.278Z
modified: 2023-10-28T13:46:14.957Z
---

# lib-db-postgresql-community-internals

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## Postgres is an amazing database. It’s only significant weakness now is in Materialized views, with their lack of incremental refresh._202207
- https://news.ycombinator.com/item?id=32097663
  - Was disappointing to see there was no progress towards this in v15.
- That work towards incrementally updated views is happening and progressing. 
  - For now, it's a separate extension, though: https://github.com/sraoss/pg_ivm
- I wanted incremental refresh in Postgres as well and found that you can manage your own table to get something close.
  - Basically you create a regular table in place of a materialised one, only aggregate data newer than what's currently in the table then store the new aggregates in table. Repeat this an interval.
- Interestingly, DBT does not support creating materialized views.

# discuss-concurrency
- ## 

- ## 

- ## [PostgreSQL reconsiders its process-based model | Hacker News_202306](https://news.ycombinator.com/item?id=36393030)

- Sorry if I offend anybody, but this sounds like such a bad idea.
  - I have been running various versions of postgres in production for 15 years with thousands of processes on super beefy(粗壮的, 结实的) machines
  - Postgres has 99% of the time proven to be resilient. The idea that a bad client can bring the whole cluster down because it hit a bug sounds scary.
  - crashes are part of that workflow, and changing this from process to threading would mean all the other clients also crashing and cutting connections. 
  - This as a potential problem because I want to avoid context switching overhead or cache misses, no thanks.

- 👉🏻 Oracle has similar problems. On UNIX systems, Oracle uses a multi-process model
  - Windows forks processes about 100x slower than Linux, so Oracle runs threaded on that platform in one great big PID.
  - Sybase was the first major database that fully adopted threads from an architectural perspective, and Microsoft SQL Server has certainly retained and improved on that model.
- If you run postgres under WSLv1 (now available on Server Edition as well), the WSL subsystem handles processes and virtual memory in a way that has been specifically designed to optimize process initialization as compared to the traditional Win32 approach.
- Yeah multiprocess isn't Microsoft's style given how expensive creating processes is on Windows.
- Didn't Oracle switch to threaded model in 12c
  - It's optional, and the default is still a process model on Linux.

- Reminds me of PHP 6... For those who don't follow PHP closely - that version was an attempted refactor of the string implementation which essentially shut down nearly all work on PHP for a decade, stagnating the language until it became pretty terrible compared to other options. 
  - They finally gave up and started work on PHP 7 which uses the (perfectly good) PHP 5 strings. 
  - Ten years of wasted time by the best internal PHP developers crippled(使伤残; 严重损坏) the project - I'm amazed it survived at all.

- I've seen (and reported) bugs that caused panics/segfaults in specific psql processes. Not just connections, also processes related to wal writing or replication. The way it's built right now, a child process can be just forced to quit and it does not affect other processes. Hopefully switching into thread won't force whole PostgreSQL to panic and shut down.
  - Because of shared memory most panics and seg faults in a worker process take down the entire server already (this wasn’t always the case, but not doing so was a bug).

- The thing is... multi-process with a bespoke shared memory system isn't better than multithreading; it's much worse.

- 
- 
- 

# discuss
- ## 

- ## 

- ## 

- ## [Unexpected downsides of UUID keys in PostgreSQL | Hacker News_202306](https://news.ycombinator.com/item?id=36429986)
- CouchDB uses sequential UUID by default
  - the choice of UUID has a significant impact on the layout of the B-tree, prior to compaction.

- 
- 
- 

- ## 🔥 [Get PostgreSQL Database Structure as a Detailed JavaScript Object | Hacker News_201912](https://news.ycombinator.com/item?id=21714500)
- 
- 
- 
