---
title: lib-collab-yjs-community-stars
tags: [collaboration, community, yjs]
created: 2022-10-22T18:46:22.507Z
modified: 2022-10-22T18:46:45.456Z
---

# lib-collab-yjs-community-stars

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## ✏️ [Modeling slate split node behavior in YJS - Yjs Community](https://discuss.yjs.dev/t/modeling-slate-split-node-behavior-in-yjs/283)
- Is there a way to perform a slate like split node operation in YJs?
  - Currently I’m modeling a split node operation by removing the 2nd part of the split text from the “origin” node and creating a new text with the removed part, but this leads to issues
- There are two answers to this:
- Answer 1: Use Y. Text
- Answer 2: There is no right solution for splitting nodes
  - Sync conflicts are resolved almost immediately. So in the unlikely case that two users really split the same node concurrently, the users will easily manage to undo one of the splits and continue working together. Shared editing cannot be implemented perfectly and it is impossible to model every intention. Most users will avoid working on the same paragraph anyway when they see the cursor location of another user. So implementing shared cursors already solves this issue.


- ## 🌵 [Document branches like git branches? - Yjs Community](https://discuss.yjs.dev/t/document-branches-like-git-branches/697)
  - I’m wondering if I can build like a branch structure with Yjs docs.
  - My use case, imagine I have a parent document with a lot of work made on it, then we want to make a copy of this document to derivate some content.
  - We should have the possibility to integrate parent changes in our clone, and reversely we want to be able to move back some child content to the parent.
  - And the child document could have different user and access policies, so we want to kindly clean the data.

- So if I want to collapse the metadata at the end, I can simply create a brand new doc and iterate over the previous one to clone the content, so I would have only one clientID and one clock.
  - The clientIDs don’t leak any user information. In order to get rid of stored content, you can simply load the content into a fresh Y. Doc with gc enabled (it is enabled by default).
  - This way you can still merge updates from the original document and vice versa. The metadata that is retained doesn’t leak any user-information or editing snippets. If you tried might be able to recognize editing patterns as you can see how much content was inserted and deleted.

- ## 🆚️🛢️ [How is this different from ShareDB · yjs/yjs _201801](https://github.com/yjs/yjs/issues/93)
- I try to advertise that Yjs is much easier to use, has offline support, and works peer-to-peer. 
- I argue that ShareDB is rather hard to use because you, as a user of the library, have to know about how the data is structured and have to apply transformations on the data. 
  - Yjs provides types that are observable, convenient to use, and have bindings to several editors (Ace, QuillJs, ..).
- There are a lot of things that you can do in Yjs, but you can't do in ShareDB. 
  - For example, you can design a completely distributed application with Yjs (see y-webrtc or y-ipfs). It is also possible to scale Yjs to serve millions of users. 
  - As a comparison, you can open a google docs document with at most 50 users. While ShareDB generally supports more users than that, it is hard to scale ShareDB, because there is only a single source of truth - a single source of failure. This is a limitation of the transformation approach that is used in ShareDB (OT).
  - yjs的计算发生在客户端而不是server

# discuss
- ## 

- ## 

- ## 


- ## [Support for PubSub communication protocol · yjs/yjs_201701](https://github.com/yjs/yjs/issues/63)
- We recently published a paper about the CRDT used it Yjs: yjs.pdf If you are familiar with WOOT: they share some similarities.

- ## [Should we do state management directly with yjs, or through bindings like SyncedStore? - Yjs Community](https://discuss.yjs.dev/t/should-we-do-state-management-directly-with-yjs-or-through-bindings-like-syncedstore/1345)
- It really depends. There are arguably nicer libraries for state management. 
  - Yjs is meant to have a minimalistic interface for observing changes (and calculating differences) that can be integrated into other libraries. 
  - It doesn’t have the reactive interface of mobx, and isn’t immutable like Redux. 
- However, nothing is perfect. Most users of state management libraries don’t think too much about properly organizing data for managing conflicts, optimizing shared data for performance, and migrating existing data to new schemas. 
  - React data stores are, in my opinion, too close to the representation. You likely want to reorganize data when the structure of your application changes. synced-store might make it too easy to make an existing application collaborative. 
  - Instead, you should think very carefully about the schema of your data. Because it’s really hard to change it once you have active users.

- ## 🤔🌲 [How would you model a complex diagram page? - Yjs Community](https://discuss.yjs.dev/t/how-would-you-model-a-complex-diagram-page/2114)
- I have 2 ideas:
  - 1. State as sequence of actions
  - 2. Represent everything as map
  - 3. Integrate yjs deeply into the system and build an object graph

- ## 🌲 [Full JSON representation](https://github.com/yjs/yjs/issues/284)

- One of the advantages of using a JSON structure it because it is a bit more human readable. 
  - In our case we save snapshots of the document in json format that can be queried afterwards. 
  - We save it by doing `doc.toJSON()` and we also have a recursive function that allows us to recreate a document from a JSON structure that we previously saved.
  - That also decouples us from YJS, so in the future if we need to migrate away from YJS we already have the data in a JSON structure.
  - I know this is a different case than what is proposed here, but I wanted to contribute some ideas that we are using.

- The biggest use case for JSON is not just in Human Readability you could just use Yjs 's toJSON() for logging / debugging. JSON is ubiquitous, nearly every open source project in every language uses it as the encoding for transport / state.
  - I am working with a new Text Editing framework that gives its state as a JSON. If I have to use Yjs here I will constantly be converting the JSON to Yjs Map / Array for every keystroke and vice versa.
- If I have to use Yjs here I will constantly be converting the JSON to Yjs Map / Array for every keystroke and vice versa.
  - 👉🏻 This might in fact be the best move here. You could probably develop an intermediate representation that allows you to efficiently map changes from the JSON state to the Yjs state without having to re-parse the entire structure every time. While not as efficient as using Yjs types directly, it could still be adequately performant, and would allow a wide variety of other tools to integrate with Yjs.
- Yes, you can definitely map the Yjs state to a JSON(-like) object. I recommend SyncedStore or alternatives listed in the readme or the forum.
  - Mapping CRDT state to a JSON object is out of scope for the Yjs package. This should be provided by a separate module.

- You might wanna look into Ron which aims to standardize encoding in different encodings. 
  - I like the approach, but I can't use it in Yjs because it implements a unique, heavily optimized encoder.
  - [Replicated Object Notation — RON](http://replicated.cc/)
  - SwarmDB is a proof-of-concept key-value RON store

- The original question was about representing the CRDT updates in a JSON representation for logging purposes. 
  - I provided functions to convert updates to a JSON format for debugging. However, most people won't be able to understand the generated state changes as one would need to understand how the CRDT works. 
  - Even then, it is basically impossible to read useful data out of them as they are only useful for debugging a CRDT. 
  - You always need to apply updates to a Yjs document (or Yrs, Ypy, ..).
- There are still so many projects that transport the Yjs updates as a JSON Array (instead of using base64) which makes me sad. So many wasted bytes... 
  - So I can't stress this enough. Never ever transport Yjs updates as-is in a JSON object. Use base64 if you must
- 👉🏻 CRDTs that use JSON encoding generally don't perform well in JavaScript. 
  - Parsing JSON is expensive and allocates memory inefficiently. 
  - I indirectly make use of the fact that modern JavaScript engines optimize memory allocation of the same object (in Yjs the "Item" class). 
- Another advantage of the Yjs encoder is that it achieves high compression at no cost without using an expensive generic compression algorithm (e.g. zip). 
  - In some cases, the encoder achieves 300x better compression rates & 1000x better performance than other CRDTs that use JSON encoding
- I'm a big fan of immutable state. But I believe that this is not the correct solution for implementing a CRDT. However, you should be able to implement immutable state on-top of Yjs(zustand-yjs). 
- The advantage of JSON encoding is that it is human-readable. But CRDTs that use JSON encoding don't perform well in practice. With compression techniques like RLE encoding, variable-length encoding, and tabular encoding we can make CRDTs viable in practice. For this reason, I don't recommend JSON encoding as a go-to solution.

- My motivation is to create some sort of a standard like JSON Patch, but something for CRDTs, I guess something like RON but dedicated to JSON data type.
- I'm not sure if it is feasible to create a JSON representation just for the sake of using JSON instead of binary encoding. I still don't understand the advantages.
  - For manipulating content you should rather use the methods that are provided by Yjs. You could also add functionality for Yjs to accept changes that are expressed in the JSON Patch format. Yjs already supports the Quill Delta format, which was originally developed for Operational Transformation.
  - I feel you might be interested in something like the json1 type in @ottypes

- ## [Is it possible to use yjs for collaboration over a nested object (modeled as a JSON object)?)? - Yjs Community](https://discuss.yjs.dev/t/is-it-possible-to-use-yjs-for-collaboration-over-a-nested-object-modeled-as-a-json-object/102)
- The Yjs data types are more expressive as JSON. 
  - You can model any JSON document using Yjs types.
- JSON is just an encoding technique. 
  - In JavaScript, you can efficiently express complex data structures using the JSON consisting of Object, Array, and primitive data types (number, string, …). 
  - You can model any Object as a Y. Map, and you can model any Array as a Y. Array. 

- ## [Extending Yjs Types without breaking everything - Yjs Community](https://discuss.yjs.dev/t/extending-yjs-types-without-breaking-everything/769)
  - I came with the idea to create custom Yjs types to extends defaults shared types methods and to get a better type experience DX, code clarity etc.
  - `export class YColumn extends Map<any> {` 继承
  - But when we encode state as update or play with the history, custom types are loss with their functionalities and the app crashes as expected.
- I tackled this via composition rather than inheritance, as I ran into similar roadblocks.
- The way I have “solved” it temporarily is instead of using inheritance, Extend the prototype

- ## [History of collaborative editing solutions. What usually people used before automerge, yjs etc.. ?](https://github.com/automerge/automerge/discussions/496)
  - I found automerge (2017), yjs (2015), sharedb (2013). All of them are relatively new.

- Before CRDTs came along, the main technology for real-time collaboration on text documents was Operational Transformation (OT); 
  - the most common algorithm was introduced by the Jupiter system at Xerox PARC in 1995, and adopted by Google Docs in 2010. 
  - Jupiter assumes that all edits flow via a central server. 
- CRDTs arose from the difficulty of making p2p OT work, and represented a new start using a completely different approach. 
  - The idea only appeared around 2006 or so, and early implementations were very inefficient. 
  - It took perhaps a decade for the CRDT algorithms to be refined to the point where you could use them for non-trivial documents.
- Interestingly, the world of multiplayer games is totally separate: afaik, very few people in the collaboration software community know what techniques are used in games and vice versa. 
  - my take-away from this is that the needs of games and application software are sufficiently different that it does not make much sense to share techniques. 
