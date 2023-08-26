---
title: lib-db-dolt-blog
tags: [blog, dolt]
created: 2023-08-25T21:17:17.666Z
modified: 2023-08-25T21:17:31.432Z
---

# lib-db-dolt-blog

# guide

# [类Git数据库Dolt的使用方法 - 掘金](https://juejin.cn/post/7232600368752115770)
- Dolt支持三种使用模式，三种都可对数据进行版本控制
  - 数据库模式，使用时通过类Mysql客户端连接和操作
  - Git模式，本地修改后推送到远端，只是操作的是表和数据，编辑具体的数据是用dolt sql -q "增册改查sql"来实现。
  - 数据库副本模式，将Dolt配置为Mysql的副本，与Mysql主备模式类似

- 遇到的大坑
  - 我用的腾讯云Mysql8，有些字符排序规则Dolt还没有支持
  - 不支持一些字符排序规则，例如：utf8mb4_0900_ai_ciutf8mb4_0900_ai_ci
  - Dolt部分设置没有做持久化，每次重启时需要重新设置
# [Building with Patterns: The Document Versioning Pattern | MongoDB_201904](https://www.mongodb.com/blog/post/building-with-patterns-the-document-versioning-pattern)
- Document Versioning Pattern
  - This pattern is all about keeping the version history of documents available and usable. 
  - we are able to avoid having to use multiple systems for managing the current documents and their history by keeping them in one database.

- This pattern addresses the problem of wanting to keep around older revisions of some documents in MongoDB instead of bringing in a second management system.
  - we add a field to each document allowing us to keep track of the document version. 
  - The database will then have two collections: one that has the latest (and most queried data) and another that has all of the revisions of the data.
- The Document Versioning Pattern makes a few assumptions about the data in the database and the data access patterns that the application makes.
  - Each document doesn’t have too many revisions.
  - There aren’t too many documents to version.
  - Most of the queries performed are done on the most current version of the document.

- One drawback to this pattern is the need to access a different collection for historical information. 
  - Another is the fact that writes will be higher overall to the database. 
  - This is why one of the requirements to use this pattern is that it occurs on data that isn’t changed too frequently.

- [Building with Patterns: The Schema Versioning Pattern | MongoDB](https://www.mongodb.com/blog/post/building-with-patterns-the-schema-versioning-pattern)
# [So you want a Git Database? | DoltHub Blog](https://www.dolthub.com/blog/2021-11-26-so-you-want-git-database/)
- Dolt implements the Git command line and associated operations on table rows instead of files. 
- Data and schema are modified in the working set using SQL.
- In SQL, dolt implements Git read operations (ie. diff, log) as system tables and write operations (ie. commit, merge) as functions. 
- Dolt produces cell-wise diffs and merges, making data debugging between versions tractable.
- That makes Dolt the only SQL database on the market that has branches and merges.
- You can run Dolt offline, treating data and schema like source code. Or you can run Dolt online, like you would PostgreSQL or MySQL.
# [So you want Database Version Control? | DoltHub Blog](https://www.dolthub.com/blog/2021-09-17-database-version-control/)
- The term of art for version controlling database schema is database migrations.
- If you want your application to be aware of data versioning, you can create some semblance of version control with schema. 
  - The term of art for this is Slowly Changing Dimension. This is not true version control. 
  - You concoct a schema using columns that indicate inactive or active or "active from" to "active to" dates.
  - Then, your application uses these columns to construct present and historical views of the data. Your application never deletes, just changes state from active to inactive. 
- We now have the technology to fully version (ie. lineage, branch, merge, diff) large data! Noms laid the groundwork with a core storage format called a prolly tree, a content addressed binary tree. This data structure allows for fast diff and merge on binary trees, the core data structure in most databases, without compromising too much read or write performance. Recently, a couple new databases have emerged using this or similar technology, TerminusDB for graph or document databases and Dolt for relational databases.
# [So you want Database Versioning? | DoltHub Blog](https://www.dolthub.com/blog/2022-08-04-database-versioning/)
- For the purposes of versioning, a database can be thought of as two separate concepts: schema and data. 
- Schema is all the table definitions, views, constraints, triggers, and stored procedures. 
- Data is the contents of all the tables. 
- Usually data is large scale making it traditionally difficult and costly to version.
- Until recently, database schema was all you could version. The term I heard for for version controlling database schema was database migration. 
- If you want your application to be aware of data versioning, you can create some semblance of version control with schema. The term of art for this is Slowly Changing Dimension. Your application never deletes, it soft deletes
- Noms laid the groundwork with a core storage format called a prolly tree, a content addressed binary tree. 
- This data structure allows for fast diff and merge on binary trees, the core data structure in most databases, without compromising too much read or write performance. 
- Combining prolly trees with a Merkle DAG allows data to be structurally shared across versions, preserving disk space. 
- Recently, a couple new databases have emerged using this or similar technology, TerminusDB for graph or document databases and Dolt for relational databases.
# [How Dolt Stores Table Data | DoltHub Blog](https://www.dolthub.com/blog/2020-04-01-how-dolt-stores-table-data/)
- Dolt is a SQL database that lets you clone, branch, diff, merge, and fork your data just like you can with a filesystem tree in Git. 
- This blog post explores one of the fundamental datastructures that underlies Dolt's implementation of SQL tables.
- Dolt currently supports a subset of SQL where every table must have a primary key
- The SQL layer is implemented on top of a table storage layer that models a key-value store, where keys and values are both byte arrays. 
- The data structure that allows the storage layer to achieve these properties in Dolt is called a Prolly-tree. A Prolly-tree is a block-oriented search tree that combines the properties of a B-tree and a merkle tree. It uses a clever approach to forming variable-sized blocks in order to optimize for structural sharing and to minimize write amplification on small mutations.
- Prolly-tree is at the heart of Dolt's ability to efficiently implement Git functionality, such as branch, merge, and diff, for relational data with SQL semantics.
# [lakeFS: The Guide to Data Versioning](https://lakefs.io/blog/data-versioning/)
- How Is Data Versioning Implemented?
Versioning Approach #1: Full Duplication
Versioning Approach #2: "Valid_from/to" Metadata
Versioning Approach #3: First-class Data Version Control
Versioning in lakeFS

- Data Versioning Best Practices
  - Use TTL's to expire old versions
  - Version semantically, not temporally
    - tying versioning to the start and/or completion of data pipeline tasks. 
  - Leverage versioning for collaboration
# more-blogs
- [Mergeable persistent data structures](https://blog.acolyer.org/2015/01/14/mergeable-persistent-data-structures/)
  - What if you could version-control a (mutable) persistent data structure, inspect its history, clone a remote state and revert it to a previous state?
  - Irmin is an OCaml implementation of this idea, using the Git repository format

- [Dolt数据库版本控制 - 知乎](https://zhuanlan.zhihu.com/p/623256407)
