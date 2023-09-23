---
title: lib-db-datalog-blog
tags: [blog, database, datalog]
created: 2023-09-16T17:27:45.505Z
modified: 2023-09-16T17:27:59.262Z
---

# lib-db-datalog-blog

# guide

# blog

## 📝 [Datalog in Javascript](https://www.instantdb.com/essays/datalogjs)

- Datalog is a logic-based query language that’s as powerful as SQL. 
- SQL databases store data in different tables
- In Datalog databases, there are no tables. Or really everything is just stored in one table, the **triple table**
- A `triple` is a row with an `id`/`attribute`/`value`. 
  - Triples have a curious property; with just these three columns, they can describe any kind of information!

- SQL has roots in relational algebra. You give the query engine a combination of clauses and statements
- Datalog databases rely on pattern matching. We create “patterns” that match against triples. 
- In Datalog, we still rely on pattern matching for join. 
  - The trick is to match multiple patterns

## 👥 [Datalog in JavaScript | Hacker News_202204](https://news.ycombinator.com/item?id=31154039)

- It’s fascinating to see so many different parties converging on Datalog for reactive apps & UI.
  - Roam Research and its clones Athens, Logseq, use Datascript/ClojureScript
  - differential-datalog isn’t an end-to-end system, but is highly optimized for quick reactivity
  - Datalog UI is a Typescript port of some of differential-datalog’s ideas
- I think **an under appreciated aspect of Datalog is as a pure specification language for relationships**. 
  - Schema languages like GraphQL specify a relation between types exists, but not how it is computed. 
  - Prisma and other ORM DSLs like ActiveRecord do a better job specifying how to compute a relation from SQL tables, but support only a few strict computation types that can be modeled using SQL JOIN on columns.
- Datalog lets you purely specify arbitrarily complex logical relationships between data types. 
  - Even if you were to only use Datalog as a rules engine at test time, it could still be quite powerful for validating logic implemented in different languages on the same data model, to say keep your Typescript, Kotlin and Swift logic in sync.

- It is really great that people are discovering the utility of triplestores through their ubiquity in the Clojure ecosystem (e.g. Datomic and its many clones).
  - I do feel saddened that few seem to realise that the fundamental idea actually comes from **RDF** (i.e. the semantic web) and that Datomic's Datalog dialect is actually very similar to **SPARQL**. 
  - **Datomic's primary innovation is the immutability/time travel feature**, not the fact that is uses triples and works like a graph database. 
  - If you find triplestores fascinating I implore(恳求；哀求) you to explore the semantic web stack too.

- The most important thing that datomic and friends brought, is usability and pragmatism.
  - While RDF has an elegant core, it is bogged down(陷入泥沼, 陷入困境) by the complexity of the web and ancillary(辅助的) technologies.
  - XML Types, cURIes, OWL, the different encodings.
  - They all make RDF a nightmare to work with, and to implement in practice.
  - The is simply no good RDF software ecosystem, yet the Spec ecosystem continues to grow (wildly out of control).
- On a technical note, SPARQL and Datomic Datalog are very different beasts.
  - The former is conjunctive queries with optionals and regular path expressions (i.e. Conjunctive queries + XPath + nonmonotonic defaults) while the latter is recursive conjunctive queries (i.e. Datalog).
- there are other GraphDBs with additional properties and custom query languages such as Neo4j and its query language Cypher.
  - I Find that Neo4j's property graph is more intuitive to model data with than a plain RDF store and Cypher has some advantages over SPARQL as well

- Rich often mentions the RDF heritage. I think the separation of reads and writes through the transactor is also a significant innovation.

- In Datalog databases, there are no tables. Or really everything is just stored in one table, the triple table
  - The author conflates(合并，混合) Datomic family databases which use triples as their data model and datalog as their query engine, with datalog the pure prolog subset / conjunctive query + recursion fragment.
  - Not a great start for a novel DB product

- How does datalog the pure prolog subset store its data?
  - SWI Prolog's RDF store is implemented as a C extension. Apparently, it uses skip-lists for indexes.
- Datalog is a query language similar to SQL. It doesn't store data. Some database would store data however it likes then provide a datalog query interface.
- Datalog also lets you define facts and rules, in addition to posting queries. 
  - A key attraction of Datalog is that the same simple and very uniform syntax is used in all cases. 
  - All these cases are special cases of a single unifying language element called Horn clauses, which are clauses with at most one positive literal: 
    - **Queries** have no positive literal, 
    - **rules** have exactly one positive literal and at least one negative literal, 
    - and **facts** consist of a single positive literal.
# roam-research

## [【译】Roam Research 自定义组件 —— 跟 {{roam/render}} 来一次亲密接触_202103](https://blog.jimmylv.info/2021-03-10-a-closer-look-at-roamrender-zh-translation/)

- [A closer look at {{roam/render}}_202102](https://www.zsolt.blog/2021/02/a-closer-look-at-roamrender.html)
# more
- [MiniLitelog: Easy Breezy SQLite Datalog](https://www.philipzucker.com/tiny-sqlite-datalog/)
  - This blog post about is about a very lightweight encoding of datalog to SQLite.

- [（三）Datalog和程序分析 - 知乎](https://zhuanlan.zhihu.com/p/581748024)
  - 基本语法简介
