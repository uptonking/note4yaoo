---
title: lib-db-sqlite-blog-stars
tags: [blog, sqlite]
created: 2023-10-26T17:32:53.997Z
modified: 2023-10-26T17:33:04.929Z
---

# lib-db-sqlite-blog-stars

# guide

# blog-stars

## [SQLite isn't it](https://github.com/vlcn-io/docs/blob/main/pages/blog/sqlite-isnt-it.mdx)

- I've been building with nothing but SQLite for 2 solid years. I've also bet most of my work on the future of SQLite when it comes to [vlcn.io]
  - SQLite is still the best we have in terms of embedded relational DBs but, all that said, it's a square peg(钉，栓) trying to fit a round hole.
- 🐛 SQLite is a bad fit for client side applications. 
  - It is designed for 1990's- early 2000's era request-response style and it completely misses the mark when it comes to addressing the needs of today's client side applications.
- Let's take a step back. How do today's client side applications make use of client side data stores?

### Observation 1: Static Queries, Dynamic Data

- > Most databases were built when data was static and queries were dynamic. For applications, most queries are static and the data is dynamic
  - Applications, other than BI and analytics apps, have relatively static queries but dynamic data.
  - Take Messenger as an example. The query that shows the user their list of threads is a static one. It is the same query every time. The threads that that query is surfacing, however, are changing all the time. 
  - Same with a Google doc. The queries to show its content, comments, edits, viewers, etc. are all static. Each of those datasets, however, changes all the time.
- The model of static queries and dynamic data requires a subscription model
  - but SQLite only provides a request-response model for queries.
- Since SQLite only support request-response, using it to implement a view that updates whenever the underlying data changes requires one or more of:
  1. Polling SQLite
  2. Relying on the shaky [data change notification callbacks] provided by SQLite
  3. Creating a separate data model (e.g., a View Model or a Domain Model) on top of SQLite that handles reactivity 

#### Polling

- Polling isn't ideal since:
1. It introduces latency into the system. Responding to a write is only as quick as the polling interval.
2. Wastes resources. The data may not have changed between polls.
3. Wastes resources. Re-runs a full query rather than only computing a difference.

#### Data Change Notifications

- SQLite does provide [data change notification callbacks](https://www.sqlite.org/c3ref/update_hook.html) but they're severely limited.
  1. They do not work on `without rowid` tables
  2. They do not provide notifications if other connections make a write
  3. They do not provide notifications if other processes make a write
  4. They only tell you the `rowid`,       `table`,       `db`, and `operation` of the change. It is your job to figure out what queries that would impact.
  5. They don't contain the data that changed meaning you need to re-query to get the new values

- The data change notification callbacks are what Vulcan-web currently use to provide reactivity (as well as other projects like [GRDB](https://github.com/groue/GRDB.swift)). 
  - These projects show that these limitations can be worked around if you're clever (by combining sqlite's byte code extension, pre_update hook, commit_hook, authorizer callbacks and more) but you run into another wall.

- The solutions:
  1. Are not incremental. They require re-running the entire query if the data it used changed.
  2. Over-invalidate. Other than point queries (`SELECT FROM foo WHERE id = ?`), you'll need to invalidate and re-run all queries that used any table that was written.

#### Separate Data Model

- A final option is building out a separate data model on top of the database. 
  - Something where you read and write to objects that exist in-memory and later persist them to the database. 
  - This is today's status quo(现状). Think things like CoreData, MobX + Persistence, Room Persistence Library.

- Benefits:
  1. Read are as fast as working with memory (after initial hydration)
  2. Writes are as fast as working with memory (when persistence is done lazily)
  3. The libraries include fine grained subscriptions to objects, object properties and collections of objects.

- These benefits come with huge downsides as in-memory model is effectively building a database outside of the database.

- 🐛 Downsides:
1. Increased complexity. Must deal with the DB idiosynchracies as well as the ORM / in-memory model's. The in-memory model adds a whole new layer that requires mapping results to/from.
2. Transactions I. Many of these solutions do not provide an ability to update the in-memory model transactionally, leading to observation of stale state.
3. Transactions II. If many writes are made to the in-memory model then the lazy persist fails, what can be done? Can the in-memory model be rolled back?
4. Invariants. The DB will have foreign key constraints, check constraints, and unique indices. For the in-memory model to always succeed in persisting to the DB, these constraints must be replicated and checked there too.
5. 🔀Concurrency. the database will have a defined concurrent model to deal with concurrent updates. Now that needs to be replicated in the in-memory model or concurrency must be forbidden.
6. Other processes. The in-model can not observe writes made by other processes and coordinating processes must be eliminated else risk model & db divergence.
7. Writes may no longer go directly to the DB. Allowing someone to bypass the in-memory model to issue a write will cause the DB and in-memory model to fall out of sync. Trying to subscribe the in-memory model to the DB to fix this lands us back to square 1.
8. Limited subscription primitives. The in-memory model can only be subscribed to on a collection of key-value basis. No subscribing to other styles of queries.

- It is a shock that the status quo has been to use this fraught approach for so long.

- Rather than creating a db outside the db, applications should be able to code directly against the database and let the database manage everything it is good at:
  - atomicity
  - consistency
  - isolation & concurrency
  - durability
  - indexing
  - querying

### Observation 2: UIs Present De-normalized Data

- Data should always be stored in a normalized form. It ensures there is only ever one copy of a thing and that inconsistent states do not occur. 
  - The relational model also ensures that the applications built on top can always access the data in a way that makes sense to them. 
  - Contrast with the network or graph models which require knowing specific paths to objects in order to load them and create a tight coupling between how data is laid out and how it is accessed.

- Once the data starts to be used, however, it is almost always used in a de-normalized way.

- Given:
1. Apps have many static queries
2. These queries fetch de-normalized data
- An embedded DB for client side applications should have first class support for incrementally maintained views. 
  - There should be no need to re-run the set of joins required to produce a view every time the view is requested.
- Taking this a step further -- an embedded DB could even preclude the developer from having to define indices. 
  - If the views and queries are known ahead of time (which they are), a build process can create the correct indices to serve the needs of the application.

- 🐛 SQLite, unfortunately, has no support for incrementally maintained views just as it has limited support for subscriptions. 
  - One could maintain sets of triggers to manually maintain incremental views but this isn't ideal.
- The counter-argument is that: SQLite, being embedded, [makes many small queries efficient](https://www.sqlite.org/np1queryprob.html) which obviates(排除，消除) the need for joins. 
  - While this is true, it doesn't completely remove the need for them. 
  - In addition, the cost of traversing `WASM<->JS` boundaries in the web platform, makes many small queries much less attractive. 
  - Finally, being able to see the full data needs of a UI tree as a single query opens up many new avenues in terms of data syncing and collaboration.

### Observation 3: Write Priorities

- Not all writes are created equal. 
  - Some writes, like those initiated by a user event, need to be responded to immediately. 
  - Other writes, such as a background import of some data, can be given a lower priority.
- Along the same lines as write priorities, not all writes need to be immediately durable. 
  - To give the user a faster experience, it may be preferable to non-durably write their update in order to reflect back changes more quickly.
- The inability to selectively relax durability is a performance bottleneck when it comes to responding to writes as we're limited [by the transaction throughput of writing to disk](https://www.sqlite.org/faq.html#q19). 
  - SQLite is designed to handle bulk updates well by amortizing the cost of writing to disk over all the statements in a transaction. 
  - It is not designed to handle the many small updates you'd get in most applications. E.g., typing characters into a doc, dragging shapes in figma, scrubbing the playback state over a video or song.

### Observation 4: Collaboration

- The world of client side applications is not what it was two decades ago when SQLite was created. 
  - In the 90's and early 2000's a client side application only had to concern itself with the computer it was running on. 
  - Fastforward a bit, everyone has many devices and expects their data to be available on all of those devices.

### Problem: Language Barrier

- Application developers would rather query their data in a language that more closely integrates and embeds into their host language. 
  - SQL is also an opaque barrier that hides many useful features of the DB. E.g., the query planner or direct index access.

### Problem: The Browser Platform

- Maybe I can re-work SQLite enough to shore up these problems in a fork. Maybe it requires something new.
  - This means that to support the use case of dynamic data you need to implement some sort of polling or manually invalidate and re-run entire queries.
- What you need to support this is queries to which you can subscribe. The model of SQLite has minimal support for this setup.

- Normalized
- To de-Normalized
- Index selection and creation
- Query layer / lack of SDK
- Collaboration
- Write prioriteis

- What are all of the knock on effects of this?
  - Reactivity
  - Intent -> SQL -> Parse -> Plan -> Execute -> Finally deliver
  - Write priorities. Single writer.
  - Incremental View Maintenance
  - Collaboration

- Re-running queries is especially problematic on the web platform.
- It's design follows too much in the footsteps of client-server DBs and it doesn't leverage its unique position as an embedded database as well as it could.
  - You can get very clever and work around all of these limitations. E.g., by watching the DB files (WAL, Journal, SHMem, main DB file) to understand when other processes write, by using a single write connection or coordinating write connections, by inspecting the byte code of read queries to understand all the tables they use, by hacking together `authorizer` and `pre_update` hooks to understand columns used and written. 
  - But at the end of the day, it is still a far cry from incremental subscriptions.

### Lessons Learned

- Riffle: https://riffle.systems/
- Or, a tldr from [against-sql](https://www.scattered-thoughts.net/writing/against-sql/):

- > But in the database world there is a missing step between demos on toy relational algebras and handling the enormity of SQL, down which most compelling research quietly plummets. Bringing anything novel to a usable level requires a substantial investment of time and money that most researchers simply don't have.

## ⚡️💾 [In-Memory SQLite Perf / Matt | Observable_202401](https://observablehq.com/@tantaman/in-memory-sqlite-perf)

- SQLite is unfortunately too slow in the browser to be used as a reactive database.
- If we use SQLite as our program memory (storing all app state and data), how does it perform when benchmarked against manipulating vanilla JS variables, objects, and data structures?
- Conclusion:
  - An in-memory SQLite can be, at worst, 1, 000x slower than direct manipulation of a variable.
  - This is vastly worse once persistence comes in as SQLite requires all transactions to be durably committed before returning and apps are generally doing many small transactions of a few updates. E.g., cursor moves, drags, rotates, scrolls.

- [SQLite FAQ - INSERT is really slow - I can only do few dozen INSERTs per second](https://www.sqlite.org/faq.html#q19)
  - SQLite will easily do 50, 000 or more `INSERT` statements per second on an average desktop computer. 
  - But it will only do a few dozen transactions per second. Transaction speed is limited by the rotational(轮流, 轮换) speed of your disk drive. 
  - A transaction normally requires two complete rotations of the disk platter(盘，碟), which on a 7200RPM disk drive limits you to about 60 transactions per second.
  - Transaction speed is limited by disk drive speed because (by default) SQLite actually waits until the data really is safely stored on the disk surface before the transaction is complete. That way, if you suddenly lose power or if your OS crashes, your data is still safe. 
  - By default, each `INSERT` statement is its own transaction. But if you surround multiple `INSERT` statements with `BEGIN...COMMIT` then all the inserts are grouped into a single transaction. The time needed to commit the transaction is amortized(摊销, 摊还) over all the enclosed insert statements and so the time per insert statement is greatly reduced.
  - Another option is to run `PRAGMA synchronous=OFF`. This command will cause SQLite to not wait on data to reach the disk surface, which will make write operations appear to be much faster. But if you lose power in the middle of a transaction, your database file might go corrupt.

## 🌵 [Tracking SQLite Database Changes in Git_202311](https://garrit.xyz/posts/2023-11-01-tracking-sqlite-database-changes-in-git)

- SQLite stores data in binary. If you want to track changes and updates to a database using Git, you won't be able to see full diffs by default. 
- Here's a diff between two states of the SQLite database of GnuCash
- 
- 

## 📝 [Hosting SQLite databases on Github Pages_202104](https://phiresky.github.io/blog/2021/hosting-sqlite-databases-on-github-pages/)

## 👥🔥 [Hosting SQLite databases on any static file hoster (2021) | Hacker News_202210](https://news.ycombinator.com/item?id=33182417)

- 
- 
- 

## 👥🔥🔥 [Hosting SQLite databases on GitHub Pages or any static file hoster_202105](https://news.ycombinator.com/item?id=27016630)

- how is this possible???
  - Use Http Range (normally used for pausing and continuing large file downloads) to request specific byte ranges from the file. 
  - From there you can pull only what you need. 
  - With sql indexes it'll be very tiny since the lookup is optimized. 
  - Of course if you `select *`, you're still going to pull the entire database locally.
- TL; DR http, properly implemented, supports a ton more stuff than even many “web developers” are aware of, like… range requests, which are exactly what you’d think they’d be.
  - Also SQLite store data in pages and the page size can be tweaked. Combined with range requests any part of the database can be requested.
- Have you actually read the article? SQLite is unmodified, and thinks it runs on a virtual file system, which fetches file chunks via HTTP range headers. It's REALLY impressive that you only need to read 54 KB out of 700 MB, to fetch the records.
  - the harsh reality is that doing sensible queries that only reference and return the data actually needed always makes things faster. Even with server DBMS. Oh, how many times have I lamented the naive "select *" for forcing all the row contents even when there was index coverage for the actually needed data.
- Do most static site hosters support range requests?
  - Most web servers do out of the box, so I would assume most do. Basically all unless they have some reason to turn range processing off or are running a custom/experimental/both server that have implemented the feature (yet).
  - Not supporting range requests would be a disadvantage for any service hosting large files. 
  - Resuming failed long downloads wouldn't work so users might not be happy and there would be more load on your bandwidth and other resources as the AU falls back to performing a full download.
- More interestingly, do reverse-proxies like Varnish/CDNs like Cloudflare support range requests? If so, do they fetch the whole content on the back, and then allow arbitrary range requests within the cached content on the front?
  - Yes, Cloudflare behaves as you describe.

- One of the heaviest users of range requests is (or was) the Adobe Acrobat PDF plugin.
  - Also .mp4 files. The format is designed for seekability, and browsers take advantage of this.
  - You can even point VLC at a .iso file on a web server, and seek around in it.
  - Progressive JPEGs work well for this too, so you could have the same file used for a tiny thumbnail and large preview and full sized photo by sending different range requests. However you need to know how many bytes to request.
- I'm surprised this isn't used on mobile browsers to lower data usage. I'm sure with a little research you could figure out what a good mapping from pixel size to byte size should be to give good enough results.
  - A browser doesn't have enough information to use this optimization. 

- This is easily the most clever web programming hack I’ve seen this year. Bravo. I had seen this used for video or audio of course but it never occurred to me you could use it for databases. There are probably a ton of other formats this is good for too.
  - This is pretty much exactly what we do to serve aerial/satellite imagery maps. We convert the imagery into Cloud optimised geo tiffs and store them in S3 https://www.cogeo.org/ then the browser can request the tiles directly from S3. Even the big imagery providers are now storing their imagery as COGs

- I believe this is protomaps approach: re-encode the mbtiles (sqlite-based ) format in to something that can be requested with a http range request and thus served from a single dumb webserver that doesn't need to understand sqlite or mbtiles parsing
  - This is the approach I took with protomaps/pmtiles , though it's optimized for the very specific use case of going from Z/X/Y integer coordinates to binary blobs, and takes shortcuts to accomplish that (fixed-width keys and root index page)

- The innovation here is getting sql.js to use http and range requests for file access rather than all being in memory.

- There are a bunch of *-to-sqlite utilities in corresponding dogsheep project.
  - Datasette is one application for views of read-only SQLite dbs with out-of-band replication.
  - Arrow JS for 'paged' browser client access to DuckDB might be possible and faster but without full SQLite SQL compatibility and the SQLite test suite
  - DuckDB can directly & selectively query Parquet files over HTTP/S3 as well.
  - In-browser notebooks like Pyodide and Jyve have local filesystem access with the new "Filesystem Access API", but downloading/copying all data to the browser for every run of a browser-hosted notebook may not be necessary.

- Microsoft Access Cloud Edition, basically?
  - Sort of. Access had a "Forms" feature that let you create basic GUIs on top of your database.

## 👥 [Hosting SQLite Databases on GitHub Pages | Hacker News_202107](https://news.ycombinator.com/item?id=28015980)

- 
- 
- 

## 👥 ["Hosting SQLite databases on Github Pages" is absolutely brilliant: it adds a virtual filesystem to SQLite-compiled-to-WebAssembly in order to fetch pages from the database using HTTP range requests ](https://twitter.com/simonw/status/1388933092216164352)

- Check out this demo: I run the SQL query `select country_code, long_name from wdi_country order by rowid desc limit 100` and it fetches just 54.2KB of new data (across 49 small HTTP requests) to return 100 results - from a statically hosted database file that's 668.8MB!
  - Looks like the core magic here is only around 300 lines of (devastatingly clever) code
  - https://github.com/phiresky/sql.js-httpvfs
- But it does not support updates, right?
  - Of course it can’t write to this file, but a read-only database is still very useful
- I love SQLite but it has it's limitations and if handled improperly it can be a nightmare and even degrade performance & security issues.
  - e.g. not using block SQL transactions will quickly result in read-writes that take millennial(一千年的).
- It used to take me 15 hrs plus to write 10, 000 records to a sqlite file and block commits using transactions reduced that to a few minutes.
  - I used to do a big transaction in sqlite for this, copy the DB file, # pragma synchronized off, write everything, done.
- Are service workers good enough that we can write full stack apps (possibly with @vercel 's NextJs) with SQL + RestAPI + SPA and deploy the whole thing to a CDN?
- We have some fun experiments going with this and actions
  - the hard part is dealing with concurrent actions (and teaching git to diff/merge sqlite) 
  - but the kludgy(不成熟的，蹩脚的) solution of "if push rejected, reset pull and retry" is surprisingly effective
  - Have you got a prototype of git diffing SQLite? That could be fantastic for a whole bunch of my projects. I have a sqlite-diffable thing I've been playing with
  - https://github.com/simonw/sqlite-diffable
  - it works by dumping the DB to plain text (ndjson)
  - ultimately my use-case was append-only, so I went with the retry-upon-failure strategy (which only really matters in case of concurrent action execution). Not elegant but did the trick!

## 🛢️ [SQLite as a document database_202006](https://dgl.cx/2020/06/sqlite-json-support)

- SQLite has had JSON support for a while.
- However recently it added a killer feature: **generated columns**. (This was added in 3.31.0, released 2020-01-22.)
  - This makes it possible to insert JSON straight into SQLite and then have it extract data and index them, i.e. you can treat SQLite as a document database.

- https://github.com/dpapathanasiou/simple-graph /sql
  - This is a simple graph database in SQLite, inspired by "SQLite as a document database"
  - The schema consists of just two structures: Nodes(json) and Edges({id:json})
  - There are also traversal function templates as native SQLite Common Table Expressions which produce lists of identifiers or return all objects along the path.
  - [SQLite as a document database_202006](https://dgl.cx/2020/06/sqlite-json-support)
# blogs

# blogs-internals

## 📝 [SQLite Internals: How The World's Most Used Database Works](https://www.compileralchemy.com/books/sqlite-internals/)

- To all SQLite lovers. This book discusses SQLite internals in depth.
  - Particular thanks to the LibSQL maintainers. Started this book as a series of presentations to DevFest and the LibSQL community. 
- 
- 

## 👥🔥 [SQLite internals: How the most-used database works | Hacker News_202212](https://news.ycombinator.com/item?id=34032990)

- 
- 

## 📝 [SQLite Internals: Pages & B-trees · Fly.io](https://fly.io/blog/sqlite-internals-btree/)

- I love SQLite’s 130KLOC core code base
  - This constrained size means that SQLite doesn’t include every bell and whistle. 
  - It’s careful to include the 95% of what you need in a database—strong SQL support, transactions, windowing functions, CTEs, etc—without cluttering the source with more esoteric features. This limited feature set also means the structure of the database can stay simple and makes it easy for anyone to understand

## 👥 [SQLite Internals: Pages and B-trees | Hacker News_202207](https://news.ycombinator.com/item?id=32250426)

- 
- 
- 

- I dream of a SQLite-like embeddable database engine based on Datomic’s data model and queryable with Datalog. Written in something like C, Rust, or Zig. 

- I wonder if it’s possible to build it on top of SQLite somehow?
  - I tried. It's not easy because of how limiting SQLites indexes are. You have to build your own indexes using TRIGGERs or in a software wrapper and tables.
  - You can see me prototype here: https://git.sr.ht/~chiefnoah/quark
- Commendable attempt! I've considered writing a datalog storage backend on sqlite just like your prototype. Thank you for sharing, now I can lazily study your prototype instead of doing the hard work myself. I'm curious, what kinds of limitations of SQLite indexes are you referring to?
  - 👉🏻 Sparse indexes are pretty limited and it only supports B-tree, which make implementing AVET and VAET difficult. Further efficiently finding the current value for a E + A is difficult to do in SQL in a way that doesn't require maintaining a whole copy of the data. 
  - I actually bumped up against what I believe are weird edge-case bugs in the SQLite query planner when dealing with sparse indexes as well.
  - I think I gave up when trying to implement one-many relationships because the SQL was getting too gnarly(困难的; 挑战性的).

- 
- 

## 👥🔥 [HC-tree is an experimental high-concurrency database back end for SQLite | Hacker News_202301](https://news.ycombinator.com/item?id=34434025)

- 
- 
- 

## 👥🔥🔥 [How SQL Database Engines Work, by the Creator of SQLite (2008) [video] | Hacker News_201806](https://news.ycombinator.com/item?id=17387851)

- 
- 
- 

# more
