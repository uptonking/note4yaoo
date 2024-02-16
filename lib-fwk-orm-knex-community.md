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

- ## 

- ## 
# discuss-cluster
- ## 

- ## 

- ## 

- ## [nodejs pg split read/write request to database - Stack Overflow](https://stackoverflow.com/questions/70980495/nodejs-pg-split-read-write-request-to-database)
- You can create two Pool instances with the different host urls for the master and replica DBs 

- ## [Seprate Read And Write Support _201502](https://github.com/knex/knex/issues/703)
  - Are there plans to support, writing to master and reading from a read-replica just by a simple config?

- That would be an interesting feature. It's something that would require a number of very substantial changes so it's not something you'll see for quite a while
  - Right now only `node-mysql` supports clustering and we'd need uniform support in order to do this.
  - This request is definitely a helpful data point in thinking about how to structure the pool API. We'd need to at least have a synchronous API for checking whether a connection was available from the read pool and preferentially using that. If not, we'd need to carefully think through how to choose which pool to make an async connection request to (read only or duplex).

- ## 🤔 [Customize connection pool and/or queries for cluster instances _201710](https://github.com/knex/knex/issues/2253)

- Currently not supported. I wrote a quick (and dirty) work around that just juggles Knex instances until Knex can be updated with specific functionality.

- The "simple" way is to have a knex handle for writes and a knex handle for reads.

- I have approached it by separating knex instance of read and write. However, within read and write, one may want to use multiple connection hosts vs relying on a single server and creating a new knex instance for each host is lot of manual work + waste of resources.

- I've set up a Connection Pool and added the WRITER and READER endpoints from the Aurora cluster. Then each time I execute a query I regex it to see if it only contains selects.

- having read/write routing inside the pool would be a solution
  - I would like to propose having this above the pool, as a router/layer that possibly encapsulates multiple tagged pools and serves acquire() requests using tags

- Having load balancing in db driver has many advantages by removing all the intermediate services (pgpool/virtual interfaces). 

- 
- 
- 

- I am trying u use mysql read write replica, i created 2 connection the knex config file, and i am using the read configuration for read queries and write configuration for write queries, 
The problem is that the read replica of mysql server are updated by the master server (which handles write queries) in 20ms, so if we do read immediately after write we dont get the new data there.
- this sounds like a really bad idea in multiple ways (trying to create pseudo synchronous replication setup with application side code).
  - I would just suggest to configure replication setup to work in synchronous manner and that way DB know when to lock (it slows down writes a bit, but it sounds like a lot loss of a problem). Also this effectively limits your write speed to < 10 writes per second or those delays will block all your DB reads...

- ## [[Help]: need figure out how to do Read/Write Splitting with mysql _201703](https://github.com/knex/knex/issues/1951)
- As i know mysql now support cluster model, could you please help me to figure out how to do Read/Write Splitting with knex?

- How do you do read/write splitting directly with node-mysql driver? Do you have separate IP where to send reads and other for writes or does mysql know how to route queries correctly from any of the nodes?
  - Sounds like you need to create 2 knex instances, one for master and one for slave and select by hand each query where to send them... What happens if master goes down? Is one of the slaves promoted to master automatically? How the client code gets information about that? Is there list of IPs in slave configuration? Sorry, I don't know exactly how mysql clustering works and I don't have time to look into it right now, so I might not be much of help.
# discuss
- ## 

- ## 

- ## [Add option to skip unnecessary select after create · prisma/prisma](https://github.com/prisma/prisma/issues/4246)
- This is likely going to be an unsatisfying recommendation but all those who have felt the pain for long enough will agree - just use a query builder. 
  - Knex is great and while there's marginally more boilerplate, it's easy and extensible.

- The reason why I'm not satisfied with Prisma (and other ORMs that lack of SQL optimization such as GORM in Go)
