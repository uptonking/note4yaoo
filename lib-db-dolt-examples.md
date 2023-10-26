---
title: lib-db-dolt-examples
tags: [dolt, examples]
created: 2023-08-25T22:30:55.259Z
modified: 2023-08-25T22:31:05.132Z
---

# lib-db-dolt-examples

# guide

- branch和versioning的参考方案
  - 同类产品，如git
  - 编辑器，如vscode、ckeditor、ospreadsheet
  - 数据库，如dolt、mongodb-doc-ver
  - version/revision history可以在orm层实现，不必执着于数据库内置
  - branch的粒度在table-row，而不是全库-文件
# popular
- https://github.com/mikolalysenko/version-tree /201404/js/inactive
  - A data structure for maintaining a tree of versions. 
  - This can be useful when implementing fully persistent data structures using the DTSS method. 
  - Works in both node.js and browserify. 
  - All operations use amortized O(1) space and time.

- https://github.com/dstanesc/HexFluidTree /ts
  - Experimental FluidFramework tree distributed data structure (DDS) featuring SCM (Git) like versioning and branching
  - [Tree DDS Design Notes](https://github.com/dstanesc/HexFluidTree/blob/master/docs/design-notes.md)

- https://github.com/justinsheehy/vertree /201707/rust/inactive
  - a library providing the "vertree" data structure. 
  - hierarchical storage (a tree) of data
    - The hierarchical structure of vertree is similar to a traditional filesystem. 
    - Each inner (non-leaf) node is a "Directory" node, a mapping of UTF-8 strings to child nodes of that Directory. 
    - Each leaf node has a specific data type such as Blob, Queue, or Set
    - The sub-items inside Queue and Set nodes are always Blob, so a leaf node itself is not arbitrarily complex in content.
  - rich data structures at the leaves (not just blobs)
  - linear versioning of all changes to items and subtrees
    - One of the essential features of vertree is that every node has a version.
    - All mutation operations on either a leaf node's content or on the vertree itself cause the version to be incremented both at the node where the change occurred and at every node above it
  - CAS and related operations

- https://github.com/mikeal/prolly-trees /js
  - Implementation of peer-to-peer search trees (probabalistic b-trees trees) as used in dolt and noms.
  - It does not have an opinion about how blocks are encoded and hashed.

- https://github.com/fireproof-storage/fireproof /MIT/ts
  - https://use-fireproof.com/
  - Live database for the web
  - Simplify your application state with a live database. Automatically update your UI based on local or remote changes, and optionally integrate with any cloud for replication and sharing.
  - Fireproof is an embedded JavaScript document database designed to streamline app development. 
  - Data resides locally, with optional encrypted cloud storage and realtime collaboration.
  - 依赖 @ipld/dag-json|car|unixfs、@web3-storage/clock、idb、prolly-trees
  - JSON Documents - Encrypted changes are persisted locally and to any connected storage.
  - File Attachments - Share social media or manage uploads within Fireproof's file attachment API.
  - Live Query - Sort and filter any database with CouchDB-style map functions.
  - Realtime Updates - Subscribe to query changes in your application
  - Cryptographic Proofs - Fireproof's Merkle clocks and hash trees are immutable and self-validating
  - Fireproof has a unique take on distributed data integrity, rooted in immutable data and cryptographically verifiable protocols. 
  - The core Merkle hash-tree clock is based on Alan's Pail
  - Mikeal wrote the prolly trees implementation.

- https://github.com/versionpress/versionpress /php/ts/inactive
  - https://versionpress.com/
  - a user-friendly versioning solution for WordPress powered by Git

- https://github.com/bokusunny/Elaborate /ISC/201911/ts/inactive
  - A hosting, version controlling service for documents.
  - created by diverting the idea of Git into document development. It enables to host their documents centralizedly and to control their versions.
  - 依赖Firebase、material-ui.v3、draft-js、formik、react-redux
- https://github.com/azuzunaga/reminisce /201805/js/inactive
  - a "GitHub for Writers" built using the MERN stack -- Express, MongoDB, and React/Redux.
  - We enabled writers to execute complex version control actions by recreating the committing and branching workflows natively and simplifying processes by removing the use of terminal and using custom React modals in its place. 
    - We used **Myers' diff** algorithm to identify the text differences between commits and branches.
# data-branching-versioning/revisions
- https://github.com/snowtrack/snowfs /GPLv3/ts/inactive
  - https://www.snowtrack.io/
  - SnowFS is a high-performance command-line application and node library for Windows, macOS and Linux with a focus on **binary file versioning**. 
  - It is made for the graphics industry and was initially developed for Snowtrack.
  - Support for instant snapshots
  - Support for instant rollback
  - Supports Branches
  - Super-fast-detection of modifications in large binaries
  - Block-cloning and Copy-on-Write support for APFS, ReFS and Btrfs
  - Support for removing single versions and/or binaries
  - Primarily I/O bound through libuv
  - SnowFS works on plain filesystems like FAT, NTFS, HFS+ and has extended support for APFS, ReFS and Btrfs.
  - Why not Git/Git-LFS, libgit2, or SVN?
    - due to their focus on the software development lifecycle they are not suitable to version binaries or graphic files. 

- https://github.com/dominictarr/snob /201207/js/inactive
  - Snob is a Distributed Version Control System implemented is js. 
  - You can think of it as a Model layer for realtime collaborative applications, or as a peer to peer database.
  - Each node has a Repo object, and they replicate by sending change sets to each other.
  - Snob has the same architecture as git, but with plugable diff-tools. 
    - That means, it can support any kind of objects, if you can diff, diff3, and patch them.
    - by default, snob uses xdiff

- https://github.com/Berylsoft/LesserBase /rust/inactive
  - A version control system based on file system and document database, designed as content management system for wikis and knowledge bases.

- https://github.com/neondatabase/neon /rust
  - https://neon.tech/
  - Neon is a serverless open-source alternative to AWS Aurora Postgres. 
  - It separates storage and compute and substitutes the PostgreSQL storage layer by redistributing data across a cluster of nodes.
  - A Neon installation consists of compute nodes and the Neon storage engine. Compute nodes are stateless PostgreSQL nodes backed by the Neon storage engine.
  - Compute is fully client-compatible with Postgres because a Neon compute is Postgres.
  - Neon allows you to instantly branch your Postgres database to support modern development workflows. 
    - You can create branches for test environments and for every deployment in your CI/CD pipeline.
    - Branches are created using the "copy on write" technique, making them virtually free.

- https://github.com/attic-labs/noms /apache2/go/archived
  - The versioned, forkable, syncable database
  - Dolt is a fork of this project and actively maintained.
  - forks
    - https://github.com/ndau/noms
  - [Question: What is a Prolly Tree?](https://github.com/attic-labs/noms/issues/3849)
    - Prolly trees are very different than tries. 
    - While tries have a history-independent structure, they do not have the performance /noms of b-trees.
    - b-trees guarantee a min/max fanout, independent of the data you put in. 
    - Prolly trees guarantee an *average* fanout, independent of the data you put in.
  - [Remove noms JS implementation](https://github.com/attic-labs/noms/issues/3120)
    - JS isn't a great place to be implementing a full noms client.
  - [Some notes and questions on Prolly Trees](https://github.com/attic-labs/noms/issues/3878)
    - Noms only exposes data structures like maps, sets and lists. It doesn't have a notion of a table. Maybe you are thinking of Dolt?
  - [Noms — The Decentralized Database](https://github.com/attic-labs/noms/blob/master/doc/decent/about.md)
    - Like most databases, Noms features a rich data model, atomic transactions, support for large-scale data, and efficient searches, scans, reads, and updates.
    - Unlike any other database, Noms has built-in multiparty sync and conflict resolution. This feature makes Noms a very good fit for P2P decentralized applications.

- https://github.com/dolthub/dolt /apache2/go/170k-loc
  - https://docs.dolthub.com/introduction/what-is-dolt
  - Dolt – Git for Data
  - Dolt is a SQL database that you can fork, clone, branch, merge, push and pull just like a Git repository.
  - Git versions files. Dolt versions tables. It's like Git and MySQL had a baby.
  - Dolt implements the Git command line and associated operations on table rows instead of files.
  - Dolt ships with a MySQL compatible database server and client built in. Dolt supports any MySQL-compatible client 
    - Dolt can be set up as a replica of your existing MySQL or MariaDB database using standard MySQL binlog replication. 
    - Every write becomes a Dolt commit. 
  - Dolt commands map exactly to their Git equivalent with the targets being tables instead of files. 
    - In SQL, Dolt exposes version control read operations as system tables and version control write operations as stored procedures.
  - Dolt produces cell-wise diffs and merges, making data debugging between versions tractable. 
  - That makes Dolt the only SQL database on the market that has branches and merges.
  - https://github.com/dolthub/go-mysql-server /go
    - go-mysql-server is a drop-in replacement for MySQL. Any client library, tool, query, SQL syntax, SQL function, etc. that works with MySQL should also work with go-mysql-server.
    - A simple in-memory database implementation is included, and you can query any data source you want by implementing your own backend.

- https://github.com/terminusdb/terminusdb-store /341Star/apache2/202309/rust
  - a tokio-enabled data store for triple data
  - This library implements a way to store triple data - data that consists of a subject, predicate and an object, where object can either be some value, or a node
  - This library is intended as a common base for anyone who wishes to build a database containing triple data.
  - This library is tokio-enabled. Any i/o and locking happens through futures, and as a result, many of the functions in this library return futures. 
  - The HDT format, which the terminusdb-store layer format is based on
  - We are constantly developing terminusdb-store to make it a high quality succinct(简洁的) graph representation versioned datastorage layer. 
  - Starting with version 0.20.0, terminus-store uses a new storage format, which bundles all files into a single archive, and also supports value types. 

- https://github.com/terminusdb/terminusdb /prolog语言
  - https://terminusdb.com/
  - TerminusDB is a distributed database with a collaboration model
  - Revision Control: commits for every update
  - Diff: differences between commits can be interpreted as patches between states
  - Push/Pull/Clone: communicate diffs between nodes using push / pull / clone
  - TerminusDB allows you to link JSON documents in a knowledge graph through a document API.
  - TerminusDB is available as a standalone server, or you can use our headless content and knowledge management system TerminusCMS.
  - TerminusDB is a "git graph database". 
    - TerminusDB has full schema and data versioning capability. 
    - but offers a graph database interface using a custom query language called Web Object Query Language (WOQL). WOQL is schema optional. 
    - TerminusDB just released the option to query JSON directly, similar to MongoDB, giving users a more document database style interface.
  - [Recently minted database technologies that I find intriguing | Hacker News](https://news.ycombinator.com/item?id=23531825)
    - We are focused on the revision control aspects of Terminus - trying to make the lives of data intensive (ML etc.) teams a little easier. 
    - We use a delta encoding approach to updates like source control systems such as git and provide the whole suite of revision control features: branch, merge, squash, rollback, blame, and time-travel. Idea is to provide continuous integration for the data layer. 
    - Basically squash(压扁，挤碎) all the tools and processes mentioned here into a versioned graph

- https://github.com/perkeep/perkeep /apache2/go
  - https://perkeep.org/
  - a set of open source formats, protocols, and software for modeling, storing, searching, sharing and synchronizing data in the post-PC era. 
  - Data may be files or objects, tweets or 5TB videos, and you can access it via a phone, browser or FUSE filesystem.
  - [Perkeep – Open-source data modeling, storing, search, sharing and synchronizing | Hacker News_201712](https://news.ycombinator.com/item?id=15928685)

- https://github.com/treeverse/lakeFS /go
  - https://docs.lakefs.io/
  - open-source tool that transforms your object storage into a Git-like repository.
  - lakeFS provides version control over the data lake, and uses Git-like semantics to create and access those versions. 
  - It minimizes data duplication via a copy-on-write mechanism.
  - lakeFS supports managing data in AWS S3, Azure Blob Storage, Google Cloud Storage (GCS) and any other object storage with an S3 interface. 
  - LakeFS sits in front of your cloud storage and adds data versioning to the data in your lake. 
    - Merge is supported but conflicts are detected at the file level and are "up to the user to resolve". 
    - A file in this case can be quite large, more like a dataset than a single row of data. Data is shared at the file level between commits, but a new version of the data means a new version of the file so storage can grow quite big with multiple versions.
  - [Concepts and Model](https://docs.lakefs.io/understand/model.html)
    - lakeFS blends concepts from object stores such as S3 with concepts from Git
    - The actual data itself is not stored inside lakeFS directly but in an underlying object store. lakeFS manages pointers and additional metadata about these objects.
    - The underlying storage is a location in an object store where lakeFS keeps your objects and some immutable metadata.
    - In lakeFS, a repository is a set of related objects (or collections of objects).

- https://github.com/aergoio/litetree /202003/c/inactive
  - It is a modification of the SQLite engine to support branching, like git!
  - Each database transaction is saved as a commit, and each commit has an incremental number
  - We cannot write to the database when we are in a defined commit, writing is only possible at the head of each branch. If you want to make modifications to some previous commit you must create a new branch that starts at that commit.

- https://github.com/postgres-ai/database-lab-engine /go
  - Blazing-fast Postgres cloning and branching
  - Provide temporary full-size database clones for SQL query analysis and optimization
  - Available for any PostgreSQL, including self-managed and managed* like AWS RDS, GCP CloudSQL, Supabase, Timescale.
  - **Thin cloning is fast because it is based on Copy-on-Write(CoW)**. 
    - DBLab employs two technologies for enabling thin cloning: ZFS (default) and LVM.
    - Using ZFS, DBLab routinely takes new snapshots of the data directory, managing a collection of them and removing old or unused ones. When requesting a fresh clone, users have the option to select their preferred snapshot.
  - [How Database Lab Works | Database branching for any Postgres DB](https://postgres.ai/products/how-it-works)

- https://github.com/sirixdb/sirix /BSD/java
  - https://sirix.io/docs/index.html
  - an embeddable, temporal, evolutionary database system, which uses an append-only approach to store immutable revisions. 
  - a log-structured, temporal JSON and XML database system, which stores evolutionary data. It never overwrites any data on disk.
  - stores a revision history of every resource in the database without imposing extra overhead. It uses a huge persistent, durable page tree for indexing revisions and data.
  - It keeps the full history of each resource. 
  - Every commit stores a space-efficient snapshot through structural sharing.
  - It is log-structured and never overwrites data. 
    - Similarly to the file systems Btrfs and ZFS, SirixDB uses CoW semantics, meaning that SirixDB never overwrites data. Instead, database-page fragments are copied/written to a new location. 
    - SirixDB does not simply copy whole pages. Instead, it only copies changed records plus records, which fall out of a sliding window.
  - uses a novel page-level versioning approach.
  - appends data to an indexed log file without the need of a WAL
  - One file stores the data with all revisions and possibly secondary indexes. 
    - A second file stores offsets into the file to quickly search for a revision by a given timestamp using an in-memory binary search.
  - [Why And How We Built a Temporal Database System Called SirixDB From Scratch | HackerNoon_201812](https://hackernoon.com/why-and-how-we-built-a-temporal-database-system-called-sirixdb-open-source-from-scratch-a7446f56f201?source=rss----3a8144eabfe3---4)
  - [Building A Time-Traveling Contacts App with SirixDB - DEV Community](https://dev.to/sirixdb/building-a-time-traveling-contacts-app-with-sirixdb-2amo)
  - It currently supports the storage and (time travel) querying of XML and JSON data in its binary encoding, tailored to support versioning. 
    - The index structures and the whole storage engine has been written from scratch to support versioning natively. 
    - We might also implement storing and querying other data formats as relational data.
  - uses a huge persistent (in the functional sense) tree of tries, wherein the committed snapshots share unchanged pages and even common records in changed pages
    - The system only stores page fragments during a copy-on-write out-of-place operation instead of full pages during a commit to reduce write-amplification
    - During read operations, the system reads the page fragments in parallel to reconstruct an in-memory page 
  - not only supports snapshot-based versioning on a record granular level through a novel versioning algorithm called sliding snapshot, but also time travel queries, efficient diffing between revisions, and storing semi-structured data.
  - [Introduce Dagger as DI framework for the project](https://github.com/sirixdb/sirix/pull/381)
  - [Implementation of a form of Adaptive Radix Trie for secondary index structures](https://github.com/sirixdb/sirix/issues/306)
    - Reducing storage space of the "compound nodes" can be done as in ART and Hash Array Mapped Tries (like we also do in our simple trie for dense ascending IDs).
  - in SirixDB to use a persistent data structure and a sliding snapshot data page versioning algorithm
  - uses a novel page versioning algorithm and stores binary JSON and XML resources in a huge persistent (persistent data structure) and durable index-tree, sequentially written to a log-file.
  - SirixDB was forked from Treetank
  - https://github.com/sebastiangraf/treetank /201503/java/inactive
    - Secure Treebased Storage
    - Treetank stores data securely by applying different layers on the stored data. 
    - Flexible handling of flat as well as tree-based data is supported by a native encoding of the tree-structures ongoing with suitable paging supporting integrity and confidentiality to provide throughout security.

- https://github.com/pfrazee/hyper-vcr /ts
  - A p2p version-controlled repo (built on hypercore)
  - VCR is built on Hypercore's Autobase
  - This repo was created for edword, a p2p text editor.
  - I began exploring VCR as a Git/VCS model for edword because I thought it might provide the most intuitive UX for multi-user collaboration. 
  - I eventually became convinced that the commit-style approach is actually not ideal for this use-case.
    - commit semantics are less useful than I first imagined.
    - I think instead the UX of SyncThing and Dropbox, which just allow per-file conflict states to bubble up to the user, will be a better approach
  - https://github.com/atek-cloud/edword
    - A peer-to-peer text editor built on Hypercore's new multiwriter Autobase.

- https://github.com/RecallGraph/RecallGraph /apache2/202104/js/inactive
  - https://recallgraph.tech/
  - a versioned-graph data store - it retains all changes that its data (vertices and edges) have gone through to reach their current state. 
  - It supports point-in-time graph traversals, letting the user query any past state of the graph just as easily as the present.
  - It is a Foxx Microservice for ArangoDB that features VCS-like semantics in many parts of its interface
  - It is currently being developed and tested on ArangoDB v3.6

- https://github.com/koordinates/kart /python
  - https://kartproject.org/
  - Distributed version-control for geospatial and tabular data
  - Built on Git, works like Git - uses standard Git repositories and Git-like CLI commands
  - supports Microsoft SQL Server, PostgreSQL/PostGIS, MySQL and GeoPackage, with more coming soon
  - accurately synchronize datasets between systems in seconds. Kart moves and applies a minimal compressed set of changes.
  - Your repository consists of two “trees” maintained by kart. 
    - The first one is your working copy which is a GeoPackage holding the features you access & edit with your data tools. 
    - The second one is the HEAD which points to the last commit you’ve made.

- https://github.com/iterative/dvc /python
  - https://dvc.org/
  - DVC is a command line tool and VS Code Extension to help you develop reproducible machine learning projects
  - Version your data and models. Store them in your cloud storage but keep their version info in your Git repo
  - Track experiments in your local Git repo (no servers needed).
  - Compare any data, code, parameters, model, or performance plots.

- https://github.com/orpheus-db/implementation /MIT/201709/python/inactive
  - http://orpheus-db.github.io/
  - OrpheusDB is a database system with versioning capabilities.
  - OrpheusDB is a hosted system that supports relational dataset version management.
  - OrpheusDB is built using PostgreSQL and Click
  - Our current version supports advanced querying capabilities, using both the git-style version control commands, as well as SQL queries on one or more dataset versions.

- https://github.com/liquibase/liquibase /java
  - https://www.liquibase.org/
  - Liquibase helps millions of developers track, version, and deploy database schema changes. 

- https://github.com/redwood/redwood /go
  - https://docs.redwood.dev/
  - Redwood is a highly-configurable, distributed, realtime database that manages a state tree shared among many peers. 
  - Imagine something like a Redux store, but distributed across all users of an application, that offers offline editing and is resilient to poor connectivity.
  - Redwood is also an application server. Developers can store and update assets (HTML, Javascript, images) directly in the state tree.
  - Git-style version control systems
  - Redwood can act as a Git server.

- https://github.com/surrealdb/surrealdb /rust
  - A scalable, distributed, collaborative, document-graph database, for the realtime web
  - [SurrealDB Features Documentation](https://surrealdb.com/docs/introduction/features)
    - 已支持: 单击或分布式架构、multi-tenancy、schema-optional、table-events
    - 未支持: Versioned temporal tables、Table indexes、fts
  - [Feature: Database Branching](https://github.com/surrealdb/surrealdb/issues/2323)
    - Until this is supported by the database itself, I've had a good experience playing with the branching tool found in odonno/surrealdb-migrations#database-branching.
  - [Feature request: Data Versioning (Dolt/Dolthub like)](https://github.com/surrealdb/surrealdb/issues/2371)
  - https://github.com/Odonno/surrealdb-migrations
    - SurrealDB migration tool, with a user-friendly CLI and a versatile Rust library
    - [Pull, push and diff data from/to remote and other databases (Dolt/Dolthub like)](https://github.com/Odonno/surrealdb-migrations/issues/47)
    - Database Branching is currently a feature in progress. 
    - The idea is to be able to work with branches locally, for your development workflow. Or even with a production database, giving you full control over data management.
  - [SurrealDB – Document-graph database, for the realtime web | Hacker News_202208](https://news.ycombinator.com/item?id=32550543)
  - [SurrealDB: Distributed document-graph database for the realtime web | Hacker News_202209](https://news.ycombinator.com/item?id=32874597)

- https://github.com/flyway/flyway java
  - https://flywaydb.org/
  - Database Migrations Made Easy.
  - Flyway是一个简单开源数据库版本控制器（约定大于配置），主要提供migrate、clean、info、validate、baseline、repair等命令。
  - 它支持SQL（PL/SQL、T-SQL）方式和Java方式，支持命令行客户端等，还提供一系列的插件支持（Maven、Gradle、SBT、ANT等）。
  - https://github.com/domdinnes/node-flyway

- https://github.com/qri-io/qri /go/inactive
  - https://qri.io/docs/concepts/understanding-qri/what-is-qri
  - qri is a distributed platform for managing datasets. 
  - Qri is, all at the same time, a data format, a version control system, a distributed network, and an accessible cloud data repository.
  - Qri developed a new dataset format. To keep things organized, we define a dataset as a set of extensible components. For the data itself, we have the “body”. For metadata, we chose to use JSON as a key/value store in a component called “meta”. For validation rules, column types, and other critical information about what’s in the data, we made a component called “structure”.

- https://github.com/infostreams/db
  - Version control for databases: save, restore, and archive snapshots of your database from the command line

- https://github.com/presslabs/gitfs /python
  - gitfs is a FUSE file system that fully integrates with git. 
  - You can mount a remote repository's branch locally, and any subsequent changes made to the files will be automatically committed to the remote.

- https://github.com/fluree/db /agpl/Clojure
  - https://developers.flur.ee/docs/overview/about/
  - an immutable RDF graph database written in Clojure and built on W3C standards. 
  - The Fluree system natively supports JSON and JSON-LD and can leverage or enforce any RDF ontology
# utils
- https://github.com/VladislavPixel/persi-library /ts
  - Library of persistent data structures with support for change history and versioning.
  - https://github.com/VladislavPixel/library-persi /js

- https://github.com/PistonDevelopers/history_tree /rust
  - A persistent history tree for undo/redo
  - This data structure makes programming of editors easier when the editor environment is open ended, such as editors that are hosting other editors. 
  - It makes it possible to create game engines where scripted components are interdependent and basis for new editor functionality.
  - A persistent data structure is one that stores immutable data efficiently. 
    - This allows a programming pattern that does not rely on undoing and redoing by mutating a data structure. 
    - Instead, you store data in blocks that is referenced by index in the history tree.
  - This history tree stores records that points to previous version and parent. 
    - The tree is a function of these records plus a cursor. 
    - The cursor determine which records are active.

- https://github.com/Yomguithereal/baobab /js/inactive
  - JavaScript & TypeScript persistent and optionally immutable data tree with cursors.
  - It is mainly inspired by functional zippers (such as Clojure's ones) and by Om's cursors.
  - It aims at providing a centralized model holding an application's state and can be paired with React easily through mixins, higher order components, wrapper components or decorators
  - you can create cursors to easily access nested data in your tree and listen to changes concerning the part of the tree you selected.
  - Note that the tree, being a persistent data structure, will shift the references of the objects it stores in order to enable immutable comparisons between one version of the state and another
  - Baobab lets you record the successive states of any cursor so you can seamlessly implement undo/redo features.
  - https://github.com/Yomguithereal/baobab-react
    - React integration for Baobab.

- https://github.com/functional-data-structure/persistent /js
  - Persistent data structures for JavaScript
  - https://github.com/functional-data-structure/finger-tree

- https://github.com/simonlast/node-persist /js
  - easy persistent data structures in Node.js
  - Node-persist doesn't use a database. Instead, JSON documents are stored in the file system for persistence. 
  - Node-persist uses the HTML5 localStorage API, so it's easy to learn.

- https://github.com/cthulhu-bot/temporal-collections /js
  - a library implementing collections of persistent data structures.

- https://github.com/mafintosh/append-tree /js
  - Model a tree structure on top off an append-only log.
  - The data structure stores a small index for every entry in the log, meaning no external indexing is required to model the tree. Also means that you can perform fast lookups on sparsely replicated logs.

- https://github.com/marcuscuongdoan/organizationing /ts
  - https://organizationing.vercel.app/
  - A test to do an undo, redo action with no cloning, with tree-like model.

- https://github.com/sdq/history-tree /js
  - https://sdq.github.io/history-tree/
  - An interactive history tree for undo/redo/reset/revisit in javascript

- https://github.com/orium/rpds /1kStar/MPLv2/202308/rust
  - provides fully persistent data structures with structural sharing.
  - support: List, Stack, Queue, Vector, HashTrieMap/Set, RedBlackTreeMap/Set
  - All data structures in this crate can be shared between threads, but that is an opt-in ability. This is because there is a performance cost to make data structures thread safe. 
  - This crate supports no_std.
  - We support serialization through serde

- https://github.com/victorcolombo/prust /rust
  - a collection of immutable and persistent data structures, inspired by the standard libraries found in Haskell, OCaml, Closure and Okasaki's Purely Functional Data Structures book.
  - Prust's data structures are inherently thread-safe

- https://github.com/tobgu/pyrsistent /python
  - a number of persistent collections (by some referred to as functional data structures). 
  - Persistent in the sense that they are immutable.
  - All methods on a data structure that would normally mutate it instead return a new copy of the structure containing the requested updates. 

- https://github.com/ssaarela/javersion /java
  - a data versioning toolkit for Java.

- https://github.com/elves/elvish/tree/master/pkg/persistent /EPL/go
  - a Go clone of Clojure's persistent data structures.
  - The list provided here is a singly-linked list and is very trivial to implement.
  - The implementation of persistent vector and hash map and based on a series of excellent blog posts as well as the Clojure source code
# more
