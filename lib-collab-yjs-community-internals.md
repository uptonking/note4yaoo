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
# discuss
- ## 

- ## 

- ## [Moving elements in lists - Yjs Community _202005](https://discuss.yjs.dev/t/moving-elements-in-lists/92)
- Moving element(s) is possible in any list CRDT, as Martin Kleppmann described. He just discusses a single approach, but there are probably more solutions that can be explored. 
- My first idea was to use special move-items that will refer to a range (start; beginning) of items (In Yjs terms an item is an integrated list-CRDT operation that consists of a unique id, content(s), and a position (next item; previous item)). 
  - The moved items would be marked as moved and would refer to the move operation. 
  - In case of a concurrent move, a last writer wins algorithm is simply implemented by comparing the unique identifiers of the move items that overlap.

- 🆚️ Yjs’s arrays have stricter semantics than the fractional indexing implementation. 
  - In particular, Y. Arrays do not suffer from interleaving. 
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
