---
title: lib-db-sqlite-community
tags: [community, sqlite]
created: '2021-08-30T17:33:26.516Z'
modified: '2021-08-30T17:33:46.086Z'
---

# lib-db-sqlite-community

# guide

### [Hosting SQLite databases on GitHub Pages or any static file hoster](https://news.ycombinator.com/item?id=27016630)

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

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [sqlite rowid after deleting rows](https://stackoverflow.com/questions/35876171)
  - I delete rows with id 3 and 4 and run above query again.
  - Now my problem is rowid not getting reset and holes.
  - 在删除某些行后，其他所有行的rowid不变，不受影响，就会形成断断续续的rowid
- rowid is really special. So special that if you have an `INTEGER PRIMARY KEY` , it becomes an alias for the rowid column. 
  - when your primary key is an alias for rowid, it would be terribly inconvenient if this could change. 
  - Since rowid is now aliased to your application data, it would not be acceptable for sqlite to change it.
- If you really really really absolutely need the rowid to change on a VACUUM, you can avoid this aliasing behavior. Note that it will decrease the performance of any table lookups using your primary key.
  - To avoid the aliasing, and degrade your performance, you can use `INT` instead of `INTEGER` when defining your key