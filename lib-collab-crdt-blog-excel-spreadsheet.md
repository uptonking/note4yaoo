---
title: lib-collab-crdt-blog-excel-spreadsheet
tags: [blog, collaboration, crdt, excel, spreadsheet]
created: 2023-10-28T09:03:59.953Z
modified: 2023-10-28T09:04:42.521Z
---

# lib-collab-crdt-blog-excel-spreadsheet

# guide

# blogs

# 📈 [Conflict-free Replicated Spread Sheets_202310](https://www.bartoszsypytkowski.com/crdt-tables/)

- Before going to implementation details, let's specify the characteristics of the spread sheets workloads. Once data volume grows, its impossible to optimize the data structure for all work patterns. We need to pick our battles. For this reason we need to construct some initial assumptions:
  - Some spread sheets can consists of hundreds of columns and (in some cases) hundreds of thousands of rows. For this reason, the size of metadata per row (and per cell) matters.
  - Relative position of rows is usually not that important - unless we apply specific ordering rules (like order rows by column X), the insertion order rarely changes the meaning of the entire context. This is very much in contrast to ie. text editors where preserving the intended order of inserted characters is a grave matter. For that reason we acknowledge `interleaving` as an acceptable tradeoff.
  - The majority of changes come from cell updates, including deletion of cell contents. Our conflict resolution should work on cell level not row level
  - The majority of inserts are actually appends of consecutive ranges of rows and columns, including copy/pasting massive amount of rows from another source. Inserting rows in between existing rows can happen but it's less common than ie. in case of text editors.
  - Even if our sheet has thousands of rows, we usually render only a handful of them (adjacent to each other within window boundaries) at the time. For this reason its good to keep similarity between how rows are presented to a user, and their actual in-memory layout

- 🧮 we're going to keep track of inserted columns and rows by using LSeq data structure: represented in our case as array of fractional keys. 
  - While we did describe LSeq in the past, let's gloss over it very quickly: linear sequence inserts elements at index i by generating key for new inserted entry, that's lexically smaller than the key at position i+1 and greater than the key at position i-1.
- What's important here is that, neighbour keys are needed only during key generation time, not a conflict resolution time. 
  - It means that if we can guarantee causality of our operations (and prevent duplicate updated), we don't need to preserve tombstones of removed elements.
- That being said, our implementation uses tombstones simply because we don't use replication protocol that preserves causality - we simply shove updates around. With a protocol capable of deduplicating updates we wouldn't need them.

- When working with spread sheets, quite often we want to be able to select a window of data. 
  - Using markers like `A1:B3` mentioned above has common problem: they represent current order as observed by user. When other users will start to concurrently insert/remove rows or cells, these positions may no longer refer to fragments of data we intended them to. 
  - For this reason, we're going to represent our selections as a combination of two opposite points using logical indexing (our fractional keys) instead

- Keep in mind that when we're referring to ranges, we actually what to refer to spaces between elements at given indexes - hence notion of left/right side inclusive/exclusive ranges. 
  - Same problem concerns windows of data. This usually requires keeping additional flags around. 
- Moreover, if we want to mark an entire range of values (eg. all current and future elements of a row/column), we need additional way to describe it as well.

- we'd need to add some degree of reactivity: whenever a value inside of selection changes, we need to recompute formulas in all affected cells. For that we may need to quickly locate selections containing given cell or those that intersect with updated range ie. when we copy paste area of cell values at once.
  - With small number of listening selections, doing a brute force check over all of them may be probably enough.
- Indexing selections for fast constains/overlaps search operations may sound like a hard problem. However in the past we already covered concept of index structures optimized for multi-dimensional values: R-Trees. Below you can see how databases like Postgres use R-Tree to recursively split search space to improve lookups of geographical data.

- R-Tree is build on B+Tree, where we have a fixed-size nodes of keys/areas (here: selections). 
  - Keys in each node can be summarized as another selection that fits them all within its boundaries. This way keys can be grouped and build a recursive hierarchical tree structure. 
  - When node is full and a new selection needs to be inserted, we split that node in two and assign existing values as follows - pick two selections that are most far away from each other as seeds for newly created buckets, then split remaining values from old bucket by computing how much area covered of each bucket would grow if that key would have to be added there and pick the one where this growth rate is lower.

- if we're talking about LSeq, we can technically implement move(source, destination) as simple delete+upsert (with a little twist)

- The table we described here is row-oriented (array of rows). However when it comes to serialization, it turns out that serializing data by columns is often more feasible. It's because cells existing in the same columns are more likely to have the same data type, and having the same type can make a huge difference.

- [R-Tree: algorithm for efficient indexing of spatial data_202204](https://www.bartoszsypytkowski.com/r-tree/)

- https://github.com/Horusiath/crdt-table /5Star/GPLv3/202309/js
  - This is proof of concept for Conflict-free Replicated Data Type representing 2-dimensional table
  - Insert or update existing rows (conflict resolution timestamp per cell basis)
  - Insert new series of rows in between existing rows.
  - 🔀 Row/column inserts are resolved using `LSeq` - while it has interleaving issues, we believe its not that important on that field as when it comes to ie. collaborative text editing.
    - Cell updates and cell updates against row/column deletions are resolved using Last-Write-Wins semantics.
    - There's a minimal overhead related to keeping tombstone information when entire rows/columns are deleted. This could also be shifted to partially ordered log for keeping info about commutative updates.
  - This implementation uses a combination `{HybridLogicalTimestamp,PeerID}` as a means of conflict resolution, which on positive side is quite lightweight, but otherwise is pretty cumbersome: 😩 possible clock drifts on client devices; 😩 no ability to recognize concurrent updates ie. conflict resolution for things like update cell / delete column now depends on the clock timestamp
    - Easiest proposal is to switch to vector versions, with optional clock timestamps where useful, but they can be quite heavy (especially if used on per cell basis). 
    - Another proposal is to use partially-ordered log to detect concurrent conflicts (which would be also usefull ie. for undo/redo feature).
  - Selections represents focused areas within a table/grid. In this PoC selections defined by user API using similar `{row:number,col:number}` pairs of opposite corners, however as row and column numbers can change under concurrent updates, **the internal representation of selection uses fractional keys (keys used internally by `LSeq` to establish order)**.
    - Quite often we need to react on changes happening within the boundaries of the selection.This requires efficient way to find selections that contain given cell or intersect with range of changed cells (ie. when we copy paste multiple rows/columns).
    - For small number of selection brute(纯体力的) force over all known selections wouldn't be an issue. 
    - For bigger number, we could modify indexing structures for 2-dimensional data such as R-Trees (used ie. to index geospatial data).
# more

# discuss-excel-collab

- ## 

- ## 

- ## 

- ## Multiplayer sync with spreadsheets is so unbelievable complicated, even after multiple years of working on it, it still makes my head spin.
- https://twitter.com/AJNandi/status/1760740582480335208
- Toy examples with a handful of cells and formulas are really easy to build with some off the shelf sync providers, and are great learning examples.
- But as soon as you get to anywhere above an average spreadsheet of ~1k rows, everything gets way more complex.
- You've got to handle things like
  - batching of thousands of cells changing in a single command
  - lazy instantiation of cells, rows, columns that don't exist yet but are referenced in formulas
  - communicating with web workers to run calculations off the main thread
  - immutable references to mutable cell addresses like A1, B5 etc.
  - ... there's probably 15 other things I could complain about, lmk if you're curious!
