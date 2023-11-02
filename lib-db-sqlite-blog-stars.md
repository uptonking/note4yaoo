---
title: lib-db-sqlite-blog-stars
tags: [blog, sqlite]
created: 2023-10-26T17:32:53.997Z
modified: 2023-10-26T17:33:04.929Z
---

# lib-db-sqlite-blog-stars

# guide

# blog-stars

## 🌵 [Tracking SQLite Database Changes in Git_202311](https://garrit.xyz/posts/2023-11-01-tracking-sqlite-database-changes-in-git)

- SQLite stores data in binary.If you want to track changes and updates to a database using Git, you won't be able to see full diffs by default. 
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
