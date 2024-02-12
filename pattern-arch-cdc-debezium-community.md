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

- ## 

- ## 🌰 [Streaming Databases in Real-Time with Kafka, Debezium, and MySQL | Hacker News _201703](https://news.ycombinator.com/item?id=13995648)
- Totally agree! Once we were very close to implement a very similar scenario (stream of events, some lightweight processing, kafka for distribution, hbase/solr for storage). 
  - If you go for such thing, better be sure that your business analysts are on the same page as you. 
  - Otherwise, instead of a clean event sourcing model, you may end up with some sort of message protocol that spans across the schema/data format/business logic/weird requirements. It is just that this thing will become your new "model".

- The "traditional" Kafka infrastructure (i.e. LinkedIn) uses Kafka as the source of truth. Everything gets written directly into Kafka and makes its way from there. This is a powerful concept, but involves giving up a lot of advantages of a RDBMS.
  - This is the first time I've heard of the approach WePay uses and I really like it. Now MySQL is the source of truth and Debezium pipes it into Kafka, allowing you to leverage Kafka while still using MySQL as your primary data store. (Or Postgres, which Debezium includes support for.)
