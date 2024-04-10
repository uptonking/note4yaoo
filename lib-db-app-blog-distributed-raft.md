---
title: lib-db-app-blog-distributed-raft
tags: [blog, database, distributed, raft]
created: 2024-02-05T09:43:51.280Z
modified: 2024-02-05T09:44:21.665Z
---

# lib-db-app-blog-distributed-raft

# guide

# blogs
- [Object Storage and In-Process Databases are Changing Distributed Systems _202402](https://blog.colinbreck.com/object-storage-and-in-process-databases-are-changing-distributed-systems/)
# blogs-jepsen

## [Deterministic Simulation Testing for Our Entire SaaS - WarpStream - Stream More, Manage Less](https://www.warpstream.com/blog/deterministic-simulation-testing-for-our-entire-saas)

- Why use Antithesis instead of a traditional Jepsen test? 
  - The Antithesis technology is more robust, and much more likely to catch bugs than the Jepsen harness
  - Antithesis integrates natively into how our engineers are used to working. The entire test setup is expressed using standard docker-compose files and Docker images, and Antithesis tests are kicked off using Github Actions that push WarpStream images to Antithesis’ docker registry.
  - Antithesis testing is designed to be a continuous process with accompanying professional services that help you grow and adapt the tests as the scope of your product increases
  - it would not have been practical to continuously test our entire SaaS platform with Jepsen in the same way that we do with Antithesis. 

- https://twitter.com/jorandirkgreef/status/1767767536572006436
# blogs-vendor

## 🐛 [Distributed SQL Databases And The Costs of Being Distributed | by Adam Prout | Medium _202401](https://medium.com/@adamprout/distributed-sql-databases-and-the-costs-of-being-distributed-ab7b38b0fa50)

- Distributed databases can do some amazing things — they allow a workload to harness the power of 1000s of cores and terabytes of memory or allow apps to seamlessly span regions across the globe.
- These extra costs, at a high level, are somewhat obvious given that data is spread (sharded) across many hosts in a distributed database. 
- Sharding the data means many query shapes need to connect to all hosts within the cluster to run over the entire data set resulting in extra network hops
  - The extra hops increase latency and can limit the overall scalability of the database
- This blog post is about any database that is made up of multiple hosts and shards/partitions the data between those hosts.
- A cheap query in a single host database can be expensive in a distributed database. These different performance characteristics often require schema or query tuning when moving from a single host database to a distributed database.
- I think the best way to demonstrate how the extra network hops impact applications is with a non-exhaustive set of example query shapes or features that are slower (or have higher overhead) in distributed databases. I’m not assuming any particular distributed database implementation in these examples. Some distributed databases have features you can use to work around some of these problems, but in general these examples are things to keep an eye on.
- Low Latency Writes are a challenge in a distributed database because rows need to be routed to the particular shard that should store the row. Most distributed databases have one extra network hop to redirect the write from the host the application connected to, to the host that should store the row
- Queries using secondary keys. Lookups on keys that the data is not sharded on require querying every host in a distributed database 
- Limits or Top N queries. On a single host database, a top N query is a simple table or index scan with a counter used to top the scan when N rows have been matched.
- Distinct queries. On a single host database, distinct queries will either scan an index on the distinct columns, if one exists, to find unique values (i.e., “streaming group by”) or build a local hash table that stores unique entries during a table scan.
- Distributed joins. Single host databases don’t need to send any data over the network to run a join 
  - Distributed databases often have to shuffle or broadcast data across the network between hosts to run a join
  - A shuffle join is one way to get these rows together on the same host but it involves O(num_hosts²) connections in general so it doesn’t scale well with cluster size. 
  - There are other ways of running joins in a distributed database, but they will all in involve sending data over the network in some way.
- Transaction commit — To support ACID transactions, distributed databases require an extra co-ordination protocol to make sure commits are atomic across all hosts in the database, typically two phase commit. This extra network traffic on commit slows down small low latency write transactions. Single host databases don’t have this extra overhead.
- Strong Transactions (Snapshot or Serializable Isolation level). Isolating transactions from each other across hosts in a distributed database is more complex. It requires a clock algorithm to globally order transactions across the hosts 
- Foreign keys — In a single host database foreign keys are usually implemented by doing extra index lookups on writes to ensure the foreign key is satisfied.
- Unique keys have similar challenges to secondary keys. 
  - A single host SQL database will have a global unique index to figure out if a new value is a duplicate with a single index lookup. 
  - A distributed database will need to query all shards for every row inserted to check for duplicates unless the unique key is part of the key used to shard the data (in which case the system knows which shard will hold the duplicate if it exists).
- If distributed databases have all this extra overhead why do we use them?
  - if a query is doing enough other work (expensive filters, aggregations, calculations, etc.) per network hop introduced by the distributed database, then using a distributed database is typically a win for lowering the latency of these queries. 
  - This is why distributed databases are the norm for data warehouses or analytical databases that run complex queries across large data sets requiring lots of compute (BigQuery, Redshift, Snowflake, Clickhouse, SingleStoreDB, etc.). 
- for OLTP or operational workloads, distributed SQL databases are not as common. 
  - In my opinion, this is because they don’t provide enough value to overcome their extra costs for many applications. 
  - Single host SQL databases like PostgreSQL, MySQL, Amazon Aurora (or RDS), Oracle and Azure SQL DB dominate the OLTP database market as of today.

- There are a few common features of distributed SQL databases designed to work around some of the above performance problems. 
  - For example, many databases support defining a table as a “reference table”. 
  - These tables are copied to every host in the distributed database, so writing to them is much slower, but they allow for more local read operations on the individual hosts.
- Distributed database also typically allow collocating tables by sharding them on the same key. If the common sharding key is in the ON clause of a join, again a shuffle join can be avoided — the join can be done locally at each host. 

- So, adopting a distributed SQL database comes with some trade-offs
# blogs-protocols

## [ScyllaDB’s move from Paxos to Raft _2024](https://www.scylladb.com/glossary/paxos-consensus-algorithm/)

- The core Raft protocol is implemented in ScyllaDB and ScyllaDB 5.4 implements strongly consistent schema management and topology updates. 
  - ScyllaDB Summit 2024 also features multiple discussions on what ScyllaDB is doing with Raft and what this means for ScyllaDB users.

- [ScyllaDB Open Source 5.4 Release _202312](https://www.scylladb.com/2023/12/11/scylladb-open-source-5-4/)

- https://twitter.com/eatonphil/status/1754228943501054080
- 💡 extra handshake required for paxos that is removed in raft
- You mean longer term leaders in raft right? This is what I assumed too but I'd still like to read their details
  - in paxos originally had 4 back/forth
  - lwt paxos 3
  - raft 2
# more
- [An intuition(直觉感知的事, 直觉知识) for distributed consensus in OLTP systems _202402](https://notes.eatonphil.com/2024-02-08-an-intuition-for-distributed-consensus-in-oltp-systems.html)
