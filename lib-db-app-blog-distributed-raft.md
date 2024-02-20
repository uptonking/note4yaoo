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
# blogs-vendor

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
