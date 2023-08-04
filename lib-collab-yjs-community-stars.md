---
title: lib-collab-yjs-community-stars
tags: [collaboration, community, yjs]
created: 2022-10-22T18:46:22.507Z
modified: 2022-10-22T18:46:45.456Z
---

# lib-collab-yjs-community-stars

# guide

# discuss
- ## 

- ## 

- ## 🤔 We’re open sourcing y-sweet, a standalone Yjs CRDT server written in Rust.
- https://twitter.com/drifting_corp/status/1687148228259577856
  - The core idea of y-sweet is that documents are files, not database entries. 
  - It uses a session backend model to store files directly on S3-compatible storage (including R2).
- 👉🏻 We discussed the idea that file editors should use files, rather than databases, in the last Browsertech Digest. 
  - y-sweet’s architecture is heavily inspired by Figma’s persistence and multiplayer.
- Our goal is to help to elevate Yjs to the level of end-to-end developer ergonomics developers expect from a collaboration frameworks, but without the lock-in. 
  - We’re also releasing React hooks and an SDK for integrating client token generation with your existing auth.

- ## Seriously question, is YATA/YJS the same model as WooT and/or WootH. _202009
- https://twitter.com/kevin_jahns/status/1300857487466229760
  - What are the characteristic differences that distinguish from this original implementation and recent updates inspired by RGA?
- 👉🏻 I don't see how YATA is similar to WOOT. They are completely different algorithms with different performance characteristics. IMO the biggest contribution of the YATA paper was that conflicts can be visualized.
  - Choosing a CRDT algorithm is always a tradeoff. YATA requires additional metadata for conflict resolution (one integer more). Using the compression format, this drawback is eliminated (just look at https://github.com/dmonad/crdt-benchmarks/pull/4). In exchange, Yjs applies updates more efficiently.
- Nice! In regards to GC "a tombstone object can be removed only if no future operation will be concurrent with  the delete operation that converted the object into a tombstone" Isn't this mathematically impossible given conditions like being disconnected/offline?
  - Yes, exactly! But if you assume that clients will be connected (which I did at the time, as it is the case with GDocs that also didn't allow offline editing), then you can garbage collect tombstones. You could gc after a week, and assume that all documents synced in that time.
- Just to be completely clear here: GC approaches can work, but they are not worth the risk of diverging documents. Which is why this GC approach is no longer a part of Yjs. There are other ways to compress tombstones in a secure manner, as I explained here

- One characteristic similarity that jumped out at me is the use of linked lists as structure. But it looks like that's about the only similarity. I'm only beginning to grasp the differences here in implementation (CT/Chronofold/OpLog..etc)
  - Yeah, I get that. Also it doesn't help that Chengzheng Sun published a series of misleading articles that describe Yjs as a WOOT based CRDT with an incorrect garbage collection scheme. This is probably where you got the idea from.

- It is often claimed that RGA is the fastest linear CRDT, which is clearly not the case. YATA can be implemented very efficiently. Using the visual representation, conflicts are resolved without any transformation in most cases.
  - The current implementation has the same runtime performance as RGA, but works better in practice. In the benchmarks Yjs outperforms any RGA implementation - just look at how badly RGA performs in B1.3 or B3. 

- I'm also curious on a more complete benchmark of Chronofold and using RON for encoding. I saw @gritzko posted here https://github.com/dmonad/crdt-benchmarks/issues/3 One thing that jumps out for me is that chronofolds may not necessarily have the same op seq as each of the peers (though still converges)
  - Whoops, you already shared the link. But the point is that RONs representation is apparently worse in B1.4 than Yjs (100kB RON, 30kB Yjs). The C++ implementation runs obviously much faster than js. We should be able to compare Yjs with more CRDTs once Yjs has a Rust port.

- ## [Support for PubSub communication protocol · Issue #63 · yjs/yjs_201701](https://github.com/yjs/yjs/issues/63)
- We recently published a paper about the CRDT used it Yjs: yjs.pdf If you are familiar with WOOT: they share some similarities.

- ## [Which algorithm y-array is using? · y-js/y-array_201708](https://github.com/y-js/y-array/issues/9)
- Yjs does not share any concepts with the RGA algorithm. 
  - If you want to compare it conceptually, Yjs is actually more similar to WOOT.

- While both algorithms have a time complexity of O(H^2), the syncing process is actually very performant in Yjs. 
  - In WOOT, you basically have to apply all operations from the beginning of time. 
  - In Yjs only missing operations need to be applied.
- You got me thinking. I could improve the complexity to O(log(n)*N) by using a lookup table. 
  - This will make Yjs look better on paper. 
  - But I doubt that this makes a difference in practice. 
  - Conflicts rarely occur in practice. 
  - Again to clarify, this is the number of characters that is inserted at the same time+same position. 
  - Have a look at this comparison of CRDTs. 
  - Even when a large number of conflicts are forced, WOOT performs pretty similar to RGA, without having a big memory overhead.

- In JS and other higher-level languages, objects have quite a lot of overhead: headers, gc bookkeeping, etc. 
  - That may dwarf those 62+8 bytes. 
  - That's why Causal Tree (my RGAish algo) keeps the data in strings or typed arrays.

- ## It looks like Automerge 2 latest is faster than Yjs, but still uses 2x more memory._202301
- https://news.ycombinator.com/item?id=34586433
  - Yjs (pure javascript?) is quoted on the paper benchmark at 1, 074ms and 10, 141, 696 bytes of memory, compared to Automerge 2.0.2-unstable at 661ms and 22, 953, 984 bytes of memory. 
  - I wonder if this is comparing usage from JS via bindings, or directly comparing two different rust implementations, or comparing Automerge 2.0.2-unstable via Rust to Yjs via NodeJS.
  - I am still not sure which set of tools I would recommend; I believe Yjs is more actively deployed in production since the Automerge implementation was so far behind performance wise until now. 
  - However one of the Peritext authors (https://twitter.com/sliminality who is on my team at Notion) tells me that 👉🏻 Automerge is better at text because it doesn't suffer from interleaved characters like Yjs does. So consider it instead of Yjs!
- 👉🏻 I’ve spent a lot of time benchmarking both libraries and talking to the authors. The main difference is that yjs has an extra optimization that’s still missing from automerge: Yjs does internal run-length encoding of adjacent inserted items. And adjacent inserts come up a lot in real text editing traces.
  - Adding this optimization to diamond types, in pure rust, improved performance by another order of magnitude (25ms for the same test with this tweak). It also dropped memory usage to about 2MB. 
  - The automerge engineers know about this trick (I’ve talked to them about it). So I assume it’s in the pipeline somewhere. And yjs is working on a rust reimplementation, which should bring its performance in line too.
- This optimization is indeed in the pipeline, although there are other things nearer the front because performance is currently Good Enough ™ that other things are more pressing (other things being e.g. completing the Peritext implementation, improving the sync protocol).

- diamond-types (for reference for others [0]) still only supports plain text, is that right? I was thinking of using it for more general use cases such as an offline habit tracker, which isn't text of course, but I was interested to hear more on the progress towards other data types such as generic JSON data.
  - Currently for this use case I've been using autosurgeon [1] so far which has a nice Rust API for structs, even if it might be slower than yjs (or yrs, its Rust implementation) or diamond-types.
- Yep; sadly still true. I started some work last year to simultaneously add support for arbitrary JSON data and add a database-like storage layer to allow us to safely stream changes to disk. (Automerge and yjs usually require the entire data set to be re-saved in its entirety when updates happen). Its taken longer than I thought, because I've gone through a bunch of different designs for both pieces. We'll get there; everything just takes longer than you want when you do it for the first time. I'll look at autosurgeon. Having similar APIs is good for everyone.

- ## [Should we do state management directly with yjs, or through bindings like SyncedStore? - Yjs Community](https://discuss.yjs.dev/t/should-we-do-state-management-directly-with-yjs-or-through-bindings-like-syncedstore/1345)
- It really depends. There are arguably nicer libraries for state management. 
  - Yjs is meant to have a minimalistic interface for observing changes (and calculating differences) that can be integrated into other libraries. 
  - It doesn’t have the reactive interface of mobx, and isn’t immutable like Redux. 
- However, nothing is perfect. Most users of state management libraries don’t think too much about properly organizing data for managing conflicts, optimizing shared data for performance, and migrating existing data to new schemas. 
  - React data stores are, in my opinion, too close to the representation. You likely want to reorganize data when the structure of your application changes. synced-store might make it too easy to make an existing application collaborative. 
  - Instead, you should think very carefully about the schema of your data. Because it’s really hard to change it once you have active users.

- ## [Full JSON representation](https://github.com/yjs/yjs/issues/284)

- One of the advantages of using a JSON structure it because it is a bit more human readable. 
  - In our case we save snapshots of the document in json format that can be queried afterwards. 
  - We save it by doing `doc.toJSON()` and we also have a recursive function that allows us to recreate a document from a JSON structure that we previously saved.
  - That also decouples us from YJS, so in the future if we need to migrate away from YJS we already have the data in a JSON structure.
  - I know this is a different case than what is proposed here, but I wanted to contribute some ideas that we are using.

- The biggest use case for JSON is not just in Human Readability you could just use Yjs 's toJSON() for logging / debugging. JSON is ubiquitous, nearly every open source project in every language uses it as the encoding for transport / state.
  - I am working with a new Text Editing framework that gives its state as a JSON. If I have to use Yjs here I will constantly be converting the JSON to Yjs Map / Array for every keystroke and vice versa.
- If I have to use Yjs here I will constantly be converting the JSON to Yjs Map / Array for every keystroke and vice versa.
  - 👉🏻 This might in fact be the best move here. You could probably develop an intermediate representation that allows you to efficiently map changes from the JSON state to the Yjs state without having to re-parse the entire structure every time. While not as efficient as using Yjs types directly, it could still be adequately performant, and would allow a wide variety of other tools to integrate with Yjs.
- Yes, you can definitely map the Yjs state to a JSON(-like) object. I recommend SyncedStore or alternatives listed in the readme or the forum.
  - Mapping CRDT state to a JSON object is out of scope for the Yjs package. This should be provided by a separate module.

- You might wanna look into Ron which aims to standardize encoding in different encodings. 
  - I like the approach, but I can't use it in Yjs because it implements a unique, heavily optimized encoder.
  - [Replicated Object Notation — RON](http://replicated.cc/)
  - SwarmDB is a proof-of-concept key-value RON store

- The original question was about representing the CRDT updates in a JSON representation for logging purposes. 
  - I provided functions to convert updates to a JSON format for debugging. However, most people won't be able to understand the generated state changes as one would need to understand how the CRDT works. 
  - Even then, it is basically impossible to read useful data out of them as they are only useful for debugging a CRDT. 
  - You always need to apply updates to a Yjs document (or Yrs, Ypy, ..).
- There are still so many projects that transport the Yjs updates as a JSON Array (instead of using base64) which makes me sad. So many wasted bytes... 
  - So I can't stress this enough. Never ever transport Yjs updates as-is in a JSON object. Use base64 if you must
- 👉🏻 CRDTs that use JSON encoding generally don't perform well in JavaScript. 
  - Parsing JSON is expensive and allocates memory inefficiently. 
  - I indirectly make use of the fact that modern JavaScript engines optimize memory allocation of the same object (in Yjs the "Item" class). 
- Another advantage of the Yjs encoder is that it achieves high compression at no cost without using an expensive generic compression algorithm (e.g. zip). 
  - In some cases, the encoder achieves 300x better compression rates & 1000x better performance than other CRDTs that use JSON encoding
- I'm a big fan of immutable state. But I believe that this is not the correct solution for implementing a CRDT. However, you should be able to implement immutable state on-top of Yjs(zustand-yjs). 
- The advantage of JSON encoding is that it is human-readable. But CRDTs that use JSON encoding don't perform well in practice. With compression techniques like RLE encoding, variable-length encoding, and tabular encoding we can make CRDTs viable in practice. For this reason, I don't recommend JSON encoding as a go-to solution.

- My motivation is to create some sort of a standard like JSON Patch, but something for CRDTs, I guess something like RON but dedicated to JSON data type.
- I'm not sure if it is feasible to create a JSON representation just for the sake of using JSON instead of binary encoding. I still don't understand the advantages.
  - For manipulating content you should rather use the methods that are provided by Yjs. You could also add functionality for Yjs to accept changes that are expressed in the JSON Patch format. Yjs already supports the Quill Delta format, which was originally developed for Operational Transformation.
  - I feel you might be interested in something like the json1 type in @ottypes

- ## [Is it possible to use yjs for collaboration over a nested object (modeled as a JSON object)?)? - Yjs Community](https://discuss.yjs.dev/t/is-it-possible-to-use-yjs-for-collaboration-over-a-nested-object-modeled-as-a-json-object/102)
- The Yjs data types are more expressive as JSON. 
  - You can model any JSON document using Yjs types.
- JSON is just an encoding technique. 
  - In JavaScript, you can efficiently express complex data structures using the JSON consisting of Object, Array, and primitive data types (number, string, …). 
  - You can model any Object as a Y. Map, and you can model any Array as a Y. Array. 

- ## [Extending Yjs Types without breaking everything - Yjs Community](https://discuss.yjs.dev/t/extending-yjs-types-without-breaking-everything/769)
  - I came with the idea to create custom Yjs types to extends defaults shared types methods and to get a better type experience DX, code clarity etc.
  - `export class YColumn extends Map<any> {` 继承
  - But when we encode state as update or play with the history, custom types are loss with their functionalities and the app crashes as expected.
- I tackled this via composition rather than inheritance, as I ran into similar roadblocks.
- The way I have “solved” it temporarily is instead of using inheritance, Extend the prototype

- ## [History of collaborative editing solutions. What usually people used before automerge, yjs etc.. ?](https://github.com/automerge/automerge/discussions/496)
  - I found automerge (2017), yjs (2015), sharedb (2013). All of them are relatively new.

- Before CRDTs came along, the main technology for real-time collaboration on text documents was Operational Transformation (OT); 
  - the most common algorithm was introduced by the Jupiter system at Xerox PARC in 1995, and adopted by Google Docs in 2010. 
  - Jupiter assumes that all edits flow via a central server. 
- CRDTs arose from the difficulty of making p2p OT work, and represented a new start using a completely different approach. 
  - The idea only appeared around 2006 or so, and early implementations were very inefficient. 
  - It took perhaps a decade for the CRDT algorithms to be refined to the point where you could use them for non-trivial documents.
- Interestingly, the world of multiplayer games is totally separate: afaik, very few people in the collaboration software community know what techniques are used in games and vice versa. 
  - my take-away from this is that the needs of games and application software are sufficiently different that it does not make much sense to share techniques. 
