---
title: lib-db-app-blog-vendors
tags: [blog, database, vendors]
created: 2023-09-16T17:53:11.838Z
modified: 2023-10-26T18:14:17.038Z
---

# lib-db-app-blog-vendors

# guide
- [TiKV 源码解析 | PingCAP](https://cn.pingcap.com/blog/tag/tikv-source-code-analysis/)
- [TiDB 源码阅读 | PingCAP](https://cn.pingcap.com/blog/tag/tidb-source-code-reading/)
# blogs-vendors

## [Designing a Distributed SQL Engine: Challenges & Decisions | OceanBase_202304](https://en.oceanbase.com/blog/2596985600)

## [TiKV - Building a Large-scale Distributed Storage System Based on Raft_202005](https://tikv.org/blog/building-distributed-storage-system-on-raft/)

- A great overview of different sharding strategies, their trade offs and the design choices for TiKV.

## [当 TiDB 遇上 Jepsen | PingCAP](https://cn.pingcap.com/blog/tidb-jepsen/)

- Jepsen 是由 Kyle Kingsbury 采用函数式编程语言 Clojure 编写的验证分布式系统一致性的测试框架，作者使用它对许多著名的分布式系统（etcd, cockroachdb...）进行了“攻击”（一致性验证）

## 📝 [Turning the database inside-out with Apache Samza | Confluent_201503](https://www.confluent.io/blog/turning-the-database-inside-out-with-apache-samza/)

## 👥🔥 [Turning the database inside-out with Apache Samza | Hacker News_201503](https://news.ycombinator.com/item?id=9145197)

- Immutability is hardly a cure-all, see the discussion here for why RethinkDB moved away from it
  - The reality is shared, mutable state is the most efficient way of working with memory-sized data. People can rant and rave all they want about the benefits of immutability vs mutability, but at the end of the day, if performance is important to you, you'd be best to ignore them.
  - Actually, to be more honest, reality is more complicated still. MVCC that many databases use to get ACID semantics over a shared mutable dataset is really a combination of mutable and immutable.
- RethinkDB's storage engine heavily relies on the notion of immutability/append-only. We never modify blocks of data in place on disk -- all changes are recorded in new blocks. We have a concurrent, incremental compaction algorithm that goes through the old blocks, frees the ones that are outdated, and moves things around when some blocks have mostly garbage.
  - The system is very fast and rock solid. But...
  - Getting a storage engine like that to production state is an enormous amount of work and takes a very long time. If we were starting from scratch, I don't think we'd use this design again. It's great now, but I'm not sure if all the work we put into it was ultimately worth the effort.

- I really think there are a couple of levels of immutability that it is easy to conflate(混合).
1. In memory data structures...this is the contention of the functional programming people.
2. Persistent data stores. This is the lsm style of data structure that substitutes linear writes and compaction for buffered in-place mutation.
3. Distributed system internals--this is a log-centric, "state machine replication" style of data flow between nodes. This is a classic approach in distributed databases, and present in systems like PNUTs.
4. Company-wide data integration and processing around streams of immutable records between systems. This is what I have argued for and I think Martin is mostly talking about.
- There are a lot of analogies between these but they aren't the same. Success of one of these things doesn't really imply success for any of the others. Functional programming could lose and log-structured data stores could win or vice versa. 

- Samza sounds like an event-sourcing style immutable event log. You could think of it like the transaction or replication log of a traditional database. Having that be immutable is very sensible! But you can't always query that in "real-time". On the other hand, the data structures you query in real-time, making that immutable is problematic, because then you'll need a LevelDB style compaction step. That doesn't mean to say that it can't be done well, but that it's hard to do well.

- I'm not sold on Samza, but I can tell you that creating isolated services that create their datastore from a stream of events is a really useful pattern in some use cases (ad-tech).
- 
- 

## 📝 [Reddit’s database has two tables_201209](https://kevin.burke.dev/kevin/reddits-database-has-two-tables/)

- Lesson: Don’t worry about the schema.
  - it looks like they use two tables for each “thing”, so a thing/data pair for accounts, a thing/data pair for links, etc.

## 👥🔥 [Reddit’s database has two tables (2012) | Hacker News_202208](https://news.ycombinator.com/item?id=32407873)

# discuss-key-value

## [Build a BLAZINGLY FAST key-value store with Rust for Riak_202302](https://www.tunglevo.com/note/build-a-blazingly-fast-key-value-store-with-rust/)

- Nice overview on implementing #Bitcask (originally, the storage engine of Riak)
- In this blog series, I’ll be sharing my experience implementing Bitcask in Rust and discussing some of the techniques I used to make it goes blazingly fast. 
# blogs-aws-s3

## [S3 as the universal infrastructure backend_202310](https://medium.com/innovationendeavors/s3-as-the-universal-infrastructure-backend-a104a8cc6991)

- 
- 

## 🛢️ [Building and operating a pretty big storage system called S3 _202307](https://www.allthingsdistributed.com/2023/07/building-and-operating-a-pretty-big-storage-system.html)

# more
- [planetscale - Database branching: three-way merge for schema changes_202304](https://planetscale.com/blog/database-branching-three-way-merge-schema-changes)

- [The Taming(驯服) of the B-Trees - ScyllaDB_202111](https://www.scylladb.com/2021/11/23/the-taming-of-the-b-trees/)
