---
title: lib-fwk-orm-knex-community
tags: [community, knex, orm]
created: 2023-01-22T19:51:36.967Z
modified: 2023-01-22T19:52:09.270Z
---

# lib-fwk-orm-knex-community

# guide

# discuss-stars
- ## 

- ## 🆚️ [How is Node.js Knex similar/different to Sequelize? - Stack Overflow](https://stackoverflow.com/questions/56028287/how-is-node-js-knex-similar-different-to-sequelize)
- Sequelize is full blown ORM forcing you to hide SQL behind object representation. 
  - Knex is plain query builder, which is way too low level tool for application development.
  - Better to use objection.js it combines good parts of ORMs without compromising power of writing any kind of SQL queries.

- ## [PgBouncer transaction pooling vs. Knex pooling? _201902](https://github.com/knex/knex/issues/3069)
- Using pg-pool for handling pooling when running knex in multiple processes sounds like nice idea. 
  - I have usually just set databases connection limit to (knex instance count * knex pool size), but having external shared connection pool might be a better choice in some cases, for example where you are not able to tune database settings to allow huge connection counts.

# discuss-partition/sharding
- ## 

- ## 

- ## [How to use `partition by` with knex?](https://github.com/knex/knex/issues/3391)
- Seems that partition by with order is not supported by Knex. like partition by user_id order by created_at asc

- Is there an alternative for this? E.g. a mixture of Knex functions with raw db query to create table with partitions using Knex migration?
  - There is an example that has worked for me.

- ## 🐛 [No option to partitioning a table _201710](https://github.com/knex/knex/issues/2289)
- Partitioning option is available for all knex supported databases
  - But 'Partitioning By' is available in following databases

- postgres 10.3 use PARTITION BY RANGE that is not supported by knex and I think also not supported from ORMs
# discuss-split-read/write
- ## 

- ## [Support for read replica connections? · mikro-orm/mikro-orm](https://github.com/mikro-orm/mikro-orm/issues/77)
- [feat(core): add support for read connections · mikro-orm/mikro-orm _201909](https://github.com/mikro-orm/mikro-orm/pull/116)

- ## [Knex Support for Read Replicas - Stack Overflow](https://stackoverflow.com/questions/47957116/knex-support-for-read-replicas)
  - Does Knex support routing queries to MySQL read replicas like Sequelize does? If so, how can I accomplish this?
- Not supported currently in knex (0.14). To accomplish something similar you need to create multiple knex instances and explicitly send read queries to read replica knex instances and write queries to master instance. There has been discussion about implementing this feature, but I don't think that anyone is currently working on it.

- If DB driver supports the feature, it might be possible to use with knex also.

- ## [nodejs pg split read/write request to database - Stack Overflow](https://stackoverflow.com/questions/70980495/nodejs-pg-split-read-write-request-to-database)
- You can create two Pool instances with the different host urls for the master and replica DBs 

- ## [Read Write Replica Delay _201709](https://github.com/knex/knex/issues/2250) 
  - I am trying u use mysql read write replica, i created 2 connection the knex config file, and i am using the read configuration for read queries and write configuration for write queries, 
  - The problem is that the read replica of mysql server are updated by the master server (which handles write queries) in 20ms, so if we do read immediately after write we dont get the new data there.

- this sounds like a really bad idea in multiple ways (trying to create pseudo synchronous replication setup with application side code).
  - I would just suggest to configure replication setup to work in synchronous manner and that way DB know when to lock (it slows down writes a bit, but it sounds like a lot loss of a problem). Also this effectively limits your write speed to < 10 writes per second or those delays will block all your DB reads...
  - You could implement functionality you need for example with rxjs, that always before making query you'll pass them through rxjs, pipe which always waits your delay in case of write operation is being done... knex doesn't help you much with this.

- ## [Seprate Read And Write Support _201502](https://github.com/knex/knex/issues/703)
  - Are there plans to support, writing to master and reading from a read-replica just by a simple config?

- That would be an interesting feature. It's something that would require a number of very substantial changes so it's not something you'll see for quite a while
  - Right now only `node-mysql` supports clustering and we'd need uniform support in order to do this.
  - This request is definitely a helpful data point in thinking about how to structure the pool API. We'd need to at least have a synchronous API for checking whether a connection was available from the read pool and preferentially using that. If not, we'd need to carefully think through how to choose which pool to make an async connection request to (read only or duplex).

- ## [[Help]: need figure out how to do Read/Write Splitting with mysql _201703](https://github.com/knex/knex/issues/1951)
- As i know mysql now support cluster model, could you please help me to figure out how to do Read/Write Splitting with knex?

- How do you do read/write splitting directly with node-mysql driver? Do you have separate IP where to send reads and other for writes or does mysql know how to route queries correctly from any of the nodes?
  - Sounds like you need to create 2 knex instances, one for master and one for slave and select by hand each query where to send them... What happens if master goes down? Is one of the slaves promoted to master automatically? How the client code gets information about that? Is there list of IPs in slave configuration? Sorry, I don't know exactly how mysql clustering works and I don't have time to look into it right now, so I might not be much of help.

- ## [Read Replication · Issue · knex/knex _202209](https://github.com/knex/knex/issues/5322)
- This is indeed a duplicate of the long-standing issue #2253, which has been tracking read/write replica support since 2017.
  - The good news is that while Knex doesn't provide built-in read replica support, there are several proven workarounds that the community has developed over the years, and there's now active discussion about adding official support for this feature.
- 💡 The most popular approach, which has been battle-tested in production for years, was shared by @Frolanta in #2253. 
  - The technique involves creating two Knex instances (one for the master/writer endpoint, one for read replicas) and a wrapper instance that overrides the client.runner method to automatically route queries based on their type (SELECT vs INSERT/UPDATE/DELETE). 
  - This solution also provides a way to force specific queries to use the master connection via .queryContext({ useMaster: true }), which is crucial for handling replication lag when you need to read immediately after writing.
- 💡 Another useful tool is @thetutlage's `knex-dynamic-connection` module, which allows you to provide an array of connection configurations and compute the connection at runtime, enabling round-robin load balancing between multiple read replicas.

- 📡 There's now a concrete proposal in #6246 for adding Connection Routing Hooks API to Knex, which would provide official support for read/write splitting without requiring core changes to Knex. 
  - This proposal includes a resolver function approach that would allow developers to implement custom connection selection logic, support for dynamic addition/removal of connections (important for auto-scaling), and access to pool information for intelligent load balancing.
  - For now, I'd recommend implementing one of the proven community workarounds mentioned above, particularly @Frolanta's wrapper approach if you want automatic query routing, or the separate read/write Knex instances approach if you prefer explicit control over which operations go where.

- ## 🤔 [Customize connection pool and/or queries for cluster instances _201710](https://github.com/knex/knex/issues/2253)

- Currently not supported. I wrote a quick (and dirty) work around that just juggles Knex instances until Knex can be updated with specific functionality.

- The "simple" way is to have a knex handle for writes and a knex handle for reads.

- I have approached it by separating knex instance of read and write. However, within read and write, one may want to use multiple connection hosts vs relying on a single server and creating a new knex instance for each host is lot of manual work + waste of resources.

- I've set up a Connection Pool and added the WRITER and READER endpoints from the Aurora cluster. Then each time I execute a query I regex it to see if it only contains selects.

- having read/write routing inside the pool would be a solution
  - I would like to propose having this above the pool, as a router/layer that possibly encapsulates multiple tagged pools and serves acquire() requests using tags

- Having load balancing in db driver has many advantages by removing all the intermediate services (pgpool/virtual interfaces). 

- I am trying u use mysql read write replica, i created 2 connection the knex config file, and i am using the read configuration for read queries and write configuration for write queries, 
The problem is that the read replica of mysql server are updated by the master server (which handles write queries) in 20ms, so if we do read immediately after write we dont get the new data there.
- this sounds like a really bad idea in multiple ways (trying to create pseudo synchronous replication setup with application side code).
  - I would just suggest to configure replication setup to work in synchronous manner and that way DB know when to lock (it slows down writes a bit, but it sounds like a lot loss of a problem). Also this effectively limits your write speed to < 10 writes per second or those delays will block all your DB reads...

- 202508: After thoroughly analyzing this issue that's been open since 2017, examining multiple PR attempts, and researching how competing libraries handle this problem, I want to provide a comprehensive response on the state of read/write splitting in Knex.
  - Each attempt revealed the same core challenges: the complexity is database-specific, cloud-provider-specific, and use-case-specific. 
  - The 2018 PR closure perfectly encapsulates our position - whether this belonged in Knex core vs. an independent npm module, and after discussion, the consensus was that external solutions were preferable.

- Current State & Why This Hasn't Been Implemented
- The fundamental challenge isn't technical capability -- it's architectural philosophy. Knex was designed as a query builder first, with connection management as a supporting feature. Adding read/write splitting requires fundamental changes to how Knex thinks about connections, and there are several critical design decisions that have prevented consensus:
  - Abstraction Level Mismatch: Knex operates at the query building level, while read/write splitting is a connection routing concern. The current architecture tightly couples query building with connection acquisition through the Runner class, making clean separation difficult.
  - Database-Specific Complexity: Each database has different replication mechanisms (Aurora's reader endpoints, PostgreSQL streaming replication, MySQL's binlog replication). Building a one-size-fits-all solution risks being too generic to be useful or too specific to cover all cases.
  - Transaction Semantics: Transactions must stay on the master, but determining transaction boundaries across nested transactions, savepoints, and query contexts is non-trivial.
  - Replication Lag: The 100ms+ replication lag issue that @Frolanta discovered is real and varies by provider. Any built-in solution needs to handle read-after-write consistency, which is application-specific.

- What Other Libraries Do
- Having examined Sequelize, TypeORM, Rails ActiveRecord, and node-mysql, there are two main patterns:
- Pattern 1: Configuration-Based (Sequelize, TypeORM)
  - Separate configuration for read/write hosts
  - Automatic routing based on query type
  - Explicit override mechanisms for edge cases
- Pattern 2: Connection Pool Management (node-mysql, Rails)
  - Multiple named pools with pattern matching
  - Middleware/interceptor-based routing
  - Session-based consistency tracking
- Why Community Solutions Work Better
  - The beauty of @Frolanta's runner override pattern and @thetutlage's knex-dynamic-connection is they solve specific problems without requiring Knex to make opinionated choices. They demonstrate that Knex's current architecture, while not ideal, is flexible enough for userland solutions.
- The Real Problem: AWS Aurora
  - The elephant in the room is AWS Aurora. Its reader endpoint rotation every second, combined with connection pooling behavior, breaks assumptions about load balancing. 
  - This isn't a Knex problem -- it's an impedance mismatch between Aurora's design and traditional connection pooling. 
  - The solution (querying AWS SDK for replica endpoints) is too AWS-specific to belong in Knex core.

- My Recommendation
- Rather than adding half-baked read/write splitting to Knex core, we should:
  - Document the Pattern: Create official documentation showing @Frolanta's runner override pattern as the recommended approach. It's battle-tested and elegant.
  - Enhance Extension Points: Add official hooks for connection routing without breaking changes
  - Embrace the Ecosystem: The fact that multiple solutions exist (knex-multiconnect, knex-dynamic-connection) shows the community can solve this better than a one-size-fits-all core implementation.
  - Consider a Plugin System: Long-term, Knex needs a plugin architecture. Read/write splitting is the perfect candidate for an official plugin maintained separately from core.

- Not implementing this feature has been the right call. 
  - Look at TypeORM -- their built-in replication has edge cases around raw queries always using master. 
  - Sequelize's implementation doesn't handle dynamic replica discovery. 
  - Rails requires careful configuration to avoid stale reads.
- By keeping this out of core, Knex avoids:
  - Breaking changes for existing users
  - Maintenance burden of database-specific replication quirks
  - Support overhead for cloud provider peculiarities
  - Opinion lock-in that might not fit all use cases

- For Users Needing This Today
  - Use @Frolanta's pattern from the issue comments. It works, it's production-tested, and it gives you full control. That's more valuable than any half-measure we could add to core.

- This response acknowledges the real need while explaining why the current approach (community solutions) is actually the right one for Knex's philosophy and architecture. After 10 years of requests and attempts, the evidence strongly supports maintaining separation of concerns - keeping Knex focused on query building while letting specialized libraries handle connection routing.
# discuss-knex-orm-objection
- ## 

- ## 

- ## 🗑️ [Objection.js has been sunset, which ORM/querybuilder did you move to? : r/node _202212 ](https://www.reddit.com/r/node/comments/zblmqf/well_shit_objectionjs_has_been_sunset_which/)

- [The future of Objection.js · Vincit/objection.js _202211](https://github.com/Vincit/objection.js/discussions/2463)
  - The main reason for this is that Objection's typescript typings would need a full rewrite for them to become competitive and up to today's high standards for typescript codebases. 
  - I simply don't have time, or quite frankly the interest, to do that. 
  - Objection was designed before typescript was widely adopted

- If you like knex's query builder and objection.js's relation capabilities, sutando is a better alternative
# discuss-scaling-k8s
- ## 

- ## 

- ## [How to configure Knex for a horizontally scaled system? - Stack Overflow](https://stackoverflow.com/questions/71760396/how-to-configure-knex-for-a-horizontally-scaled-system)
- As per your configuration it looks like you expect 4 node instances max (25*4 = 100). If you want to scale to more processes either reduce the max number of connections per process or increase the max total connection on your db/pooler. It's all just math. There is no magic, everything is a compromise.
  - Yes, we ended up reducing the max number of DB connections per process. And we are planning to use a pooler that can avoid pinning all requests made through Knex. Looks like AWS RDS Proxy made some improvements to make this possible

- ## [How to use a docker container name instead of IP for DB connection with knex - Stack Overflow](https://stackoverflow.com/questions/56299533/how-to-use-a-docker-container-name-instead-of-ip-for-db-connection-with-knex)
- The Docker DNS resolution with container names only works from within containers but you could publish the port to the hosts IP/localhost and connect to that

# discuss-drizzle
- ## 

- ## 

- ## 

- ## With http://drizzle.run, Drizzle Lab CLI, Visualizer, VSCode extension, and Drizzle API (Kit API fork), you can: play with Drizzle in your browser, visualize your schema, transform it to JSON/SQL and back.
- https://x.com/rphlmr/status/1858201283548811482
  - It's been over 9 months of dedicated work, making impossible things possible... don't judge me too harshly on the code
  - As promised, everything I've done around @DrizzleORM is now fully open source.

# discuss
- ## 

- ## 

- ## [Knex how to use database functions within schema building functions](https://github.com/knex/knex/issues/1185)
- After double checking, I found out that uuid extension was not installed the postgresql database

- ## [Knex many-to-many relationships _201502](https://github.com/knex/knex/issues/714)

- ## [Add option to skip unnecessary select after create · prisma/prisma](https://github.com/prisma/prisma/issues/4246)
- This is likely going to be an unsatisfying recommendation but all those who have felt the pain for long enough will agree - just use a query builder. 
  - Knex is great and while there's marginally more boilerplate, it's easy and extensible.

- The reason why I'm not satisfied with Prisma (and other ORMs that lack of SQL optimization such as GORM in Go)

- ## 🚀 [Knex and Bookshelf – ORM for JavaScript | Hacker News _201312](https://news.ycombinator.com/item?id=6871725)
- 🆚️ how does Bookshelf compare to Sequelize in terms of maturity and feature set
  - I'd actually created Bookshelf after seeing a lack of good support for SQL abstractions in javascript, especially comparison to other languages and frameworks.
  - In terms of maturity, Bookshelf & Knex are still definitely young and a work in progress, but fairly mature in the sense that they are both heavily inspired (and in Knex's case, mostly copied) from the excellent Laravel PHP framework's query builder and ORM. 
  - Bookshelf also adapts different conventions I found useful from Backbone.js' Models, Collections, and Events - I'm also aiming to eventually make the libraries usable outside of Node (webSQL or otherwise).
  - I've been looking to take the best from other languages' data interfaces and try to adapt them into a few great packages for javascript, as opposed to completely re-inventing the wheel.
  - Some of the differentiating features include eager-loading and nested eager-loading relations, the ability to constrain those relations, polymorphic relations, a distinct separation between the ORM and the query builder layer, and until recently transactions 
  - 🐛 Some things that Bookshelf doesn't have out of the box are explicit typecasting (hooks exist to handle this if you need, but most times the db takes care of this for you) or validations (IMO out of scope for Bookshelf/Knex, but something I'll have incorporated in my next database package), and static finder methods User.find(1), User.findOrCreate({...}) - easily added but these will also come in the next package in progress.
  - Bookshelf aims to be a simple Data-Mapper, rather than a full out Rails ActiveRecord style ORM... This is something that will be a different project entirely which I'm actively working on building out. Sitting atop of Bookshelf, it will include scopes, validators, callbacks, helper methods, etc

- Any thoughts on migrations with Bookshelf?
  - Bookshelf is running on top of Knex.js, so I suppose you can use its migration features
- I've used node-db-migrate on some toy projects in conjunction with Bookshelf, and it seemed to work fine.
# discuss-sql-builder
- ## 

- ## 

- ## 

- ## [Progressively migrate from knex to kysely · kysely-org/kysely _202308](https://github.com/kysely-org/kysely/issues/630)
- You should be able to use knex and Kysely side by side in the same project without any issues. The only thing I can think of, off the top of my head is that, depending on the setup, you might end up with two connection pools. That might not be an issue, but something to keep in mind.
  - Knex uses it's own connection pool, so there's no way to share that with Kysely currently. We could in theory create a KnexDialect that takes a knex instance and uses it as the driver 

- ## [Kysely: TypeScript SQL Query Builder | Hacker News _202301](https://news.ycombinator.com/item?id=34506657)
- 
- 
- 

- ## 🆚️ [Kysely vs. Knex.js : r/node _202402](https://www.reddit.com/r/node/comments/1anoemm/kysely_vs_knexjs/)
- Kysely has some really great typing support plus it can generate types from an existing database out of the box, so you don't need to write any types manually.
