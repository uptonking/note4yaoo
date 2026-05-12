---
title: lib-db-postgresql-community-mvcc-transaction
tags: [community, concurrency, mvcc, postgresql, transaction]
created: 2024-02-18T13:51:11.282Z
modified: 2024-02-18T13:52:07.926Z
---

# lib-db-postgresql-community-mvcc-transaction

# guide

# discuss-stars
- ## 

- ## 

- ## It is once again time for my monthly gripe(牢骚；怨言) that this is not a transaction. You might as well say that Postgres' default mode is transactionless.
- https://twitter.com/aboodman/status/1758593374435860688
- When you say "this" is not a transaction, do you mean Postgres's "Read Committed isolation level in PostgreSQL"?
  - Yes

- Isn't it still a transaction in the "either all writes succeed or none of them do" sense?
  - Why do people want “all succeed or none do”? So that they don’t read a mix of two different writes. But this definition of “transaction” allows exactly that.

- I’m trying to figure out if this is a technical limitation. I guess it’s just a big performance hit because you might need to read-lock a whole table  for the second query while you wait for the first to finish… Related: I notice a lot of people confuse read-write transaction consistency with atomicity.
  - No locks needed, Postgres uses MVCC. But yeah you need to keep old tuples around rather than being able to update them in place so REPEATABLE READ is definitely more expensive.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## Postgres uses a process-per-connection model not thread-per-connection.
- https://x.com/codersGyan/status/2054041396873454073
  - That means every connection is expensive : memory, file descriptors, process overhead.
  - Now the connection math matters.
  - A default pool of 100 connections is roughly ~1GB of RAM before queries even run. 4 app servers x 100 connections = 400 connections. Postgres defaults to max_connections = 100. Now the database starts refusing connections.
  - The fix usually isn’t “add more connections.” It’s a connection pooler. 
  - PgBouncer in transaction mode is the standard answer.
  - Apps connect to PgBouncer (cheap). PgBouncer multiplexes them onto a much smaller pool of real Postgres connections (expensive).
  - 1, 000 app connections can fan into 20 actual DB connections. Before reaching for it, read the caveats. 
  - Prepared statements, session-level state, advisory locks.. all behave differently. 
  - If your scaling plan is just increasing max_connections, you probably don’t need a bigger database. You need PgBouncer.

- ## 🤼 PostgreSQL的快照隔离在有长事务的情况下性能不良，因为并行事务不能写冲突。也就是说如果很多个事务试图修改计数器，那么除了一个事务其他都必须失败。
- https://x.com/JXQNHZr1yUAj5Be/status/2027003437200674862
  - 而MySQL的update是当前写（原子寄存器语义），意味着它总是看到最新的状态，对同一个行的写不会导致事务被取消。因此它更有利于长事务和写入。
  - 因此从互联网的主要业务看，PostgreSQL的设计是失败的。
- 差点被糊弄过去。首先 PostgreSQL 和 MySQL 在这个情况下的写锁行为差不多，PostgreSQL 只会可重复读和可串行化级别存在违反的时候会滚事物，对应 MySQL 的行为是数据错误或者死锁。 此外你说的计数器场景，大家都使用读已提交隔离级别，两边的行为几乎一致。

- ## 🔒📝 Postgres locks are interesting. e.g. CREATE INDEX allows reads but blocks Writes, while VACUUM FULL blocks all queries.
- https://twitter.com/hnasr/status/1781129355286229229
  - In this article I explore all locks in Postgres and show my http://pglocks.org tool which identifies conflicting commands.
  - [Postgres Locks — A Deep Dive _202303](https://medium.com/@hnasr/postgres-locks-a-deep-dive-9fc158a5641c)

- What about existing running queries ser?
  - existing running queries will also obtain locks and hold them until they commit or rollback

- Does Vaccum wait for the lock release that is acquired by other queries? Postgres execute query in order?
  - It depends on the query and whether it’s conflicting. regular vacuum can run concurrently with all queries (select/updates) except for ddls 
  - but full vacuum cannot run if there is an existing running select query, the select needs to finish, and if a vacuum full starts it blocks all reads and writes.

- ## 🆚️ PostgreSQL MVCC has one well-known➖: vacuum and only two➕often mentioned: simpler indexes, fast rollback
- https://twitter.com/FranckPachot/status/1770214536261386477
  - IMO the HUGE ➕of PostgreSQL MVCC compared to Oracle is the ability to do unlogged DML on a table. 
  - I've seen many Oracle DBs generating tons of redo for staging tables

- What do you mean by “unlogged DML on a table”? Are you talking about UNLOGGED TABLES?
  - Yes. I precised DML because all DML are unlogged. Oracle has nologging tables but that affects only direct-path append which is more like DDL (locking the table in exclusive mode)

- ## Postgres doesn't use threads, pgbouncer doesn't use threads. 
- https://twitter.com/samokhvalov/status/1762113679372521706
  - If critical processes like walsender, logical replication worker or pgbouncer reach 100% of a single vCPU, we have a big trouble.
  - Now: how come nobody (uppercase, NOBODY) among monitoring developers recognized that and added proper metrics to observe usage & saturation risks?

- There is a really big effort ongoing to make Postgres multithreaded
  - Define "ongoing". Unfortunately, the latest msg in that thread is from Aug.
- We have Google AlloyDB and we see 100 pct CPU utilisation. Not able to figure out how this happens. Max_connetions set 1000 (alloydb default) and pgBouncer max_client connections=500 default_connection_pool=100.
  - This is different, I think. I was talking about 100% of a single vCPU, and excluding regular Postgres backends that process queries (they can hit 100% of one vCPU all the time -- just let them do SeqScans, for instance)

- ## Postgres MVCC Backstage Run a few basic SELECTS, INSERTS, and UPDATES to see how the MVCC engine functions internally
- https://twitter.com/denismagda/status/1760780953285284251
  - https://github.com/dmagda/DevMastersDb/blob/main/postgres/postgres_mvcc_backstage.md

- ## 🤼🏻 [PostgreSQL reconsiders its process-based model | Hacker News_202306](https://news.ycombinator.com/item?id=36393030)

- Sorry if I offend anybody, but this sounds like such a bad idea.
  - I have been running various versions of postgres in production for 15 years with thousands of processes on super beefy(粗壮的, 结实的) machines
  - Postgres has 99% of the time proven to be resilient. The idea that a bad client can bring the whole cluster down because it hit a bug sounds scary.
  - crashes are part of that workflow, and changing this from process to threading would mean all the other clients also crashing and cutting connections. 
  - This as a potential problem because I want to avoid context switching overhead or cache misses, no thanks.

- 👉🏻 Oracle has similar problems. On UNIX systems, Oracle uses a multi-process model
  - Windows forks processes about 100x slower than Linux, so Oracle runs threaded on that platform in one great big PID.
  - Sybase was the first major database that fully adopted threads from an architectural perspective, and Microsoft SQL Server has certainly retained and improved on that model.
- If you run postgres under WSLv1 (now available on Server Edition as well), the WSL subsystem handles processes and virtual memory in a way that has been specifically designed to optimize process initialization as compared to the traditional Win32 approach.
- Yeah multiprocess isn't Microsoft's style given how expensive creating processes is on Windows.
- Didn't Oracle switch to threaded model in 12c
  - It's optional, and the default is still a process model on Linux.

- Reminds me of PHP 6... For those who don't follow PHP closely - that version was an attempted refactor of the string implementation which essentially shut down nearly all work on PHP for a decade, stagnating the language until it became pretty terrible compared to other options. 
  - They finally gave up and started work on PHP 7 which uses the (perfectly good) PHP 5 strings. 
  - Ten years of wasted time by the best internal PHP developers crippled(使伤残; 严重损坏) the project - I'm amazed it survived at all.

- I've seen (and reported) bugs that caused panics/segfaults in specific psql processes. Not just connections, also processes related to wal writing or replication. The way it's built right now, a child process can be just forced to quit and it does not affect other processes. Hopefully switching into thread won't force whole PostgreSQL to panic and shut down.
  - Because of shared memory most panics and seg faults in a worker process take down the entire server already (this wasn’t always the case, but not doing so was a bug).

- The thing is... multi-process with a bespoke shared memory system isn't better than multithreading; it's much worse.
