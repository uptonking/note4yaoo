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
# orm
- https://github.com/edgedb/imdbench
  - A benchmark intended to compare various Python and JavaScript ORMs with realistic queries required for a hypothetical IMDB-style movie database application.
  - js: prisma、typeorm、sequelize、edgedb
  - python: django、sqlalchemy、edgedb
- https://github.com/emanuelcasco/typescript-orm-benchmark /202009/ts/inactive
  - ORM benchmarking for Node.js applications written in TypeScript

- https://github.com/tkssharma/nodejs-db-orm-world /202003/ts
  - Node JS with different ORM like Typeorm, Knex, Prisma and Sequelize with Node JS API Development Node JS with without any ORM (MYSQL raw queries)

- typeorm /30.1kStar/MIT/202301/ts
  - https://github.com/typeorm/typeorm
  - http://typeorm.io/
  - TypeORM is an ORM that can run in NodeJS, Browser, Cordova, PhoneGap, Ionic, React Native, NativeScript, Expo, and Electron platforms
  - Supports MySQL, PostgreSQL, MariaDB, SQLite, MS SQL Server, Oracle, SAP Hana, sql.js.
  - Supports MongoDB NoSQL database.
  - ✨ TypeORM supports both Active Record and Data Mapper patterns
  - 依赖date-fns, reflect-metadata, buffer
  - TypeORM is highly influenced by other ORMs, such as Hibernate, Doctrine and Entity Framework.

- mikro-orm /5.5kStar/MIT/202301/ts/开发者主程只有1个
  - https://github.com/mikro-orm/mikro-orm
  - https://mikro-orm.io/
  - TypeScript ORM for Node.js based on Data Mapper, Unit of Work and Identity Map patterns.
  - 依赖acorn-loose, fs-extra, reflect-metadata
  - Supports MongoDB, MySQL, MariaDB, PostgreSQL and SQLite databases.
  - Heavily inspired by Doctrine and Nextras Orm. (两者都为PHP设计)
  - 使用基于装饰器
  - Unit of Work maintains a list of objects (entities) affected by a business transaction and coordinates the writing out of changes. 
  - Identity Map ensures that each object (entity) gets loaded only once by keeping every loaded object in a map. Looks up objects using the map when referring to them. 

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

- https://github.com/sequelize/sequelize
  - An easy-to-use multi SQL dialect ORM for Node.js
  - 不支持mongo

- typetta /63Star/apache2/202301/ts
  - https://github.com/twinlogix/typetta
  - ORM written in TypeScript that aims to allow seamless access to data in a typed fashion to all main SQL databases 
  - 依赖knex、graphql
  - (MySQL, PostgreSQL, Microsoft SQL Server, SQLLite3, CockroachDB, MariaDB, Oracle e Amazon Redshift) and also to the NoSQL database MongoDB.

- https://github.com/walinejs/dittorm
  - A Node.js ORM for MySQL, SQLite, PostgreSQL, MongoDB, GitHub and serverless service like Deta, InspireCloud, CloudBase, LeanCloud.
  - 依赖think-model, think-mongo(think.js)

- https://github.com/balderdashy/waterline /202208/js/inactive
  - An adapter-based ORM for Node.js with support for mysql, mongo, postgres, mssql (SQL Server), and more
  - Waterline is a next-generation storage and retrieval engine, and the default ORM used in the Sails framework.

- https://github.com/drizzle-team/drizzle-orm
  - a TypeScript ORM for SQL databases
  - 支持mysql、postgresql、sqlite，不支持mongo
  - 代码量少

- bookshelf /6.3kStar/MIT/202007/js/inactive
  - https://github.com/bookshelf/bookshelf
  - Bookshelf is a JavaScript ORM for Node.js, built on the Knex SQL query builder. 
  - It features both Promise-based and traditional callback interfaces, 
  - It is designed to work with PostgreSQL, MySQL, and SQLite3.
  - Bookshelf aims to provide a simple library for common tasks when querying databases in JavaScript, and forming relations between these objects, taking a lot of ideas from the Data Mapper Pattern.
  - https://github.com/seegno/bookshelf-json-columns
    - Parse JSON columns with Bookshelf.js

- https://github.com/vincit/objection.js
  - Objection.js is an ORM for Node.js
  - built on an SQL query builder called knex
  - https://github.com/feathersjs-ecosystem/feathers-objection
    - Feathers database adapter for Objection.js

- orbit /2.3kStar/MIT/202209/ts
  - https://github.com/orbitjs/orbit
  - Orbit is a composable data framework for managing the complex needs of today's web applications.
  - Although Orbit is primarily used as a flexible client-side ORM, it can also be used server-side in Node.js.
  - Interact with data from a variety of sources: a REST server, a WebSocket stream, an IndexedDB backup, an in-memory store, etc.
  - Work offline, work online, and seamlessly transition between both modes.
  - Support undo、redo

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

- https://github.com/izelnakri/memoria
  - Single JS/TS ORM for frontend, backend & in-memory testing
  - It is a very flexible typeorm-like entity definition API that just use JS classes and decorators to define or generate the schema. 
  - You can choose different adapters and use the same CRUD interface: MemoryAdapter, RESTAdapter or SQLAdapter.
  - The http mock server(@memoria/server) can be run in-browser and node environments, thus allows for running your in-memory test suite in SSR(server-side rendering) environment if it is needed.

- https://github.com/1602/jugglingdb /201607/js/inactive
  - Multi-database ORM for nodejs: redis, mongodb, mysql, sqlite3, postgresql, arango, in-memory

- https://github.com/egomobile/node-orm
  - https://github.com/egomobile/node-orm-pg
  - A simple and generic ORM mapper.

- https://github.com/js-data/js-data /202201/js/inactive
  - JSData is a framework-agnostic, datastore-agnostic ORM for Node.js and the Browser.
  - Adapters allow JSData to connect to various data sources such as Firebase, MySql, RethinkDB, MongoDB, localStorage, Redis, a REST API
# database
- https://github.com/codefollower/H2-Research
  - H2数据库源代码学习研究
  - 包括代码注释、文档、用于代码分析的测试用例
# rdbms
- https://github.com/erikgrinaker/toydb /202205/rust
  - Distributed SQL database in Rust, written as a learning project
  - 内部自己实现了SQL Parser、Query Planner、Storage（包括一个B+Tree）和Raft，都是直接编写的（简化版本）的源码而不是用外部库，确实很适合用来学习

- https://github.com/nukep/llamadb /201712/rust
  - a simple SQL database, written entirely in Rust 

- https://github.com/PostgREST/postgrest
  - https://postgrest.org/
  - PostgREST serves a fully RESTful API from any existing PostgreSQL database. 
  - It provides a cleaner, more standards-compliant, faster API than you are likely to write from scratch.
  - 可直接将 PostgreSQL 数据库发布成 REST API，甚至有基于此库的 SaaS 服务如 supabase 可提供类 Google Firebase 的功能。
# orm-non-js
- https://github.com/upper/db /202208/go
  - Data access layer for PostgreSQL, CockroachDB, MySQL, SQLite and MongoDB with ORM-like features
# json based database
- SirDB /493Star/AGPLv3/202012/js
  - https://github.com/c9fe/sirdb
  - A simple database on the file system.
  - JSON files organised into subdirectories for each table.
  - ServeData is a powerful yet simple server for SirDB 
    - with baked-in schemas, users, groups, permissions, authentication, authorization and payments.
  - text-based. 
    - Everything is a JSON file, including the database meta information.
  - is around 500 lines of code and 6.6Kb gzipped.
# db-non-js
- https://github.com/pingcap/talent-plan /使用rust实现db
  - https://tidb.net/talent-plan
  - Talent Plan 301 课程 TinySQL, 实现一个 Mini 版本的分布式关系型数据库
  - Talent Plan 302 课程 TinyKV, 实现一个 Mini 版本的分布式 Key-Value 数据库

- https://github.com/unum-cloud/ukv /cpp
  - Modular Transactional NoSQL Database
  - choose either: RocksDB • LevelDB • UDisk • UMem 
  - to store: Blobs • Documents • Graphs • Vectors • Texts
  - It is a "build your database" toolkit and an open standard for NoSQL potentially-transactional databases, defining zero-copy binary interfaces for CRUD

- https://github.com/isar/isar /Flutter
  - Extremely fast, easy to use, and fully async NoSQL database for Flutter
  - The new Isar Core (written in Rust) can be compiled to wasm and will be insanely fast with all features. Unlike the current IndexedDB implementation.
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
