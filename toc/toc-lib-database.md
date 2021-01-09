---
title: toc-lib-database
tags: [database, lib, toc]
created: '2020-10-05T16:22:46.508Z'
modified: '2020-10-22T13:11:04.726Z'
---

# toc-lib-database

# orm

- https://github.com/typeorm/typeorm
  - /22kStar/MIT/202011/ts
  - TypeORM is an ORM that can run in NodeJS, Browser, Cordova, PhoneGap, Ionic, React Native, NativeScript, Expo, and Electron platforms
  - Supports MySQL, PostgreSQL, MariaDB, SQLite, MS SQL Server, Oracle, SAP Hana, WebSQL databases.
  - TypeORM supports both Active Record and Data Mapper patterns
  - TypeORM is highly influenced by other ORMs, such as Hibernate, Doctrine and Entity Framework.

- https://github.com/prisma/prisma
  - /6.7kStar/Apache2/202012/ts
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

- https://github.com/orbitjs/orbit
  - Orbit is a composable data framework for managing the complex needs of today's web applications.
  - Although Orbit is primarily used as a flexible client-side ORM, it can also be used server-side in Node.js.

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

# popular database

- https://github.com/typicode/lowdb
  - a small local JSON database powered by Lodash 
  - supports Node, Electron and the browser

- https://github.com/pubkey/rxdb
  - A realtime Database for JavaScript Applications
  - a NoSQL-database for JavaScript Applications like Websites, hybrid Apps, Electron-Apps and NodeJs. 
  - Reactive means that you can not only query the current state, but subscribe to all state changes like the result of a query or even a single field of a document.
  - RxDB implements rxjs to make your data reactive. 
    - This makes it easy to always show the real-time database-state in the dom without manually re-submitting your queries.
- https://github.com/Nozbe/WatermelonDB
  - Reactive & asynchronous database for powerful React and React Native apps

- https://github.com/google/lovefield
  - Lovefield is a relational database for web apps. 
  - Written in JavaScript, works cross-browser. 
  - Provides SQL-like APIs that are fast, safe, and easy to use.
  - https://github.com/teambition/ReactiveDB
    - Reactive ORM for Lovefield
    - 一个 Reactive 风格的前端 ORM。基于 Lovefield 与 RxJS

- https://github.com/techfort/LokiJS
  - /5.6kStar/MIT/202012/js
  - javascript embeddable/in-memory database
  - The super fast in-memory javascript document oriented database.
  - Its purpose is to store javascript objects as documents in a nosql fashion and retrieve them with a similar mechanism. 
  - Runs in node (including cordova/phonegap and node-webkit), nativescript and the browser.

- https://github.com/codefollower/H2-Research
  - H2数据库源代码学习研究
  - 包括代码注释、文档、用于代码分析的测试用例

# rdbms

# nosql

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

# more-database

- https://github.com/lealone/Lealone
  - /1.6kStar/Apache2+H2MPL2/202012/java
  - 兼具RDBMS、NoSQL优点的面向OLTP场景的异步化NewSQL单机与分布式关系数据库
