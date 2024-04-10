---
title: lib-collab-yjs-community-internals
tags: [community, internals, yjs]
created: 2024-04-09T04:28:54.264Z
modified: 2024-04-09T04:29:05.430Z
---

# lib-collab-yjs-community-internals

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 🧮🆚️ [Which algorithm y-array is using? · y-js/y-array_201708](https://github.com/y-js/y-array/issues/9)
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

- ## 🆚️ Seriously question, is YATA/YJS the same model as WooT and/or WootH. _202009
- https://twitter.com/kevin_jahns/status/1300857487466229760
  - What are the characteristic differences that distinguish from this original implementation and recent updates inspired by RGA?
- 👉🏻 I don't see how YATA is similar to WOOT. They are completely different algorithms with different performance characteristics. IMO the biggest contribution of the YATA paper was that conflicts can be visualized.
  - Choosing a CRDT algorithm is always a tradeoff. 
  - YATA requires additional metadata for conflict resolution (one integer more). 
  - Using the compression format, this drawback is eliminated. 
  - In exchange, Yjs applies updates more efficiently.
- Nice! In regards to GC "a tombstone object can be removed only if no future operation will be concurrent with  the delete operation that converted the object into a tombstone" Isn't this mathematically impossible given conditions like being disconnected/offline?
  - Yes, exactly! But if you assume that clients will be connected (which I did at the time, as it is the case with GDocs that also didn't allow offline editing), then you can garbage collect tombstones. You could gc after a week, and assume that all documents synced in that time.
- Just to be completely clear here: GC approaches can work, but they are not worth the risk of diverging documents. Which is why this GC approach is no longer a part of Yjs. There are other ways to compress tombstones in a secure manner, as I explained here

- One characteristic similarity that jumped out at me is the use of linked lists as structure. But it looks like that's about the only similarity. I'm only beginning to grasp the differences here in implementation (CT/Chronofold/OpLog..etc)
  - Yeah, I get that. Also it doesn't help that Chengzheng Sun published a series of misleading articles that describe Yjs as a WOOT based CRDT with an incorrect garbage collection scheme. This is probably where you got the idea from.

- It is often claimed that RGA is the fastest linear CRDT, which is clearly not the case. YATA can be implemented very efficiently. Using the visual representation, conflicts are resolved without any transformation in most cases.
  - The current implementation has the same runtime performance as RGA, but works better in practice. In the benchmarks Yjs outperforms any RGA implementation - just look at how badly RGA performs in B1.3 or B3. 

- I'm also curious on a more complete benchmark of Chronofold and using RON for encoding. I saw @gritzko posted here https://github.com/dmonad/crdt-benchmarks/issues/3. One thing that jumps out for me is that chronofolds may not necessarily have the same op seq as each of the peers (though still converges)
  - Whoops, you already shared the link. But the point is that RONs representation is apparently worse in B1.4 than Yjs (100kB RON, 30kB Yjs). The C++ implementation runs obviously much faster than js. We should be able to compare Yjs with more CRDTs once Yjs has a Rust port.
# discuss
- ## 

- ## 

- ## [Moving elements in lists - Yjs Community _202005](https://discuss.yjs.dev/t/moving-elements-in-lists/92)
- Moving element(s) is possible in any list CRDT, as Martin Kleppmann described. He just discusses a single approach, but there are probably more solutions that can be explored. 
- My first idea was to use special move-items that will refer to a range (start; beginning) of items (In Yjs terms an item is an integrated list-CRDT operation that consists of a unique id, content(s), and a position (next item; previous item)). 
  - The moved items would be marked as moved and would refer to the move operation. 
  - In case of a concurrent move, a last writer wins algorithm is simply implemented by comparing the unique identifiers of the move items that overlap.

- 🆚️ Yjs’s arrays have stricter semantics than the fractional indexing implementation. 
  - In particular `Y.Array`s do not suffer from interleaving. 
- Of course, you can represent the array as a map and then convert the map to an array using some kind of sort on the data. This is basically the approach I laid out in the bottom of my answer Moving elements in lists
  - I suggest not to use maps as the top-level data structure. Deleted properties will always take up space (the key-name can’t be removed). When you store the data in a `Y.Array`, you can delete data very efficiently.
  - I’m actually planning a Y. Set implementation for exactly for this use-case. This would allow to implement efficient move-semantics using a sort algorithm on the data.

- This is basically the fractional indexing approach described above that Figma uses right?
  - Exactly! It is just an adaption to support move operations.
  - Re-parenting on maps is currently not supported. v12 supported reparenting, but I removed this feature because it is hard to keep track of potentially cyclic structures. Furthermore, the child cleanup approach wouldn’t work anymore.

- Having a separate map might make sense. I think you read a thread of me suggesting to Duane that he should not use a top-level data structure. In his case, he stored millions of different keys in a single top-level map. For a small file system (with probably less than 10k files) it won’t make a difference. The advantage is that you could use the much simpler first approach. Although the second approach is probably optimal because it is more efficient and allows you to keep everything in a single data structure.

- 
- 
- 
