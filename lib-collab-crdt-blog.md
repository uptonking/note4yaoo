---
title: lib-collab-crdt-blog
tags: [blog, collaboration, crdt]
created: 2022-10-13T07:59:52.953Z
modified: 2022-10-13T08:00:21.260Z
---

# lib-collab-crdt-blog

# guide

# [Operation-based CRDTs: registers and sets](https://www.bartoszsypytkowski.com/operation-based-crdts-registers-and-sets/)
- Registers are one the most wide spread ways of working with CRDTs. 
  - The reason is simple: they allow us to wrap any sort of ordinary data types in order to give them CRDT-compliant semantics.
  - However, this comes at the price - we cannot simply change any non-CRDT value into CRDT without some compromises: if that would be possible, we wouldn't need CRDTs in the first place. 
  - For these, two popular approaches are known as last-write-wins and multi-value registers.
# [supabase: `pg_crdt` - an experimental CRDT extension for Postgres_202212](https://supabase.com/blog/postgres-crdt)
- https://github.com/supabase/pg_crdt
  - pg_crdt is an experimental extension adding support for conflict-free replicated data types (CRDTs) in Postgres.
  - It supports Yjs/Yrs and Automerge.
  - Our goal was to evaluate if we could leverage a Postgres-backed CRDT and Supabase's existing Realtime API for change-data-capture to enable development of collaborative apps on the Supabase platform.
  - pg_crdt extension is a proof-of-concept that wraps rust's yrs and automerge libraries using the pgx framework to add a Postgres native CRDT, crdt.ydoc.

- CRDTs are a special type of data structure designed to solve a specific problem: they can merge changes in a way that the final state of the data will be the same, no matter the order in which the updates were applied.
  - In simple terms, a CRDT allows multiple users to make changes to the same data without the need for a central authority to coordinate their actions.
- I personally believe CRDTs are the future. For some things. If databases were invented today, I'm certain most of the effort would be spent developing CRDT databases or something with “offline algorithms” built-in.
- It's possible that developers will need to be selective about their “level” of offline support, at least if they plan to use an “incumbent” databases. 
  - For the cases, a simple “last write wins” strategy is probably acceptable (see the excellent Replicache and Watermelon libraries), but there will be important pieces of their application where it is not.
- pg_crdt is an extension which adds CRDT support to Postgres as a data type.
  - The `content` column is now a Yjs Doc. 
  - Updates to this column are commutative and idempotent. 
  - This means that they can be applied in any order and multiple times, and the result will always be the same.
- both Yjs and Automerge have JavaScript and Rust implementations, which means they work natively in both a browser and a Postgres environment. 

- ❓ Why not build this into Realtime?
- An alternative approach for CRDT support in Supabase is to build support directly into Realtime and use it as an Authoritative server.
  - In this scenario, Realtime would serialize the CRDT and save it to Postgres (probably as a bytea data type). 
  - Yjs has the concept of Providers which would facilitate this. 
- realtime as an authority
  - Realtime acts as the “middleman” for saving the CRDT in the database
- postgres as an authority
  - CRDT is pushed directly to the database, and Realtime receives updates from Postgres. (Note also that clients can send peer-to-peer updates.)
- If we make Realtime the authority, it strongly couples developers to the Supabase infrastructure. 
  - By placing the CRDT into the database, it simplifies the architecture, enables other tools (like Debezium), and provides the possibility to update the database directly (for semi-realtime events like counters or page-views).

- These are a few of the known limitations:
  - Realtime broadcasts database changes from the Postgres write ahead log (WAL). The WAL includes a complete copy of the the underlying data so small updates cause the entire document to broadcast to all collaborators
  - Frequently updated CRDTs produce a lot of WAL and dead tuples
  - Large CRDT types in Postgres generate significant serialization/deserialization overhead on-update.

## [Show HN: Pg_CRDT – an experimental CRDT extension for Postgres | Hacker News](https://news.ycombinator.com/item?id=33931971)

- [pg_crdt - a CRDT extension for #postgresql](https://twitter.com/kiwicopple/status/1601553881246609409) 

- The heavy-lifting is done by the teams at Yjs[0] and Automerge[1], who have re-implemented their JS libs in Rust. This made it possible for us to wrap them into a Postgres extension using pgx[2] (which is fast becoming a de-facto tool at supabase)

- Support for CRDT columns within a db to enable JSON like indexing/querying capabilities is fundamental to then building some exciting further developments. Supporting both Yjs and Automerge is exactly the right route forward.
- did you investigate querying/indexing within the documents?
  - Without the ability to index properties, or do ad-hock queries, on the documents there is little reason to to the merging in-DB. It then makes more sense to merge outside the DB and save both the raw CRDT object and a serialised JSON next to it for querying. I assume that if you had found it's performance better, indexing+querying would have been the next step?
  - Personally I find the offline + eventual consistency the most interesting use case. The ability to sync a users document set to a local db (SQLite or a future mini-pg/supabase) with local querying and then merge them back later. This could be as basic as a three column table (guid, doc, clock), the clock being a global Lamport like clock to enable syncing only changed documents.

> This could be as basic as a three column table (guid, doc, clock), the clock being a global Lamport

This would be achievable, but also perhaps quite strict - we're dictating a table structure rather than working with existing CRDT libs. That said, we could probably do this today, without any mods/extensions

> querying/indexing

Yeah, there is nothing in this implementation for that

> Without the ability to index properties, or do ad-hock queries, on the documents there is little reason to to the merging in-DB

One benefit is the ability to send "directly" to the database, but I agree that lack of additional features in the current form outweighs this benefit

> a serialised JSON

This is how we might do it with with "Realtime as an authority" approach (and is the most likely approach tbh).

- Last Writer Wins is not the most compelling use case for CRDT because if those fruits were denormalized into Postgres rows, you'd already have the behavior described. 
- In general, Sequence CRDTs seem to be the most difficult and most interesting area of continuous research. In my own work, I've implemented a sequence CRDT to create a distributed log of events across users that then (because the order is guaranteed to eventually be the same for each device) can just be reduced to whatever data structure you need. It means, we end up with one CRDT to rule them all and then can just write the "conflict resolution" in simple term with the business logic.
# [去中心化在线协作：Feakin 的图形协作是如何设计的？_202209](https://www.phodal.com/blog/collaboration-with-crdt/)
- 通讯协议：WebSocket vs HTTP
- 数据格式：JSON vs Binary
- 协作算法：中心化还是去中心化？ OT 算法 vs CRDT

- 服务端：Actix + Diamond Types + CRDT
- 客户端：编辑生成 patches
- 客户端：编辑器应用 patches
# [CRDT——解决最终一致问题的利器_201809](https://juejin.cn/post/6844903672032264199)
- 先简单统一一下概念
  - object: 可以理解为“副本”
  - operation: 操作接口，由客户端调用，分为两种，读操作query和写操作update
  - query: 查询操作，仅查询本地副本
  - update: 👉🏻 更新操作，先尝试进行本地副本更新，若更新成功则将本地更新同步至远端副本
  - merge: update在远端副本的合并操作

- 一个数据结构符合CRDT的条件是update操作和merge操作需满足交换律、结合律和幂等律
- 如果update操作本身满足以上三律，merge操作仅需要对update操作进行回放即可，这种形式称为op-based CRDT，最简单的例子是集合求并集。
- 如果update操作无法满足条件，则可以考虑同步副本数据，同时附带额外元信息，通过元信息让update和merge操作具备以上三律，这种形式称为state-based CRDT。
- 让元信息满足条件的方式是让其更新保持__单调__，这个关系一般被称为__偏序关系__。
  - 举一个简单例子，每次update操作都带上时间戳，在merge时对本地副本时间戳及同步副本时间戳进行比对，取更新的结果，这样总能保证结果最新并且最终一致，这种方式称为Last Write Wins
- update操作无法满足三律，如果能将元信息附加在操作或者增量上，会是一个相对state-based方案更优化的选择
- 如果同步过程能确保exactly once的语义，幂等律条件是可以被放宽掉，比如说加法本身满足交换律结合律但不幂等，如果能保证加法操作只回放一次，其结果还是最终一致的。
# [如何设计 CRDT 算法](https://www.zxch3n.com/crdt-intro/design-crdt/)
- 以 Op-based CRDT 的思路设计 Last-write-wins Set(LWWSet)
# [数据库系统小报：CRDT初探](https://zhuanlan.zhihu.com/p/510797688)

# [CRDTs go brrr](https://josephg.com/blog/crdts-go-brrr/)
- Automerge (and Yjs and other CRDTs) think of a shared document as a list of characters. 
  - Each character in the document gets a unique ID, and whenever you insert into the document, you name what you're inserting after.
# [I was wrong. CRDTs are the future_202009](https://josephg.com/blog/crdts-are-the-future/)
- I saw Martin Kleppmann’s talk a few weeks ago about his approach to realtime editing with CRDTs, and I felt a deep sense of despair(绝望). 
  - Maybe all the work I’ve been doing for the past decade won’t be part of the future after all, because Martin’s work will supersede it. Its really good.
- Around 2010 I worked on Google Wave. 
  - Wave was an attempt to make collaboratively editable spaces to replace email, google docs, web forums, instant messaging and a hundred other small single purpose applications. 
- Internally, Wave’s collaborative editing was built on top of Operational Transform (OT). 
  - OT has been around for awhile - the algorithm we used was based on the original Jupiter paper from 1995. 
  - It works by storing a chronological(按时序排列的) list for each document of every change.
- Most of the time, users are editing the latest version of the document and the operation log is just a list of all the changes. 
  - But if users are collaboratively editing, we get concurrent edits. 
  - When this happens, the first edit to arrive at the server gets recorded as usual. 
  - If the second edit is out of date, we use the log of operations as a reference to figure out what the user really intended. (Usually this just means updating character positions). 
  - Then we pretend as if thats what the user meant all along and append the new (edited) operation. 
  - Its like realtime git-rebase.
- Once Wave died, I reimplemented the OT model in ShareJS.
  - https://github.com/josephg/sharejs
  - It only took about 1000 lines of code to get a simple collaborative editor working
  - At its heart, OT is a glorified(吹捧的；吹嘘的；美化的) `for()` loop with some helper functions to update character offsets. 
  - In practice, this works great. OT is simple and understandable. 
  - Implementations are fast. (10k-100k operations per second in unoptimized javascript. 1-20M ops/sec in optimized C.). 
  - The only storage overhead is the operation log, and you can trim that down if you want to. (Though you can’t merge super old edits if you do). 
  - You **need a centralized server to globally order operations**, but most systems have a centralized server/database anyway, right?

- The **big problem with OT is that dependency on a centralized server**.
  - The reason (I think) is that when you open a google doc, one server is picked as the computer all the edits run through. When the mob descends, google needs to pull out a bunch of tricks so that computer doesn’t becomes overwhelmed.
- There’s some workarounds they could use to fix this. 
  - Aside from sharding by document (like google docs), you could edit via a retry loop around a database transaction. 
  - This pushes the serialization problem to your database. (Firepad and ShareDB work this way).
  - Its not perfect though. 
  - We ended up with a scheme where every wave would arrange a tree of wave servers and operations were passed up and down the tree. But it never really worked. 
  - I don’t think they were ever fixed in the opensource version. Its all just too complicated.

- researchers have been busy trying to make OT work better. 
  - The most promising work uses CRDTs (Conflict-Free Replicated data types). 
  - CRDTs approach the problem slightly differently to allow realtime editing without needing a central source of truth.
- People have been asking me what I think of them(CRDT)
  - They’re slow. Like, really slow. Eg Delta-CRDTs takes nearly 6 hours to process a real world editing session with a single user typing a 100KB academic paper.
  - Because of how CRDTs work, documents grow without bound. The current automerge master takes 83MB to represent that 100KB document on disk. It needs to be loaded into memory to handle edits.
  - CRDTs are missing features that OT has had for years. For example, nobody has yet made a CRDT that supports /object move/ (move something from one part of a JSON tree to another). 
  - CRDTs are complicated and hard to reason about.
  - You probably have a centralized server/database anyway.
- I made all those criticisms and dismissed CRDTs. But in doing so I stopped keeping track of the literature. 

- CRDTs went and quietly got better.
  - Speed: Using modern CRDTs (Automerge/RGA or y.js/YATA), applying operations should be possible with just an log(n) lookup. 
  - Size: Martin’s columnar encoding can store a text document with only about a 1.5x-2x size overhead compared to the contents themselves. 
  - Features: There’s at least a theoretical way to add all the features using rewinding and replaying, though nobody’s implemented this stuff yet.
  - Complexity: I think a decent CRDT will be bigger than the equivalent OT implementation, but not by much. 
- Martin managed to make a tiny, slow implementation of automerge in only about [100 lines of code](https://github.com/automerge/automerge/blob/main/test/fuzz_test.js).
  - https://github.com/automerge/automerge
  - A JSON-like data structure (a CRDT) that can be modified concurrently by different users, and merged again automatically.
  - Automerge is a library of data structures for building collaborative applications in JavaScript.
- I still wasn’t completely convinced by the speed argument, so I made a simple proof of concept CRDT implementation in Rust using a B-tree using ideas from automerge and benchmarked it.
  - So that means we’ve made CRDTs good enough that the difference in speed between CRDTs and OT is smaller than the speed difference between Rust and Javascript.
- automerge isn’t the only decent CRDT out there. 
  - Y.js works well and kicks the pants off automerge’s current implementation in the Y.js benchmarks. 
  - Its missing some features I want, but its generally easier to fix an implementation than invent a new algorithm.

- I care a lot about inventing the future.
  - But I’m no longer convinced OT - and all the work I’ve done on it
  - I feel really sad about that.
- JSON and REST are used everywhere these days. Lets say in 15 years realtime collaborative editing is everywhere. Whats the JSON equivalent for realtime editing that anyone can just drop in to their project? 
  - In the glorious future we’ll need high quality CRDT implementations, because OT just won’t work for some applications. 
  - You couldn’t make a realtime version of Git, or a simple remake of Google Wave with OT. 
- But if we have good CRDTs, do we need good OT implementations too? I’m not convinced we do. 
  - Every feature OT has can be put in to a CRDT. (Including trimming operations, by the way). But the reverse is not true.
  - Smart people disagree with me, but if we had a good, fast CRDT available from every language, with integration on the web, I don’t think we need OT at all.
- OT’s one advantage is that it fits well in centralized software - which is most software today. 
  - But distributed algorithms work great in centralized software too. (Eg look at Github). 
  - And I think a really high quality CRDT running in wasm would be faster than an OT implementation in JS. 
  - And even if you only care about centralized systems, remember - Google runs into scaling problems with Google Docs because of OT’s limitations.
- So I think its about time we made a lean and fast CRDT. The academic work has been mostly done. We need more kick-ass implementations.
- I increasingly don’t care for the world of centralized software.
  - Philosophically, if I modify a google doc my computer is asking Google for permission to edit the file. 
  - (You can tell because if google’s servers say no, I lose my changes.
- In comparison, if I git push to github, I’m only notifying github about the change to my code. My repository is mine.
  - I own all the bits, and all the hardware that houses them. 
  - This is how I want all my software to work.
- Thanks to people like Martin, we now know how to make good CRDTs. 
  - But there’s still a lot of code to write before local first software can become the default.
  - I mourn all the work I’ve done on OT over the years. 
  - But OT is no longer fits into the vision I have for the future. 
  - CRDTs would let us remake Wave, but simpler and better. 
  - And they would let us write software that treats users as digital citizens, not a digital serfs(农奴).

- discussion

- [CRDTs are the future](https://news.ycombinator.com/item?id=24617542)
- I'm part of the team that makes Zoho Writer (a Google Docs alternative)
  - We went with OT for our real-time syncing of edits in 2010 and a decade later, we are still sticking with OT
  - However, in the spirit of "There are no solutions, only trade-offs" CRDTs are absolutely necessary for certain type of syncing - like syncing a set of database nodes.
  - But for systems which already mandate a central server (SaaS/Cloud) and especially for a complex problem like rich-text editing (i.e semantic trees) I still think OT provides better trade-offs than CRDT.
- We went with OT five years ago in CKEditor 5 and we have the same experience. While it would be tempting to try CRDT, it seems to come with too significant tradeoffs in our scenario.

- Right now if you want you can use yjs or sharedb. But the APIs aren't spectacular. Eventually I want these things integrated into svelte / react / swiftui and postgres / sqlite / whatever so it just sort of all works together and we get nice tutorials taking you through what you need to know.
  - We aren't there yet. Automerge is slow (but this is being worked on). Yjs is hard to use well with databases, and its missing some features. We'll get there. The point of all the mathematical formalisms is that if we do it right, it should just work and you shouldn't have to understand the internals to use it.
- It's worth noting that many of the CRDT discussions focus on collaborative text editing. That's a really hard problem. CRDTs are (and have been for some time) a useful primitive for building distributed systems.
# [Are CRDTs suitable for shared editing?__202008](https://blog.kevinjahns.de/are-crdts-suitable-for-shared-editing/)
- CRDT don't require a central authority to resolve sync conflicts
  - They open up new possibilities to scale the backend infrastructure and are also well-suited as a data-model for distributed apps that don't require a server at all.
- However, several text editor developers report not to use them because they impose a too significant overhead.
- Marijn Haverbeke wrote about his considerations against using CRDTs as a data model for CodeMirror 6
  - the cost of such a representation is significant, and in the end, I judged the requirement for converging positions to be too obscure to justify that level of extra complexity and memory use
- The Xi Editor used a CRDT as its data model to allow different processes (syntax highlighter, type checker, ..) to concurrently access the editor state without blocking the process. They reverted to a synchronous model because
- [CRDT is not pulling its (considerable) weight.__201905](https://github.com/xi-editor/xi-editor/issues/1187#issuecomment-491473599)
  - By now we have lots of examples where trying to design features around the structure imposed by CRDT turned out to be a lot more complicated than it would be in a more synchronous world - we saw the auto-indent stuff above, difficulty getting the selection right in transpose
  - CRDT is a tradeoff

## Are CRDTs suitable for shared editing?_202008

- https://news.ycombinator.com/item?id=24176455
- I’m part of the team that makes Zoho Writer (Google Docs alternative)
  - Back in 2009, we wrote our real time collaboration component using Operational Transformations (OT). 
- But when CRDTs started to gain the spotlight, these are the reasons why it didn’t warrant a rewrite to our stack:
  1. Memory issues with tombstones(墓碑). Marking as deletion has a cost of maintaining them throughout the session.
  2. CRDTs were perfect for plain strings and arbitrary key/value pairs. But when it comes to schematic JSON that has semantic value, CRDT was an added overhead. For example, try making a collaborative HTML editor with support for table operations. It is very likely you will end up with a table structure that is invalid to render. In OT analysing, modifying or cancelling ops were much easier.
  3. Since the software is primarily a cloud document editor, a central server is necessary even otherwise. So why not use the server for efficient version management and operation sequencing as well? Why prefer CRDTs whose bulk of complexity comes from eliminating the need of a central system?
- Such practical reasons have kept us from venturing into CRDTs. 
  - As of now, common editing platforms like Google Docs, Zoho Writer, CKEditor, ProseMirror, Quill, CodeMirror - all of these work with OTs instead of CRDT for collaborative editing.
- I think the main impetus for this post is to assert that #1 and #2 aren't much of a problem for Yjs, as they are for the arguably more well-known CRDT lib for JS, Automerge.
  - With respect to #3, one reason to prefer CRDTs over OT (even if a central server is required for other stuff) is that making the collaboration infra P2P can save a lot of resources if most of your collab is happening between a few individuals at a time. 
  - Not very necessary at a small scale, but if you have 10, 000 small teams collab'ing, the cost savings you get from off-loading RTC to the end users can definitely add up.

- OT doesn’t require a central server, just a tie breaker. You could just do leader election over webRTC using raft and offload OT to the client side as well and have that node push updates to the server for durable saving every x seconds and shift RTC off your infra.
  - Right, the idea that OT requires a "central server" is a bit of an oversimplification. It requires an authority that can serialize concurrent revisions into a globally consistent sequence. By far the easiest way to achieve that is an actual central server, but distributed algorithms have also been published for a long time, for example SOCT2 which uses a state vector.
  - **The downside is the complexity**. Now there are more things that can go wrong: the OT algorithm can fail (either due to bugs or because of corrupted data), and now also the distributed consensus algorithm can fail as well. 
  - When you have this level of complexity, going to CRDT is pretty appealing as an alternative.

- I've implemented operational transform based systems several times, and every time I check out CRDTs I end up staying with OT.
  - I find the complexity arguments against OTs to be far, far overblown and mostly academic, and that OT is, for me, much easier to understand.
  - The **two big critiques against OT are transform explosion**: you could have N^2 transforms. Except that not every operation pair interacts. I usually see just a couple of categories of operations: text, key/value, tree, and list, and they all only need transforms within a category.
  - The **second critique is around sequencing in a distributed system**, but I've also never seen a production system that doesn't have a central coordinating service. With a star topology OT sequencing because simple. You don't even need a lamport clock, you can get away with a simple counter. Buffering at the clients simplifies even more.
  - There's a great series of posts on collaborative editing by Marijn Haverbeke, the author of CodeMirror and ProseMirror, that are designed with OT in mind

- It seems like CRDTs would be useful for contact tracing in that distributed contact tracers collect data on cases and potential cases. They operate independently for hours through the day with occasional network access or at least end of day.
  - Since there is no concurrency in contact tracing (only you will manipulate your own data), a CRDT might be an unnecessary overhead. 
  - There is concurrency in contact tracing. In developing nations it’s like a map reduce problem. You send out the contact tracers in the morning, they gather results and sync up at the end of the day.
# more-crdt
- [CRDTs and Realtime Collaboration](https://nyxtom.dev/2020/09/01/intro-to-crdts)

- [Introduction to CRDTs for Realtime Collaboration](https://dev.to/nyxtom/introduction-to-crdts-for-realtime-collaboration-2eb1)
  - 对各种数据类型进行了简介

- [Collaborative Web Apps_202108](https://zjy.cloud/posts/collaborative-web-apps)
  - At the time of the writing, one shortcoming of Replicache is that its local transactions are not fast enough to enable heavy interactions such as drag and drop. 
  - To prevent lagging, we turned on the useMemstore: true option to disable offline support. 
