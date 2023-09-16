---
title: lib-db-datalog-community
tags: [community, database, datalog]
created: 2023-09-16T17:27:24.479Z
modified: 2023-09-16T17:27:42.089Z
---

# lib-db-datalog-community

# guide

- communities
  - https://twitter.com/search?q=datomic%20datalog&f=live
# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## [Open source Datomic?](https://www.reddit.com/r/Clojure/comments/yj1oah/open_source_datomic/)
- XTDB is open source and does immutability but it has significant differences to datomic. 
  - XTDB is document oriented and has no built-in schema or constraint checking.

- 🤔 Do databases like Datomic perform better or are safer than SQL databases, like postgresql? What advantages do they have?
  - They are structured differently: EAV oriented, documents or graphs, rather than traditionally relational. 
  - Secondly they are all (with exceptions) temporal databases. 
  - Third they are directly embedded in Clojure both in terms of syntax and proximity: even though most have external storage backends, the indices are typically right there for you to interact with.
- The biggest advantage is typically temporal awareness built into the database, meaning data is not forgotten when updated, like in a SQL database, but rather the database remembers what the value used to be.
  - You can model it in SQL, but it's typically a real headache once it starts to grow.
  - If you want versioning on all your entities in SQL, each table definition must include time columns, and each transaction must know how to attach time data to the transacted data. The problem compounds if you want to know which of your entity's attributes changed when, or know which entities across different tables changed together.
  - Even if you manage to get version data attached to everything you want versioned, you also have the difficulty of building queries that are aware of that version information and can deliver point-in-time results.
  - Datomic has easy solutions built in for all these problems.
- If all you want a log, it's typically not so bad. Or just want to be able to take snapshots of single tables, and be able to go back.
  - Once you move beyond that, and start from a point in time for multiple tables and how they relate at that specific point in time, the queries tend to get very involved. Historic comparisons further complicates things when you now need to consider more than one point in time.
  - It's all doable, but the code/SQL queries will lend itself towards increased complexity, and once you hit a case (such as new business questions) where you need to rebuild the tower of complexity you built

- It depends on the query patterns. If you have simple queries, and row-like data then probably worse, very graph-like data and targeted queries (that the query planner can't compile away) then probably better.
  - But these dbs both have a different query paradigm and a different storage/indexing paradigm, and SQL dbs have many different storage/indexing paradigms, so it's hard to generalize.
  - The query language is basically just better in all ways, although SQL standardization has lead to a lot of great tooling you lose access to.
  - Plus there is, in most of the datomic variants, the time awareness/db-as-value part, which is a huge advantage.

- ## [The Essence of Datalog (2018) | Hacker News](https://news.ycombinator.com/item?id=19351385)

- ## Are you familiar with Datalog-style queries? 
- https://twitter.com/ccorcos/status/1534074897294495744
  - Seems pretty similar, except the edges are traversed recursively without having to define methods to traverse school edge. 
  - Just remember that Datomic also allows you to query into the past so that's why `tx` lands in their indexes.
- 
- 
- 

- ## What database has the best query language that’s not sql?
- https://twitter.com/gusbicalho/status/1607857080450404356
- #datomic's #datalog is very intuitive if all you need are inner joins, which is just unification of variables. 
  - The minute you need anything else, things get ugly. Uglier than SQL? Who knows, pick your poison.

- ## We also tried the datalog-centric thing (reflecting spreadsheet-like application UI from Datomic queries), we found it not powerful enough to express what Rails can express. 
- https://twitter.com/dustingetz/status/1662626589505355780
  - Something closer to Airtable but powered by Datomic could have worked for a team with fundraising skillz
- My new database is Datomic inspired, fireproof

- ## a thing i made in JS similar to datomic datalog, except JSON + symbol DSL for lvars, e.g. _.foo instead of ?foo
- https://twitter.com/alandipert/status/1398296493392424960
- Are you doing incremental/differential view maintenance, or just recomputing?
  - just recomputing, but if something end-to-end looks workable i hope to revisit that part and make incremental
- 👉🏻 Incremental datalog evaluation is not too hard to implement until you hit recursive rules. Then you need differential dataflow
- If you're just recomputing on diffs, I wonder if it wouldn't be easier to just use DataScript or Datahike (or even Posh), and wrap in a JS API if that's what you want. Then you're just responsible for translating your JSON queries to edn.
