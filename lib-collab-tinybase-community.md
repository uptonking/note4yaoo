---
title: lib-collab-tinybase-community
tags: [collaboration, community, tinybase]
created: 2023-01-12T15:51:52.243Z
modified: 2023-01-12T15:52:42.418Z
---

# lib-collab-tinybase-community

# guide

# discuss
- ## 

- ## 

- ## 

- ## TinyBase v3 is going to have two demos to showcase CRDT synchronization.
- https://twitter.com/jamespearce/status/1608520684795465728
  - One will be P2P (over WebRTC), and one will be multi-party (via a central server). 
  - But even P2P requires a server to set up the signaling.

- I like using Replit for when I need a low usage multiplayer backend. Interested to hear about a good stateful simple deployment solution. Cloudflare workers for sure is a good option as evidenced by an increasing use of it for multiplayer backends.

- ## HLCs & CRDTs are easy! The harder part is shrinking them into tiny negotiable P2P payloads...
- https://twitter.com/jamespearce/status/1604304923247939584
- Each HLC entry is a 16 digit radix-64 string comprising 42 bits for time in ms, 24 bits for the counter, 30 bits for hash of unique client id. They're string-sortable.
- Every change that a database knows about (whether local or remote) is put into this Patricia-like trie.
  - Each HLC is split into four parts (3 + 4 + 4 + 5 chars) to address the nodes, and the leaf is the [table, row, cell, value] change.
  - `undefined` is a cell deletion.
- For shipping over the wire, the tree is encoded in three parts:
  1) an array of JSON-encoded table Ids, row Ids, cell Ids, and cell values.
  2) an array of radix-64 safe strings (which don't need quoting!) for the trie vertices.
  3) a tightly packed serialization of the tree.
- Because the tree's shape is well-known, this encodes and decodes pretty quickly.
  - It's quite easy to merge and diff these trees. So when a client makes a request to a peer for changes, it sends its own changes in the request. The peer's response is just then the new changes.
- Adding Merkel hashing to the tree would be slower but would allow the negotiation to bail out (or identify tree diffs) much sooner.
  - Or perhaps the tree could be progressively negotiated. 
  - (The trickiest thing might be version-controlling an evolving protocol!)
- Warning! This is all still in 'hacker space'. There's no concrete implementation in the TinyBase repo yet. But it might be worth rolling out an experimental branch soon. We'll see.
- You can use “pako” to compress and decompress your payload to make it smaller over the wire

- ## RFC! TinyBase HLC format. Needs to be small and fast for packing into binary tries & CRDTs
- https://twitter.com/jamespearce/status/1599796118014918658
- 11 byte(88 bits) bigint of
  - 42 bits, millis (~139 years)
  - 14 bits, counter (~16k)
  - 32 bits, hash of client id (~4 billion)
- You may want to consider using a `TypedArray` with `DataView` instead of `BigInt` to store the data if you really care about in memory size and layout. 
  - I wouldn't trust that bigint for such small sizes would not have a lot of additional memory overhead.
- Interesting. I was more worried about performance initially but that seems within 10% of Number (at least for the operations I need like shift, xor, gt, lt). I should check memory though - good point.
- Also I should mention I ideally need this as a key for a Map (or member of a Set).
  - You can use the index in the typedarray for key
  - Not sure I follow. If I have two HLCs coming from different systems with the same binary value, I'll want them to key the same value from a local map. (I'd need to convert to BigInt to do by value rather than differing reference, no?)
  - If it's coming from different system, just ignore me
  - Otherwise, whenever you generate a bigint key, you would use the index as reference going forward. But it may not be practical in many cases.
  - One thing I could do is use an array of two 53-bit or three 32-bit Numbers, and then have a map of maps (or map of map of maps)

- ## [TinyBase v2.0: reactive data store for local-first apps | Hacker News_202209](https://news.ycombinator.com/item?id=32871392)
- RxDB with PouchDB has support for typescript, json schema, and binary attachments. Moving the attachments to the file system will be up to you.

- I’m my limited experience, a reliable CRDT implementation necessitates a CDRT-first design baked into the core of any data / transaction model. Like I’ve heard some game developers say- multiplayer needs to come first because tacking it onto a single player game is a nightmare.

- ### [CRDTs for tinybase_202209](https://github.com/tinyplex/tinybase/discussions/31)
- I've had to do a bunch of background reading. Still not sure of quite the right strategy yet... 
  - but in our favor we have the fact that TinyBase can listen and update on a cellular granularity, reducing the likely conflicts per row or table.
- The current checkpoints module is an example of keeping a sequence of cell-level changes like that (and it handles deletes a charm). But I need to think about what a flexible API to get or replay such a log in a CRDT context would look like.
- I've started a dedicated disposable repo for these half-baked ideas. 
  - https://github.com/tinyplex/tinysync

- ## Here's an interesting browser state solution: A database, written in JS, called TinyBase.
- https://twitter.com/housecor/status/1492859757941637126
  - Tables, rows, cells, indexes, relationships, undo, and more. 
  - Persist the data to the browser, files, or a server.
- what sense makes database on client when you need to transfer the data? also all data is public by default
  - You can use it offline.
- Interesting for client-first apps!
  - I'm using Dexie.js on top of IndexedDB, but it has its limitations wrt/ queries (and performance).
  - Another crazy experiment on my list of things to try is @jlongster 's Absurd SQL
- I wonder if theres a world where you use absurdSQL (or raw SQLite wasm) as custom persistor with it? 
  - Currently persistence is just "where can you save and load a JSON string?" at a Store-wise level. So sure! 
  - But I once had an experiment for sharded persistence per table or row. 
  - At that point, keeping it in sync with a 'real' database might be quite scalable and interesting.
