---
title: lib-collab-automerge-blog
tags: [automerge, blog, collaboration]
created: 2023-09-01T11:01:04.574Z
modified: 2023-09-01T11:01:24.685Z
---

# lib-collab-automerge-blog

# guide
- ["New algorithms for collaborative text editing" by Martin Kleppmann (Strange Loop 2023) - YouTube_202309](https://www.youtube.com/watch?v=Mr0a5KyD6BU)
# blogs

## 📝 [Automerge-Repo: A "batteries-included" toolkit for building local-first applications_202311](https://automerge.org/blog/2023/11/06/automerge-repo/)

- Automerge is a fairly mature CRDT implementation. 
- The API is quite low-level though, and Automerge-Core has no opinion about how networking or storage should be done. 
- Often, the first thing developers ask after discovering Automerge was how to connect it into an actual application.
- automerge-repo, extends the collaboration engine of Automerge-Core with networking and storage adapters, and provides integrations with React and other UI frameworks. 
  - You can get to building your app straight away by taking advantage of default implementations that solve common problems such as how to send binary data over a WebSocket, how often to send synchronization messages, what network format to use, or how to store data in places like the browser's IndexedDB or on the filesystem.

- automerge-repo works with both client-server and peer-to-peer network transports.

- Create a repo by initializing it with an optional storage plugin and any number of network adapters.
- A `DocHandle` is a reference to an Automerge document that a Repo syncs and stores . The Repo instance saves any changes you make to the document and syncs with connected peers. Likewise, you can listen over the network for to a Repo for any changes it received.
- Each DocHandle has a `.url` property. This is a string which uniquely identifies a document in the form `automerge:<base58 encoded bytes>`. Once you have a URL you can use it to request the document from other peers.

- You can extend automerge-repo by writing new storage or network adapters.

- The basic shape of the API is simple and useful, and not having to think about the plumbing makes it much, much faster to get a useful application off the ground. 
- 👉🏻 However, there are some performance problems we're working on:
  - 😩 Documents with large histories (e.g. a collaboratively edited document with >60, 000 edits) can be slow to sync.
  - 😩 **The sync protocol currently requires that a document it is syncing be loaded into memory**. This means that a sync server can struggle to handle a lot of traffic on large documents.

- automerge-repo solves a bunch of the hard problems people were encountering around networking and storage.
- There are still plenty of other difficult problems in local first software where we don't have turnkey(一切齐全可以立即使用的) solutions: authentication and authorization, end-to-end encryption, schema changes, version control workflows etc. 

- ### 👥 Build local-first apps the way we do at Ink & Switch with automerge-repo
- https://twitter.com/pvh/status/1722303054299725837
  - It's a lightly opinionated approach and wraps Automerge's core data structure with event-based subscriptions and pluggable network/storage.
- I've been trying to use automerge but having difficulty "slicing" the store, basically my entire app re-renders when anything in the store changes rather than using something like redux where you can provider a selector. Any chance you can point in my a direction?
  - using something like zustand I'm able to slice effectively. I'm sure there's a way to make it work with automerge, just not seeing it yet
- Right, the document is changing so the render functions are being called. I think idiomatically I would pass down the counter values and a change function to a child but I agree the way you want to do this is reasonable.
  - Yeah I guess I could do that and memoize the child 

## 👥 [Automerge-Repo: A "batteries-included" toolkit for local-first applications | Hacker News_202311](https://news.ycombinator.com/item?id=38193640)

- What do you suggest is the sweet spot for document size and "hotness"? And is the "atom of contention" the document as a whole, or do you have any plans for merging of sub-parts?
  - The way I think about it is that if the data should always travel together it should be in one document. For example -- if your TODO list always goes as a unit, then make it an array of objects in a single Automerge document. On the other hand, if you want to build an issue tracker and to be able to link to individual issues or share them individually then a document each is the way to go. Does that help?
  - As for network transports you can indeed have multiple at once. I usually have a mix of in-browser transports (MessageChannels) and WebSocket connections. I suspect we'll need to do a little adjusting to account for prioritization once people really start to push on this with things like mDNS vs relay server connections but the design should accommodate that just fine.

- The sync protocol does indeed calculate the delta between peers and efficiently catches both sides up.

- Congrats! Many moons ago the lack of undo/redo was the main blocker. Has this been added?
  - Robust undo/redo remains an ongoing research project.but in my experience you can usually get passable results by letting editors default undo behaviour reverse text input.
  - For applications with more document-structured data, you can now produce inverse patches using Automerge.diff to go between any two points. To implement a reasonable undo in this environment you can record whatever document heads you consider useful undo points and then patch between them.

- Automerge is not VC-backed software. Indeed, for a number of years Automerge was primarily a research project used within the lab. Over the last year, it has matured to production software under the supervision of Alex Good. The improved stability and performance has been a great benefit to both our community and internal users. Our intention is to run the project as sponsored open source for the foreseeable future

## 👥 [Automerge: A JSON-like data structure (a CRDT) that can be modified concurrently_202202](https://news.ycombinator.com/item?id=30412550)

## 👥 [Automerge: JSON-like data structure for building collaborative apps_201802](https://news.ycombinator.com/item?id=16309533)

## 🎯📝 [Automerge 2.0_202301](https://automerge.org/blog/automerge-2/)

- Earlier versions of Automerge were implemented in pure JavaScript. 
  - Our initial implementations were theoretically sound but much too slow and used too much memory for most production use cases.
  - JavaScript support on mobile devices and embedded systems is limited. 
- Instead of trying to coordinate multiple distinct versions of Automerge, we decided to rewrite Automerge in Rust and use platform-specific wrappers to make it available in each language ecosystem. 
  - This way we can be confident that the core CRDT logic is identical across all platforms and that everyone benefits from new features and optimizations together.
- For JavaScript applications, this means compiling the Rust to WebAssembly and providing a JavaScript wrapper that maintains the existing Automerge API.

## 🎯👥 [Automerge 2.0 | Hacker News_202301](https://news.ycombinator.com/item?id=34586433)

- It looks like Automerge 2 latest is faster than Yjs, but still uses 2x more memory.
  - Yjs (pure javascript?) is quoted on the paper benchmark at 1, 074ms and 10, 141, 696 bytes of memory, compared to Automerge 2.0.2-unstable at 661ms and 22, 953, 984 bytes of memory. 
  - I wonder if this is comparing usage from JS via bindings, or directly comparing two different rust implementations, or comparing Automerge 2.0.2-unstable via Rust to Yjs via NodeJS.
  - I am still not sure which set of tools I would recommend; I believe Yjs is more actively deployed in production since the Automerge implementation was so far behind performance wise until now. 
  - However one of the Peritext authors (https://twitter.com/sliminality who is on my team at Notion) tells me that 👉🏻 Automerge is better at text because it doesn't suffer from interleaved characters like Yjs does. So consider it instead of Yjs!
- 👉🏻 I’ve spent a lot of time benchmarking both libraries and talking to the authors. The main difference is that yjs has an extra optimization that’s still missing from automerge: Yjs does internal run-length encoding of adjacent inserted items. And adjacent inserts come up a lot in real text editing traces.
  - Adding this optimization to diamond types, in pure rust, improved performance by another order of magnitude (25ms for the same test with this tweak). It also dropped memory usage to about 2MB. 
  - The automerge engineers know about this trick (I’ve talked to them about it). So I assume it’s in the pipeline somewhere. And yjs is working on a rust reimplementation, which should bring its performance in line too.
- This optimization is indeed in the pipeline, although there are other things nearer the front because performance is currently Good Enough ™ that other things are more pressing (other things being e.g. completing the Peritext implementation, improving the sync protocol).

- diamond-types (for reference for others) still only supports plain text, is that right? I was thinking of using it for more general use cases such as an offline habit tracker, which isn't text of course, but I was interested to hear more on the progress towards other data types such as generic JSON data.
  - Currently for this use case I've been using autosurgeon so far which has a nice Rust API for structs, even if it might be slower than yjs (or yrs, its Rust implementation) or diamond-types.
- Yep; sadly still true. I started some work last year to simultaneously add support for arbitrary JSON data and add a database-like storage layer to allow us to safely stream changes to disk. (Automerge and yjs usually require the entire data set to be re-saved in its entirety when updates happen). Its taken longer than I thought, because I've gone through a bunch of different designs for both pieces. We'll get there; everything just takes longer than you want when you do it for the first time. I'll look at autosurgeon. Having similar APIs is good for everyone.

- As it stands CRDTs are only really useful for a narrow subset of data. Data is guaranteed to converge, but there is no guarantee that the final result makes any kind of semantic sense in the application domain.
  - One can write custom conflict resolution and treat the data structures as a convenient baseline for event sourcing, but that requires a lot of work and potentially often user guided resolution.
  - I'd really love to see some research into deriving CRDT merge semantics from a formal description of application behaviour.

- 
- 
- 

# more
