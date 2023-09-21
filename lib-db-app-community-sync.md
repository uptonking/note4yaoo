---
title: lib-db-app-community-sync
tags: [community, data-sync, database, synchronization]
created: 2023-09-17T17:35:30.868Z
modified: 2023-09-17T17:35:53.774Z
---

# lib-db-app-community-sync

# guide

- partial-sync
  - 参考sqlite+http-range的部分下载示例(sql.js-httpvfs)
# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## [Kb: A minimalist hacker-oriented knowledge base manager | Hacker News_202009](https://news.ycombinator.com/item?id=24506280)
- For me this kind of tool needs to provide a way to sync between devices to be useful, and ideally be available on mobile. As it's using sqlite3 to store documents, it's probably not trivial to sync with something like Dropbox.
- Why would a sqlite3 DB file not be trivial to sync with Dropbox or Syncthing? Are there platform-specific nuances to decoding or something?
  - Syncing at db-file level would create false sync conflicts when making edits while offline. You may even lose data, depending on how Dropbox/Syncthing resolve file-level conflicts. For fully automatic sync, you need to operate at the level of records.
- You may even lose data, depending on how Dropbox/Syncthing resolve file-level conflicts.
  - It's even worse - Dropbox can corrupt the database file even without conflicts - it's not safe to copy database file which is currently open in some process since it can change within the reading operation. I mean, the original file stays OK, but the copy will be likely corrupt (and in this corrupt state synced into another instance).
  - For safe copy, Dropbox would have to force some FS-level snapshotting, but that would halt all database operations. I have received few bug reports for my app which were eventually traced into attempts to sync it with Dropbox and similar services.



