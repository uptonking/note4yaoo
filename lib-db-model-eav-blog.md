---
title: lib-db-model-eav-blog
tags: [blog, database, entity-attribute-value]
created: 2023-09-25T17:51:20.050Z
modified: 2023-09-25T17:52:11.778Z
---

# lib-db-model-eav-blog

# guide

# blogs

## [entity-attribute-value design in PostgreSQL - don't do it!_202111](https://www.cybertec-postgresql.com/en/entity-attribute-value-eav-design-in-postgresql-dont-do-it/)

- What is entity-attribute-value design?
- The idea is not to create a table for each entity in the application. Rather, you store each attribute as a separate entry in an attribute table
- There are several variations of the basic theme, among them:
  - omit the objects table
  - add additional tables that define “object types”, so that each type can only have certain attributes

- Why would anybody consider an entity-attribute-value design?
- The principal argument I hear in support of the EAV design is flexibility. You can create new entity types without having to create a database table. Taken to the extreme, each entity can have different attributes.
- I suspect that another reason for people to consider such a data model is that they are more familiar with key-value stores than with relational databases.

- Performance considerations of entity-attribute-value design
- In my opinion, EAV database design is the worst possible design when it comes to performance.

- But we need an entity-attribute-value design for flexibility!
- Relational data models are not famous for their flexibility. After all, that is the drive behind the NoSQL movement. However, there are good ways to deal with variable entities.
- 👉🏻 Creating tables on the fly
  - Nothing keeps you from running statements like `CREATE TABLE` and `CREATE INDEX` from your application.
  - Creating tables on the fly will only work well if the set of attributes for each entity is well-defined. If that is not the case, we need a different approach.
- 👉🏻 Using JSON for a flexible data model
  - PostgreSQL has extensive JSON support that can be used to model entities with a variable number of attributes.
  - you model the important and frequently occurring attributes as normal table columns. Then you add an additional column of type jsonb with a GIN index on it. This column contains the “rare attributes” of the entity as key-value pairs.

- Avoid entity-attribute-value designs in your relational database. EAV causes bad performance, and there are other ways to have a flexible data model in PostgreSQL.

- I've encountered this approach (luckily) only once, and it was horrible.
  - it appears to work great if you have a bunch of "objects", but quickly drives the database (and the application) unresponsive as soon as you load some real data into it.
- JSON(B) offers a great way to implement a part of schema-free entities easing also the application deployment against other customers (since you don't need a way to deploy schema changes because, well, there are not!).

## [Entity-Attribute-Value Implementation - MariaDB Knowledge Base](https://mariadb.com/kb/en/entity-attribute-value-implementation/)

- Open-ended set of "attributes" (key=value) for each "entity". That is, the list of attributes is not known at development time, and will grow in the future. (This makes one column per attribute impractical.)
- It goes by various names
  - EAV -- Entity - Attribute - Value
  - key-value
  - RDF -- This is a flavor of EAV
  - MariaDB has dynamic columns that look something like the solution below, with the added advantage of being able to index the columns otherwise hidden in the blob. (There are caveats.)
  - MySQL 5.7 Has JSON datatype, plus functions to access parts
  - MongoDB, CouchDB -- and others -- Not SQL-based.

- Decide which columns need to be searched/sorted by SQL queries. No, you don't need all the columns to be searchable or sortable. Certain columns are frequently used for selection; identify these. You probably won't use all of them in all queries, but you will use some of them in every query.
  - The solution uses one table for all the EAV stuff. The columns include the searchable fields plus one BLOB. Searchable fields are declared appropriately (INT, TIMESTAMP, etc). The BLOB contains JSON-encoding of all the extra fields.

- 
- 

## [Magento Entity Attribute Value (EAV) Model - Magento Tutorial_201709](https://blog.magestore.com/entity-attribute-value-in-magento/)

## [Entity-Attribute-Value Model | Dremio](https://www.dremio.com/wiki/entity-attribute-value-model/)

- One of the key features of the EAV model is its ability to handle dynamic and sparse data. It allows for the addition of new attributes without altering the underlying schema, making it highly adaptable to evolving data requirements.
- In the EAV model, data is stored in a set of tables: one table to hold the entities, one table to store the attributes, and one table to store the attribute values. These tables are linked through primary and foreign keys, establishing relationships between the entities, attributes, and values.
  - To retrieve data, a query must join these tables together, filtering by the desired entity and attribute. This flexibility allows for complex and customized queries, enabling users to extract specific information from the database.

## [Entity-Attribute-Value (EAV) database model · Coding Notes](https://pbedn.github.io/post/2020-05-25-entity-attribute-value/)

- EAV database model, as well known as ‘open schema’ or ‘vertical model’, describe entities where the number of all attributes in unknown and potentially significant, however number of attributes for a particular entity is small.
- Why vertical model? Because the table usually consists of a few columns, but a large number of rows. Another say - “long and skinny
- The great thing here is that, when we need to describe new information about customer (entity) or product, we do not need to alter the table, by adding new columns. There is as well no duplicated information. When we want to insert a new attribute, we do it directly to attribute and value tables.
- One of the cons is that it is costly for performance, as it requires at least two queries with many joins (one to get all attributes, values and entities, and second to assemble them in a usable format). 
  - Another problem is that the data stored in the value table can have different types. To fix that Magento decided to split value table into additional value tables, one for a specific value type, for example, one for varchar, one for datetime etc. However, that makes a lot of additional queries to execute. And here Magento proposed to have another table called flat table, where it stores all data, and values could be taken by using a single select.

- EAV Advantages
  - Flexible mechanism, supports multiple projects, broad community.
  - Little consideration of DB structure at the initial design stage.
  - Database schema does not change, when model changes, allowing updates through for example web UI.

- EAV Disadvantages
  - Complexity - a high learning curve for new developers.
  - Loose data validation that needs to be implemented later in the code.
  - Performance - multiple join queries (though good cache system can improve it).
  - Does not provide a way for grouping of related entity types.
  - Does not provide a mechanism to create relationships between entities of different subtypes.
  - Developers have to recreate relational database technology (graphical system tools, data security, incremental back-up and restore, exception handling, etc.).
  - Often you cannot just use ORM, but write complex SQL queries.

- EAV modelling is an example of space (and schema maintenance) versus CPU-time tradeoff. So should we use it or not? Well, it depends, like with everything in software engineering. However, probably there are **more cons than pros**, and a number of good use cases are limited. A good example of usage is proposed by Magento for e-commerce; however, as we see even they need to use some hacks to make it work, and as a result they implement database inside the database anyway.

## 📝 [A Graph-Based Firebase_202208](https://stopa.io/post/296)

- In A Database in the Browser(blog), I wrote that the schleps(艰难的旅途) we face as UI engineers are actually database problems in disguise(装扮；伪装)
- my co-founder Joe and I decided to build one and find out. This became Instant. 
  - I’d describe it as a graph-based successor to Firebase.
  - You have relational queries and basic auth. Optimistic updates come out of the box, and everything is reactive. 
- we started with SQL but ended up with a triple store and a query language that transpiles to Datalog.
- Why triple store? What query language? read on.

- Delightful Apps
  - Optimistic Updates
  - Multiplayer
  - Offline-Mode

- Bespoke Solutions
  A. DB
  B. Permissions
  C. Sockets
  D. In-Memory Store
  E. IndexedDB
  F. Screens
  G. Mutations

- Inspiration
  - if we look at how Figma, Linear, and Notion work, we find clues. Squint, and their architecture looks like a database!
- If our Local DB and Backend DB spoke the same language, both could understand and apply the same mutations. 
- Databases handle replication. So what if we made the client a special node? The Local DB already knows the queries to satisfy. So it can talk to the backend and get the data it needs.

- A SQL-based tool is closest at hand. I enjoyed looking at absurd-sql. This uses sql.js (SQLite compiled to webassembly) and persists state into IndexedDB.
- SQL has a schema. Schema is useful, but it make things less easy than Firebase. 
- SQL isn’t simple or easy. It’s a tough combination of lots of features, with little of it being useful for the frontend.

- So we wrote a graph database to find out. 
  - We chose Triple Stores, one of the simplest kinds of graph databases. 
- If you haven’t tried one, here’s a quick intuition:
  - we need to be able to express a node with attributes. These sentences translate to lists
  - Then we want a way to describe references.these translate to lists just as well
- Put these lists in a table, and you have a triple store! Triple is the name of the list we’ve been writing
  - The first item is always an `id`, the second the `attribute`, and the third, the `value`. 
  - Turns out triples are all we need to express a graph. 
- once you’ve expressed a graph, you can traverse it. 
  - Triple stores have interesting query languages. 
  - Here’s Datalog

## 👥 [A Graph-Based Firebase | Hacker News_202208](https://news.ycombinator.com/item?id=32595895)

- I came to many similar conclusions completely independently, even attempted to build a typesafe in memory datalog in typescript.
  - I also came to the conclusion that just exposing datalog triples as a query language would never feel right and tried to expose a graphql like language that generated the datalog triples.
  - IMO react relay offers a great similar offering with their normalized cache. Relay has great DX too and can be totally type safe. To my knowledge datalog is way too dynamic for static analysis.

- I have built my own similar reactive in-memory triple store with typescripts type safety, but then I realized I still need transactions which are a bit of a pain, because transactions are bundling the otherwise separete triplets, so the atomic, independent logic of triplets and related effects breaks a bit. (I am sure it's solvable.)
  - The example code uses a `transact` function. But it really depends on what you mean by “transaction”. 
  - 👉🏻 We don’t use a triple store at Notion, but we do use an abstraction that ensures a collection of operations either all succeed or all fail. 
  - We don’t support “interactive” transaction, where you can read, modify, write as an atomic group. 
  - This just isn’t desirable in a multiplayer or offline system - in cases we need that kind of consistency we use a normal HTTP API which is online-only.
- As jitl points out, in multiplayer settings, what you need is some way to commit a series of transactions all-together or not at all. We support this.
  - In the case where you want to read the database inside your transaction, we take inspiration from Datomic. **Datomic runs all mutations in one high-memory box**. You can provide functions that run in that box. This way, you can guarantee that the reads inside your transaction have the latest value. There's a lot of UX to figure out there, and this would be something to try to avoid in an offline-available setting.

- Datalog isn't even really a query language. It's a class of query languages with a specific expressive power.
  - Whereas SQL is essentially conjunctive queries with non-stratified Negation, Datalog is recursive conjunctive queries with no or only stratified negation.
  - Datalog also has nothing to do with triples, they are two completely orthogonal concepts.

- tripletstore/datalog actually seems like a decent compromise between SQL and no-SQL that could actually work out! Awesome idea!

- Another product that does all this (relations, reactivity, offline, permissions, sync, etc…) really well, is Realm.
# more-blogs
- [Entity-attribute-value model in relational databases. Should globals be emulated on tables? Part 1. - DEV Community](https://dev.to/intersystems/entity-attribute-value-model-in-relational-databases-should-globals-be-emulated-on-tables-part-1-2e49)

- [The Anti-Pattern – EAV(il) Database Design ? – The Anti-Kyte](https://mikesmithers.wordpress.com/2013/12/22/the-anti-pattern-eavil-database-design/)
