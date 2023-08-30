---
title: lib-db-dolt-blog
tags: [blog, dolt]
created: 2023-08-25T21:17:17.666Z
modified: 2023-08-25T21:17:31.432Z
---

# lib-db-dolt-blog

# guide

- resources
# author-blogs
- [Have Postgres. Want Dolt. | DoltHub Blog](https://www.dolthub.com/blog/2022-03-28-have-postgres-want-dolt/)

- [Benchmarking Dolt with TPC-C | DoltHub Blog](https://www.dolthub.com/blog/2022-09-16-tpcc-update/)

- [Everything through the SQL Engine | DoltHub Blog](https://www.dolthub.com/blog/2022-01-22-everything-to-sql-path/)

- [Maintained Wikipedia ngrams dataset in Dolt | DoltHub Blog](https://www.dolthub.com/blog/2019-12-04-maintained-wikipedia-ngrams-dataset/)

- [How Dolt Types Work | DoltHub Blog](https://www.dolthub.com/blog/2020-04-15-how-dolt-types-work/)
# [Three-Way Merges in Dolt: Modeling Schema Conflicts | DoltHub Blog](https://www.dolthub.com/blog/2023-05-01-schema-conflicts/)
- At the storage layer, Dolt and Git both leverage Merkle-Trees that enable scalable diff algorithms. 
  - However, Dolt's implementation is specifically tailored to handle database tables and schemas. 
  - This unique storage engine is what sets it apart from other databases: it was built from the ground up to support the database version control use-case.
- Dolt's three-way merge model is designed to accommodate a wide range of workflows and scenarios, making it a versatile and powerful tool for Dolt users
- Today's blog details the mechanics of three-way merge in Dolt and how we solved the problem of versioning schema and data with a performant approach.

- we have a database with one table and two branches. Both branches have made changes since the common ancestor
  - Post-merge we can see that all the changes are reflected on the tip of branch main and the history of both branches are reflected in the commit log. 
  - Merkle-Tree storage engine allows this merge process to scale sub-linearly with the size of the table, regardless of how deep and complicated the commit history is. The cost of doing a three-way merge only depends on the size of the change sets being merged.

- 👉🏻 **Dolt's three-way merge algorithm works by first reconciling schema differences between each side of the merge, and then merging the table data using this new schema**.
- Dolt's merge algorithm is "cell-wise", meaning we can automatically merge any change sets that are disjoint at the cell level. 
  - However, if both branches change the same cell to a different value, we have no choice but to escalate this decision to the user and let them decide what the final value should be
- When two branches both modify the same portion of a table's schema, we must escalate the resolution decision to the user and let them decide what the final schema should look like. You can find a full list of Dolt's schema conflict rules in the docs 

- This approach to version control allows users to keep track of changes to database schema and data, making it easier to collaborate with others and maintain a consistent version history.
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
# [So you want Database Forks? | DoltHub Blog](https://www.dolthub.com/blog/2022-07-29-database-forks/)
- Conceptually, a "fork" in the software context is a copy that can be modified with the intent of living on as a separate copy
  - This is distinct from a "branch" which implies the intent to merge the changes on the copy back into the original
  - A "fork" means you are making a copy and never coming back.

- Making a database fork is pretty simple practically. 
  - First, you create a backup. 
  - Then you restore from the backup in another location, like on another server.
  - The issue with this approach is backing up and restoring can be slow. 
  - If you abstract the storage from the database, you maybe be able to fork faster. 

- Cloud Hosted Databases Make Forking Easy
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
# [So You Want Git for Data? | DoltHub Blog](https://www.dolthub.com/blog/2020-03-06-so-you-want-git-for-data/)
- Do you mean data versioning? If so, which parts of version control do you care about? Do you care about rollback? Diffs? Lineage, i.e. who changed what and when? Branch/merge? Sharing changes with others?

- we encountered a number of products with some relationship to “Git for data”. 
  - We narrowed the list to nine
- The products fell into three general categories

## Data catalogs

### Kaggle

- Kaggle started by hosting machine learning competitions. 
- The contest runner posts an open dataset, sets the terms of the contest, and receives model submissions.
- It has evolved into a social network of sorts for data scientists, continuing to run contests, but also hosting public datasets and modeling code in the form of notebooks. 
- The datasets are distributed as CSVs or JSON. Datasets are versioned in the sense that older versions are still available on Kaggle.

### data.world

- an online tool for building data projects. 
- As part of data projects there is data hosting. 
- The focus is at a higher level than the data itself. On data.world, you create a data project with data, documentation, queries, insights, etc.
- You can collaborate and share those projects with other people.
- I could not locate a versioned dataset but there is an activity link on the dataset page. It looks like data versioning is not really a priority for data.world.

### Quilt

- Quilt v2 as Yum, Homebrew, or NPM for data
- The data was immutable and versioned, as in multiple versions of the packages existed in the central repository, but there was no diff or branch/merge.
- v2019 launch seemed to indicate the shift from data versioning to data discovery on top of S3.

### qri

- Qri is a data catalog built on the distributed web. 
- There is a command line tool as well as a desktop application to get access to and publish datasets.
- Qri structures data into a few components including the schema and data, but also metadata like a README.
- Qri really seems to be chasing the “Git and GitHub for data” analogy pretty closely
- I struggled with whether to put Qri in the data catalog or versioned database section of this blog
  - I settled on the data catalog section because fundamentally, Qri is not a database. 
  - It is a wrapper around a file-based data format. 
  - There is no query language and I don't think it handles multiple tables in the same dataset right now.

## Data pipeline versioning

### Pachyderm

- Pachyderm is a data pipeline versioning tool. 
- In the Pachyderm model, data is stored as a set of content-addressed files in a repository. 
- Pipeline code is also stored as a content-addressed set of code files. 
- When pipeline code is run on data, Pachyderm models this as a sort of merge commit, allowing for versioning concepts like branching and lineage across your data pipeline.

### DVC (Data Version Control)

- Similar to Pachyderm, DVC versions data pipelines. 
- Unlike Pachyderm, DVC does not have its own execution engine. 
- DVC is a wrapper around Git that allows for large files (like git-lfs) and versioning code along with data. 
- It also comes with some friendly pipeline hooks like visualizations and reproduce commands.
- DVC seems lighter weight and more community-driven than Pachyderm. 

### Noms

- The versioned, forkable, syncable database.
- Attic Labs sold to Salesforce in January 2018. The open source project has not seen many updates since.
- Aaron Boodman, the founder and CEO, recently announced a new project that may or may not be Noms-based called Replicache. 
- Noms implements a Merkle DAG that allows the database to be truly distributed, just like Git.
# [How Dolt Stores Table Data | DoltHub Blog](https://www.dolthub.com/blog/2020-04-01-how-dolt-stores-table-data/)
- Dolt is a SQL database that lets you clone, branch, diff, merge, and fork your data just like you can with a filesystem tree in Git. 
- This blog post explores one of the fundamental datastructures that underlies Dolt's implementation of SQL tables.
- Dolt currently supports a subset of SQL where every table must have a primary key
- 👉🏻 The SQL layer is implemented on top of a table storage layer that models a key-value store, where keys and values are both byte arrays. 
- The data structure that allows the storage layer to achieve these properties in Dolt is called a Prolly-tree. 
  - A Prolly-tree is a block-oriented search tree that combines the properties of a B-tree and a merkle tree. 
  - It uses a clever approach to forming variable-sized blocks in order to optimize for structural sharing and to minimize write amplification on small mutations.
- Prolly-tree is at the heart of Dolt's ability to efficiently implement Git functionality, such as branch, merge, and diff, for relational data with SQL semantics.
# [Introducing Secondary Indexes | DoltHub Blog](https://www.dolthub.com/blog/2020-05-22-introducing-secondary-indexes/)
- Indexes are a data structure that is used by many relational databases to allow for quick retrieval of a value given a key. 
- Typically indexes are implemented as additional tables that reference the target table, but in all cases, they rely upon the data that is stored in their target table.
- indexes are not always perfect for every table, as they incur a performance penalty to write operations on those tables, since the **indexes must be kept in sync with their target table's data**. 
  - If a table is primarily for storage of data, with a relatively small amount of retrieval of that data, then an index may hurt more than help. 
  - However, for tables that are heavily read from, indexes are the best option to improve query performance.
- For the user, indexes usually don't involve any extra bookkeeping after their creation. The database updates the indexes for you, allowing you to keep the same workflow as before their creation.

- Perhaps the most common index is usually one that isn't referred to as such: the primary key! It has special significance in that it is used to determine the uniqueness of a row in a table
- primary keys may be one of the most well-known indexes, but they're far from the only one. 
  - We call all of these other indexes "secondary indexes". 
- For this article, I'll just mention three others
- the column index
  - It may be applied to a single column, and it supports the majority of commonly-used data types, such as INT, DATETIME, VARCHAR, etc
- composite index
  - applied to multiple columns, and generally the order of the columns is important.
  - The data types allowed are the same as with column indexes.
- unique indexes
  - These are either column or composite indexes, however they have a unique constraint on them. 
  - This constraint enforces uniqueness amongst the values or value combinations within a table.
  - Some databases will actually make use of a unique index as the primary key if one is provided during table creation and no explicit primary key is specified.

- 💡 How they're implemented in Dolt
- In Dolt, table data is implemented as a sorted map, with 
  - the key being a tuple of the primary keys, 
  - and the value being a tuple of all of the other columns.
- For indexes, this idea is modified a bit. 
  - For the key tuple, we take the columns that are indexed and append the primary keys to them (if they're not a part of the indexed columns), and store that as the key for the map. 
  - The value is left empty, which essentially turns the map into a set.

- If we did not have a secondary index, then we would have to scan the entire table, row by row, to find all rows that satisfy the conditions.
  - However, by using the index, we can jump to where we first find 1.0, and iterate until we find a different number
- indexes make writes more expensive. 
- Right now, Dolt has full support for column, composite, and unique indexes.
- In the future, we plan to add support for index prefixes (also known as partial indexes), fulltext indexes, and spatial indexes. 
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

- [What's a good algorithm for 2-dimensional diffs? | Lobsters](https://lobste.rs/s/ypmznb/what_s_good_algorithm_for_2_dimensional)

- [Git like Branching with Graph database](https://digitalcarpenter.dev/graph-branching-timeseries)
