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

- npm test
- Uncaught Error: cannot call iterator() before open()
  - x2
- done() called multiple times in hook
  - x2
- Uncaught Error: Callback was already called.
  - x1
# issues
- ## [A doc can be written to index w/o being saved](https://github.com/Ivshti/linvodb3/issues/16)
  - Somehow, a document can end up being written to an index without being saved yet. It's either the save or update methods

- Actually, this turns out to be by design. In most cases, docs are written to the indexes and afterwards commited. This is a tough one

- The way to fix this is actually simple
  - Upon the `_persist` function, write to a cache `saving[]`. 
  - When the doc is committed to levelup, delete it from that cache.
  - Modify `cursor.getMatchesStream` to use this cache if the doc is there
