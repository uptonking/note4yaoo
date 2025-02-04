---
title: lib-db-app-blog-stars
tags: [blog, database]
created: 2023-09-16T17:49:18.664Z
modified: 2023-09-16T17:49:28.532Z
---

# lib-db-app-blog-stars

# guide

# blogs

## 💡 [The Strength of the Record · XTDB Docs](https://docs.xtdb.com/concepts/strength-of-the-record/)

- There is some surface area to a database that allows us to store, query, and listen. This is our user interface. It is also our storage metaphor.
- 👉🏻 Storage metaphors come in three broad structural categories: rows in tables, documents in trees, triples in graphs. 
  - These structures, in turn, are bound to a three-dimensional field. 
  - Our X-axis is schema, from hard to soft, our Y-axis is depth, from flat to nested, and our Z-axis is shape repetition, from regular to unique. 
- Rows in a relational database table will subscribe to a hard schema, a flat depth, and a common shape. 
- Document stores will subscribe to a softer schema, a nested depth, and (potentially) unique shapes. 
- Triples do not dictate schema by their nature but they have negligible(不重要的；很小的) depth and negligible variety. The uncomplicated nature of triples is reminiscent(引起联想的, 提示的) of LISP’s absence of syntax. That makes them attractive…​ but esoteric(只有内行才懂的；难懂的).

- Tables: the hometown favourite
- A table is an intuitive concept, even to children. But we all know, just as my teacher understood, that text in an arbitrary table is effectively meaningless, text in a spreadsheet table is meaningful but unconstrained, and text in a database is constrained by datatype. 

- Documents: structs, trees, and nests
- An object isn’t a simple or intuitive concept; an object is type-matching dynamic dispatch implemented over a collection of closures which in turn share a second collection of lexically-bound variables which themselves are — you guessed it — more objects.
- Document DBs, on the other hand, were not such a bad idea. They were just poorly implemented. Standard query languages? Nope. Schemaless? Nope. Relationships? Not really. Append-only, immutable data? That gets pretty expensive when you denormalize all your records into a deeply-nested rat’s nest.
- MongoDB lacked basic joins until version 3.2 but this was an honest mistake. MongoDB engineers believed their customers could survive on schemaless, denormalized data with no relationships. We now know this isn’t true. All databases have schema. All databases have relationships. Our schema and relationships may be implicit but they are truths we must face.
- Neo4j, on the other hand, is a document database that actually works. Neo4j is a property graph and property graphs do not pretend relational data doesn’t exist — or that it exists but somehow isn’t important. Unfortunately, Neo4j has its own homebrew query language, Cypher, with its own baggage. Although an open standard since 2017, Cypher queries are difficult to compose because the language lacks a foundation in logic
- Rather than hide behind a deeply-nested document model or inglorious query languages, we can put our faith in decades of research. 

- Triples: oh, the trouble with triples
- I was excited about the possibility of Clojure-style simplicity in database form: The triple-store.
- Roughly, there are two categories of triples: **RDF triples**, which attempt to encode relationship semantics, and **EAV triples**, which only encode the relationship
  - A semantic triple might look something like `[Bob belongs_to CommunistParty]` where an EAV triple is more likely to take the shape `[Bob :party CommunistParty]`.
- Rather than debate the semantics of semantic triples, we’ll treat them as loosely equivalent for this story. Caveat lector.
- My team was immediately attracted to triples. The declarative logic of Datalog, with its Prolog origins, felt like the perfect way to ask questions of a database. Having never worked with triple-stores before, there was a purity to EAV triples none of us had ever imagined possible during our career with relational databases. An immutable store of pure facts? Count us in!
- Back in 2014 our triple-store of choice had a hard schema, not unlike the schema definitions in most relational databases. However, it went so much deeper than that. 
- In retrospect, it feels as though there must be an underlying reason RDF has never enjoyed general database success. Despite more than two decades of research and implementation, RDF remains the storage metaphor of museum artefacts and government statistics.
  - The elevation of purity above all else is a certainly one problem with triples. 
  - Their true deficiency, however, is hidden in plain sight: **triples by their very nature only describe relationships**. 
  - Despite their name, relational databases consign(移交；交付) the very notion of a "relationship" to the realm of the derivative. 
  - Triples have the opposite problem. Triples treat nouns as second-class citizens.

- Enter The Record
- relational databases fail the dictionary definition. Most lack a meaningful, first-class representation of time with which to view the past. The flip side of that coin is the absence of immutability.
- Triples fail our mental model instead. The client record card is natural. Specifying each individual fact about your client is not. If we want to see that natural record, triples force synecdoche on us.
- It is possible to find a middle path between hard, flat rows in tables and infinitely malleable(容易改变的，易受影响的) triples. Surprisingly, documents are that middle path.

- Records: doing documents right
- "Flat is better than nested" is a guideline, not a rule.
- To ensure nothing crazy will ever happen, our storage metaphor of "documents" must play by the rules. The dictionary says our database must store immutable facts on a timeline. Computer Science says our database must speak a standard query language. Our experience and intuition says our database should provide us lightweight references between our documents and discourage deep nesting.
- These are not abstruse or mystical ideas, but they do demand a reappraisal of the database. We can’t just tack immutability onto MongoDB or temporality onto Postgres. We must rebuild the foundation. We must record a graph of immutable facts on a timeline tolerant of growth and query them by time-aware logic. That’s a mouthful, so let’s just call it a Record. This is the new metaphor.  
# blogs-sync/change-data-capture

## [Change Data Capture in practice 2_202310](https://medium.com/fever-engineering/implementing-change-data-capture-in-practice-part-2-89e6b8d4fdd)

- Implementing Change Data Capture was relatively easy, but along the way we found some challenges that we did not foresee. 
- Limited availability of previous values
- PostgreSQL TOASTED fields
- Schema evolution
- Handling tombstones

## [Change Data Capture in practice 1_202309](https://medium.com/fever-engineering/implementing-change-data-capture-in-practice-part-1-38259260d9a2)

- As software systems move towards models of distributed data, more and more copies of the same information are required, each of them reformatted for a specific purpose. 
  - The copying process takes time, but users expect a unified view of the system as if the source of all information was the same.
- 👉🏻 One of the solutions to address this replication challenge in a scalable way is known as **Change Data Capture (CDC)**: 
  - capturing and publishing changes made to the primary source of the data, known as the system of record; 
  - and then listening to those changes in the derived systems to keep a near-real-time up-to-date copy of the information.

- This post explores the reasons why we decided to adopt this technology at Fever and how we implemented it. 

- Our platform receives tens of thousands of requests per minute and as such, we’re always looking to continue growing while offering the best user experience, which ultimately, is what drives us to use techniques such as Change Data Capture.
- As a platform offering a huge variety of experiences, ranging from art exhibitions or beer tasting sessions to big stadium-filling events, there is no one-size-fits-all alternative for the purchase flow.
- For the different selectors to work, we need aggregated information about all the sessions of the experience, which in quantity, could range in the thousands depending on the kind of event. 
  - At first, the aggregations were happening each time a client visited the page, but shortly after, we decided to **use PostgreSQL materialized views as a simple way to pre-compute them**. 
  - They were calculated every minute, and were working perfectly fine for our needs at the time. 
- After a certain point, our database was struggling to compute the materialized views, and this is a use case where near real-time is important because it has a direct impact on sales. 
  - To put this into numbers, the total database execution time of the refresh process for the calendar materialized view was 7.05 minutes per hour. 

- At the heart of every data use case, from recommendation algorithm execution to partner-facing dashboards, lies the Data Warehouse (DWH). This is where information from multiple sources is gathered, curated and organized using Apache Airflow.
  - Airflow is based on the concept of DAGs (Directed Acyclic Graphs): collections of tasks that constitute a batch data processing job, most of which are used as ETLs (Extract-Transform-Load) and scheduled to run at a configured interval. 
  - These processes are heavy by nature, and even though a lot of optimizations are regularly done, they have one essential shortcoming: they work by “pulling” rather than “pushing”.

- When analyzing all of these issues, the first idea that came to mind was to use domain events to swap from a pull to an incremental push model by subscribing to the events from each derived data system. 
  - The first problem of using domain events here is the initial synchronization.

- smart people in the software world already came up with a solution for this issue: Event Sourcing. 
  - The idea is to have the application’s source of truth be an append-only sequence of domain events so that the current state of an application is determined by examining all change events associated with it since its inception, rather than saving only the current state. 
  - This allows applications to rebuild the state at any point in time by replaying events.
- we discarded event sourcing as a valid solution for our issues, mainly for 2 reasons:
  - Having the source of truth be the domain events requires a profound technical and mentality change that was not worth the cost for us. migrating our core application’s main design is too high a price to pay for the data integration problem we’re trying to solve.
  - There are many legacy use cases without domain events integration. One of the most prevalent entities in the derived data systems is our Session, and a quick usage search for this entity in our main application yields 723 usages. 

- The solution - CDC
- Having discarded replication at the domain level, we started looking for replication solutions at the infrastructure level, and thus arrived to Change Data Capture (CDC). 
- This is the process of observing all data changes written to a database and extracting them in a form in which they can be replicated to other systems 
  - The source of information to observe is the database replication log, a persistent log where the engine first writes the changes before actually changing the data in the corresponding disk pages. 
  - The replication log’s main purpose is to provide durability guarantees on crash recovery scenarios
- In our particular case, we’re using PostgreSQL so this replication log is the WAL (Write-Ahead Log). 
  - Initially, the WAL format was considered to be an internal implementation detail, but in order to support logical replication, PostgreSQL 9 introduced a Streaming Replication protocol standardizing a format for the WAL contents to be streamed.
  - Later, in release 9.4, they added the logical decoding feature, introducing the concept of replication slot and allowing to customize the output format for each slot using output plugins. And this is exactly what Debezium, our CDC tool of choice, uses under the hood.
- Debezium is a piece of software for CDC that monitors a database replication log and converts that log of changes into Kafka records with a structured format. 
  - It runs on top of Apache Kafka as a set of Kafka Connect connectors, one for each of the supported database technologies: PostgresSQL, Oracle, MySQL, MongoDB, Cassandra, DB2…
- Once we have the set of database changes serialized as Kafka records, we need a way to transform them into the format required at the derived system. 

- The benefit of CDC becomes apparent once we start using it as a solution for the rest of the issues mentioned in the beginning of the article. 
# blogs-internals

## [How MVCC databases work internally_201712](https://kousiknath.medium.com/how-mvcc-databases-work-internally-84a27a380283)

- it’s pretty clear that such systems maintain different versions of data with identifier like rev_no or version_no etc & when data is queried, the latest version is returned.
- Typically traditional database systems use locking when multiple readers & writes access some resource. 

- MVCC systems also use B-Tree internally. But it does not do in place B-Tree update as random write is very costly and less efficient in any kind of disk. Instead it takes append only approach like LSM tree systems. Each & every time some data is updated, a copy of the original leaf node is created and appended to the end of the file.

## 👥🔥 [Basic Data Structures and Algorithms in the Linux Kernel | Hacker News_201311](https://news.ycombinator.com/item?id=6787836)

- 
- 
- 

# more
