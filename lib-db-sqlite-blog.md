---
title: lib-db-sqlite-blog
tags: [blog, sqlite]
created: 2022-11-18T17:06:45.809Z
modified: 2022-11-18T17:06:54.371Z
---

# lib-db-sqlite-blog

# blog-stars

## [Hosting SQLite databases on GitHub Pages or any static file hoster](https://news.ycombinator.com/item?id=27016630)

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
# blog

## [What If OpenDocument Used SQLite?](https://www.sqlite.org/affcase1.html)

- The Open Document Format for Office Applications (ODF), also known as OpenDocument, is an open file format for word processing documents, spreadsheets, presentations and graphics and using ZIP-compressed XML files. 
  - It is also the default format for documents in typical Linux distributions
  - It was based on the Sun Microsystems specification for OpenOffice.org XML, the default format for OpenOffice.org and LibreOffice. 
- The most common filename extensions used for OpenDocument documents are:
  - .odt and .fodt for word processing (text) documents
  - .ods and .fods for spreadsheets
  - .odp and .fodp for presentations
  - .odg and .fodg for graphics
  - .odf for formula, mathematical equations

- Benefits would include:
  - Smaller documents
  - Faster File/Save times
  - Faster startup times
  - Less memory used
  - Document versioning

- Limitations Of The OpenDocument Presentation Format
  - Incremental update is hard.
  - Startup is slow.
  - More memory is required.
  - Crash recovery is difficult.
  - Content is inaccessible.

- First Improvement: Replace ZIP with SQLite
- Second Improvement: Split content into smaller pieces
- Third Improvement: Versioning

- Review Of The Benefits Of Using SQLite
  - An SQLite database file is approximately the same size, and in some cases smaller, than a ZIP archive holding the same information.
  - The atomic update capabilities of SQLite allow small incremental changes to be safely written into the document. This reduces total disk I/O and improves File/Save performance, enhancing the user experience.
  - Startup time is reduced by allowing the application to read in only the content shown for the initial screen. 
  - The memory footprint of the application can be dramatically reduced by only loading content that is relevant to the current display and keeping the bulk of the content on disk.
  - The schema of an SQL database is able to represent information more directly and succinctly than a key/value database such as a ZIP archive. 

## [Consider SQLite](https://blog.wesleyac.com/posts/consider-sqlite)
- There are a few legitimate downsides to using SQLite. 
  - First off, the data type system. It's bad. Luckily, as of a month ago, you can use strict typing instead, which somewhat improves the situation. 
  - Support for migrations is worse — SQLite has essentially no support for live migrations, so you need to instead make a new table, copy the data from the old table into the new one, and switch over. 
- It's significantly harder to geo-shard your app, although you can get very far with CDNs and caches, and once Litestream supports read replicas, there'll be another excellent tool for improving this.
- Using SQLite has some failure modes that most programmers are not used to — most notably, if you begin a transaction, then go off and do some blocking operation, you will be blocking all writes for the time that you're doing that, unlike in a connection-based database with a connection pool. If you want to write fast and scalable apps with SQLite, you need to think carefully about your architecture and schema.
- On the whole, I think using SQLite is a good tradeoff for a lot of projects

## [SQLite Forensics with Belkasoft X](https://belkasoft.com/sqlite)

- In this article, we will review the most forensically(争论，辩论) interesting SQLite features, dangers of using a non-forensic tool for SQLite analysis and offer a set of requirements for a proper tool to use.
- Freelists: a special area inside a SQLite database, which contains recently deleted data
- Journal and Write-Ahead Log (WAL) files: transactional files, which can store recently added or recently deleted data
- Unallocated space: not to be confused with hard drive unallocated space, this SQLite feature allows finding deleted data even outside of freelists
# more

- [SQLite的文艺复兴 - 知乎](https://zhuanlan.zhihu.com/p/601510076)
