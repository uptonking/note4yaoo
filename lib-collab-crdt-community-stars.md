---
title: lib-collab-crdt-community-stars
tags: [collaboration, community, crdt]
created: 2021-11-24T17:08:48.275Z
modified: 2022-04-05T10:09:51.343Z
---

# lib-collab-crdt-community-stars

# guide

 

- resources
# discuss-crdt-event/log
- ## 

- ## 

- ## CRDTs can _technically_ represent any computable data structure. Informal proof:
- https://twitter.com/paulgb/status/1720865931243504039
  - Every data structure can be represented as a sequence of mutations starting applied to an initial value.
  - Put those mutations in a list CRDT, then apply them in the same order on every client.
- Some data structures have mutations that are only valid in certain states (for example, deleting item 8 in a 4-item list is an error). Simply treat these as a no-op.
  - This is not generally a good idea! The performance is not good and it does not preserve intent well. But it is useful to understand when thinking about CRDTs that need to maintain invariants (like a tree CRDT), since they implicitly do something like this in disguise.
- Transactions could either be combined into one mutation or transaction start and end could be represented as mutations of their own. You could guarantee that a transaction is all-or-nothing, but not that a transaction could not be undone.
- does a crdt guarantee ordering of mutations?
  - The mutations that go in to a CRDT are unordered, but a list CRDT can turn them into an ordered list. The trick is to combine that ability with the fact that every data structure can be represented as a state machine.

- yeah!! have you seen @martinkl 's work on OpSets which explores this? I find it to be a really elegant way to think about CRDT behavior independent of performance

- ie: As long as you maintain a newtonian(牛顿学说的) absolute time for all observers, changes can be viewed in an absolute way

- ## 💡 This confluence of things is going to unlock some stellar new infrastructure.
- https://twitter.com/tantaman/status/1715046327892025526
  - Event sourcing
  - CRDTs & Causal Graphs
  - Incremental View Maintenance
  1. Event source your entire app.
  2. Incrementally maintain app state as a view of events.
  3. Rebase events for multiplayer.
- I'm experimenting with this stuff - I believe that massively scalable multi-master even stores could be implemented with an append only log and some kind of index of event ID -> index-in-log. The index could just be resident in memory too.

- 🤔 Any thoughts on compressing the log? People have made a ton of progress in terms of compacting sequence crdt event logs. Not sure about generic event logs.
  - I do feel as if history pruning would go against event sourcing though. Compaction makes a lot of sense - probably for events that have gone offline? (IE not accepting any more writes for last years events... following businesss rules).
- Abtimatter is interesting since it finds history that doesn’t matter and can be dropped even if peers never saw it and things still converge to the same state without those events.
- Ideas for log pruning exists almost from the very beginning. The problem is always the same - you need to be able to restrict the set of writers or deny concurrent updates.
- No I just naiively assume storage will keep getting better and it's fine

- ## 🌰 [Show HN: fuzzynote - CRDTs+WASM for local-first, collaborative note-taking in the browser | Hacker News_202204](https://news.ycombinator.com/item?id=30904405)
- A little while ago I shared the terminal based version of the project (https://github.com/Sambigeara/fuzzynote /golang) with the community. I since got inspired, and disappeared into my loft for 9 months to work on leveraging the core logic for use in a WASM-based web client. So you can now sync your notes between your terminal and any reasonable modern browser (some early limitations in mobile)!

- https://twitter.com/fzn_sam/status/1578782505792143363 _202210
  - New tree CRDT is live, sync is an order of magnitude faster, and it now loads on iOS again
  - Next, complete revamp of sync algo for more efficiency gainzz (and infra cost reduction)
  - For anyone curious about the tree #CRDT implementation, it's here
    - https://github.com/Sambigeara/fuzzynote/blob/main/pkg/service/tree.go
  - The hardest bit was supporting "move" operations. Wreaks havoc.

- What CRDT library are you using? Or is this something new?
  - I built this one myself, it's an event log which is used to progressively build onto a secondary data structure (which is more closely tied to the client)

- Did you implement CRDTs manually or depend on yjs?
  - Manually! The CRDT itself is an event log. The client state is built from a secondary data structure which replays from the log (the extent of the "replay" determined by how much data needs to be merged etc)

- What's the worst edge case you're aware of that you're not handling?
  - It's probably not even an edge case (dependent on usage), but a limitation right now is that **a unique "unit" of collaboration is a single item/line**, so if two people update a line offline, the winning line will the most recently updated. I can imagine that would get pretty annoying pretty fast. Granular collaboration (updating per character rather than per line) is on the backlog, priority will be determined by feedback of course.
  - Another thing to solve is **ever-growing data sets**. I've tinkered with some mechanisms to combat this (namely compacting the CRDT event log based on a bunch of rules) but this is tricky and I'd prefer the app to mature a little before I implemented this. Also on the backlog! Lots to do for sure.

- ## [Lasp: a little further down the Erlang rabbithole | Hacker News_201705](https://news.ycombinator.com/item?id=14300763)
- My favourite thing about CRDTs (and event sourced data in general) is that they force us to consider the meaning of time and order as it relates to information.
  - When handled with clarity of thought there are flow on effects in correctness of processing
  - 🐛 The downside is that popular frameworks don't mesh well, or at all, with this paradigm. Trying to shoehorn(强挤硬塞) event-based data into say, Rails (which I've done), is an frustrating exercise in resolving massive impedance mismatches and growing technical debt. 
  - Turns out most database-driven MVC frameworks have a very limited understanding of time and order.
  - CQRS helped here, because I realised that my MVC can and should just be a view & query layer, and I should be building the event sourced/CRDT-based logic elsewhere.
- I've found that many of the modern JavaScript UI libraries play very well with event sourcing, IMHO. 
  - React and Vue.js in particular work very well when combined with Redux/Vuex and a CRDT database. 
  - Both of those stores are essentially event sources themselves, where the actions and mutators are separated and the data store itself is updated only in one place. 
- 🔀🤔 What CRDT databases do you use in this sort of application?
  - Currently leveraging CouchDB and it's incremental map-reduce to handle the "CRDT" merging of an event stream. 
  - Technically I'm not using a CRDT library or DB, but it's surprisingly easy to implement the core "commutative operations" of CRDT's via a modified deep-merge versioning algorithm.
  - Works pretty well as I can deploy 20, 000+ user interactions on an embedded CouchDB instance with steady performance.

- ## 🆚️🧮 Here's a visual comparison of the data structures underlying three different "collaborative text editing" algorithms.
- https://twitter.com/jaredforsyth/status/1232532781936173056
  - [yjs vs automerge vs rga](https://text-crdt-compare.surge.sh/)
  - yjs uses a doubly-linked list of nodes
  - mine(local-first-rga) uses a tree
  - automerge uses a transaction log (and has in-memory caches for perf)
- Your approach seems to resemble RGASplit which I believe is bases for

# discuss-gc
- ## 

- ## 

- ## [A highly-available move operation for replicated trees | Hacker News_202203](https://news.ycombinator.com/item?id=30811072)
- Question for the authors (if they are around): any ideas for how we might get to efficient pruning of old operations? I don't have any ideas. Do you all have some idea of how we might be able to prune this old log? Or even sketches of ideas?
  - The authors actually do briefly mention this concern in the section titled 3.7 Algorithm extensions (under Log truncation):
  - > However, in practice it is easy to truncate the log, because apply_op only examines the log prefix of operations whose timestamp is greater than that of the operation being applied. Thus, once it is known that all future operations will have a timestamp greater than t, then operations with timestamp t or less can be discarded from the log.
  - The main issue seems to be that we need to know about all the replicas that we want to be able to synchronize with - but I guess there isn't really a way around this.
- You're right that in order to ensure that you won't receive timestamps lower than some threshold, you need to know all the nodes in the system, and you need to hear from all of them (if even just one node is unreachable, that will be enough to hold up the process). That's quite a big assumption to make, but unfortunately there doesn't really seem to be a good way around it. Lots of CRDT algorithms have this problem of requiring causal stability for garbage collection.
  - Using a consensus protocol is possible, and would have the advantage that it only requires communication with a quorum (typically a majority of nodes), rather than all nodes. However, it has the downside that now a node cannot generate timestamps independently any more — generating a timestamp would then also require a round trip to a quorum, making the algorithm a lot more expensive.

# discuss-stars
- ## 

- ## I’m wondering if we can have best of both worlds (“plain text interoperability” + crdt versioning metadata
- https://twitter.com/YousefED/status/1770364932334260257
- automerge member: I don't see how? like yjs+filesystem?
- most approaches that do this sort of thing are lossy and beed to do diffs to convert into ops.

- ## OT & CRDTs (with history) are great for most data types, but don't really make sense for supporting arbitrary binary file formats (as there are *so many*). 
- https://twitter.com/JungleSilicon/status/1738332065777738092
  - The diffs between them end up *huge* and aren't realistic to store in a causal tree. 
  - How would you approach this?
- Some ideas come to mind:
  - Lower resolution snapshots for binary files (e.g. git or checkpoints).
  - Try to crowdsource transformers for each binary file type that can convert the binary file formats into diffs which are better suited to a history of changes.
  - Store the *version history* of binary files but ignore their values, only store the latest value for them.

- Multi-value registers don't solve any of this? This thread is about the sheer amount of data necessary if you want a history of binary files.
  - Causal tree's often use multi-value registers.

- You could use a rolling hash like bup

- Content addressing, versioning, and partial sync

- ## Slapping(~on添加) a CRDT on something isn't enough to make a truly collaborative or offline friendly app. 
- https://twitter.com/c_pick/status/1716827138253529578
  - CRDTs can make your app consistent, but consistently wrong if you're not preserving user intent. This is nowhere near a solved problem yet, the general case might never be solved!
- We don't need a perfect solution for general cases. We just need a good enough one and allow users to resolve conflicts manually when the default merge result is unsatisfactory. So, the worst case is to fall back to something like git.
- Counterpoint(形成对比的论点): I’ve supported more peer-to-peer database applications in prod than almost anyone out there. Only a handful of times did conflict resolution strategies have to be proactively(积极的; 主动的) coded. Getting document granularity right is most of the work.
- Having built on top of crdts quite a bit, I think that the replicache model is probably the more explicit, better abstraction. It's very clear what effect concurrent edits will have as you write reducers and very hard to model the same with crdts without simulation.

# discuss-crdt-db
- ## 

- ## It is relatively easy to turn any LSM databases ( @cassandra , @LevelDB , @RocksDB , Pebble of @CockroachDB ) into mutually compatible syncable CRDT databases
- https://twitter.com/gritzko/status/1777966931804631387

# discuss
- ## 

- ## 

- ## 

- ## 

- ## ⚡️ [Making CRDTs More Efficient | Hacker News _202310](https://news.ycombinator.com/item?id=37915934)
- OP implements their own RLE-based compression scheme. I bet you'd get better results from emitting an uncompressed binary format, and then passing the whole thing through a general-purpose compressor like zstd.
- General compression algorithms like zstd will do way, way better on previously encoded data. Sorting, RLE, etc, are all going to lead to a smaller resulting binary after going through the generalized algorithm.
  - You're also going to be relying on heuristics that may fail. Zstd has no idea that your UUIDs are going to repeat, it doesn't know to dictionary encode them or to create frequency mappings. What it ends up doing is unlikely to be as effective as doing the work ahead of time, then allowing zstd to find the interesting and complex patterns that arise out of your encoded format.

- Given equivalent data stored in both JSON and BSON format I would expect them both to compress down to blobs of roughly equivalent sizes. This is because both encode roughly the same amount of information, so the compression algorithm will tend to compress down to the same final result. I haven't run this as an experiment though..that would be fun.

- ## I think I will stop using the term "CRDTs".
- https://twitter.com/LewisCTech/status/1759148577174204815
  - I'm interested systems that can be written to w/o coordination and sync predictably. 
  - And every single one of those will obey the CRDT laws, whether they know the term or not. 
  - Amazon Dynamo obeyed those laws, but it predates the term.

- ## [What Is JSON Patch? | Hacker News_202205](https://news.ycombinator.com/item?id=31301627)

- 🌰 Last year I experimented with an app architecture that used CouchDB/PouchDB for for synchronising data for a single user, multi device app. Then using Yjs to merge the conflicting edits - it worked incredible well. If I had the time, I would love to build a Yjs/CRDT native CouchDB like database that could use the Yjs state vectors as a wire protocol for syncing…
  - This is the very rough code behind the PouchDB/Yjs datastore. Effectively each Pouch/Couch document is actually "managed" by Yjs, all changes/operations via it. It then saves the binary Yjs blob as an attachment on the Pouch document with the current Yjs state exported as JSON for the main Pouch document. This gives you all the indexing/search you get with Pouch/Couch but with automatic merging of conflicting edits.
  - 🧐 **Ultimately though I don't think PouchDB is a good platform for this**, building something that is native Yjs would be much better. If anyone is interested I would love to hear from them though!
- I'm also interested in following updates to your approach here. Something that stands out immediately to me is that reliance on binary attachments. 
  - 👉🏻 In my own CouchDB ecosystem work binary attachments have turned out to be just about the worst part of the ecosystem. 
  - PouchDB stores them pretty reliably, but every other CouchDB ecosystem database (Couchbase, Cloudant) including different versions of CouchDB itself (1.x is different from 2.x is different from 3.x in all sorts of ways) all have very different behavior when synchronizing attachments, the allowed size of attachments, the allowed types of attachments, the allowed characters in attachment names, and 😩 in general the sync protocol itself is prone(易于做某事；有做某事的倾向) to failures/timeouts with large attachments that are tough to work around because the break in the middle of replications. 
  - The number of times I've had to delete an attachment that PouchDB stored just fine to get a sync operation to complete with another server has been way too many already.
  - I've had to build bespoke(定制的) attachment sync tools because I haven't been able to rely on attachments working in the CouchDB ecosystem.
  - I've been thinking that I need to replace the CouchDB ecosystem as a whole. PouchDB is great, but the flux(一系列的变化；持续的变化) I've seen in the Apache CouchDB project and the issues I've had with the managed service providers especially Cloudant after IBM makes it really hard to recommend the ecosystem. Overall it seems unhealthy/in-decline, which is sad when the core sync infrastructure seems so nice to work with when it works

- ## [Conflict-Free Replicated Data Types (CRDT) | Hacker News_202204](https://news.ycombinator.com/item?id=30983770)
- CRDTs are pretty rad. They’ve been rad for years, and a lot of work has been done around them. Usually people find that there are simpler/better ways to get the job done. I think they’re better left as an implementation detail at this point.
- > Usually people find that there are simpler/better ways to get the job done.
  - CRDTs can do one magic trick no other technology solutions can do: They can let users collaboratively edit without needing a centralized server. And this works between users, between devices or between processes.
  - Its just, most of the time that doesn't matter. Servers are cheap, and big companies frankly seem to love it when we're dependent on their infrastructure.
  - I want CRDTs for more "personal computing". I want my data to be shared between my devices seamlessly. 
- You can always have an intermediary server with CRDTs is you want. They're just another peer on the network.
  - Yeah I'm aware - I got the impression from your comment you were advocating for a more pure P2P approach (not necessarily CRDT related).
- > Usually people find that there are simpler/better ways to get the job done.
- Here's all the ways I know for dealing with write conflicts in a distributed systems:
  - Last write wins, AKA I'm going to pretend I've solved the problem and just randomly lose data
  - Record all versions of the data, pick an arbitrary winner, store a revision, and surface it to the user if there's a conflict (the CouchDB strategy, I don't know anything else using this)
  - Model your data so it's append only (events, maybe) then merge just becomes a set union of all the different nodes
  - So including CRDTs, that's my general taxonomy of solutions to this problem. Are there more?
- CRDTs don’t quite fit in this list, as these are all valid merge strategies that a CRDT can use. The fundamental idea of a CRDT is that all of these schemes have something in common: They’re based on iteratively merging a bunch of versions together with a merge operator that fulfills a few basic properties Associativity/Commutativity/Idempotency/Closure. As long as your merge operator has all of these properties, you get the strong eventual consistency result that makes CRDTs a useful abstraction
- That part is clear to me. What's not immediately obvious is that the DT in a CRDT can be entire database. Certainly the focus seems to be on individual data structures within a data store.
- Slightly pedantic(学究式的；书呆子气的), but I think you'll actually find that all of these are CRDTs. If you read "Conflict-free Replicated Data Types: An Overview", it refers to both last write wins and "record all versions of the data" as CRDTs in 2.1.1. My understanding is that "CRDT" really just means that you've defined how you're going to resolve conflicts consistently (see criteria in s2.2 of the paper above).
  - Yeah it had occurred to me that what I'm doing was just a GSet write large. In my mind a CRDT was always a single record, not a collection of them - still not convinced that doesn't change it.
  - But if CRDTs really are a kind of a meta-language for resolving conflicts in a sane way - whether the CRDT is a single record or a whole data store - that's a nice thought. The CouchDB CRDT could be defined.

- ## 💡 I'm basically only interested in 3 CRDTs - g-sets, multi-value registers, and OR-maps whose values are multi-value registers. 
- https://twitter.com/LewisCTech/status/1715268425629716784
  - These are the core constructs for database syncing insofar(到这种程度) as I see it - the rest have applications in collaborative software.
  - To be clear - obviously syncing complicated stuff like relational databases needs a lot more sophistication. 
  - But the above 3 can be applied to someones existing NoSQL data solution in industry a lot more easily.
- But I want to apply CRDTs to playlist synchronization. I need support for arrays where the user defines the position of the items.

- ## 💡💡 You can move CRDT data over whatever data layer you have on hand, and insert them into whatever data stores you want. _202204
- https://news.ycombinator.com/item?id=30984776
  - Care for the special **semantics of CRDT are only needed when merging CRDTs**, storage and transportation is like any other encoded format, like moving a JPEG encoded image over HTTP, or storing a JPEG as a byte stream in a database. 
  - Neither the HTTP client or the database need to know how to turn the JPEG bytes into screen pixels.
- Here’s a possible design for a CRDT editor system:
  - Browser client composes a CRDT locally in-memory, and saves the CRDT data into IndexedDB periodically as a Blob of bytes.
- When the client is online, it periodically performs a sync with the server using HTTP, with this protocol:
  1. HTTP GET /doc/:id/stateVector - returns the latest state vector on the central server. A little analogous for checking the refs of a git remote.
  2. HTTP POST /doc/:id/push - send the difference between the state vector returned from (1) and the client’s local state to the server. This is kinda like `git push` .
  3. The server responds to (2) with the missing state on the client. It can compute this from the data the client sent.
- Inside the server, writes are handled like this:
  1. Start a RW transaction on a Postgres row containing the CRDT data.
  2. Read the data from the DB and merge it with the incoming data in the client post.
  3. Compute the update delta for the client
  4. Write the merged data back into the DB
  5. Commit.
  6. Respond with the delta computed in (3).
- This scheme is not optimally efficient, but shows that you can put together a CRDT system with a normal database and a bit of HTTP.
- See https://docs.yjs.dev/api/document-updates#syncing-clients for more info on how Yjs (the most production ready library) handles these concepts.

- Yep. I've done something very similar on top of Diamond Types for a little personal wiki. This page is synced between all users who have the page open. Its a remarkably small piece of code, outside of the CRDT library itself (which is in rust via wasm).
  - Code is here, if anyone is interested. The whole thing is a few hundred lines all up

- ## Stellar(优秀的；杰出的) example of the difficulty of maintaining global invariants with CRDTs. 
- https://twitter.com/tomlarkworthy/status/1660217410517979137
  - It's probably possible via a clever change of representation but if you have the option of a server authority, take it and save yourself the PhD work and keep the intuitive representation.
- Yeah, 100% I do think CRDTs are in a hype cycle and the enthusiasts will eventually have to reconsider that they are not a good choice for vanilla app development. They have unique strengths but huge drawbacks too so the problem has be matched for CRDTs to be the answer

- ## [JSON CRDT 2.0](https://github.com/streamich/json-joy/issues/228)
- Things to consider:
  - Move operations across different document nodes.
  - Low-level multi-value register support. (MV register can be done in user-space using an RGA array.)
  - Currently, JSON CRDT is operation-based CRDT. Consider if it also should work as state-based CRDT and delta CRDT.

- ## 🆚️ Has anyone seen a good comparison between @partykit_io @liveblocks @replicache ?
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

- ## @replicache does give you local-first state, but you provide the backend
- https://twitter.com/aboodman/status/1637192004441612288
  - Convex has the “you program via client side js and it’s reactive” like firebase, but it doesn’t “sync” in the sense of having local-first; offline accessible state afaik. 
  - Supabase same but with sql-based db
- Replicache works with anything w/ serializable transactions but the server-side reactive functions, builtin logical timestamps, and JS aspect of Convex should make it a tastes-great-together with Replicache
- Convex doesn't e.g. store pending mutations past closing the browser tab. You could do this in userspace (and maybe Convex will add this) but approaching the problem holistically, Replicache does it right.

- A terrific amount of work has been put into Replicache to do background sync + partial offline support Right

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

- ## 🌰🤔 [Why CRDT didn't work out as well for collaborative editing xi-editor _201905](https://news.ycombinator.com/item?id=19886883)
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

- ## [CRDTs: The Hard Parts [video] _202007](https://news.ycombinator.com/item?id=23802208)

- ## [An Introduction to Conflict-Free Replicated Data Types _202006](https://news.ycombinator.com/item?id=23737639)
