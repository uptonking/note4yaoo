---
title: lib-collab-crdt-blog-excel-spreadsheet
tags: [blog, collaboration, crdt, excel, spreadsheet]
created: 2023-10-28T09:03:59.953Z
modified: 2023-10-28T09:04:42.521Z
---

# lib-collab-crdt-blog-excel-spreadsheet

# guide

# blogs

# 🪟 [Conflict-free Replicated Spread Sheets_202310](https://www.bartoszsypytkowski.com/crdt-tables/)

- https://github.com/Horusiath/crdt-table /5Star/GPLv3/202309/js
  - This is proof of concept for Conflict-free Replicated Data Type representing 2-dimensional table
  - Insert or update existing rows (conflict resolution timestamp per cell basis)
  - Insert new series of rows in between existing rows.
  - Row/column inserts are resolved using `LSeq` - while it has interleaving issues, we believe its not that important on that field as when it comes to ie. collaborative text editing.
    - Cell updates and cell updates against row/column deletions are resolved using Last-Write-Wins semantics.
    - There's a minimal overhead related to keeping tombstone information when entire rows/columns are deleted. This could also be shifted to partially ordered log for keeping info about commutative updates.
  - This implementation uses a combination `{HybridLogicalTimestamp,PeerID}` as a means of conflict resolution, which on positive side is quite lightweight, but otherwise is pretty cumbersome: possible clock drifts on client devices; no ability to recognize concurrent updates ie. conflict resolution for things like update cell / delete column now depends on the clock timestamp
    - Easiest proposal is to switch to vector versions, with optional clock timestamps where useful, but they can be quite heavy (especially if used on per cell basis). 
    - Another proposal is to use partially-ordered log to detect concurrent conflicts (which would be also usefull ie. for undo/redo feature).
  - Selections represents focused areas within a table/grid. In this PoC selections defined by user API using similar `{row:number,col:number}` pairs of opposite corners, however as row and column numbers can change under concurrent updates, **the internal representation of selection uses fractional keys (keys used internally by `LSeq` to establish order)**.
    - Quite often we need to react on changes happening within the boundaries of the selection.This requires efficient way to find selections that contain given cell or intersect with range of changed cells (ie. when we copy paste multiple rows/columns).
    - For small number of selection brute(纯体力的) force over all known selections wouldn't be an issue. 
    - For bigger number, we could modify indexing structures for 2-dimensional data such as R-Trees (used ie. to index geospatial data).
# more
