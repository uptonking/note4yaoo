---
title: lib-db-datalog-dev
tags: [database, datalog]
created: 2023-09-16T17:26:48.256Z
modified: 2023-09-16T17:27:17.186Z
---

# lib-db-datalog-dev

# guide

- features
  - implicit join
  - Declarative and pattern matching make it elegant to read

- pros
  - express recursive relationships
  - **reusable rules for query** (easier to migrate)

- cons

- datalog vs sql
  - easier to express recursive relationships in Datalog compared to SQL
  - with the datalog (as well as prolog) syntax, is you are able to build a vocabulary of re-usable queries

- choices
  - 前后端的数据模型有必要保持一样吗，传统架构都是分层的dao/dto/vo

- alternatives
  - sql
  - SPARQL
  - **graphql**
  - graph query languages: Cypher, Gremlin, nGQL
  - more: Apache AGE graph extension

- resources
# dev
- dev-to
  - excel-sql
  - excel-datalog

## [Datalog programming language - Wikipedia](https://en.wikipedia.org/wiki/Datalog)

- Datalog is a declarative logic programming language. 
  - While it is syntactically a subset of Prolog, Datalog generally uses a bottom-up rather than top-down evaluation model. 
  - It is often used as a query language for deductive databases.
# more
