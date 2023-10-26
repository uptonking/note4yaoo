---
title: lib-db-sqlite-blog
tags: [blog, sqlite]
created: 2022-11-18T17:06:45.809Z
modified: 2022-11-18T17:06:54.371Z
---

# lib-db-sqlite-blog

# guide

# blog

## [Show HN: Reduce SQLite database size by up to 80% with transparent compression | Hacker News_202208](https://news.ycombinator.com/item?id=32303762)

- 
- 
- 

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

## [Consider SQLite_202112](https://blog.wesleyac.com/posts/consider-sqlite)

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

## 📝 [SQLite is not a toy database_202103](https://antonz.org/sqlite-is-not-a-toy-database/)

- 
- 

## 👥🔥 [SQLite is not a toy database (2021) | Hacker News_202208](https://news.ycombinator.com/item?id=32478907)

## 👥🔥 [SQLite is not a toy database | Hacker News_202103](https://news.ycombinator.com/item?id=26580614)

- 
- 
- 

## 📝 [SQLite the only database you will ever need in most cases_202104](https://unixsheikh.com/articles/sqlite-the-only-database-you-will-ever-need-in-most-cases.html)

- 
- 
- 

## 👥🔥 [SQLite the only database you will ever need in most cases (2021) | Hacker News_202302](https://news.ycombinator.com/item?id=34812527)

- 
- 
- 

## 👥🔥 [SQLite the only database you will ever need in most cases | Hacker News_202104](https://news.ycombinator.com/item?id=26816954)

- 
- 
- 

# more
- [SQLite的文艺复兴 - 知乎](https://zhuanlan.zhihu.com/p/601510076)

- [Exciting SQLite Improvements Since 2020 | Hacker News](https://news.ycombinator.com/item?id=35740683)
