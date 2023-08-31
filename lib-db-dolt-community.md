---
title: lib-db-dolt-community
tags: [community, database, dolt]
created: 2023-08-25T21:16:51.669Z
modified: 2023-08-25T21:17:11.979Z
---

# lib-db-dolt-community

# guide

- creators
  - https://twitter.com/ZachMusgrave
# discuss-versioning
- ## 

- ## [数据库版本管理应该如何实现？ - 知乎](https://www.zhihu.com/question/20080857/answers/updated)
- 😣 目前是把DDL、存储过程、函数、核心数据整理成SQL文件，做为baseline，提交SVN；
  - 每次修改，均记录到文件、整理成增量的sql update语句，提交svn；同时更新整体的SQL语句。
  - 很复杂，尤其是开发、内部测试、客户手上多个版本，想死的心都有了

- [用版本控制工具将数据库版本化](https://blog.csdn.net/tywo45/article/details/2480078)
  - 版本化数据库的起点——创建一个数据库Schema基线，这个基线是一些数据库脚本（包括 create table ，alter table ，drop table ，insert data ，update data ，delete data等）。
  - 这些脚本可以位于同一.sql文件中，也可根据其它规划分别位于不同文件中，例如将视图脚本，初始化数据脚本，建表脚本分别置于不同的文件中。
# discuss-dolt-stars
- ## 

- ## 

- ## 

- ## 

- ## [Building a branched versioning model for relational databases - Database Administrators Stack Exchange](https://dba.stackexchange.com/questions/74210/building-a-branched-versioning-model-for-relational-databases)
- Managing and keeping track on data modification (insert, update, delete) can be done quite easy using an audit table with trigger that keep track on every change.

- ## Anyone have a good algorithms for minimum 2-dimensional diff? 
- https://twitter.com/DoltHub/status/1331751370802642944
  - Input is 2 trimmed and clean CSVs (files don’t end in \n; lines don’t end in , ; no quotes or escaping)
- Okay an honest review (one of two tweets). 
  - 1) I think you are at the forefront of this space 
  - 2) I think there's a clear target everyone should aim for. 
  - 3) forget about SQL for a long while. 
  - 4) focus on TSVs 
  - 5) "**Dolt is Git for TSVs**".
  - 6) You can do really clever things with 2-D diffs, and do an end around on Git. 
  - 7) Git's only serious weakness is its 1D nature. 
  - 8) In 2027, most source code will be written in 2-d (https://longbets.org/793/) and dolt could be the VCS for 2-d.

- My predictions are often wrong. But I do think nailing Git for TSV may make sense, then graduate to SQL (though I understand the latter is where the businesses are). I'm not 100% positive what "git for TSV" even means but the links here are good

- why would I want to store my data in a binary dolt file? 
  - Why not just CSVs? 
  - Plain text, little noise, super fast sync via git, and works with thousands of applications and web apps.

- We think the real answer is if you want both versioning (diffs, branch, merge) and a shareable database, Dolt is the answer. If you want one or the other, CSVs in Git or SQLite are fine answers.

- ## As part of our Dolt 1.0 launch extravaganza, DoltHub runs on Dolt now._202305
- https://twitter.com/timsehn/status/1657072076531064834
  - [DoltHub on Hosted Dolt | DoltHub Blog](https://www.dolthub.com/blog/2023-05-12-dolthub-on-hosted-dolt/)
  - Note, the OLTP database on DoltHub is used to store things like users, organizations, pull requests, etc. 
  - The actual Dolt data is stored and served from S3 through an API. 
  - The OLTP database on DoltHub doesn't do the heavy stuff.

- ## discuss-author
- https://twitter.com/DoltHub/status/1694034481739390984
- We want Dolt to be a drop-in replacement for MySQL.
  - A customer reported problems getting XCA to work with Dolt. 
  - So we fixed the missing functionality and now XCA works with a Dolt database backend! 

- We are a fork of Noms. Lots of incremental changes and we're in the process of a major storage engine overhaul (what we use Noms for) for performance as we speak.

- 
- 
- 
- 
- 

# discuss-dolt
- ## 

- ## 

- ## [Dolt is Git for data | Hacker News_202003](https://news.ycombinator.com/item?id=22731928)

- Does Dolt have any benchmarks against other databases at scale? I would think that a git SQL database would not be very snappy at scale
  - We're working on building performance benchmarks right now. We started with correctness. 
  - We think over time (like years) we can achieve read performance parity with MySQL or PostgreSQL. 
  - Architecturally, we will always be slower on write than other SQL databases, given the versioned storage engine.
- Right now, Dolt is built to be used offline for data sharing. And in that use case, the data and all of its history needs to fit on a single logical storage system. 
  - The biggest Dolt repository we have right now is 300Gb. It tickles some performance bottlenecks.
  - In the long run, if we get traction we imagine building "big dolt" which is a distributed version of Dolt, where the network cuts happen at logical points in the Merkle DAG. Thus, you could run an arbitrarily large storage and compute cluster to power it.

- With Dolt, you can view a human-readable diff of the data you received last time versus the data you received this time. How is this accomplished if the data is binary?
  - No data diffs is the data is binary. But diffs are cell-wise
  - `git-lfs` lets you put store large files on GitHub. 
  - With Dolt, we offer a similar a similar utility called `git-dolt`. 
  - Both these allow you to store large things on GitHub as a reference to another storage system, not the object itself.

- 
- 
- 
- One really important feature of time series data is the preservation of what the dataset looked like at each point in time. 
  - Financial data providers will make a mistake (off by order of magnitude, missed a stock split, etc) and then go back and correct it. 
  - This means you end up training models entirely on corrected data, but trade based on uncorrected data.

- storage engine is a mashup of a Merkle DAG and a B-tree called a Prolly Tree

- What is your take on the need for time-travel queries for versioned, mutable data?
- The storage system we use only stores the rows that change. 

- For the record, Replicache uses Noms internally, so I think ... something ... will still become of Noms. We're just not sure how to move forward with it at this point.

- 
- 
- 
- 

- Is it feasible to use Conflict-free Replicated Data Types (CRDT) for this?
  - I'm not familiar with CRDT. Will read up on that.
- you can read some of the old docs from Noms here (Dolt uses a fork of Noms as its internal storage layer).
  - To answer your question, it is pretty easy to make Noms (or Dolt) into a CRDT by defining a merge function that is deterministic.
  - We experimented with this in Noms but the result wasn't that satisfying and we didn't take it any further
  - [Noms — The Decentralized Database](https://github.com/attic-labs/noms/blob/master/doc/decent/about.md)
    - Like most databases, Noms features a rich data model, atomic transactions, support for large-scale data, and efficient searches, scans, reads, and updates.
    - Unlike any other database, Noms has built-in multiparty sync and conflict resolution. This feature makes Noms a very good fit for P2P decentralized applications.

- How does this compare to something like Pachyderm?
- Weighing in as Pachyderm founder.
  - We're designed for version controlling data pipelines, as well as the data they input and output.
  - Pachyderm's filesystem, pfs, is the component that's most similar to dolt. Pfs is a filesystem, rather than a database, so it tends to be used for bigger data formats like videos, genomics files, sometimes databases dumps. 
  - And the main reason people do that is so they can run pipelines on top of those data files.
  - Under the hood the datastructures are actually very similar though, we use a Merkle Tree, rather than a DAG. 
  - But the overall algorithm is very similar. 
  - Dolt, I think, is a great approach to version controlling SQL style data and access. Noms was a really cool idea that didn't seem to quite find its groove. 
  - Whereas dolt seems to have taken the algorithm and made it into more of a tool with practical uses.

- Git succeeded because it was free, and then business models were able to be built up around the open-source ecosystem after a market evolved naturally. There is a need, but if you go into it trying to build a business from scratch, you're going to have a bad time.
- Mercurial has since added features, that are not the recommended workflow according to their docs, to have similar branching model to git but the default "as designed" workflow of hg is arguably inferior to git 

- 关于产品方向的改变
- I started a company with the same premise(前提; 假定, 假设) 9 years ago, during the prime "big data" hype cycle. 
  - We burned through a lot of investor money only to realize that there was not a market opportunity to capture. 
  - That is, many people thought it was cool - we even did co-sponsored data contests with The Economist - 
  - but at the end of the day, we couldn't find anyone with an urgent problem that they were willing to pay to solve.
  - Perhaps things have changed; we were part of a flock of 5 or 10 similar projects and I'm pretty sure the only one still around today is Kaggle.
- We also started "Git for data" several years ago but since then pivoted to data science/ML tooling by building features that people actually want on the original product. 
  - I guess "Git for data" is not very useful if you don't have the whole platform built around it to actually use the features. We mainly use it for data synchronization between the nodes and provenance tracking so people can see what data was used to build specific models and to track how the project evolves itself without forcing people to "commit" their changes manually (as we have seen that often data scientists don't even use git, just files on their Jupyter notebooks).

- https://github.com/dat-ecosystem/dat
  - this project is old. I brought it up in the context of older projects, independent of whether they succeeded pivoted, etc. (2013) - 'Introducing Dat: If Git Were Designed For Big Data' Talk by the founder.
  - My point is they pivoted and so maybe this idea won't work, or this was too early.
  - Dat is more about distribution (decentralized, distributed, P2P) but it's not possible to make queries.
  - Yes, the project used to associate itself as a git for data, but I guess not in the sense of a db.
  - That project looks like a command-line p2p file sharing system. There doesn't appear to be any branching. It also doesn't appear to be a database (like with a schema), but simply raw files being passed around. There's no data types or queries.

- ## [Dolt is Git for Data | Hacker News_202103](https://news.ycombinator.com/item?id=26370572)
- Dolt might be good but never underestimate the power of Type 2 Slowly Changing Dimension tables

- I don't see how it can be for production databases involving lots of users, because while it seems appealing as a way to upgrade and then roll back, you'd lose all the new data inserted in the meantime. When you roll back, you generally want to roll back changes to the schema (e.g. delete the added column) but not remove all the rows that were inserted/deleted/updated in the meantime.

- One of the main use cases you can see them targeting, and that I think makes a ton of sense, is providing tools for collecting, maintaining and publishing reference data sets using crowd sourcing.

- It is not the first time I have seen immutable B-trees being used as a method for being able to query a dataset on a different point in time.
  - Spanner (and its derivatives) uses a similar technique to ensure backup consistency. Solutions such as CockroachDB also allows you to query data in the past, and then uses a garbage collector to delete older unused data. The Time-to-live of history data is configurable.
  - I just find interesting that both databases (CockroachDB and Dolt) share the same principal of immutable B-Trees.

- I've looked into Dolt perviously for powering our product that is Git for financials.
  - The trouble is that most of our complexity lies in our data's relationships. 
  - Merging is very tricky when some data that has been added in one branch has not had a specific change in properties when other data in a master branch has been modified.
- Good point - and why a graph based approach has advantages in some use cases (disclaimer TerminusDB co-founder here). Allows more flexibility in versioning relationships and more scope to merge in the scenario you outline.

- Is it for versions of the database design or versions of the data?
  - Both. Schema changes are versioned like everything else. But depending on what the change is, it might make merges difficult.

- This could be useful for integration tests, especially for testing schema changes.

- It is a database. It implements the MySQL dialect and binary protocol, but it isn't MySQL. Totally separate storage engine and implementation.
- Is this mysql only?
  - It uses the mysql SQL dialect for queries. But it's its own database.

- ## [Dolt is Git for Data | Hacker News_202206](https://news.ycombinator.com/item?id=31847416)
- This is the future of databases, but nobody seems to realize it yet.
- One of the biggest problems with databases (particularly SQL ones) is they're a giant pile of mutable state. 
- The whole idea of "migrations" exists because it is impossible to "just" revert any arbitrary change to a database, diff changes automatically, merge changes automatically. 
  - You need some kind of intelligent tool or framework to generate DDL, DML, DCL, they have to be applied in turn, something has to check if they've already been applied, etc. 
  - And of course you can't roll back a change once it's been applied, unless you create even more program logic to figure out how to do that. It's all a big hack.
- By treating a database as version-controlled, you can treat any operation as immutable. 
- The effect is going to be as radical as the popularization of containers.

- This is how relational databases have commonly worked since at least the 1990s and is called multi-version concurrency control (MVCC).
  - Welcome to the future, it is called PostgreSQL. 
- There are at least two reasons no sensible database designer would allow users to operate a database in this way even though they are technically capable of it.
- First, keeping every version of every piece of data forever is an excellent way to consume non-intuitively vast amounts of storage even if your data model is tiny.
  - Every time this feature has been offered by databases, it immediately causes a rash of "out of storage" errors that force the user to manually and permanently delete large numbers of old versions.
  - This is extremely user-unfriendly, so the feature is almost immediately removed in subsequent versions because the pain it causes far outweighs the benefits even when used carefully. 
  - In typical MVCC systems, old versions are aggressively garbage collected automatically to limit out-of-storage errors.
- Second, finding or reconstructing an arbitrary number of old versions of data is unavoidably expensive. 
  - Much of the architectural difference between various MVCC implementations are trying to manage the rather severe performance tradeoffs of maintaining multiple versions of data and navigating to the version you need, with the understanding that all of these versions live on storage and rarely in a single place. 
  - There is no optimal way, and keeping version chains short is critical for good performance.
- There is very deep literature around MVCC-style databases. The challenges of generalizing and maximally exploiting MVCC as a user feature while having performance that is not poor to the point of unusability are thoroughly documented.

- MVCC is not version control, and time travel / historical querying is not version control.
- Dolt's unique functionality isn't time travel, although it has that. It's version control, i.e. branch and merge, push and pull, fork and clone. A bunch of database products give you some of this for schema migrations, but Dolt is the only one that does it for table data as well.

- It is not a new idea. True git-like version control systems for managing large volumes of data have been built on MVCC kernels for a decades -- branch and merge, push and pull, fork and clone.
  - The platforms always had the ambition to be general but the design tradeoffs required to make them scale requires narrowly overfitting for a particular type of data model such that they can only be used for the original use case. And even then, the performance ends up being not good.
- Git-like version control requires a Merkle DAG. Unless you know something I don't, there are no RDBMS products that incorporate a Merkle DAG for storage. Dolt is the first.
  - Table data is stored in a cross between a Merkle DAG and a B Tree (a prolly tree), which is what makes diff / merge performant and scalable. We didn't invent these data structures but we believe we are the first to build a SQL database on them.

- Git-like version control requires a Merkle DAG.
  - This is false, you are conflating the abstract algorithm with a narrow implementation. 
  - Tangentially(偏题的，略微相关的；不直接相关的), the "prolly tree" is intrinsically(本质的；内在的) not a scalable data structure. That may satisfy your design requirements but I can't tell.
- > Tangentially, the "prolly tree" is intrinsically not a scalable data structure.
  - First: Dolt publishes industry standard performance benchmarks and they are an average of 4.4x slower than MySQL
  - This is using the original storage format from noms which wasn't written for oltp workloads. A new storage format is coming which is and will dramatically improve this
  - Second: In a purely algorithmic sense, prolly trees are the definition of scalable. They are log(n) (with a large base) for inserts, deletes, and seeks and they have efficient ordered scans. They have basically the same algorithmic complexity as B Trees, B+ Trees, LSM trees, etc -- very similar properties to the data structures used by other databases. 
  - The problem with prolly trees is actually the reverse: they are scalable, but have large constant factors due to the overhead of hashing.
  - But a single-digit constant factor slower performance than MySQL but with versioning seems like a great product for many applications.

- Doesn’t Datomic do all this for some years now?
  - Lots of databases offer time travel / historical querying, including datomic, MySQL, Postgres, etc (plugins required in some cases).
  - Dolt's unique functionality isn't time travel, although it has that. It's version control, i.e. branch and merge, push and pull, fork and clone.
- I think TerminusDB does that as well.
  - Yup, TerminusDB has a very similar set of capabilities, just for a graph DB instead of SQL / relational. Very cool product if you're in the market for a graph DB.
- QLDB seems like something that goes in this direction. What's your opinion of it ?
  - QLDB isn't version controlled, it's an immutable ledger database.
  - Ledgers are simplified, centralized versions of blockchains: blockchains without consensus.
- Basically my research project sirixdb I'm working on in my spare time is all about versioning and efficiently storing small sized revisions of the data as well as allowing sophisticated time travel queries for audits and analysis.
  - Of course all secondary user-defined, typed indexes are also versioned.
  - Basically the technical idea is to map a huge tree of index tries (with revisions as indexed leave pages at the top-level and a document index as well as secondary indexes on the second level) to an append-only file. To reduce write amplification and to reduce the size of each snapshot data pages are first compressed and second versioned through a sliding snapshot algorithm. Thus, Sirix does not simply do a copy on write per page. Instead it writes nodes, which have been changed in the current revision plus nodes which fall out of the sliding window (therefore it needs a fast random-read drive).
- That sounds somewhat similar to Dolt's storage index structure: Prolly Trees

- DVC is great for tracking locally-stored data and artifacts generated in the course of a research project, and for sharing those artifacts across a team of collaborators (and/or future users).
  - However DVC is fundamentally limited because you can only have dependencies and outputs that are files on the filesystem.
  - Theoretically they could start supporting pluggable non-file-but-file-like artifacts, but for now it's just a feature request and I don't know if it's on their roadmap at all.
  - it kind of sucks for when your data is "big"-ish and you can't or don't want to keep it on your local machine, e.g. generating intermediate datasets that live in some kind of "scratch" workspace within your data lake/warehouse
  - The universal solution is something like Airflow, but it's way too verbose for use during a research project, and running it is way too complicated. It's an industrial-strength data engineering tool, not a research workflow-and-artifact-tracking tool.
- I have dvc pipelines such that input/output is iceberg snapshot files. The data gets medium-big and it works well.
- I'm looking into DVC right now, and I feel like the code history (in git) and the data history are too intertwined. If you move the git HEAD back, then you get the old data back, but you also get the old code back. I wish there was a way to move the two "heads" independently. Or is there?
  - If you want the dataset to be independent, I would recommend having a seperate repository for the dataset, and using Git Submodules to pull it in. That way you can checkout different versions of the dataset and code because they are essentially in seperate working trees.

- I've (partially / POC) implemented time travel in a SQLite database; the TL; DR is that whenever you create a table, you add a second, identical or nearly-identical table with a `_history` suffix; the history table has a valid from and valid to. Then you add a trigger on the primary table that, on update or on delete, makes a copy of the old values into the history table, setting the 'valid_to' column to the current timestamp.
  - The reason I used a separate table is so that you don't have to compromise or complicate the primary table's constraints, indices and foreign keys; the history table doesn't really need those because it's not responsible for data integrity.

- We use DataVault for that. And perhaps Databricks at some point in the future

- I have been interested in this space, but have failed to understand how these versioning solutions for data work in the context of environments.
  - There are aspects of time travel that line up better e.g. with data modelling approaches (such as bitemporal DBs, xtdb etc.) others more with git-like use cases (e.g. schema evolution, backfilling) some combinations. The challenge is, with data I don’t see how you’d like to have all environments in same place/repo and there may be additional considerations coupled with directionality of moves, such as anonymisation for moving from prod to non-prod , back filling for moving from non-prod to prod etc

- It's not like there is a standard definition for "merge operation" on data. Even Git tries to do more than line-level changes, taking context into account, and turning one line change into two line changes if merging across a file copy for example.
  - Dolt markets itself as "a version controlled SQL database", so I think it is perfectly reasonable to consider the standard that already exists for concurrent changes to a SQL database, and that's transaction isolation.
- You're thinking too small. The transaction is generally not the unit you want to apply version control to, databases already have robust concurrency support at that level.
  - What you want is to have branches on your data that have many transactions applied to them, for days or weeks. Then you merge the branch back to main when it's ready to ship.

- If you're a data cleaning guy, you might be interested in our data bounties program. It's collaborative data importing / cleaning

- XTDB is a general-purpose bitemporal database with graph query capabilities
  - The talk expands on what "bitemporal" means in this context, namely, separate "valid" and "audit" time dimensions.

- Git-like functionality on top of existing RDBMS solutions would significantly reduce the overhead of managing ephemeral test environments for us. It would be awesome to see Dolt as a thin layer on top of MSSQL or Postgres that would allow my team to easily test changes before deploying to prod.
  - Today, this means creating a snapshot of the DB, creating a new DB instance, copying the data over, doing a deploy, testing changes, teardown and cleanup. Branching with copy-on-write (very similar to what neon.tech offers) on top of on-prem instances would be lifechanging for teams operating in legacy dbs.
- We might have what you're looking for with sgr [0] (I'm the co-founder) which works by running SQL commands on top of a PostgreSQL instance and uses PostgreSQL audit triggers for versioning, though note it currently only works on top of a custom PostgreSQL Docker image, since it requires some extensions.

- I get "git for data" by putting iceberg snapshot files _in_ git. That's it. It's literally git for data.
- Dolt is git for databases.
- Nessie is git for data.

- It's quite similar to https://qri.io functionality, but unfortunately Qri stopped providing their Cloud service

- I’ve been looking for something like this where you can bring your own DB. The ability to version schema and metadata is much more interesting over a saas DB host.

- This looks super handy, probably worth the performance penalty in most cases to make every command undo-able (except drop database).
  - We're trying to close the performance gap. 
  - We're even slower on heavy transactional use cases.

- Only MySQL-compatible, apparently?
  - You only connect with a MySQL-client. There is no MySQL code in it.
  - We will eventually build a Postgres Foreign Data Wrapper.

- 
- 
- 

- It's a pipedream(白日梦，空想), not the future.
  - Your database is either too big / has too much throughput or migrations just don't matter. 
  - And it's not like you wouldn't need migrations with a versioned schema, as otherwise a rollback would mean data loss.
- You're suffering from a failure of imagination.
  - Consider a CMS, one of the most common forms of database backed applications. What if you could give your customer a "dev" branch of all their data to make their changes on and test out new content, that you could then merge with back to prod after somebody reviews it in a standard PR workflow?
  - This is the workflow one of our earliest customers built.
- Personally working with timeseries data my experience is that clients typically underestimate how much storage they need for a single state, let alone including historic versions. The decision people want more data, not more snapshots for a given storage spend. But that's timeseries.

- do we keep improving change over time functionality in databases, or make VCS backends with more formal database-like behavior?
  - IIRC, Trac stores its wiki history in a subversion repository. Since it already had to understand commit histories and show diffs, that was a sensible choice. Of course it is easier to live with such a decision if the API is good, but I haven't heard anyone say that about any version control system yet.
- Version control of source code, packaged applications, container images, databases are all quite different.
  - Git is a distributed file manager that operates on files where every change is a commit, and a commit is a set of operations on files, and/or a change to a block of text strings terminated by newlines. Versions are merkle trees of commits.
  - RPM/Deb/etc is a semi-centralized file manager that operates on files assuming each change is a collection of files with executable stages before and after copying/linking/unlinking. Versions are arbitrary key=value pairs which optionally depend on other versions, with extra logic to resolve relative versions.
  - Docker/OCI is a distributed file manager that operates on layers assuming every layer is a collection of files overlaid on other layers, with extra logic to do extra things with the layers at runtime. Versions are (I think?) merkle trees of layers.
  - The database is going to need a helluva lot of custom heuristics and operations to do version-control, because how you use it is so much different than the above. Databases are much more complex beasts, require higher performance, higher reliability, tons more functionality.

- I think the problem is that the tradeoffs already exist. Most users would prefer more usable space or less money to a full history of their data.

- Would love to know the size of the team that built this
  - 12 Software Engineers

- 
- 
- 

- ## "the only database with branches" because didn't we all want to resolve some merge conflicts in our datastore as well 
- https://twitter.com/xeraa/status/1245346877509382145
  - on a more serious note: didn't CouchDB do something similar 10+ years ago (just without calling it git)?

- Couch doesn’t have branches. Nodes are allowed to diverge but as soon as they come into contact they must immediately reconcile. There’s no concept of long lived forks.
- it's been a really long time, but couldn't you build something similar with the _changes API aka filtered replication (with a little plumbing around)?
  - Don't see how. I mean you can build anything with anything if you put your mind to it, but it's clearly not a built-in feature.

- ## is it possible to access data of dolthub repos with some sort of REST or GraphQL API?
- https://twitter.com/DoltHub/status/1253724553106165762
- It's on the roadmap :-) 
  - **We think of APIs as "releases" on top of specific database versions**. 
  - We would love to host those APIs on DoltHub. 
  - Right now, you have to clone the data locally, run `dolt sql-server` , and then connect to the database as you would any MySQL db.
- 
- 
- 

- ## [Dolt performance comparison to postgres and mysql](https://github.com/dolthub/dolt/issues/6536)
- I suspect there might be two actual issues at play: one causing our client to behave slowly, and another slowing down the actual execution of the query. (Hence why connecting with a mysql client is approximately as fast as running the query locally.)

- ## [Document Version Control · frappe-erp](https://github.com/frappe/frappe/issues/22075)

# discuss-noms
- ## 

- ## [Noms – A new decentralized database based on ideas from Git | Hacker News_201608](https://news.ycombinator.com/item?id=12211754)
- this reminds me a little bit of datomic - all data history is preserved/deduplicated, fork/decentralization features. Can you comment on how it compares?
  - I feel weird speaking for them, but at a product level, I think it's fair to characterize Datomic as an application database -- competing with things like mongo, mysql, rethink, etc.
  - While Noms might be a good fit for certain kinds of application databases (cases where history, or sync, is really important) we're really more focused more on archival, version control, and moving data between systems than being an online transactional database.
  - Also, at a technical level, unless I'm wildly mistaken, I don't believe that Datomic is content-addressed, and I wouldn't call it "decentralized" (though that word is a bit squishy).

- Could you tell us a bit about how this compares to dat?
  - Dat is (currently) focused on synchronizing files in a peer-to-peer network.
  - Noms can store files, but it is much more focused on structured data. You put individual values (numbers, strings, rows, structs, etc) into noms, using a type system that noms defines, and this allows you to query, diff, and efficiently update that data.
  - Also Noms isn't peer-to-peer (although we hypothesize that it could run reasonably on top of an existing network like IPFS).
  - dat has changed so much, and there has been so much hype and tooling (probably now broken) around it, and yet it doesn't seem to be delivering anything, nor there seems to be many data willing to be published with it.

- Why would you exclusively support schema inference, rather than also allowing users to manually specify their schemas?
  - In Noms every value has a type. It's an immutable system, so this type just is. 
  - We don't try to infer a general database schema from a few instances of data. We just apply this aggregation up the tree and report the result.
  - That all said, we do want to eventually add schema _validation_, by which I mean the ability to associate a type with a dataset and have the database enforce that any value committed to the dataset is compatible with that type (following subtyping rules).
- It sounds like Noms is dynamically typed, rather like SQLite — types are associated with values, not (just) with datasets. The difference is that SQLite (like Python or JS) only types leaf/atomic data, while you're also typing aggregate data. Is that right?
  - Right - the challenge is that with dynamic typing and without schema validation, it's incredibly easy to break any strongly typed client/consuming application. You think you are dealing with a `List<Number>`, you have Go/Java/Haskell/whatever apps which are consuming that in a strongly typed fashion using their idiomatic record types, and then suddenly a user accidentally sends in a single value which turns the tree of values into a `List<Number|String>`, and all your consuming apps break.
  - Given that schema validation ("does this instance match this type?") is simpler to implement than schema inference ("what is the type of this instance?"), it's surprising to me to deliver inference first

- if you want people to be able to link to Noms datasets on the web, maybe you should switch to using URLs to name the datasets, instead of a two-part identifier with an URL separated from a dataset name by a "::"? Darcs and Git seem to get by more or less with URLs and relative URLs; do you think that cold work for Noms too?
  - The super REST harmonious way to do this would be to define a new media-type for Noms databases with a smallish document that links to the component parts. Like torrent files, but using URLs (maybe relative URLs) instead of SHA1 hashes for the components, maybe?
- We never thought of these strings as URLs, but there are places where it would be nice to use them that only want URLs (the href attribute, for example).
- The hash portion of a URL is not transmitted to the server by browsers, so it wouldn't help in the case of putting the string into a URL bar or a hyperlink.

- Is it possible that their target market is not current users of decentralized DBs?
  - At first glance, it strikes me as a solution for people storing something like scientific data sets rather than application data. In which case, posting CSV files on a website is pretty much best-case scenario. Although, in the "scientific data set" scenario, I'm not sure how much value there would be in storing version history.
  - Right, this looks like it has far more immediate value for storing data which will be collaboratively mutated, so: a company directory, a knowledgebase, a CRM datastore... For large scale datasets, I'd be looking at GIS data maybe.

- ## 💡 We are using Noms heavily inside @replicache and it's overall pretty good._20200401
- https://twitter.com/pvh/status/1245202163384500224
  - There are some *really* sharp API edges, but it's a powerful tool.
- Are there any good articles comparing/contrasting Noms and Dat?
  - Not that I know of, but they are pretty wildly different at this point. 
  - Noms doesn't include any networking component at all -- if you can find some way to get two Noms nodes to talk to each other they can sync, but how they do that is out of scope for Noms itself.
  - And dat doesn't expose any sort of structured data model at all - it's about syncing files around p2p and forking/branching them.
- True, I guess I'm thinking of how automerge/hypermerge used dat. I'm guessing @pvh might be able to weigh in
  - Dat is replicated append-only logs. 
  - Noms is a database designed for rsyncing. 
  - They're... neighbors in the p2p ghetto but they don't share a wall.
- Still no article that I'm aware of, they aren't really trying to do the same thing. 
  - There are so many differences, but maybe the simplest way to think of the difference is the problem the three set out to solve:
  - Automerge: I have this JSON document. I wish that multiple parties could be editing it disconnected and the edits would always merge correctly.
  - Hypermerge: Same as Automerge, 'cept I want to do it over P2P. 
  - Noms: I wish there was something like SQLite, but where I could see the history of changes and push/pull them to and from servers.
  - Or stated another way: Noms is a much lower level piece of machinery: it doesn't guarantee convergence by itself, you'd have to put something on top that does. **Noms is also focused a lot more on being a database** (larger data, better performance, indexes, etc).

- noms is a git-like database, implementing B+Trees (maps, sets, secondary indexes, lists, blobs) with chunks, split at boundaries chosen by rolling hash function to deduplicate. 
# discuss-branching
- ## 

- ## [LiteTree: SQLite with Branches | Hacker News](https://news.ycombinator.com/item?id=17865687)
- Fossil is a SCM system (like git) created by the very same author of SQLite (D. Richard Hipp). 
  - It uses SQLite as its database and implements versioning and branching and even merging (which LiteTree doesn't do) on its own, by recording the changes on each item on a separate table.
  - This approach is more complex to implement but a lot more versatile and flexible. Most of times you wouldn't want to version or branch the whole database, but only parts of it.

- 
- 
- 
- 
- 

- ## [How does irmin compare to camlistore?](https://news.ycombinator.com/item?id=8054721)
- They are different design philosophies: Irmin is closer to "Sqlite-with-Git-instead-of-SQL", since it's just an OCaml library that lets you build graph-based datastructures that are persisted into memory or Git. Higher-level datastructures are built in the usual OCaml style on top of it.
- You could build a Camlistore-like service on top of Irmin, but this design/eval hasn't happened yet to my knowledge. It's on the TODO list for Irmin applications -- while I really like Camlistore, I do also want finer control over routing of blobs in a content-addressed network to manage the physical placement of my personal data.
- Another interesting aspect of Irmin is that the backend blob stores are also just another functor. In addition to the existing memory/HTTP-REST/Git backends, we've sketched out the design for a convergent-encrypted backend store as well. Other backends such as existing k/v stores like LevelDB or Arakoon shouldn't be difficult, and patches are welcome.

# discuss-fossil
- ## 

- ## 

- ## 
# discuss-terminusdb
- ## 

- ## it seems to be the only db to do what I want, which is immutable graph DB, with branching, AND query!
- https://discord.com/channels/689805612053168129/722568409211994194/951039054722510868
  - Was looking into Fluree before, but no branching

- ## [TerminusDB – An open source in-memory graph database | Hacker News_202004](https://news.ycombinator.com/item?id=22867767)
- TerminusDB is an open source (GPLv3) full featured in-memory graph database management system with a rich query language: WOQL (the Web Object Query Language).
- the linked-data and RDF tool-chains were severely lacking. We evaluated several tools in an attempt to architect a solution, including Virtuoso and the most mature technology StarDog, but found the tools were not really up to the task.
- the HDT library exhibited a number of problems. 
  - First it was not really designed to allow programmatic access which was required during transactions and so we found it quite awkward. 
  - Second, we had a lot of problems with re-entrance leading to segfaults. This was a serious problem on the Polish commercial use case which needed multi-threading to make search and update feasible. Managing all of the layering information in prolog was obviously less than ideal - this should clearly be built into the solution at the low level. We either had to fix HDT and extend it. Or build something else.
- To take advantage of this DataOps/’Git for data’ use case we implement a graph database with a strong schema so as to retain both simplicity and generality of design. Second, we implement this graph using succinct immutable data structures. 

- I am curious why a new query language WOQL was designed and implemented instead of just using SPARQL. It seems like it would be not too difficult to write a converter between WOQL and SPARQL.
- We debated using SPARQL initially, and even had a test implementation leveraging the version shipped with SWI-prolog. However we found SPARQL to have a number of short comings that we wanted to see addressed.
  - Firstly, there were features. Tighter integration with OWL and schema-awareness was something we wanted to build in at a low level. We also wanted to leverage CLP(fd) for time and other range queries. If we were going to need to fundamentally alter the semantics anyhow, it didn't seem that important to start with SPARQL. Other features that are coming down the pipes very soon are access to recursive queries and manipulation of paths through the graph.
  - Secondly, we wanted better composability. One of the real strengths of SQL as a language is that it is very easy to compose language elements. By contrast SPARQL feels quite ad-hoc, mimicing some of the style of SQL but losing this feature.
  - Lastly, we wanted to have a language which would be easy to compose from Javascript, or python. Javascript, because we live in a web age, and python, because it's the choice for many datascientists. JSON-LD provides a nice intermediate language in which to write queries in either of these languages. No need to paste together strings! And then, because of the choice of JSON-LD, we can naturally store our queries in the graph (and even query our queries).

- ## [Git for Data – A TerminusDB Technical Paper | Hacker News_202001](https://news.ycombinator.com/item?id=22045801)
- TerminusDB is the graph cousins of Dolt. Great to see so much energy in the version control database world!
  - We are currently focused on data mesh use cases. 
  - Rather than trying to be GitHub for Data, we're trying to be YOUR GitHub for Data. 
  - Get all that good git lineage, pull, push, clone etc. and have data producers in your org own their data.
  - We see lots of organizations with big 'shadow data' problems and data being centrally managed rather than curated by domain experts.

- ## With there only being a handful of temporal, datalog based databases out there, what sets TerminusDB apart from XTDB, and when would one choose one over the other?
- https://discord.com/channels/689805612053168129/689892819678134354/1133508959341395969
- TerminusDB works with RDF while XTDB data-model is bespoke(定制的), 
  - and while I'm not the biggest fan of RDF, I found data-export generally unpleasant in Datomic family databases. (you can kinda export to EDN, but it's not data-exchange first like RDF is)
- XTDB has SQL with extra stuff and Datomic/EDN query notation, TerminusDB has GraphQL queries as well as its own query language called WOQL, depending on your background/environment you might gravitate towards one or the other
- In XTDB transactions are appended in some immutable log e.g. single partition Kafka topic, which makes it behave like a plain old database. 
  - TerminusDB is more like git, where commits are first class citizens, can be rebased, merged, forked, exported e.t.c.
- They seem to have different approaches to bitemporality. 
  - In a temporal database, bitemporal data is both the valid time and transaction time of the data.
  - XTDB is using two timestamp ranges per triple, with transactions manifested in one of the timestamps. 
  - In TerminusDB bitemporality is achieved via it's commits, but it doesn't give every triple a "valid-time" range like TXDB does.

- TerminusDB makes heavy use of succinct(简洁的) datastructures and will probably have lower memory footprint than in-memory XTDB, 
  - but otoh graph processing is limited to in-memory processing (which is fine imho, most databases become unusable once their indexes no longer fit into memory even with disk storage, and the succinct datastructures mean that you can fit a lot of data in memory), 
  - TXDB has a wide array of index, document and log backend (in-memory and on-disk) at the cost of more memory usage.

- ## Having a Javascript client running in browser, where does the client side TerminusDB store data?
- https://discord.com/channels/689805612053168129/689892819678134354/1130494867575943188
  - is there any limitation that would prevent it's use in an offline mobile application?
- **client side really only connects to a server, it has no local data**. 
  - but you could maybe ship your app with an instance of terminusdb in which case it'd store on that localhost terminusdb. 
  - Then whenever you have internet access again, you can make that local terminusdb push/pull to syncrhonize with some server if you like.
  - That said I don't think we've had anyone develop a proper app with terminusdb and i'm not sure how viable it is to have the server running on a phone. 
  - We know we can build on ARM (as long as it is 64 bit) so that shouldn't be the issue. The issue is more going to be in packaging it all

- ## 💡 I've been looking for a graph database that might have the possibility of being used in an offline-first mobile application written in Rust and run through Tauri
- https://discord.com/channels/689805612053168129/689892819678134354/1130415411792453744
  - I came across the Terminus-Store Github repo, which is the new Terminus datastore layer and is compatible with Rust and offers a "triple store".
  - Would using the Terminus-Store package still give you the same querying power (especially that Datalog syntax) as the regular Terminus DB clients ?
- 👉🏻 **store will not give you the same querying power**. 
  - The only thing it can do is iterate over all triples, or look up by a few predefined patterns (by subject, by subject-predicate, by object, or by predicate).
  - All the actual dataloggy stuff, as well as all the document extraction logic, is in terminusdb proper 
- we have been pushing more and more things down into rust though_20230717, and it's not unimaginable that at some point, we will have a standalone rust version for at least a significant portion of the server. 
  - But at this point that's a dream for the future, and nowhere near completion
- interesting to see that a lot of Terminus is written in Prolog. What areas do you feel Prolog is the best fit vs Rust / when do you choose one tool over the other?
- prolog is pretty good for search algorithms so it's a pretty natural fit for writing a query language
- so we use rust to produce iterators over triples for us, then drive their iteration from prolog in creative ways
  - but rust is much better when it comes down to actually storing things, doing bit-level operations, synchronizing access, etc
  - much faster too
  - we also tend to push things down into rust once we understand an area well and the interface to it has stabilized, but we want it to go faster. In that case it's worth spending the extra effort to get a bit more power
