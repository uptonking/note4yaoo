---
title: lib-db-app-community-comparison
tags: [community, comparison, database]
created: 2023-09-17T17:45:34.428Z
modified: 2023-09-17T17:46:07.620Z
---

# lib-db-app-community-comparison

# guide

# discuss-stars
- ## 

- ## 

- ## do you use Postgres or MySQL at work?
- https://twitter.com/jarredsumner/status/1710737550292423152
  - pg vs mysql = 0.56: 0.21
  - mongodb

- ## A cheat sheet of various databases in cloud services, along with their corresponding open-source/3rd-party options.
- https://twitter.com/alexxubyte/status/1710680670568394996
  - Note: Google has limited documentation for their database use cases. Even though we did our best to look at what was available and arrived at the best option, some of the entries may be not accurate.

- ## 🛢️🔥 [Never Write Your Own Database (2017) | Hacker News_201805](https://news.ycombinator.com/item?id=16995612)
- As soon as you allow some kind of user-defined meta data, you basically end up with the entity-attribute-value pattern.
  - Every sufficiently advanced system does that, be it a CRM that allows custom fields, or a project management or ticket system, a workflow system etc. And basically all enterprise software contains elements of these systems.

- A good alternative would be to use JSON types in RDBMS in combination with classic field types. EAV is really just free form data and JSON is easier to query in MySQL or Postgres.

- ## 🔥 [Comparing Database Types | Hacker News](https://news.ycombinator.com/item?id=21060866)
- Deductive databases derive logical consequences based on facts and rules.
  - Datalog and its superset Prolog are notable instances of this idea, and they make the connection between the relational model and predicate logic particularly evident.

- The column-family databases mentioned (Cassandra, HBase) are both just fancy key-value stores that add semantics for separate tables and cell-level data so you're not rolling it yourself.
# discuss
- ## 

- ## 

- ## 

- ## if I was starting a new Rails app today, I would either pick SQLite with Litestream or MySQL on PlanetScale, depending on my expectations for scale.
- https://twitter.com/joeldrapper/status/1763150631018127579
- is there something today in the market like "planetscale for postgres"? I don't think so, right?
  - YugabyteDB is the distributed Postgres (shared-nothing, fault-tolerant, on-prem or cloud). It has a schema/data migration tool
- Amazon RDS for PostgreSQL
  - This service does not scale horizontally. Planetscale does.

- I just read about SQLite on Litestream 5 minutes ago; does this mean you deploy on one dedicated server and all the infra lives on one machine?
  - Yes. Also means you can do SQL queries in microseconds because there’s no latency. 

- ## There's been a trend back to SQL databases in the latest set of database-y startups ( @neondatabase , @supabase , @tursodatabase , @PlanetScale , et. al).
- https://twitter.com/elithrar/status/1735691896373096485
  - Is the era of alternative NoSQL architectures (like DynamoDB, MongoDB or FaunaDB) over?
  - One of the advantages of SQL-databases, especially using mature query languages (SQLite w/ @cloudflare D1 or Turso, Postgres w/ Neon+Supabase, MySQL w/ PlanetScale) is that there's a tremendous amount of tooling that "just works" (or takes very little adaptation).

- many organizations are still adopting DynamoDB& and MongoDB, and even if the "NoSQL" hype of the 2010's has died down, those models can bring distinct performance and data modelling advs. ^ yes, Dynamo has a SQL-ish interface, but it's non-standard and simplified.
  - This is especially true in the age of "edge" computing, where you want to get your compute *and* data closer to your users. 
  - NoSQL architectures have tended to make this way easier to achieve in practice, especially if you're primarily building user-facing apps w/ OLTP use-cases.

- Plenty of Postgres schemas have jsonb columns, and tools like Electric SQL sync between embedded SQLite DBs on the app side by way of CRDTs, not to mention other paradigms, like streaming, with various levels of integration... The landscape is more complex (and interesting) than it was during the summer of no-SQL.

- Being able to store and query json inside sql has filled much of the needs nosql were solving.

- ## I want a database where I can subscribe to a complex query, 
- https://twitter.com/steveruizok/status/1719442425398038900
  - eg “select id, name from all files in any of the groups that this user is a member of”. What do I pick in 2023?
- @supabase pretty good for this. (Postgres based)
  - think supabase only does it for tables?
  - Hm. You might be right
- evolu: We do that. But only for local SQLite and without any magic. It's just brutal force in Web Worker. It’s good enough for local-first.
- always go for Mongo, you don't want a boring life.
  - [mongodb Watch for Changes — Node.js](https://www.mongodb.com/docs/drivers/node/current/usage-examples/changeStream/)

- ## 💡 [How to Efficiently Choose the Right Database for Your Applications | Hacker News_202102](https://news.ycombinator.com/item?id=26290252)
- I kinda disagree with separate branch for "document database" for Mongo. Mongo is a key-value storage, with a thin wrapper that converts BSON<->JSON, and indices on subfields.
  - You can achieve exactly the same thing with PostgreSQL tables with two columns (key JSONB PRIMARY KEY, value JSONB), including indices on subfields. With way more other functionality and support options.
- Not really true. MongoDB natively supports sharding, multiple indexes, high availability, arrays, sub documents, array traversal, etc - all able to be accessed in your native language with get/set functionality (or via MQL if you want). While PostgreSQL is a really powerful database, the JSON support is really painful to program against.

# discuss-kv
- ## 

- ## 🆚️ [TiDB和FoundationDB各有什么优劣？ - 知乎](https://www.zhihu.com/question/274003103)
- FoundationDB和TiKV是一个层次的东西，都是一个支持分布式事务ACID的ordered KV map。
- 架构：都是shared nothing，TiKV单机引擎rocksdb，核心数据结构skiplist，FoundationDB单机基于磁盘的B-Tree。
  - 两者都强调分层，下面是存储，上面是接口层，TiDB是TiKV的SQL接口层，FoundationDB core就是下面的存储层。
  - 稍一点不同的是，因为TiKV本质上还是为TiDB服务的，所以加了一些接口专门给TiDB用，主要是为了计算下推。
- 隔离级别：都是SSI，基本就是拿一个快照，然后事务内的写自己能读到(不确定TiKV是SI还是SSI)。
- 事务冲突检测：TiKV冲突检测在各个TiKV节点上，FoundationDB拎了一个单独的叫做resolver的组件出来做冲突检测，这个组件可以有多个，组件会把最近5s的已经提交的写的key放在内存中，这也是known limitations中一个事务中最大只支持5s的原因之一。
- 副本复制协议：TiKV用raft，FoundationDB用paxos。
- share nothing指的是节点之间，不是region之间

- ## [rocksdb对leveldb做了哪些优化？ - 知乎](https://www.zhihu.com/question/328622742/answer/713388283)
- 两个代码都看过，leveldb感觉更像是一个教学性质的项目，在发布后没有做太多变革性的更新，基本维持了原貌。
  - rocksdb做了太多适合于工业界的优化，代码复杂度感觉至少是前者10倍

# discuss-mongo-like
- ## 

- ## 

- ## 

- ## Are there any reasons to use MongoDB (instead of, say, Postgres) for new projects these days? _202403
- https://twitter.com/ohmypy/status/1772181070202417245
- New projects? Probably nah. But not having to deal with migration is a big deal in a distributed system. 
  - Eventual consistency is a pain but you have to deal with that even w/ Postgres when you have a single writer with ~15 readers—writes take time to show up in all of them.
- I use it in iximiuz labs - pretty happy about it. But I generally an anti-JOIN person
- Personal preference to write JavaScript for data extraction
- every company I have seen mongo in prod ends up regretting it. Every one.
- Migrations
  - Why not simply design the schema correctly from the start

- ## When you think about the reasons people reached out for Mongo in 2010:
- https://twitter.com/glcst/status/1735695103962894701
  - It was dead simple.
  - It allows you to scale to 100s of GB, even a whole TB.
  - Fast forward to 2023: SQLite is easier than Mongo, and with the database-per-tenant pattern you can essentially emulate collections (each collection is a DB).
  - You can rent a 10TB box (or more) from AWS and others and be done with it.
  - Many use cases for NoSQL in specialized data processing. Not a lot in the center.

- Mongo's main value add was being able to store JSON. Most RDBMSs now support JSON type. And mongo's distributed story is not very strong.

- I 100% agree. Multi-tenant SQLite is the way to scale.

- We're seeing similar trends w/ parallel filesystems.  Large NFS servers are now able to reach rates previously only attained by clustering storage servers and pci-e gen5 is just now becoming available!  Once 6 hits the market, the consolidation will intensify.
  - also the RAM-size of newer nodes starts to get insanely large - while the caching capabilities of many networked/clustered filesystems just can't really make efficient use of this - at least not yet 

- ## 🆚️🍃🐬 [Mongo (Atlas) vs. Planetscale for my simple SaaS?_202208](https://www.reddit.com/r/Database/comments/wh9rd1/mongo_atlas_vs_planetscale_for_my_simple_saas/)
- Mongo:
- Pros: I have the most experience with it, super easy to get up and running, built for simple document structure like my use case, very cheap pay-as-you-go pricing on Atlas.
- Cons: Database doesn't enforce schema (ofc) so while as a dev I love it, as a business owner it feels maybe too risky. Has low connection limit (500) which could possibly bottleneck with serverless connections.

- Planetscale:
- Pros: Enforces schema and even has cool branching/merging of schema changes so feels much "safer" than Mongo to protect it from me doing something dumb. Unlimited connections so no bottleneck there.
- Cons: Free tier is probably good for a while but then immediately jumps to $29 unlike mongo where prices scales with me (though obviously thats not too bad, just more). Don't necessarily need a relational DB, but doesn't hurt I guess. A little bit more setup/work than Mongo because I have to build/migrate/merge the DB branches/schemas.

- I second the suggestion of trying CockroachDB serverless.
  - What about CockroachDB free tier serverless? You would go a very long time before paying a bill.

- Actually you can create a schema validation in Mongo. Check it out
  - [Schema Validation — MongoDB Manual](https://www.mongodb.com/docs/manual/core/schema-validation/)

- my advice would be to stick to what you know. If you know Mongo well go for it. 
  - If you're starting a business, proving the idea and marketing it is going to be a lot more important than the tech unless you're doing something bleeding-edge. 
  - Try to not overfocus on the tech. NextJS + your preferred DB seems like a good place to start.

- ## 🍃🪶 [FerretDB: Show HN: MongoDB Protocol for SQLite | Hacker News_202307](https://news.ycombinator.com/item?id=36590834)
- Mongo's sharding is nice but I'm really tired of their support. They force you to run smaller machines in the contract so they can charge more for # of nodes, and it adds complexity to your architecture so you're swayed into buying Atlas. I could replace it all with a few PG shards with bigger machines.
  - Yes this is one of the reasons we started FerretDB. Atlas is very easy to use, but it is nearly impossible to move away from later on, as there is no alternative (unless you are ready to rewrite your app). We think that most of its killer features, like easy sharding, can be done with Postgres and/or SQLite.

- 🤔🛋️ Honest question: why doesn't Couchdb receive any love on HN?
  - CouchDB needed to periodically run a gargage-collection-like operation. (If I remember correctly, records were not deleted, but instead hidden until you run the cleanup.) The problem was that the cleanup process was so unoptimized that CouchDB copied the entire database without the deleted records. In our case, the disk we had was about 90% occupied, so we couldn't run cleanup.

- MongoDB has a similar sync to Realm, which seems a lot more capable than Couch sync.
  - But only through their opaque sync service right?

- Is there any documentation on the native schema used to store the documents. Is it sane enough that you could manually roll your own JSON1 queries in SQL to facilitate more relational join like features?
  - Some time ago, we wrote a blog post about it: https://blog.ferretdb.io/pjson-how-to-store-bson-in-jsonb/ A few details changed after that (for example, type information is not mixed with values anymore), but the general idea is the same. We probably need to document it better.
  - Yes, querying it with SQL should be possible.

- ## 🍃🐘 [FerretDB: open-source MongoDB alternative | Hacker News_202304](https://news.ycombinator.com/item?id=35539464)
- FerretDB is a layer which implements the MongoDB wire protocol on top of Postgres. Right now we are using JSONB, but this affects performance and we need to depart from this strategy in the long run
- What's the alternative you want to move to?
  - Probably a custom PostgreSQL extension for BSON support.
  - The biggest issue right now is that MongoDB compares and sorts values differently than PostgreSQL/jsonb. For that reason, we have to do a lot of filtering on the FerretDB side, and that can't be great for performance. Pushing more work on the database size should make FerretDB perform much better.

- I realized that PostgreSQL has nice JSONB type (supports indices for subfields). So I put all the mongo data into tables with a single JSONB column (or two columns id+data, if you prefer). Turned out that was much faster to run analytical queries
  - "document" is just row
  - "collection" is just table
- My off-the-cuff suggestion is that document databases are not built to model normalized relational data. If you try to do so, you bring a whole new level of pain upon yourself. It is do-able, but it is hard and annoying.

- We've been on a big "Use postgres for everything" path. Mostly migrating dynamodb, elasticsearch, and redis to postgres.

- 👉🏻 If there were JOINs, it may be a sign MongoDB was not the best DB for you. It means the model was relational and a relational DB would be a better fit. 
  - MongoDB lookups are discouraged in general, and especially in analytical workloads, which cover a lot of data. 
  - MongoDB is better for the scenario, where all you need is already in the document.
- It may also mean poor schema design. You can absolutely model relational data in MongoDB without relying on joins. If you want to normalize your data don't pick Mongo.
- agreed, you can have reference fields to other collections and filter by them or query related data. But I wouldn't say its designed for relational workloads. Similarly I wouldn't use MongoDB for graph queries, even though it has an operator for just that.
- > agreed, you can have reference fields to other collections and filter by them or query related data.
  - Yes it has that, but that's an anti-pattern. What I'm referring to is schema design. In Mongo you denormalize and store relational data in the same document as references. 
  - In SQL you a record might be split up into 3 tables, in Mongo that should all live in the same document. 
  - If you can't embed and need lookups, you should avoid Mongo and other nosql DBs

- No, our app didn't use JOINs for the main work. But, as I wrote, every now and then we had some one-off requests that required either JOIN or GROUP BY or both.
  - With postgres+JSONB we could do both at the same time on live data.

- MongoDB really only makes sense when you have an extremely large set of documents and you don't need to do this kind of statistics.
  - Yep, although for large datasets I'd prefer multi-master architecture, depending what is needed, for example Blob storages or Cassandra for key-value, and BigQuery or Clickhouse for analytics.

- The only problem I have with PostgreSQL's JSONB type is it strictly implements the JSON standard, so things like nulls and integers aren't supported. Depending on your data, this could be a real problem.
  - FWIW, JSONB supports JSON nulls, and all numbers are encoded as numeric type, storing integers and float64 values precisely (well, as much as possible for float64 values). But you comment is correct for other data types like date-times and binary strings where some form of encoding/decoding is needed.
- The json standard has nulls

- if ferretDB truly does provides ad-hoc queries, indexing, aggregation, and real-time data processing, making it well-suited for a wide range of applications, then sure , it’s a great alternative . I can see all types of web apps even enterprise systems working well w it.

- One thing that I didn't see discussed was why FerretDB uses Postgres as a backend and not a storage engine. Perhaps I am just missing something though.
  - Because PostgreSQL Is fantastic Open Source database engine, very popular with a lot of operational experience and tooling support.
  - Just a few of the things you need to build if you don't do it this way. 
    - 1. A storage layer, 
    - 2. A network protocol with clients and servers, 
    - 3. A replication system, 
    - 4. an authentication system. 
    - 5. Administrative tools.
  - If you roll everything yourself, you pretty much have to reinvent everything PostGres has except the SQL and relational aspects.

- ## 🍃 [FerretDB: MangoDB: An open-source MongoDB alternative | Hacker News_202111](https://news.ycombinator.com/item?id=29071623)
- Recently went deep on efficient kv storage in postgres, there is an order of magnitude different in storage size between different approaches (naive skinny table, EAV, array values, mapped generic columns etc). I wonder what approach this project takes, I’ll have to poke around!

- There’s already a mongodb compatible document layer for FoundationDB
  - Yes. The Problem with Document Layer it implements MongoDB API v 3.0.0 and has not been significantly updated for years.

- ## [Ask HN: Do you still use MongoDB? | Hacker News_202005](https://news.ycombinator.com/item?id=23270429)
- 
- 
- 

- ## [Jepsen: MongoDB 4.2.6 | Hacker News_202005](https://news.ycombinator.com/item?id=23290844)
- I just don't want to be called to the office on a weekend anymore for this sort of BS.
  - Production incidents with MongoDB last year: 15 
  - Production instances with redis, elasticsearch and mysql combined last year: 2 (and with much less severity)
- This is why most of us don’t use mongo in production. It’s just not worth it. Postgres is a tank and supports Json when you really need it.

- MySQL is less of a joke than MongoDB is. They similarly started by someone who didn't know anything about databases and learned about them on the go. Actually both of them started as much faster alternatives to other databases, both ended up having complete rewrite of its engine written by someone from outside that knew their stuff. MySQL ISAM then MyISAM and then InnoDB (written by an outsider). Similarly MongoDB got a WiredTiger written.
  - This is contrasting with PostgreSQL, where correctness and reliability was #1 from the beginning. It started as an awfully slow database, but performance for improved and we now have correct, reliable and fast database.

- what was the reason that your team decided to work around the problem instead of migrating away from MongoDB?
  - Once you find yourself having to patch it too often, you start thinking about migrating away.

- MySQL still has no transactional DDL (and I think still even autocommits if you try). This is a major difference from Postgres which I believe supports everything short of dropping tables.

- Mongo has been related to "perpetual irritation" up to "major production issue" at all three of my last companies.
  - For as easy as it is to use jsonb in Postgres, or Redis, or RocksDB/SQLite, or whatever else depending on your use case - I can't find any reason to advocate its use these days
- Postgres 12 has generated columns, so you can throw your data in a jsonb column and have Postgres pull data out of it into separate columns for indexing for example.
  - Generated columns are not necessary for indexing in Postgres, you can create an index on any expression based on the record (supported by many versions now).

- ## [Jepsen Disputes MongoDB's Data Consistency Claims | Hacker News_202005](https://news.ycombinator.com/item?id=23285249)
- We encourage MongoDB to report Jepsen findings in context: while MongoDB did appear to offer per-document linearizability and causal consistency with the strongest settings, it also failed to offer those properties in most configurations.

- Postgres most certainly does fsync by default.

- There is much amusement to be obtained from reading Jepsen's report:
  - "MongoDB’s default level of write concern was (and remains) acknowledgement by a single node, which means MongoDB may lose data by default.... Similarly, MongoDB’s default level of read concern allows aborted reads: readers can observe state that is not fully committed, and could be discarded in the future. As the read isolation consistency docs note, “Read uncommitted is the default isolation level”.
  - We found that due to these weak defaults, MongoDB’s causal sessions did not preserve causal consistency by default: users needed to specify both write and read concern majority (or higher) to actually get causal consistency. MongoDB closed the issue, saying it was working as designed, and updated their isolation documentation to note that even though MongoDB offers “causal consistency in client sessions”, that guarantee does not hold unless users take care to use both read and write concern majority. A detailed table now shows the properties offered by weaker read and write concerns
- That sounds like a valid redress, or am I missing something ?

- MongoDB's big problem is that their present user base does not want the problems fixed, particularly at default settings, because it would mean going slower. Their users are self-selected as not caring much about integrity and durability. There are lots of applications where those qualities are just not very important, but speed is. People with such applications do need help with data management, and have money to spend on it.

- 👉🏻 MongoDB started life as a database designed for speed and ease of use over durability. That's not a good look for a database.
  - I think it depends. One could say the same about Redis, but it's wildly successful and people love it.
  - The difference is now they are advertised. Redis makes no claims to be anything other than what it is - a fast in-memory database that has some persistence capability but isn't meant to be a long-term data store. MongoDB, on the other hand, made (and continues to make) claims about being comparable in atomicity and durability to traditional SQL databases (but magically much faster!) that haven't withstood scrutiny.
  - Keep in mind, too, that most data ain't worth much. It's one thing to entrust data of low value in MongoDB; another to store mission-critical data in it. 
- I think 90% of the Mongo installs I've been exposed to were set up by people that were tired of fighting with Hibernate configurations and schema migrations.

- I find with the MongoDB style of database, it's easy to prototype without needing to do the heavy schema management of SQL. But, if you need a traditional ACID database, the flexibility comes with punch in the groin technical debt.

- If you're looking for MongoDB done right, it does exist and it's called RethinkDB. For some reason it didn't catch on and become popular — but it's nicer, and most importantly, it doesn't lose your data.
- The only other correct distributed database with strict serializable guarantees that I know of is FoundationDB, which nowhere near as easy to use as RethinkDB is (but it's somewhat easier with their document layer, which pretends to be MongoDB, just done right).

- ## [Was MongoDB Ever the Right Choice? | Hacker News_201903](https://news.ycombinator.com/item?id=19497817)
- I would argue that MongoDB is not—and has never been—the best choice for solving any particular technical problem. 
  - But it had some other "advantages" over other, better solutions – in that it was easier to set up, didn't require schema definition, had a passable clustering story etc.

- MongoDB gets bad press on Reddit / HN probably because of past marketing campaigns, but nowdays it's a very solid solution.

- In what situations do you feel MongoDB is a better solution than Postgres? The latter is both relational and document-oriented as required.
  - Setting up a simple cluster without relying on addons, or having to worry about which server in the cluster your writes are going to (bisected application configurations)

- Elasticsearch can index documents dynamically, and doesn't require a schema to create an index. Dynamic data types for fields may not always produce what you want, but it's possible to define a partial schema for the fields that are important and let Elasticsearch handle the rest. The query language is verbose but I would hesitate to call it a nightmare. You can always search using the Lucene query language, and SQL support is landing sometime soon.

- Someone has mentioned PostgreSQL jsonb, which basically works the same way as Mongo, although I won't argue the query syntax is easier to learn. But also, PostgreSQL supports arrays, so you can have much more native tags as well, and it can be indexed and searched in a more traditional SQL fashion.

- After using mongodb for many years, I haven't run into a use case where I should have used it over SQL. The only benefit is rapid prototyping for me
  - But you pay for it big time as you go and find that anything difficult means you'll have to do backflips and more requests to get things done and get used to very strange and verbose nested json queries. It's the 10-15% use cases that are really hard. 
  - NoSQL is especially annoying when needing any type of joins because despite your best planning, it still happens. 
  - There were many cases I needed to fallback on postgres to get stuff done and have a second source of data to sync and then I was wondering why I didn't just do it all in postgres first.

- The main reasons I chose Couch over something relational like MySQL was essentially 1. to have a a clear path for data to go as JSON from server/API/client without the need for mapping, 2. Schemaless to allow for quick iterating and development, 3. Easy to start with local first development and then rollout for deployment. 
  - I still needed to create externalized "views" of the data that either combined data from multiple documents and the need to hide private data. I still needed to serve lists of data in pages. More importantly I needed to provide a lot of adhoc reporting over the various data I'm storing across multiple Couch dbs.
  - The views and paging are all easily solvable with Couch, but so much easier to implement using SQL and it feels like I'm just pushing that need or compensating somewhere else in the implementation. But the friction around quick reporting has made me second guess choosing Couch/document based vs. something like a MySQL/ORM.
  - Once you understand the way that views and map/reduce work, it's super powerful for doing large scale statistics on data sets quickly. Only thing that I wish for is a Mongoose adapter for couchdb so I can use it as a backend for when an open-source project wants to use MongoDB (Looking at keystone.js for example)...

- ## [Amazon DocumentDB, with MongoDB compatibility | Hacker News_201901](https://news.ycombinator.com/item?id=18869755)
- I don't understand why people are reacting to it so aggressively. 
  - That's basically how AWS works, they did the same to Apache Kafka with Kinesis, Prestodb with Athena, PostgreSQL and MySQL with Aurora, Redis with ElastiCache and many others over the last 4 years so it's not new.
  - It took too long for the open-source community to figure out that the cloud providers are killing them, now it's too late. Well played, AWS.

- MongoDB Atlas is the name of the cloud service run by MongoDB themselves, with which Amazon DocumentDB competes.
- MongoDB Atlas runs the full implementation of MongoDB in the cloud.
- Many features of MongoDB are documented as not being implemented by DocumentDB: these include change streams, many aggregation operators including `$lookup` and `$graphlookup`.

- So now AWS DocumentDB, Azure CosmosDB, and even Apple's FoundationDB have a MongoDB compatible API. I expect other multimodal databases to offer the same soon enough.
  - when they have a restrictive license.

- 🤔 is there any real reason to use Mongo over Elasticsearch?
  - ES grew out of Lucene, which provided an inverted index of all the text in a document, with a bunch of NLP related features bolted onto that.if all you need is a text index on a document store with a static schema, it does its job reasonably well.
  - In my experience Mongo truly is developer-friendly as long as you don't try to use it as a full-blown transactional database with lots of complex data shapes and indexes.
- Elasticsearch is a distributed index, not a reliable document store. You can expect availability problems and data loss. This is fine, because you can rebuild the index from your source of truth.
  - In my experience with ES, definitely don't treat it as a source of truth; allow it to be rebuilt.
- Yes. Elasticsearch is not nearly as easy to use and is not really designed to be a transactional database.

- CouchDB "replication" was designed to be "master-master" (or "no master" sort of) where replication is not a coordinated process but a distributed push/pull of concurrent revisions with basic conflict resolution rules.
  - Whereas, Mongo only built support for classic RDBMS-style replication where one database serves as the master or primary, and any number of secondaries can try to keep up with it.

- ## 🍃🐘📡 [Goodbye MongoDB, Hello PostgreSQL (2015) | Hacker News_202103](https://news.ycombinator.com/item?id=26420665)
- Proper replication topologies (e.g. multi-master configurations) and JSON columns killed the NoSQL movement.
- There are plenty of modern, distributed RDBMSes that make sharding transparent to the user (E.g. cockroachDB, yugabyte, vitess, many cloud offerings, etc.). Most NoSQL databases end up adding transactions because they are important, and thus the scale advantages for NoSQL systems over relational databases are diminishing, if remaining at all.

- At this point I would consider Postgres only in the following case: If my data structure is like a non-tree graph. In that case I would expect to do multiple complex join and expect transaction consistency between tables.

- Is there a situation where I SHOULDN'T use Postgres?
- Postgres is incredibly flexible and scales beyond what most projects will ever need. We use it both as a very large scale CMDB store and as an small embedded DB 
- Use cases where we hit road bumps earlier were:
  1. High churn data. Postgres copies data for each rite update and then vacuums to clean the old versions. These use cases dominated our DB load and moving them out helped a lot.
  2. Large JSON blobs. Postgres automatically compresses and will pull large (~>8kB) columns into a separate “toast” table. This makes sense but also means they are often a real bottleneck if you expect to work with larger JSON blobs as you core model. pg is great for JSON, but if you are using it at scale do pre-work and testing of this factor and how it plays with your model.
  3. Of course, long term archive of data objects is much more cost efficient and scalable in an object store like S3.
  - Bet on Postgres. Whatever you use case it will work great until you are large enough to really understand your data and optimize for your business.

- If you find yourself reaching for EAV because you have schema-less data (custom fields, for example), nosql can make your life so much easier, as long as you understand the trade-offs.

- What surprises me is that so far none shoehorned Postgres on top of FoundationDB.

- ## 🍃🐘 [Goodbye MongoDB, Hello PostgreSQL | Hacker News_201503](https://news.ycombinator.com/item?id=9178773)
- Learn SQL rather than wrapping it.
  - It's not so much about not wanting to write/understand SQL (both are still very much required), but about composability. If you want to re-use bits of a SQL query written as a string literal your only option is string concatenation or using some kind of string builder/template system. 
  - In both cases there's little validation of the query's correctness (syntax wise) until you actually run it.
- CTEs and SQL functions in PostgreSQL strike a good balance in the composability department for me, while still being able to write SQL.

- ## [Never use MongoDB (2013) | Hacker News_202102](https://news.ycombinator.com/item?id=25990400)
- I’ll just say a great classic: pick something you know, use it well, build something good, end of story!

- SQL databases don't support easy schema evolution, sharding and so on.

- We've used MongoDB at our SaaS and have grown to well over $1m ARR and never had an issue.

- ## [Why You Should Never Use MongoDB | Hacker News_201311](https://news.ycombinator.com/item?id=6712703)
- We have a CMS application that supports creating custom web forms, which each have a different set of fields which hold different types of data. Email addresses, multi-select radio buttons, text areas, etc. Some forms only gets submitted once or twice, others are submitted many thousands of times. To store this in a normal relational database you either need many tables, or you need to normalize your data (probably Entity-Attribute-Value (EAV) style). We didn't want hundreds of tables, and designing a good EAV system can be tough (Magento anyone?), so we looked at other options.
  - We've settled currently on using MongoDb, with one collection to hold the (versioned) definition of each form's fields (data type, order, validation rules, etc), and another collection to hold all of the submissions (this is a laaarge collection). There _is_ a "relation" between the form definition and the submissions, but because you always query for submissions based on the form (by form_id), you don't really need to do "JOINs" (you just query out the form definition once, before the submissions). Also, because the forms are versioned, and each submission is associated with a particular version of a form, there is no need to retroactively update the de-normalized schema of past submissions (although this does limit your ability to query the submissions if a form is updated frequently - or drastically). It's not perfect, but this use case for MongoDb has been working well for us so far.

- A good simple use-case for a document database (could be MongoDB, but not necessarily) is configuration and system "schema" type data. For example, storing all of a user's settings and preferences into a document keyed by the user's Id.
- We use it for event storage in the event sourced parts of our app. For the rest of our data, we're currently migrating off of Mongo to Postgres due to an experience similar to the OP's.

- ## [Don't use MongoDB | Hacker News_201111](https://news.ycombinator.com/item?id=3202081)
- Anyone with half a brain can go look at the MongoDB codebase and deduce that it's amateur hour. It's start up quality code but it's supposed to keep your data safe. That's pretty much the issue here -- "cultural problems" is just another way of saying the same thing. 
  - Compare the code base of something like PostgreSQL to Mongo, and you'll see how a real database should be coded. Even MySQL looks like it's written by the world's best programmers compared to Mongo.
  - Most RDBMSes have been around for 10+ years, so it's going to take a long, long time for Mongo to catch up in quality. But it won't, because once you start removing the write lock and all the other easy wins, you're going to hit the same problems that people solved 30 years ago, and your request rates are going to fall to memory/spindle speed.
- I looked at using BSON in a project a while back, and ended up scrapping it mainly due to perceived poor code quality. Plenty of potential errors ignored, unclear error messages, unsafe practices.
  - I was also turned off by the sloppy use of memory. Heap allocated objects returned from functions with poor checks to see if anyone manages that memory on the other side. Lots of instances of strcmp, strcpy and similar unsafe string/buffer manipulation functions.

- These are not new approaches to data modelling.
  - Document databases, network databases and hierarchical databases (IMS, CODASYL etc) predate relational databases by decades.
  - Relational is the universal default for a simple reason. When first introduced it proved to be far better, in every conceivable way, than the technologies it replaced.
- I agree entirely - I think when people rebel against "relational databases" they're actually just realizing that the normalization fetish can be harmful in many application cases.
- The relational model is ideal in many circumstances. However, it breaks down in semi-structured content, content where---parentheses for grouping---(hierarchical structure is important, data is seldom written and frequently read, and where read performance navigating the hierarchy is most important) and so forth.

- One of the things that I love about Couch is that the standard way to shutdown the process is simply doing a kill -9 on the server process. No data loss. No Worries. Want to back up your data? rsync it and be done with it. Couch may have its warts, but it is damn reliable.

- ## 🆚️ [Cassandra vs MongoDB vs CouchDB vs Redis vs Riak comparison | Hacker News_201012](https://news.ycombinator.com/item?id=2052852)
- This article is mostly marketing phrases from the websites of the various projects. 

- While I'm at it I like to share that in this exact days I'm working at a Redis disk back end.
  - The idea is that everything is stored on disk, in what is a plain key-value database (complex values are serialized when on disk), and the memory is instead used as an object cache. It is like taking current Redis Virtual Memory and inverting the logic completely, the result is the same (working set in memory, the rest on disk), but this implementation means that there are no limits on the data you can put into a single instance, that you don't have slow restarts (data is not loaded on memory if not demanded), and there isn't to fork() to save. Keys marked as "dirty" (modified) are transfered to disk asynchronously as needed, by IO threads.

- My understanding is that in CouchDB you can't guarantee that older versions of documents will still exists (they might be there, but they could have been removed by compaction or not replicated). However, there is a fairly nice way of storing older versions of documents - hold older versions as file attachments on the document.
  - This is probably the biggest misunderstanding of couchdb, imo. The versioning system in couchdb is only there to make the seamless replication possible. There's no guarantee that previous versions will exist at a future time, like in git.
- Trying to use CouchDB's versioning system seems like depending on a very leaky abstraction. That you can see it's versioning is a side-effect of how it behaves; not a feature it is providing. If you need versioned records, you are likely better off identifying your versioning requirements and building to those than trying to piggyback off of something else poorly suited.
