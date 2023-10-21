---
title: lib-collab-crdt-blog-vendors
tags: [blog, collaboration, crdt, vendor]
created: 2023-05-30T15:50:07.368Z
modified: 2023-05-30T15:50:39.683Z
---

# lib-collab-crdt-blog-vendors

# guide

# blogs

## [Ditto Delta State CRDT](https://docs.ditto.live/javascript/common/how-it-works/crdt)

- [Extend Hybrid Logical Clock documentation](https://github.com/getditto/docs/issues/413)

- The Ditto document is a JSON like document made from a CRDT Map that represents the JSON Object. 
  - The JSON properties are map keys, and the values are any of the Counter/Register/Map types
  - One way to think about the types that make up a Ditto document is like a tree, where there are collections (Array and Map) and leaf values that are registers or counters.
  - Register: A single primitive value (Number, String, Boolean, Binary File)
  - Counter: A special number capable of preserving incrementing and decrementing semantics
  - Map: A dictionary of name->value mappings

- The foundation of determining how data should be merged is using a Ditto document's **version vector**.
  - Every time a change is made to a document, the version of that document is incremented by one. 
  - When a peer incorporates changes from other peers, the local peer can use the incoming remote peer's version vectors to determine whether the changes are new or old. 

- Each document in each peer contains a hidden metadata map of a `Site_ID` and a `HLC`. 
  - The HLC stands for a hybrid logical clock. This HLC is used to determine whether a change has "happened before".
  - Ditto uses a `UInt128` to represent the `Site_ID` and `64bit` timestamp for the `HLC`. But for educational purposes, this documentation will often use strings and numbers for readability.
- In Ditto's distributed system, the HLC is a `64-bit` timestamp comprised of `48 bits` of a physical timestamp and `16 bits` of a monotonically increasing logical clock.

## [Using Ditto as a Local Database](https://ditto.live/blog/local-database)

- you can use Ditto in your apps as a regular document database

## [jupyterlab-rtc: We can class the RTC Algorithms into 3 main categories crdt/ot/diff](https://jupyterlab-rtc.readthedocs.io/en/latest/about-rtc/algorithms.html)

- We can class the RTC Algorithms into 3 main categories:
  - CRDT category doesn’t need a central server and is used by Riak, TomTom GPS, Teletype for Atom…
  - OT category needs a central server and is used by Google Docs, Office365…
  - Diffs category used by Cocalc

## [zed: How CRDTs make multiplayer text editing part of Zed's DNA_2022212](https://zed.dev/blog/crdts)

# more
- [Collaborative and Offline Editing Using CRDTs • Decipad's Blog_202309](https://www.decipad.com/blog/decipads-innovative-method-collaborative-and-offline-editing-using-crdts)
