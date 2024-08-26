---
title: lib-db-app-blog-rewrite
tags: [blog, database, postgresql, rewrite, sqlite, toys]
created: 2022-11-27T19:19:22.406Z
modified: 2023-10-29T02:09:26.414Z
---

# lib-db-app-blog-rewrite

# guide

# db-toys
- https://github.com/plexidev/quick.db /MIT/202310/ts
  - https://quickdb.js.org/
  - http://docs.plexidev.org/
  - provide an easy way for beginners and people of all levels to access & store data in a low to medium volume environment.
  - All data is stored persistently via either better-sqlite3 or promise-mysql

- https://github.com/weinberg/SQLToy /js/NoDeps
  - https://github.com/weinberg/SQLToy/wiki
  - SQLToy is an in-memory SQL database written in Javascript. 
  - It is under 500 lines of code and has zero dependencies.
  - [Show HN: SQLToy – a tiny relational database for learning SQL via code | Hacker News_202111](https://news.ycombinator.com/item?id=29385432)

## db-rs

- https://github.com/yywe/yoursql /rust
  - Your SQL database for learning purpose
  - recently I'm learning the source code of `arrow-datafusion`. I'm trying to a tiny version of it by extracting the most essential parts. 
  - Although database books talked about query parser, query plan, query execution, etc, I find there is a large gap between theory and implementation
  - In the latest revision, I'm keep each dev branch named as "MILSTONEn-**"
# db-js

## ⤴️ [Creating a database from scratch with Node.js](https://dev.to/ciochetta/creating-a-database-from-scratch-with-node-js-4dmk)

- https://github.com/ciochetta/learndb /24Star/202101/js/mongodb
  - https://github.com/ciochetta/testing-luisdb
  - my first attempt at creating my own database from scratch.
  - I will not be doing a SQL database, instead, I will follow his steps but try to create a document database, like MongoDB
  - [LearnDB: Learn how to build a database | Hacker News_201811](https://news.ycombinator.com/item?id=18557260)
  - https://github.com/ciochetta/lql-parser
    - parser for my database project. 基于nearley moo
    - Moo is a highly-optimised tokenizer/lexer generator. Use it to tokenize your strings, before parsing 'em with a parser like nearley or whatever else you're into.
    - nearley is a streaming parser with support for catching errors gracefully and providing all parsings for ambiguous grammars. It is compatible with a variety of lexers (we recommend moo)

- p1: database的结构，存储层是map，更新基于command，主要逻辑在解析参数、执行cmd
- p2: 拆分cmd到单独文件，对create/insert/use命令支持持久化
- p3: parser支持array of objects，query支持返回指定字段
- p4: Luis Query Language, 支持 select 语句
- p5: LQL 支持 where、and 关键字
- p6: 支持 update、delete
- p7: 支持 bulk insert 语句
- p8: 拆分每个table为单独文件，开始实现btree索引
- p9: 创建索引、使用索引搜索
- p10: 索引优化，I am not considering the operation being tested by the where function so I am not locking the paths it would not make sense to search
- p11: refactor with clean code book

- pg-mem /1.1kStar/MIT/202211/ts
  - https://github.com/oguimbal/pg-mem
  - An in memory postgres DB instance for your unit tests
  - It works both in Node or in the browser.
  - https://github.com/oguimbal/pgsql-ast-parser
    - a Postgres SQL syntax parser. 基于nearley、moo实现
    - This parser does not support (yet) PL/pgSQL.
# db-non-js

## 🐭 [Build your own Database Index: part 1 _202312](https://dx13.co.uk/articles/2023/12/02/byo-index-pt1/)

- I’ve been working through creating a simple database-like index, to understand the concepts involved more concretely.
- I’ve been reading Database Internals as part of a book club for the last few weeks. One of the noticeable things in the first few chapters is that nearly everything is based on a storage layer with a relatively simple interface, that of a key-value store where both key and value are byte arrays.
  - The stores are ordered by key and are used for both storing primary data (eg, key = primary key; value = relational row data) and for indexes (key = indexed value; value = referenced row’s primary key). 
- Inspired by my reading, I decided to have a go at writing a simple index for JSON data.

- I wanted to concentrate on the index part, so used an existing key-value store. Any would do, but I decided to use PebbleDB which is the underlying store used by CockroachDB. I chose PebbleDB because it was written in Go. I was going to write my code in Go

- I wanted to create a generic JSON index. Generic, meaning that adding an arbitrary JSON document should index each field automatically, without having a pre-existing schema.

- 👥 
- https://twitter.com/ifesdjeen/status/1761109124924797103

- Working on an MPP type on Prem database for long, I had no idea about challenges faced by distributed systems. The whole LSM tree and B+ tree research etc. The book was an eye opener for me.

- It's crucial for engineers to build performant, scalable, and cost-optimized data systems. Your book clearly guides me through the 'what' and 'why' of my work. But when I write code it’s a different ball game , connecting the theory and implementation is the goal.

## 🦀 [Build your own SQLite, Part 1: Listing tables _202407](https://blog.sylver.dev/build-your-own-sqlite-part-1-listing-tables)

- https://github.com/geoffreycopin/rqlite /202408/rust

- As developers, we use databases all the time. But how do they work? In this series, we'll try to answer that question by building our own SQLite-compatible database from scratch.
  - Source code examples will be provided in Rust, but you are encouraged to follow along using your language of choice, as we won't be relying on many language-specific features or libraries.

- As an introduction, we'll implement the simplest version of the tables command, which lists the names of all the tables in a database

- 
- 

## 🐭 [Writing a SQL database from scratch in Go](https://notes.eatonphil.com/tags/databases.html)

- [1. SELECT, INSERT, CREATE and a REPL](https://notes.eatonphil.com/database-basics.html)
- [2. binary expressions and WHERE filters](https://notes.eatonphil.com/database-basics-expressions-and-where.html)
- [3. indexes](https://notes.eatonphil.com/database-basics-indexes.html)
- [4. a database/sql driver](https://notes.eatonphil.com/database-basics-a-database-sql-driver.html)

- https://github.com/eatonphil/gosql /go
  - An early PostgreSQL implementation in Go

### 👥🐭🔥 [Writing a SQL database from scratch in Go | Hacker News](https://news.ycombinator.com/item?id=22850817)

## 🧲 [Writing a sqlite clone from scratch in C](https://cstack.github.io/db_tutorial/)

- https://github.com/cstack/db_tutorial /c
  - Writing a sqlite clone from scratch in C
  - B-Tree Leaf Node Format
  - prepare_statement (our “SQL Compiler”) does not understand SQL right now. In fact, it only understands two words select and insert

- [Writing a SQLite Clone from Scratch in C (2022) | Hacker News_202305](https://news.ycombinator.com/item?id=35800109)
- [Writing a SQLite clone from scratch in C (2017) | Hacker News_202104](https://news.ycombinator.com/item?id=27731966)

### 👥🧲🔥 [Let’s Build a Simple Database (2017) | Hacker News_201904](https://news.ycombinator.com/item?id=19581721)

- 
- 
- 

### 👥🧲🔥 [Writing a SQLite clone from scratch in C | Hacker News_201709](https://news.ycombinator.com/item?id=15168467)

## 🧲 [Build Your Own Database From Scratch using cpp](https://build-your-own.org/database/)

- Part I: Simple KV Store
- Part II: Mini Relational DB
# sql

## 🔍🦀 [A SQL query compiler from scratch in Rust (step by step): Part one, the query plan representation _202312](https://andres.senac.es/posts/query-compiler-part-one/)

- https://github.com/asenac/rust-sql-playground /202307/rust
  - a SQL query compiler written in Rust mainly for learning and blogging purposes.
  - There is no SQL parser yet and its overall functionality is very limited, although the logical optimizer is getting real.
  - JsonSerializer utility can be used to dump the query plan in JSON format that can be rendered with any of the utilities in tools folder, using different graph rendering libraries.
# more
- 👥🔥[The “Build Your Own Database” book is finished | Hacker News_202304](https://news.ycombinator.com/item?id=35666598)
