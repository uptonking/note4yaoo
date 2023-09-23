---
title: lib-db-datalog-community
tags: [community, database, datalog]
created: 2023-09-16T17:27:24.479Z
modified: 2023-09-16T17:27:42.089Z
---

# lib-db-datalog-community

# guide

- communities
  - https://twitter.com/search?q=datomic%20datalog&f=live
# discuss-stars
- ## 

- ## 

- ## 
# discuss-sql-cte
- ## 

- ## 

- ## 

- ## 👉🏻 [SQLite now allows multiple recursive SELECT statements in a single recursive CTE | Hacker News_202010](https://news.ycombinator.com/item?id=24843643)

- 🤔 **Anyone have a recommended resource for understanding the practical application of recursive CTEs / Graph DBs**?
  - Look for a good reference about handling trees in SQL. There are a number of books on the whole area, and many smaller more focused articles online.
  - The most common place I've encountered recursive CTEs being massively useful in real world work is working with company responsibility & reporting hierarchies (line management, regulatory supervision, "spans of control" reporting, ...) where there is not a fixed number of levels.
  - When there are a small and fixed number of levels (for instance every drone has a supervisor and senior supervisor and you don't monitor connections above that) there are often other solutions that people find easier to understand and/or perform faster but for deeper trees or those where the level structure is any less static, recursive CTEs are a godsend.
  - Other examples include nested taxonomies (nature, book or other publication filing, nested tags for categorisation), properly threaded discussion records, family trees (though these are graphs rather than trees unless you impose some strict limits on what you count), representing file-system like structures in the DB, ...
  - Graphs get tricker (trees are a subset of graphs) as you may need to consider multiple paths to the same node, infinite loops, and other complications, so I suggest looking into trees first then expending your research.
- The most common example for graphs in DBs would be a graph representing the friends/contacts of users. It's one of these "you'll know when you need it" solutions.
  - Sometimes your data structure is a graph, and sometimes you want that graph to live in a database.
  - And in even rarer cases you want to search that graph in your database in some recursive manner.
- Recursive Common Table Expressions (CTE) are hard to understand until you've worked through at least one real-world example. 
  - The SQLite documentation on the `WITH` Clause has a couple of simple examples for an Org Chart and a Family; both represent **hierarchical data structures**.
  - The Fossil discussion involves the SCM's representation of a File System, probably the most common hierarchical data structure we regularly encounter. 
- Hierarchical data structures are notoriously hard in SQL. 
  - **Recursive CTEs are not easy but they are useful and efficient for hierarchical data**.

- In the past I used recursive CTEs in Postgres to calculate the BOM of a product. Products consisted of "parts", and each "part" had a cost and could consist of any number of other "parts" (subassemblies). This was for a homemade ERP resembling software.

- A graph database usually means you’re storing the graph nodes and edges as entities, so you can traverse the graph easily from any direction, and express different kinds of relationships.

- One application not mention in this thread is to traverse trees, like in the old forums where you had many levels of categories/subcategories. AKA hierarchical query. SQLite already has support for this[0]. It seems they are supporting multiple selects now.

- This means you can use SQLite as a graph database.
- why do we want to use SQLite as one
  - Because SQLite is ubiquitous. It's simply everywhere. And it doesn't need a dedicated server to run.
  - another good reason is that it's probably going to be the most reliable, best tested part of any stack you decide to use.

- While you can use recursive common table expressions to perform graph queries, **certain queries like breadth-first traversal are not very efficient for anything but trees** (not even DAGs). 
- Still cannot use window functions in recursive queries, e.g. select row_number() over () to enumerate and distinguish paths along the edges of a graph. This works in PostgreSQL, but is an error in SQLite, just tested with preview 3.34.0 2020-10-20. This greatly diminishes the utility of graph querying because only (nearly) trivial queries don't drag window functions into them.

- Doesn't the graph database community have something better to offer? I would assume by default that anything involving graphs should not involve SQL.
  - That would be a questionable assumption. SQL databases are a widely tested tool, and SQL itself can allow you to augment your "graph" with constraints and semantics that many graph-focused systems have trouble with. CTE's, while not entirely trivial, are not overly complex; they're not something you'd spend "hours" debugging.

- SQL has a knack(技巧；诀窍) for doing really easy things well, and moderately complicated things badly. I would assume by default that anything involving graphs should not involve SQL
  - A schema may have only one, or anyway, comparatively very few instances, of recursion.
  - In this case, using two separate data stores would be too much overhead; if the CTE doesn't do anything particularly fancy, that is, if it just retrieves records recursively associated via keys, it's not implicitly hard to debug (actually, there isn't much to debug).
  - A point in case is GitLab's users management, which dropped MySQL also because of the lack of CTEs (at the time).

- Some of the early RDF Graph Stores were indeed based on SQL databases (Jena RDB/SDB) but you're correct in that they didn't scale particularly well.
  - There are pure graph stores out there, AllegroGraph, OpenLink Virtuoso (although this is a strange hybrid of SQL + Graph technologies) and others - and for more advanced graph query constructs like path finding there are optimisations that are difficult/not well supported in SQL.

- use of a well known and mature SQL database is no bad starting point.

- Yes why not? If you have a data model where parts of the data is graph-like, and other classic relational, why would you not want to store the entire thing in the same database?
  - SQL is an implementation of relational algebra, and databases that implement it are relational databases for storing relational data.
# discuss
- ## 

- ## [RDFox uses datalog to apply inference rules to graph data, it has some state of ... | Hacker News](https://news.ycombinator.com/item?id=21666872)
- RDFox uses datalog to apply inference rules to graph data, it has some state of the art algorithms for making datalog multi-core. It still uses SparQL, which is really similar to datalog for querying. There's some recent work on horizontally scaling datalog queries, but I hadn't seen anything in production.
  - Probably the most popular implementation is datomic and its free variants. Which has a lot of convenience to it as you can embed custom java functions.
  - It's not datalog but cypher has a lot of amazing ideas like easily combining algorithms to potentially recursive relationship queries, eg, "Give me the all shortest paths between these two peoples where there's at most 6 hops" -> allShortestPaths((n1: Person)-[*..6]->(n2: Person)) .
- I work on Crux, which is also a Java-friendly Datalog database. It sits on top of lazy EAV indexes in RocksDB/LMDB so it's pretty fast and scales well (though technologies like Neo4j/GraphBLAS will be faster!).
  - We don't have online REPL just yet but Nextjournal is pretty great if you want to play through the tutorials interactively [1]. The other unique angle is that Crux gives you "bitemporal" Datalog queries

- ## [Datalevin is good, but its more useful in the same realm as sqlite | Hacker News](https://news.ycombinator.com/item?id=31127793)
- Not exactly. My goal of developing Datalevin is to replace our use of both Datomic and Postgres, so we have a single DB. 
- The aim is to provide a versatile(多用途的，多功能的) database that meets data needs of most use cases.
- I mention Sqlite in README because I have not finished the query engine rewrite of Datalevin, so the query performance is not up to my standard of being competitive with relational databases for large data sets. 
  - However, even at the current state, Datalevin is already faster than the alternative Datalog stores in the Clojure world for the most part.
- Finally, since you seems to want to go into this space, I will mention that: **without some new tricks in query algorithms, triple stores would be always slower than standard relational DBs**. 
  - This is not a solved problem. 
  - Just be aware what you are getting yourself into.

- ## [Soufflé: A Datalog Synthesis Tool for Static Analysis | Hacker News_202211](https://news.ycombinator.com/item?id=33806419)
- You could theoretically use Datalog anywhere you're currently using a SELECT SQL statement - it's a declarative way to produce a set of tuples given some existing sets of tuples.
  - But, Datalog is much better at deductive(推论的，演绎的) reasoning compared to SQL. There's a great interactive tutorial here: https://percival.ink/. 
  - To see how Datalog and SQL can be equivalent, I have a build of percival.ink that transforms simpler queries to SQLite
- I've also worked on percival a bit, it compiles (transpiles?) the datalog ast into javascript code on demand and executes it to get the results
- Depending on what you mean, I'd say datalog is partially characterized as compared to prolog by it's lack of unification (also it's typically executed bottom up and sometimes considered to not have compound terms). 
  - Unification is roughly bidirectional pattern matching whereas datalog rules are in essence performing unidirectional pattern matching / query on a database.

- **You can do "deductive" reasoning in SQL too, via views and possibly-recursive CTE's**.
  - Sure; you can do most Datalog things in SQL and most SQL things in Datalog. But I find it much clearer to express deductive reasoning in Datalog. I built a toy Datalog-to-CTE compiler

- Datalog is a formalism like relational algebra but additionally supports recursion.
  - So it can roughly play the role of SQL. Compiler writers have used it to query their symbol tables and identify patterns for example (seems to be the origin of Soufflé, "static analysis").
- I believe the reemergence of datalog is at least in part due to compute and memory being more plentiful so it is more affordable and practical to use a declarative query language. A lot of databases (or the part that is relevant for answering a particular query) comfortably fits in a single machine's memory and an expressive query language is fun to use. There is also an incremental evaluation story.
  - Another potential reason is that the logical data model makes it easy to represent any kind of data without schema changes and such.
- A lot of programs end up either doing SQL or something SQL-like. There are therefore many applications of such datalog like languages.
- In many places where people use custom "rule languages" they could use datalog instead. (edited: typo & rule languages)
- As I understand, implicit joins are another selling point

- Souffle Datalog is used for defining program analyses in such projects like Doop  for Java and cclyzer++ for LLVM.
  - GitHub's CodeQL is another Datalog dialect used for detecting bugs and vulnerabilities.
  - Datomic is a database that uses Datalog as the query language.

- ## [I dream of a SQLite-like embeddable database engine based on Datomic’s data mode... | Hacker News](https://news.ycombinator.com/item?id=32251654)
- I dream of a SQLite-like embeddable database engine based on Datomic’s data model and queryable with Datalog. 

- I’m surprised something like this doesn’t exist yet - I wonder if it’s possible to build it on top of SQLite somehow?
  - I tried. It's not easy because of how limiting SQLites indexes are. You have to build your own indexes using TRIGGERs or in a software wrapper and tables.
  - You can see me prototype here: https://git.sr.ht/~chiefnoah/quark /python
- Commendable attempt! I've considered writing a datalog storage backend on sqlite just like your prototype. Thank you for sharing, now I can lazily study your prototype instead of doing the hard work myself. I'm curious, what kinds of limitations of SQLite indexes are you referring to?
  - 👉🏻 Sparse indexes are pretty limited and it only supports B-tree, which make implementing AVET and VAET difficult. Further efficiently finding the current value for a E + A is difficult to do in SQL in a way that doesn't require maintaining a whole copy of the data. 
  - I actually bumped up against what I believe are weird edge-case bugs in the SQLite query planner when dealing with sparse indexes as well.
  - I think I gave up when trying to implement one-many relationships because the SQL was getting too gnarly(困难的; 挑战性的).

- I think the problem with querying is efficient query-planning requires understanding the indexes on the dataset, so you at least need to be able to expose indexes and the their properties in an API.
- Imho the 90% of query planning is not that hard at all in practice. If it's your data, and your query you'll probably have a pretty good idea which table you'll want to filter first, and what to join the same you would with any data structures.
  - The hard part is getting all of that consistent with concurrent writes. Can rows change while you scan? can indexes? How do you check that your write is valid immediately before committing, etc. things like that.
- IMNSHO query planning is pretty hard. I recently found exponential behavior in SELECT query processing that depends on the depth of subselects. This happened with pretty seasoned database system, let me say.

- ## ✨ [Differential Datalog | Hacker News_202103](https://news.ycombinator.com/item?id=26514456)
- The fact that this is bottom up makes me think that you probably can't go crazy with the number of rules.

- It's great to see differential-dataflow and timely-dataflow (both by Frank McSherry) come to life recently with this and materialize.com

- Dynamic changes to the database have advantages and drawbacks. 
  - On the plus side, they let us incorporate new knowledge and rules, and we automatically benefit from built-in features such as argument indexing. 
  - However, running the same query twice can lead to different results, changes in the order of goals can affect the meaning of the conjunction, and we can no longer reason about different predicates in isolation. Dynamic changes of the database are said to be side-effects, since they affect the program in a way that is outside the logical interpretation of the given definitions.
- I wonder if that is part of the benefits advertised by DDlog, the ability to update a program without having to worry about clause ordering (which one does not have to, with datalog and bottom-up evaluation) or generally side effects.
  - Very tentatively(未定的; 暂时性的), I'm guessing that, since datalog programs lack negation, any new facts or rules added to the (extensional) database will update the "output" of the database (its Herbrand model) monotonically, i.e. you'll see new facts comeing out but no facts will "disappear". I'm a bit unsure because the DDlog github is talking about functions and typed datalog and I'm not really sure how that works now.
- Most modern datalogs, this one included, support negation, with some limitations.
- The notably limitation being that you can't combine negation and recursion.

- Aside from their custom syntax in DDlog, how much semantic overlap is there with the query language of Datomic/Crux/Datalevin/Datascript flavour? Apart from the differential features. This one seems to be big on static type definitions at least.
- You don't really use dynamic datalog queries with DDlog. Instead you write rules that handle your queries in a streaming fashion ("prepare" statement at compile time, stream tuples of parameters at runtime and listen for outputs), if you can't afford to keep a materialized view up-to-date that turns your queries into simple KV-lookup operations.
  - But, do not worry: **Support for run-time rule updates is in the works** and would allow for arbitrary dynamic datalog queries.
- So could you use this to implement always-up-to-date materialized views in Postgres? It says it uses relational data for inputs and outputs. It says it operates in-memory but also that it starts up from a set of known facts (which sounds like it could just read the current matview at startup). This would be a really cool extension for someone to build!
  - Yes. Almost exactly what you're describing exists already. https://materialize.com/

- Looks like it’s Postgres protocol compatible rather than running as a Postgres extension?
  - It doesn't run as an extension (at least that's not the typical deployment, and I'd be surprised if it did).
  - You can feed a CDC to Materialize and either feed the output back to Postgres, or just query it directly in Materialize (via a normal postgres client).

- Prolog's top-down evaluation starts with the "head" of rule (1), grandparent(X, Y) and proceeds to its "body", (parent(X, Z), parent(Z, Y)) to instantiate the variables {X, Y, Z} according to the facts in the database and derive the new fact grandparent(maria, yannis).
- Datalog's bottom-up evaluation instead starts with the facts in the program: parent(maria, kostas), parent(kostas, yannis) and adds those to the set of immediate consequences of the program (TP is called the "immediate consequence operator"):
- 👉🏻 The advantage of bottom-up evaluation is decidability, as long as a program is datalog, which means no function symbols other than constants (which are function symbols of arity 0, i.e. with 0 arguments) and no negation.
- By contrast, Prolog's top-down evaluation will first correctly derive the two new "ancestor" facts from the head of rule (2) but then will try to evaluate the first ancestor(X, Z) fact in the body of rule (3). This will take it back to the head of rule (3) and evaluation will be stuck in an infinite recursion.
- The **trade-off** is that **bottom-up evaluation cannot handle negation or functions** (including the cons function used to construct lists) and so is, in that sense, incomplete, whereas Prolog can do both. 
  - For this reason, datalog is preferred as a database language that offers a limited ability for reasoning (certainly richer than what is possible e.g. with SQL, that essentially only allows facts) whereas **Prolog is preferred for general-purpose programming**.

- ### [Differential Datalog: a programming language for incremental computation | Hacker News_202211](https://news.ycombinator.com/item?id=33521561)
- Why does it have to be a new programming language? Why not a library/framework for an existing language?
  - We didnot get whole fields of mathematics until a clear syntax was developed; and likewise, what patterns of thinking a syntax affords makes a big difference to the designs one chooses.
- A DSL for differential-dataflow would be great. A big niche/yawning chasm for such a DSL to fill would be to allow for runtime dataflow programs (i.e., to have a parser/interpreter that then relies on differential-dataflow).

- ## ✨ [Show HN: Cozo – new Graph DB with Datalog, embedded like SQLite | Hacker News_202211](https://news.ycombinator.com/item?id=33518320)
- I have been making this Cozo database since half a year ago, and now it is ready for public release.
  - My initial motivation is that I want a graph database. Lightweight and easy to use, like SQLite. Powerful and performant, like Postgres. I found none of the existing solutions good enough.
  - Deciding to roll my own, I need to choose a query language. I am familiar with Cypher but consider it not much of an improvement over CTE in SQL (Cypher is sometimes notationally more convenient, but not more expressive). I like Gremlin but would prefer something more declarative. **Experimentations with Datomic and its clones convinced me that Datalog is the way to go**.
  - Then I need a data model. I find the property **graph model (Neo4j, etc.) over-constraining, and the triple store model (Datomic, etc.) suffering from inherent performance problems**. They also lack the most important property of the relational model: being an algebra. **Non-algebraic models are not very composable**: you may store data as property graphs or triples, but when you do a query, you always get back relations. So I decided to have relational algebra as the data model.

- you may store data as property graphs or triples, but when you do a query, you always get back relations. 
  - Can you elaborate on this? in datomic you can get back hierarchical data
- I believe you are referring to Datomic's pull syntax (https://docs.datomic.com/on-prem/query/pull.html). 
  - The way I see it is that this is an add-on to the query language, not a core part of it, since it applies to the output of the query only. 
  - This would be analogous to having a GraphQL server on top of Cozo's relational model. 
  - (In fact, in earlier versions of Cozo we did have something like the pull syntax, but we quickly decided that we do not want two distinct ways of querying data in the same database, nor do we want to create a GraphQL clone).
- I personally find Datomic's way of doing things a bit too convoluted, as you need to
  - learn how to define the schema
  - learn how to transact data
  - learn how to query data
  - learn how to "pull" data after the query is done

- Graph query over relational data, brilliant. I need this yesterday.

- The main thing I will be wondering now is how it will scale to really large datasets. Any input on that?
  - It currently uses RocksDB as the storage engine. If your server has enough resources, I believe it can store TBs of data with no problem.
  - Running queries on datasets this big is a complicated story. 
  - Point lookups should be nearly instant, whereas running complicated graph algorithms on the whole dataset is (currently) out of the question, since **all the rows a query touches must reside in memory**. 
  - Also, the algorithmic complexity of some of the graph algorithms is too high for big data and there's nothing we can do about it. 
  - We aim to provide a smooth way for big data to be distilled layer by layer, but **we are not there yet**.
- **Does that mean all rows will not be in memory?**
  - Yes. For example, in Postgres you can sort tables arbitrarily large, not constrained by main memory. Postgres uses external merge sort when the tables are really large. There are other situations where the working data are disk-based when they are too large in Postgres. We will eventually be able to do that in Cozo as well, but no timetable is available yet.
- what if you had not so many nodes but each node had a lot of data would that improve it? 
  - For your second question, say you have a relation with lots of fields, one of them particularly large. As long as you don't use that field in your query, it will not impact memory usage. The query may be slower though since the RocksDB storage engine needs to read more pages from disk, but the fields that are loaded by RocksDB but not needed will be promptly(及时的; 迅速的) evicted(驱逐) from memory.

- 🆚️ Have you looked at **differential-datalog**? It's rust-based, maintained by VMWare, and has a very rich, well-typed Datalog language. differential-datalog is in-memory only right now, but could be ideal to integrate your graph as a datastore or disk spill cache.
  - Differential-datalog is a cool project. I think the targeted use cases are different as compared to Cozo. 
  - The **most important difference** is that Cozo is focused on graphs, whereas differential-datalog is focused on incremental computation. 
  - These two goals are somewhat at odds with each other, as for queries with lots of joins (very common in graph computations), you can't know whether it's better to compute new results incrementally or to recompute everything until you actually run the query. 
  - Also, Cozo caters for the exploratory phase of data analysis (no need to define types/tables beforehand), whereas in differential-datalog everything must be explicit upfront.

- **I thought there was a big class of queries Datalog could not express** -- something about negation, queries like "all X for which not Y". Is that not true? Or if it is, is Datalog somehow Turing complete nonetheless?
  - Technically, Cozo is using something called "Datalog with stratified negation, stratified aggregation, and function symbols", allowing aggregations to be auto-recursive when they form a semi-lattice, together with built-in algorithms which are black boxes taking in relations and giving you back another relation. Your example is taken care of by the "stratified negation" part. I believe "Datalog with function symbols" is already Turing complete, but you are right, what they call "Datalog" without any qualification in academic papers is not.

- What's the max practical graph sizes you anticipate?
  - For the moment: you can have as much data as you want on disk as long as the RocksDB storage engine can handle it, which I believe is quite large. For any single query though, you want all the data you touch to fit in memory. The good news is that Rust is very efficient in using memory. This will be improved in future versions.
  - For the built-in graph algorithms, you are also limited by the algorithmic complexity, which for some of them is quite high (notably betweenness centrality). There is nothing the database can help in this case, though we may add some approximate algorithms with lower complexities later.
- And what is the biggest size that you have tested?
  - Around 10 GBs of data, on the standalone version. We will have systematic benchmarks when the API, syntax, etc. settle down a little bit.

- I like the design choices of Datalog for the query language and Relations for the data model. 
  - This contrasts with the typical choices made for graph databases where the word graph seems to make **links** a mandatory query and representation tool.

- 🆚️ You mention how Cypher is not much of an improvement over CTE in SQL, I was wondering if you could expand on this point a bit if possible?
  - Some part of me is considering using Apache AGE graph extension for postgres, but another part wonders whether it's worth it considering CTE's can do a lot very similarly.
- Perhaps I should start by clarifying that I am talking about the number of queries the Cypher language can express, without any vendor-specific extensions, since my consideration was whether to use it as the query language for my own database. And **Cypher is of course much more convenient to _type_ than SQL for expressing graph traversals** - it was built for that.
  - With that understanding, **any cypher pattern can be translated into a series of joins and projections in SQL**, and **any recursive query in cypher can be translated into a recursive CTE**. 
  - Theoretically, SQL with recursive CTE is not Turing complete (unless you also add in window functions in recursive CTE, which I don't think any of the Cypher databases currently provide), whereas Datalog with function symbol is. 
  - Practically, you can easily write a shortest path query in pure Datalog without recourse to built-in algorithms, and at least in Cozo it executes essentially as a variant of Dijkstra's algorithm. 
  - I'm not sure I can do that in Cypher. I don't think it is doable.
- Otherwise the thing I have noticed **with the datalog (as well as prolog) syntax, is you are able to build a vocabulary of re-usable queries, in a much more usable was than any of the solutions I've seen in SQL**, or other similar languages.
  - It thus allows you to raise your level of abstraction, by layer by layer define your definitions (or "classes" if you will) with well crafted queries, that can be used for further refined classifying queries.
- Re Datalog syntax: yes, the "composability" is the main reason that I decided to adopt it as the query language. This is also the reason why we made storing query results back into the database very easy (no pre-declaration of "tables" necessary) so that intermediate results can be materialized in the database at will and be used by multiple subsequent queries.

- 
- 

- ## [Ideas for DataScript 2 | Hacker News_202208](https://news.ycombinator.com/item?id=32447636)
- **Reactive updates** is the big one, in my opinion. 
  - DataScript is a triumph and arguably is the reason why so many note-taking tools (Roam, Athens, Logseq, etc) are written in Clojure. 
  - But there are so many cases where it would be nice to react when some set of entities is changed.
- I think what we need is to figure out **how to combine DataScript with a rules engine**. I wrote a rules engine and made a writeup that compares the two together
- Subscribing to individual entities is nice but with a rules engine you have so much **more fine-grained control over your reactions**. And with the RETE algorithm this can be done efficiently. Most libraries in this space just ignore it and make their own ad-hoc solution -- an informally-specified, bug-ridden, slow implementation of half of a rules engine.

- The rules engine direction is definitely an interesting one, hopefully there’s more exploration into that in the future.
  - For my needs now I actually wrote something pretty hacky to get a 'reactive' version of DataScript’s Entity API.

- The big question is: if you don't need queries (which I agree you don't), then why bother with DataScript at all? Why not just store your data in native Clojure/ClojureScript data structures, using the right structure for each thing and use a small number of data access functions, possibly maintaining an index or two?
  - This is what I did: migrated an app (arguably a fairly complex one) from DataScript to native Clojure data structures. 
  - Not because I didn't like DataScript: I actually liked the idea a lot, but because I couldn't justify the cost in performance and complexity (in my case, DataScript not handling nil values was a problem as well).

- The "Optimized B-Trees" section I _think_ is suggesting to get rid of datoms, which I 100% agree with. I do not think they add anything at all; IME you can have a collection of all attributes indexed by entity ID and then have additional indexes on top of that collection.
  - My stupid question is: why even bother with B-Trees? I believe asami stores everything in memory using Clojure maps & sets.

- I know the founders of InstantDB are using some of these ideas for inspiration 
  - Oh boy, their blog[1] is really painful to read for someone with a database background. They conflate so many different concepts, like datalog and triple-stores, apparently having seen only Datascript/Datomic.

- Very good pointers, match my thinking on the topics I had considered.
  - One thing though is that I'm not a fan of uuids, I think content addressing is sufficient if you build everything around that. 
  - Actually I feel all IDs can be content address and type/name/context. Ofc I'm approaching this slightly differently, I don't care about web browsers but I care about p2p and replication..

- How come there is no SQLite of Datalog? You can find plenty of implementations of embedded datalog database in a specific language, where the query API is tied to the language. I want to write text datalog queries and access my database from multiple languages. Why doesn’t this exist?
  - Mozilla was working on the opposite, a Datalog of SQLite, with Mentat, now abandoned: https://github.com/mozilla/mentat
  - It's a superset, but couldn't you just use Prolog?
    - No, 👉🏻 **the standard evaluation model of Prolog is top-down, while that of Datalog is bottom-up**. 
    - As such, some queries will perform very differently between the two.

- RxDB seems to use a document-based model, not triples like entity-attribute-value? Fundamentally different model if so.

- ## [Open source Datomic?](https://www.reddit.com/r/Clojure/comments/yj1oah/open_source_datomic/)
- XTDB is open source and does immutability but it has significant differences to datomic. 
  - XTDB is document oriented and has no built-in schema or constraint checking.

- 🤔 Do databases like Datomic perform better or are safer than SQL databases, like postgresql? What advantages do they have?
  - They are structured differently: EAV oriented, documents or graphs, rather than traditionally relational. 
  - Secondly they are all (with exceptions) temporal databases. 
  - Third they are directly embedded in Clojure both in terms of syntax and proximity: even though most have external storage backends, the indices are typically right there for you to interact with.
- The biggest advantage is typically temporal awareness built into the database, meaning data is not forgotten when updated, like in a SQL database, but rather the database remembers what the value used to be.
  - You can model it in SQL, but it's typically a real headache once it starts to grow.
  - If you want versioning on all your entities in SQL, each table definition must include time columns, and each transaction must know how to attach time data to the transacted data. The problem compounds if you want to know which of your entity's attributes changed when, or know which entities across different tables changed together.
  - Even if you manage to get version data attached to everything you want versioned, you also have the difficulty of building queries that are aware of that version information and can deliver point-in-time results.
  - Datomic has easy solutions built in for all these problems.
- If all you want a log, it's typically not so bad. Or just want to be able to take snapshots of single tables, and be able to go back.
  - Once you move beyond that, and start from a point in time for multiple tables and how they relate at that specific point in time, the queries tend to get very involved. Historic comparisons further complicates things when you now need to consider more than one point in time.
  - It's all doable, but the code/SQL queries will lend itself towards increased complexity, and once you hit a case (such as new business questions) where you need to rebuild the tower of complexity you built

- It depends on the query patterns. If you have simple queries, and row-like data then probably worse, very graph-like data and targeted queries (that the query planner can't compile away) then probably better.
  - But these dbs both have a different query paradigm and a different storage/indexing paradigm, and SQL dbs have many different storage/indexing paradigms, so it's hard to generalize.
  - The query language is basically just better in all ways, although SQL standardization has lead to a lot of great tooling you lose access to.
  - Plus there is, in most of the datomic variants, the time awareness/db-as-value part, which is a huge advantage.

- ## [The Essence of Datalog (2018) | Hacker News](https://news.ycombinator.com/item?id=19351385)

- ## Are you familiar with Datalog-style queries? 
- https://twitter.com/ccorcos/status/1534074897294495744
  - Seems pretty similar, except the edges are traversed recursively without having to define methods to traverse school edge. 
  - Just remember that Datomic also allows you to query into the past so that's why `tx` lands in their indexes.
- 
- 
- 

- ## What database has the best query language that’s not sql?
- https://twitter.com/gusbicalho/status/1607857080450404356
- #datomic's #datalog is very intuitive if all you need are inner joins, which is just unification of variables. 
  - The minute you need anything else, things get ugly. Uglier than SQL? Who knows, pick your poison.

- ## We also tried the datalog-centric thing (reflecting spreadsheet-like application UI from Datomic queries), we found it not powerful enough to express what Rails can express. 
- https://twitter.com/dustingetz/status/1662626589505355780
  - Something closer to Airtable but powered by Datomic could have worked for a team with fundraising skillz
- My new database is Datomic inspired, fireproof

- ## a thing i made in JS similar to datomic datalog, except JSON + symbol DSL for lvars, e.g. _.foo instead of ?foo
- https://twitter.com/alandipert/status/1398296493392424960
- Are you doing incremental/differential view maintenance, or just recomputing?
  - just recomputing, but if something end-to-end looks workable i hope to revisit that part and make incremental
- 👉🏻 Incremental datalog evaluation is not too hard to implement until you hit recursive rules. Then you need differential dataflow
- If you're just recomputing on diffs, I wonder if it wouldn't be easier to just use DataScript or Datahike (or even Posh), and wrap in a JS API if that's what you want. Then you're just responsible for translating your JSON queries to edn.

- ## [Introduction to Datalog | Hacker News](https://news.ycombinator.com/item?id=34801457)
- 
- 
- 
- 
- 
- 
- 

# discuss-graph-db
- ## 

- ## 

- ## [Postgres as a graph database | Hacker News](https://news.ycombinator.com/item?id=35386948)
- I designed and maintain several graph benchmarks in the Linked Data Benchmark Council, including workloads aimed for databases. We make no restrictions on implementations, they can any query language like Cypher, SQL, etc.
  - In our last benchmark aimed at analytical systems [2], we found that SQL queries using WITH RECURSIVE can work for expressing reachability and even weighted shortest path queries. However, formulating an efficient algorithm yields very complex SQL queries [3] and their execution requires a system with a sophisticated optimizer such as Umbra developed at TU Munich [4]. Industry SQL systems are not yet at this level but they may attain that sometime in the future.
  - **Another direction to include graph queries in SQL is the upcoming SQL/PGQ (Property Graph Queries) extension**. I'm involved in a project at CWI Amsterdam to incorporate this language into DuckDB [5].

- 
- 
- 

- ## [PageRank algorithm for graph databases | Hacker News_202301](https://news.ycombinator.com/item?id=34577832)
- is there a good "graph layer" for SQLite? I understand that graph databases use specific data structures to optimize for graph queries instead of row-oriented but sometimes you need something in the middle: representing graphs and doing basic queries.
- It's nearly a decade old at this point and probably not optimal even for the time, so there may be better approaches, but here's a few basic algorithms on SQLite. PageRank is at the bottom.
- Common graph databases are network-based for scaling purposes. You do have a database server then you talk to the server somehow for the queries. Sqlite is a single-file database. You do not have a server so you do not need an extra layer in database side.
  - Instead, Run the graph algorithms on a stringified json stored as a text in sqlite. They will be running in some process in anyway.

- 
- 
- 

# discuss-datomic
- ## 

- ## 

- ## [Datomic is Free | Hacker News_202304](https://news.ycombinator.com/item?id=35727967)
- 
- 

- Although it is true that "time traveling" queries are relatively rare for production needs, the basic architecture supports things that many applications really need:
  - It is possible to make queries against the database PLUS additional data not yet added, that is, "what if" queries
  - Having a stable database-as-value is really useful for paginating results; you don't have to worry about new values being inserted into your results during execution, the way you do with traditional databases no longer how long (minutes, hours, even days) you take to traverse the data
  - Reified(物体化；具体化) transactions makes it possible to store extra data with each transaction, trivially, such as who made the update and why
  - Immutability is amazing for caching at all layers

- 
- 
- 

# discuss-alternatives-datalog/datomic
- ## 

- ## 

- ## [Tree structure query with PostgreSQL | Hacker News](https://news.ycombinator.com/item?id=9111362)
- Recursive CTEs are a cool feature, but it's a shame the syntax is so awful. You really have to work to understand what the query is trying to do.
- Other query languages that make recursion much more bearable are SPARQL (on RDF data), Cypher (Neo4j) or Datalog (Datomic, Cascalog, etc). 


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

- [Composeability is front and center in GQL, so you may want to consider it. | Hacker News](https://news.ycombinator.com/item?id=22872470)
  - Cypher is by far the biggest graph query language and they seem to have the most weight in the conversation so far, but we are going to try to represent datalog as far as possible. 
  - Even if woql isn't the end result, we think datalog it is the best basis for graph query so we'll keep banging the drum (especially as most people realize that composability is so important)

- ## [Graph query languages: Cypher vs. Gremlin vs. nGQL | Hacker News_202003](https://news.ycombinator.com/item?id=22482665)
- Datalog is such a delight to use especially since queries are just data structures are just code. 
  - Once the basics clicked I felt empowered to do anything in Datalog, while I feel like I always have to learn or remind myself of more syntax when I want to do anything fancy with SQL.

- I agree that SPARQL must be considered, and so must Datalog and Prolog. Idk but I'm starting to believe that new-fangled standardization efforts (if you want to call those that) are starting over from scratch and actively avoid looking at prior art as a generation thing.
  - Though I could see **why someone wouldn't like SPARQL and RDF**, with its bulk reuse of other W3C and TBL concepts such as URLs, resulting in atom and predicate names verbosely and pointlessly beginning with "http://".

- ## [Why isn't differential dataflow more popular? | Hacker News_202101](https://news.ycombinator.com/item?id=25867693)
- disclaimer: I work at Materialize and I work with Differential regularly
  - Differential dataflow lets you write code such that the resulting programs are incremental e.g. if you were computing the most retweeted tweet in all of twitter or something like that and 5 minutes later 1000 new tweets showed up it would only take work proportional to the 1000 new tweets to update the results. It wouldn't need to redo the computation across all tweets.
  - Unlike every other similar framework I know of, Differential can also do this for programs with loops / recursion which makes it more possible to write algorithms.
  - Beyond that, as you've noted it parallelizes work nicely.

- I don't think it is possible to compare "differential dataflow" with projects like Spark. (don't know about kafka streams)
  - Spark is a "product" -- it has extensive documentation, supports multiple languages, and generally is production-grade. It is full of "nice-to-haves", like interactive status monitors, helper functions, serialization layers, and so on. It integrates with existing technologies (Hadoop, K8S, HDFS, etc..). It has this "finished product" feel.
  - "differential dataflow" seems to be a library. It only supports a single language. The documentation is very basic 

- A possible reason not mentioned in the post is that writing efficient incremental algorithms is just fundamentally hard, despite the primitives and tooling afforded by the differential dataflow library. For example, even with a lot of machine learning libraries targeting python, there are only a couple that really implement online algorithms.

- 
- 
- 
