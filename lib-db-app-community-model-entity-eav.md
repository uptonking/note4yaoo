---
title: lib-db-app-community-model-entity-eav
tags: [community, database, database-design, eav, entity-attribute-value, graph-database]
created: 2023-09-24T15:41:34.538Z
modified: 2023-09-24T15:43:13.230Z
---

# lib-db-app-community-model-entity-eav

# guide

# discuss-stars
- ## 

- ## 

- ## [“We already store data. In a database. It works well” | Hacker News_202002](https://news.ycombinator.com/item?id=22296659&p=2)
- Some people would take issue with the "It works well" part. https://lists.wikimedia.org/pipermail/wikidata/2020-February... Turns out that scaling up a general-purpose triple store beyond 10B triples is really, really hard, and that few or no people in the FLOSS community (important due to Wiki's reproducibility and freedom-to-fork requirements) are paying attention to the problem.

- MediaWiki (the actual Wikipedia website) runs on top of a traditional SQL database (originally just MySQL, but others are now supported too):
  - There have been various forays into Semantic Web technologies. Previously people have done things like parse the infoboxes on Wikipedia pages and then import that into a triple store.
  - It seems that now the Wikimedia Foundation is finally interested in moving in this direction. But the software isn't there yet, certainly not at the scale Wikipedia needs.

- ## [The Block Protocol | Hacker News_202201](https://news.ycombinator.com/item?id=30103401)

- The Block Protocol is building on a pretty large history of similar ideas, but none have really succeeded. Joel's interest in this project is some cause for hope as is the embrace of existing standards like react, webcomponents, and HTML.
- Historically, OpenDoc is pretty relevant. So is OLE. More recently Notion, Coda, Microsoft Loop, Anytype.io, etc lean on the same concepts to allow you to break documents into independent & reassemble-able components. 
  - There hasn't been a large ecosystem here, although the componentized approach has more traction now as we move away from skeuomorphism.
- On the data side, Solid is the most relevant. The models are often the same, users give applications very granular data permissions and progressively authorize data access as required for additional functionality. Developers seem to dislike the model... You don't really know what you're going to be rendering and key features are not really used.
- From a pure schema perspective, you have schema.org. It's a pretty comprehensive attempt to catalog structured data for most use cases. It's nice that this project can kinda build on the semantic web, but most people ignore it! That being said, adoption would go a long way towards interoperability between OSS projects.

- 
- 
- 

- 🤔 Why is RDF a bad thing?
  * Layers upon layers of complexity: Implementing CURIs alone is a non trivial task, although all that's really needed to describe entities and attributes is 128bit UUIDs.
  * There is no good build-in way for authentication and trust.
  * Description Logic (the foundation of OWL) has a fundamentally prescriptive philosophy, which makes it inappropriate for most practical applications.
  * No good library and tool support in general, due to the complexity.
  * Blank Nodes
  * No good consistency mechanism for distributed data generation, and Quads (having multiple graphs) don't properly solve this.
  * Using human readable entity and attr id's leads to more bike-shedding and accidental collisions than it's worth.
  * High barriers to entry.
  * After years of developer disappointment the earth is pretty much salted.

- What you've outlined above is a common misconception about RDF. Here's another way of looking at RDF:
  - An abstract data definition language for structured data represented as entity relationship graphs. Basically, the same Entity-Attribute-Value model that's existed for eons plus the addition of formalized identifiers (i.e., IRIs) for denoting entities, attributes, and values.
  - RDF Schema, OWL Ontology, etc.. are simply Data Dictionaries comprising terms that describe Entity Relationship Types.

- How does the Block Protocol differ from or add to Web Components? Is it the standardization of how structured data that can be passed with the blocks?
  - Based on what I can gather from the documentation I think the answer is basically: Yes, it’s the structured data.
  - My guess is the creators of Block Protocol want to promote the free exchange of structured data and decided that coupling the data to UI components is the best way to do that? It’s notable that the web has faced challenges encouraging use of both structured data (Semantic Web) and UI components (Web Components). Maybe they can be more appealing bundled together.
- This is correct: it's the standardization of the interface between blocks and things using them, which includes structure in the data being passed back and forth, and the structure of the interface itself (e.g. what operations are available).
  - We do want to promote the free exchange of structured data, and to have data captured and marked up according to some structure - we also want to promote the portability and easy-of-setup of UI components.
  - Our FAQ illustrates how we relate to and intend to use existing standards - https://blockprotocol.org/docs/faq - we'd be interested in any others you think worth building on.

- 
- 
- 

# discuss
- ## 

- ## [Mistakes Beginners Make When Working with Databases | Hacker News_201606](https://news.ycombinator.com/item?id=11862723)
- EAV isn't all bad, there are use-cases for it. If you have a highly dynamic data (user configurable) then EAV might be a good way to STORE that data.
  - Is it ugly, it sure is. **Moving read out to a cache layer, and search out a purpose built system, the DB becomes a persistence engine**. You have solved the other issue you don't mention with EAV, and thats performance.
- Most EAV implementations I've seen had under 10 distinct "schema-less" virtual tables (sorry about lack of terminology) with perhaps 40-60 distinct "columns" and the different variations of a record types usually had consistent attributes.
  - Basically the whole thing could've been replaced by 5-10 tables. Maybe taking advantage of Postgres OORDBMS capabilities for the common columns.
  - Queries tended to group complex CTEs and multiple self-joins. You know it's an anti-pattern when devs start complaining about postgres join performance and you see they got two tables being joined 15 times
- 
- 

- ## [The Impedance Mismatch Is Our Fault (2012) | Hacker News_202004](https://news.ycombinator.com/item?id=22803776)
- I'm half-way through the video, and he's pushing the Entity Attribute Value (EAV) model. He's right. He's absolutely right.
  - There is a duality between the much-hated EAV and table-oriented representations of data, especially if you are disciplined in your schema design so that the mapping between your EAV schema and a SQL table-oriented schema is natural.
- EAV is, essentially, the most normal form you can construct. And the more normal the form, the easier it is to apply CRDT techniques should you want to. Also, if you normalize the keys (see SQLite4[0], yes, 4, an abandoned project, but the docs are still there) then you get to trivially use any distributed ordered key/value store, and you can distribute the key ranges, and it's trivial.
- Now, EAV is much hated. But that hatred is wrong. The problem is that RDBMSes aren't exposing a dual of EAV and tables. 
  - **If you have an EAV schema, you can create VIEWs that look like equivalent table-oriented schemas -- the reverse is also possible, but somewhat harder**. 
  - Using VIEWs to bridge the gap imposes a heavy burden on the query optimizer. 
  - But SQLite4 and similar database designs essentially have EAV stores internally that they could expose with a lot less complexity than VIEWs impose.
- We can haz EAV and table orientation at the same time. We should have it.
- Plus, as TFA says, you can combine EAV with timeseries, which allows you to have time travel in your queries, and even transactions (e.g., run a transaction now that has an effect in the future), which makes your data naturally copy-on-write, which greatly improves read performance. Granted, you have to cleanup unnecessary history at some point, otherwise it piles up (vacuum), but that's OK.

- There's a class of databases called EAVT databases which include time

- I believe it leads to datomic, a database you can try out on Aws (datomic cloud) to see the implementation of all the things he's getting excited about.

- ## [Never Write Your Own Database (2017) | Hacker News_201805](https://news.ycombinator.com/item?id=16995612)
- As soon as you allow some kind of user-defined meta data, you basically end up with the entity-attribute-value pattern.
  - Every sufficiently advanced system does that, be it a CRM that allows custom fields, or a project management or ticket system, a workflow system etc. And basically all enterprise software contains elements of these systems.

- A good alternative would be to use JSON types in RDBMS in combination with classic field types. EAV is really just free form data and JSON is easier to query in MySQL or Postgres.

- ## [Show HN: A Schemaless Data Store Within Your SQL Database | Hacker News_202202](https://news.ycombinator.com/item?id=30291592)
- EAV is a pattern you can easily roll out - https://docs.sqlalchemy.org/en/14/orm/examples.html

- Another commenter illustrated some of the issues you will run into with this pattern at scale.
- It would probably help to benchmark some complex queries on a sizable data set. And compare against mongo, postgres jsonb, vanilla eav, clickhouse, etc. Without much information to go on, it's hard to know what this is.

- 
- 
- 

- ## [Django EAV 2 – Entity-Attribute-Value Storage for Django | Hacker News_201807](https://news.ycombinator.com/item?id=17628685)
- Or just use JSONField, because that’s exactly the reason why it exists.

- ## [When to Avoid JSONB in a PostgreSQL Schema | Hacker News_201609](https://news.ycombinator.com/item?id=12408634)

- EAV is typically considered to be an anti-pattern for several reasons: 
  - it becomes very expensive to rematerialize a entity with all of its attributes/values, 
  - it becomes difficult to have any kind of constraints on the values (this is also a problem with jsonb), 
  - and it's hard for the database to maintain good statistics on the values of different attributes as most databases don't keep multi-column statistics. 
  - Don't worry, I've had similar ideas before.

- If you want to allow user-defined fields in a relational database, your realistic are either EAV or stuff json into a text column. EAV, if done extremely carefully, can be a good solution, but 99% of the time, it's going to be a huge pain.

- I used JSONB to keep the Tags on an object. Used to be EAV. Works way better here

- 
- 
- 
- 

- ## [Pivot – Rows to Columns | Hacker News_201802](https://news.ycombinator.com/item?id=16310117)
- In a real EAV where you have just one table and you only change data not the table structure you can only really query for a list of attributes. In that case there is no performant way of querying for a specific attribute.
- The value of this style of database seems limited because you have to change the application in order to make good use of the new attribute you've added but you refuse to change the database at the same time. The best systems are where application and database match; either both contain knowledge of an attribute or neither contain knowledge of an attribute. The case of neither having knowledge is only useful where an outside party (such as the end user) alone can interpret the attribute. For example listing device specs where the user alone can compare them and not the application like: backlight = LED, subpixel = PenTile, power-supply = switch-mode.

- One thing EAV is really good for is allowing for user-defined attributes - some privileged users are allowed to add a new user defined field, and there's a UI that allows regular users to view and maintain them. A pain for reporting, but you can either update a view as UDF's are added or drop and recreate a materialized view at set intervals. I've worked with applications where there's a user-defined screen for each entity in the system, it can be a great get-out-of-jail card for a lot of late/ad-hoc requests.

- ## 👉🏻 [We saved $50k/year with a Go microservice coded in a hackathon | Hacker News_201808](https://news.ycombinator.com/item?id=16806388)

- 👉🏻 This is a pretty popular pattern known as Entity-Attribute-Value. 
  - It's used by many products where a) data model needs to be very flexible and allow new attributes without schema changes, or b) a typical entity has a large number of possible attributes that may or may not be set for all entities ("sparse" attributes). 
  - WordPress uses this to store post metadata, Magento uses this to store product attributes and most of other data, Drupal uses a variation of this to store all the posts and other content you create… I have too much experience with this model to be surprised.
- Sounds like a great case for Postgres hstore (like OpenStreetMap does it)?
  - hstore querying is quite slow (and GIN indexes on hstores are pretty massive). 
  - I'd always go jsonb over hstores these days, but jsonb has the same indexing problem. 
  - JSON has a well-optimized/spec compliant serializer/deserializer in every language you can imagine as a baseline, whereas hstore does not.

- Entity attribute value anti pattern - this has been well known for at least 20 years. 
  - It can be tempting when you want to design a "flexible" system but really needs to be used sparingly. 
  - I was BI team lead on a product where the architect insisted that it be used on every entity (>300) as you never knew when you might want to add some bit of data. 
  - It led to some interesting (multi-page) sqls and the project ultimately failed. 
  - This was one of the reasons. 
  - Slow performance and often runtime errors when expected data wasn't present and the application layer couldn't cope
- EAV pattern has trade-offs you need to compensate for (performance). Production systems that use EAV have flat tables, and heavy caching to have be flexible with acceptable performance.
- You could argue that there are cases for it. Datomic is basically EAV on steroids.

- Oh gosh this pattern. The first time I encountered it was in my first job where we used Magento. Super flexible. Also super slow. Does anyone have any advice how to make a db design like this work faster? Generally I thought when data is arranged like this it might be a prime candidate for document based storage. But I'm no dba so I have no idea if that would be correct.
  - If you are using Postgres, the `JSONB` datatype will let you do exactly this while still using the full power of SQL. Simply create a column where you keep a JSON object full of random user properties, if flexibility is what you want. You can even index properties.
- The question is whether it can be stored like this while allowing for fast queries. For example, unless it changed recently, **Postgres doesn't calculate statistics to help the query planner on jsonb fields**.
  - JSONB columns should behave just like any datatype with a GIN index in the recent releases, to my knowledge.
  - Still, **a JSON column will arguably be faster than a pure KV table** since you can more efficiently query it, especially any non-JSON columns.
- IIRC JSONB still has problem with index statistics
  - So values in JSONB columns can be indexed nicely, but the statistics can be much worse than for non-JSONB columns, which can lead the query planner astray.
- Postgres will let you create an index on an expression into the JSON column, so querying should still be very quick.

- Or just create ad hoc tables with user fields. Quite often it's not that a customer has n different fields for n entities, but a few that apply to the majority (like internal ERP ids, classifcation etc.). Put them in a few tables, index them, join them. If you don't want to parse internal DB descriptors, create a set of "schema" tables to build queries from.

- If they are using some sort of middleware orm, which they may well be because of their model, they are most likely using an EAV schema which, although flexible for writes, is horrendous for reads. The join plus pivot is a disaster on virtually any relational system.

- And I don't think you will necessarily get better performance with json fields vs an EAV model. 
  - Yes, you can index json fields by creating virtual views, but that requires that you know the field ahead of time. 
  - With an EAV model, you can have your values table indexed and then join.
  - But I am excited to start using the json field types. In many cases, it will really simplify things over the traditional EAV stuff.

- Wondering if they shoved the data in PostgreSQL with JSONB how well it would perform over EAV.
  - I think that jsonb may not be as performant as EAV. 
  - You don't need joins or unions, but if you are dealing with dynamic fields, **you need to know the fields ahead of time and set indexes for them in jsonb**. 
  - For eav you just have to index your values table.
- PostgreSQL can use multiple indexes so you don't need to worry about needing to know about the fields ahead of time.
  - Likewise[We saved $50k/year with a Go microservice coded in a hackathon | Hacker News](https://news.ycombinator.com/item?id=16806388) you can get away with a full document GIN index.
  - I played around with some basic report stuff at work last year, the EAV data on my local machine, the report took ~7 seconds to run. I shoved the same data into PostgreSQL as JSONB, indexed it just as full doc cos I was lazy, the same report took ~80ms.

- ## ✨ [Eva – A distributed entity-attribute-value database in Clojure | Hacker News_201906](https://news.ycombinator.com/item?id=20304686)
- I was really interested in the now defunct mentat project, but was written in Rust - it's a game changer to have a JVM-powered datomic-ish project with time as a first class citizen.

- time as a first class citizen
  - It's worth noting that time now has two levels of meaning in this context - transaction time and valid time. 
  - Disclosure: working on Crux
- could you highlight the differences between Eva and Crux as you see them, today?
  - `EAV+T+added?` is the canonical data representation used by Eva, whereas Crux relies on two discrete "document" and transaction logs as the canonical representation. 
  - There are many reasons for this (data eviction, "unbundled" scalability etc.) but **bitemporality (i.e. the ability to transact into the past/future) is definitely the primary reason why Crux doesn't follow the EAV+T+Added? pattern**.

- Last time I saw the EAV pattern used was in Magento. It was an absolute nightmare to query against.
- I don't think Magento used it right.
  - I eventually dropped this solution in favor of Clojure data structures: if you have an in-memory (in-browser) database anyway, why keep the data in Datascript, if you can simply keep it as ClojureScript data structures?
- I think Magento did use it right, but EAV is impractical on a relational database not designed for EAV. This fact, however, doesn't show itself until you've reached a certain (arguably low by today's standards) scale.
- I also started with Datascript both on frontend and backend, but ended up using instead its core data structure - persistent-sorted-set [1], which works really well if all you need is indexing.

- I agree that the experience of querying EAV databases using SQL can feel cumbersome [0]. But Datomic's dialect of Datalog [1] is a great fit for EAV and can produce much more readable and simpler queries.

- EAV is not for everyone. You have to have a data set for which each entity can have values defined for some of, but not all of a large set of attributes. It’s a bit like sparse matrices(稀疏矩阵), actually.
  - And, yes, you want your tools and application to abstract away some of the messiness involved in something as simple as “load/save this object from the database, ” otherwise you’ll end up with a much larger amount of code for such a simple operation. I’ve seen it done in a Django app, and it’s not bad to work with once those abstractions are in place.

- Why not just use a json store for those sparse attributes? EAV performance at large scale is really dreadful. So many queries.
  - EAV with a query engine and syntax not designed for it is awful. EAV (and AEV and AVE and VAE) with datalog queries is performant, a joy to use, and way more flexible than json stores.

- The EAV model is great in theory and is probably great in practice _if_ the backing software has been _designed_ with EAV in mind.
  - In the context of Magento, it is a real _nightmare_ and is one of the major contributor of the slowness of the Magento platform (at least for magento < 2.0).
  - The reason for this slowness is that in a relational database, the EAV model makes it so that e-v-e-r-y s-i-n-g-l-e SQL query is one gigantic query made of tons of JOINs.
  - To give you an example, querying a product in Magento may need to join no less than 11 tables!
- In order to fix this issue, **the Magento team created what they call "flat tables"** which are tables that are created by querying the database with an EAV query (i.e. the query with a million joins) and **putting the results in a table with as many columns** as there is attributes being returned by the original query.
- We use Magento at betabrand.com and I can confidently say 90% of the slowness of our website is due to Magento's EAV tables and we have spent a humongous number of engineering hours optimizing this.

- AP or CP?
  - Definitely CP. 
  - With Eva and Datomic, transactions are serialised through a single transactor node at a time.
  - **The transaction log design is a fundamental design tradeoff that Eva/Datomic/Crux share**, which means system throughput is limited by the throughput of a single process. The argument in favour of such a design is that most businesses & business applications don't actually experience transactional data volumes over 10K tx/sec.

- ## 🌰 [Reddit's database has only two tables | Hacker News_201209](https://news.ycombinator.com/item?id=4468265)
- This is called eav
- They've built a database in their database. Also known as the **inner platform** antipattern

- Datomic takes similar approach. A unit of Entity, Attribute, Value and Time is called datom. Although in this approach we don't have to have schema, datomic forces us to define schema for some benefits.

- The last company I worked at made an application that used the Entity-Attribute-Value pattern in the database. The stated reason was to be dynamic, so we didn't have to worry about adding new columns and the associated downtime (assuming the DB got huge, which of course it would because this app would surely be a huge success). We had that problem on our main app (with 10s of millions of rows) where adding a column was always tricky, so I think management over-corrected. The other supposed win was that since the model didn't change, the code didn't need to be updated.
  - The data that was being stored fit into the relational model pretty well. But thanks to E. A. V. it was very difficult to query. The kinds of questions we often looked at (how many records from this zip code) would have been trivial without the E. A. V. Today you might use a NoSQL database (which were just starting to get noticed at the time), but in reality it fit into MySQL just fine.
- The real sad part is, we never used that functionality in the 2-3 years after it was developed while I was there. The app wasn't big enough for adding columns to take much time at all. All that "flexibility" we needed? We didn't use it, because it would have taken additional time to implement the additional front-ends and update the other backend systems.

- ## [EAV is considered an antipattern. | Hacker News](https://news.ycombinator.com/item?id=24049559)
- I've been working on a project using schema.org objects (100's of types of objects) in postgres in a graph/tree like structure. While structured the objects are not consistent enough for me to want separate schemas for them. Using JSONb in postgres allows me to index separate fields within the JSON while still having all the objects in a single graph.
  - If I couldn't use JSONb with indexes (and triggers for custom foreign key checks) it'd be much harder to do this in in a relational database (and the data is relational, it just isn't consistent across all types).
  - Perhaps this would be better in a Triplestore but there are a lot of features of postgres that are not available in them.

- GP cited EAV as an antipattern, yet it is one of the most reasonable approaches to user-defined fields (especially when suitably augmented), which are frequently a business requirement.

- Not even just user-defined fields, any time where the fields need to be defined as data values rather than part of your concrete data model. Product attributes on a big multi-category e-commerce site being another example. You could just stick them in JSON, but it's still essentially EAV, just with a different storage mechanism.

- Another advantage of EAV as a pattern, is it makes it straightforward to add metadata to values, like "where did this value come from?". For systems with audit trails, just having keys and values isn't enough.

- EAV wouldn't be the first tool I'd jump to -- I've definitely seen it go wrong -- but it feels like it's going too far to call it an anti-pattern.

- The traditional approach to efficiently modelling data like that with relational databases is to use the EAV model, which works quite well in practice.

- 💡 Can you give some examples where a relational schema isn’t suitable?
  - Storing historical webhook notifications
  - The bonus with this is that at the start you are probably only interested in a few of the fields in the webhook, but as your application develops, you may need to extract more. If you've stored the JSON of previous webhooks, you have an easy migration path.
- **Sparse data**.
  - For example, if there are 1000 possible attributes, only 5% are populated for any given row. If you have 1000 columns you are going to have a ridiculously wide and mostly empty table.
  - In Postgres, NULL values take one bit of storage as far as I understand. So a table has to be very, very wide before this becomes a benefit. Of course if you have attributes that you don't control but are e.g. user-specified, JSONB column are a good choice.
  - **The traditional approach to efficiently modelling data like that with relational databases is to use the EAV model**, which works quite well in practice.

- I use the JSONP column type in Postgres for data that is structured but user-supplied.
  - There is a key-value interface.
- Why not store this data into a relational database?
  - Because values can be different types (string, int, boolean).
  - Can't you store them all as varchar? You could even have a type column if you wanted to enforce the types in some way at the application level.
- Product data on a webshop. If you have a wide selection of product categories you’ll have a huge number of attributes that aren’t relevant across your categories.
  - There’s a number of ways to deal with the issue, e.g. a model per category or an EAV database pattern (this is what platforms like Magento does). None are really ideal, but storing the product attributes as JSON works pretty well. Even more so when your database supports querying the JSON blob.
- Storing arbitrarily complex Boolean queries (think Elasticsearch's query syntqx). While this could be done in SQL tables, there are no gains with referential intregity and while there would be some in consistency, I don't think they're worth it.
- There are scenarios when you can't avoid EAV and then JSON is great even when it's for denormalized data.
- More importantly, JSONFields can be used as a substitute for EAV pattern.

- ## [The Inner Json Effect | Hacker News_201607](https://news.ycombinator.com/item?id=12185727)
- They describe something akin to Wordpress' custom fields
- That's because custom fields in WordPress, as well as in Liferay and in a bunch of other products, are implemented as EAV, Entity–attribute–value model, which is an abomination(可憎的事物, 令人厌恶的东西).
  - It is a relational "design pattern" used to implement a database inside a database, instead of using the database itself as it was designed to be used.
  - This has all sorts of fun (not) and useful (neither) effects, including: worsened performance; inability to ensure data integrity through constraints; bloated / unreadable queries; hard to find bugs; needlessly complicated migrations; and so on.
- So, EAV and even "inner platforms" are not always necessarily bad, so long as you know that's what you're doing.
  - For example, Firefox extensions could be easily considered an inner platform but they have the benefit of providing a platform which is safer and more extensible than the underlying OS.
  - Likewise, EAV provides a poor functional replacement for an actual database. But they also prove a lower curve for implementing very simple extensions and limit the capacity for trivial mistakes. Speaking from experience, it's the WordPress sites where plugins have created a whole bunch of extra poorly-built tables that worry me most.
- The alternative to EAV for custom fields is allowing users to modify the database schema. I'd rather stick with EAV.

- What’s wrong with just namespacing tables per module/app/whatever? `wordpress_%app_table1` etc
  - PostgresSQL support namespacing out of the box
- Because giving a webapp sufficient permissions to CREATE, ALTER, and DROP tables is risky.
  - It gets harder to make assumptions about what tables are there when you want to migrate things. I also think it's a hassle if you want to do something like have multiple tenants in a single DB (not impossible, I suppose).

- Having dealt with both, I'm split. I think, in the end, I'd rather model the DDLs and have everything point to separate database on the same server or a new namespace in the existing database. You give enough rope for the customer to hang themselves, but sometimes their requirements are to build a gallows(网板吊架).

- 👉🏻 Sometimes, the thing you need to model in a database behind an application you sell to a customer turns out to be... a sort of limited database with a schema the customer can control and design. When that happens, **EAV is one of the common attractors in design space that everyone gravitates towards**.
  - Of course, it's worth remembering that real databases do not typically use an EAV storage pattern for their data, so maybe it's not the only way to model a custom data store within a relational system.
- It's also an option when the properties of objects going in the table are going to be wildly different or are not known at write time.
  - This is a candidate for something like a **schemaless datastore or a PostgreSQL JSONB column**. Depending on your choice of datastore you can still at least get some indexing and schema help if you choose. With EAV you generally throw all of that out.
# discuss-triplestore
- ## 

- ## 

- ## [Fabric – A simple triplestore written in Go | Hacker News_201908](https://news.ycombinator.com/item?id=20806916)
- What’s the industry take up of data stores like this? It always struck me as much more academic and not used as much in industry. 
  - Nubank recently raised $400M at a $10B valuation and they depend on Datomic heavily for their core systems.
  - The RDF database marketplace is very established [3], and the likes of MarkLogic, DB2, and Oracle have clearly encountered profitable reasons to add RDF support. I believe RDF has good traction in knowledge-intensive industry domains such as clinical research and life sciences.
  - Disclosure: I work on Crux which adds bitemporal versioning and eviction to a document->triplestore model running on top of Kafka.

- Triple relationships like the above are the kind of queries a Prolog engine can answer well (and far more).

- 🤔 What's the use-case for a triple store vs a graph DB? Social networks?
  - People also call triple stores graph DBs.
  - Triple stores support a disciplined set of primitive types that come from xml schema, so you have "xsd:integer", "xsd:datetime", "xsd:decimal", really the critical things that are missing in JSON. That is, there is a kind of fact where the object is a literal.
  - Triple stores also support facts where the object is an identifier for another object. That could be a URI which names it, or it could be an internal "blank node" identifier.
  - Other kinds of "graph database" have different semantics, for instance they might not have support for literals, or have a different set of literal data types, or they might let you attach facts to the edges (hypergraph, property graph, ...)

- ## [Google Badwolf: Temporal graph store abstraction layer | Hacker News_201510](https://news.ycombinator.com/item?id=10432071)
- Badwolf is a immutable triple store with temporal predicates.

- 🤔 Why is this better than just using any SQL database?
  - Lots of SQL databases don't have good constructs for dealing with ranges, which make lots of operations you'd want to do with temporal data awkward (PostgreSQL since 9.2 has range types, and lots of useful features attached to them, that address this.)
  - Beyond that, pretty much all the normal SQL vs. NoSQL considerations would seem to apply without much change when you address temporal data, so the usual mix of ACID vs. scalability, schema enforcement vs. schemaless flexibility, etc., considerations apply.
- If you want to know the advantages of triple stores, there's a lot out there.
  - One key strength is that triple stores have a "schema as data" approach, meaning that schemas can be made to follow rules on the fly based on the data contained within them. Nothing that application code can't do, of course, but the entire purpose of these kinds of databases is to find a way to have data be as self-descriptive as possible.
- Triplestores are good for storing and processing graphs, which don't fit the relational database model very well. There is a variant of SQL called SPARQL intended specifically for querying triplestores
