---
title: lib-db-app-community-distributed
tags: [community, database, distributed]
created: 2023-10-26T19:03:45.307Z
modified: 2023-10-26T19:04:00.318Z
---

# lib-db-app-community-distributed

> about database distributed/decentralized

# guide
- openraft's raft implementation is solid!
# discuss-stars
- ## 

- ## 

- ## 

- ## 🆚️ 如果今天还有人津津乐道什么分表分布式海量规模高并发，只能说明一件事：这哥们过去十年已经停止学习了，还活在上一个时代里。
- https://twitter.com/GobeUncleWang/status/1725311478528721026

- ### 👇🏻 支持分布式

- 对于海量数据而言，依然会装不进一台机器里，所以还是会需要分布式。 
  - 至于那些一上来就几个 PB 的存储也只是能存而已，要算的时候瓶颈立刻就出来了。
  - 最好的的系统还是既能在高性能节点上高效率运行，又能支持分布式
- 另外，如果所用的硬件没有 mainframe 那种硬件容错的能力，单个节点出现任何故障都会导致服务中断
  - 容灾这种事集中式数据库也有主从复制，其实也是广义上的分布式，就像我们也不会管一个CPU内的两百个核叫分布式一样，通常也不会管这种叫分布式就是了。

- AP还是需要存算分离做分布式。TP做分布式性能都损失了，这个tradeoff随着单机硬件变强越来越不划算
- OLAP的数据仓库场景，明显现在再强的单机肯定是不行的，顶多顶多的就是服务一个用户同时查询使用，多个机器同时协作来服务一个请求才能给一个即席化的统计分析场景提供很好的体验，甚至更好的服务一个多人同时使用的即席化使用场景

- 你这明显是误导。只要需求超越单机上限，你就得分布式。你见过HPC是单机吗？连CPU都得是分布式网状结构，就因为处理需求远超“单处理结构”的能力上限，必须集群化处理。

- 这文章没考虑到实际工程场景。单机必然是不安全的，外部因素比如网络抖动，断网断电，bug导致进程异常终结，内部因素比如特性更新/版本更新导致的重启。单机必然存在一定时间的停机，这在实际的工程场景中是无法忍受的。
  - 你说的叫冗余和文章说的分布式是两回事。文章的分布式是指同一个任务通过特定的协议分散到不同的主机上协同处理，单机需要怎么做冗余，分布式也是一样要做的。

- 存储能存 不代表要计算 查找的时候 能快速算得出来 查得出来。 

- ### 👇🏻 支持单机

- 你单机怎么保证availability
  - 主从

- 分布式是当年硬件算力不够的时代没有办法的办法。当时不是每个公司都能买得起一百多个CPU的服务器，现在硬件价格下来了，性能上去了，个人电脑都能64核，硬件这种强悍的性能，基本上企业90%的需求，买两三台服务器就能满足，再也不需要被迫搞一堆花里胡哨的配置来实现分布式。

- 大规模情况下的数据分片不均（倾斜）造成负载不均衡，这依然是一个固有的未曾解决好的问题，分库分表对应的是关系表这样的数据，但对于递归的图数据怎么做到分布式情况下的处理（rpc开销如何优化调度），也没有成熟方案吧
  - 单机内部就能调整

- 要是有底层库能用H100这样的显卡做加速，硬件的上限会更恐怖。

- 容灾不是分布式

- 
- 
- 

- ## 🕛🔥 [A history of the distributed transactional database | Hacker News_201812](https://news.ycombinator.com/item?id=18600404)
- 
- 
- 

- ## 🔥 [We put a distributed database in the browser and made a game of it | Hacker News_202307](https://news.ycombinator.com/item?id=36680535)
- Is this something similar to couch/pouchdb?
  - TigerBeetle is more domain-specific, i.e. focused on financial transactions and high-performance, high-availability. There are just two entity types in the database: accounts and transfers between accounts. 
- > In comparison to {C, P}ouchDB, I think the question is around offline-first availability.
  - Got it, thanks! Yeah that is indeed not how TigerBeetle works. If you ever cannot connect to the cluster, you keep retry messages (idempotently) until you connect and the message succeeds.

# discuss-decentralized/p2p
- ## 

- ## 

- ## 🔥[OrbitDB: Peer-to-Peer Databases for the Decentralized Web | Hacker News_202103](https://news.ycombinator.com/item?id=26310094)
- 
- 
- 

- ## 🔥 [OrbitDB: Peer-to-peer databases for the decentralized web | Hacker News_202004](https://news.ycombinator.com/item?id=22918467)
- 
- 
- 

- ## 🔥 [OrbitDB – serverless, peer-to-peer database on top of IPFS | Hacker News_201812](https://news.ycombinator.com/item?id=18748542)
- I'm looking for a distributed scalable P2P triple store (or graph database) to store and retrieve RDF using SPARQL.
  - SOLID (Tim Berners-Lee, RDF)
  - GUN (ours, graph)

# discuss
- ## 

- ## 

- ## 

- ## 6 Load Balancing ALGORITHMS you Must Know
- https://twitter.com/AmigosCode/status/1725507946950344949
1. Round Robin 🔄
 - Allocates incoming requests to each server in a circular sequence. It ensures an equal distribution of the workload among servers.
2. Sticky Round Robin 🍭🔄
 - Similar to Round Robin, but with the added feature of maintaining session persistence. Once a client is assigned to a server, subsequent requests from that client continue to be directed to the same server.
3. Least Time⏱️
 - Assigns requests to the server with the least expected processing time. This algorithm considers factors like server response time and current load.
4. Least Connections 🔗🔀
 - Directs traffic to the server with the fewest active connections. This helps distribute the load more evenly across servers, preventing overload on any single server.
5. IP/URL Hash 📌🔗
 - Uses a hash function on the client's IP address or URL to determine which server should handle the request. This ensures that requests from the same client are consistently directed to the same server.
6. Weighted Round Robin ⚖️🔄
 - Similar to Round Robin, but assigns different weights to servers based on their capacity or processing power. Servers with higher weights receive more requests, allowing for proportional load distribution.

- Each of these load balancing algorithms plays a crucial role in optimizing the performance and reliability of server clusters by efficiently distributing incoming requests.

- ## 有啥工具可以比较好的在单机模拟分布式的环境吗？主要是想模拟一下带宽限制和网络延迟
- https://twitter.com/leiysky/status/1725430083106836637
- sudo tc qdisc add dev wlan0 root netem delay 1000ms
- chaos-mesh + minikube （或者直接 tc。可以限制 bandwidth。都是用的 tc qdisc，限流是 tbf 延迟是 netem。
- 我用 Clojure 写的一个工具，jepsen

- ## 💡 Database Sharding Explained
- https://twitter.com/arcnotes/status/1719692415995425014
  - [Database Sharding Explained](https://architecturenotes.co/database-sharding-explained/)

- ## 🔥 [From coding bootcamp graduate to building distributed databases | Hacker News_202102](https://news.ycombinator.com/item?id=26209594)
- 
- 
- 

- ## 🔥 [The Inner Workings of Distributed Databases | Hacker News_202304](https://news.ycombinator.com/item?id=35602983)
- 
- 
- 

- ## 🔥 [Technical Challenges Developing a Distributed SQL Database | Hacker News_201904](https://news.ycombinator.com/item?id=19759101)
- 
- 
- 

- ## 🔥 [How does database sharding work? | Hacker News_202304](https://news.ycombinator.com/item?id=35476518)
- 
- 
- 

- ## 🛢️🔥 [Azure Cosmos DB, a globally distributed database | Hacker News_201705](https://news.ycombinator.com/item?id=14308814)
- 
- 
- 

- ## 💫🔥 [Distributed algorithms in NoSQL databases | Hacker News_201709](https://news.ycombinator.com/item?id=15367003)
- 
- 
- 

- ## 🔥 [Principles of Sharding for Relational Databases | Hacker News_201708](https://news.ycombinator.com/item?id=14971650)
- 
- 
- 
