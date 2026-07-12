---
title: toc-db-orm
tags: [database, lib, orm, toc]
created: 2020-10-05T16:22:46.508Z
modified: 2021-08-30T18:56:09.644Z
---

# toc-db-orm

# guide

- 支持mongodb的orm
  - typeorm, prisma, mikro-orm, typetta, dittorm

- https://dbdb.io/
  - Discover and learn about 924 database management systems
# orm
- https://github.com/edgedb/imdbench
  - A benchmark intended to compare various Python and JavaScript ORMs with realistic queries required for a hypothetical IMDB-style movie database application.
  - js: prisma、typeorm、sequelize、edgedb
  - python: django、sqlalchemy、edgedb
- https://github.com/emanuelcasco/typescript-orm-benchmark /202009/ts/inactive
  - ORM benchmarking for Node.js applications written in TypeScript

- https://github.com/JS-AK/db-orm-benchmarks /202402/ts
  - ORM benchmarking for Node.js
  - 50_000 queries in await Promise.all() 
  - 50_000 queries in await one by one in for loop

- https://github.com/drizzle-team/drizzle-northwind-benchmarks /202304/ts/inactive
  - 测试项目 sqlite3、knex、prisma、mikro
  - https://github.com/drizzle-team/drizzle-northwind-benchmarks-pg
    - Postgres benchmarks between Drizzle ORM and other popular ORM

- https://github.com/tkssharma/nodejs-db-orm-world /202203/ts
  - Node JS with different ORM like Typeorm, Knex, Prisma and Sequelize with Node JS API Development Node JS with without any ORM (MYSQL raw queries)

- https://github.com/MiroslavPetrik/edgedb-vs-knex
  - Comparison of Knex/Objection ORM & EdgeDB query builders by implementing & testing a task model with each setup

- typeorm /30.1kStar/MIT/202301/ts
  - https://github.com/typeorm/typeorm
  - http://typeorm.io/
  - TypeORM is an ORM that can run in NodeJS, Browser, Cordova, PhoneGap, Ionic, React Native, NativeScript, Expo, and Electron platforms
  - Supports MySQL, PostgreSQL, MariaDB, SQLite, MS SQL Server, Oracle, SAP Hana, sql.js.
  - Supports MongoDB NoSQL database.
  - 使用示例是装饰器风格
  - ✨ TypeORM supports both Active Record and Data Mapper patterns
  - 依赖date-fns, reflect-metadata, buffer
  - TypeORM is highly influenced by other ORMs, such as Hibernate, Doctrine and Entity Framework.

- mikro-orm /5.5kStar/MIT/202301/ts/开发者主程只有1个
  - https://github.com/mikro-orm/mikro-orm
  - https://mikro-orm.io/
  - TypeScript ORM for Node.js based on Data Mapper, Unit of Work and Identity Map patterns.
  - 依赖esprima、dataloader、acorn-loose、fs-extra、reflect-metadata、knex
  - 使用示例是装饰器风格
  - Supports MongoDB, MySQL, MariaDB, PostgreSQL and SQLite databases.
  - Heavily inspired by Doctrine and Nextras Orm. (两者都为PHP设计)
  - Unit of Work maintains a list of objects (entities) affected by a business transaction and coordinates the writing out of changes. 
  - Identity Map ensures that each object (entity) gets loaded only once by keeping every loaded object in a map. Looks up objects using the map when referring to them. 
  - [MikroORM 3: Knex.js, CLI, Schema Updates _202001](https://mikro-orm.io/blog/mikro-orm-3-released)
    - Knex.js is now used as both a query builder and a query runner for all SQL drivers. 
    - With Knex.js used as a query runner, support for connection pooling is finally available
  - [Who uses MikroORM in production?](https://github.com/mikro-orm/mikro-orm/issues/296)
    - Mikro relies on `Knex` to create and manage the connection
    - Even if I don't have much time for feature development in the future, I've always preferred fixing bugs and helping out others with issues
  - [Choosing the Right TypeScript ORM: MikroORM vs. TypeORM _202308](https://medium.com/@mybytecode/choosing-the-right-typescript-orm-mikroorm-vs-typeorm-fed5d7d9b514)
    - MikroORM excels with its simplicity and optimized performance, making it perfect for streamlined projects. 
    - In contrast, TypeORM offers a rich toolkit of features, catering to projects with diverse database requirements and complex queries.

- https://github.com/sequelize/sequelize /MIT/202402/ts/js
  - https://sequelize.org/
  - An easy-to-use multi SQL dialect ORM for Node.js
  - 不支持mongo
  - 使用示例是非装饰器风格

- https://github.com/drizzle-team/drizzle-orm /17kStar/apache2/202401/ts/代码量少
  - https://orm.drizzle.team/
  - a TypeScript ORM for SQL databases
  - 支持mysql、postgresql、sqlite，不支持mongo

- knex /18.5kStar/MIT/202401/js
  - https://github.com/knex/knex
  - http://knexjs.org/
  - A query builder for MSSQL, MySQL, PostgreSQL, SQLite3, Oracle
  - 依赖commander、tarn
  - feathers.v5抽象出schema+resolver，通过knex+mongoose支持rdbms和nosql
  - knex-based orm: mikro-orm, bookshelf, objection.js

- prisma /28.1kStar/apache2/202301/ts
  - https://github.com/prisma/prisma
  - https://www.prisma.io/
  - Modern database access (ORM alternative) for Node.js & TypeScript | PostgreSQL, MySQL, MariaDB & SQLite
  - Prisma Client: Auto-generated and type-safe query builder for Node.js & TypeScript
    - used in any Node.js or TypeScript backend application (including serverless applications and microservices). 
    - This can be a REST API, a GraphQL API, a gRPC API 
    - ORM是映射数据库的表到编程语言上的类。
    - 而Prisma是一个数据库工具，能够根据数据模型生成特定的查询工具。
    - Prisma会根据数据库的Schema，生成js的客户端库。在里面定义了相应的数据接口，关联关系和函数等。通过这些，来完成对数据的操作
  - Prisma Migrate: Declarative data modeling & migration system
  - Prisma Studio: GUI to view and edit data in your database
  - [Prisma ORM Architecture Shift: Why We Moved from Rust to TypeScript _202501](https://www.prisma.io/blog/from-rust-to-typescript-a-new-chapter-for-prisma-orm)
  - [为什么要用 Prisma？](https://zhuanlan.zhihu.com/p/142607078)
    - 自己手写SQL：控制力极强，生产力弱
      - 可以完全控制数据库操作，但是，生产力却不高，而且会遇到很多细碎的事情（如手动处理链接、操作模板）
      - 另一个问题在于你获取的查询结果时不是类型安全的，你可能会手动书写这些查询结果的类型
      - 手动构造SQL字符串的时候，编辑器没法给你任何提示
    - SQL构造器：控制力强，生产力一般
      - 使用SQL构造器（如 knext.js）以提高生产力，这种工具为构建 SQL 语句提供了封装层次较高的 API
      - 最大的问题在于这种工具需要开发者从 SQL 的角度来对待数据，但应用数据往往是关系型的对象，开发者不得不经常切换思维模型才能写好 SQL 语句。
    - ORM：控制力弱，生产力不错
      - ORM可以让开发者将所有数据定义为 class，一个 class 就是一个数据表，开发者不需要对 SQL 有那么深的理解了。
      - 可以通过 class 的方法来对数据库进行读写，非常方便
      - 开发者将数据理解为一个一个的对象集合，但实际上这些数据是一个一个的表。
      - 上个例子揭露了ORM的一个大陷阱：使用 ORM 表面上可以通过点符合来访问另一个实体，但是私底下却会构造 SQL JOIN 语句，这些 JOIN 是有性能陷阱的，很可能把你的应用拖得很慢，比如著名的 n+1 问题。
      - ORM的优点是抽象出关系模型并仅根据对象来操作数据。但是问题在于，关系型数据表并不能轻松地映射到对象，这会带来很多复杂性
    - Prisma：更高的生产力
      - 主要目标就是让开发者在处理数据库是更具生产力
      - 用对象来思考，而不是在大脑中映射关系型数据库
      - 数据库和数据模型来自同一个地方
      - 控制力高于SQL构造器，低于手写SQL； 但生产力最高

- typetta /63Star/apache2/202301/ts
  - https://github.com/twinlogix/typetta
  - ORM written in TypeScript that aims to allow seamless access to data in a typed fashion to all main SQL databases 
  - 依赖knex、graphql
  - (MySQL, PostgreSQL, Microsoft SQL Server, SQLLite3, CockroachDB, MariaDB, Oracle e Amazon Redshift) and also to the NoSQL database MongoDB.

- https://github.com/walinejs/dittorm /MIT/202305/ts/inactive
  - A Node.js ORM for MySQL, SQLite, PostgreSQL, MongoDB, GitHub and serverless service like Deta, InspireCloud, CloudBase, LeanCloud.
  - 依赖think-model, think-mongo(think.js)

- https://github.com/balderdashy/waterline /5.4kStar/MIT/202211/js/sails/inactive
  - An adapter-based ORM for Node.js with support for mysql, mongo, postgres, mssql (SQL Server), and more
  - Waterline is a next-generation storage and retrieval engine, and the default ORM used in the Sails framework.

- https://github.com/vincit/objection.js /MIT/202402/js
  - ORM for Node.js
  - built on an SQL query builder called knex
  - All databases supported by knex are supported by objection.js
  - https://github.com/feathersjs-ecosystem/feathers-objection
    - Feathers database adapter for Objection.js
  - forks
  - https://github.com/ovos/objection.js

- bookshelf /6.3kStar/MIT/202007/js/inactive
  - https://github.com/bookshelf/bookshelf
  - Bookshelf is a JavaScript ORM for Node.js, built on the Knex SQL query builder. 
  - It features both Promise-based and traditional callback interfaces, 
  - It is designed to work with PostgreSQL, MySQL, and SQLite3.
  - Bookshelf aims to provide a simple library for common tasks when querying databases in JavaScript, and forming relations between these objects, taking a lot of ideas from the Data Mapper Pattern.
  - https://github.com/seegno/bookshelf-json-columns
    - Parse JSON columns with Bookshelf.js

- https://github.com/Fibonacci-Solucoes-Ageis/MyBatisNodeJs /js
  - MyBatisNodeJs is a port from the The MyBatis data mapper framework for Node. Js.
  - MyBatisNodeJs understands the same xml files as input like MyBatis Java.
  - https://github.com/fsx950223/MyBatis-Node /ts
- https://github.com/PeterMu/nodebatis
  - A sql style orm lib for nodejs. (similar to mybatis on java)
- https://github.com/vyspace/nbatis
  - a node.js plugin about data persistence, similar to mybatis
- https://github.com/mybatis/mybatis-3
  - /14.3kStar/Apache2/202009/java
  - MyBatis SQL mapper framework for Java
  - https://github.com/pagehelper/Mybatis-PageHelper
  - https://github.com/baomidou/mybatis-plus
  - https://github.com/abel533/Mapper

- https://github.com/SpoonX/wetland
  - A Node.js ORM, mapping-based. Works with MySQL, PostgreSQL, SQLite and more.
- https://github.com/alfateam/rdb /js
  - ORM for nodejs. Supports postgres, msSql, mySql, Sybase SAP and sqlite.

- https://github.com/1602/jugglingdb /201607/js/inactive
  - Multi-database ORM for nodejs: redis, mongodb, mysql, sqlite3, postgresql, arango, in-memory

- https://github.com/egomobile/node-orm
  - https://github.com/egomobile/node-orm-pg
  - A simple and generic ORM mapper.
# orm-alternatives
- https://github.com/kysely-org/kysely /8.9kStar/MIT/202403/ts
  - https://kysely.dev/
  - a type-safe and autocompletion-friendly typescript SQL query builder. 
  - Inspired by knex. 

- https://github.com/archfirst/joinjs /MIT/201902/js/NoDeps/单文件/inactive
  - A JavaScript library to map complex database joins to nested objects
  - It's a simpler alternative to a full-blown Object-Relation Mapper (ORM), and gives you direct control over your database interactions.
  - JoinJS takes a much simpler and straightforward approach inspired by a popular Java mapping framework called MyBatis 
  - You can use any database driver or query builder (such as Knex.js) to query your database, however you use JoinJS to convert the returned results into a hierarchy of nested objects.
  - ResultMaps are used to teach JoinJS how to map database results to objects. 

- https://gitlab.com/dmfay/massive-js /BSD/202302/js/deprecated
  - a data mapper for Node.js that goes all in on PostgreSQL, and embraces the power and flexibility of SQL itself and of the relational metaphor
  - Massive is not an object-relational mapper (ORM)! It doesn't use models, it doesn't track state
  - https://gitlab.com/monstrous/monstrous /js
    - a lightweight SQL composer for Node.js and PostgreSQL

- https://github.com/foxifyjs/odin /MIT/202009/ts
  - Odin is an implementation of the Active Record pattern in TypeScript
  - JSON Schema generator (based on model schema)

- https://github.com/DavidDuwaer/Coloquent /MIT/202202/ts/inactive
  - library mapping objects and their interrelations to JSON API, with a clean, fluent ActiveRecord (e.g. similar to Laravel's Eloquent) syntax for creating, retrieving, updating and deleting model objects
# odm/object-document-mapper
- https://github.com/NaturalCycles/db-lib /202401/ts
  - Lowest Common Denominator API to supported Databases
  - DBQuery allows to use the same query syntax across different DBs. So, you can run it against Datastore, Firestore, Redis, MongoDB, Airtable, etc.
  - You can test your code against `InMemoryDB` (that implements full CommonDB interface, even with querying, streaming, etc). 

- https://github.com/biggora/caminte /MIT/201805/js
  - cross-db ORM for nodejs, providing common interface to access most popular database formats.
  - mysql, sqlite3, riak, postgres, couchdb, mongodb, redis, neo4j, firebird, rethinkdb, tingodb
  - [You support couchbase, not couchdb_201803](https://github.com/biggora/caminte/issues/181)
  - [Getting Null Values from CouchDB (cloudant)](https://github.com/biggora/caminte/issues/134)
    - I would recommend that if you are using cloudant or couch, just start from a scratch nodejs app, don't use any library for connection, as their is none that is well maintained and fully functional . All the best.
- https://github.com/grimen/node-document /201311/js
  - Minimalistic ODM for Node.js implementing the most fundamental operations (such as GET/SET/DEL) on different kinds of "document(-ish)" stores using one unified API. Switching database should be a matter of changing a line of code.
  - To stick to this philosophy more advanced operations won't be supported in core, but node-document can be used along with any 3rd-party drivers.

- https://github.com/Agrejus/db-framework /MIT/202311/ts
  - Database agnostic ORM for NodeJS and the web
  - a TypeScript first ORM designed to wrap existing database frameworks such as PouchDB to augment its functionality
  - Inspired by . NET's Entity Framework, Db Framework operates the same way and tries to keep method names as close as possible.
  - Db Framework provides a ton of flexibility, even going as far as offering a local state store (think Redux).
  - https://github.com/Agrejus/db-framework-plugin-examples
  - https://github.com/Agrejus/db-framework-plugin-memory
  - https://github.com/Agrejus/db-framework-plugin-local-storage
  - https://github.com/Agrejus/db-framework-plugin-capacitor-realm

- orbit /2.3kStar/MIT/202209/ts
  - https://github.com/orbitjs/orbit
  - Orbit is a composable data framework for managing the complex needs of today's web applications.
  - Although Orbit is **primarily used as a flexible client-side ORM** , it can also be used server-side in Node.js.
  - Interact with data from a variety of sources: a REST server, a WebSocket stream, an IndexedDB backup, an in-memory store, etc.
  - Work offline, work online, and seamlessly transition between both modes.
  - Support undo、redo
  - [How difficult is to create an offline-first app?](https://github.com/orbitjs/orbit/issues/790)
    - There is currently no CRDT implementation in orbit. There is no server implementation at all.

- https://github.com/izelnakri/memoria
  - Single JS/TS ORM for frontend, backend & in-memory testing
  - It is a very flexible `typeorm-like` entity definition API that just use JS classes and decorators to define or generate the schema. 
  - You can choose different adapters and use the same CRUD interface: MemoryAdapter, RESTAdapter or SQLAdapter.
  - The http mock server(@memoria/server) can be run in-browser and node environments, thus allows for running your in-memory test suite in SSR(server-side rendering) environment if it is needed.

- https://github.com/js-data/js-data /MIT/202201/js/inactive
  - JSData is a framework-agnostic, datastore-agnostic ORM for Node.js and the Browser.
  - Adapters allow JSData to connect to various data sources such as Firebase, MySql, RethinkDB, MongoDB, localStorage, Redis, a REST API
  - With JSData you can re-use your data modeling code between environments, with a unified data API on the server and the client. 

- https://github.com/paperhive/octonom /201802/ts
  - General-purpose models and collections with multi-database support, written in TypeScript
  - Collections are specific to the database you use (e.g. MongoCollection, CouchCollection)

- https://github.com/oslabs-beta/LiveStateDB /js/inactive
  - LiveStateDB is a database subscription API that enables developers to make state reflect database changes in real time. 
  - Currently, LiveStateDB only supports MongoDB.
  - LiveStateDB features a client side library and a server side library that can be installed via npm or yarn with the following commands. The libraries need to be installed on both sides in order to make use of LiveStateDB's real time updates.
# orm-non-js
- https://github.com/diesel-rs/diesel /MIT/202402/rust/同步api
  - https://diesel.rs/
  - A safe, extensible ORM and Query Builder for Rust
  - Supported databases: PostgreSQL, MySQL, SQLite
  - Preventing Runtime Errors: eliminate the possibility of incorrect database interactions at compile time.
  - Performance: Our focus on zero-cost abstractions allows Diesel to run your query and load your data even faster than C.
  - Extensible: Unlike Active Record and other ORMs, Diesel is designed to be abstracted over.
  - [What ORM do you use? : r/rust _202305](https://www.reddit.com/r/rust/comments/13d9ayi/what_orm_do_you_use/)
  - https://github.com/diesel-rs/diesel-dynamic-schema
    - Query schemas not known at compile time with Diesel
    - This code is merged into the main diesel repository

- https://github.com/SeaQL/sea-orm /MIT/202402/rust/异步api
  - https://www.sea-ql.org/SeaORM/
  - An async & dynamic ORM for Rust
  - Async: Relying on SQLx
  - Dynamic: Built upon SeaQuery, SeaORM allows you to build complex dynamic queries.
  - Service Oriented: Quickly build services that join, filter, sort and paginate data in REST, GraphQL and gRPC APIs.
  - 🆚️ [Compare with Diesel](https://www.sea-ql.org/SeaORM/docs/internal-design/diesel/)
    - the number one requested feature, async Rust support.SeaORM together with SQLx offers you a pure Rust technology stack. Diesel uses native drivers by default and it may take some effort for you to replace it with a pure Rust driver. 
    - big distinction between Diesel and SeaORM is static vs dynamic.
    - Diesel provides an everything-compile-time API where types can be checked entirely statically. You can also do dynamic queries with Diesel, but you'd lose some of the benefits of compile-time type-checking.
    - SeaORM is dynamic, in which things are established at runtime. It offers more flexibility. 
  - https://github.com/SeaQL/sea-query /rust
    - A dynamic SQL query builder for MySQL, Postgres and SQLite
  - https://github.com/SeaQL/starfish-ql
    - a graph database and query engine to enable graph analysis and visualization on the web. 
    - StarfishQL uses a SQL database internally and is built on top of other libraries in the SeaQL ecosystem.

- https://github.com/launchbadge/sqlx /MIT/202402/rust
  - an async, pure Rust† SQL crate featuring compile-time checked queries without a DSL.
  - Truly Asynchronous. Built from the ground-up using async/await for maximum concurrency.
  - Compile-time checked queries (if you want). See SQLx is not an ORM.
  - Database Agnostic. Support for PostgreSQL, MySQL, MariaDB, SQLite.
  - Runtime Agnostic. Works on different runtimes (async-std / tokio / actix) and TLS backends (native-tls, rustls).

- https://github.com/upper/db /202208/go
  - Data access layer for PostgreSQL, CockroachDB, MySQL, SQLite and MongoDB with ORM-like features
# db-non-js
- https://github.com/pingcap/talent-plan /使用rust实现db
  - https://tidb.net/talent-plan
  - Talent Plan 301 课程 TinySQL, 实现一个 Mini 版本的分布式关系型数据库
  - Talent Plan 302 课程 TinyKV, 实现一个 Mini 版本的分布式 Key-Value 数据库
  - https://github.com/iFaceless/tinkv
    - fast key-value storage engine written in Rust. Inspired by basho/bitcask, written after attending the Talent Plan courses.
    - provides a bultin CLI and a Redis compatible server
- https://github.com/talent-plan/tinykv /go
  - The TinyKV course builds a key-value storage system with the Raft consensus algorithm. It is inspired by MIT 6.824 and TiKV Project.
- https://github.com/talent-plan/tinysql /go
  - a course designed to teach you how to implement a distributed relational database in Go. 
  - The name TinySQL indicates it is a simplified version of TiDB.

- https://github.com/risinglightdb/risinglight /rust
  - An OLAP database system for educational purpose

- https://github.com/erikgrinaker/toydb /202205/rust
  - Distributed SQL database in Rust, written as a learning project
  - 内部自己实现了SQL Parser、Query Planner、Storage（包括一个B+Tree）和Raft，都是直接编写的（简化版本）的源码而不是用外部库，确实很适合用来学习
  - [ToyDB: Distributed SQL Database in Rust | Hacker News_202107](https://news.ycombinator.com/item?id=27874992)
- https://github.com/JRMurr/SQLJr /rust
  - Toy DB to get more systems expereince
  - [Building a Simple DB in Rust - Part 1 - Parsing](https://johns.codes/blog/build-a-db/part01)
- https://github.com/mzinsmeister/OxidSQL /apache2/202306/rust
  - Toy SQL Database in Rust

- https://github.com/nukep/llamadb /201712/rust/inactive
  - a simple SQL database, written entirely in Rust 
  - SQLite documentation helped shed some light on the SQL syntax and other crucial details such as their B-Tree implementation.
  - [LlamaDB: A simple SQL database written in Rust | Hacker News_201504](https://news.ycombinator.com/item?id=9395690)

- https://github.com/khonsulabs/bonsaidb /918Star/MIT/202311/rust
  - https://bonsaidb.io/
  - A programmable document database inspired by `CouchDB` written in Rust.
  - ACID-compliant, transactional storage of Collections
  - Role-Based Access Control (RBAC)
  - Local-only access, networked access via QUIC, or networked access via WebSockets
  - [Introducing PliantDb](https://ecton.dev/introducing-pliantdb/)
  - [Branch support](https://github.com/khonsulabs/nebari/issues/29)
    - For BonsaiDb we plan on supporting the replication logic at the BonsaiDb level, and we are hoping to support bi-directional replication with customizable conflict resolution. 
    - This is a form of branching, because you can clone a database using replication, modify it, and then eventually replicate again in either direction.
  - [Project Status_202301](https://github.com/khonsulabs/bonsaidb/issues/262)
    - One serious thought I still have is whether Nebari should exist, or whether BonsaiDb should just use another database format. 
  - https://github.com/khonsulabs/nebari /rust
    - A pure Rust database implementation using an append-only B-Tree file format.
    - This crate provides the Roots type, which is the transactional storage layer for BonsaiDb. It is loosely inspired by `Couchstore`.
    - This crate blocks the current thread when accessing the filesystem. If you are looking for an async-ready database, BonsaiDb is our vision of an async-aware database built atop Nebari.
    - Nebari exposes multiple levels of functionality. The lowest level functionality is the `TreeFile`. A `TreeFile` is a key-value store that uses an append-only file format for its implementation.
    - Using TreeFiles and a transaction log, Roots enables ACID-compliant, multi-tree transactions.
  - Why use an append-only file format?
    - Creating ACID-compliance with append-only formats is much easier to achieve, however, as long as you can guarantee two things:
    - When opening a previously existing file, can you identify where the last valid write occurred?
    - When writing the file, do not report that a transaction has succeeded until the file is fully flushed to disk.
    - The B-Tree implementation in Nebari is designed to offer those exact guarantees.
    - The major downside of append-only formats is that deleted data isn't cleaned up until a maintenance process occurs: compaction. 

- https://github.com/mozilla/mentat /201809/rust/inactive
  - https://mozilla.github.io/mentat/
  - A persistent, relational store inspired by Datomic and DataScript
  - Mentat is intended to be a flexible relational (not key-value, not document-oriented) store that makes it easy to describe, grow, and reuse your domain schema.
  - Just like DataScript, Mentat speaks Datalog for querying and takes additions and retractions as input to a transaction.
  - Unlike DataScript, Mentat exposes free-text indexing, **thanks to SQLite** .
  - Mentat was designed for embedding, initially in an experimental Electron app 
  - Mentat uses partial indices, which are available in SQLite 3.8.0 and higher
  - 🍴 forks
  - https://github.com/qpdb/mentat
  - https://github.com/mozilla/mentat/tree/clojure /201702

- https://github.com/objectbox/objectbox-java /4.3kStar/apache2/202311/java
  - https://objectbox.io/
  - Java and Android Database - fast and lightweight without any ORM
  - ObjectBox is a NoSQL Java database designed for local data storage on resource-restricted devices, prioritizing offline-first functionality. 
  - It is a smart and sustainable choice for local data persistence in Java and Kotlin applications.
  - built-in support for object relations, allowing you to easily establish and manage relationships between objects.
  - concise API that eliminates the need for complex SQL queries, saving you time and effort during development.
  - [ObjectBox is not entirely FOSS](https://github.com/objectbox/objectbox-java/issues/1102)
    - it isn't open source. The language wrappers are apache2 but the core library is only provided as a binary blob.
    - ObjectBox bindings are open sourced under Apache 2.0; accessing the ObjectBox core is possible with a commercial licence that also includes support. The reason is that it is mainly big B2B IoT users that need access and support - and these customers allow us to maintain ObjectBox DB free to use for (almost) everyone else.

- https://github.com/unum-cloud/ukv /cpp/modular
  - Modular Transactional NoSQL Database
  - choose either: RocksDB • LevelDB • UDisk • UMem 
  - to store: Blobs • Documents • Graphs • Vectors • Texts
  - It is a "build your database" toolkit and an open standard for NoSQL potentially-transactional databases, defining zero-copy binary interfaces for CRUD

- https://github.com/arangodb/arangodb /cpp/js
  - https://www.arangodb.com/
  - ArangoDB is a native multi-model database with flexible data models for documents, graphs, and key-values.
  - Native graphs, an integrated search engine, and JSON support, via a single query language. 
  - ArangoDB runs on-prem, in the cloud – anywhere.
  - ArangoDB is available in a free and open-source Community Edition, as well as a commercial Enterprise Edition with additional features.
  - [ArangoDB: Multi-model highly available NoSQL database | Hacker News_201901](https://news.ycombinator.com/item?id=18926054)

- https://github.com/engula/engula /apache2/rust/inactive/selectdb成员项目
  - https://engula.io/
  - a distributed key-value store, used as a cache, database, and storage engine.
  - [Engula Development Guide](https://github.com/engula/engula/discussions/244)
    - API: inspired by Redis, and some programming languages like Rust, Python, etc.
    - Architecture: inspired by Socrates, Aurora, Spanner, BigTable, TAO.
    - Transaction: inspired by hybrid-logical-clocks (HLC)
    - Stream engine: inspired by LogDevice, Delos
    - Object engine: inspired by RocksDB, GFS, and DeltaLake.
  - https://github.com/w41ter/sekas /rust
    - a distributed key-value store, used as cache, database, and storage engine for other distributed system.

- https://github.com/isar/isar /Flutter
  - Extremely fast, easy to use, and fully async NoSQL database for Flutter
  - The new Isar Core (written in Rust) can be compiled to wasm and will be insanely fast with all features. Unlike the current IndexedDB implementation.

- https://github.com/pruttned/owl-invoice /ts
  - [Turning Git into an application database](https://nede.dev/blog/turning-git-into-an-application-database)
  - using Git backed filesystem as an application database.

- https://github.com/codefollower/H2-Research
  - H2数据库源代码学习研究
  - 包括代码注释、文档、用于代码分析的测试用例

- https://github.com/erthink/libmdbx /c/inactive
  - an extremely fast, compact, powerful, embedded, transactional key-value database, with permissive license. 
  - Provides extraordinary performance, minimal overhead through Memory-Mapping and Olog(N) operations costs by virtue of B+ tree.
  - Compact and friendly for fully embedding. Only ≈25KLOC of C11, ≈64K x86 binary code of core, no internal threads neither server process(es), but implements a simplified variant of the Berkeley DB and dbm API.
  - Historically, libmdbx is a deeply revised and extended descendant of the amazing Lightning Memory-Mapped Database. libmdbx inherits all benefits from LMDB, but resolves some issues and adds a set of improvements.

- https://github.com/hoytech/quadrable /cpp
  - an authenticated multi-version database that can efficiently sync itself with remote instances. 
  - It is implemented as a sparse binary merkle tree with compact partial-tree proofs. 
  - Many different versions of the database can exist at the same time. Deriving one version from another doesn't require copying the database. Instead, all of the data that is common between the versions is shared. This copy-on-write behaviour allows very inexpensive database snapshots and checkpoints.
  - applications can synchronise with remote instances. Conflict-handling is flexible, and can work by either cloning one side or by merging the states together (like a CRDT)

- https://github.com/mkaminski1988/mkdb /go
  - a SQL-based relational database management system (RDBMS) written in Golang (1.18+) with zero third-party dependencies. 
  - The goal of the project is to provide a creative outlet for developers who want to experiment with database development 
  - On-disk B+ tree
  - Write-ahead logging (WAL)

- https://github.com/vaticle/typedb /java
  - a strongly typed database with an intelligent reasoning engine to infer new data and a declarative query language based on composable patterns to find it easily.
  - Model data naturally – as the entities, relations, and attributes defined in an entity-relationship diagram.
  - https://github.com/vaticle/typeql /java/rust
    - TypeQL is a fully declarative query language based on pattern matching. 
    - TypeQL allows you to model your domain based on logical and object-oriented principles. 
    - Composed of entity, relationship, and attribute types, as well as type hierarchies, roles, and rules, TypeQL allows you to think higher-level as opposed to join-tables, columns, documents, vertices, edges, and properties.

## db-olap

- https://github.com/splitgraph/seafowl /rust
  - https://seafowl.io/
  - Analytical database for data-driven Web applications
  - Its CDN and HTTP cache-friendly query execution API lets you deliver data to your visualizations, dashboards and notebooks by running SQL straight from the user's browser.
  - built around Apache DataFusion, a fast and extensible query execution framework. 
  - It uses Apache Parquet columnar storage, adhering to the Delta Lake protocol, making it perfect for analytical workloads.
  - For SELECT queries, Seafowl supports a large subset of the PostgreSQL dialect. 
  - It ships as a single binary, making it simple to run anywhere, letting you separate storage and compute. 
  - Seafowl's query execution API follows HTTP cache semantics. This means you can put Seafowl behind a CDN like Cloudflare 
  - We (Splitgraph) implemented WASM UDFs in Seafowl, Users can call CREATE FUNCTION within an SQL query to create a WASM UDF.
# db-popular
- https://github.com/vitessio/vitess /17.9kStar/apache2/202405/go
  - https://vitess.io/
  - Vitess is a database clustering system for horizontal scaling of MySQL through generalized sharding.
  - Vitess is the cloud-native, open source technology powering PlanetScale.
  - By encapsulating shard-routing logic, Vitess allows application code and database queries to remain agnostic to the distribution of data onto multiple shards
  - Vitess has been a core component of YouTube's database infrastructure since 2011, and has grown to encompass tens of thousands of MySQL nodes.
  - [RFC: Postgres support · vitessio/vitess _202011](https://github.com/vitessio/vitess/issues/7084)
    - FYI: there is Citus and it is doing something similar to Vitess.
    - I'll probably start with Citus or Yugabyte for now, since even if Postgres support is added it is still far away.

- https://github.com/dolthub/go-mysql-server /1.2kStar/apache2/202311/go
  - A MySQL compatible database engine written in pure Go
  - go-mysql-server is a drop-in replacement for MySQL. Any client library, tool, query, SQL syntax, SQL function, etc. that works with MySQL should also work with go-mysql-server.
  - go-mysql-server is a data-source agnostic SQL engine and server which runs queries on data sources you provide, using the MySQL dialect and wire protocol. 
  - A simple in-memory database implementation is included, and you can query any data source you want by implementing your own backend.
  - dolt is the main production database implementation of this package.

- https://github.com/dolthub/doltgresql /365Star/apache2/202311/go
  - a Postgres-flavored version of Dolt. 
  - Doltgres offers all the Git-style log, diff, branch, and merge functionality of Dolt on your Postgres database schema and data.
  - connect to Doltgres with a Postgres client and use Postgres SQL

- https://github.com/facebook/mysql-5.6 /GPLv2/cpp/c
  - http://myrocks.io/
  - Facebook's branch of the Oracle MySQL v5.6 database. This includes MyRocks.
# db-streaming
- https://github.com/MaterializeInc/materialize /rust
  - https://materialize.com/
  - Materialize is a fast, distributed SQL database built on streaming internals.
  - Materialize is a streaming database powered by Timely and Differential Dataflow, purpose-built for low-latency applications. 
  - [adapter: Switch to Hybrid Logical Timestamps (HLT)_202303](https://github.com/MaterializeInc/materialize/issues/17936)
- https://github.com/TimelyDataflow/timely-dataflow
  - A modular implementation of timely dataflow in Rust
- https://github.com/TimelyDataflow/differential-dataflow
  - An implementation of differential dataflow over timely dataflow on Rust.
# gis
- https://github.com/digidem/bkd-tree /BSD/201906/js
  - multi-dimensional spatial database based on the bkd paper
  - bkd tree implementation using random-access storage
  - This module implements some of the bkd tree paper and is very fast. However, the memory usage can be high at times and some features of the paper, such as the grid bulk load algorithm, are not yet implemented.
# nosql
- https://github.com/eclipse/jnosql-databases /EPLv1
  - https://www.jnosql.org/
  - a Java framework that streamlines the integration of Java applications with NoSQL databases.
# db-middlewares
- https://github.com/Meituan-Dianping/Zebra /apache2/201911/java
  - 基于JDBC API协议上开发出的高可用、高性能的数据库访问层解决方案
  - 简化了读写分离、分库分表的开发工作

- https://github.com/JimmyAndZzZ/hulk /202308/java
  - 基于Mysql协议的数据库中间件
  - 基于Mysql协议，可以通过navicat、jdbc等连接方式
  - 支持用SQL查询非结构化和结构化数据库，例如Mysql、Oracle、Clickhouse、Excel、elasticsearch
  - 支持不同数据源之间表关联查，目前支持inner join和left join
  - 基于calcite进行SQL解析，并对SQL进行扩展，支持自定义扩展操作
  - 读写分离、单写多读
  - 支持分库分表、权限设置(可到字段级别)
# more-database
- https://github.com/lealone/Lealone
  - /1.6kStar/Apache2+H2MPL2/202012/java
  - 兼具RDBMS、NoSQL优点的面向OLTP场景的异步化NewSQL单机与分布式关系数据库

- https://github.com/Jianxff/NEDB /cpp/B+Tree
  - NEDB 是基于 C++ 的简单数据库. 项目参考 SQLite 底层原理与 InnoDB 引擎, 实现数据库[增-删-查-改]的基本操作, 并提供控制台界面与外部接口.

- https://github.com/moleculerjs/database
  - https://github.com/moleculerjs/moleculer-db
  - Advanced Database Access Service for Moleculer microservices framework. 
  - Use it to persist your data in a database.
  - Moleculer is a fast, modern and powerful microservices framework for Node.js.
