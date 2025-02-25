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

- ## 

- ## 🚨✨ [[RFC] Decorators · sequelize/sequelize _202112](https://github.com/sequelize/sequelize/issues/14298)
- One of the main issues I have with sequelize-typescript is recursive imports. When I wanted to upgrade NextJs on my project I ran into tons of problems because recursive imports suddenly become errors instead of "just" warnings. 

- Everything described in here is implemented now _202306

- ## 💡 [Delete password from sequelize model - Stack Overflow](https://stackoverflow.com/questions/71808210/delete-password-from-sequelize-model)
  - `delete user.dataValues.password` where does dataValues ​​come from
- it is same to get field from sequelize with `user.get("field_name")` , `user.getDataValue("field_name")` and `user.dataValues.field_name` . 

- I don't recommend to delete service props in Sequelize model (dataValues prop holds metadata about all fields of a certain model) because it can lead to incorrect work of this model. 
  - Instead of deleting the password field form dataValues you need to delete it from a plain object that represents a certain model instance
  - `const { password, ...plainUser } = user.get({ plain: true })`

- ## 💡 [Sequelize Update with Object - Stack Overflow](https://stackoverflow.com/questions/63261248/sequelize-update-with-object)
  - I have a code using sequelize to update one record and then return this updated record
  - It is working but I have to separate into two query statements. Is there a way I can mix them together?

- no. when you update most sql dbs will only return provide only number of affected rows. Even if sequelize provide an interface through it, the implementation will not be difference than what you did logically 

- The `returning` option of `Model.update` still only supports PostgreSQL for sequelize v6.

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
# discuss-news
- ## 

- ## 

- ## [Status of merge with sequelize-typescript _202211](https://github.com/sequelize/sequelize/issues/15334)
- /wip/202403

# discuss-scaling-k8s
- ## 

- ## [SequelizeConnectionAcquireTimeoutError randomly DB connections pool error _201910](https://github.com/sequelize/sequelize/issues/10858)
- It's very important to tell that I have different apps that run on the same K8s cluster with the same DB, same auth, and it's not crashing.
  - My bad, eventually the number of connections was not read correctly from env variables and acquire timeout was too low. Hope it will help anyone else who faces this issue.

- I'm also using the default pooling config with PostgreSQL, but I'm managing my transactions manually. If you're letting Sequelize handle the transactions, it might be due to a bug in Sequelize. A good starting point for troubleshooting the issue would be switching to manual transaction handling and seeing if the issue still occurs.

- make sure all TRANSACTIONS contain a ROLLBACK or COMMIT

- ## [Is there a better way than this to handle sequelize seeding and migration in a production grade multi stage dockerfile? : r/node _202304](https://www.reddit.com/r/node/comments/12lp1pv/is_there_a_better_way_than_this_to_handle/)
- it should be part of your deployment. If it successfully deploys run the migration. Your seeds & migrations would run everytime the docker builds. Which is not ideal as you can have start issues... and you already migrated your DB. This could also kick off parallel migrations while you scale on a cloud provider; luckily they are done in transactions so they can be rolled back for applying the changes. Ideally... you would deploy using a CI; after the deployment step you would have a migration step.

- Usual pattern is to create a container just for seeding . That way when you deploy the app in prod you can add it as a proper init container
# discuss
- ## 

- ## 

- ## [SQLite Array type · Issue · sequelize/sequelize](https://github.com/sequelize/sequelize/issues/9209)
- 202204: we don't want to implement `DataTypes.ARRAY` for dialects that do not actually support arrays. 
  - Use `JSON` if you want to use JSON

- [Sequelize : SQLITE_ERROR: near "[]": syntax error - Stack Overflow](https://stackoverflow.com/questions/62752636/sequelize-sqlite-error-near-syntax-error)
  - DataTypes. ARRAY(DataTypes. DECIMAL). Only available in postgres.
  - So, you cannot use the ARRAY datatype with SQLite3, only with PostgreSQL as your backend.

- ## 💡 [Sequelize, convert entity to plain object - Stack Overflow](https://stackoverflow.com/questions/21961818/sequelize-convert-entity-to-plain-object)
- Using `.get()` won't convert included associations, use `.get({ plain: true })` instead.

- ## [Get only dataValues from Sequelize ORM - Stack Overflow](https://stackoverflow.com/questions/46380563/get-only-datavalues-from-sequelize-orm)
- const sequelize = new Sequelize('connectionUri', {   define: {     raw: true    } }); 
  - Please not this does not work with eager loading nested entities.

- ## [Sequelize.sync({ force: true }) is too dangerous to live _201412](https://github.com/sequelize/sequelize/issues/2670)
- In order to ensure a 1:1 parity between ORM model definitions and the underlying schema, the user must clutter their model definitions with attribute hints to help the ORM understand how to build the schema. This is a task for a migrator, not an ORM. 
  - If we look at ActiveRecord or Knex/Bookshelf, we see an entirely separate system at play for schema-building and model-building.
