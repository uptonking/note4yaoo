---
title: lib-db-rewrite-js
tags: [database, js, rewrite]
created: 2022-11-27T19:19:22.406Z
modified: 2022-11-27T19:20:02.987Z
---

# lib-db-rewrite-js

# guide

# [Creating a database from scratch with Node.js](https://dev.to/ciochetta/creating-a-database-from-scratch-with-node-js-4dmk)
- https://github.com/ciochetta/learndb /24Star/202101/js/mongodb
  - https://github.com/ciochetta/testing-luisdb
  - my first attempt at creating my own database from scratch.
  - I will not be doing a SQL database, instead, I will follow his steps but try to create a document database, like MongoDB
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

## [Writing a sqlite clone from scratch in C](https://cstack.github.io/db_tutorial/)

- https://github.com/cstack/db_tutorial
  - Writing a sqlite clone from scratch in C
  - B-Tree Leaf Node Format
  - prepare_statement (our “SQL Compiler”) does not understand SQL right now. In fact, it only understands two words select and insert
