---
title: toc-db-utils
tags: [db, toc, utils]
created: 2022-11-06T11:21:17.190Z
modified: 2022-11-06T11:21:27.612Z
---

# toc-db-utils

# guide

- [DB Fiddle - SQL Database Playground](https://www.db-fiddle.com/)
  - An online SQL database playground for testing, debugging and sharing SQL snippets.

- [dbdiagram.io - Database Relationship Diagrams Design Tool](https://dbdiagram.io/home)
  - simple tool to draw ER diagrams by just writing code
  - Designed for developers and data analysts
# popular
- https://github.com/www-zerocode-net-cn/ERD-Online /MIT/202312/ts
  - https://www.erdonline.com/
  - 开源、免费在线数据建模、元数据管理平台
  - 团队协作：三级权限（拥有者、管理员、普通角色）管理，元素级权限控制
  - 依赖antd-pro、mui5、ace、spreadsheet-ce、handsontable.v6
  - 元数据设计：快速复制已有表结构、JSON 生成表，表默认字段、默认大小写等控制
  - 支持多种数据库连接在线管理（Mysql、Oracle、DB2、SqlServer、PostGreSql），各数据源之间元数据结构同步
  - 版本管理：每个需求与变动，都可以生成版本；每个版本之间可以比对差异
  - 可将所有表结构，自动生成 word、html、md 文档，便于线下流动

- https://github.com/findyourmagic/dber /MIT/202311/js/inactive
  - https://dber.tech/
  - 基于实体连接图的数据库设计工具
  - 拖拽生成模型引用关系
  - 一键导出 SQL 语句
  - 依赖SVG、Next.js、DBML、ArcoDesign、Dexie(indexDB)、Soul CLI(sqlite)
  - 实现有些粗糙，但胜在免费的，也没有表数量限制

- https://github.com/PieterjanDeClippel/DragDropOrderingDatabase /202111/csharp/inactive
  - How to reorder items at database level using the Stern-Brocot technique

- https://github.com/fasiha/mudderjs /Unlicense(free)/202301/js/inactive
  - Lexicographically-subdivide the “space” between strings, by defining an alternate non-base-ten number system using a pre-defined dictionary of symbol↔︎number mappings. 
  - Handy for ordering NoSQL keys.
# rest
- https://github.com/formio/resquel /202101/ts/inactive
  - Express.js middleware library that is able to convert SQL databases into a REST API.
  - works seamlessly with the Form.io platform where you can build Angular.js and React.js applications on top of your SQL database.
  - This library has been validated with Microsoft SQL Server, MySQL, and PostgreSQL.

- https://github.com/TRUEPIC/queryql /202206/js
  - QueryQL takes a parsed query string (like Express' req.query) and translates it into the appropriate function calls that your query builder/ORM understands to filter, sort, and paginate the records.
  - QueryQL works with any Node.js web framework (be it Express, Koa, etc.), supports any query builder / ORM through adapters, and allows for custom validators so you can define validation in a familiar way.

- https://github.com/PostgREST/postgrest /haskell
  - PostgREST serves a fully RESTful API from any existing PostgreSQL database. 
  - It provides a cleaner, more standards-compliant, faster API than you are likely to write from scratch.
# apps
- https://github.com/multiprocessio/datastation /ts/go
  - DataStation is an open-source data IDE for developers. 
  - It allows you to easily build graphs and tables with data pulled from SQL databases
  - Write embedded scripts as needed in languages like Python, JavaScript, R or SQL. All in one application.

- tad /2.5kStar/MIT/202212/ts/duckdb/SlickGrid
  - https://github.com/antonycourtney/tad
  - Tad desktop application enables you to quickly view and explore tabular data in several of the most popular tabular data file formats: CSV, Parquet, and SQLite and DuckDb database files. 
  - 依赖aggtree、reltab
  - Internally, the application is powered by an in-memory instance of `DuckDb`, a fast, embeddable database engine optimized for analytic queries.
  - The core of Tad is a React UI component that implements a hierarchical pivot table that allows you to specify a combination of pivot, filter, aggregate, sort, column selection
  - Tad uses `SlickGrid` for rendering the data grid. 
  - Tad was initially released in 2017 as a standalone desktop application for viewing and exploring CSV files.
  - reltab
    - The core abstraction used in Tad for programmatically constructing and executing relational SQL queries.
    - This also defines the driver interface implemented by specific database back-ends, and a small, transport-agnostic remoting layer to allow queries and results to be transmitted between a web browser (or electron renderer process) and a reltab backend server.
# etl
- https://github.com/Claviz/bellboy /202305/ts
  - Highly performant JavaScript data stream ETL engine.
  - Bellboy streams input data row by row. Every row, in turn, goes through user-defined function where it can be transformed.
  - When enough data is collected in batch, it is being loaded to destination.
  - A job in bellboy is a relationship link between processor and destinations
  - Each processor in bellboy is a class which has a single responsibility of processing data of specific type
  - Every job can have as many destinations (outputs) as needed. For example, one job can load processed data into a database, log this data to stdout and post it by HTTP simultaneously.
  - New processors and destinations can be made by extending existing ones.

- https://github.com/ZJONSSON/node-etl /202201/js
  - ETL is a collection of stream based components that can be piped together to form a complete ETL pipeline with buffering, bulk-inserts and concurrent database streams. 

- https://github.com/MrSmallLiu/node-datax /202012/ts
  - 使用TypeScript开发的Node的数据提取工具
  - 仅支持postgres
# migrate
- https://github.com/wekan/minio-metadata /202304/js
  - Transfer files from MongoDB GridFS to Minio file server, and MongoDB text to SQLite
  - Bash scripts to transfer attachment and avatar files from MongoDB GridFS to Minio file server
    - To make MongoDB Server database size smaller (like from 800 GB tIo 10 GB), store files elsewhere, and have files visible in upcoming version of WeKan.
    - Meteor WeKan will continue using MongoDB for text data. Files can be stored outside of MongoDB.
    - Upcoming WeKan will use SQLite database for text data. Files are stored outside of SQLite.

- https://github.com/sensedeep/onetable-migrate /js/参考kv存储的迁移
  - This library provides migrations support for DynamoDB OneTable.
# utils
- https://github.com/holistics/dbml /2.4kStar/apache2/202404/js
  - https://dbml.dbdiagram.io/
  - Database Markup Language (DBML), designed to define and document database structures
  - a simple, readable DSL language designed to define database structures.
  - simple, flexible and highly human-readable
  - database agnostic, focusing on the essential database structure definition without worrying about the detailed syntaxes of each database
  - Comes with a free, simple database visualiser at dbdiagram.io

- https://github.com/Qovery/Replibyte /rust
  - https://www.replibyte.com/
  - fast tool to seed your databases with your production data while keeping sensitive data safe
  - [Replibyte – Seed your database with real data | Hacker News_202207](https://news.ycombinator.com/item?id=32047535)

- https://github.com/w3tecch/typeorm-seeding
  - A delightful way to seed test data into your database.
  - Inspired by the awesome framework laravel in PHP and of the repositories from pleerock

- https://github.com/datacosmos-br/cloudbeaver
  - Cloud Database Manager - Community Edition.

- https://github.com/nlfiedler/fastcdc-rs /MIT/202310/rust
  - FastCDC implementation in Rust
  - FastCDC: a Fast and Efficient Content-Defined Chunking Approach for Data Deduplication
  - This crate contains multiple implementations of the "FastCDC" content defined chunking algorithm originally described in 2016, and later enhanced in 2020, by Wen Xia, et al. 
  - A critical aspect of its behavior is that it returns exactly the same results for the same input.
# db-cache
- https://github.com/CyCraft/magnetar
  - Magnetar is a state management library.
  - A library that brings a simple syntax for reading and writing data and allows you to easily work with this data in your app like a global store.
  - A framework-agnostic syncing solution that auto-connects any DB/API with your local data store and has optimistic-UI built in
  - Magnetar has 2-way sync database integration for Google Firestore (and others coming). You do not need to learn to work with the database SDK.
# db-client
- https://github.com/outerbase/studio /AGPLv3/202412/ts
  - https://studio.outerbase.com/
  - A lightweight Database GUI in your browser. 
  - It supports connecting to Postgres, MySQL, and SQLite.
  - a lightweight, browser-based GUI for managing SQL databases, designed for simplicity and versatility. 
  - Initially built for LibSQL and SQLite, it now supports a broad range of databases
  - Outerbase Studio Desktop is a lightweight Electron wrapper for the Outerbase Studio web version. 
  - https://x.com/ImSh4yy/status/1864723257410167065
    - been using it with cloudflare d1 during dev, pretty good

- https://github.com/Microsoft/azuredatastudio /MIT/202412/ts
  - https://learn.microsoft.com/sql/azure-data-studio
  - Azure Data Studio is a data management and development tool with connectivity to popular cloud and on-premises databases.
  - Azure Data Studio supports Windows, macOS, and Linux, with immediate capability to connect to Azure SQL and SQL Server
  - Browse the extension library for more database support options including MySQL, PostgreSQL, and MongoDB.
  - Query Results Viewer with advanced data grid supporting large result sets, export to JSON\CSV\Excel, query plan and charting
  - Visual Data Editor that enables direct row insertion, update and deletion into tables
  - Management Dashboard supporting customizable widgets with drill-through actionable insights
  - Workspaces with full Git integration and Find In Files support to managing T-SQL script libraries
  - [What's Happening to Azure Data Studio? | Microsoft _202502](https://learn.microsoft.com/en-us/azure-data-studio/whats-happening-azure-data-studio)
    - Azure Data Studio officially retires on February 28, 2026. You should migrate to Visual Studio Code

- https://github.com/dbgate/dbgate /MIT/202402/ts/svelte
  - https://dbgate.org/
  - Database manager for MySQL, PostgreSQL, SQL Server, MongoDB, SQLite and others. 
  - Runs under Windows, Linux, Mac or as web application

- https://github.com/dolthub/dolt-workbench /apache2/202402/ts
  - https://hub.docker.com/r/dolthub/dolt-workbench
  - A modern, browser-based, open source SQL workbench for your MySQL and PostgreSQL compatible database with version control features when connected to Dolt.
  - Use Dolt to unlock powerful version control features.

- https://github.com/mlaanderson/database-js
  - Database-js implements a common, promise-based interface for SQL database access. 
  - Inspired by JDBC, it uses connection strings to identify the database driver. 

- https://github.com/slashbaseide/slashbase /ts/go
  - Collaborative in-browser database IDE for your team. 
  - Supports PostgreSQL & MongoDB.

 - https://github.com/dbeaver/cloudbeaver /java/ts
   - CloudBeaver is a web server which provides rich web interface. 
   - Server itself is a Java application, web part is written on TypeScript and React.

- https://github.com/egoist/querybase /AGPL/202501/ts
  - A simple and smart GUI client for PostgreSQL, MySQL, SQLite

- https://github.com/csanyipal/ajqvue /java/inactive
  - Ajqvue provides an easy to use Java based user interface frontend for viewing, adding, editing, or deleting entries in several mainstream databases.
  - Plugin Framework.
# schema
- https://github.com/schemaspy/schemaspy /LGPLv3/202402/java/js
  - http://schemaspy.org/
  - a database metadata analyzer. 
  - It helps your database administrators and developers visualize, navigate and understand your data model. 
  - SchemaSpy is a standalone application without GUI. Just download the latest JAR file
# testing
- https://gitlab.com/gitlab-org/database-team/gitlab-com-database-testing /202410/ruby
  - This project contains automation to test GitLab database migrations on the GitLab.com dataset. 
  - This is intended to be used before the migration code is being merged and deployed.
  - By using thin-clone technology provided by postgres.ai, the dataset used is very close to actual GitLab.com production. This allows us to analyze migrations and their behavior on the actual dataset, before merging code.
# more
- https://github.com/mlaanderson/database-js
  - Database-js implements a common, promise-based interface for SQL database access. 
  - Inspired by JDBC, it uses connection strings to identify the database driver.

- https://github.com/prsn/redux-persist-sqlite-storage
  - A redux-persist store adaptor that uses SQLite to persist store
