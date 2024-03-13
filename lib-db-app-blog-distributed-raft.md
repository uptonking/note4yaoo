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
