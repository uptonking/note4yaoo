---
title: lib-db-model-eav-community-triple
tags: [community, database-design, eav, entity-attribute-value, graph-database, triplestore]
created: 2023-09-24T15:41:34.538Z
modified: 2023-09-25T09:00:49.722Z
---

# lib-db-model-eav-community-triple

# guide

# discuss-stars
- ## 

- ## 

- ## Another really cool usecase for JSON is Triplestore/Entity-Attribute-Value (EAV) graph-like data
- https://twitter.com/GavinRayDev/status/1528434390514159621
  - The performance difference between a regular table (entity, attribute, value), and JSON columns is obscene(大得惊人的；多得骇人听闻的; 不道德的 )
  - [Replacing EAV with JSONB in PostgreSQL_201601](https://coussej.github.io/2016/01/14/Replacing-EAV-with-JSONB-in-PostgreSQL/)

- ## 💡 [Is EAV (Entity Attribute Value) equal to SPO (Subject Predicate Object)?](https://answers.knowledgegraph.tech/t/is-eav-entity-attribute-value-equal-to-spo-subject-predicate-object/4815)
- The Entity-Attribute-Value model is a quite mature knowledge representation structure in the database community. Especially, Kingsley Idehen is utilizing it quite often to propagate a Semantic-Web-independent Linked Data meme. 
  - On the other side, there is the Subject-Predicate-Object form (knowledge representation structure) which we know at its best from simple natural language sentences and which is applied in the design of RDF Model and viewed there as a specialisation of Semantic Networks.
  - However, I'm wondering about whether EAV is really a good "generalisation" of SPO. 
  - As far I understand the EAV model, due its extension to EAV/CR (EAV with Classes and Relationships) it is possible to describe complex substructures, hence it is the basis for a hierarchical structure. 
  - The SPO model isn't restricted to that issue, it is the basis for a graph structure. 
  - So, I wouldn't insist an equivalence relation of EAV and SPO. I might endorse(endorse) a subset relation where EAV is a subset of SPO.

- Yes, it is re. my world view.
  - Semantic Web community align SPO and RDF, and by effect the specifics of some granularity associated with RDF specification e.g., typed literals handling.

- [What is Linked Data, really?](https://www.openlinksw.com/blog/~kidehen/?id=1639)
  - EAV is just an Entity-Attribute-Value 3-tuple pattern. I equate it to Subject-Predicate-Object. When I do my equivalence though, I explicitly state the addition of Reference Values in the E & A slots with V being optional.
- EAV or in actuality EAV/CR + URIs == more open approach to Linked Data

- ## [Ask HN: What Is Going on with Neo4j? | Hacker News](https://news.ycombinator.com/item?id=33916240)
- triple stores (or quad stores with providence) never quite worked as well as simple property graphs (at least for the problems I was solving). I was never really looking for inference, more like extracting specific sub-graphs, or "colored" graphs, so property attribution was much simpler. Ended up fitting it into a simple relational and performance was quite good; even better than the "best" NoSQL solutions out there at the time.
  - And, triple stores just seem to require SO MANY relations! RDF vs Property Graphs feels like XML vs JSON. They both can get the job done, but one just feels "easier" than the other.
- RDF is the JSON of graphs. OWL is the Json-Schema of RDF.

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
# discuss
- ## 

- ## 

- ## 🌰 Triple stores are the main technology behind knowledge graphs. 
- https://twitter.com/geobrowser/status/1590007004030185485
- Triples consist of an Entity, Attribute & Value.
  - An entity is a thing that can be referenced by a globally unique ID
  - An attribute is a property of that thing
  - The value is what you want to say about that thing
- Using triples, we can assert facts and describe relationships between anything! The **data is unstructured** and can include any relevant information or connections.
  - From there we can add structure to view things in more and more useful ways.

- Geo’s triple store runs on @graphprotocol .
  - With knowledge graphs on public networks, we have a robust architecture for public software in the internet age.

- ## 🌰 [Launch HN: Narrator (YC S19) – a data modeling platform built on a single table | Hacker News](https://news.ycombinator.com/item?id=24640540)
- Wish you the best of luck but isn't this just a fancier version of EAV?
  - Yeah, Entity modeling was one of the big inspirations to our approach. The main difference is how do you reassemble the single time-series table to create any table.

- This is the problem with EAV/nosql/schemaless/etc and ultimately the problem I think you are going to have to solve. Instead of using ETL to model how the activities relate and reifying that model as database objects, EAV just kicks the can down the road to the query/BI tool.
  - Sprawl - The BI tool will end up containing most of the real business logic sprawled across many reports.
  - Single source of truth - A lot of the reports will be very similar but they will be based off slightly different activities or slightly different filtering logic. Which report is the correct one?
  - Traceability - I think this is more of an end-to-end "garbage-in, garbage-out" problem that all ETL/BI tools have that wouldn't be specific to your tool. It's more of an organizational/people problem.
  - Coherent model - In my experience, EAV isn't enough to cover the breadth of analyses mature businesses need to do and most business users won't be able to wrap their head around it. There will have to be some data person that creates a more coherent, tabular/spreadsheet-like model and in the case of this tool it looks like that model will have to exist in the BI tool. Which brings us back to sprawl/single source of truth issues.

- My last encounter with EAV was briefly said disastrous.
  - On the other hand, HW gets better and better, and if you are able to do on the fly, what used to be a "cached" entity, then there you go.
- Often, people think that just creating a time-series table is enough but it is so hard to use and so hard to maintain that you will hate yourself. Narrator.ai solve all those problems so your experience become truly incredible!

- [A data modeling platform built on a single table](https://twitter.com/rob_van_dort/status/1313037246803709952)
  - This is basically the RDF / Triple or EAV (Entity Attribute Value) approach. Existing implementations known for over 20 years. Most extensive example known to me: Stanford's Protégé. Store metamodel, model, data & user interface layout in one table.

- ## 👉🏻 [Revisit indexes for DB performance · WordPress/performance_202201](https://github.com/WordPress/performance/issues/132)

- 
- 

- WP is a 2-person boat. More than a year ago, @OllieJones and I provided a plugin that makes it a 4-person boat. This discussion seems to be a debate between these options:
- The reason that WP will never hold more than 4 persons is the underlying "meta" design. It is based on "Entity-Attribute-Value" (EAV). That design pattern provides flexibility (great tor 2-person boats), but becomes very sluggish as the database grows.
  - There is no next step after WP gets too sluggish due to too many people on the boat. Throwing it out and starting over is the only real answer.
  - (I am a developer and have pursued the EAV schema for over 20 years. I speak from frustration with EAV's appeal but inefficiency.)

- WP will not become a 5000 person boat, not with the EAV schema. but can we throw some duct tape and save some people either at sea or about to launch their boat? yes? then there is no reason to not do it.

- 
- 

- ## [Questions: EAV vs Triplestore, Gremlin, Geographical data, immutability, further readings? · google/badwolf](https://github.com/google/badwolf/issues/82)
- 

- ## [Directus EAV · directus/directus](https://github.com/directus/directus/discussions/2840)
- Use relationships

- ## 🤔 [Rhizome on top of RDF · RhizomeDB/rs-rhizome](https://github.com/RhizomeDB/rs-rhizome/discussions/107)

- EAV vs SPO.
  - From my understanding, the subtle difference between the two is in attempt of SPO to interlink mutable objects/places, whereas EAV aims to provide immutable and persistent values (entities).
  - Also SPO uses globally unique names in order to identified objects, whereas EAV makes use of content-based addressing.
  - Overall, I'm all up for EAV.
  - Because mutability makes a precarious foundation.
- Also names make it difficult to interlink by content, there may exist multiple objects, like "moon/luna"
  - RDF folks cleverly try to solve it with content-based addressing for names, however that creates a problem of propagating/superseeding new values, but I guess there is no escaping that.
- So it's nice that EAV is name-less, akin to content-addressed RDF, making for a simpler model, allowing naming to exist, if one wishes, at a higher level.
- Overall, immutable and persistent EAV seems to be a great foundation.

- (the approach above (given it makes sense 😄 ) is just one way to have a mutable interface on top of immutable data, other's Datomic's txTime, XTDB's validTime)

- ## [EAV Container Feature in MikroORM · mikro-orm/mikro-orm](https://github.com/mikro-orm/mikro-orm/issues/817)
- From my experience the best way to work with EAV is by writing own project specific ORM. Which can take into consideration all project specific nuances and can apply optimizations where needed.
  - But from what I saw in mikro orm it should be quite easy to implement this on top. I’ve never tried though

- [Add support for usage with vanilla JS by B4nan · mikro-orm/mikro-orm](https://github.com/mikro-orm/mikro-orm/pull/13)

- ## 🤔 [Extend QueryBuilder and DataMapper to map Business Model into EAV structure · typeorm/typeorm](https://github.com/typeorm/typeorm/issues/3217)
- EAV is bad from all perspectives. Maybe you are right, but I didn't ever face issue that only EAV can resolve.
  - What you are saying is possible, just dig into QueryBuilder internals, but it has a very high complexity. I don't think we would ever support this in TypeORM.

- If you want to add flexibility to your app and give user (or developer or yourself) ability to manipulate with a lot of entity attributes himself, you have three ways:
  - use array/json column
  - EAV
  - document-oriented database
  - But **if you want have ability to get stats** (or complex reports or filters or other kind of complex SELECT queries) on this "dynamically structured data" - EAV is only way.
  - And EAV is standard pattern. It would be great if ORM support easy creation of such type of model.

- You can also take a look at PHP based version on top of Doctrine ORM: VincentChalnot/SidusEAVModelBundle
  - Also, I want to point that this is the only way to store any data for information integration systems (ontology based systems) like Palantir
  - By the way, later data can be replicated & searched by elastic search.
  - So, eventually dB is required only for acid & key lookups
- I did this using sequelize. Frankly speaking, you don’t need ORM for EAV. Use something like knex.js and write your own.

- ## [How to implement inheritance? · agentm/project-m36](https://github.com/agentm/project-m36/discussions/344)
- In summary, you have a bunch of options depending on how static you want the attributes to be.

- ## [Custom Orders and Products Table using the EAV data model · woocommerce/woocommerce](https://github.com/woocommerce/woocommerce/issues/17241)
- I'm still puzzled why people thing the EAV data-structure doesn't scale. As far as a DB Server is concerned results are simply reserved memory addresses, there's no concept of rows vs columns having any preference for addressing.
- The main advantage of EAV is the relationship table being an integer index in its own right, so negating the need for a separate index creation and maintenance expense - and while the horizontal data model creates empty reserved memory addresses for empty fields, the EAV model does not, similarly to NoSQL models - and the blockchain seems to be scaling just fine.
- So the EAV tables will be smaller, indexed by design and less fragmented.
- Performance debates aside, EAV is more easily extendable with plugins not needing to include SQL patches and removals for fields & indexes, so in the spirit of extensibility, EAV still serves WP & Woocommerce rather well.

- it does not scale because the data is not in a format that could be indexed well. Sure the data can be stored and inserted efficiently enough, if other modifications were made to how it is inserted. However this does not solve the fact that all reporting and other querying of products or orders will be terrible. 

- who says Woocommerce and the standard Wordpress EAV structure doesn't scale? 
  - 800, 000 products searched & filtered in ~0.5s on a $40 Digital Ocean droplet with a little tweaking - by Dave Hilditch the SkyScanner.net DBA

- ## [Convert CMS pages into a EAV model · magento/magento2](https://github.com/magento/magento2/issues/17270)
- We should convert the CMS pages into an EAV model, so fields like `title, URL key and content` can be overridden/translated on a per store basis. Doing so, also makes it possible to link multi-language content using "hreflang" and module developers can have more options to expand on CMS pages.

- ## If you're familiar with #wordpress databases, you'll recognize the key-value (#EAV) structure. 
- https://twitter.com/LucasJohnston3/status/1610192301464100864
  - For Wordpress this structure allows flexibility in which data is stored for posts. That's why a post in WP can represent any sort of #data_entity. Admittedly with a performance penalty.
  - There is understandable criticism on the #eav_structure. 
  - But I'd argue it has proven useful for the world-leading #CMS of today (WP), so it can't be that bad.

- ## Has anyone in Laravel land integrated an EAV architecture into their app? If so, have any advice or gotchas to look out for?
- https://twitter.com/MarkShust/status/1698317826564505970
- 🤔 Please correct me if I’m wrong, but isn’t Notion’s database architecture basically just a giant EAV system?
- I would look further, salesforce is designed on top of eav too.

- I think, JSON column type wins over the EAV for attributes because of its simplicity and support on RDBMS level. MySQL allows to query and filter JSON fields very efficiently using indexes.

- One gotcha to any EAV is that excluding values on a search can also include the absence of the parameter. Test again 'null' for example should also test against not having the parameter in the join.
  - Searching on multiple parameters means a join for every one. It gets slow quick.
- ea filtering attributes is going to be a bit tricky, but I think it’s just an implementation detail. So long as indexes are set up, joins shouldn’t really mean a lot unless there are really a *lot* of attributes being joined in (hundreds). Can also always optimize for something like indexing to flat tables, but that definitely has a sense of some complexity.
  - Magento’s EAV structure of having a different table for each field type is probably the most optimal way to do this, but it’s inherently very complex, and I think starting out with the simpler table structure, one for E, A & V will be far easier to implement.

- Yeah Magento is a great example. And they also have an optimization where they compile the EAV to a flat table for speed
  - If anything, I think your right on the simple approach. Optimization can come later.
  - Might be cursing in church; but WordPress is a great EAV example.

- I have done that in the past on Yii being under impression of eav from M1. 
  - But nowdays I do not have that addiction. 
  - EAV is overvalued. We still end up by creating those attributes by data patch, means they are hardcoded. Adding static field to table covers most of requirements

- ## Friends don't let friends use the entity-attribute-value (EAV) model.
- https://twitter.com/pim_brouwers/status/1599862878932111360
- It's what drove me to project read-only views to lucene/solr/Elasticsearch so maybe you should?
  - Have a soft spot for EAV models if the usecase dictates it (rarely though).

- ## [Everything you wanted to know about SQL injection (but were afraid to ask) | Hacker News](https://news.ycombinator.com/item?id=6129669)
- Whereas traditional EAV is a triple - entity, attribute, value - Datomic is a quad. Datomic adds a timestamp and treats every value as an immutable fact at a point in time. Which is exceptionally valuable for highly regulated systems like finance, pharma and healthcare.
- yeah, Datomic is EAV (technically EAVT, it's event sourced so there is a notion of time and reads/writes need be acid with transactions and stuff) and EAVT can express even higher level queries than an ORM can, mostly because you can cache the indexes locally so you can do consistent read queries in your app process (Datomic's query engine is a library that runs inside your app, if cache is hot reads don't touch network... like git). From my understanding it doesn't have much to do with sparseness, though you certainly can support sparse objects performantly with EAVT.
  - EAVT/Datomic is a better fit for apps with complex structured data than an ORM over SQL, but migrating there is no trivial feat. Nor is convincing my customers in their due diligence phase, as they have surely been burned before by some kid pushing MongoDB, but they understand SQL and know the product can be successful with SQL, they know they can go get Oracle consultants to save their ass in 10 years when my company is sold, etc.

- ## [A humble guide to database schema design | Hacker News](https://news.ycombinator.com/item?id=22806142)
- I’ve been through this before: storing a couple addresses for a few hundred different countries in an otherwise very normalized RDBMS. We couldn’t figure out anyway to do it other than EAV tables and a defined attribute pattern for each country. Anyone come up with something better?
  - We went the EAV route instead of just a free form text field because we still wanted to expose discrete fields to in the UI and have some front-end validation. But sure, from a data integrity standpoint it’s no better than a text field.

- ## [SAML Is Insecure by Design | Hacker News_202108](https://news.ycombinator.com/item?id=28064835)
- What kills me about SAML is that instead of this straightforward XML style
  - It instead encodes elements and attributes using elements and attributes, in the manner of the classic "inner platform effect" anti-pattern
  - This is roughly the equivalent of the SQL table schema where there's one table with the columns "rowid, columnname, value" along with a "schema table" that some hand-rolled code uses to validate that the data table contains only data that is valid according to the schema.

- Btw I think your SQL example is called "EAV Schema" and does have a legitimate purpose once in a while.
- I've always wondered why more people didn't actually issue DDL for these kinds of databases. Like if you want to let your user define their own custom fields, just take what they enter and actually CREATE TABLE / ALTER TABLE to build the the tables they need. And then more or less you could just write regular queries.
- I've worked on a system like that, writing software on a project base for enterprise clients.
  - Turns out sysadmins get REALLY nervous when you tell them your application needs permission to use DDL at runtime. It required a lot more filling out forms.
- You can scope the DDL permissions to a single schema while still using the same database (and benefit from all the transactional guarantees a single database offers).
- Yes, if database supports it (I guess every major ones now do) then it's great. Postgres's transactional DDL seems like great fit.
- This is how arcgis works and it really sucks when your tier 1 starts adding columns to your schema because they made a typo.
- Some people do that, and at one point it was much faster to do that so it was more common, but as databases have generally gotten faster that kind of optimization is less interesting to people.

- these days if you are modeling the "sparse, high-dimensional data" of the kind that EAV schema does well, you probably should be reaching for JSON columns instead of EAV schema.
  - Some databases support "sparse columns", which use EAV under the hood but are better optimised
- Isn't that the problem that these "columnar store" DBs address?
  - A bunch of dictionaries containing UUID/data, where each dimension is its own dict, and the dicts might or might not be running on the same system?

- There's a reason for that. The attribute statement / attribute name / attribute value style has a consistent schema that won't change despite any custom attributes that are being added.

- Yeah, that's known as "entity-attribute-value model" (or just "EAV") and is considered an anti-pattern unless you actually need the flexibility it provides (which is fairly rare).
  - Yup. We run a system that uses this pattern for user-defined data fields. It works, but not without difficulty. It's very difficult to validate with business rules because you can't eliminate nulls and the "value" field is forced to be a character field. The system does have type checking enforced by the application, but multiple applications access the data.

- **Database EAV would likewise be 100% appropriate if users could use the database to store arbitrary attributes. (Think JIRA custom fields.)**
  - But if users are limited to certain attributes, then encode that in the schema.

- ## 💡 [Dynamic Django Models with Model Models | Hacker News_201808](https://news.ycombinator.com/item?id=17808442)
- It is essentially EAV isn't it? Well integrated into Django so it works with the admin and migrations.
- No it's not EAV. EAV is an sql (anti) pattern where you have a table with varchar fields such as name, type and value. This makes it very difficult to do aggregates and you can't do any consistency checks from the db.
  - **What the article proposes is much better than this: A way to create models (ie tables in the database) dynamically**. 
  - To make it more clear if you are not familiar with django, it'd be the same as if the `CREATE TABLE` sql was generated dynamically depending on the user selections.
  - So in this case each model will be in its own table and the fields will have proper types. You may even be able to have referential consistency using a ForeignKey field!

- I know it's possible to take the ModelModel approach a bit further and add ForeignKeys to it. **JSONField is like a better EAV, but it doesn't do dynamic relationships**.

- ## [Is JSONB + Postgres still a viable way of storing varying attributes? : rails](https://www.reddit.com/r/rails/comments/10x3x0d/is_jsonb_postgres_still_a_viable_way_of_storing/)
- Postgres jsonb columns will probably get you most of what you need, and even scale fairly well if you keep a few things in mind and plan ahead.
  - They're pretty efficient and queryable these days. I believe you can even use GIN indexes on data within the columns. The main downsides are a lack of column types (and therefore all the activerecord inference and other niceties) and needing to put a little more effort into setting defaults/checking if attributes exist
- I'd also highly recommend taking a look at the EAV (Entity Attribute Value) design pattern. I can't say whether it'd serve you better than JSON for your requirements here, but it's a great approach to "lots of dynamic/optional attributes" for records.

- Store model and store attributes gems makes jsonb first class activerecord members. Add gin indexes to the field and reads are just as fast as native fields. Writes are always slower

- Completely viable. And if you want formal, "validatable" data in your JSON you can always turn to JSON-LD or any of the other schema systems.

- We use it heavily in production everyday in our pg cluster and it has not failed us yet. Highly recommend!

- In my opinion JSONB is one of the many (or most) awesome aspects of Postgres.
  - It frees developers to have a hybrid sql/no sql datastore without using something like mongo (yuck).
  - u/demillir suggested the EAV (Entity Attribute Value) design pattern and I would avoid it like the plague.
  - JSONB is fast, easy to cache, and can expand or contract as needed - you'll just need some organization, discipline, and a ton of checks in your code as to whether or not an attribute exists.
  - After adding JSONB columns to very structured tables I haven't really had to run many (if any) db migrations.
  - The query syntax for JSONB syntax is a little weird, but once you get used to it it's pretty awesome - just make sure queries that need sums, totals, etc. are still in structured fields.

- ## [Anti relational pattern? : Database](https://www.reddit.com/r/Database/comments/ng7akp/anti_relational_pattern/)
- that's called Entity Attribute Value and is considered an anti-pattern
  - Use SQL Table Inheritance instead
- Nice SO answer. I always go for "Concrete Table Inheritance", then use a view to UNION if that's necessary.
  - The tables remain decoupled from each other which is important for keeping technology debt, and it's a very simple solution with no magic (like a Type field). Simplicity is way more important than DRY.
  - (I think that antipattern is also called "database in database")

- Which is fine if your DB platform supports table inheritance and your team knows the feature well enough to not make it a disaster.

- Most of my database have this design. It makes maintenance way easier as a user can define a new element without the need for a database structure change. This model also makes it very easy to generate JSON objects that a web page can use. Be sure to always indicate in the element constraints the real data type and precision.
  - The constraint table holds the definition of the element and then you can put all of the required data types in that such as if it's an integer whether it's a string a date things like that. You can also store validation methods there also

- So the EAV model you have here will work find with smaller amounts of data. However, things get really bad when your data grows. 
  - I remember, before the elastisearch implementation, there was an issue where a query with multiple properties checked would cause the ORM to create an insane sql query over 100k characters in length.

- I've worked with a few databases that have the need for this flexible metadata. PostgreSQL has both `hstore` and `json` datatypes that are ideal.

- I wish somebody would implement Dynamic Relational. Some domains could really use such. You can incrementally "lock down" columns and/or tables with stricter rules to gradually make it resemble current "static" RDBMS as projects mature.

- ## [Is Entity Attribute Value (EAV) the right move here? : SQL](https://www.reddit.com/r/SQL/comments/vvyi4f/is_entity_attribute_value_eav_the_right_move_here/)
- An EAV could work in your situation, however performance tanks hard when the database gets very large. Relational databases excel at structured data, and that is not quite what you want to store here. 
  - Perhaps you would benefit more from a different data store like a NoSQL solution.

- Nowadays I would almost always choose JSON over EAV to store dynamic (unknown) attributes.
  - Some DBMS also let you index the whole JSON value, so that you arbitrary query conditions can be supported by an index to increase query performance.

- ## [EAV - is it really bad in all scenarios? - Software Engineering Stack Exchange](https://softwareengineering.stackexchange.com/questions/93124/eav-is-it-really-bad-in-all-scenarios)
- Using an EAV structure for has several implications that are trade offs.
- You are trading off a 'less space for the row because you don't have 100 columns that are null' against 'more complex queries and model'.
  - Having an EAV typically means the value is a string that one can stuff any data into. This then has implications on validity and constraint checking.
  - The thing to realize here is that you can't use an index reasonably on the value. You also can't prevent someone from putting in something that isn't an integer there, or an invalid integer (uses '-1' batteries) because the value column is used again and again for different purposes.

- Some alternatives or modifications to the pattern to consider is instead of a free form key, to have another table with valid keys. It means instead of doing string comparisons in the database, you are checking against the equality of foreign key ids. Changing the key itself is done in one spot. You've got a known set of keys which means that they can be done as an enum.

- An example of this can be seen in the database model for Redmine you can see the `custom_fields` table, and the `custom_values` table -- those are parts of the EAV that allows the system to be extended.

- Note that Postgres actually stores JSONB, not plain text JSON, and it does support indexes on fields inside of a JSONB document / field, in case you discover that you actually do want to query against that data.
  - Also, note that fields within a JSONB field cannot be modified individually with an UPDATE query; you would have to replace the entire content of the JSONB field.
- Just to keep others on track, MS SQL was supporting XML columns with ability to index them for a while and starting from 2016 it can do the same with JSON (although JSON is not a native column type in MS SQL, you can still index it). 

- Storing EAV as one big table with three columns entity_id, attribute_id, value is an inefficient implementation of EAV. For more efficiency: attributes should be columns.

- ## [database - Which aspect of normal forms do entity-attribute-value tables violate, if any? - Software Engineering Stack Exchange](https://softwareengineering.stackexchange.com/questions/160700/which-aspect-of-normal-forms-do-entity-attribute-value-tables-violate-if-any)
- An EAV (aka Key-Question-Answer) table is technically in 3NF
- It's not Normalized
  - One of the Rules of Normalization is that : A field should have the same meaning in each row of the table

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

- ## [Django EAV 2 – Entity-Attribute-Value Storage for Django | Hacker News_201807](https://news.ycombinator.com/item?id=17628685)
- Or just use JSONField, because that’s exactly the reason why it exists.

- ## 👉🏻 [When to Avoid JSONB in a PostgreSQL Schema | Hacker News_201609](https://news.ycombinator.com/item?id=12408634)

- EAV is typically considered to be an anti-pattern for several reasons: 
  - it becomes very expensive to rematerialize a entity with all of its attributes/values, 
  - it becomes difficult to have any kind of constraints on the values (this is also a problem with jsonb), 
  - and it's hard for the database to maintain good statistics on the values of different attributes as most databases don't keep multi-column statistics. 
  - Don't worry, I've had similar ideas before.

- If you don't have JSONB, EAV is the only remotely-reasonable way to implement user-defined fields (e.g. product-specific attributes in e-commerce).

- If you want to allow user-defined fields in a relational database, your realistic are either EAV or stuff json into a text column. EAV, if done extremely carefully, can be a good solution, but 99% of the time, it's going to be a huge pain.
- You did see the article was about JSONB, which is significantly more sophisticated than "json in a text column", yes?
  - Yes, the person I was replying to was asking about what to do if you don't have jsonb.

- I used JSONB to keep the Tags on an object. Used to be EAV. Works way better here

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

- ## 🌰 [Adobe to Acquire Magento | Hacker News_201805](https://news.ycombinator.com/item?id=17121721)
- They had to adopt EAV database schema model because they want to design a schema that can be as generalized and flexible as possible. Obviously performance is the trade off. As a result, every Magneto shop has to use multiple layers of caching, which complicates the maintenance of Magneto, an open-source ecommerce off-the-shelf platform that's supposed to be easier than homebrew your own, ironically.

- Avoiding the EAV model while still being flexible (e.g. sparse attributes for any variety of products) is one place where the JSON datatype really shines. 
  - Throw your non-standard attributes into a JSON object and use the native DB functions to filter accordingly. 
  - In Postgres and MySQL 8 you can add conditional/functional/virtual indexes to keep things speedy. Maybe Magento will one day take advantage of these features.
  - It's basically a modern-day approach to Serialized LOB: https://martinfowler.com/eaaCatalog/serializedLOB.html

- ## 🌰 [Reddit's database has only two tables | Hacker News_201209](https://news.ycombinator.com/item?id=4468265)
- This is called eav
- They've built a database in their database. Also known as the **inner platform** antipattern

- Datomic takes similar approach. A unit of Entity, Attribute, Value and Time is called datom. Although in this approach we don't have to have schema, datomic forces us to define schema for some benefits.

- The last company I worked at made an application that used the Entity-Attribute-Value pattern in the database. The stated reason was to be dynamic, so we didn't have to worry about adding new columns and the associated downtime (assuming the DB got huge, which of course it would because this app would surely be a huge success). We had that problem on our main app (with 10s of millions of rows) where adding a column was always tricky, so I think management over-corrected. The other supposed win was that since the model didn't change, the code didn't need to be updated.
  - The data that was being stored fit into the relational model pretty well. But thanks to E. A. V. it was very difficult to query. The kinds of questions we often looked at (how many records from this zip code) would have been trivial without the E. A. V. Today you might use a NoSQL database (which were just starting to get noticed at the time), but in reality it fit into MySQL just fine.
- The real sad part is, we never used that functionality in the 2-3 years after it was developed while I was there. The app wasn't big enough for adding columns to take much time at all. All that "flexibility" we needed? We didn't use it, because it would have taken additional time to implement the additional front-ends and update the other backend systems.

- Wordpress uses the EAV db pattern too (have a look at the `wp_options` and `wp_meta` tables).
  - Of course, Magento and Wordpress use it in fundamentally different ways 
- Squiz's Matrix (open-source CMS) also uses an EAV model.

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

- ## 💡 [The Inner Json Effect | Hacker News_201607](https://news.ycombinator.com/item?id=12185727)
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
# discuss-rdf
- ## 

- ## What are the limitations of RDF (resource description framework) for modeling knowledge / discourse graphs?
- https://twitter.com/RobertHaisfield/status/1491131538075168769

- RDF is good for structured data. Knowledge/discourse isn't structured data. (At least not in a repeatable way. Lotsa people cargo-culting pseudo-data again....)

- Lack of edges. Isn't RDF modelled on triples rather than edges with properties?
  - I was under the impression that you can map one to the other but I feel like you're right actually, doesn't seem like it's fully mappable. In any case I find the triple model to be very confusing honestly. A model like neo4j does it feels much more natural.
- I agree, I definitely find it Neo4j a lot less verbose than RDF and a natural fit for record-centric storage & querying - the price being that it lacks RDF's granularity.

- RDF is still misunderstood, after 25y. It's abstract, implementation-agnostic. Its goal is interoperability. It's limited when used for graph analytics but coz it's not made for that. But that's solvable. It doesn't have built-in streaming capabilities, but that's also solvable.

- RDF itself is not very limited; it's extremely flexible. It can however be cumbersome, and it's a lot for people to learn.

- ## [Apache Jena | Hacker News_201903](https://news.ycombinator.com/item?id=19419025)
- Wikidata is built mostly on RDF ideas. For example, there's SPARQL query interface for it
  - Schema.org is heavily used by search engines and metadata in its format is found on many websites. It's an RDF-based format.

- I think Resource Description Framework (RDF) is overkill.
  - The underlying idea that is triple store (reminiscence of Entity-Attribute-Value model) is a good idea because it allows to model data with less overhead than a graph database will do over the same problem. Think of a list of items attached to a node or hypergraphs. All that is easier to do in a triple store.
  - Actually, I think that triple stores are not given enough buzz. Most of RDF buzz is around ontologies (aka. standard vocabulary for describing things). Datomic proves that triple store is a great idea in itself.
  - Datomic is RDF in disguise. That is, it implements a versioned triple store and a language similar to SPARQL (based on core.logic (aka. clojure's minikanren))).
  - When you think about it, a versioned database is a gem when it comes to debugging. Versioning a database is next to the best idea of the decade and that would not have been possible with another model than the triple store model.
  - The idea of database versioning or more generally versioning of structured data, especially versioning ala git is making its way

- if I were building a custom Knowledge Graph for a company or organization today, I would likely use a graph database like Neo4J. Maybe not though - it would depend on the application
- Really? Why not Jena or Marmotta with Postgres backend?
  - I can't speak for OP, but in my humble opinion, they don't really serve the same purpose. **Jena and Marmotta are implementation of standards**, while Neo4J is more of a proprietary system, and the underlying paradigm is different between triple graphs (for Jena and in a lesser dimension Marmotta) and property graphs (for most graph databases, e.g Neo4J, Apache Tinkerpop, OrientDB...).
- To make a very short summary, RDF is more concerned with the possibility to link data, so each piece of information is identified by a dereferencable URI, and can be described with an explicit model called an ontology (fancy word for a vocabulary used to describe data). 
  - On the other hand, Neo4J is more concerned with performance, but does not consider linking data accross the Web, or using an explicit schema. 
  - And for Marmotta, it is in kind of a bad place right now, the development seems a bit stalled, and the standard it implements is quite complicated compared to the majority of the problem it solves. 
  - This might evolve however, since Linked Data Platform (said standard) is now promoted by SOLID, a new initiative by Tim Berners Lee et al. to enable a truly distributed Web.

- If performance matters in any way then Dgraph and Neo4J are much much better. **Jena is a relic of semantic web past which you need if you want to do academic stuff like ontolgies, Owl, Sparql and inference**. But hardly for building 'real' applications for actual users and datasets.

- Different use cases. I think RDF/RDFS/OWL excel at combining different linked data sources with SPARQL queries. I think graph databases like Neo4J may be easier to work with if you are building a local knowledge base. These are just my opinions.

- What is the value offering on apache Jena?
  - RDF, and in particular OWL2 (reformulation of RDF tech based on description logic) is about decidable fragments of first-order logic, whereas Prolog is an existential Horn fragment on terms with Turing-complete extra-logical additions such as negation-as-failure and "cut" hence has undecidable decision problems.
- Not 100% certain, but I think the killer feature is the ability to manage your own data while exposing semantic representations that external apps can interact with.
  - The guiding idea behind RDF was (at one point) that users manage their own data while apps they give permission to can use that data.

- 👉🏻 Can anyone compare and contrast Jena in a Java project and/or operation against flat files with Neo4J or other graph systems?
  - **Jena is an RDF triple store whereas Neo4J, Memgraph, or JanusGraph, for example, are property label graphs**. Two different data models with distinct use-cases. I would compare Jena to other RDF engines like Stardog or Anzo graph
  - From a java project perspective, it doesn't really matter which one you choose as they all expose JDBC.

- ## [SPARQL Protocol for RDF | Hacker News_201706](https://news.ycombinator.com/item?id=14599462)
- Triple-stores can, but don't necessarily, layer on top of SQL databases. 
  - Jena has (had?) a triple-store engine that used JDBC to store the triples in a traditional relational database, but it's been deprecated for years in favor of a specialized engine designed specifically for storing RDF.
- Jena works for RDF data. But the OP is correct in their broader point that RDF is rarely a good choice and **SPARQL is a pretty horrible solution for querying it**.
- Jena works for RDF data. But the OP is correct in their broader point that RDF is rarely a good choice and SPARQL is a pretty horrible solution for querying it.

- We use quite a bit of SPARQL to reason over medical ontologies. It's not exactly "semantic web", but ontological knowledge (such as the Gene Database, UMLS, etc) are naturally serialized in graphs, which makes them an excellent fit for RDF triplestores, hence SPARQL. We regularly query millions of concepts with billions of relations in milliseconds. True, RDF under the hood is just a EAV model, but thinking about the identity between triples, graphs, and logic programming makes a lot of sense for us.

- ## [Update of the RDF and SPARQL (RDF star) families of specifications | Hacker News](https://news.ycombinator.com/item?id=36001509)
- RDF is not dependent on XML as a syntax. 
  - There's a text-based syntax in common use (Turtle), as well as a separate one based on JSON (JSON-LD).

- As well as a nigh tabular form in "N-triples" and "N-quads" which can end up as the easiest formats to work with sometimes.

- ## [The Future Is Big Graphs: A Community View on Graph Processing Systems | Hacker News](https://news.ycombinator.com/item?id=28499999)
- I only use RDF triples as a storage format for edges. I don't normally take advantage of triple stores (e.g. apache Jena), sparql query engines, etc.
  - It's just a simple format and it's easy to build different types of query/analysis capabilities around.
  - The only thing that's a little awkward is applying types to items in an rdf triple (in a way that's computationally cheap). Typing is a general problem, though.
- I strongly agree with this - RDF is fine and there are some great concepts in the SemWeb world (IRIs for example), but **OWL and SPARQL are confusing and can be off-putting**, especially when it is all rolled together. The latest iteration of our triple store actually moves radically towards linked-document or a 'document graph' to make it more understandable while keeping RDF at the base.

- 
- 

# discuss-triplestore
- ## 

- ## [I've been considering writing a graph database on top of SPARQL and RDF. Beyond ... | Hacker News](https://news.ycombinator.com/item?id=26782333)
- I've been considering writing a graph database on top of SPARQL and RDF. Beyond the official docs (which are pretty good), can you recommend any other resources for easily getting the hang of SPARQL?
  - I'll second the recommendation of Jena (and associated sub-project Fuseki). If you know Java (or any JVM language) you can use the Jena API directly for manipulating the triplestore, and submitting SPARQL queries. If you don't want to do that, Fuseki exposes an HTTP based API that you can interact with from any environment you prefer.

- ## 💡 [OrbitDB – serverless, peer-to-peer database on top of IPFS | Hacker News](https://news.ycombinator.com/item?id=18748542)
- I'm looking for a distributed scalable P2P triple store (or graph database) to store and retrieve RDF using SPARQL.
  - SOLID (Tim Berners-Lee, RDF)
  - GUN (ours, graph)

- ## 💡 [How should you build a high-performance column store for the 2020s? | Hacker News](https://news.ycombinator.com/item?id=15672027)
- I was under the impression, based on its docs, that Datomic only supports processing transactions serially through a single transactor.
  - To scale writes you shard writes. This generally means running multiple databases (in any DBMS)
  - The key insight is that **Datomic can cross-query N databases as a first class concept**, like a triple store. 
  - You can write a sophisticated relational query against Events and Photos and Instagram, as if they are one database (when in fact they are not).
  - This works because **Datomic reads are distributed**. You can load some triples from Events, and some triples from Photos, and then once you've got all the triples together in the same place you can do your queries as if they are all the same database. (Except **Datomic is a 5-store with a time dimension, not a triple store**.)
  - In this way, a Datomic system-of-systems can scale writes, you have regional ACID instead of global ACID, with little impact to the programming model of the read-side, because reads were already distributed in the first place.
  - For an example of the type of problems Datomic doesn't have, see the OP paragraph "To sort, or not to sort?" - Datomic maintains multiple indexes sorted in multiple ways (e.g. a column index, a row index, a value index). You don't have to choose. Without immutability, you have to choose.

- What is the primary reason people choose Datomic? From reading the website, I get the impression that the append-only nature and time-travel features are a major selling point, but in other places its just the datalog and clojure interfaces. I'm sure it's a mix, but what brings people to the system to begin with?
  - Immutability in-and-of-itself is not the selling point. Consider why everyone moved from CVS/SVN to Git/dvcs. The number of people who moved to git then and said "man I really wish I could go back to SVN" is approximately zero. Immutability isn't why. Git is just better at everything, that's why. Immutability is the "how".

- Datomic is essentially a triple store with a time dimension so it can do what triple stores do. What do you think the use cases are for a key-value-time store?
- If I understand Datomic correctly, I can think of the time dimension in the triple store as a sequence of transactions each of which produces a new state. How that maps onto real storage is flexible (Datomic supports a number of backends which don't explicitly support the notion of immutable database).
  - So what would a key-value-time store be useful for? Conceptually it seems that if Datomic triples are mapped onto the key-value database then time in Datomic becomes transactions over the log. So one area of interest is as a database backend for Datomic that is physically designed to be immutable. There is a lot of hand waving, and Datomic has a large number of optimizations. Thanks for answering some of those questions about Datomic. It's a really fascinating system.

- ## [there's also AllegroGraph product implementing triple store (kinda RDF) | Hacker News](https://news.ycombinator.com/item?id=15179)
- there's also AllegroGraph product implementing triple store (kinda RDF), that can be accessed via Prolog. 
  - i like that kind of data store very much -- it is as convenient as using plain objects, but supports complex queries, and do not have any additional layers like ORM.

- ## [Fabric – A simple triplestore written in Go | Hacker News_201908](https://news.ycombinator.com/item?id=20806916)
- What’s the industry take up of data stores like this? It always struck me as much more academic and not used as much in industry. 
  - Nubank recently raised $400M at a $10B valuation and they depend on Datomic heavily for their core systems.
  - The RDF database marketplace is very established [3], and the likes of MarkLogic, DB2, and Oracle have clearly encountered profitable reasons to add RDF support. I believe RDF has good traction in knowledge-intensive industry domains such as clinical research and life sciences.
  - Disclosure: I work on Crux which adds bitemporal versioning and eviction to a document->triplestore model running on top of Kafka.

- Triple relationships like the above are the kind of queries a Prolog engine can answer well (and far more).

- 🤔 **What's the use-case for a triple store vs a graph DB**? Social networks?
  - People also call triple stores graph DBs.
  - Triple stores support a disciplined set of primitive types that come from xml schema, so you have "xsd:integer", "xsd:datetime", "xsd:decimal", really the critical things that are missing in JSON. That is, there is a kind of fact where the object is a literal.
  - Triple stores also support facts where the object is an identifier for another object. That could be a URI which names it, or it could be an internal "blank node" identifier.
  - Other kinds of "graph database" have different semantics, for instance they might not have support for literals, or have a different set of literal data types, or they might let you attach facts to the edges (hypergraph, property graph, ...)

- ## [Google Badwolf: Temporal graph store abstraction layer | Hacker News_201510](https://news.ycombinator.com/item?id=10432071)
- Badwolf is a immutable triple store with temporal predicates.

- 🤔 **Why is this better than just using any SQL database?**
  - Lots of SQL databases don't have good constructs for dealing with ranges, which make lots of operations you'd want to do with temporal data awkward (PostgreSQL since 9.2 has range types, and lots of useful features attached to them, that address this.)
  - Beyond that, pretty much all the normal SQL vs. NoSQL considerations would seem to apply without much change when you address temporal data, so the usual mix of ACID vs. scalability, schema enforcement vs. schemaless flexibility, etc., considerations apply.
- If you want to know the advantages of triple stores, there's a lot out there.
  - One key strength is that **triple stores have a "schema as data" approach**, meaning that schemas can be made to follow rules on the fly based on the data contained within them. Nothing that application code can't do, of course, but the entire purpose of these kinds of databases is to find a way to have data be as self-descriptive as possible.
- **Triplestores are good for storing and processing graphs**, which don't fit the relational database model very well. There is a variant of SQL called SPARQL intended specifically for querying triplestores
