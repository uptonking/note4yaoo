---
title: lib-db-app-blog-sync-replicate-cdc
tags: [blog, change-data-capture, data-sync, database, replication]
created: 2023-12-10T18:38:07.660Z
modified: 2023-12-10T18:38:43.604Z
---

# lib-db-app-blog-sync-replicate-cdc

# guide

# blogs

## 👨🏻‍🏫 [Database Replication Under the Hood_202312](https://newsletter.systemdesigncodex.com/p/database-replication-under-the-hood)

- there are different replication methods and techniques at play.

### Statement-based Replication

- Statement-based replication is one of the oldest techniques of replication.
  - It was used by databases like MySQL. 
  - But over the years, it has largely fallen out of favor.
- Let’s say you are going for leader-based replication and there are one or more follower nodes under a single leader node. 
  - With Statement-based Replication, two things happen: The leader will log every write request or statement that it executes. It will also send that statement log to its followers.
- This means that every INSERT, UPDATE & DELETE statement is forwarded to followers.
  - Followers parse and execute the SQL statement as if they had received it directly from a client.
- 🌹 This mechanism had a few advantages:
  - Highly efficient in terms of network bandwidth because only SQL statements are sent to the followers rather than the complete data
  - Higher portability across different database versions.
  - Simpler and easier to use.
- 🐛 it fell out of favor because of some big limitations:
  - Any statement that calls a non-deterministic function (such as `NOW()` & `UUID()`) to get the current date and time will generate a different value on each replica.
  - If statements use an auto-incrementing column, they must be executed in the same order on each replica. In other words, you can’t have multiple transactions executing concurrently.
  - Statements with side effects such as triggers or stored procedures can create unforeseen effects on the replica.

### Shipping the Write-Ahead Log (WAL)

- The write-ahead log is an append-only sequence of bytes that contains all writes to the database.
  - Databases create a write-ahead log for their own purposes to safeguard against potential crashes. 
  - this log can also be shipped to the followers.
- By shipping the write-ahead log or WAL to another node, it’s possible to build an exact replica of the data.
  - The leader node ships its own log to the followers and the followers process this log and build a copy of the exact same data structures as found on the leader.
- 🐛 This method can be used in PostgreSQL and other databases but it has one glaring disadvantage.
  - The write-ahead log describes the data at a very low level. Basically, it contains details of which bytes were changed in which particular disk blocks. 
    - In other words, it depends on the exact storage engine to make sense.
    - if a database changes its storage format from one version to another, you can’t use the same log as it might lead to unpredictable results.
  - The operational impact of this is that you cannot implement a zero-downtime upgrade.

### Row-Based Replication

- row-based replication gets around the issue with write-ahead logs by using different log formats for replication and storage engine.
- It does so by creating a logical log - a sequence of records showing all the writes to the database tables in row format.
- Here’s how it works:
  - For an insert operation, the log contains the new values of all the columns.
  - For a delete operation, the log contains information to uniquely identify the deleted row such as the primary key.
  - For an updated row, the log contains information to uniquely identify the updated row and the new values of all the modified columns.
- In case multiple rows are impacted by an update operation, several log records are generated.
- Since the row-based replication is not tightly coupled with the storage engine, it can support backward compatibility across database versions.
- In other words, leaders and followers can potentially run different versions of the database.

### How Discord Dealt with Trillions of Messages?

- In 2017, Discord was storing billions of messages from users all across the globe. 
  - At that point, they migrated from MongoDB to Cassandra in search of a scalable, fault-tolerant and low-maintenance database.
  - Over the next few years, Discord’s database cluster grew from 12 Cassandra nodes to 177 Cassandra nodes storing trillions of messages.
  - The Cassandra cluster ran into serious performance issues requiring lots of effort to run and maintain resulting in frequent on-call issues, unpredictable latency and expensive maintenance operations.

- The Reasons for Discord’s Database Problems
- Reason#1 - Partitioning Strategy
  - In Discord, messages belong to a channel and are stored in a table known as messages. 
  - This table was partitioned by the `channel_id` along with a bucket. The bucket is basically a static time window.
  - Such a strategy meant that all messages for a given channel and bucket (time period) would be stored on the same partition.
  - The implication of this was that a Discord server with hundreds of thousands of people could potentially generate enough messages in a short period of time to overwhelm a particular partition. This was a big performance pitfall.

- Reason#2 - Cassandra Reads More Expensive Than Writes
  - By design, reads in Cassandra are more expensive than writes.
  - This is because writes are appended to a commit log and written to an in-memory structure called a memtable. Periodically, the memtable is flushed to the disk in the form of SSTable.
  - When you are writing new records, this doesn’t cause issues.
  - However, read operations need to potentially query the memtable and multiple SSTables. This is an expensive operation and lots of concurrent reads in high-volume Discord channels can eventually hotspot a partition.
  - These hot partitions created cascading latency issues across the entire database cluster.
  - A surge in traffic for one channel and bucket pair led to increased latency in a node as it tried harder to keep up and serve the incoming traffic. Other queries to this node also got affected resulting in broader end-user impact.

- Reason#3 - Trouble with Cluster Maintenance
  - Over a period of time, Cassandra compacts SSTables on disk to improve the performance of read operations. However, during the compaction period, the ongoing read operations suffered even more.
  - To mitigate this situation, the team was forced to take the node undergoing compaction out of rotation so that it didn’t get traffic and bring it back into the cluster to resume activities.

- The Solution
- S1-Migration to ScyllaDB
- Why ScyllaDB?
  - It was Cassandra compatible
  - Written in C++ rather than Java
  - It provided better workload isolation via its shard-per-core architecture
  - No garbage collection
  - Special support by the ScyllaDB team
- Based on the documentation released, the main reason for choosing ScyllaDB appeared to be the lack of a garbage collector.
  - The Discord team had faced many issues with Cassandra’s garbage collector.
  - GC pauses affected the latency in a big way. 
  - In fact, some consecutive GC pauses forced an operator to manually reboot and babysit the node back to health.
- S2-Building Dedicated Data Services
  - During their experiences with Cassandra, the Discord team struggled a lot with hot partitions. High traffic to a given partition resulted in uncontrolled concurrency resulting in cascading latency. Therefore, it became necessary to control the amount of concurrent traffic to hot partitions in order to protect the database from being overwhelmed.
  - To handle this, the team wrote special data services using Rust.
  - These were basically intermediary services that sat between the API monolith and the database cluster. Rust was chosen because of team familiarity and the promise of C/C++ speeds without sacrificing safety.
  - Each of the data services contained roughly one gRPC endpoint per database query and no business logic.
  - But the real magic of these data services was request coalescing.
  - What is request coalescing? If multiple users are requesting the same row at the same time, request coalescing helps query the database only once.

## [Implementing CDC: 3 Approaches to Database Replication_202302](https://www.upsolver.com/blog/mysql-cdc-and-database-replication-for-the-data-lake-age)

- In this article we’ve discussed high-level concepts related to CDC and drilled into Upsolver’s unique capabilities related to CDC-based database replication.  

- Comparing database replication approaches
  - Delta by comparison
  - Timestamp-based CDC
  - Transaction Log-based CDC

## [A Taxonomy Of Data Change Events _202403](https://www.decodable.co/blog/taxonomy-of-data-change-events)

# more
