---
title: lib-collab-yjs-docs
tags: [collaboration, docs, yjs]
created: 2022-04-05T10:11:07.891Z
modified: 2022-04-05T10:11:21.023Z
---

# lib-collab-yjs-docs
# [Yjs Internals](https://github.com/yjs/yjs/blob/main/INTERNALS.md)


- The Yjs CRDT algorithm is described in the YATA paper from 2016.
- At its heart, Yjs is a list CRDT. 
  - Everything is squeezed into a list in order to reuse the CRDT resolution algorithm
  - Arrays are  lists of arbitrary items.
  - Text is a list of characters, optionally punctuated(不时打断) by formatting markers and embeds for rich text support. 
  - Maps are lists of entries. The last inserted entry for each key is used
- Each client is assigned a unique clientID property on first insert. js-safe random 53-bit integer


- Deletions in Yjs are treated very differently from insertions. 
  - 👉🏻 Insertions are implemented as a sequential operation based CRDT, but deletions are treated as a simpler state based CRDT.
# yjs-docs

- Yjs documents are collections of shared objects that sync automatically.

- Yjs doesn't make any assumptions about the network technology you are using. 
  - As long as all changes eventually arrive, the documents will sync. 
  - The order in which document updates are applied doesn't matter.
- Most shared editing solutions depend on a single source of truth - a central server - to perform conflict resolution. 
  - Yjs doesn't need a central source of truth. This enables you to design the backend using ideas from distributed system architecture. 

- Editor bindings are a concept in Yjs that allow us to bind the state of a third-party editor to a syncable Yjs document. 
  - The `ytext` object is a shared data structure for representing text. It also supports formatting attributes (i.e. bold and italic). 
  - Yjs automatically resolves concurrent changes on shared data so we don't have to worry about conflict resolution anymore. 
  - Then we synchronize ytext with the quill editor and keep them in-sync using the QuillBinding. 
  - Almost all editor bindings work like this. 

- editor doesn't sync to other clients yet! We need to choose a provider or implement our own communication protocol to exchange document updates with other peers.
- Providers sync Yjs documents through a communication protocol or a database. 
  - Most providers have in common that they use the concept of room-names to connect Yjs documents.
- Providers are meshable. 
  - You can connect multiple providers to a Yjs instance at the same time. 
  - Document updates will automatically sync through the different communication channels. 
  - Meshing providers can improve reliability through redundancy and decrease network delay.

- Awareness 
  - By sharing cursor locations and presence information, we help our users to actively work together. 
  - Most applications also assign a unique name and color to each user. 
  - This kind of information can be generally classified as "Awareness" information. 
  - It gives you hints about what other users are currently doing.
- We could share even more awareness information like the mouse position of each user, or a live video recording of each user. 
  - But when we share too much information, we distract our users from the task at hand. 
  - So it is important to find the right balance, that makes sense for your application.
- Awareness information isn't stored in the Yjs document, as it doesn't need to be persisted across sessions. 
  - Instead, we use a tiny state-based Awareness CRDT that propagates JSON objects to all users. 
  - When you go offline, your own awareness state is automatically deleted and all users are notified that you went offline. 
  - While this feature is optional, it is recommended that network providers implement the awareness protocol to make it easier to switch providers. 
- The fields of the Awareness CRDT are not standardized. You can set any JSON-encodable value.

- network providers sync document updates over a network protocol to other peers. 
  - Database providers sync document updates to a database.

- Shared types allow you to make every aspect of your application collaborative.
- Shared types are similar to common data types like Array, Map, or Set. 
  - The only difference is that they automatically sync & persist their state (using the providers) and that you can observe them.
- Shared type instances must be connected to a Yjs document so we can sync them. 
  - First, we define a shared type on a Yjs document. 
  - Then we can manipulate it and observe changes.
- You can even insert Yjs types, allowing you to create nested structures
  - Note that the above observer doesn't fire when you insert content into subArray
  - You need to create an observer on subArray instead
  - Alternatively you can observeDeep on yarray (allowing you to observe child-events as well)
- You can't insert the array at another place. A shared type can only exist in one place.
yarray.insert(0, [subArray]) // Throws exception!

- There are some things that are not possible with shared types, but that are possible with normal data types. 
  - Most importantly, it is not possible to move a type that was inserted into a Yjs document to a different location. 
  - The other important caveat is that you shouldn't modify JSON that you inserted or retrieved from a shared type. 
  - Yjs doesn't clone the inserted objects to improve performance. 
  - So when you modify a JSON object, you will actually change the internal representation of Yjs without notifying other peers of that change.

- All changes must happen in a transaction. 
  - When you mutate a shared type without creating a transaction (e.g. yarray.insert(..)), Yjs will automatically create a transaction before manipulating the shared object.
- Event handlers and observers are called after each transaction. 
  - If possible, you should bundle as many changes in a single transaction as possible. 
  - The advantage is that you reduce expensive observer calls and create fewer updates that are sent to other peers.
- Especially when manipulating many objects, it makes sense to reduce the creation of update messages. So use transactions whenever possible.

- We often want to manage multiple collaborative documents in a single Yjs document. 
  - You can manage multiple documents using shared types.

- Shared types are not just great for collaborative editing. 
  - They are a unique kind of data structure that can be used to sync any kind of state across servers, browsers, and soon also native applications.

## api

- Positions may represent cursor locations, selection ranges, or even assign a comment to a range of text. 
  - Normal index-positions (expressed as integers) are not convenient to use because the index-range is invalidated as soon as a remote change manipulates the document. 
  - Relative positions give you a powerful API to express positions.
- A relative position is fixated to an element in the shared document and is not affected by remote changes. 
- Relative positions are guaranteed to always point to the same location ⇒ When all clients sync up, all relative positions will translate to the same index-position. This is not possible in OT-like solutions
