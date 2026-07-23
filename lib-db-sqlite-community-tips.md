---
title: lib-db-sqlite-community-tips
tags: [community, dev-xp, sqlite]
created: 2023-10-28T13:37:34.769Z
modified: 2023-10-28T13:38:46.522Z
---

# lib-db-sqlite-community-tips

# guide

# discuss-stars
- ## 

- ## SQLite supports databases up to 281 terabytes in size
- https://x.com/levelsio/status/2052459324308373505
  - SQLite is a highly optimized piece of software and can easily write 500, 000 rows per second with proper batching

- Yet single row is limited to 2GiB in size.
- 2, 000 columns.

- currently running my entire AGNT ecosystem on sqlite. its handling hundredsof gigs of my trace and generation data. i love sqlite

- Correct but it is tricky to scale if you have multiple VPS/containers (no matter their load). Afaik it can't work well over NFS or other network solutions. MySQL/PostgreSQL are better in that sense.

- ## Reminder: SQLite is 35% faster than the filesystem while also using 20% less disk space
- https://x.com/iavins/status/1850165947392254445
- SQLite could be default storage engine for an OS?
  - Great question! There have been attempts. Sharing some from my notes: sqlitefs, libsqlfs, wddfs

- Plain text is 35% slower than SQLite and takes up 20% more disk space but is more human readable. ScrollSets are the future

- What you're saying is not the same as what they are saying. If the thumbnails were in a sprite instead of individual files, that might be just as fast/faster than SQLite. Treating 1 single opened Sqlite DB to multiple unopened file descriptors isn't apples to apples comparison

- ## 看 SQLite 的介绍从数据库读小文件性能比从文件系统直接读要提升 35%，因为小文件读取大部分时间都消耗在了 open 和 close 的调用，而数据库只用一次 open 就够了
- https://x.com/liumengxinfly/status/1818514354196955539
- 大量小数据肯定要拼接然后自己维护 metadata 去索引的，前有 css sprites，后有 sstable
- 说起css sprites，自从前端模块化后这个就没再见到用了。
  - 说起css sprites，自从前端模块化后这个就没再见到用了。
- 类似 tcp 多路复用

# discuss-vendors-sqlite
- ## 

- ## 

- ## 

- ## 

- ## [D1 bill went from $0 to $1, 381 in 18 days. : r/CloudFlare _202607](https://www.reddit.com/r/CloudFlare/comments/1v3env9/d1_bill_went_from_0_to_1381_in_18_days/)
  - We run our global routing registry on D1 
  - We run sandboxes for agents and use D1 on every sandbox creation to decide which region the sandbox lands in.
  - Around Jun 28, our bill started climbing from $8/day, then $60, then $190/day by Jul 13.
  - There was no traffic spike, no errors, and latency was fine.
  - The cause: one frequent query running every 5 mins had no composite index covering its WHERE clause, so SQLite was scanning the entire table, multiple times per run.
  - Per million-row read pricing cooked us lmao.
  - Fix: one `CREATE INDEX` . Bill back to effectively zero.

- This is why I prefer to not use databases with row read billing. Worst case on a regular database your query performance starts degrading and you aren't billed an arm and a leg for badly optimized queries.
# discuss-license-sqlite
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Making a change to SQLite source code | Hacker News_202210](https://news.ycombinator.com/item?id=33339634)
- Not mentioned is that the full test sqlite test suite is proprietary and you need a super expensive sqlite foundation membership to get access to it. That means (unless you get that membership), your patched/forked version will be less extensively tested than the official version. So sqlite is in reality very difficult to fork. Sqlite is very solid, but bugs do sometimes show up in it despite all that testing, and more relevantly, some bugs in development are presumably caught by the testing, which outsiders don't have access to.

- ## [SQLite's proprietary test suite is its secret sauce that has kept it closed to contributions... | Hacker News](https://news.ycombinator.com/item?id=33083993)
- SQLite's proprietary test suite is its secret sauce that has kept it closed to contributions and kept forks from happening. It is the thing that made the SQLite Consortium a going business proposition. It is the thing that makes it possible to fund an open source infrastructure project with a small, cohesive team.
  - Any fork will instantly lose the benefits of that private test suite. This is what keeps the SQLite team able to reject external contributions, and what keeps forks from taking hold.
  - I believe a Rust re-write would have much less trouble w.r.t. the private test suite, owing to Rust's memory safety. But any fork that remains C-coded will have trouble getting public acceptance, and will have to have amazing features -or a new public test suite- to get acceptance.

- The private suite is about (among others) MCDC ie extremely stringent test coverage constraints at the binary level - what does this have to do with rust vs c?
# discuss-sqlite-server
- ## 

- ## [I'm all-in on server-side SQLite (2022) | Hacker News_202309](https://news.ycombinator.com/item?id=37613747)
- 
- 
- 

- ## [I'm all-in on server-side SQLite | Hacker News_202205](https://news.ycombinator.com/item?id=31318708)
- 🆚️ In which scenario would you use litestream vs rqlite?
- rqlite author here. The way I think about it is that both systems add reliability to SQLite, but in addition rqlite also offers high-availability.
  - Another important difference is that Litestream does not require you to change how your application interacts with the SQLite database, but rqlite does.
  - It's important to understand that rqlite's goal is not to replicate SQLite per-se. Its primary goal is to be the world's "easiest to operate, highly-available, distributed relational database". It's trivial to deploy, and very simple to run. As part of meeting that goal of simplicity it uses SQLite as its database engine.
- Litestream author here. I agree with Philip. Litestream relaxes some guarantees about durability and availability in order to make it simpler from an operational perspective. 
  - I would say the the two projects generally don't have overlap in the applications they would be used for. 
  - If your application is ok with the relaxed guarantees of Litestream, it's probably what you want. 
  - If you need stronger guarantees, then use rqlite.

# discuss-sqlite-rust
- ## 

- ## [SQLite with a Fine-Toothed Comb (2016) | Hacker News_201807](https://news.ycombinator.com/item?id=17506000)
- Richard Hipp (creator of SQLite) had this to say about Rust and SQLite in the comments:
  - > Rewriting SQLite in Rust, or some other trendy “safe” language, would not help. In fact it might hurt.
  - Prof. Regehr did not find problems with SQLite. He found constructs in the SQLite source code which under a strict reading of the C standards have “undefined behaviour”, which means that the compiler can generate whatever machine code it wants without it being called a compiler bug. That’s an important finding. But as it happens, no modern compilers that we know of actually interpret any of the SQLite source code in an unexpected or harmful way. We know this, because we have tested the SQLite machine code – every single instruction – using many different compilers, on many different CPU architectures and operating systems and with many different compile-time options. So there is nothing wrong with the sqlite3.so or sqlite3.dylib or winsqlite3.dll library that is happily running on your computer. Those files contain no source code, and hence no UB.

- ## 👉🏻 Nobody is feasibly going to rewrite Sqlite in Rust.
- https://news.ycombinator.com/item?id=25464846
  - Is making a file based database that hard, compared to creating new programming language for example ?

- If you gave me two year I'm not sure I could implement a filesystem API that correctly did something as simple as "atomically append to a file". See also Dan Luu's writing on the topic of filesystems

- The problem is to write a reliable file database. 
  - Firefox got a lot of bugs related to history file corruption until it was replaced with SQLite. 
  - The same story was with Subversion where they replaced Berkeley key DB due to reliability issues.
  - This reliability comes from a very deep knowledge of OS API and all their corner cases. 
  - Creating a programming language typically involves less corner cases and the bugs in the compiler/runtime are much simple to reproduce (again, typically).
# discuss-perf
- ## 

- ## 

- ## SQLite requires a different mindset for performance tuning than most dbs. 
- https://twitter.com/fractaledmind/status/1774121491778441680
  - For MySQL or PG the default advice is to prefer a smaller number of large queries, to minimize network latency. 
  - For SQLite, you should prefer a larger number of small queries.
- Writes block, so you want to avoid long running write queries. So if you want to avoid busy errors, you want to keep your writes small and quick. This allows SQLite to linearize them and keep any from overflowing the timeout.

# discuss-db-per-user
- ## 

- ## 

- ## 

- ## 

- ## I learned that Bue Sky uses one SQLite database per user, as God intended. Where can I read more about its high level architecture?
- https://x.com/iavins/status/1850036886938497410
- A step in the right direction. One SQLite per user = 1 file per user. It's only 1 step from there to ScrollSets (1 plain text file per user ).

- Dan did a great talk about the high level architecture. as for the tech each part uses, the PDSes are TypeScript+SQLite, the Relay is Go+Postgres, and the AppView is half Go+Scylla, half TypeScript

- https://x.com/iavins/status/1850201235347128640
  - They have a service called PDS (Personal Data Server) which contains all user data, where each user has their own SQLite db.
  - They push new changes from SQLite to Scylla. How are the changes from SQLite observed - through changesets or by monitoring WAL?
- the PDS exposes a websocket which sends changes. the appview consumes these events to construct its view of the network
  - as an optimisation, a service called a relay aggregates events from all the PDSes on the network into a single stream, called the firehose
# discuss-sqlite-testing
- ## 

- ## 

- ## 

- ## TIL that SQLite's test suite is proprietary and non-public.
- https://x.com/charliermarsh/status/1866575755783921810
- It’s the secret of their business model really. It’s a pretty fascinating approach and it worked for them for a long time. Not sure how much that works in the general sense. They also don’t take contributions.

- The test suite is how they make money. Only thing that they sell. It cost about $3, 000 decades back. Should be far higher now. Not published. Negotiated.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 看了 SQLite 论战，好有意思, 各种观点
- https://x.com/alswl/status/2072094812376097259
  1. 数据归属：结构化数据 vs Plain Text。
  2. 工程结构：RDBMS vs AOF。
  3. 实现选择：成熟外部工具引入 vs 自建协议库。
  4. 关注点：讨论工程 vs 信任权威
  - PS：我站 SQLite，考虑长期功能诉求和可维护性，总有需要引入一套复杂数据结构，不是自己写就是用别人的。

- 数据主权，用户有没有权利以开放格式访问自己的聊天数据？

- ## SQLite in the backend is a terrible choice!
- https://x.com/CFDevelop/status/1904623460447641786
  - It suffers from the same problem as document dbs. There are only a handful of data types so you can’t do powerful querying 
  - Use something like Postgres for an RDBMS on the backend

- ## Generated columns are calculated based on other columns in the same table. 
- https://twitter.com/ohmypy/status/1788193851099726311
  - For example, we can calculate the failure rate based on the number of queries
  - Another common use case is to extract a certain JSON path into a separate column and optionally index it (see the screenshot). This allows using SQLite as a document database
  - Generated columns can be computed on the fly or stored on disk. Stored are rarely used in practice.
  - Available since SQLite 3.31 (Jan 2020).

- ## Modern SQLite #1: STRICT Tables
- https://twitter.com/ohmypy/status/1786733812346450422
  - SQLite's type system is very flexible (some people even call SQLite the JavaScript of databases) — you can store any value in any column type (e.g. create an INTEGER column and store text values there, or a REAL with blob values).
  - at some point the SQLite authors introduced STRICT tables. They check types the same way other DBMS do
  - Even with strict tables, you can still explicitly declare a column as ANY — such columns can hold values of any type. So you can have the best of both worlds — strict type checking and type flexibility.
- I wasn't aware of this but always validated data before sending it to SQLite so that I wasn't abusing the DB type system. 

- ## 因为没有 network latency，SQLite 不需要优化 N+1 Query，但这玩意写入容易成为瓶颈...
- https://twitter.com/Hooopo/status/1774372573222236582
- 但凡 sql 场景，explain analyze 保命
- 还得看下硬件，如果使用 pcie 4.0 的企业级 ssd，4k 的 iops 写都可以到 200k 了，很多场景都够用了，如果使用傲腾的话单盘 iops 到 550k 也是很可观了

- ## how fast can you put a 10 million row, 11gb CSV into SQLite while handling NULL correctly? I’m at about a minute
- https://twitter.com/jitl/status/1768710776552853582

- ## The more I work with SQLite, the more I believe it's the perfect database for most indie products.
- https://twitter.com/ImSh4yy/status/1758577293763514822
- how do you get around the write limitations?
  - Spoiler alert: most never get there.

- @tursodatabase even makes multi-tenant stuff a breeze

- ## When should you pick SQLite as your production database?
- https://twitter.com/penberg/status/1748649917428453524
  - tl; dr, if you don't have high write throughput requirements or are already sharding your data, SQLite may be a good choice as a production database.
  - Right now, SQLite is finding its way to modern application stacks through things like Turso, LiteFS, and Cloudflare D1.
  - One of the apparent benefits of SQLite is that while it's lightweight, it's very fast. You can reasonably expect 100k queries per second (QPS) per database on a small machine, and SQLite scales to millions of QPS
  - 🐛 However, there is a gotcha: SQLite uses a single-writer model, limiting it to about 50k writes per second. 
  - Now, there are ongoing work from SQLite folks to address this with things like `BEGIN CONCURR ENT` and hctree, but in terms of write performance, the limit is there. 
  - Of course, many applications can work around this by sharding the data (e.g., with a database per tenant model), but it's not for all apps.

- ## 🤔 [Why you should probably be using SQLite | Hacker News_202310](https://news.ycombinator.com/item?id=38036921)
- 
- 
- 

- ## 🔥 [Why SQLite succeeded as a database (2016) | Hacker News_202301](https://news.ycombinator.com/item?id=34258858)
- 
- 
- 

- ## 🔥 [Why SQLite succeeded as a database (2016) | Hacker News_202002](https://news.ycombinator.com/item?id=22367104)
- 
- 
- 

- ## 🤔 [Why isn't SQLite more commonly used for save files or for other user-facing application file formats? : programming](https://www.reddit.com/r/programming/comments/h86v81/why_isnt_sqlite_more_commonly_used_for_save_files/)
- What did SQLite gave us? SQL.
  - XML schemas are gnarly, SQL schemas are easy.
  - Primary keys are great. Foreign keys are gorgeous.
  - Constraints on columns are handy.
  - :memory: is awesome for unit-tests.
- A lot of user applications store some or all their state in sqlite, firefox being a prominent example. That is what embeddable databases are designed for. It is not frequently used as an exchange format though, because it is no designed to be a good exchange format.
- Why is it not a good exchange format? Relational tables are an excellent exchange format, and SQLItes is specifically designed to be portable across time and architectures.
  - It's only unportable if you do something like use platform serialization to store your data structures in blobs. Don't do that, or serialize them to JSON/XML/etc before putting them in a blob.

- Also most data in iPhone apps is stored in sqlite files. Rip apart an iphone backup some time and peek at the contents.
