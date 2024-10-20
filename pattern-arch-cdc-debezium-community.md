---
title: pattern-arch-cdc-debezium-community
tags: [change-data-capture, community, debezium, event-sourcing]
created: 2024-02-12T17:46:39.296Z
modified: 2024-02-12T17:47:34.152Z
---

# pattern-arch-cdc-debezium-community

# guide

# dev

# discuss-stars

- ## 

- ## 

- ## [Is Event sourcing using Database CDC considered good architecture? - Stack Overflow](https://stackoverflow.com/questions/54379623/is-event-sourcing-using-database-cdc-considered-good-architecture)
- So here's the problem: unless you are in some extreme edge case, your database is probably some general purpose application that you are customizing/configuring to meet your needs. Change data capture is going to be limited by the fact that it is implemented using general purpose mechanisms. So the events that are produced are going to look like general purpose patch documents (here's the diff between before and after).
  - But if we trying to align our events with our domain concepts (ie, what does this change to our persisted state mean), then patch documents are a step in the wrong direction.

- ## 🤔 would it be hard to simulate a stream of change-data-capture?
- https://twitter.com/MichaelDrogalis/status/1711844926642848132
  - It required a few extra functions, but it works great. 
  - It builds off the idea of state machines that I talked about last week.
  - Modeled after @gunnarmorling 's Debezium
  - 提供了事件数据json示例
- Harder than it looks!
  - It was! Lots of little rules, like an upsert can't happen before an insert, and not all keys should change on every upsert, etc.
  - I've been there for sure! Wracked my brain. Probably top 5 hardest programming problems I've worked on.
- Is this a paid only offering? 
  - yeah

# discuss-cdc/change-data-capture
- ## 

- ## 

- ## 

- ## 📝 "CDC Is a Feature Not a Product": Some thoughts on Change Data Capture as a Service.
- https://x.com/gunnarmorling/status/1847280389443706914
  - [CDC Is a Feature Not a Product - Gunnar Morling _201410](https://www.morling.dev/blog/cdc-is-a-feature-not-a-product/)
- 100% this, CDC must be a part of a larger platform to actually form a product. It’s just a piece somewhere at the begging of data pipeline.

- What if every database and SaaS provided near real-time (e.g. Every minute) data dump in Iceberg format export to blob storage?

- ## The number one cause of production database outages I see these day is because of CDC tools. 
- https://x.com/craigkerstiens/status/1824114371737616794
  - Enter CDC (change data capture) basically taking each record/update to data that happens to your database and replicating it over to a data warehouse. 
  - In almost every case I've seen this increases the issues on the production database and causes outages–not an exaggeration. 
  - Several tools recommend polling for updates and changes which is absolutely terrible. All can hold up replication slots at times to unhealthy levels and quickly fill up a disk. 

- Since PG 13 or so, you can configure a max size a slot can hold on to, at the price of course that consumers need to re-snapshot when being offline for too long.
- one culprit is the IMO unfortunate design that Postgres replication slots are bound to one database, while the WAL is global for the entire host. This can trigger WAL pile-up when combining high/low traffic DBs on one host.
- Tl; dr CDC is actually a hard category of problems within distributed systems. It’s not as simple as polling an API or cron jobs to copy files around. The WAL is vital to the database’s O. S. level operations so extracting business events from it is not trivial.
- That's what max_slot_wal_keep_size is for
- I think those issues are due to lack of system understanding by Management who priorize CDC over production OLTP. You can always drop your CDC pipeline in case of a Wal pile up.
- So, the CDC applications you have seen were poorly implemented or with tools that do not perform CDC correctly. I have applied CDC in large retail companies, banks, and education companies that buy dozens of smaller colleges, and I have never had any problems.
  - #Debezium with Oracle, SQL Server and now DB2 Z/OS. Everyone is happy, and little OPEX
- For Oracle, it polls the LogMiner views (not the actual data tables), the overhead for Postgres and most other connectors is much lower.

- ## Seven Ways to Put CDC to Work
- https://twitter.com/gunnarmorling/status/1720468080281702888
  - [Seven Ways to Put CDC to Work](https://www.decodable.co/blog/seven-ways-to-put-cdc-to-work)

- ## [Why NoSQL | Hacker News_202110](https://news.ycombinator.com/item?id=28767996)
- > Use Debezium or similar to broadcast entity changes to a Kafka topic keyed on entity id. If you want to retain all changes (e.g., for event streaming), then use an appropriate retention strategy. If you want to retain only the latest state, use log compaction - it will retain the latest record with a given key.
- Yes, now keep tugging(沿某方向拉或拖) on the thread of that thought. 
  - If you try to write code to reconstruct the state of your relational database based on those changes, you've got two copies of your logic that will inevitably get out of sync, and you'll have bugs that you only discover when you try to actually do it. (And if you only record differences between writes that actually made it into the relational database, you haven't solved the original problem of data being lost because writes are rejected). 
  - What you want to do is instead make those Kafka events the primary "source of truth" and construct the "current state of the world" based on that, i.e. event sourcing.
  - You don't, and can't, make use of transactions with that approach - you get (eventual) consistency because each log is ordered, which gives you the properties that you want with less of the downsides (deadlocks), but writing and reading the eventual results of that write is a fundamentally async process (which is good in the long term - it forces you think about your dataflow and avoid loops - though it might involve more work upfront). 
  - 👉🏻 And you don't really have relationality - if you need a relation in your live dataflow, you'll generally join at the event pipeline level and make the joined thing its own stream (much like a materialized view in SQL-land). You can build secondary indices etc. but those are explicitly a secondary thing layered on top of your primary datastore.

# discuss-debezium
- ## 

- ## What could be a valid use case for also updating the primary key on upserts? 
- https://twitter.com/thegeeknarrator/status/1763866449360162968
  - The way Debezium works in this case is it creates a Delete and an Insert event with the new key. 
  - I believe this is how CDC is supposed to work and I think it makes sense. Thoughts? 

- This should only occur when using some business key as the primary key, say an email address. I'd always advise to use immutable surrogate(替代物；代用品) keys instead. That way, there are no ordering concerns (delete + insert with new key may yield different partition).
  - Yes, that’s is what my recommendation was. Delete and insert going to different partitions wasn’t really an issue in this case, but yes could be a concern.

- ## 🌰 [Streaming Databases in Real-Time with Kafka, Debezium, and MySQL | Hacker News _201703](https://news.ycombinator.com/item?id=13995648)
- Totally agree! Once we were very close to implement a very similar scenario (stream of events, some lightweight processing, kafka for distribution, hbase/solr for storage). 
  - If you go for such thing, better be sure that your business analysts are on the same page as you. 
  - Otherwise, instead of a clean event sourcing model, you may end up with some sort of message protocol that spans across the schema/data format/business logic/weird requirements. It is just that this thing will become your new "model".

- The "traditional" Kafka infrastructure (i.e. LinkedIn) uses Kafka as the source of truth. Everything gets written directly into Kafka and makes its way from there. This is a powerful concept, but involves giving up a lot of advantages of a RDBMS.
  - This is the first time I've heard of the approach WePay uses and I really like it. Now MySQL is the source of truth and Debezium pipes it into Kafka, allowing you to leverage Kafka while still using MySQL as your primary data store. (Or Postgres, which Debezium includes support for.)
