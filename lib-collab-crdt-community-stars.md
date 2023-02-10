---
title: lib-collab-crdt-community-stars
tags: [collaboration, community, crdt]
created: 2021-11-24T17:08:48.275Z
modified: 2022-04-05T10:09:51.343Z
---

# lib-collab-crdt-community-stars

# guide

 

# discuss
- ## 

- ## [Building a BFT JSON CRDT | Hacker News](https://news.ycombinator.com/item?id=33694568)
- It's the Byzantine Fault Tolerant part of this that is particularly innovative and based on Kleppmanns most recent work. I believe it solves the issue of either malicious actors in the networks modifying others transactions, spoofing them, or the messages being modified by third parties ("outside" the network) who have MITM the connection. These are really great problems to solve.

- Interesting, yeah access-control is kinda open problem with Yjs. Regarding ProseMirror and rich-text documents, you can mess up documents in other ways as well. Eg deploy a faulty command with a transaction that inserts nodes with invalid children (can be prevented though by using createChecked). Or just changing your schema in an incompatible way with the previous version. So you kinda have to deal with possible malformed documents either way.
  - And about the schema layer on top of Yjs, you possibly could inspect every update and apply some validation rules. Arent all operations just inserts, updates or deletes of nodes? You can at least rollback to previous version as you flush the updates to the doc in the db. Not ideal though.

- When I was working on this problem with Fluid Framework, we did a few interesting experiments with "owned objects" and centralized ACL objects. I believe the team primarily implemented centralized ACL because that implementation works for many enterprise use cases.
  - With a centralized schema provider, you run a connected node on a trusted server and reject changes that are out of schema or should not be accessed by a user.
  - An owned object is an object where a user (or user group that votes via quorum) that owns the object can veto changes to the object. The changes are temporarily applied until accepted by the owners. I haven't dug deep enough into this BFT implementation to know how our model would map to this model.

- ## I remember having read about Gun a few years ago and there was a lot of (apparently) valid criticism. Do you know how much of that is still valid today?_201803
- https://news.ycombinator.com/item?id=16523087
  - [Show HN: Gun v0.1.0 – The Easiest Database Ever_201502](https://news.ycombinator.com/item?id=9076558)
- If you intend to use GUN for banking or any globally consistent (CP) system, then yes.
  - However, for everything else, the criticisms no longer apply.
  - GUN is an CRDT based AP (highly-available, partition tolerant) strongly eventually consistent system, and therefore should not be used for banking-like systems.

- Neo4j is Master-Slave, GUN is Master-Master (or Multi-Master, or Masterless). Basically, GUN is P2P/decentralized, Neo4j is centralized.
- GUN has realtime updates/sync built in, Neo4j does not.
- GUN has offline-first features, Neo4j does not.
- Neo4j has its own query language, GUN has a FRP (Functional Reactive Programming) based JS API.
- Neo4j is over a decade old, GUN since late 2014.
- Neo4j is more monolithic, GUN is more microservice-y.

- ## [OT and CRDT trade-offs for Real-Time collaboration_202001](https://news.ycombinator.com/item?id=22039950)
- [Creating a Collaborative Editor](https://pierrehedkvist.com/posts/1-creating-a-collaborative-editor)
  - In my CRDT implementation, I would add meta-data to each character, with the boolean property which is either bold or not. It's certainly cumbersome to keep the cursor at the right place when inserts are being made, but it's doable.
  - I personally never understood how OT actually works, clearly, Google Docs and others find it useful. But to me, CRDT has more solid proof and reasoning behind it, and it is easier to comprehend.
- The best CRDTs do treat each character separately (as I think I mentioned at one point?). But not all of them - the video and my example is an example of one that doesn't.
  - It's also very difficult to support arbitrary nested trees with a per-character data type, which leads to the compromises I talked about.

- After 8 years of working on this, I have changed my thoughts:
  - The correct algorithm is not always the correct user experience.
  - End-to-end encryption is too important to not have.
  - Offline support is great, but it behaving consistently is more important than it behaving "intently".
  - Biggest pain points can most easily be solved at the editing layer, not data layer.
  - As a result, OT gets thrown out the door immediately.
- I built the most popular CRDT powered database on the market https://github.com/amark/gun, but have some harsh words for CRDT obsessed people
  - CRDTs are great, but if you create an infinitely complex one to handle "every word editing operation" it'll actually result in an inferior(较差的；次的) user experience.
  - As such, for example, GUN supports lock-free concurrent operations on any depth of data in a graph, but keeping text/strings behavior atomic is way more important than having built-in automatic string merges.
- 👀 Another example is, in our blog editing tools, despite having spent years researching & implementing (+ others in our community) precise character-by-character CRDT resolution schemes, I found I personally had a much better offline & local first user experience with a predictable per-paragraph sync scheme.
  - This is a stupid simple approach, but what it means is that I as a user, can easily predict whats going to happen, so if I'm offline I know I should just copy a new paragraph and fiddle with things there, cause it isn't gonna get "auto delete regrammar merged".
  - Generally speaking, me and colleagues don't "fight" over the same paragraph, we're usually concurrently writing different "sections" at the same time, it is pretty rare to grammar fix their edit same paragraph as they're typing it - that is also just kinda, rude looking.
- 👉🏻 Anyways, finally, is that the majority of text styling and DOM edge cases can be handled by having a deterministic canonical DOM hierarchy that always gets applied at the editing layer, BEFORE any CRDT operations even occur.
  - So for instance, re-arrange the DOM tree such that `<i>` is always inside `<u>` inside `<b>`, or something like that.
  - We built this into a library called normalize, and it instantly eliminated so much complexity, especially at the CRDT level. Ping me if you want a demo of this library.
- Finally, for everyone else, we also built an INTERACTIVE CARTOON EXPLAINER of an extremely basic text CRDT to help others understand the more detailed concepts
  - [Dependent Causality](https://gun.eco/explainers/school/class)
- Do you have any document that explain what resolution algorithm uses in what cases? For example, one peer change a property value and the other peer deletes it.
  - https://gun.eco/distributed/matters
  - It is a vector + timestamp + lexical sort/rank/order(字母顺序排序).
  - A delete is changing a value to `null`, it would lose (I assume you are asking if/when these 2 changes happen at the exact same microsecond time, conflicting?) as is it has a lower lexical rank.

- 🤔 Is the article suggesting to apply a string CRDT to an entire JSON structure? Are people doing that?
  - 👉🏻 No, the state of the art CRDT solution for json is something like Automerge that treats the document like a collection/combination of CRDTs of different types.

- In OT, every user action is broken down into one or more operations. These operations are transmitted between clients along with their baseline reference; if two users perform actions at the same time, incoming operations must be transformed to include the local operations that have happened since that baseline. They are then applied locally and form the new baseline.
  - This constant transformation of operations turned out to have too many edge cases where clients were found to not produce the same baseline (the "wrong" papers above). When that happens, the clients will never converge on the same result and break the fundamental assumption of collaboration.
  - exactly right. It’s fairly easy to have an OT system that is very vulnerable, because clients can cheaply generate change sets that are extremely computationally expensive on the server side. I’ve seen a system where a single mobile phone could, in a few seconds, lock up the synchronisation server for days.

- ## 分享我设计的基于CRDT的软件架构 hamsterbase
- https://twitter.com/hamsterbase/status/1590005075581497344
  1. 以 CRDT 文件作为 single source of truth, 保证向前向后兼容。
  2. 以 sqlite 数据库作为缓存。 sqlite 的数据库格式可以按照需求任意设计，可以随意修改。
  3. 不同客户端直接通过点对点同步 CRDT 文件，支持完全离线可用，同步无冲突。
- 数据库的crdt同步怎么设计的
  - 一个网页对应一个 CRDT 的文件（类似于 JSON）
  - 每次同步的时候，获取对方的文件列表、本地的文件列表
  - 对列表进行 DIFF, 发送本地多的，拉取本地少的。

- 你可以在本地跑 hamsterbase 试试看。 文件结构都在本地的
  - 可以把文件的版本号放在前面，这样可以在不读取完整文件的情况下获取当前的所有 CRDT 文件。

- 可以把 CRDT 同步抽象出来，同步服务不需要关心 CRDT 的格式
  - 这个是我从零设计的。 CRDTSyncDir 可以用 webdav , fs , oss , http 实现。 
  - 每次同步就是拿本地 fs 实现的 dir 和 http 实现的 remote dir 同步。

```typescript

interface CRDTSyncDir{
  listAllFiles();
  fileStat(id,version)
  listVersions(id)
  getVersion(id)
  read(id,version,filter)
  write(id,content)
}

```

- ## I've begun building out a server tick rate for message sending in Tiny Merge._202211
- https://twitter.com/JungleSilicon/status/1597770904716865538
  - 轮询：Starting out with 30 messages per connection per second.
  - I'm thinking I'll eventually move to something like a minimum send rate and a maximum depending on activity.

- we should talk more, I'd argue for pull-based with some good use cases there.
- I think it depends on the kind of application you're building. 
  - For real-time applications like a game a tick-rate would be more ideal. 
  - For something like a notion or linear something pull-based could be more ideal.
- ooh yeah, I think about modern multiplayer techniques there and I agree with that.
  - rollback-based multiplayer I think is what I'm thinking of there.

- ## Building the first Byzantine Fault Tolerant JSON CRDT
- https://twitter.com/_jzhao/status/1594732151400189953
  - A deep dive into what CRDTs are, how CRDTs are different from traditional consensus, what makes them tick, and how we can adapt them to tolerate malicious actors
  - [Building a BFT JSON CRDT](https://jzhao.xyz/posts/bft-json-crdt/)
- https://github.com/jackyzha0/bft-json-crdt /202211/rust
  - the first JSON-like Byzantine Fault Tolerant CRDT in Rust

- ## If anyone has been curious about how to build a CRDT but thought the idea was too daunting. tiny-merge-legacy_202205
- https://twitter.com/JungleSilicon/status/1526123548753858560
  - I've created one with as much of the complexity stripped out as I could whilst keeping it useful.
  - I call it Tiny CRDT.
  - Refactored it by separating the ram from the crdt & added a sequencer.

- https://github.com/siliconjungle/tiny-merge-ts
  - A Tiny CRDT library.
  - I converted the trimmed-down version of Tiny Merge to Typescript and swapped the objects out for maps.
  - https://github.com/siliconjungle/tiny-merge-ts/tree/feature-rich

- https://github.com/siliconjungle/tiny-merge-legacy
  - A tiny CRDT implementation in Javascript.

- ## The main trade offs between history and state based CRDT's is this:
- https://twitter.com/JungleSilicon/status/1559749305467957248
- History:
  - More capabilities (rewinding time, more complex merging logic).
  - Requires more storage.
  - Can have smaller network messages.
  - Is more complicated.
- State:
  - Simpler.
  - Less capabilities.
  - Less storage required.
  - Larger message sizes (especially on connect).

- ## It's becoming really clear that CRDT's become much more powerful and easy to reason about when you break them down into their tiniest pieces.
- https://twitter.com/JungleSilicon/status/1525515082876063750
  - Below I've separated where values are defined from the keys that reference them. This separation allows you to easily modify the data and change which keys point to which data in memory.
- https://github.com/siliconjungle/reference-crdt
  - An implementation of CRDT object references.

- ## I made a simple list CRDT that only supports push and replace operations. (No inserts before the end).
- https://twitter.com/JungleSilicon/status/1511523633294094337
  - It requires no history and is extremely light-weight. Useful for things like message histories or posts.

- ## The future of apps is local-first and CRDTs
- https://twitter.com/AdventureBeard/status/1495973698846736387
  - [Local-first software](https://www.inkandswitch.com/local-first/)

- ## Peritext: a CRDT for rich text collab

- https://twitter.com/geoffreylitt/status/1463244227412824066
- It's a data structure for async collaborative editing of rich text documents. 
- I believe the tools we use to collaborate can deeply shape the outcomes.
  - Real-time writing tools like Google Docs are an incredible step forward from emailing files, but they do promote a very specific workflow: "one live doc", that everyone is editing at the same time
  - This is fine for light docs, but in my experience it's not great for serious writing, like an essay or academic paper.
  - I want private calm space to try out edits; I want to suggest changes and discuss them as a batch... I want version control; "one live doc" is not enough! 
  - BTW, if you've ever developed software, you're probably familiar with the benefits of version control and branching workflows--maybe overkill for a tiny solo project, but indispensable for serious collaborative work.
- collaboration algorithms underpinning services like Google Docs are generally designed with "one live doc" in mind, not async collaboration. 
- So that brings us to this project.
  - CRDTs are a kind of data structure that allow people to asynchronously make local changes, and then merge those changes back together when people are ready to sync. 
  - The thing is, there has been a _ton_ of research on CRDTs for plain text, but barely any on rich text... which is essential for real writing.
- So that brings us to Peritext: a CRDT for rich text.
  - We've tried to pin down how async edits on rich text should be merged in a bunch of example cases, and proposed an algorithm that just always does the right thing.

- Circa 2012, I did CRDT rich text along the same lines. Compared to your case, I cut some corners though. 
- https://twitter.com/gritzko/status/1463404022212304898
  - Regarding the performance, the key trick was to use paragraph ids along with character ids (paragraph id is the id of the '\n'). Paragraphs/lines have manageable size, can put them in a hash table, then just scan them.

- Any thoughts on how @ProseMirror does this ?
  - One difference is that Prosemirror's collaboration system is designed to work with a single central server, whereas CRDTs are designed to work in distributed settings without a central authority.

- https://twitter.com/geoffreylitt/status/1463291185032679425
  - In my view the main problem with non-realtime merging is that undesirable merges (which any algorithm will sometimes produce) are harder to notice, so you'll want some kind of interactive UX that detects and points out potential conflicts to the user.
  - I'm curious, does Prosemirror's OT system have a notion of conflicts? We currently just arbitrarily resolve conflicts, but our approach would support detecting + showing conflicts a different way
  - Would also love to chat more sometime about Prosemirror's OT and understand better. It seems like key differences are:
  - 1) CRDT works in distributed setting, as you note (if you care about that property)
  - 2) It seems more straightforward to me to reason about correctness of CRDT w/ char IDs and commutative ops, than position mappings and rebasing operations. But that's subjective and I'm curious if you agree
- That's definitely true wrt to OT that supports reordering, but dumbed-down OT where every client ends up applying the operations in the same order converges pretty much trivially, and is not hard to reason about.
  - That being said, there's definitely advantages to adressable tokens, if you can afford the general conceptual complexity it introduces

- https://twitter.com/simonw/status/1463352229746786307
- I'm really excited for one with robust JavaScript and Python libraries that's well suited to using SQLite as the backend data store - I want to build a collaborative editor on top of Datasette which supports offline editing that can be merged back in when the client reconnects. Basically I want to build my own version of Apple Notes, crossed with Google Docs, crossed with a Markdown wiki
- Interesting! Offhand, **maybe could store/sync a SQLite table storing the history of CRDT operations, and replay that into a text doc format?** Although that table would get fairly large, and wouldn't get the benefit of a custom file format to compress down at all
  - That's pretty much what I want to do - I figure I can have a table of operations and every 10 days or so compress it down to a single savepoint and start building up the operations again to avoid size problems
  - Yeah seems sensible, and not much of a loss if you rarely have edits come in on top of a really stale version

- ## if you were building a collaborative web application today, you'd use_202109
- https://twitter.com/tmcw/status/1433436431658196997
  - automerge or yjs
  - replicache
  - ot
- going down this rabbit hole again today. it's been a mental block because the lock-in for these systems is so big - you're replacing state management, rewriting all of the places you transform your application's data, etc. i've been collecting notes
- i'm no longer considering yjs or gun, because they require transforming data back to native js structures for things like 'updating the map' - similar feeling to using immutable.js
- automerge's removal of built-in undo/history in the 1.x branch i think also removes it from the running, because history is sort of more important than collaboration for my usecase and i don't want a redundant history implementation. OT with immer might be the way.
- an oversimplified gist here is that "ot is theoretically inferior, practically superior, and not P2P, but you probably, unfortunately, aren't building true P2P"
  - a sicko approach i'm considering is to write application logic _as_ json patches instead of generating them.
- I'd use @CroquetIO where the data is only processed client-side but you still get to write server-like code (it's not a database, OT or CRDT).
- i picked OT but with a hefty dose of “other”. my biggest problem with all the frameworks in the poll is that they are javascript on the server side. that’s a show-stopper for me; i’ve found it a major pain to build stuff beyond PoCs in node.
  - replicache is implementable in whatever language you want, though tbh i am using all typescript on the server because it's what's comfortable
- CRDTs, we make collaborative apps for the maritime industry where internet is very bad and intermittent... everything needs to work offline and reach consensus on state without coordination and with minimum amount of data transfer
- I think it's application specific which is the right answer.
  - OT/CRDT when you really have multiple clients manipulating the exact same block of data at the same time and you can't represent the work as deltas to stream to a data owner.
  - It does happen, but rarer than you think.

- natto: I feel this pain going from nothing -> yjs -> hybrid replicache. one thing that I'm happy with is having a unified subscription and mutator interface so it's easier to make these changes
  - i'm intrigued(好奇的), what makes your replicache setup hybrid? so far i like replicache but totally missing the low-boilerplate bliss of @blitz_js 's query/mutation system
  - it's hybrid in that there are two types of natto canvases. 
  - "browser drafts" (single-player local-only) don't use replicache. 
  - "user canvases" (ugh - synced to server) use replicache.
  - mutators are implemented 3 times.. twice on client (one for local-only mode, one for client replicache) and once on server for persistence (replicache)
  - but if i want to switch to yjs or something else, i can just swap out the implementation of the mutators and subscriptions in a single file.

- ## Great writeup by @josephgentle on making CRDTs orders of magnitude faster. 
- https://twitter.com/martinkl/status/1423230479222939648
  - [5000x faster CRDTs: An Adventure in Optimization](https://josephg.com/blog/crdts-go-brrr/)
  - We're working on a similar approach for Automerge, and it's encouraging to see how much performance improvement is possible!
- Are either of you aware of any efforts to make CRDTs based on 3-way merging? Like a self pruning git history, with peer branches, retaining only the bare minimum of common ancestors to support future merges?
  - https://gowthamk.github.io/docs/mrdt.pdf

- ## every collaboration tech that i'm seeing is either: closed-source, limited to small data, limited to text-like data, inefficient, or all of the above
- https://twitter.com/tmcw/status/1422934838873571342
- replicache is [open-source](https://github.com/rocicorp) but not free. Their approach is giving you a spec to implement for the backend; they're not hosting anything for you. I also think approach handles scale pretty well because it doesn't keep history like some CRDTs
- Very hard to build a generic collab tech without diving into the domain. 
  - Text editing collab has requirements like intent preservation while drawing, say, requires lots more data shipped around. 
  - And CRDTs eschew(回避，避免) centralization but very few apps don’t need authority.
  - And if you to ship a lot of data, say megabytes, you basically need something like a CAS (like git for binaries), which means you need to remember all the hierarchy of files and/or do things to actually separate content to its data/metadata
  - Gaming is instructive here. Every type of multiplayer game has diff strategies. Some send pure inputs from the clients, others do a lot more simulation locally and most do a bit of both, depending on the game and reqs(RTS, FPS, cheating) And it’s never good enough!
- The best examples I can think of violate #1 (game server architectures), and they are generally written custom for every game, or at least every studio/franchise. Even Unity has very limited support for a generic solution, despite being a slam dunk feature.

- ## Why CRDT didn't work out as well for collaborative editing xi-editor _201905
- https://news.ycombinator.com/item?id=19886883
- TL; DR 
  - CRDT is completely irrelevant to any of the highlighting/etc stuff
  - Most highlighters are lexers. Advanced highlighters/folders are parsers.
  - The lexing/parsing that is required for highlighting is easy to make incremental for all sane programming languages.
  - for LL(star) grammars, adding incrementality is completely trivial (i sent patches to ANTLR4 to do this)
  - for LR(k) grammars, it's more annoying but possible (tree-sitter does this)
  - For lexing, doing it optimally is annoying, doing it near optimally is very easy.
  - optimal incremental lexing requires tracking, on a per token basis, how far ahead in the character stream the recognizer looked (easy), and computing the affected sets (annoying)
  - Most real programming languages have a lookahead of 1 or 2. Near-optimally requires tracking only the max lookahead used, and assuming all tokens need that max-lookahead. In a world where min token length is 1, that means you only need to re-lex an additional (max lookahead) tokens before the changed range. In a world where min token length is 0, it's all zero length tokens + (max lookahead) tokens before the changed range. This does not require any explicit per-token computation.
  - Again for basically all programming languages, this ends up re-lexing 1 or 2 more tokens total than strictly necessary.
  - Tree-sitter does context-aware on-demand lexing. i have patches on the way for ANTLR to do the same.
  - The **only thing CRDT helps with in this equation at all is knowing what changed and producing the sequence of tree-edits for the lexer/parser**.
  - The lexer only cares about knowing what character ranges changed, which does not require CRDT. The typical model for this kind of edit is what vscode's document text changes provide (IE For a given text edit, old start , old end, new start , new end)
  - **The parser only cares about what token ranges changed, which does not require CRDT**.

- ## more-discuss
- Open source collaborative text editors _201905
  - https://news.ycombinator.com/item?id=19845776
- An Introduction to Conflict-Free Replicated Data Types _202006
  - https://news.ycombinator.com/item?id=23737639
- CRDTs: The Hard Parts [video]_202007
  - https://news.ycombinator.com/item?id=23802208
