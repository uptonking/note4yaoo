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

- ## 
# discuss
- ## 

- ## [如何评价nats这套信息系统（对比于kafka) ？ - 知乎](https://www.zhihu.com/question/267769248)
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

- ## basecamp is using their MySQL database as a queue running millions of jobs each day.
- https://twitter.com/tobias_petry/status/1753408067578773710
  - But you say that a database couldn't handle your (tiny) load and you have to use something more complex?
  - Blindly following the architectures of some FAANG companies (e.g. using Kafka when not needed) will just make your stack more complicated.

- The database queue also makes totally sense when used with transactions. Your job will be visible to outer world the same time the data is visible. Or not when the transaction is aborted. A lot of complexity can be removed by that requirement.
  - The ability to query and re-prioritise things on the fly makes it a more interesting solution too imho.

- Millions of queries per day is tiny. I have databases that do millions of queries a minute.

- ## Just curious, why no one has used Redis streams to build a queue system? 
- https://twitter.com/AmanVirk1/status/1739538111485358269
  - Especially with Consumer groups, it seems to be a great solution.
- Symfony has it well implemented 
- I do. Quite simple to implement.

- ## Seeing several #Postgres-based queue implementations lately, 
- https://twitter.com/gunnarmorling/status/1733245970341646742
  - one thing I've been wondering: could vacuuming become an issue here, with lots of potentially short-lived records in high volume/through-put scenarios?
- Bloat needs to be managed. Autovacuum can be tuned aggressively to deal with it, but it is not free. We wrote about that
- Right. This is how PGQ https://github.com/pgq/pgq works for decades already (developed in Skype long ago). Nobody has achieved better results yet I think, and all new tools should look at this experience. BTW, CloudSQL is equipped with PGQ as I learned recently.
- Of course, a Postgres-based queue has its limits compared to message brokers, but with reasonable care, it can go far 
