---
title: lib-db-app-community-model-graph
tags: [community, graph-database]
created: 2023-10-26T15:04:15.201Z
modified: 2023-10-26T15:04:42.968Z
---

# lib-db-app-community-model-graph

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 

- ## 🕸️🔥🔥 [Postgres as a graph database | Hacker News_202303](https://news.ycombinator.com/item?id=35386948)
- I designed and maintain several graph benchmarks in the Linked Data Benchmark Council, including workloads aimed for databases. We make no restrictions on implementations, they can any query language like Cypher, SQL, etc.
  - In our last benchmark aimed at analytical systems, we found that SQL queries using WITH RECURSIVE can work for expressing reachability and even weighted shortest path queries. However, formulating an efficient algorithm yields very complex SQL queries and their execution requires a system with a sophisticated optimizer such as Umbra developed at TU Munich. Industry SQL systems are not yet at this level but they may attain that sometime in the future.
  - **Another direction to include graph queries in SQL is the upcoming SQL/PGQ (Property Graph Queries) extension**. I'm involved in a project at CWI Amsterdam to incorporate this language into DuckDB.
- This same technique - WITH RECURSIVE - is also supported by SQLite.

- Take a look at RDFox, unlike postgres where you can only derive a column from another column once, you can't derive a column from a derived column, RDFox can derive unlimited columns or even objects through rules incrementally. Kind of like unlimited chaining of materialized views

- I do love PostgreSQL, and I often reach for this approach when working with hierarchical data, but a word of warning: Recursive queries will not scale to handle _very_ large edge tables. The recursive query will always consider _all_ edges, even when the outer query seeks only a single node's relationships. The solution is to build and index denormalized n-th order relationship tables.

- I've since worked on SpiceDB which scales much better by taking the traditional design approach for graph databases and **only treating Postgres as triple-store**. IME, there's no short-cut: if you need a graph, you probably want to use a database optimized for graph access patterns. Most general-purpose graph databases are full of optimizations for common traversals that are uncommon operations in relation databases.

- Postgres is powerful. I've implemented graph DB, mapreduce, huge sparse matrix math (which was cool), and ofc a KV store with it. With actual performance benefits over the alternatives. It's not very ergonomic for those, but it works.
  - That said, I've had so many jobs where the team decides to fit our whole data model into a fully recursive graph, and it's been a huge mistake every time regardless of whether they use Postgres or a dedicated graph DB. 
  - **Just because you can do it (you always can!) doesn't mean you should**. 
  - Start with just a traditional n-hierarchy schema and only look at modeling things as a graph if you're sure it's necessary. Usually it's not. Sometimes you'll have a mostly non-graph schema with a couple of graph tables for the things that really need that.

- ## 🕸️🔥 [Show HN: Simple-graph – a graph database in SQLite | Hacker News_202012](https://news.ycombinator.com/item?id=25544397)
- I did something similar recently, a block store for a rust implementation of ipfs, which models a directed acyclic graph of content-addressed nodes.
  - I found that performance is pretty decent if you do almost everything inside SQLite using WITH RECURSIVE.

- if you're looking for more hierarchical support, SQLite does has a transitive closure extension that might be of some assistance
  - [Querying Tree Structures in SQLite using Python and the Transitive Closure Extension](https://charlesleifer.com/blog/querying-tree-structures-in-sqlite-using-python-and-the-transitive-closure-extension/)
- I've actually been working on an extension to perform breadth first search queries in SQLite on general graphs. The extension is actually based off of the transitive closure extension. 

- Why not add that functionality directly to SQLite via stored procs*
  - [Code Generator for SQLite | CG/SQL](https://cgsql.dev/)

- How does this perform compared to a “native” graph database like Neo4J?
  - I would benchmark the tasks "traversal", "aggregation" and "shortest past" for a 10k to 10M node graph. Anything under 10k would be good enough with most techs and over 10M need to consider more tasks (writes, backup, the precise fields queried can become their particular problems at larger scale).

- 👉🏻 There has been a lot of progress on creating standardized query languages for graphs. The two most notable ones are [2]:
  - SQL/PGQ, a property graph query extension to SQL is planned to be released next year as part of SQL:2021.
  - GQL, a standalone graph query language will follow later.
  - While it is a lot of work to design these languages, both graph database vendors (e.g. Neo4j, TigerGraph) and traditional RDBMS companies (e.g. Oracle [2], PostgreSQL/2ndQuadrant [3]) seem serious about them. And with a well-defined query language, it should be possible to build a SQL/PGQ engine in (or on top of) SQLite as well.
- SQL/PGQ and GQL target the property graph data model and support an ASCII-art like syntax for pattern matching queries (inspired by Cypher). They also offer some graph traversal/shortest path operations (including shortest path and regular path queries). Additionally, GQL supports returning graphs so it's queries can be composed.

- It depends on how the graph is stored in the database. In this project the nodes ids are TEXT so it will likely not scale very well. I know because I use a similar implementation with GUID as string in Sqlite in a project since a couple of years and while it works fine for the graph I have (<1 million nodes, few edges per nodes) it won’t perform too well past that.

- ## 🆚️🔥 [Bullshit graph database performance benchmarks | Hacker News_202301](https://news.ycombinator.com/item?id=34342371)
- 
- 
- 

# discuss-graph-query
- ## 

- ## 

- ## [SQL:2023 is finished: Here is what's new | Hacker News_202304](https://news.ycombinator.com/item?id=35562430)
- I don't believe that adding property graph support to SQL makes much of a difference for SQL and relational databases...
  - However, the PG query additions (I believe they are close to the Cypher language neo4j) being part of the SQL standard will give a boost to marketing and adoption of PG databases. 
  - Vendors can now say "our language follows the SQL standard" instead of referencing cypher and indirectly neo4j. Even if neo4j may have the best intentions, marketing is very important in databases and it is unlikely that vendors could have supported Cypher and thus admit that they are following neo4j rather than leading.
- I think SQL/PGQ have the potential to outright kill the whole field of PG databases (if/once existing databases actually start implementing it).
  - The big marketing claim of Neo4J & friends has always been that they make graph queries possible, with a big portion of that claim being that those queries would be intractable for RDBMs performance-wise.
  - With SQL/PGQ it becomes quite apparent that there is next to no magic sauce in PG databases and that it's all just syntactic sugar on top of node/vertex tables. All the rest of their query plans looks 1:1 what you'll find in a RDBMs. Now that they are on a level playing field query syntax-wise, PG databases will have to compete against RDBMs with a lot more advanced query optimizers, better administrative tooling etc..
- This is my expectation as well. At CIDR this year there was a paper that presented an implementation of SQL/PGQ in DuckDB, and it outperforms Neo4J in a few selected benchmarks

- In relational databases, the property graph queries can be really effective to write authorization queries.

- Cypher has built-in support for traversing relationships between nodes in a graph, which can be more intuitive and efficient than using SQL to join tables.

- ## 🆚️ [Can you elaborate on "datalog queries blows SQL out of the water"? | Hacker News](https://news.ycombinator.com/item?id=13058399)
- 🤔 at my company we're heavy users of Datomic
  - Declarative and pattern matching make it elegant to read.
  - Syntax more appropriate for code generation and introspection (since it's just a bunch of nested lists). A big plus when pairing w/ Clojure.
  - Allows recursive queries.
  - You can reference metadata associated to any transaction that ever touched any attribute in your database within the same query constructs.
  - You can easily query the entire history of records.
  - You can easily execute a query against how your database looked like months ago using as-of

- 🤔 I'd be interested to know if anyone has compared Datalog and Neo4j/Cypher.
- Neo4j focuses on modeling nodes and it's relationships, and allows you to attach metadata to the later, but doesn't really have transactions as first-class objects.
  - Datomic focuses on modeling facts (entity-attribute-value). This is a very stable data representation that allows modelling tables, documents or graphs, on top of carrying transaction explicitly on an additional index for the time-travel magic.
  - I guess Neo4j might make a good DB for ETL-ing into and running certain kinds of analysis.
- **Cypher doesn't have named queries** (and thus not recursive ditto either), AFAIK. 

- ## [Composeability is front and center in GQL, so you may want to consider it. | Hacker News](https://news.ycombinator.com/item?id=22872470)
- Cypher is by far the biggest graph query language and they seem to have the most weight in the conversation so far, but we are going to try to represent datalog as far as possible. 
  - Even if woql isn't the end result, we think datalog it is the best basis for graph query so we'll keep banging the drum (especially as most people realize that composability is so important)

- ## 💡🔥 [New Query Language for Graph Databases to Become International Standard | Hacker News_201909](https://news.ycombinator.com/item?id=21004115)

- GQL will be a declarative language in the spirit of existing property graph query languages like Cypher, so that gives you an idea. 
  - Yup, you can think of ISO GQL as the future of Cypher.
- Is GQL a new name for Cypher?
  - Sort of. ISO **GQL is largely about taking the best ideas from Cypher** (and other graph query languages) into a language overseen by an international standards body backed by multiple companies and implementations.

- 🤔 **What's wrong with SPARQL?** What advantages has this over SPARQL?
  - Very few real advantages on a technical level.
- Currently it is relatively difficult to move data from one (open)cypher implementation to an other. Also as support is uneven for all features it is not so simple to get started on Neo4J and then evaluate e.g. TigerGraph if you find that Neo4J is not ideal for your usecase.
  - If your application only uses GQL then you could start on Neo4J but after two years in production cheaply move to a competitor. By just switching your backend and run your test cases etc. your data did not change, your queries remain the same, so evaluation is relatively straightforward.
- SPARQL is purpose built for the RDF world where you're mixing and matching a zillion different vocabularies, all of which have to be painstakingly declared and name spaced every time.
  - For most of us working not on the "semantic web", we typically only have 1-2 vocabularies, which is our data model, and SPARQL is super clunky to use.
- SPARQL requires buy-in into the world of the semantic web even when all you want to do is store and query graph data.
  - Also, property graphs wouldn't have managed to get the traction they have if SPARQL would have been sufficient. SPARQL simply suffers from being designed in a way that does not sufficiently address the needs of application developers, in expressivity, ease of use, let alone allowing easy migration of existing relational data by sharing the same type system with SQL.
- Not true at all. You can query an RDF dataset with SPARQL and not have any RDFS/OWL schema. A schema/ontology/vocabulary gives you a domain model, but it’s optional.
- SPARQL doesn't allow unbound recursive queries.
- SPARQL suffers from Not Invented Here Syndrome.
- SPARQL is for RDF data, which not every graph database conforms to.
- SPARQL is not as easy to read. I can show SQL or Cypher

- GraphQL has nothing to do with graph databases.
- GraphQL is about modeling business domain objects in graphs [0] and querying them. Isn't that basically what Graph DB languages do too?
  - It is a query language for APIs, name like RestQL or JsonQL would be much more suitable.
  - The expressiveness of GraphQL is severely limited, it doesn't allow you to express even simple patterns like triangles, depth n, paths etc..
- Exactly. **GraphQL solves the same problem as REST. It is not a graph query language despite its unfortunate name**.

- It would be nice if there were layered language approach, with a core Datalog/SPARQL-like core language specified first, then the sugary language that target it.

- ## 🆚️ [Graph query languages: Cypher vs. Gremlin vs. nGQL | Hacker News_202003](https://news.ycombinator.com/item?id=22482665)

- 'GQL is an upcoming International Standard language for property graph querying that is currently being created. The idea of a standalone graph query language to complement SQL was raised by ISO SC32/ WG3 members in early 2017, and is echoed in the GQL manifesto of May 2018.
  - GQL supporters aim to develop a rock-solid next-generation declarative graph query language that builds on the foundations of SQL and integrates proven ideas from the existing openCypher, PGQL, GSQL, and G-CORE languages.

- Datalog is such a delight to use especially since queries are just data structures are just code. 
  - Once the basics clicked I felt empowered to do anything in Datalog, while I feel like I always have to learn or remind myself of more syntax when I want to do anything fancy with SQL.

- I agree that SPARQL must be considered, and so must Datalog and Prolog. Idk but I'm starting to believe that new-fangled standardization efforts (if you want to call those that) are starting over from scratch and actively avoid looking at prior art as a generation thing.
  - Though I could see **why someone wouldn't like SPARQL and RDF**, with its bulk reuse of other W3C and TBL concepts such as URLs, resulting in atom and predicate names verbosely and pointlessly beginning with "http://".
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 🕸️🌵🔥 [RecallGraph – an open-source graph database, for version controlled graph data | Hacker News_202006](https://news.ycombinator.com/item?id=23455516)
- 
- 
- 

- ## 🔥 [RedisGraph: a fast, queryable property graph database for Redis | Hacker News_201810](https://news.ycombinator.com/item?id=18270996)
- 
- 
- 

- ## 🔥 [Basic terminology and practices related to graph databases and graph modeling | Hacker News_202303](https://news.ycombinator.com/item?id=35041873)
- 
- 
- 

- ## 🔥 [Show HN: Nebula – a distributed graph database written in C++ | Hacker News_202001](https://news.ycombinator.com/item?id=22051271)
- 
- 
- 

- ## 🔥 [High-Performance Graph Databases | Hacker News_202305](https://news.ycombinator.com/item?id=36022042)
- 
- 
- 

- ## 🤔🔥 [Why Nasa Converted Its Lessons-Learned Database into a Knowledge Graph | Hacker News_201902](https://news.ycombinator.com/item?id=19095849)
- 
- 
- 

- ## [dgraph: Build your next app with a graph database | Hacker News_202007](https://news.ycombinator.com/item?id=23783923)
- 
- 
- 

- ## [What Every Competent Graph DBMS Should Do | Hacker News_202301](https://news.ycombinator.com/item?id=34358912)

- SQL is getting a Property Graph Query extension that should finally match the ease of querying of typical graph DB. That said, RDBMS should cover the basic use case quite well unless you are doing very exotic things with network analytics and such.
  - Yes, this will be interesting to see. This is the SQL/PGQ extension that's coming in 2023. On the one hand, as I articulate in my post, GDBMSs are based on relational principles, so building a system that can seamlessly query in relational and graph model is a good idea. On the other hand, there is this: (1) no SQL extension into a graph-based model has been successful historically (e.g., into RDF or XML or even json). That seems to confuse users, so sticking to a single model seems like a good idea. (2) RDBMSs that implement SQL/PGQ will not be very performant unless they change their cores with several techniques I and my research group has been advocating for (e.g., how to do predefined joins, worst-case optimal joins, factorization etc.).

- As I say in the blog, there is no perfect data model. RDF is great fit for certain things, e.g., when storing dbpedia-like datasets, and doing "automatic" advanced OWL reasoning over it by implementing OWL rules. 

- You can search for this on the link: "GQL will incorporate this prior work, as part of an expanded set of features including regular path queries, graph compositional queries (enabling views) and schema support."

- Kùzu is currently integrating Arrow not as a core storage structure but as a file format from which we can ingest data. We are writing Kùzu's entire storage, so it's our own design. It has three components: Vanilla columns for node properties, columnar compressed sparse row join indices and relationship properties, and a hash index for primary keys of node records. We don't use Arrow to store db files.
  - For serializability: yes, we support serializable transactions. So when you insert, delete or update node, rel records, you get all or nothing behavior (e.g., if you rollback none of your updates will be visible).
  - That said, supporting ACID transactions is a completely separate design decision in DBMSs, so our (or other systems') mechanisms to support transactions (for example whether it's based on write ahead logging or not) and storage designs are generally mutually(相互地；共同地) exclusive(独有的; 专有的; ) decisions.

- ## 🤔 [Ask HN: Why are relational DBs are the standard instead of graph-based DBs? | Hacker News_202110](https://news.ycombinator.com/item?id=28736405)
- Yet a relational database in 5th normal form is equivalent to a RDF-Like first order Triple graph.
  - Not quite. The definition of 5NF depends on real-world constraints on valid combinations of attributes in the database; it has nothing to do with any pre-defined data model such as RDF. There can be "wide", horizontally-modeled tables (quite unlike the RDF model) which are in 5NF simply because no real-world constraints apply to the data beyond those that are implied by the candidate keys.

- I'm a huge fan of LogicBlox and RelationalAI, and the research done at both had a huge impact on me as an undergrad! While you're here, could you provide some insight on why you folks went with arbitrary width tuples for your datamodel? Limiting youself to triples seems to drastically ease the implementation of WCOJ algorithms without much loss of expressivity, and provides compatibility with existing RDF research.
- With triples you need to reify hyper edges into nodes (a relation is just a hyper edge). This can lead to pretty awkward models, for example for temporal data. Most graph databases (eg Neo4J) have the same limitation and as a result struggle with temporal data or other higher-dimensional data.
  - We prefer to support general relations (hyper edges) and face the complications of query planning. We really want a general relational system that decouples the complications in query processing from the way you need to model your data and write your queries
  - This gets particularly important for what we do besides graphs: we also aim to support machine learning workloads (we have some references to papers on our website).
  - We still do automatic index selection, but indeed it is important that you do not create too many of these unnecessarily if you relations with arity bigger than triples.

- ### [Ask HN: Why are relational DBs are the standard instead of graph-based DBs? : programming](https://www.reddit.com/r/programming/comments/q0g48b/ask_hn_why_are_relational_dbs_are_the_standard/)
- apparently reddit did this at the start
  - Some parts of this were moved into Cassandra when I was at reddit in 2014-2015, but a lot was still in Postgres. I don't think they really tried to get rid of Thing until a couple years after that, and it wouldn't surprise me if a lot of still there.
- However you usually want to avoid using EAV unless you have no alternative. Performance is usually miserable and you lose most of the advantages an RDBMS offers.

- Exactly the process taken by Apache AGE.

- Unlike some other commenters, I agree that graph models are usually a better fit for most data than relational models. There's been some interesting work in recent years developing this idea: in the Clojure world there's Datomic, XTDB, and a host of competitors, all of which build on work from Semantic Web/SPARQL/triplestores and logic programming.

- Datomic is brilliant imo due mostly to event sourcing at the data layer

- Hierarchies have arguably been a weak spot in relational. However, a good set of API's or new SQL key-words could improve this area. While doing such may not make it better at trees than Datalog, it could at least make it "good enough". Apps that need hierarchies typically also have non-tree needs (queries) such that switching the entire database to Datalog may not be justified(为（某事）的正当理由). It's rare you only need tree-oriented queries.

- ## [Show HN: EdgeDB 1.0 | Hacker News_202202](https://news.ycombinator.com/item?id=30290225)
- EdgeQL is designed to replace SQL, not graph query languages. 
  - Think of it as SQL getting a proper type system and GraphQL capabilities of reaching into deep relationships in an ergonomic way.

- SC32 WG3 is developing two related standards to support property graphs:
  1. SQL/PGQ (ISO/IEC JTC1 9075 part 16) -- This adds language to create property graph views on top of existing SQL tables and write property graph queries in a GRAPH_TABLE function in an SQL FROM statement.
  2. GQL (ISO/IEC JTC1 39075 Database Language GQL) -- This is a full declarative property graph database language to create, maintain, and query graphs. This includes support for both descriptive and prescriptive schemas.
  - **The Graph Pattern Matching language is identical between the two standards.**

- ## [Neo4j raises $325M series F | Hacker News_202106](https://news.ycombinator.com/item?id=27541453)
- Historically, graph databases did a passable job of supporting data models and queries that were not really possible in SQL (absent proprietary, vendor-specific extensions). 
  - That's all over now, because recent versions of SQL support recursive queries that can handle general graphs quite easily. 
  - No real need for a specialized solution, even plain vanilla Postgres is good to go.
- Sql syntax for such queries is super awkward with tones of gottyas, not sure how performance compares

- 👉🏻 Something I just found out after looking into status updates on the Property Graph Query (PGQ) work being done in SQL, is that it will exactly mirror the work going into GQL (Graph Query Language, a newish standard in its early stages of development based mostly off of Neo4j's Cypher).
  - GQL (ISO/IEC 39075) is a full database language to create and manage property graphs and create, read, update, and delete nodes and edges (or vertices and relationships)
  - SQL/PGQ (ISO/IEC 9075-16) is a new add-on part of the SQL standards which introduces the capabilities to create property graph views on top of existing tables in an SQL database, as well as the ability to query property graphs using a GRAPH_TABLE function in an SQL FROM clause
- The input to the SQL/PGQ GRAPH_TABLE function is a property graph query, sometimes referred to as Graph Pattern Matching or GPM. **Graph Pattern Matching is common between SQL/PGQ and GQL**. **That is, the syntax accepted in a GRAPH_TABLE function in an SQL FROM clause is identical to the syntax in a GQL graph query**. Because GPM is the same in both draft standards, changes to GPM for SQL/PGQ also apply to the GPM portions of the GQL specification.
- I also just came across the Apache AGE project which basically allows you right now to extend PostgreSQL DBs with property graph capabilities and enables full(?) use of Cypher/GQL.

- Also, **nested sets and materialized paths have been around forever to do graphs inside SQL**.

- According to Crunchbase, Neo4j was founded in 2007! Is this correct? 14 years in and they are still raising VC money!?

- ## 🕸️🔥 [PageRank algorithm for graph databases | Hacker News_202301](https://news.ycombinator.com/item?id=34577832)
- is there a good "graph layer" for SQLite? I understand that graph databases use specific data structures to optimize for graph queries instead of row-oriented but sometimes you need something in the middle: representing graphs and doing basic queries.
- It's nearly a decade old at this point and probably not optimal even for the time, so there may be better approaches, but here's a few basic algorithms on SQLite. PageRank is at the bottom.
- Common graph databases are network-based for scaling purposes. You do have a database server then you talk to the server somehow for the queries. Sqlite is a single-file database. You do not have a server so you do not need an extra layer in database side.
  - Instead, Run the graph algorithms on a stringified json stored as a text in sqlite. They will be running in some process in anyway.

- ## 🔥 [Ask HN: What was your experience using a graph database? | Hacker News_201812](https://news.ycombinator.com/item?id=18795498)
- 
- 
- 

- ## 🔥 [Ask HN: If you've used a graph database, would you use it again? | Hacker News_201803](https://news.ycombinator.com/item?id=16542183)
- 
- 
- 
