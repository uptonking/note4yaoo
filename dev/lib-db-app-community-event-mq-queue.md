---
title: lib-db-app-community-event-mq-queue
tags: [community, database, kafka, mq, queue]
created: 2023-12-09T12:32:17.786Z
modified: 2023-12-09T12:32:50.692Z
---

# lib-db-app-community-event-mq-queue

# guide

# discuss-stars
- ## 

- ## 

- ## 🆚️ Trade-offs between Topics and Queues and 5 questions to pick the "right" one.
- https://twitter.com/RaulJuncoV/status/1767894183560220931
1. What are the Application requirements?
If you need to ensure that exactly one consumer processes a message, use a queue.
If your application requires sending messages to many consumers, use a topic.

2. Do you need message durability and delivery guarantees?
You need message durability and acknowledgments if you can't afford to lose messages.
Queues offer better support for message durability out of the box. Topics might need more configuration.

3. Scalability?
Queues are better suited for scaling workloads. Each consumer you add can process messages in parallel without stepping on each other's toes.
With topics, adding more subscribers means all subscribers process each message. You are not distributing the workload; you are only adding more consumers.

4. How about if one of your consumers is not available now?
In topics, keeping track of which subscribers have received which messages adds overhead.
Managing this state is complex, especially if message order matters.

5. How likely are your system's messaging needs to evolve?
If this is a young system, it will change frequently.
Topics may provide the flexibility needed to adapt without significant re-architecture.
For more stable, defined workflows, queues offer simplicity and directness.

- Could integrating both queues and topics offer a more versatile messaging solution?
# discuss-kafka
- ## 

- ## 

- ## In 4.0, Kafka is becoming a Queue
- https://x.com/BdKozlovski/status/1891139227599183920
  - it always fell short trying to address task coordination use-cases which lend themselves more to a queue-like system: • granular per-record acknowledgement
  - Cases like job distribution, where a consumer gets the message, acts on the job and then archives it - were trickier to implement with Kafka.
  - Another pain point was that consumers were coupled with the number of partitions.

- KIP-932 addresses this.
At a high level, it supports:
  ✅ - the ability for many consumers to read from the SAME partition
  ✅ - individual records acknowledgments
  ✅ - still keeps producers and consumers decoupled
  ✅ - no maximum queue size
  ✅ - messages are still retained - so you have the ability to replay

- ## Apache Kafka is really just software that copies files across machines and lets you reads those files’ data in real time.
- https://x.com/BdKozlovski/status/1892223118636364001
  - The best way to understand distributed systems is to look at them bottoms-up from first principles 
  - The basic storage unit in the OS is a file. The basic storage unit in Kafka is a replica.
  - A replica is really just an ordered bunch of files - a linked list where each node is a file.

# discuss
- ## 

- ## 

- ## 

- ## 最近看了一圈所谓 MQ 的实现，发现它们确实分成队列和流两种方案。
- https://x.com/tison1096/status/1898241411004481851
  - 总的来说，队列强调的是消息实时推送，可以没有消息持久化的能力；流强调的是 Append-Only 日志的读写，必须持久化。两者在消费端的差异也非常明显，队列的用例下，订阅可以是局部的，读到哪算哪；消息流的用例里，订阅通常是全局协调的。
  - 由于所有 MQ 都强调尾读尾写的效率，因此根据消息订阅模式的不同，具体的实现也会分成两种，即有或没有 Partition 的概念。
  - 典型的队列，例如 NSQ、NATS 乃至 Google Pub/Sub 等，是不需要 Partition 的，Subscriber 连上哪算哪。Broker 基本等同于一组 Publish Forwarder，消费者同时连上所有发布本主题消息的 Forwarder，Forwarder 本地管理订阅。这种设计下，如果将 Forwarder 设计成无状态的，那么一旦 Forwarder 宕机，那么发布到它上面的数据就无法恢复了。否则它就是有状态的（持久化路径位置，以及对该位置独占的状态）。
  - 典型的流，例如 Apache Kafka 等，会引入 Partition 的概念。虽然 Kafka 本身有 Broker 侧的 Partition Owner 角色，但是实际上这个角色可以被擦掉，就像 WarpStream 的设计那样。这里的重点是同一个 Partition 只会被一个消费者消费，从而将订阅管理的责任从 Broker 一侧挪到了 Client 一侧，也就引入了 Rebalance 重新分配订阅关系的需求。
- 这么看下来，由于 MQ 的消费模式是实时拉取或推送，而不是 DB 那样每次都是一个新的查询，所以 MQ 的设计，如果要求持久化，那么就有以下的实现困境：
  - 1. 如果不要 Partition 以规避 Rebalance 的复杂性和支持任意数量的消费者并发，那么就要走 Publish Forwarder 的路线。此时如果不能接受消息可能丢失，甚至要支持 Seek 重新消费数据，那么 Forwarder 必须是一个 Stateful 的部署。
  - 2. 如果支持消息堆积，实现消息流的场景，又要实现 Stateless 的 Broker，那么似乎只有引入 Topic Partition 这样的概念，引入额外的订阅协调流程，并限制消费的并发度。
  - 例如，NSQ 就是第一种，Kafka 是第二种，EMQX 是第一种。NATS 不带 JetStream 是第一种，带了 JetStream 是 Raft Group 做持久化，也是第一种。Google PubSub 是第一种，虽然实现没有披露语焉不详，但是底下看起来也是某种 Quorum-based 的存储方案，这个肯定是 Stateful 的。

- ## Kafka (somewhat) noob question: how does a client select the listener  when there are multiple advertised listeners? I have Kafka in Docker (via Testcontainers), with two advertised listeners
- https://x.com/gunnarmorling/status/1855205862492475660
  - Kafka Connect, running within the same  Docker network, picks up the former (i.e. the mapped port for access from the host). Can I force it to use that other, Docker-network, internal one?

- If you give a broker a hostname, your client can use that hostname + port in the bootstrap.servers. That way it should connect based on BROKER listener, I think.

- The client must be configured to connect to a specific listener. It cannot select on its own afaik.

- ## 🆚 [RabbitMQ vs Kafka - Difference Between Message Queue Systems - AWS](https://aws.amazon.com/compare/the-difference-between-rabbitmq-and-kafka/)
- Kafka and RabbitMQ are message queue systems you can use in stream processing. 
- RabbitMQ and Apache Kafka allow producers to send messages to consumers. 
  - Producers are applications that publish information, while consumers are applications that subscribe to and process information.
- Producers and consumers interact differently in RabbitMQ and Kafka. 
  - In RabbitMQ, the producer sends and monitors if the message reaches the intended consumer. 
  - On the other hand, Kafka producers publish messages to the queue regardless of whether consumers have retrieved them.

- 
- 

- ## FWIW, Kafka may be closer to a filesystem than a database. 
- https://x.com/felixgv/status/1794298921470333057
  - You can create and delete directories (topics), files within them (partitions), append to files, tail files, scan files and… that’s about it 

- ## Why is everyone suddenly talking about rabbitmq?
- https://twitter.com/isamlambert/status/1777344945017471156
- Dunno but I had to migrate to bullmq pretty quickly
- Everyone needs a bus for their micro service based todo apps.

- ## 🆚 [如何评价nats这套信息系统（对比于kafka) ？ - 知乎](https://www.zhihu.com/question/267769248)
- 

- [nats消息队列 - 知乎](https://zhuanlan.zhihu.com/p/666658170)
  - NATS原来是使用Ruby编写，可以实现每秒150k消息，后来使用Go语言重写，能够达到每秒8-11百万个消息。

- ## Bullmq users: What API should I use for the following scenario?
- https://twitter.com/AmanVirk1/status/1754842367536873546
  - I have a job, and when processing it, I find that some prerequisites for the job are not ready. So, I want to reschedule this job after 10 seconds. This rescheduling should not count against the failed attempts

- A custom back off strategy ?
  - Back off strategy is for re-attempting failed jobs. I don't want this job to be marked as failed, since I never processed it and technically it never failed

- Ideally avoid the race condition by splitting the requirement check and the execution in two jobs, if the requirement check pass add the execution job, if not add another requirement check job
  - The jobs are shown to the user. Think of it as your Github actions jobs list. Whatever I do, I cannot create multiple jobs for a single action. Otherwise the user will see duplicate jobs for a brief period
- I think controlling UI display in sql database and updating at job level will be the way to go with bull
  - Yeah, that is what I think I will do

- I just remove and re-add with the needed delay
  - Cannot remove a job while processing it.

- Please take a look at docs [Manually processing jobs - BullMQ](https://docs.bullmq.io/patterns/manually-fetching-jobs)

- ## 🧱 Just curious, why no one has used Redis streams to build a queue system? 
- https://twitter.com/AmanVirk1/status/1739538111485358269
  - Especially with Consumer groups, it seems to be a great solution.
- Because they are similar to Kafka Consumer Groups. You need to name each consumer (process), meaning that scaling this requires some level of manual intervention to guarantee at-least-once semantics. Essentially… SQS is a killer for all possible queues. Phenomenal DX.
  - Yeah, this is how it went for us - we used an in-house solution utilising Redis as it was already part of our stack and let us move forward. Ultimately we switched to Amazon SQS for our critical products, but redis is in our back pocket for non-critical/temporary products
- Symfony has it well implemented 
- I do. Quite simple to implement.

- Last I checked, both bull and bullmq weren't using Streams

- ## 🐬 basecamp is using their MySQL database as a queue running millions of jobs each day.
- https://twitter.com/tobias_petry/status/1753408067578773710
  - But you say that a database couldn't handle your (tiny) load and you have to use something more complex?
  - Blindly following the architectures of some FAANG companies (e.g. using Kafka when not needed) will just make your stack more complicated.

- The database queue also makes totally sense when used with transactions. Your job will be visible to outer world the same time the data is visible. Or not when the transaction is aborted. A lot of complexity can be removed by that requirement.
  - The ability to query and re-prioritise things on the fly makes it a more interesting solution too imho.

- Millions of queries per day is tiny. I have databases that do millions of queries a minute.

- ## 🐘 Seeing several #Postgres-based queue implementations lately, 
- https://twitter.com/gunnarmorling/status/1733245970341646742
  - one thing I've been wondering: could vacuuming become an issue here, with lots of potentially short-lived records in high volume/through-put scenarios?
- Bloat needs to be managed. Autovacuum can be tuned aggressively to deal with it, but it is not free. We wrote about that
- Right. This is how PGQ https://github.com/pgq/pgq works for decades already (developed in Skype long ago). Nobody has achieved better results yet I think, and all new tools should look at this experience. BTW, CloudSQL is equipped with PGQ as I learned recently.
- Of course, a Postgres-based queue has its limits compared to message brokers, but with reasonable care, it can go far 
