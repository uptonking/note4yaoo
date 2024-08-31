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
# 👥 [Faster CRDTs: An Adventure in Optimization | Hacker News _202107](https://news.ycombinator.com/item?id=28017204)
- About a decade ago, I implemented the Causal Tree CRDT (aka RGA, Timestamped Insertion Tree) in regular expressions using a Unicode string as a storage. Later we made a collaborative editor for Yandex based on that code. It used many of the tricks as described in the text, even the optimization where you remember the last insertion point. So I am terribly glad it all gets rediscovered.
  - https://github.com/gritzko/citrea-model
  - Recently I greatly improved CTs by introducing the Chronofold data structure 
  - CRDTs are fast enough, that is not a concern.
-  Do you have released a CT implementation in top of Chronofold? Have you any plans to benchmark it against other algs?
   - No, I didn't release it, although there are implementations on GitHub. Rust and Kotlin, at least. The RON proof-of-concept wiki runs on the (unreleased) C++ implementation. I benchmarked it at some point, everything was like "k nanoseconds" 

- Problem is that academics are rarely experts at programming or have knowledge of computer architectures as much as someone in the industry.

- Benchmarking papers are inaccurate when the original algorithms are not open sourced

- Have you seen my Xi CRDT writeup from 2017 before?
  - It's a CRDT in Rust and it uses a lot of similar ideas. Raph and I had a plan for how to make it fast and memory efficient in very similar ways to your implementation. I think the piece I got working during my internship hits most of the memory efficiency goals like using a Rope and segment list representation. However we put off some of the speed optimizations you've done, like using a range tree instead of a Vec of ranges. I think it also uses a different style of algorithm without any parents. We never finished the optimizing and polished it up, so it's awesome that there's now an optimized text CRDT in Rust people can use!

- Some optimizations whom you discuss are already proposed by some papers and implementations.
  - LogootSplit proposes an implementation based on an AVL tree with extra metadatas to get a range tree. LogootSplit proposes also a block-wise approach that stores strings instead of individual characters. 
  - Xray, an experimental editor built by Github and written in Rust, uses a copy-on-write B-tree. 
  - Teletype uses a splay tree to speedup local insertions/deletions based on the observation that a user performs several edits on the same region.
- And I'm not surprised these techniques have been invented before. Realising a tree is an appropriate data structure here is a pretty obvious step if you have a mind for data structures.
  - Its hard to compare their benchmark results because they used synthetic randomized editing traces, which always have different performance profiles than real edits for this stuff. 

- This is still hard for me to determine when position-based list CRDT (Logoot, LogootSPlit, ...) are better than tombstone-based list CRDT (RGA, RgaSplit, Yata, ...). It could be worth to assess that.
  - 3 year ago I started an update of LogootSplit. The new CRDT is named Dotted LogootSplit and enables delta-synchronizations. From an engineering point-of-view, I'm using a partially-persistent-capable AVL tree. Eventually I would like to switch to a partially-persistent-capable b-tree.

- > Today, it seems one would still have to transform that data to a large flat string underneath, and implement an editor that only performs edits that maintain the integrity of the higher-level object, while the flat string provides collaboration features.
  - Lots of people think this and have mentioned it over the years, but its a dangerous idea. The way concurrent edits are handled makes it really easy for the automatic merging algorithms to mess up the syntax of your XML / JSON content. And thats really hard for non-programmers to fix.
  - The right answer for this stuff is to just make CRDTs which support other data types, the same way we did for OT with ot-types
  - We need CRDT code for lists + text (working now - text is just a list of characters). And rich-text and JSON.
  - Yjs and automerge already do this. They have support for plain text, XML and arbitrary JSON structures.
  - The simplest implementation for JSON structures + tuples is probably shelf, which is so simple you can implement it in about 25 lines of javascript. Shelf doesn't support lists, but combining shelf with the list code I already have in diamond-types is probably going to be good enough for most applications.

- I've been looking for a practical OT alternative for our online word processor (https://zoho.com/writer). We already use OT for syncing our realtime edits and exploring CRDTs targetting stronger consistency for tackling offline edits (which are typically huge & defragmented, since the edits are not syncing in realtime)
  - So the baseline is that OT has a better model for holding state in terms of performance/memory, since the edits can be compiled into plain string types. CRDTs in comparison forces us to hold deleted states as well and demands richer information per unit (character/string/etc) - which makes it harder on the CPU/RAM.
  - Here's the story as I understand: 1. Automerge tackles this by just moving to a better lower-level runtime: Rust. 2. Yjs handles this by using a similar technique i.e relying on V8's hidden classes to handle the performance optimizations and assuming real-world cases to narrow down and optimize datastructures.
  - But none of these, seem to be a fundamental breakthrough in the efficiency of the algorithm itself. They all at best look like a workaround and this keeps bothering me.
- If you've got big offline edits (or you're merging multiple large sets of edits), even existing CRDTs will generally handle that more efficiently than OT will. OT algorithms are usually O(n * m) time complexity when merging n edits from one peer with m edits from another peer. A CRDT like diamond-types is O((n + m) * log(s)) where s is the current size of the document. In practice its super fast.
  - As for holding deleted states and richer information per unit, its not so bad in absolute terms. 1-2mb of data in memory for a 17 page document is honestly fine. But there's also a few different techniques that exist to solve this in CRDTs:
  - 1. Yjs supports "garbage collection" APIs.
  - 2. Sync9 has an algorithm called "antimatter" which mike still hasn't written up poke poke mike!. Antimatter actively tracks the set of all peers which are on the network. When a version is known to have been witnessed by all peers, all extra information is safely discarded. 
  - 3. Personally I want a library to have an API method for taking all the old data and just saving it to disk somewhere. The idea would be to reintroduce the same devops simplicity of OT where you can just archive old history when you know it probably won't ever be referenced again.

- Microsoft has a new set of libraries for concurrent editing called Fluid Framework. 
  - I'm told it's a "generalized data structure" that was inspired by Causal Trees but with a unique and intention-preserving editing scheme. 
  - I found out about it after they decided to use my fast-cloning-copy-on-write B+Tree for TypeScript. they sent me a pull request for diffing versions of B+ trees, but I haven't yet looked into the architecture of their concurrent data type.

- The difference between diamond native and diamond WASM demonstrates how, even with WASM, native implementations beat browsers hard, and native implementations performance-wise are still very worth, specially for lower powered devices, and, perhaps, reducing battery usage (as consequence of less CPU use) in mobile devices.
  - The wasm implementation here was still running under a JavaScript test harness, so I suspect it's the JS-WASM boundary interactions that are causing the slowdown. WASM itself (if it doesn't need to interact with JavaScript) usually runs with a much smaller performance penalty.
- Yes. Ultimately WASM is executing within a sandbox & involves being JIT compiled (read: not heavily optimized except for hot loops eventually). If native compilation is an option it makes sense to go that route. WASM competes with asm.js not asm (or, arguably, jvm etc)
- WASM JIT implementations tend to be quite a bit different from JavaScript JIT, so that's not really where the perf difference comes from.

- Reminds me of the data structures in this markdown library https://github.com/markdown-it/markdown-it/blob/master/docs/...
  - The author hand waves away the possibility that there could be memory locality performance benefits by using arrays in JS but my hunch is that there is something in that. I know the react code base for example went for a monomorphic Object structure to represent components to leverage inline caching of hidden classes.

- Xi has/had a rope library that allowed one to apply many monoids at each internal node. So one could search for a position in the document as TFA is doing, but also count bytes, Unicode codepoints, Unicode characters/glyphs/widths, etc. with just one tree.
  - What's common to xi's approach and TFA's is monoids. Monoids are at the heart of CRDT.

- If anyone is looking for the combination of a piecetable and b+tree (which appears to be what is talked about in this article), I have one that I've been using for years across various GTK components. https://gitlab.gnome.org/chergert/textrange/
# 👥 [5000x faster CRDTs: An adventure in optimization (2021) | Hacker News _202212](https://news.ycombinator.com/item?id=33903563)
- I've done a bunch more optimization since I wrote this post last year
  - Since last year I've made this algorithm run another ~2x faster. The performance improvement comes about largely thanks to replacing ropey with my own jumprope library. (~60ms -> 30ms)
  - I've written a new CRDT algorithm which is another 10x faster. (time drops to 4ms). But the algorithm is only faster when the editing history is largely linear.
  - Automerge-rs has adopted a lot of the tricks I listed in this post. But its still 100x slower than diamond types and uses 100x more RAM (200mb for automerge vs 2mb for diamond types). The main optimization automerge is missing is the internal run-length encoding trick that Yjs pioneered.

- there is no one-algo-fits all solution. Rather than trying to find a general solution that is not terrible for either case but also not optimal for either case

- I'm interested to see that the rust code run as WASM takes 193ms, but natively runs in 56ms. That's some serious overhead from the runtime! I would have hoped running wasm was closer to native speed than that.
- The JVM has a ton of different things going on, it's not an apples-to-apples comparison. 
  - For one, the JVM isn't sandboxed by default. WASM is. That adds additional overhead.
  - Another consideration is that the JVM uses garbage collection. This doesn't just apply to the code itself, it includes things like the hot code cache and stuff. The JVM trades throughput for latency. WASM doesn't have a GC model.
  - Lastly, WASM doesn't define the runtime. There is no JIT for "WASM", that's just a bytecode spec. I'm actually not even sure if when you run it in a browser it will JIT the WASM bytecode.
- V8 does JIT compile WASM
  - I would also expect GC to be an advantage for WASM here, since it originated from a language without a GC. Having to run a GC is slower than not having to run a GC, and the WASM code from the article doesn't need garbage collection.

- 🤔🆚️ I wonder how performance would change if using `SQLite` instead. You would get those range trees and indexes for free (hence much simpler implementation). Plus persistent storage, some guarantees, etc.
  - All the CRDTs I'm looking at here are doing the work in memory only. Adding a good persistence layer is a big missing piece here.
  - But some people are working on adding CRDTs to sqlite: https://github.com/vlcn-io/cr-sqlite
  - It'd be really fun to see if this approach can be adapted to sqlite's b-tree. But it might not work as-is. The b-tree implementation I have is quite a bit different from most b-trees because I'm storing offsets rather than "keys", and because I'm storing compacted runs of items rather than individual rows.

- https://github.com/vlcn-io/cr-sqlite/
  - > Tables are modeled as GSets...
  - > Rows are currently modeled as LWW maps. I.e., each column in a row is a LWW Register.
# 👥 [Faster CRDTs (2021) | Hacker News _202408](https://news.ycombinator.com/item?id=41372833)
- [Thymer](https://thymer.com/) uses CRDTs for everything. It's an IDE for tasks and planning. It's a multiplayer app, end-to-end encrypted and offline first, optionally self-hosted, and an entire workspace is a single graph. So CRDTs were the logical choice.
  - All operations in Thymer get reduced to a handful of CRDT transformations.

- 👷🏻 jitl: Today(202408) Notion is a last-write-wins system with limited intention-preserving operations for list data (like block ordering). Text is last-write-wins, each block text or property is a last-write-wins register. We're working on a new CRDT format for block text.
- Do you use last-write-wins using the received order of operations on the server or using a logical clock?
  - No clocks on the write side

- 🌰 Most of iCloud's services use CRDTs underneath I believe
  - Indeed, Apple Notes has a reasonably sophisticated CRDT, including support for tables:
  - https://github.com/dunhamsteve/notesutils/blob/master/notes.md
  - The notes are stored in ~/Library/Group Containers/group.com.apple.notes in a sqlite database named NoteStore.sqlite. The database contains sync state from iCloud. It's a CoreData store
  - Apple uses a CvRDT(state-based) for syncing 
- The code editor Zed uses them for collaboration. It was discussed in a Developer Voices episode 

- Any and all networked video games with some form of rollback or correction. Best effort with a fallback to Rollback might actually be the “best” ie ergonomic experience for CRDTs that are most widely used.
  - The most popular, highly ergonomic, best implementations of CRDTs actually break the academic rules of CRDTs.

- It's not a CRDT, it's LWW at the cell level, transmitted pretty much a typing speed so conflicts are low

- Git uses a CRDT internally?
  - No. Factually, inarguably, no.
- Yeah I think you’re correct: Git’s internal data structure is a grow-only set CRDT (well, graph) of commit objects. Grow only sets of hashed contents are one of the simplest CRDTs out there - the network just implements set union.
  - If git only had commit and fetch, it would be a crdt (though not a very useful one). But git also needs to merge commits / branches together. And it does that via diff-match-patch, which doesn’t pass the crdt rules. (Since it’s not idempotent, associative, automatic and in many cases deterministic).
- The content-addressed database for commit objects (but not their names): possibly, yes. It has trivial merge semantics, just keep everything and deduplicate.
  - But that's equally true of every content-addressed system. And entirely untrue for every named object in git, which are a critical component of git being git, instead of an opaque blobstore with zero semantics.
- Yes I agree. I still think its wrong to call Git a CRDT because git is a lot more than its content-addressable system. All that other stuff on top - you know, the parts you use to track and merge branches? That stuff isn't a CRDT. Maybe its like asking if Wikipedia is a relational database. I assume wikipedia is implemented on top of a relational database. But the resulting wikipedia website? No, not a relational database.

- there’s three criterion for CRDTs and git fails 2 of them. Even ignoring the requirement for automatic conflict resolution (which git can’t meet since automatic resolution fails as a matter of course) and ignoring that the conflict resolution algorithm has to be part of the data type (it’s not), it fails the requirement that separate different copies must eventually converge when brought online but that’s demonstrably false as people may use different conflict resolution mechanisms AND the commit graph of a resolved conflict may itself then be different resulting in different histories from the process of brining git online.
  - This is because the commit graph itself isn’t CRDT. If I commit A and then B but someone’s clone only has B applied, you can’t synchronize even automatically; different git histories don’t resolve in any way automatically at all and once you pick a solution manually your copy will not have the same history as anyone else that tries to redo your operations.

- Multi-value registers are CRDTs for sure. Conflict-free doesn't mean that values can't have concurrent histories (or, as you say, "multiple versions") -- it means that the merge operation always succeeds.

- I really wish someone would make a git-like tool on top of CRDTs. I want conflicts when merging commits like git does, but I also want the crdt features - like better cherry-picking and cleaner merging when merging several branches together. And of course, live pair programming. CRDTs store a superset of the information git stores - so we should be able to use that information to emit git style conflicts when we want. But I think nobody has implemented that yet. (Pijul probably comes closest.)

- I suspect a major reason why CRDTs haven't been a clear dominator in VCSes is that the "conflict free" decision is not necessarily the correct decision. It's merely a consistent one.

- Fossil (https://fossil-scm.org) is actually a proper grow-only set from what I can tell: merge conflicts upon synchronization are encoded in the DAG as forks of the history at the conflicting points in time. If no action is taken after a fork, all clones will eventually see the exact same view of the history.

- I would want the git-like tool to have semantic diffs, and so have much better conflict resolution as a result; not CRDTs and more obtuse & confused conflicts than it's already capable of.

- 🐛 CRDTs are powerful, but it's unfortunate that they leave behind a trail of historical operations (or elements), both in their ops- or state-based variants. Even with compression, it's still a downside that makes me concerned about adopting them.
  - I've had this conversation with people a lot. And people in the CRDT world also talk about it a lot. But in practice, at least with text editing, the overhead is so tiny that I can't imagine it ever coming up in practice. 
  - But the overhead is usually less than 1 byte for every character ever typed. If I turn on LZ4 compression on the stored text, documents edited with diamond types are often smaller than the resulting document state. Even though we store the entire editing history!
  - 🤔 Git also suffers from this problem, by the way. Repositories only grow over time. And they grow way faster than they would if modern CRDT libraries were used instead. But nobody seems bothered by it. (Yes, you can do a shallow clone in git. But almost nobody does. And you could also do that with CRDTs as well if you want!)
- I don't think the concern was necessarily about overhead, but about sensitive data. This is a problem in Git too: people make the mistake of reverting a commit with sensitive values and think it's gone, but the history is still out there.
  - 🤔 If thats what you're worried about, use Yjs. Yjs doesn't store deleted characters in documents. Unless you actively make yjs snapshots, once a character in a yjs document is deleted, its gone.
- If you’re not building something fully decentralized, you may be able to loosen some of the constraints CRDTs require. As an example, if you can guarantee that all clients have received changes later than X date, you can safely drop any operations from before that date.
- What's the concern if you can delete history?
  - In a distributed system, which is often a place CRDTs thrive, deleted history means a new client cannot be brought up to the current state unless there is some form of state summarization. Doing this summarization/checkpointing in a consistent manner is difficult to do without some form of online consensus mechanism, which is also difficult to do in a distributed system with clients popping in and out all the time.
- It depends on the system. Some approaches (like Greg Little's Shelf or my Eg-walker algorithm for text) make this trivial to implement.

- The full op-log plus deterministic merging is a great fit for immutable block storage, which can have other security, performance, and cost benefits. I'm building Fireproof to take advantage of recent research in this area. An additional benefit to content addressing the immutable data is that each operation resolves to a cryptographically guaranteed proof (or diff), enforcing causal consistency and allowing stable references to be made to snapshots. This means your interactive, offline-capable, losslessly-merging database can run on the edge or in the browser, but still have the integrity you'd have looked to a centralized database or the blockchain for in the past. (Eg you can drop a snapshot CID into a PDF for signature, or a smart contract, and remove all ambiguity about the referenced state.
- how do such immutable systems deal with redaction eg for GDPR delete requests? Do you need to repack the whole history, and break the existing signature chain?
  - Yes that’s what you’d do. Makes sense to partition eg one chat per database file / proof chain, for lots of reasons including that.

- Automerge's Rust implementation seems to have landed so it would be interesting to see an updated benchmark.
  - Author here. Yjs has also been rewritten in rust (yrs) and it’s significantly faster than the JavaScript version. I’ve also got a new, totally different approach to solving this problem too.

- Why is WASM 4x slower than native execution? I thought it was because every string operation had to be copied into WASM memory and then back into JS when the result was computed. Am I wrong? Am I misunderstanding the context? Genuinely curious!
  - Author here. This post was from a few years ago but from memory I controlled for that. So the problem wasn't FFI. I loaded the whole history into wasm before I started timing, then processed it in an inner loop that was written in rust, running in the wasm context itself. There were only 2 calls to wasm or something. The 4x slowdown wasn't FFI. The algorithmic code itself was actually running 4x slower.

- Seeing the hierarchical structure used I wonder if they tried using nested set instead. No idea if a possible gain in read operation would offset the losses in insertions.
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
  - 🔀 Shelf algorithm for last-writer-wins JSON editing is simple enough you can implement it in less than 100 lines of code. But shelf doesn't support collaborative list or text editing (text is a list of characters).
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
  - 但是会发生下面的 anomaly
  - 需要找到一个合适的数据结构来表达 pos，让 pos 具有 last writes win 的性质
  - 每个 list item 都要有一个 LWWRegister，并把它们放在一个 Add-Wins Set (AWSet) 中

## 🐛 Moving subtrees of a tree

- 在一棵树内移动子树也是个很 tricky 的问题，但是这样的场景比较常见，例如文件系统就是一棵树。
- 一个可行的解决办法是引入操作的时间戳。

## 🐛 Reducing metadata overhead

- 为了完成 undo 和 redo，CRDT 需要存储很大的 metadata
- Martin 开始介绍 automerge 项目，他的 proposal 和 PR#253 使用 columnar encoding 的思路，使得 CRDT 的 overhead 变得很小。
# more
