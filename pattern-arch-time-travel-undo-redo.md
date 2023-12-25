---
title: pattern-arch-time-travel-undo-redo
tags: [architecture, data-structure, time-travel, undo]
created: 2023-08-25T21:52:48.494Z
modified: 2023-09-12T09:36:25.608Z
---

# pattern-arch-time-travel-undo-redo

# guide
- branching和versioning的参考方案
  - 同类产品，如git
  - 编辑器，如vscode、ckeditor、ospreadsheet
  - 数据库，如dolt、mongodb-doc-ver
# dev

# blogs

- [Making Data Structures Persistent_1986](http://www.cs.cmu.edu/~sleator/papers/Persistence.htm)

## 💡 [History Data Structures](https://gist.github.com/CMCDragonkai/d266a3055735545447439f0fa662a0e1)

- For stateful applications, there are 5 different ways of managing the history of state:
  - No History - Living in the moment. - Examples: Any stateful application that doesn't discards all previous states upon mutation.
  - Ad Hoc Snapshotting - Allows restoration to manually saved snapshots. - Examples: Memento Pattern.
  - Singleton - Only remembers the previous snapshot, where undoing the undo is just another undo. - Examples: Xerox PARC Bravo.
  - 1 Stack - Allows linear undo. - Examples: AtariWriter.
  - 2 Stack - Allows linear undo and redo. - Examples: Browser History, Microsoft Word, Adobe Photoshop.
  - Append-Only Log - Allows moving forward with reversed patches/deltas (a.k.a. compensating transactions). - Examples: Git-Revert, Datomic, Blockchain, Event Sourcing.
  - Tree - The Multiverse Approach. - Examples: Git, Vim, Emacs with UndoTree, Delorean.
- There's variations and hybrid approaches that have to deal with special cases involving multi-user history, which is relevant to operational transformation applications such as Google Docs.

- there are 2 different ways of encoding states. 
  - The snapshot method and the delta method. 
- The snapshot method is where every "state" is a complete and independent snapshot of what the state was. 
- Whereas the delta method (a.k.a. delta encoding) is the (ideally minimal) difference between the past and present. 
- The snapshot method uses more storage space, while the delta method requires more computation to merge the differences.
- the time to construct the snapshots takes much longer then when using the delta method.
  - This is because you may need to transitively apply all the deltas from origin.
- There's also a theory formalising how deltas works called "Patch Theory", which is used by the Darcs and Pijul version control system.

## [Arrays that let us time travel](https://arpitbhayani.me/blogs/fully-persistent-arrays/)

## [Introduction to a data structure that let's us time travel](https://arpitbhayani.me/blogs/persistent-data-structures-introduction/)

- Ordinary data structures are ephemeral implying that any update made to it destroys the old version and all we are left with is the updated latest one. 
  - Persistent Data Structures change this notion and allow us to hold multiple versions of a data structure at any given instant of time. 
  - This enables us to go back in “time” and access any version that we want.

- Persistent Data Structures preserve previous versions of themselves allowing us to revisit and audit any historical version. 

- Depending on the operations allowed on the previous versions, persistence is classified into three categories
- **Partially Persisten**t Data Structures allows access to all the historical versions but allows modification to only the newest one. 
  - This typically makes historical versions of the data structure immutable (read-only).
- **Fully Persistent** Data Structures allows access and modification to all the historical versions. 
  - It does not restrict any modifications whatsoever. 
  - This means we can typically revisit any historical version and modify it and thus fork out a new branch.
- **Confluently Persistent** Data Structures allow modifications to historical versions while also allowing them to be merged with existing ones to create a new version from the previous two.

- Implementing Partial Persistence
- Copy on Write Semantics
- Copy on Write Semantics
- Copy on Write Semantics
- Path-Copying Method

- Since persistent data structures thrive on high memory usage, they require some garbage collection system to prevent memory leaks. 
  - Algorithms like Reference Counting or Mark and Sweep serves the purpose pretty well.

## [Persisting the version history of a complex data structure](https://medium.com/@mmdGhanbari/persisting-a-persistent-data-structure-3f4cfd46036)

- In this article, we learned about persistent data structures and the different methods available to copy a complex one, as well as how to persist them in a relational database.
  - you may also want to check the Event Sourcing pattern, which suggests persisting the change itself instead of the changed data.

## [Undo, the art of – Part 1](https://maxliani.wordpress.com/2021/09/01/undo-the-art-of-part-1/)

- I’ll touch on the fact that there is no right or wrong, that undo can be implemented in a variety of different ways and that the best practice strongly depends on the choice of data structures you designed for your application.
- At its essence, undo is a history of changes in the data within a program
- Undo must record the sequence of edit events the user executes, and unwind or rewind the changes in the data. 

## more-blogs

- [onlyoffice: Simplify History Structure](https://github.com/ONLYOFFICE/document-server-integration/issues/437)

- [Version Control · vkbo/novelWriter](https://github.com/vkbo/novelWriter/issues/383)
# more
- [Data model for storing revision history in FoundationDB · couchdb](https://github.com/apache/couchdb/issues/1957)

- [Immutable Data Structures - DEV Community](https://dev.to/martinhaeusler/immutable-data-structures-2m70)
# discuss
- ## 

- ## 

- ## Converting file system changes into ops for a rewindable Obsidian.
- https://twitter.com/JungleSilicon/status/1734394464289132751
  - Obsidian autosaves as you make changes leading to semi-realtime updates.
  - It also respects changes that other programs make, so if a *revert* button was added, Obsidian would update when you pressed it.
  - It wouldn't work for concurrent updates but it gets you to *semi-collaborative* documents.
  - The history is periodically saved to a file and can be recovered when re-opened. If the server is not running then on next open it can do a diff to create the ops.

- ## [Build Your Own X | Hacker News](https://news.ycombinator.com/item?id=32157759)
- One advice: for any of these topics take a tutorial directed at language X and implement the solution in language Y. This will prevent you from mindlessly copying the code and will force you to understand what you are doing.

- I wonder what resources it would contain to help design a software with undo/redo feature.
  - A Merkle-tree data structure + an append only log with checkpoints + a command processor would provide a basic foundation.
  - Your data can be represented in a Merkle-tree. You provide operations add-node, delete-node, move-node etc., on the Merkle-tree and build a command processor that takes as input a checkpointed Merkle-tree snapshot (could be empty when you start) and a log of operations (essentially an sequence of operations). The command processor then applies the series of tree operations in the log to build the final state of the tree. The special checkpoint operation saves a snapshot of the Merkle-tree.
- This basic set of operations should allow you to do unlimited undo/redo/transaction playback capabilities.
- check out emacs' undo-tree for a cool implementation
  - [Emacs has a powerful undo system.](https://www.dr-qubit.org/undo-tree/undo-tree.txt)
  - Unlike the standard undo/redo system in most software, it allows you to recover *any* past state of a buffer (whereas the standard undo/redo system can lose past states as soon as you redo). 
  - Emacs’s undo system is quite frankly amazing. Not only can you recover any state through an arbitrary number of undo and redo operations, but you can also localize the undo/redo operations to a selected region of the buffer.

- ## how would you write an undo system for a raster graphics illustration/painting application?
- https://twitter.com/FreyaHolmer/status/1441541405298630657
  - there's some low hanging fruit - only storing the rectangular region of the pixels that were changed, and its content, would save a lot
  - maybe some RLE compression? especially when the alpha channel is 0, but that would add compression/decompression to the time undo/redo takes
  - then there's also the question of where the data should be stored: GPU-VRAM? RAM? Disk?
- a radical alternative is to store actions on an action stack rather than raster/image data, but, this has massive implications on the architecture of, uh, everything, and has lots of drawbacks that I don't think would make it worth it
- I don’t know if it’s a good way, but what I’ve done in the past is get the delta, changed pixels, between before/after, and use RLE style compression - all non-changed pixels would compress away as “empty”. Applying the delta would undo the action.
- Reapplying deltas to a buffer repeatedly is likely to introduce small variations and possibly artifacts. The only system I'd seen in the past worked via snapshots and a stack of actions. Curious how PS Lightroom works. Has a "complete" history and is non destructive.
- Hm. I wonder if you could take that idea further with a quadtree style structure? Slice down to a min cell size to cull transparent cells... or would that contain too much overhead for the tree? Could make pixel storage more challenging.

  - iirc photoshop does it by storing every version and sharing overlapping data between them using a persistent data structure.

- this is far and away the best solution in my experience, for any kind of editor (outside of implementation practicality). i normally store the entire state each undo step in my tools since like. i'm never working with a lot of data, its super easy to implement and never breaks
- storing the entire state for image editors I feel like wouldn't work because of how much data it involves
  - storing actions means everything needs to serialize and also be reapplyable quickly on undo, and you'd likely need a hybrid model so that you can keyframe every n actions
- hybrid makes a lot of sense! the work with delta is in like. the framework (and fixing consistency bugs). the implementation of each action could definitely be sometimes just pixel data and sometimes purely tool/action information
  - maybe pixel data is the default thing that gets stored, with zero implementation (you just create a new undo state and it gets the pixel data thats changed), then you can add better data for the steps when you need to, like performance optimisations
- the drawback would be that if you have an undo history length of 80 actions, then undoing a single action means reapplying/rerendering 79 things, which, may or may not have been expensive actions, right?not to mention all actions now need to be serializable
- Make the actions reversable. When you draw, capture the data of the pixel you overwrite. That way you can undo by doing the inverse of the do.
  - this is not always possible, many actions are irreversible (gaussian blur, for example)
- Making the actions serializable shouldn't be too hard... For the redo thing, you could smooth it over by caching a certain number of previous states, as tractable. If the state is cached just swap it in; if it's past the cache window then regenerate it

- NSUndoManager on macOS implements a generic version of this
  - [NSUndoManager | Apple Developer Documentation](https://developer.apple.com/documentation/foundation/nsundomanager)

- Every X actions, you make copy of the state and mark it as a checkpoint. Reroll from there.
- Action object that holds everything for the do/undo + push(do), pop(undo) from a stack is good. For doing 80+ things, need to use OpenGL/WebGL which will easily re-render everything quickly. CPU shouldn’t really touch pixel data. E.g. a brush stroke will end up being a GL drawcall

- I briefly worked on a little touchscreen drawing app that never saw the light of day and my plan was a hybrid approach of an action stack and bitmap history - store full-frame bitmaps every few actions, and undo by re-performing just the actions since the most recent snapshot.

- Action stacks would be the way, pen down to pen up as the separator, then everything in between is tweakable (though usually forgotten)

- In my experience, you’ll need this anyway, to unify all ops into a single undo stack. Where an op is reversible, you can store it parametrically, where it isn’t, you have to fall back to storing previous states. That’s when you get into as you said, dirty regions and compression!

- We do this the old-fashioned way: a layer is split up in 64x64 pixel tiles, and we store the before-tiles in the undo/redo action. We don't keep per-stroke data -- though we're considering doing that.
  - neat! seems similar to what SAI is doing judging by the other replies I saw
  - I feel like it makes more sense than my initial idea of saving/loading the bounding rectangle of the changed regions, diagonal strokes and all that

- A good way is to divide image into fixed size blocks (say 64x64). 
  - Before editing a block, make sure it's either exclusively owned, or first copy the block (copy-on-write). Different versions of the image (for undo/redo) share the blocks that haven't changed
  - The blocks need to be reference counted and GC'd so you can determine when a block is no longer used (can be freed), exclusively owned (so you don't need to copy-on-write), or shared (so you need to first COW it before editing)

- Substance Painter stores the strokes in world space.  Which fucking sucks because you can't update your model

- I have a very simple system in rx (http://rx.cloudhead.io) -- I save a compressed snapshot of the canvas everytime it is changed. With google's 'snappy' compression library, the delay is not perceptible for reasonably sized canvases.
  - The problem with implementing brush-based optimizations is that they don't work for other types of edits, eg. flipping the canvas, filling, color replacement etc.

- Continuous undo/redo: record unit over time, use a slider/dial to move backwards or forwards in time.

- Take the diff between your start and end image and store it in a quad tree. Then serialize as byte array and gzip if you want it as small as possible.

- I think I remember a talk from adobe that said something like their canvas is basically a 2d array of pointers rather than values, so when you paint, you're just changing the pointers of those specific pixels allowing low memory footprint and enables things like the history brush
  - [GoingNative 2013 Inheritance Is The Base Class of Evil - YouTube](https://www.youtube.com/watch?v=2bLkxj6EVoM)
  - Had some free time to prototype this. Very good balance between simplicity and memory efficiency

- Refing some stuff other people mentioned in the comments, but keeping a hist of modified but also keeping a space-efficient history of each tile sounds like something a modern GPU's sparse-texture/sparse-residency would perfectly lend itself to
  - Maintain a current-state image, a change happens, you mark the tiles touched, save their state(lots of compression decisions happen here) and an undo would just be rebinding those tiles to that memory, and the older it gets, it goes from vram>ram>disc. Sparse textures are soo good
  - I've reverse engineered Paintool Sai, and they do a tile-based approach. I haven't looked at the undo system in particular, but I have reason to believe that they probably do just-that for their undo system based on how it's their core intermediate format
  - 
- 
- 
- 
- 
