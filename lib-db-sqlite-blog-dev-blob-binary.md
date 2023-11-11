---
title: lib-db-sqlite-blog-dev-blob-binary
tags: [binary, blob, blog, sqlite]
created: 2023-11-10T18:33:07.973Z
modified: 2023-11-10T18:34:09.451Z
---

# lib-db-sqlite-blog-dev-blob-binary

# guide

# blogs

# more

# discuss-blob
- ## 

- ## 

- ## 

- ## 🆚️ [Faster than the filesystem (2021) | Hacker News_202301](https://news.ycombinator.com/item?id=34387407)
- the "SQLite: Past, Present, and Future" paper has an updated version of this benchmark (see section 4.3 Blob manipulation), and also compares it with DuckDB.
- Lots of small files (particularly in a single directory) is a known failure mode of many OS filesystems. I
- Maybe node_modules could move to SQLite.

- Anyone else think maybe AWS (S3) has made this optimization already? 
  - Object stores typically do optimizations where they store small files using a different strategy than large ones, maybe directly in the metadata database.
- S3 has always been designed and optimised for large files. In order to maintain high availability they deliberately trade away latency. So this blog only really applies to local filesystems not object stores like S3.
- Facebook had a published paper on their storage system for pictures, haystack, which iirc is something like a slab allocation. S3 is similar, in the sense that it has completely different usage than a file system (no hierarchy, direct access, no need for efficient listing etc) so I'm pretty sure they use something similar.

- 🤔 Would it make sense to store images as blobs if I’m building a web app using SQLite then? Or is this specifically small images only? Saves having to do backups of data and images separately
  - one disadvantage of updating one huge file is it's harder to do efficient incremental backups. Theoretically it can still be done if your backup software supports e.g. content-defined chunking (there was a recent HN thread about Google's rsync-with-fastcdc tool). 
  - If you choose to store your assets as separate files instead though, you can trivially have incremental backups using off-the-shelf software like plain old rsync
- Although for SQLite in particular, you can do streaming incremental backups with Litestream

- ## 🆚️ [SQLite is 35% Faster Than The Filesystem (2017) | Hacker News_202107](https://news.ycombinator.com/item?id=27897427)

- ## 🆚️ [35% Faster Than The Filesystem (2017) | Hacker News_201908](https://news.ycombinator.com/item?id=20729930)

- ## 🆚️🪶📂 [SQLite small blob storage: 35% Faster Than the Filesystem | Hacker News_201706](https://news.ycombinator.com/item?id=14550060)
- I must point out Jim Gray's paper To Blob or Not To Blob. His team considered NTFS vs. SQL Server, but most rationale applies to any filesystem vs. database decision.
  - The summary was "The study indicates that if objects are larger than one megabyte on average, NTFS has a clear advantage over SQL Server. If the objects are under 256 kilobytes, the database has a clear advantage. Inside this range, it depends on how write intensive the workload is, " but keep in mind this is spinning media from 2006. 
  - Modern SSDs change the equation quite a bit, as they are much more friendly to random IO and benefit less from database write-ahead log and buffer pool behavior.
  - when deciding between blob vs. filesystem, blobs bring transactional and recovery consistency. The DB is self contained, and all blobs are contained in it. A restore of the DB on a different system yields a consistent system
- Despite all this, my practical experience is that filesystem is better than blobs for things like uploaded content, images, pngs and jps etc. 
  - Blobs bring additional overhead, require bigger DB storage (more expensive usually, think AWS RDS) and the increased size cascades in operational overhead (bigger backups, slower restore etc).

- Store the files in a database but expose them via FUSE.
  - That gives you the time cost of a filesystem plus the time cost of a database plus an extra round-trip in and out of kernel space.

- ext4 uses btrees for the directory index, so accessing files by name is just as fast as manually splitting it into a prefix-based directory tree.
  - Searching by filename on the other hand can be much faster with a prefix tree because directories only allow linear scans, not range-based ones.

- > Despite all this, my practical experience is that filesystem is better than blobs for things like uploaded content, images, pngs and jps etc.
  - This is especially true if you want to deliver them back to the users in the context of a web application. If you place this kind of content in a database, you'll need to serve them with your application.
  - If you use files for this content, you get two interesting options. For one, you can use any stock web server like nginx to serve these files - and nginx will outperform your application in this context. On top of that, it's easy to push this content onto a CDN in order to further cut the latency to the user.

- I personally prefer the database... But I think for it to work well you need a better strategy than just large BLOBs.
  - GridFS for MongoDB - https://docs.mongodb.com/manual/core/gridfs/
  - ReGrid for RethinkDB - https://github.com/internalfx/rethinkdb-regrid
  - I'm sure the same concept could apply to other databases.

- You have two consystency issues with storing the files in the filesystem:
  - rollbacks in the DB can lead to orphaned files on disk. One can try to add logic in the app (eg. a catch block that removes the file if the DB rolled back) but that is not gonna help on a crash
  - it is impossible to obtain a consistent backup of both the DB and the filesystem. You can backup the filesystem and the DB, but the two will not be consistent between them unless you froze the app during the backup. This is because the moment at which the backup 'views' the file and the DB record referencing it are distinct in time.
- Another pain point is backup; it's not possible to create a consistent snapshot of (rdbms state, other state on the file system). This is avoided entirely if you only need to snapshot (rdbms state, ).

- 🌰 For web map tiles (millions of tiny PNGs), everyone who's anyone stores their tiles in sqlite rather than on disk
  - Originator of MBTiles format here. The initial intentions were moving 100, 000s of raster map tiles between computer and mobile device, either over USB or network. Main benefit was avoiding per-file transaction overhead, as well as checksumming potential. Side benefits included a small space savings over filesystem because of block overhead, plus later iterations allowed for de-duplication of e.g. all-blue water map tiles. These days, we still use the format for transport between local machine and the Mapbox backend, despite having moved to "vector tiles", which essentially are protocol buffer-based encoded geometries directly.
  - Also, to clarify a bit on why spatial capabilities weren't part of the MBTiles spec: when rendering maps, you assemble tiles for a given zoom scale in the vertical and horizontal directions, like a checkerboard. The unique tuple defining a particular square on the map is z/x/y — zoom level, horizontal, vertical. So stuffing these into SQLite and uniquely keying across z/x/y there makes for fast retrieval at render time.

- This is weird benchmarketing. They are comparing reading/writing 100, 000 individual files vs writing 100, 000 entries into a single file(sqlite database). For comparison one could concatenate the same data into a single big file even faster than into sqlite.

- SQLite is good when you’re mostly reading. For writing, the major drawback of SQLite is it doesn’t support concurrent writes. All filesystems do (at least when writing different files), all full-fledged RDBMS-es do, even some embedded databases do (like ESENT). Yet, in SQLite only a single thread can write.
