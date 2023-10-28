---
title: lib-db-sqlite-community-extensions-utils
tags: [community, extensions, sqlite, utils]
created: 2023-10-26T22:12:35.467Z
modified: 2023-10-26T22:12:54.831Z
---

# lib-db-sqlite-community-extensions-utils

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 🪟 Introducing sqlite-xsv - a SQLite extension for quickly querying CSVs!
- https://twitter.com/agarcia_me/status/1613688022079508480
  - Custom delimiters, quotes, column names and types
  - written in Rust, with sqlite-loadable!
- For *non-analytical* queries, I have found sqlite-xsv to be:
  - 1.5-2x faster than other CSV SQLite extensions
  - 1.2-3x faster than @DuckDB, DataFusion, clickhouse-local (!!)
  - 6x faster than pandas
  - 14x faster than sqlite3's .import
  - ~300x faster than dsq, sqlite-utils
- For *analytical* queries 
  - directly on CSVs (ex GROUP BYs and ORDER BYs), both sqlite-xsv and sqlite in general fall short compared to new-age tools like @DuckDB , DataFusion, and clickhouse.


- ## 🪟 [Xlite: Query Excel and Open Document spreadsheets as SQLite virtual tables | Hacker News](https://news.ycombinator.com/item?id=31874767)
- Sqlite does not allow table valued functions to return results with varying schemas. The schema must be defined once up front and then cannot change.
  - That forum post is a request I made to them to allow dynamic columns but they don't seem interested so far.

- ## [Replacing Elasticsearch with Rust and SQLite (2017) | Hacker News_202105](https://news.ycombinator.com/item?id=27175284)
- 
- 
- 

# discuss-sqlite-json/doc
- ## 

- ## 

- ## [Show HN: Squirrelbyte – a SQLite-based JSON document server | Hacker News_202104](https://news.ycombinator.com/item?id=26766557)
- 
- 
- 

- ## 🔥 [SQLite as a Document Database | Hacker News_202011](https://news.ycombinator.com/item?id=25226260)
- 
- 
- 

- ## ✨🔥 [Show HN: Doculite – Use SQLite as a Document Database | Hacker News_202308](https://news.ycombinator.com/item?id=37040359)
- I'm the core maintainer of the npm sqlite package that your library uses. I recommend that you don't make it a direct dependency, but use dependency injection or an adapter pattern that way your library isn't dependent on a specific package version of sqlite/sqlite3

- Just curious if this is using the JSON functions/operators for SQLite under the covers?
  - Yes – I'm using JSON_extract and generated virtual columns https://www.sqlite.org/json1.html#jex Edit: the database is stored in a sqlite.db file in the cwd

- DocuLite lets you use SQLite like Firebase Firestore.
  - Honestly, that sounds absolutely frightening to my ear. There are redis, there is mongo, orient, and plenty of document-based rapid-development databases which will be a substantially better solution than turning sqlite into Firebase.
  - Yes, you can use data change notification callbacks. It is a cool feature of SQLite, but did you know that their performance is a big concern in a large-scale database (document database grows very quickly by design)? What about COUNTs? Batching operations? Deadlocks? This will go out of hand quickly, because a hammer is used as a shovel here.
- I just did a quick search and struggled to find anything about the performance issues you referred to - can you link something so I can take another look? Thanks for the suggestions.
  - From the code, it s easy to see that you create a WRITE transaction which has the side effect of triggering READ transactions. It is also important to understand that if you mix reads and writes you cannot do it well concurrently with SQLite, so every transaction will be sequential and blocking. Looking at the code further I understand that it will not scale well, since a single write can possibly trigger a waterfall of callbacks creating bottlenecks. The problem in your case is that sqlite_update_hook doesn't transport back data and that it is listening for changes in all tables having ROWID optimisation on. So first things first you only need one such callback and a different approach for integrating it in a document abstraction than table name and rowid predicate in a dozen of registered callbacks.
  - You will unveil more problems with SQLite for this job as you dig deeper. **What you really want is fast writes and dumb querying by document id, whereas SQLite gives you an ultra querying suite that you don't utilize but still have to pay with slower writes**. This is a classic system-design problem. Just try rewriting your collection and document abstractions using proper document data storage and you will see how less complicated it is.

- This is cool. There are a tonne of options for local KV stores that likely outperform this by a large margin, but the obvious benefit here is that SQLite is really simple to configure and operate!

- We currently use Realm for this use case. It’s a local database just like SQLite, but with native support for documents and listeners. Did you try that out?
# discuss
- ## 

- ## 

- ## 

- ## 🔥 [SQLite-based databases on the Postgres protocol? Yes we can | Hacker News_202307](https://news.ycombinator.com/item?id=36582255)
- 
- 
- 

- ## 🔥 [SQLite-based databases on the Postgres protocol | Hacker News_202301](https://news.ycombinator.com/item?id=34517474)
- 
- 
- 

- ## 🔥 [Use LibreOffice Base as a GUI for an SQLite Database in OS X (2016) | Hacker News_202212](https://news.ycombinator.com/item?id=34137264)
- 
- 
- 
