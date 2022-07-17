---
title: lib-collab-crdt-examples
tags: [collaboration, crdt, examples]
created: 2022-01-22T16:14:32.323Z
modified: 2022-04-05T10:08:25.947Z
---

# lib-collab-crdt-examples

# guide

# popular

# yjs-crdt
- https://github.com/yousefed/SyncedStore
  - https://syncedstore.org/docs/
  - SyncedStore CRDT is an easy-to-use library for building live, collaborative applications that sync automatically.
  - SyncedStore builds directly on Yjs and Reactive. It's also inspired by and builds upon the amazing work by MobX and NX Observe.
  - SyncedStore is built as part of TypeCell.
  - So far, we've focused mostly on how to change to state on a synced store, and how to listen (react to) changes and display them in your application.
    -  When you update data on the store, an incremental change, or update is captured and can be shared between users. These updates can be shared between users of your application with different Sync Providers. 
  - y-indexeddb for offline storage​
    - persists document updates to the browsers indexeddb database. 
    - The document is immediately available and only diffs need to be synced through the network provider.
  - https://github.com/YousefED/reactive
    - A super simple, yet powerful and performant library for State Management / Reactive Programming.
- https://github.com/inkandswitch/peritext
  - https://www.inkandswitch.com/peritext/
  - A CRDT for asynchronous rich-text collaboration, where authors can work independently and then merge their changes.
  - This repo includes:
    - A Typescript implementation of the core Peritext CRDT algorithm
    - A prototype integration with the [Prosemirror](http://prosemirror.net/) editor library
    - An interactive demo UI where you can try out the editor
    - A test suite
# examples

# crdt-repos
