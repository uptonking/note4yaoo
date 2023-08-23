---
title: lib-collab-crdt-community-stars
tags: [collaboration, community, crdt]
created: 2021-11-24T17:08:48.275Z
modified: 2022-04-05T10:09:51.343Z
---

# lib-collab-crdt-community-stars

# guide

 

- resources
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 💡 You can move CRDT data over whatever data layer you have on hand, and insert them into whatever data stores you want. 
- https://news.ycombinator.com/item?id=30984776
  - Care for the special **semantics of CRDT are only needed when merging CRDTs**, storage and transportation is like any other encoded format, like moving a JPEG encoded image over HTTP, or storing a JPEG as a byte stream in a database. 
  - Neither the HTTP client or the database need to know how to turn the JPEG bytes into screen pixels.
- Here’s a possible design for a CRDT editor system:
- Browser client composes a CRDT locally in-memory, and saves the CRDT data into IndexedDB periodically as a Blob of bytes.
- When the client is online, it periodically performs a sync with the server using HTTP, with this protocol:
- This scheme is not optimally efficient, but shows that you can put together a CRDT system with a normal database and a bit of HTTP.
- See https://docs.yjs.dev/api/document-updates#syncing-clients for more info on how Yjs (the most production ready library) handles these concepts.

- Yep. I've done something very similar on top of Diamond Types for a little personal wiki.

- ## [JSON CRDT 2.0](https://github.com/streamich/json-joy/issues/228)
- Things to consider:
  - Move operations across different document nodes.
  - Low-level multi-value register support. (MV register can be done in user-space using an RGA array.)
  - Currently, JSON CRDT is operation-based CRDT. Consider if it also should work as state-based CRDT and delta CRDT.

- ## [What do you recommend for conflict-free replicated data type (CRDT) support in Rust?](https://www.reddit.com/r/rust/comments/1064f9s/what_do_you_recommend_for_conflictfree_replicated/)
- you may find the hybrid logical clock approach more convenient than trying to maintain and manage a vector clock etc...

- I think CRDTs are the correct solution here. Another Rust-based offline-first CRDT framework is Holochain. It frequently gets mistaken for blockchain due to the name and its proximity to that space, but it is not a blockchain in any way

- ## Has anyone seen a good comparison between @partykit_io @liveblocks @replicache ?
- https://twitter.com/ptsi/status/1676064189385785344
- I've used @liveblocks and the DX is insane with zustand which my projects previously used. But it's very expensive. I think pricing is fair for enterprise products but hard to do for freemium.
  - @partykit_io sounds cool too, but never tried that... 
  - @replicache sounds more of like a sync-changes between clients thing than a instant-collaboration toolkit
- I have played around a bit with replicache and pusher, but it can be slow at times. 
  - Partykit looks interesting, but docs always seemed scant(不足的，缺少的). It’s built on cloud flare objects. y-partykit is built on yjs. 
  - Liveblocks is pretty well documented and widely used. Hugging Face uses it.
  - Live blocks can get expensive quickly. Replicache has very good docs. The way it can merge/conflict resolve is useful. I’m a yjs self roll it fan tbh.
  - I believe Liveblocks can do conflict resolution as well. Also of note is automerge if you are more into the roll it yourself yjs camp. Replicache can be used with whatever popular backend you like, postgres/mysql/couch included so you aren’t required to use their hosted service

- ## I was blown away by @aboodman 's talk and the Replicache model 
- https://twitter.com/tantaman/status/1664635160984272896
  - so I spent the last day experimenting with a variation on the idea: "Creating CRDTs without specialized knowledge"
- Glad to think about the CRDT version of this idea so more. I had forgotten but there are actually a few implementations of it. One of the key challenges I think is enforcing determinism.
  - https://tanglesync.com by @kettlecorn does this by running in a wasm container that controls indeterminism.
  - There was another product awhile back -- I swear it was called parquet -- that did the same thing by running JS in a special environment that controlled indeterminism. But now I can't find that product.
  - You're thinking of https://croquet.io/
- AssemblyScript, for mutations, might make the wasm container route bearable.

- ## GPT-4 as a viable alternative to text CRDTs? 
- https://twitter.com/geoffreylitt/status/1645961623289438208
- Yes I think this is promising for async merges!
  - Probably still want tools to review what it did, but in simple cases like this can just be a ✅
  - Auto-merging code seems easier than prose since easier to verify...
- For more synchronous workflows you probably still want something fast and deterministic, but CRDTs are already good at that part; it's these "semantic merges" that are harder

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

- ## The future of apps is local-first and CRDTs
- https://twitter.com/AdventureBeard/status/1495973698846736387
  - [Local-first software](https://www.inkandswitch.com/local-first/)

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

# discuss-more
- Open source collaborative text editors _201905
  - https://news.ycombinator.com/item?id=19845776

- An Introduction to Conflict-Free Replicated Data Types _202006
  - https://news.ycombinator.com/item?id=23737639

- CRDTs: The Hard Parts [video]_202007
  - https://news.ycombinator.com/item?id=23802208
