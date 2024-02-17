---
title: lib-fwk-orm-typeorm-docs
tags: [docs, typeorm]
created: 2023-01-20T18:43:20.588Z
modified: 2023-01-20T18:44:00.791Z
---

# lib-fwk-orm-typeorm-docs

# guide
- resources
# overview
- typeorm /30.1kStar/MIT/202301/ts
  - https://github.com/typeorm/typeorm
  - http://typeorm.io/
  - 依赖date-fns, reflect-metadata, buffer

- TypeORM is an ORM that can run in NodeJS, Browser, Cordova, PhoneGap, Ionic, React Native, NativeScript, Expo, and Electron platforms
  - Supports MySQL, PostgreSQL, MariaDB, SQLite, MS SQL Server, Oracle, SAP Hana, sql.js.
  - Supports MongoDB NoSQL database.
- ✨ TypeORM supports both Active Record and Data Mapper patterns
- TypeORM is highly influenced by other ORMs, such as Hibernate, Doctrine and Entity Framework.
# docs

# [Active Record vs Data Mapper | TypeORM](https://typeorm.io/active-record-data-mapper)
- Simply said, the Active Record pattern is an approach to access your database within your models.
  - you define all your query methods inside the model itself, and you save, remove, and load objects using model methods.
  - All active-record entities must extend the BaseEntity class, which provides methods to work with the entity.
  - BaseEntity has most of the methods of the standard Repository. 

- Simply said, data mapper is an approach to access your database within repositories instead of models. 
  - you define all your query methods in separate classes called "repositories", and you save, remove, and load objects using repositories. 
  - In data mapper your entities are very dumb - they just define their properties and may have some "dummy" methods.

- Both strategies have their own cons and pros.
- One thing we should always keep in mind with software development is how we are going to maintain our applications. 
- The Data Mapper approach helps with maintainability, which is more effective in larger apps. 
- The Active Record approach helps keep things simple which works well in smaller apps. 
  - And simplicity is always a key to better maintainability.
# DataSource/Connection
- TypeORM's DataSource holds your database connection settings and establishes initial database connection or connection pool depending on the RDBMS you use.
- Generally, you call `initialize` method of the DataSource instance on application bootstrap, and `destroy` it after you completely finished working with the database
  - In practice, if you are building a backend for your site and your backend server always stays running - you never `destroy` a DataSource.

- Once you set your DataSource, you can use it anywhere in your app

- To use multiple data sources connected to different databases, simply create multiple DataSource instances
# Entity/Table
- Entity is a class that maps to a database table (or collection when using MongoDB).
- Basic entities consist of columns and relations. 
  - Each entity MUST have a primary column (or `ObjectId` column if are using MongoDB).
- When using an entity constructor its arguments must be optional. 
  - Since ORM creates instances of entity classes when loading from the database, therefore it is not aware of your constructor arguments.

- Since database tables consist of columns your entities must consist of columns too. 
  - Each entity class property you marked with @Column will be mapped to a database table column.
- MySQL, PostgreSQL and CockroachDB all support spatial columns. 
  - MySQL's TypeORM support exposes (and expects) geometries to be provided as well-known text (WKT), so geometry columns should be tagged with the `string` type.
  - TypeORM's PostgreSQL and CockroachDB support uses GeoJSON as an interchange format, so geometry columns should be tagged either as object or Geometry (or subclasses, e.g. Point) after importing geojson types or using TypeORM built in GeoJSON types.

- TypeORM supports all of the most commonly used database-supported column types. 
  - Column types are database-type specific - this provides more flexibility on how your database schema will look like.

- Embedded column is a column which accepts a class with its own columns and merges those columns into the current entity's database table. 

- You can reduce duplication in your code by using entity inheritance patterns.
  - All columns (relations, embeds, etc.) from parent entities (parent can extend other entity as well) will be inherited and created in final entities.
- Single table inheritance is a pattern when you have multiple classes with their own properties, but in the database they are stored in the same table.
- There is an amazing way to reduce duplication in your app (using composition over inheritance) by using embedded columns.

- [TypeORM Entity Inheritance ManyToOne Relationship - Stack Overflow](https://stackoverflow.com/questions/54932600)
  - I suggest using composition over inheritance with an Embedded Entity
  - An embedded column is a column which accepts a class with its own columns and merges those columns into the current entity's database table.
  - You can use as many columns (or relations) in embedded classes as you need. You even can have nested embedded columns inside embedded classes.

- https://twitter.com/pleerock/status/1029076645934710784
  - TypeORM has its own simple and powerful features like embeds which I strongly recommend for everyone who is going to use table inheritance - you can simplify your database, models and code if you use composition over inheritance for reuse, and thats where embedded feature comes
- Take ActiveRecord's multi table inheritance mechanism for example, or as we call it "Polymorphism", very easy to implement in @rails , in TypeOrm, first of all, it didn't exist until VERY recently, so it's not as stable and complete, and on top of that, hard to implement.
  - Regarding to "multi table inheritance mechanism". First, it exist at least few years, and it was deprecated by me, because its a bad feature for TypeORM. 
- Aslan wants table inheritance which in classic oop languages usually means standard class inheritance with some hacks applied. But in JavaScript for example, we have a powerful Object Spread which can work like multiple table inheritance in context of table schema definition.
# Relations
- Relations helps you to work with related entities easily. 
- There are several types of relations:
  one-to-one using @OneToOne
  many-to-one using @ManyToOne
  one-to-many using @OneToMany
  many-to-many using @ManyToMany

- Cascades may seem like a good and easy way to work with relations, but they may also bring bugs and security issues when some undesired object is being saved into the database. 
  - Also, they provide a less explicit way of saving new objects into the database.

- Self-referencing relations are relations which have a relation to themselves. 
  - This is useful when you are storing entities in a tree-like structures. 
  - Also, "adjacency list" pattern is implemented using self-referenced relations. 
  - Basically self-referencing relations are just regular relations that targets entity itself.
# Entity Manager and Repository
- Using EntityManager you can manage (insert, update, delete, load, etc.) any entity.
  - EntityManager is just like a collection of all entity repositories in a single place.
  - You can access the entity manager via DataSource. 

- `Repository` is just like `EntityManager`, but its operations are limited to a concrete entity. 
  - You can access the repository via EntityManager.
# Query Builder
- QueryBuilder allows you to build SQL queries using elegant and convenient syntax, execute them and get automatically transformed entities.
- When using the QueryBuilder, you need to provide unique parameters in your WHERE expressions.
- You can cache results selected by these QueryBuilder methods: getMany, getOne, getRawMany, getRawOne and getCount.
# docs-pieces
- Transactions are created using DataSource or EntityManager. 

- You can create a database index for a specific column by using @Index on a column you want to make an index. 
  - You can create indices for any columns of your entity.

- Any of your entities can have methods with custom logic that listen to specific entity events. 
  - Do not make any database calls within a listener, opt for subscribers instead.
# more
