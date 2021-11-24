---
title: lib-editor-collab-crdt-community-stars
tags: [collaboration, community, crdt, editor]
created: '2021-11-24T17:08:48.275Z'
modified: '2021-11-24T17:10:40.462Z'
---

# lib-editor-collab-crdt-community-stars

# discuss

- ## Peritext: a CRDT for rich text
- https://twitter.com/geoffreylitt/status/1463244233389707265
- We've tried to pin down how async edits on rich text should be merged in a bunch of example cases, and proposed an algorithm that just always does the right thing.

- Interesting! Offhand, maybe could store/sync a SQLite table storing the history of CRDT operations, and replay that into a text doc format? Although that table would get fairly large, and wouldn't get the benefit of a custom file format to compress down at all
  - That's pretty much what I want to do - I figure I can have a table of operations and every 10 days or so compress it down to a single savepoint and start building up the operations again to avoid size problems
