---
title: pattern-arch-event-sourcing-blog
tags: [blog, event-sourcing]
created: 2023-09-13T14:37:36.816Z
modified: 2023-09-13T14:37:51.659Z
---

# pattern-arch-event-sourcing-blog

# guide

# blogs
- [kappa architecture vs event sourcing](https://github.com/tschudin/ssb-icn2019-paper/issues/6)
# blogs-vendors

## [wix: Event Driven Architecture - 5 Pitfalls to Avoid_202208](https://medium.com/wix-engineering/event-driven-architecture-5-pitfalls-to-avoid-b3ebf885bdb1)

- At Wix we have been gradually migrating our growing set of microservices (currently at 2300) from the request-reply pattern to event driven architecture over the last few years
- Below there are 5 pitfalls that Wix engineers have encountered during our experimentation with event driven architecture.
  - For each pitfall I provide battle-tested proven solutions used at Wix today.

### 1. Write to db and then fire event without atomicity

- Consider for example a simple ecom flow (we will use this example throughout this article)
  - Once the payment processing is done, the product inventory should be updated to reflect that the product is reserved for the customer.
  - Unfortunately, writing the payment-complete status to the database and then producing a “payment completed” event to Kafka (or some other message broker) is not an atomic operation. 
  - There could be situations where only one of the actions actually happens
  - For example, cases such as the database being unavailable, or Kafka being unavailable, could lead to data inconsistency between different parts of your distributed system. 
  - In the case above Inventory levels may become inconsistent with actual orders.

- There are several ways to mitigate this issue. At Wix we utilize two ways

- Atomicity Remedy I — Greyhound resilient producer
  - The first one is our own messaging platform called Greyhound, that allows us to make sure the event is eventually written to Kafka via a resilient producer.
  - One downside of this mitigation is that you can end up with out-of-order processing of events downstream.

- Atomicity Remedy II — Debezium Kafka source connector
  - The second way to make sure both DB update action and Kafka produce action happen and that data remains consistent is using the Debezium Kafka connector. 
  - Debezium connector allows to automatically capture all the change events (CDC) that happen in the database (For MySQL via binlog) and produce them as Kafka events.
  - Kafka Connect together with Debezium DB connectors guarantees that events will eventually be produced to Kafka. 

### 2. Using Event sourcing everywhere

- Event sourcing is a pattern where instead of updating an entity’s state upon a business operation, the service saves an event to its database. 
  - The service reconstructs an entity’s current state by replaying the events.
  - These events are also published on an event bus such that other services can also create materialized views on other databases that are optimized for queries by replaying the events.
- While there are certain advantages to this pattern (a reliable audit log, performing “time travel” — the ability to get the state of your entity at any point in time, and building multiple views over the same data), it is by far more complex than CRUD services that update the state of an entity stored in a database.
- 👎🏻 Disadvantages of event sourcing include:
- 👉🏻 Complexity 
  - In order to make sure read performance is not affected by a growing list of events you need to play, entity state snapshots have to be taken from time to time to reduce the performance penalty.
  - This increases the system complexity with a background process that may have its own issues and when it does the data remain stale. 
  - On top of this, having 2 copies of the data means they might get out of sync.
- 👉🏻 Snowflake nature 
  - Unlike CRUD ORM solutions, It’s harder to create common libraries and frameworks to ease development that can globally solve snapshotting and read-optimizations that can fit for every single use case.
- 👉🏻 Only supports eventual consistency (problematic for read-after-write use-cases)

- 💡 Event Sourcing alternative — CRUD+CDC
- Utilizing both simple CRUD capabilities and publishing database change events (CDC) for downstream uses (e.g. creation of query-optimized materialized views) can reduce complexity, increase flexibility and still allow for Command-Query Responsibility Segregation (CQRS) for specific use cases.
  - For most of the use-cases, the service can expose a simple read endpoint that will fetch the entity’s current state from the database. 
  - As scale increases and more complex queries are needed, the additional published change events can be used to create custom materialized views specifically tailored for complex queries.
- In order to avoid exposing DB changes as a contract to other services, and creating a coupling between them, the service can consume the CDC topic and produce an “official” API of change events similar to the event stream created in event-sourcing pattern.

### 3. No Context Propagation

- Unlike with the request-reply model, there is no explicit chain of HTTP/RPC requests to follow. 
  - Debugging code is harder as event handling code is spread out across the service code instead of being sequentially traceable by clicking into function definitions usually found in the same object/module.

- Automatic Context Propagation
  - Automatically adding identification of the broader request context for all of the events, makes it really simple to filter for all events related to the end-user request. 
  - At Wix, Greyhound automatically propagates the end-user request context when events are produced and consumed. 
  - In addition, the request context is found also in logs infrastructure, such that logs can be filtered for specific user requests.

### 4. Publishing Events with Large Payloads

- When processing large event payloads (payloads bigger than 5MB, e.g. Image Recognition, Video Analytics, etc…) it may be tempting to publish them to Kafka (or Pulsar) but there is a risk of greatly increasing latency
- Large Payloads Remedy I — Compression
  - Both Kafka and Pulsar allow compression of payloads. You can try several compression types (lz4, snappy, etc.)
  - 👉🏻 Compression on Kafka level is usually better than application level, as payloads can be compressed in batches and thus improve compression ratio.
- Large Payloads Remedy II — Chunking
  - to split the messages into chunks.
  - While chunking is already a built-in feature of Pulsar (with some limitations), for Kafka chunking has to happen on the application level.
  - The basic premise is for producers to send out the chunks with additional metadata that helps consumers to re-assemble them.

- Large Payloads Remedy III — Reference to Object store
  - The final approach is to simply store the payload in an object store (such as S3) and pass a reference (a URL usually) to the object in the event payload. 
  - These object stores allow to persist any required size without impacting first byte latency.
  - It’s important to make sure the payload is fully uploaded to the object storage before the link is produced, or else the consumer will need to keep retrying until it can start downloading it.

### 5. Not handling duplicate events

- The term for making sure a side-effect of a duplicate event only happens once is Idempotency.

- Idempotency Remedy — revisionId (versioning)
- Optimistic locking technique can serve as inspiration in cases where idempotency of event processing is needed. 
  - With this technique, the current revisionId (or version) of the stored entity is first read before any update occurs. 
  - If more than one party tries to update the entity (while incrementing the version) at the same time (concurrently), the 2nd attempt will fail as the version will no longer match with what it read before.
- In the case of idempotent handling of duplicate events, the revisionId has to be unique and part of the event itself in order to make sure that two events don’t share the same id and that 2nd updates on the same revisionId will (silently) fail even if does not happen concurrently.
- Specifically With Kafka, there is a possibility to configure exactly once semantics, but still DB duplicate updates can happen due to some failure. 
  - Luckily the txnId in this case can just be the topic-partition-offset which is guaranteed to be unique.

### Summary

- A migration to event-driven architecture can be gradual in order to reduce risks involved with it including harder debugging and mental complexity.
- As a consequence of this gradual migration approach, I strongly recommend to adopt the CDC pattern (Database changes streamed as events) as a way to both ensure data consistency (pitfall #1) and avoid the complexity and risks associated with full blown event-sourcing (pitfall #2). 
- The CDC pattern still allows to have the request-reply pattern in place side by side with the event processing pattern.
- The CDC pattern still allows to have the request-reply pattern in place side by side with the event processing pattern.
- Remediation for Pitfalls #4 and #5 are for more specific uses cases

- ### Event Driven Architecture — 5 Pitfalls to Avoid-/twitter_202208
- https://twitter.com/boyney123/status/1559837875834945536
- I'm curious what database and framework you used for event sourcing?
  - I think most cases at @WixEng use #mysql. There are 2-3 custom made libraries created at wix to help with ES implementation.
- One thing I would say is that eventual consistency isn't a requirement of event sourcing.  For instance @marten_lib leverages Postgres transactions to create strongly consistent projections.

- ### [Event Driven Architecture — 5 Pitfalls to Avoid : coding](https://www.reddit.com/r/coding/comments/wor4h2/event_driven_architecture_5_pitfalls_to_avoid/)
- Looks overcomplicated to me. Why just save an event in queue (async) or trigger (sync), and if it fails, rollback the transaction?
  - Wix services don't usually implement the saga pattern (with transaction aborting) but go for best-effort retry mechanism (see more in this post in pattern #4)

- Indeed at Wix there is a hybrid architecture of both request-reply and event-driven.
  - how come 2300? Wix hosts and renders more than 100 million websites, with complete back-office/business solutions as well and an open platform for plugins. with many different verticals (e.g. stores, restaurants, hotels, events, photography). It's a huge production eco-system

- 3 No Context Propagation. This should be number 1 on any list, unless the list also contains something about emergent behavior.

## [wix: The Reactive Monolith - How to Move from CRUD to Event Sourcing_202109](https://www.wix.engineering/post/the-reactive-monolith-how-to-move-from-crud-to-event-sourcing)

- While the traditional CRUD approach to system design focuses on state and how it is created, updated and deleted in a distributed environment by multiple users, the event sourcing approach focuses on domain events, when they happen and how they express business intent. 
  - The state, in the event sourcing approach, is a materialization from events, which is just one of many possible usages of the domain events. 

- 
- 
- 

- ### 🤔 [How to Move from CRUD to Event Sourcing | Hacker News_202109](https://news.ycombinator.com/item?id=28691728)
- I used to be really excited about event sourcing but yeah, its usually just **over-engineering**. 
  - It appeals to the nerd in me because its a powerful & clean model - events are immutable, your entire database can theoretically be reconstructed at any point in time by just replaying an event log up to time X. 
  - In the ideal form its sort of the highest fidelity version of data storage, throwing nothing away, supporting all ways of querying as materialized views or dependent DBs built on the stream. Its beautiful.
- But also we live in reality. 
- 👉🏻 DBs use checkpoints because storing/replaying an event log from time 0 would take ungodly(骇人的；无法容忍的) amounts of space and time. 
  - You deleted or resized a column to save some space? Lol no, the event log lives forever. 
  - You wanted to use SQL, a battle tested language to query your data? Lol no, the database is "inside out" so tough luck buddy, you're building the database now. 
  - Sure you might have to rebuild compaction, joins, query languages, concurrency control and the other 100 things a DB gives you, but on the plus side that one audit log that you could have built with some glue and a few INSERT triggers in Postgres is now an elegant map/reduce on your 100TB dataset! Yay!

- For non-trivial amounts of data you should combine event sourcing with snapshots - i.e. a somewhat up-to-date materialized view/DB table - so you don't have to start for 0. At that point you can delete older events or move them to cold storage.
  - A valid question then is: "what do you gain over just using the table"? You gain a well-described model of your business domain, with very clear actions about what should happen on which real-world event, and an audit log. Whether that's worth it depend on your use case.
- Secondary benefits include easily being able to share events for new apps or use-cases, business analysts really like them, and making it unlikely things go wrong because data is in an inconsistent state.

- ES is the C in CQRS though. If you're using it for the Q too, then it's no wonder you'll quickly get in a bad way. It's specifically not designed for that.
  - the benefits of ES come on the write side of the equation. Expecting it to solve read-side problems will inevitably lead to disappointment.

- Materialized views are what you should be using, not reconstructing the state from the event log every time. That gives you access to SQL and everything to do with it.
  - And in reality, the event log does live forever in the real world outside of your system. Attributes of your aggregates from last year are still valid for events related to last year, even if they're now deprecated or no longer in use.
  - CQRS/ES is about system design that evolves. It evolves in a much cleaner and easier way if you follow it.
  - Is it perfect? No. There are some gnarly problems related to, for example, GDPR's "right to be forgotten", but that needs to be solved across database backups as well.

- I would like to see answers to the question: why move from Crud to event sourcing. Because I have seen at least 5 moderate projects trying to integrate ES. They all failed in the sense that either people didn't understand the code anymore, huge integration times, performance issues and even complete project cancellation because of all people walking away

- I understand this thread is about dumping on ES... However, I must notice in your case it was an audit log. An ES system wouldn't work at all without access to events.
  - If the ES is "unnecessary", then it's not ES by definition. If events are not your source of truth, it's not event sourcing, just event logging.

- 👉🏻 Two examples of systems that use a variant of event sourcing:
  - relational database systems (their journals and async replication in particular)
  - git
- Git doesn't really store file changes as events, rather, it's a long chain of state snapshots, in something like a persistent data structure. Sure, the history is all there, but so is the current state in its most efficient form.
- DB transaction logs might be considered event sourcing by some definition, but their use is very different. It's purely a technical trick. As a consequence, logs are truncated as often as possible/reasonable, and you never rerun the transaction log from time zero. Very different from the event sourcing idea to keep events as long as possible.

- I have never implemented ES, although it seems to be useful to have the most simple version of it in place: just a queryable log of versioned events and the ability to replay it.

- Event sourced systems are actually great, as long as they aren’t branded as such. Most of the time it’s totally stupid and the state of the system isn’t reproducible anyway unless the event code is never modified.

- Extra layer of complexity. More development time. More tech dependencies. Don't use it when not needed.

- Event sourcing is decent when you ingest a lot of things that are mostly one way and immutable once they come into your system.
  - If you have bidirectional communication, you wind up contorting yourself into a pretzel to bury "state" into your event streams.

- It is striking that this thread attracts so much negative commentary, while a similar thread 49 days ago is the exact opposite. 
  - this one is about moving from CRUD, that is the most mainstream paradigm on software development into what is solution to a very niche problem, while the other is just about the solution

- As a proponent of Radical Simplicity, I'm always sceptical about event sourcing.
  - There are some benefits (I found it useful to replay events for example), but where I have seen it at work it makes things much more complex, the understanding of the system and the development of new features takes much longer.

- then you realize that the CRUD db you moved away from operates on event sourcing (WAL) anyway. And thus you’re just doing inner platform effect.
  - Correct, and many applications are using WAL via **CDC (Change Data Capture)** to gain some of the benefits of the CQRS/ES.
  - The problem is that the CRUD is only recording "What" change/mutation was done, but not "Why" by "Whom", and "When" it was done. With tailing WAL / CDC you can also capture the "When".
  - This can be partially mitigated by adding audit fields
- Yup a few fields gets you a long way, though I would recommend an audit log updated by triggers, rather than audit fields.
  - For example on my CRUD rails app, we use audit triggers in combination with setting a postgres local config variable with the username, the audit triggers pull the user info from the variables and record them into the DB. 
  - What kind of technology/data model do you use for the audit log? A timeseries db, just another table, or something else?
    - Another table in a different schema. Roughly this https://wiki.postgresql.org/wiki/Audit_trigger_91plus
- If you use log-based CDC, you typically don't need those timestamps, the WAL will contain and expose that information.
  - One way for capturing these intents is to log that information transaction-scoped in a separate table and then use downstream stream-processing to enrich actual change events (which contain the TX id themselves) with that metadata. 
  - I've blogged about one way for implementing this using Debezium and Kafka Streams a while ago

- It seems the benefits of eventsourcing can be had from using an immutable database. Auditing, Backing up state while the db is running, previous states and diffs.

## [GAT TechTalk #5 – Journey to DDD Through the Land of Dungeons, Dragons and Other Daemons_202210](https://www.globalapptesting.com/engineering/gat-techtalk-5-journey-to-ddd)

- 

- [GAT TechTalk #4 (DDD in Ruby)_202107](https://www.globalapptesting.com/engineering/gat-techtalk-4-ddd-in-ruby)
- 
- 

## [How Discord Stores Trillions of Messages_202303](https://discord.com/blog/how-discord-stores-trillions-of-messages)

- 
- 
- 
- 
- 

- [summary](https://medium.com/@iBMehta/how-discord-stores-trillions-of-messages-31ed9195c3e8)
- the evolution of message storage at Discord:
  - MongoDB ➡️ Cassandra ➡️ ScyllaDB
- In 2015, the first version of Discord was built on top of a single MongoDB replica. 
  - Around Nov 2015, MongoDB stored 100 million messages and the RAM couldn’t hold the data and index any longer. 
  - The latency became unpredictable. 
  - Message storage needs to be moved to another database. 
- Cassandra was chosen.
  - In 2017, Discord had 12 Cassandra nodes and stored billions of messages.
- At the beginning of 2022, it had 177 nodes with trillions of messages. 
  - At this point, latency was unpredictable, and maintenance operations became too expensive to run.
- reasons
  - Cassandra uses the LSM tree for the internal data structure. The reads are more expensive than the writes. There can be many concurrent reads on a server with hundreds of users, resulting in hotspots.
  - Maintaining clusters, such as compacting SSTables, impacts performance.
  - Garbage collection pauses would cause significant latency spikes
- ScyllaDB is Cassandra compatible database written in C++. 
  - Discord redesigned its architecture to have a monolithic API, a data service written in Rust, and ScyllaDB-based storage.

- [How Discord Stores Billions of Messages_201701](https://discord.com/blog/how-discord-stores-billions-of-messages)
  - [How Discord Stores Billions of Messages (2017) | Hacker News](https://news.ycombinator.com/item?id=28292369)

- ### [reddit: How Discord Stores Trillions of Messages : programming](https://www.reddit.com/r/programming/comments/11kj91n/how_discord_stores_trillions_of_messages/)
- Well this is big for Tokio. It's hard to imagine a bigger usecase for that technology than this, turns out it scales to it. Very impressive.
- There are certainly times when I think the Discord model would be better for productivity than how Slack does it.
- ScyllaDB and Rust weren't new for them tho, they've been using them since 2020.

### [How Discord Stores Trillions of Messages | Hacker News_202303](https://news.ycombinator.com/item?id=35048410)

- 🤔 Solid article. Is it fair to say that the "data services" layer is essentially a cache sitting in front of the database, or am I misunderstanding it's function?
- I work at Discord in infrastructure.
  - We use data services to do "data related things" that make sense to do at a central proxy layer. This may include caching/coalescing(联合；合并)/other logic but it doesn't always, it really depends on the particular use case of that data.
  - For messages, we don't really cache. Coalescing gives us what we want and the hot channel buckets will end up in memory on the database, which is NVMe backed for reads anyway so the performance of a cache wouldn't add much here for this use case.
  - In other places, where a single user query turns into many database queries and we have to aggregate data, caching is more helpful.
- In essence, yes, but strictly speaking, no. Instead of caching responses, that layer seems to only bundle equal requests.
  - So once a request is sent to the database, every other instance of the same request (e.g. "hey, fetch me all messages from server id 42") is put on hold. 
  - Once the initial request gets an answer from the database, that answer is distributed to the initial requester and all those which were on hold. 
  - Now if someone is late to the party, they will initiate a new request to the database, because the response is not cached.
# more
- [Datomic: Event Sourcing without the hassle | Hacker News_201811](https://news.ycombinator.com/item?id=18431382)
