---
title: lib-db-linvodb-issues-not-yet
tags: [issues, linvodb]
created: 2022-12-24T10:02:14.250Z
modified: 2022-12-24T10:02:30.813Z
---

# lib-db-linvodb-issues-not-yet

# guide

# not-yet

## testing-errors

# issues
- ## [A doc can be written to index w/o being saved](https://github.com/Ivshti/linvodb3/issues/16)
  - Somehow, a document can end up being written to an index without being saved yet. It's either the save or update methods

- Actually, this turns out to be by design. In most cases, docs are written to the indexes and afterwards committed. This is a tough one

- The way to fix this is actually simple
  - Upon the `_persist` function, write to a cache `saving[]`. 
  - When the doc is committed to levelup, delete it from that cache.
  - Modify `cursor.getMatchesStream` to use this cache if the doc is there

- ## [Performance issues](https://github.com/Ivshti/linvodb3/issues/78)
  - What I've observed so far is that queries seem to take a very long time when the number of documents returned is large, however the queries speed up if the number of returned documents is small.
  - Based on these numbers, it seems that the slowness isn't on the search via index but rather the operation(s) involved with loading the documents. The more documents that need to be loaded, the slower the query gets.

- This is a known issue, although unfortunately I have not investigated. Maybe you can look into the cursor.js code and check how long the index takes, and then how long the retrieval takes.
  - My experience is that the index is OK in terms of speed, but then taking the data out of the store can take a while for various reasons - my suspicion is that it's time lost in levelup/leveldown abstractions
  - Maybe you can try with another store (try with memdown) to see what will happen

- ## [Remove `async` dependency · Pull Request · seald/nedb](https://github.com/seald/nedb/pull/11)
  - The goal of this PR is to remove the async dependency, and maybe expose a fully retrocompatible promise-based API.
  - [Race condition & database corruption may happen when calling `ensureIndex` · Issue #9 · seald/nedb](https://github.com/seald/nedb/issues/9)
