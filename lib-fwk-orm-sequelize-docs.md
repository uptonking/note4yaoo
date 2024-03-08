---
title: lib-fwk-orm-sequelize-docs
tags: [docs, sequelize]
created: 2023-02-05T18:49:21.095Z
modified: 2023-02-05T18:49:31.166Z
---

# lib-fwk-orm-sequelize-docs

# guide

# blogs-dex-xp
- [Sequelize Data Types: a practical guide _202010](https://codewithhugo.com/sequelize-data-types-a-practical-guide/)
  - STRING A variable length string. Default length 255.
  - CHAR A fixed length string. Default length 255.
  - TEXT: An unlimited length text column
# cluster

## [Read Replication | Sequelize](https://sequelize.org/docs/v6/other-topics/read-replication/)

- Sequelize supports read replication, i.e. having multiple servers that you can connect to when you want to do a SELECT query. 
  - When you do read replication, you specify one or more servers to act as read replicas, 
  - and one server to act as the main writer, which handles all writes and updates and propagates them to the replicas 
  - (note that the actual replication process is not handled by Sequelize, but should be set up by database backend).

- [Load-balancing using sequelize _201702](https://github.com/sequelize/sequelize/issues/7176)
  - Is load balancing possible using sequelize? I want to be able to separate the read/write queries and direct the read queries to the read-only database.

- Load balancing is not in our scope, but we do offer replication
  - You can define two database config in replication.read and replication.write options for Sequelize constructor config. You can define any number of read replicas (config accept array). All your read queries will be sent to read replicas by round robin scheduling technique.
- ORM should never be in charge of populating read/write replicas, it should be managed by your db service provider. Have you used replicas before?
# docs-v7

- 
- 
- 
- 

## upgrade to v7 from v6

- Main project renamed to `@sequelize/core` from `sequelize`.
  - node v14+
  - Blocking access to /lib
- CLS Transactions are now enabled by default.
  - Sequelize's CLS implementation has been migrated to use Node's built-in `AsyncLocalStorage`.

- Data Types have been completely rewritten to be more TypeScript-friendly, and make them more powerful.

- Instance methods cannot be used without primary key.

- Removed string-based operators
  - You need to use the Op object instead
# docs-v6
- A model is an abstraction that represents a table in your database. 
  - In Sequelize, it is a class that extends Model.
  - The model tells Sequelize several things about the entity it represents, such as the name of the table in the database and which columns it has (and their data types).
  - A model in Sequelize has a name. This name does not have to be the same name of the table it represents in the database. 
- After a model is defined, it is available within `sequelize.models` by its model name.
- A model can be synchronized with the database by calling `model.sync(options)`.
- By default, Sequelize automatically adds the fields `createdAt` and `updatedAt` to every model
  - This is done in the Sequelize level (i.e. not done with SQL triggers). 

- Sequelize supports adding indexes to the model definition which will be created on `sequelize.sync()`.

- An instance of the model class represents one object from that model (which maps to one row of the table in the database). 
  - This way, model instances are DAOs.
- Although a model is a class, you should not create instances by using the new operator directly. 
  - Instead, the `build` method should be used

- Sequelize provides the `create` method, which combines the `build` and `save` methods shown above into a single method
- The `save` method is optimized internally to only update fields that really changed. 
  - This means that if you don't change anything and call save, Sequelize will know that the save is superfluous and do nothing, i.e., no query will be generated (it will still return a Promise, but it will resolve immediately).

- In order to increment/decrement values of an instance without running into concurrency issues, Sequelize provides the increment and decrement instance methods.

- By default, Sequelize assumes that the default value of a column is `NULL`. 

- INSERT
  - Model.create() 

- SELECT
  - `const users = await User.findAll();` SELECT *
  - `Model.findAll({ attributes: ['foo', 'bar'] });` SELECT fields

- WHERE
  - Post.findAll({ where: { authorId: 2 } }); 

- By default, the results of all finder methods are instances of the model class (as opposed to being just plain JavaScript objects). 
  - This means that after the database returns the results, Sequelize automatically wraps everything in proper instance objects. 

- Sequelize allows you to define custom getters and setters for the attributes of your models.
  - Sequelize also allows you to specify the so-called virtual attributes, which are attributes on the Sequelize Model that doesn't really exist in the underlying SQL table, but instead are populated automatically by Sequelize. 
  - They are very useful to create custom attributes which also could simplify your code

- Virtual fields are fields that Sequelize populates under the hood, but in reality they don't even exist in the database.

- Sequelize supports the standard associations: One-To-One, One-To-Many and Many-To-Many.

- One-To-One relationships
  - We know that in a relational database, this will be done by establishing a foreign key in one of the tables.
  - question is: in which table do we want this foreign key to be?
  - In principle, both options are a valid way to establish a One-To-One relationship between Foo and Bar. 

- A paranoid table is one that, when told to delete a record, it will not truly delete it. 
  - Instead, a special column called `deletedAt` will have its value set to the timestamp of that deletion request.
  - This means that paranoid tables perform a soft-deletion of records, instead of a hard-deletion.
- Every query performed by Sequelize will automatically ignore soft-deleted records (except raw queries, of course).

- eager Loading is the act of querying data of several models at once (one 'main' model and one or more associated models). 
  - At the SQL level, this is a query with one or more joins.
- eager loading is mainly done by using the `include` option on a model finder query (such as `findOne/findAll`, etc).

- An instance can be created with nested association in one step, provided all elements are new.
- In contrast, performing updates and deletions involving nested objects is currently not possible. 
  - For that, you will have to perform each separate action explicitly.

- If you're connecting to the database from a single process, you should create only one Sequelize instance. 
  - Sequelize will set up a connection pool on initialization. 
  - This connection pool can be configured through the constructor's options parameter (using `options.pool`)
- If you're connecting to the database from multiple processes, you'll have to create one instance per process, but each instance should have a maximum connection pool size of such that the total maximum size is respected. 
  - For example, if you want a max connection pool size of 90 and you have three processes, the Sequelize instance of each process should have a max connection pool size of 30.

- Hooks (also known as lifecycle events), are functions which are called before and after calls in sequelize are executed. 
  - For example, if you want to always set a value on a model before saving it, you can add a beforeUpdate hook.
- You can't use hooks with instances. 
  - Hooks are used with models.

- Sequelize has built-in support for optimistic locking through a model instance version count.
  - Optimistic locking is disabled by default and can be enabled by setting the version property to true in a specific model definition or global model configuration.
- Optimistic locking allows concurrent access to model records for edits and prevents conflicts from overwriting data. 
  - It does this by checking whether another process has made changes to a record since it was read and throws an OptimisticLockError when a conflict is detected.

- An instance of Sequelize uses something called Query Interface to communicate to the database in a dialect-agnostic way. 

- Scopes are used to help you reuse code. 
  - You can define commonly used queries, specifying options such as where, include, limit, etc.

- sub queries
  - how can we achieve that with more help from Sequelize, without having to write the whole raw query by hand?
  - The answer: by combining the attributes option of the finder methods (such as findAll) with the sequelize.literal utility function, that allows you to directly insert arbitrary content into the query without any automatic escaping.
  - This means that Sequelize will help you with the main, larger query, but you will still have to write that sub-query by yourself

- Sequelize does not use transactions by default. 
  - However, for production-ready usage of Sequelize, you should definitely configure Sequelize to use transactions.
- Sequelize supports two ways of using transactions:
- Unmanaged transactions: 
  - Committing and rolling back the transaction should be done manually by the user (by calling the appropriate Sequelize methods).
- Managed transactions: 
  - Sequelize will automatically rollback the transaction if any error is thrown, or commit the transaction otherwise. 
  - Also, if CLS (Continuation Local Storage) is enabled, all queries within the transaction callback will automatically receive the transaction object.

## [Associations | Sequelize](https://sequelize.org/docs/v6/core-concepts/assocs/)

- Lazy Loading refers to the technique of fetching the associated data only when you really want it; 
  - Eager Loading, on the other hand, refers to the technique of fetching everything at once, since the beginning, with a larger query.
  - Eager Loading is performed in Sequelize by using the `include` option

- The `save()` instance method is not aware of associations. 
  - In other words, if you change a value from a child object that was eager loaded along a parent object, calling `save()` on the parent will completely ignore the change that happened on the child.

- `getShip()` instance method used above is one of the methods Sequelize automatically adds to `Captain` instances.

- Defining an Alias is more powerful than simply specifying a custom name for the foreign key.
- Aliases are especially useful when you need to define two different associations between the same models
  - it is possible to define multiple associations between the same models. You just have to define different aliases for them

- When an association is defined between two models, the instances of those models gain special methods to interact with their associated counterparts.

- Why associations are defined in pairs?
  - When a Sequelize association is defined between two models, only the source model knows about it.

- Sequelize allows you to define an association that uses another field, instead of the primary key field, to establish the association.
  - This other field must have a unique constraint on it (otherwise, it wouldn't make sense).
# more
