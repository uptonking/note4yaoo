---
title: lib-fwk-orm-sequelize-community
tags: [community, sequelize]
created: 2023-02-05T18:49:33.768Z
modified: 2023-02-05T18:49:43.540Z
---

# lib-fwk-orm-sequelize-community

# guide

# discuss-stars
- ## 

- ## 

- ## [Table partitioning](https://github.com/sequelize/sequelize/issues/7673)

- > 针对pg的方案有pr，但未合并

- as far as I know none of the NodeJS ORMs show a proper implementation of partitioning and still require more steps to implement it
  - I like to take this since I personally always work with the databases partition stuff, each databases should have different what-to partitioned
  - the complex part is what the partition types is used for partitioning
  - we can implement this feature in Sequelize for every dialects.
  - partitionBy with `sequelize.literal` looks good, but since there is dialects which require more steps to finish a partitioned table, I think we need to create a new interface.

- ## ActiveRecord should be studied more. 
- https://twitter.com/stopachka/status/1715018851249745946
  - It gets a bad rep, mainly because of how meta-programming works in Ruby, but that doesn't detract from how elegant the resulting DSL is.
  - I really like how ActiveRecord does a) validations and b) callbacks

- ## 🆚️ [Why do most ORMs use ActiveRecord instead of DataMapper? - Quora](https://www.quora.com/Why-do-most-ORMs-use-ActiveRecord-instead-of-DataMapper)
- While DataMapper is much better and explicit in implementation detail not only in theory but in practice too, active record pattern is much easier when you need rapid application development. This is why most popular frameworks use active record pattern ORM.
  - But it is also possible to implement active record like declarative ORM on top of datamapper pattern. 
  - For example groovy ob grails implemented their active record pattern ORM on top of java Hibernate which strictly follow datamapper patterns.
  - So in practice it is also possible to use datamapper pattern internally for better architectural abstraction and declarative orm on top of that for rapid development with the option to mix the orm and low level api’s while necessary.

- In my opinion, the ActiveRecord pattern is simply easier for most people who are familiar with Object-Oriented Programming 
  - With ActiveRecord-based ORMs, you basically pretend that database rows are standard objects and manipulate them as such. The persistence of those objects in a database is kind of an automatic or "magical" implementation detail. This is easy and intuitive as long as it works.
  - With DataMapper-based ORMs, the programmer has a lot more responsibility and control over how objects and database rows are mapped to each other
- The Wikipedia article on `SQLAlchemy` gives a really nice succinct summary of why a direct mapping of database rows to OOP objects may not be satisfactory:
  - > SQLAlchemy's philosophy is that SQL databases behave less and less like object collections the more size and performance start to matter, ...
# discuss-issues-not-yet
- ## 

- ## 

- ## [Feature Request: Ability to get raw sql query _201409](https://github.com/sequelize/sequelize/issues/2325)
- I think we should consider reworking `QueryGenerator` to fully make it a public API. Right now, it's too much of an internal API.

- This seems like another potential use for what I mentioned here - could also be a huge opportunity to start migrating our codebase to TS. I 110% agree that `Model` should just be calling `QueryInterface`, great idea.

- ## [No query builder? Can we fix that? _201301](https://github.com/sequelize/sequelize/issues/394)
  - I was somewhat surprised (and dismayed) by the fact that Sequelize doesn't have a query builder. 
  - This means that in order to write generic selects with optional ands, or and ins, you have to start gluing strings together
  - When you have array of conditions (e.g. filtering) or more complicated queries, you risk a mental breakdown

- ORMs like `TypeORM` also provides a query builder.

- No one is working on it. Requires a lot of work obviously, a full API design and then implementation with a good test suite. Ideally i'd just like to integrate `mongo-sql` but it only supports PG atm.

```JS
sequelize.getQueryInterface().QueryGenerator.getWhereConditions({ a: 1, b: 2, c: 3 })
// "a" = 1 AND "b" = 2 AND "c" = 3
```

- knex would be the ideal solution; it is also used in Adonis ORM etc

- this is why Laravel still relevant in 2023
# discuss
- ## 

- ## 

- ## 

- ## 

- ## [Get only dataValues from Sequelize ORM - Stack Overflow](https://stackoverflow.com/questions/46380563/get-only-datavalues-from-sequelize-orm)
- const sequelize = new Sequelize('connectionUri', {   define: {     raw: true    } }); 
  - Please not this does not work with eager loading nested entities.

- ## [Sequelize.sync({ force: true }) is too dangerous to live _201412](https://github.com/sequelize/sequelize/issues/2670)
- In order to ensure a 1:1 parity between ORM model definitions and the underlying schema, the user must clutter their model definitions with attribute hints to help the ORM understand how to build the schema. This is a task for a migrator, not an ORM. 
  - If we look at ActiveRecord or Knex/Bookshelf, we see an entirely separate system at play for schema-building and model-building.
