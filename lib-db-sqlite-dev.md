---
title: lib-db-sqlite-dev
tags: [sqlite]
created: 2022-06-13T02:59:18.213Z
modified: 2022-06-13T02:59:28.865Z
---

# lib-db-sqlite-dev

# guide

- who is using #sqlite
  - cloudflare-d1

- office
  - 基于sqlite实现office类文档的文件格式，暂无实现
# [limitations-sqlite](https://sqlite.org/limits.html)

## blob

- SQLite blobs have an absolute maximum size of 2GB and a default maximum size of 1GB.
  - An alternate approach to using blobs is to store the data in files and store the filename in the database. Doing so loses the ACID properties of SQLite. There are benchmarks.

- [SQLite Forum: Write large blob, > 2GB_202008](https://sqlite.org/forum/forumpost/756c1a1e48)
  - The 2GB blob size limit is probably not going to go away any time soon. You will definitely need to start splitting blobs.
  - As currently implemented, SQLite constructs an entire row in memory whenever it needs to read or write the last column in the row. So if you have a row that contains an N-byte blob, you'll need at least N bytes of memory (probably a bit more) in order to process that row.
  - for maximum compatibility, you might do well to limit the size of each blob piece to a few megabytes.

## more

# dev
- [35% Faster Than The Filesystem](https://www.sqlite.org/fasterthanfs.html)
  - SQLite reads and writes small blobs 35% faster¹ than the same blobs can be read from or written to individual files on disk using `fread()` or `fwrite()`.
  - The performance difference arises (we believe) because when working from an SQLite database, the open() and close() system calls are invoked only once, whereas open() and close() are invoked once for each blob when using blobs stored in individual files
# more
