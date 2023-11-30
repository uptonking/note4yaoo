---
title: lib-db-model-eav-blog
tags: [blog, database, entity-attribute-value]
created: 2023-09-25T17:51:20.050Z
modified: 2023-09-25T17:52:11.778Z
---

# lib-db-model-eav-blog

# guide

# blogs-eav-jsonb
- [Replacing EAV with JSONB in PostgreSQL_201601](https://coussej.github.io/2016/01/14/Replacing-EAV-with-JSONB-in-PostgreSQL/)
# blogs
- [Entity-attribute-value model in relational databases. Should globals be emulated on tables? Part 1](https://community.intersystems.com/post/entity-attribute-value-model-relational-databases-should-globals-be-emulated-tables-part-1) 

## [Three ways to model EAV schemas and many-to-many relationships_201511](https://www.googlecloudcommunity.com/gc/Modeling/Three-ways-to-model-EAV-schemas-and-many-to-many-relationships/m-p/562454)

- The entity-attribute-value (EAV) schema is often encountered in business tools where the number of possible attributes for an entity is very large, but any given record only has data for a handful of them. 
  - This schema is very flexible and allows for efficient storage of sparse data, but unfortunately is poorly suited for analytical queries. 
  - In this article we demonstrate three options for modeling the schema in Looker so the attributes are available for effective querying. 
- Many-to-many relationships can be imagined as a special case of the EAV schema where the join table has no value column – only the association between two entities is what matters. 
  - The solutions offered here work equally well for many-to-many relationships; you will just have boolean values for the attributes instead of strings. See Option 3 for an example many-to-many dataset based on a product tagging system.

- Option 1: Create a Fact Table
- Option 2: Dynamic Joins
- Option 3: Search a serialized list of tags (many-to-many associations only)

## [Wordpress and the Curse of EAV | Antradar Blog_201407](http://www.antradar.com/blog-wordpress-and-the-curse-of-eav)

- Wordpress is a memory hog and unless you have plenty of hardware resource, your Wordpress powered website will hit a performance wall the moment you start using it seriously.
- Entity-Attribute-Value, or EAV, is a database layout. The strengths and shortcomings of EAV are directly linked to the extensibility and inability to achieve good performance of the Wordpress core and many of its extensions.

- How does Wordpress use EAV?
  - As if EAV's complexity and lack of data-type optimization weren't bad enough, Wordpress tops it by using EAV abusively and indiscriminately (read: poorly). The table that holds all the blog articles, "posts", also stores images, attachments as well as arbitrary record types from other plugins. 
  - The woocommerce plugin, for example, saves a purchase order as a post!
  - Using the same table for everything also causes severe performance penalty. For example, when someone is placing an online order, MySQL locks the "posts" table.

- No, caching is not a solution
  - Caching for these use case scenarios does not allow real-time information.

- What are the alternatives?
- Be specific with features. 
  - Wordpress uses EAV because it tries to be everything, and it _can_ be everything but poorly. 
  - When a system is built for a specific set of purposes, the data tables can be properly built and correlated (a process called normalization).
- Split the tables. 
  - If Wordpress must be used, which is often the case when we were consulted to just "optimize" a Wordpress site, we can still bring some senses to the over-generic "posts" table. 
  - We rewire the plugins so that they use a different table. This strategy helps with table locking.
- Use cEAV. 
  - The performance issues of EAV is not unique to Wordpress. There are times when we have to allow user-defined data structure. 
  - One example is faceted search on data records with arbitrary attributes. We developed a specialized engine - columnized EAV, or cEAV, to battle typical EAV problems.

## [Modelling dynamic attributes - Blueprints for the Entity-attribute-value model (EAV)](https://database-modelling.com/article/modelling-dynamic-attributes-blueprints-for-the-entity-attribute-value-model-eav)

- With a growing customer base, your customers often want to have additional input fields in your application. 
- The obvious solution for this would be simply adding a new column to your database table and extending the frontend with a new input field. 
- By using this approach you will be confronted with the following issues:
  - each of your customers sees automatically the new attribute in the user interface.
  - you have to create and apply a database migration and rollout a new version of the frontend and backend
  - a customer might want to add a new attribute or a number of attributes. He or she might not be willed to pay for just a new field without any application logic behind it.

- If your application provides a plug-in architecture or a public API through e.g. HTTP(S), you have to think about third party vendors. 
  - vendors want to keep track of additional information. This information can be either stored in an external database of the vendor or directly in your application's database.
- Depending on your applications architecture, you can track those additional information in three ways:
  - If your application provides a plug-in architecture with direct database access, vendors must store their information in additional database tables. Vendors should never change the core database tables of your application, because of security, reporting and other reasons
  - Each of database tables has an additional column in which structured information can be stored in a flattened way. This could be a column of type json or jsonb or a text type, holding an XML structure.
  - Your application already provides a generic database model for storing additional information. You are doing this by adding the Entity-attribute-value model to your database schema.

- The EAV model is a data modelling blueprint. It allows the implemented application or database to easily store additional information. Those additional information are also known as metadata.

- Disadvantages of the EAV model
- each of the models has the fundamental problem of missing referential integrity. Your other application layers have to make sure that the referential integrity can be assured.
- all metadata values have to be loaded by using JOIN clauses. 

## 📝 [Laravel Custom Fields: JSON, EAV Model, or Same Table?_202301](https://laraveldaily.com/post/laravel-custom-fields-json-eav-model-same-table)

- There are situations when we're not sure what the columns of the DB table would be, they need to be flexible. For example, e-shop product properties: size, color, fabric, there may be more in the future. What is the best DB structure? 

- Option 1. Properties DB Table and EAV Model
  - We can define a separate DB table properties and then a Pivot table product_property with many-to-many relations, and an extra field for the value.

- Option 2. JSON Column
  - We can put all properties just as an unstructured JSON column within the same DB table.

- Option 3. More Fields in the Same Table?
  - the most straightforward approach: you just add the fields that you know for now, make each of them nullable just in case, and then will add more fields to the same table as they appear.
  - in some cases, it may make sense to "hardcode" things

- Performance Comparison
  - In my benchmark test, I've seeded 1000 products with all three possible structures
  - `whereHas` EAV approach is 3-4x slower than other structures
  - JSON approach is only 10-30% slower than the approach of regular columns

- All in all, my suggestion would be to **avoid the EAV model** unless you REALLY need it. JSON columns are okay-ish in terms of performance, but depending on your (more complex?) structure may also be slower or less convenient to query.
  - The good old approach of just adding more fields to the same table may not sound "sexy" but if you go for simplicity and the quickest performance "for now", you should consider starting with that structure.

- 👥 discussions

- 6 milliseconds is indeed 3-4x slower than 1.6 ms, but honestly... who cares? Most of the webshops works with fewer than 10 000 products. 

- Allow me a php not Laravel comment, because it has caused me much pain multiple times already: Wordpress is version 1) throughout, and Woocommerce on top of it increases the complexity of your example, because all blog posts, products, orders etc. are in the same table (wp_posts), with the wp_post_meta table holding the different properties. So a customer order of 5 products (that themselves have variations) becomes a SQL nightmare. And to the comment above "it's only milliseconds": exactly this brings web shop databases to their knees, when a few hundred users access it at the same time, and the database must dig through millions of records for each.
- Thanks for the comment! And again, it's only MY benchmark in certain situation, other situations may bring different results.
- I think the main problem in Wordpress is storing all that kind of data in one table. That's why in the latest Woocommerce versions you can have separate tables for customers, orders, products etc.
- Search for Woocommerce 7.1 and High Performance Order Storage (HPOS). Now it's in woocommerce as an option and have to be enabled. Sooner or later will be in the core by default.

## 👥 [Laravel Custom Fields: JSON, EAV Model, or Same Table?_202301](https://twitter.com/PovilasKorop/status/1619633200170500096)

- Is there any downside with having a table with ~100-150 columns, when the product has a LOT of attributes?
  - Insert is usually slower then. And overall size of one table.
  - And these properties cannot have properties themselves. Think of language of a description. Or unit of a weight number. JSON is superior in this case.
- Good thing with ecommerce, inserts are done rarely than querying. And I'm definitely okay with my inserts being slow than my customers query being slow
- I would rather have two additional tables:
  - attributes table, containing the list of attributes, possibly with foreign key for product types (you don't need fabric, size or color for a DVD)
  - attribute table - related with attribute and product IDs

- Nice post. Just remember to put comment on the migration/table column that contains json structure for consistency. It helps a lot.

- I’ve seen big systems (mostly ERPs) using option 3 even if no properties are yet needed. So they add like address_1, address_2 … Then end up with table with 200+ properties
  - that may be still OK if they don't see performance/maintenance issues with that. If they do see that as a problem, then they need to give budget for refactoring.

- I blogged about this just a couple of days ago as was sick of answering the question on the @laracasts forum
  - [Modelling Products and Variants for E-Commerce - Blog - Martin Bean_202301](https://martinbean.dev/blog/2023/01/27/product-variants-laravel/)
- By using your approach. Can you show any examples of a performant query when querying for a product with an attribute of color blue.
  - It’s redundant because you’d want to use something like Elasticsearch to index and then search a non-trivial amount of products. Otherwise you could do it using simple joins.

- I would say that in this case, option 3. Mainly because it’s relatively easy to migrate to a more complex one in the future. If migration is easy, prioritize YAGNI. If not, choose a flexible structure. Also note that the numbers of records will only be ~10000 for this domain.

- When building something like the EAV model, one is basically building the edge table of a graph structure, which MySQL, Postgres and others ain't really optimized for... but I've seen it done quite a lot! Nice benchmark!

- I am building a system with loads of product data and am using JSON and extra columns on Postgresql. Works very well, is extremely flexible and if you really need to speed up reads there is the option of materialized views.

- We've used this package to simplify the EAV approach.

- We had 100000+ products, I used the many-to-many option with elastisearch key-value indexing

- I prefer EAV over JSON but also always recommend thinking thouroughly about which properties you need for product listings etc. Those are properties you really want to have in a flat table structure and you do not get  nasty performance issues because of too much table joins.

### [Modelling Products and Variants for E-Commerce - Blog - Martin Bean_202301](https://martinbean.dev/blog/2023/01/27/product-variants-laravel/)

- In traditional retail, if a product comes in many variants then each variant will be referred to as a SKU. 
  - A product would be the top-level representation of a product
  - A SKU represents a single variant, so its model needs to hold information unique to that particular variant, such as price, inventory, etc.
- Whilst the above takes care of the one-to-many relation between products and SKUs, it does leave out the topic of product attributes (like colour, size, etc). 

## [How to store schema-less EAV (Entity-Attribute-Value) data using JSON and Hibernate](https://vladmihalcea.com/how-to-store-schema-less-eav-entity-attribute-value-data-using-json-and-hibernate/)

## [Storing user customisations and settings. How do you do it? - DEV Community_201811](https://dev.to/imthedeveloper/storing-user-customisations-and-settings-how-do-you-do-it-1017)

- I've recently embarked on scaling up a side hustle which entails storing a large amount of user settings and customisations that they can make to a web platform. 
- Now, the methods and scenarios I've come up with after some brainstorming to potentially manage these settings and customisations:

- A single row of settings per customer
  - I could store all of the settings required for each users application in a single table "settings", with each setting taking up a column and each user taking up a row.

- JSON Storage
  - I could take my existing JSON and push it into the relational database such as Postgres for storage. 

- A property bag / key value approach
  - I could create a very simple table containing an id, user_id, key, value in my database and ensure I have the flexibility to store settings with ease, whilst also being able to query for a user_id and pull back the whole set in one go.
  -  I could create a very simple table containing an id, user_id, key, value in my database and ensure I have the flexibility to store settings with ease, whilst also being able to query for a user_id and pull back the whole set in one go.

- An alternative?
  - I have to face facts, each option actually is flirting with a nosql equivalent. 

- 👥 discussions

- Your property bag idea is usually called the entity-attribute-value or EAV pattern in database design, and it's notoriously messy. There are some situations where it's called for but it's hard to think of an example where it isn't a compromise with an inherently unpleasant structure.
  - Attribute per column is effective but leads to really sparse tables and puts major implementation & operational constraints around customizability.
  - Postgres' JSON/JSONB can do a lot more than you might think. 

- Would love to hear your thoughts 2 years later - how did it go? Thinking of Postgres + JSON most myself in a similar situation.
  - Ended up with everything in postgres.
  - Settings table is very wide right now but I'll be converting it over to a few columns of jsonb in postgres.
  - Running 2 databases really wasn't an issue but I found myself often wanting to join data across both e.g. is setting A turned on and therefore I need some data from table B.
  - I decided to move everything off mongo once j got myself used to using JSON in postgres. I use the citus extension to scale horizontally as needed.

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
  - 👉🏻 **We don’t use a triple store at Notion, but we do use an abstraction that ensures a collection of operations either all succeed or all fail**. 
  - We don’t support “interactive” transaction, where you can read, modify, write as an atomic group. 
  - This just isn’t desirable in a multiplayer or offline system - in cases we need that kind of consistency we use a normal HTTP API which is online-only.
- As jitl points out, in multiplayer settings, what you need is some way to commit a series of transactions all-together or not at all. We support this.
  - In the case where you want to read the database inside your transaction, we take inspiration from Datomic. **Datomic runs all mutations in one high-memory box**. You can provide functions that run in that box. This way, you can guarantee that the reads inside your transaction have the latest value. There's a lot of UX to figure out there, and this would be something to try to avoid in an offline-available setting.

- Datalog isn't even really a query language. It's a class of query languages with a specific expressive power.
  - Whereas SQL is essentially conjunctive queries with non-stratified Negation, Datalog is recursive conjunctive queries with no or only stratified negation.
  - Datalog also has nothing to do with triples, they are two completely orthogonal concepts.

- tripletstore/datalog actually seems like a decent compromise between SQL and no-SQL that could actually work out! Awesome idea!

- Another product that does all this (relations, reactivity, offline, permissions, sync, etc…) really well, is Realm.
# blogs-vendor

## [Magento 2 EAV Model - Things You May Not Know](https://bsscommerce.com/confluence/magento-2-eav-model/)

## [Magento Entity Attribute Value (EAV) Model - Magento Tutorial_201709](https://blog.magestore.com/entity-attribute-value-in-magento/)

## [Thoughts on Tableau - Data Modeling and EAV - Data + Tableau + Me_201602](http://www.datatableauandme.com/2016/02/thoughts-on-tableau-data-modeling-and.html)

- Like I've said before, I prefer this approach for a lot of my use cases, mainly because I feel it gives me more flexibility. I like thinking through Tableau in terms of Calculations and Aggregation. 
  - What can be considered a downside to this approach, is the fact that you have to force yourself to think in terms how Tableau aggregates your result set in the viz. You have to force yourself to see Tableau as drawing graphs based on the results of Aggregated Queries. It can be more difficult to create/use "Row Level Calcs", since you might have to enforce aggregation on the Calcs or use LoDs. 
  - The other potential downside to this is Size. Using this method will create a lot of additional records, and will increase the overall size of the dataset. So if you are working with very large datasets, that would be made even larger, this might not be the best approach.

- ### do you think EAV Model approach to Data Design is best for most cases in @tableau ?
- https://twitter.com/RodyZakovich/status/694626637787353088
- I don't think there's one size fits all, I think you can take the column route too far. All depends what you need IMO
# more-blogs
- [Entity-attribute-value model in relational databases. Should globals be emulated on tables? Part 1. - DEV Community](https://dev.to/intersystems/entity-attribute-value-model-in-relational-databases-should-globals-be-emulated-on-tables-part-1-2e49)

- [The Anti-Pattern – EAV(il) Database Design ? – The Anti-Kyte](https://mikesmithers.wordpress.com/2013/12/22/the-anti-pattern-eavil-database-design/)
