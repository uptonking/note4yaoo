---
title: lib-collab-crdt-blog-creator
tags: [blog, collaboration, crdt, creator]
created: 2023-10-28T12:53:24.928Z
modified: 2023-10-28T12:53:48.869Z
---

# lib-collab-crdt-blog-creator

# guide

# blogs

# 📝 [5000x faster CRDTs: An Adventure in Optimization__202107](https://josephg.com/blog/crdts-go-brrr/)
- Automerge (and Yjs and other CRDTs) think of a shared document as a list of characters. 
  - Each character in the document gets a unique ID, and whenever you insert into the document, you name what you're inserting after.

- Automerge is based on an algorithm called RGA
  - Automerge (RGA) solves this with a neat hack. It adds an extra integer to each item called a sequence number. 
  - Whenever you insert something, you set the new item's sequence number to be 1 bigger than the biggest sequence number you've ever seen
  - The rule is that children are sorted first based on their sequence numbers (bigger sequence number first). 
- Why is automerge slow though?
  - Automerge's core tree based data structure gets big and slow as the document grows.
  - Automerge makes heavy use of Immutablejs
  - Automerge treats each inserted character as a separate item.

- Yjs - which we'll see more of later - implements a CRDT called YATA. 
- YATA is identical to RGA, except that it solves this problem with a slightly different hack. 
- Instead of implementing the CRDT as a tree like automerge does
  - Yjs just puts all the items in a single flat list

- how do you insert a new item into a list? 
- With automerge(tree) it's easy:
  - Find the parent item
  - Insert the new item into the right location in the parents' list of children
- But with this list approach it's more complicated:
  - Find the parent item
  - Starting right after the parent item, iterate through the list until we find the location where the new item should be inserted (?)
  - Insert it there, splicing into the array

- I implemented both Yjs's CRDT (YATA) and Automerge using this approach in my experimental reference-crdts codebase
  - It's hard to understand, but once you understand it, you can implement the whole insert function in about 20 lines of code

- The important point is this approach is better:
  - We can use a flat array to store everything, rather than an unbalanced tree. This makes everything smaller and faster for the computer to process.
  - The code is really simple. Being faster and simpler moves the Pareto efficiency frontier. Ideas which do this are rare and truly golden.
  - You can implement lots of CRDTs like this. Yjs, Automerge, Sync9 and others work. You can implement many list CRDTs in the same codebase. In my reference-crdts codebase I have an implementation of both RGA (automerge) and YATA (Yjs). They share most of their code (everything except this one function) and their performance in this test is identical.
# 📝 [I was wrong. CRDTs are the future__202009](https://josephg.com/blog/crdts-are-the-future/)
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
# 👥 [CRDTs are the future | Hacker News_202204](https://news.ycombinator.com/item?id=31049883)
- I don't really understand why every single article on CRDTs is about collaborative text editing. Is no one else bothering to build systems with CRDTs outside of this space?
- Why have I been focussing on collaborative text editing? Because I think performance has been the #1 blocker stopping us from using CRDTs in most software. And text CRDTs are a canary in the coal mine for performance. Uh, thats a tortured metaphor. I mean, If we can make text CRDTs fast, we can make everything fast.
  - And JSON editing (what everyone actually wants) needs to embed text editing anyway. So we've sort of gotta do that first anyway.
  - Smart people have also been working on the JSON editing problem. 
  - Shelf algorithm for last-writer-wins JSON editing is simple enough you can implement it in less than 100 lines of code. But shelf doesn't support collaborative list or text editing (text is a list of characters).
  - thats something Yjs and automerge both already do, and do quite well.

- 👉🏻 Probably because outside collaborative text editing, it's called more generally, like CQRS or event sourcing

- More generally, CRDTs are useful when syncing any kind of change-events between peers (with no central ability to pre-linearize those events), where the ordering of change-events doesn't matter — i.e. where the operations described by the events are "commutative", such that you'll get the same results out if you apply events {1, 2, 3} or {3, 2, 1} or any other order. 
  - As long as all peers see all events, all peers arrive at the same eventually-consistent position in the "lattice" of possible states. 
  - In other words, CRDTs + gossip protocols = the ability for peers to just process events as they hear about them, without a worry about receiving events from peers "out of order"; rather than needing to wait around for a some elected peer to forcibly linearize the events (i.e. without the need to introduce a serial write bottleneck.)
- A good example of the distributed-systems-backend kind of use of CRDTs, is in the Elixir web framework Phoenix, which does a sort of mesh delivery of web-socket messages between a cluster of backends. CRDTs are used to sync presence information (= which clients are connected to which backend) between the backends.
- On the other hand: A lot of practical applications are fine with last write
- I’m more excited about the use of CRDTs outside of text editing, there are so many use cases. However there are still some problems to solve with the existing general purpose toolkits such as Yjs and Automerge. 
  - Take Yjs and it’s ProseMirror bindings, Yjs can represent any internal state of a ProseMirror document and merge them. However it does not have an understanding of the specific ProseMirror schema being used, this could limit the valid states possible (a max length on a heading for example). When Yjs merges multiple edits you could end up with an invalid document for your schema, Yjs loads this into ProseMirror which then throws away the invalid data (with the heading example it just deletes the excess text, it may be better to dump it into the next line but should be configurable).
  - Ultimately the general purpose CRDT toolkits need to have more internal types with a wider ability to capture intent. I also think they need to have the ability to understand the schema of the data structure they are tracking and how to handle more complex merges.
  - The alternative to doing that with a general purpose toolkit is to build your own CRDTs from scratch for your data model. I don’t think many people would go that route though.
- Not all CRDT libraries focus on text editing. For example, I'm working on a Byzantine fault tolerant general-purpose data sync library loosely based on CRDTs: https://www.hyperhyperspace.org

- We at www.ditto.live will likely get to a SQL like implementation with Delta state CRDTs this year.
# 👥 [CRDTs are the future | Hacker News_202009](https://news.ycombinator.com/item?id=24617542)
- I'm part of the team that makes Zoho Writer (a Google Docs alternative)
  - We went with OT for our real-time syncing of edits in 2010 and a decade later, we are still sticking with OT
  - However, in the spirit of "There are no solutions, only trade-offs" CRDTs are absolutely necessary for certain type of syncing - like syncing a set of database nodes.
  - But for systems which already mandate a central server (SaaS/Cloud) and especially for a complex problem like rich-text editing (i.e semantic trees) I still think OT provides better trade-offs than CRDT.
- We went with OT five years ago in CKEditor 5 and we have the same experience. While it would be tempting to try CRDT, it seems to come with too significant tradeoffs in our scenario.

- Right now if you want you can use yjs or sharedb. But the APIs aren't spectacular. Eventually I want these things integrated into svelte / react / swiftui and postgres / sqlite / whatever so it just sort of all works together and we get nice tutorials taking you through what you need to know.
  - We aren't there yet. Automerge is slow (but this is being worked on). Yjs is hard to use well with databases, and its missing some features. We'll get there. The point of all the mathematical formalisms is that if we do it right, it should just work and you shouldn't have to understand the internals to use it.
- It's worth noting that many of the CRDT discussions focus on collaborative text editing. That's a really hard problem. CRDTs are (and have been for some time) a useful primitive for building distributed systems.
# 📝 [Are CRDTs suitable for shared editing?__202008](https://blog.kevinjahns.de/are-crdts-suitable-for-shared-editing/)
- CRDT don't require a central authority to resolve sync conflicts
  - They open up new possibilities to scale the backend infrastructure and are also well-suited as a data-model for distributed apps that don't require a server at all.
- However, several text editor developers report not to use them because they impose a too significant overhead.
- Marijn Haverbeke wrote about his considerations against using CRDTs as a data model for CodeMirror 6
  - the cost of such a representation is significant, and in the end, I judged the requirement for converging positions to be too obscure to justify that level of extra complexity and memory use
- The Xi Editor used a CRDT as its data model to allow different processes (syntax highlighter, type checker, ..) to concurrently access the editor state without blocking the process. They reverted to a synchronous model because
- [CRDT is not pulling its (considerable) weight.__201905](https://github.com/xi-editor/xi-editor/issues/1187#issuecomment-491473599)
  - By now we have lots of examples where trying to design features around the structure imposed by CRDT turned out to be a lot more complicated than it would be in a more synchronous world - we saw the auto-indent stuff above, difficulty getting the selection right in transpose
  - CRDT is a tradeoff
# 👥 [Are CRDTs suitable for shared editing?_202008](https://news.ycombinator.com/item?id=24176455)
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
# 📝 [CRDTs The Hard Parts 笔记_202010](https://zhuanlan.zhihu.com/p/265074361)
- 包括 Google Docs、Figma、Trello 在内的协同编辑软件，需要依赖收敛算法（convergence algorithms）使得不同节点上发生的修改可以确定地（deterministically）合并到一致的状态。
  - 最常见的收敛算法有两类：OT（Operational Transformation）和 CRDT（Conflict-free replicated data type）。

- 首先以 Google Docs 为例介绍 OT。
  - server 会接收不同节点的写，按照规则调整插入的 offset
  - OT 的关键在于使用 server 统筹不同节点的写。
  - OT 保证了只要两个节点接收到同一列操作，即便两列操作的顺序不同，节点上的状态也肯定收敛至相同状态。
- 收敛是很好的性质，但收敛到的状态是否合意（desirable），还需要人为的判断，这一点对于 CRDTs 同样适用。
  - 相比 OT，CRDT 的合并是去中心化的，无需通过 server，但同样需要保证合并是合意的。

## 🐛 Interleaving anomalies(异常事物)

- 方案一：给新插入的字母分配一个位于[0, 1]的数字。
  - 这种方法确实能保证收敛，但下面这种情况明显不是合意的收敛
  - 这种 interleaving 发生在很多 CRDTs（包括 Logoot、LSEQ、Astrong）实现中，而且没办法修复，因为问题根植在算法本身。

- 方案二：RGA。一种叫做 RGA 的 CRDT 算法存在不那么严重的 interleaving 问题。
  - 用户 2 输入的 Alice 可能被插入到用户 1 输入的 dear 和 reader 之间，原因在于 RGA 使用了一种基于时间戳的列表数据结构。
  - 根据 RGA 算法，用户的节点上会形成一个如下的树状链表，每个节点都指向输入时该位置所位于的节点

## 🐛 Moving list items

- 许多 CRDTs 都实现了 List 数据结构，但不支持 move 操作。
  - 用户可以把 move 拆解为 delete-then-insert。
  - 但是会发生下面的 anomaly。
  - 需要找到一个合适的数据结构来表达 pos，让 pos 具有 last writes win 的性质
  - 每个 list item 都要有一个 LWWRegister，并把它们放在一个 Add-Wins Set (AWSet) 中

## 🐛 Moving subtrees of a tree

- 在一棵树内移动子树也是个很 tricky 的问题，但是这样的场景比较常见，例如文件系统就是一棵树。
- 一个可行的解决办法是引入操作的时间戳。

## 🐛 Reducing metadata overhead

- 为了完成 undo 和 redo，CRDT 需要存储很大的 metadata
- Martin 开始介绍 automerge 项目，他的 proposal 和 PR#253 使用 columnar encoding 的思路，使得 CRDT 的 overhead 变得很小。
# more
