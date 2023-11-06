---
title: lib-db-postgresql-blog-xp
tags: [blog, dev-xp, postgresql]
created: 2023-10-26T17:28:59.526Z
modified: 2023-10-26T17:29:11.388Z
---

# lib-db-postgresql-blog-xp

# guide

# blogs

# more

- [PostgreSQL: No More VACUUM, No More Bloat_202307](https://www.orioledata.com/blog/no-more-vacuum-in-postgresql/)
  - The way InnoDB does this is by effectively doing two writes: the fsync’d-ack-end-user store is a ringbuffer that then gets copied in bulk into the main db file with a whole page-reuse scheme. It is very complicated and took half a decade to get correct and fast.
