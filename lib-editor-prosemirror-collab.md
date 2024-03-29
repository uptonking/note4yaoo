---
title: lib-editor-prosemirror-collab
tags: [collaboration, editor, prosemirror]
created: 2021-10-14T05:02:01.304Z
modified: 2021-10-14T05:03:19.234Z
---

# lib-editor-prosemirror-collab

# not-yet

- not-yet-基于crdt实现text文本协作的问题
  - 对不同分支的文档在相同位置粘贴相同的文本时，crdt会保留重复的文本

- ❓️ 基于轮询的服务端和基于socket的服务端示例，是如何决定接收一个op，然后拒绝其他op的
  - If two editors make changes concurrently, they will both go to this authority with their changes. 
  - The authority will accept the changes from one of them, and broadcast these changes to all editors. 
  - The other's changes will not be accepted, and when that editor receives new changes from the server, it'll have to rebase its local changes on top of those from the other editor, and try to submit them again.
# guide
- [Collaborative Editing in CodeMirror_202005](https://marijnhaverbeke.nl/blog/collaborative-editing-cm.html)
- To recap, ProseMirror uses something similar to OT, but without a converging transformation function. 
  - It can transform changes relative to each other, but not in a way that guarantees convergence. 
  - ProseMirror's document structure is a tree, and it supports various types of changes, including user-defined changes, that manipulate this tree. 
  - I didn't have the courage to try and define a converging transformation function there. 
  - When a client receives conflicting remote changes, it first undoes all its local pending changes, applies the remote changes, and then the transformed form of its local changes. 
  - This means that everybody ends up applying the changes in the same order, so convergence is trivial.
# blogs

## [Manuscripts | Living Pixel](https://livingpixel.io/work/manuscripts)

- From 2019-2022 I was one of the principal engineers on Manuscripts.io, a platform for authoring, editing, and submitting scientific publications on the web. 
  - I contributed code primarily impacting the rich-text editing experience within the browser, as well as solutions for data synchronization and conflict resolution. 
- The editing experience in Manuscripts was based on ProseMirror, and data were serialized and stored in a local PouchDB database. 
  - The collaborative (possibly offline) editing experience was provided by a syncing protocol which required a git-like merge resolution system that was understandable by non-programmers. 
  - Later we built a change-tracking system on top of that.
- The project has been retired by Atypon, but the main repository is available on GitLab.
  - https://gitlab.com/mpapp-public/manuscripts-frontend

## 🌰 [Collaborative text editor with ProseMirror and a syncing database_202007](https://emergence-engineering.com/blog/prosemirror-sync-1)

- [blog src code](https://gitlab.com/emergence-engineering/blog/-/tree/master/articles/prosemirror-sync-1)

- tldr
  - web-based collaborative editor based on ProseMirror
  - use PouchDB (CouchDB) to abstract away all the hassle that comes with directly managing WebSockets
  - Any database with real-time syncing functionality can be used

- Although the `prosemirror-collab` module is not very hard to use, a communication layer is necessary for the clients to receive new steps to update their local document, keeping them in sync. 
  - This is usually done with WebSockets, which adds another layer in the stack where bugs can hide. 
  - This article shows a path to get rid of that layer by using a well-tested layer in the form as a syncing database. (PouchDB/CouchDB)
  - This approach has also been tested with Firestore.

- You can follow the steps (changes) that are emitted from the active editor in the ClientSteps list table. Here you can see all the steps that are being sent from the clients.
- The ServerSteps list table displays the history of the valid conflict free steps ( changes ). Each of these steps has a version just like git commits.

- step: an object which describes the necessary information to update a document ( like add/delete a letter from a given position in a document.
- ProseMirror document version: A version of the document starts from 0 and incremented every time a new step is applied.

- Sync database: A database which is capable of automatically replicating the state of a remote database, so they both contain the same content eventually. For example CouchDB, Google Firestore etc...
- PouchDB: A JS implementation of the CouchDB protocol. This means that it can run in the browser, and sync up to another database which implements the CouchDB protocol.
- listener: A callback which is called every time the there is new data in the database

- This is very similar to a REST API, but the server now can push data to the clients directly. 
  - Of course this can be done with just WebSockets ( and that's what behind the implementation of most sync databases ), 
  - but that's usually a quite complex hard-to-test part, and using a well-tested database has some obvious benefits in that sense. 

- In this demo there are two ProseMirror editors and each of them has a dedicated PouchDB instance. 
  - These databases sync up to a third database, which belongs to a "server". 
  - If client A is updated, then the server is updated which ideally propagates client B.

- we use PouchDB for this demo which is a JavaScript implementation of the CouchDB protocol. There are three collections:
  - 1. PMDocument: stores the ProseMirror document
  - 2. ClientSteps: stores the steps coming from the clients
  - 3. ServerSteps: stores the steps accepted by the server

- Data flow on the server
  - The server listens to new documents in ClientSteps
  - If the version of the steps is correct, the client is synced up to the server
  - And finally: the server updates the ProseMirror document stored in PMDocument ( referenced by the incoming step ) and saves the accepted steps to ServerSteps

- Data flow on the clients
  - postSteps.ts is called by ProseMirror whenever there is an incoming ProseMirror transaction ( either the user did something in the editor, or the server sent new steps coming from another user ). 
  - In that function, sendable steps are calculated by the prosemirror-collab module, and if there's any then they are written to the database as ClientSteps. 
  - The ProseMirror view is also updated.
  - only listens to the step in ServerSteps which has the version that updates the current document. I

-  Offline functionality is also possible with the same structure ( with some added code ), but keep in mind that ProseMirror's collaborative feature is not meant for offline use and it is possible to lose some information ( for example if a user typed into an existing paragraph when offline, and then the paragraph is deleted then the information is lost ), but in general, it works great.
# [Collaborative Editing in ProseMirror__201507](https://marijnhaverbeke.nl/blog/collaborative-editing.html)

## [「译」ProseMirror 中的协同编辑实现](https://www.xheldon.com/tech/Collaborative-Editing-in-ProseMirror.html)

- Unlike OT, it does not try to guarantee that applying changes in a different order will produce the same document.

- Unlike in git, the history of the document is linear in this model, and a given version of the document can simply be denoted by an integer.
- Also unlike git, all clients are constantly pulling (or, in a push model, listening for) new changes to the document, and track the server's state as quickly as the network allows.

- my initial impulse was to split ReplaceStep up into steps that remove and insert content. But because the position map created by a replace step needs to treat the step as atomic (positions have to be pushed out of all replaced content), I got better results with making it a single step.

- For doing offline work (where you keep editing when not connected) or for a branching type of work flow, where you do a bunch of work and then merge it with whatever other people have done in the meantime, the model I described here is useless (as is OT).
  - In cases like this, I think a diff-based approach is more appropriate.

## The Problem

- A real-time collaborative editing system ensures that the documents stay synchronized—changes made by individual users are sent to other users, and show up in their representation of the document.
- Since transmitting changes over any kind of network is going to take time, **the complexity of such systems lies in the way they handle concurrent updates**.
- One solution is to allow users to lock the document (or parts of it) and thus prevent concurrent changes from happening at all. 
  - But this forces users to think about locks, and to wait when the lock they need is not available. We'd prefer not to do that.
- If we allow concurrent updates, we get situations where user A and user B both did something, unaware of the other user's actions, and now those things they did have to be reconciled. 
  - The actions might not interact at all—when they are editing different parts of the document—or interact very much—when they are trying to change the same word.

## Operational Transformation

- A lot of this research is about truly distributed systems, where a group of nodes exchange messages among themselves, without a central point of control. 
  - The classical approach to the problem, which is called Operational Transformation, is such a distributed algorithm. 
- It defines a way to describe changes that has two properties
  - You can transform changes relative to other changes. So if user A inserted an “O” at offset 1, and user B concurrently inserted a “T” at offset 10, user A can transform B's change relative to its own change, an insert the “T” at offset 11, because an extra character was added in front of the change's offset.
  - No matter in which order concurrent changes are applied, you end up with the same document. This allows A to transform B's change relative to its own change, and B to transform A's change similarly, without the two users ending up with different documents.
- An Operational Transformation (OT) based system applies local changes to the local document immediately, and broadcasts them to other users. 
  - Those users will transform and apply them when they get them. 
  - In order to know exactly which local changes a remote change should be transformed through, such a system also has to send along some representation of the state of the document at the time the change was made.
- That sounds relatively simple. But it is a nightmare to implement. 
  - Once you support more than a few trivial types of changes (things like “insert” and “delete”), ensuring that applying changes in any order produces the same document becomes very hard.

## Centralization

- The design decisions that make the OT mechanism complex largely stem from the need to have it be truly distributed. 
  - Distributed systems have nice properties, both practically and politically, and they tend to be interesting to work on.
- But you can save oh so much complexity by introducing a central point. 
  - I am, to be honest, extremely bewildered(困惑的) by Google's decision to use OT for their Google Docs—a centralized system.

- **ProseMirror's algorithm is centralized**, 
  - in that it has a single node (that all users are connected to) making decisions about the order in which changes are applied. 
  - This makes it relatively easy to implement and to reason about.
- And I don't actually believe that this property represents a huge barrier to actually running the algorithm in a distributed way. 
  - Instead of a central server calling the shots, you could use a consensus algorithm like Raft to pick an arbiter.

## The Algorithm

- Like OT, ProseMirror uses a change-based vocabulary and transforms changes relative to each other.
- Unlike OT, it does not try to guarantee that applying changes in a different order will produce the same document.

- By using a central server, it is possible—easy even—to have clients all apply changes in the same order. 
  - You can use a mechanism much like the one used in code versioning systems. 
  - When a client has made a change, they try to push that change to the server. 
  - If the change was based on the version of the document that the server considers current, it goes through. 
  - If not, the client must pull the changes that have been made by others in the meantime, and rebase their own changes on top of them, before retrying the push.
- Unlike in git, the history of the document is linear in this model, and a given version of the document can simply be denoted by an integer.
- Also unlike git, all clients are constantly pulling (or, in a push model, listening for) new changes to the document, and track the server's state as quickly as the network allows.
- The only hard part is rebasing changes on top of others. This is very similar to the transforming that OT does. But it is done with the client's own changes, not remote changes.
- Because applying changes in a different order might create a different document, rebasing isn't quite as easy as transforming all of our own changes through all of the remotely made changes.

## Position Mapping

- Whereas OT transforms changes relative to other changes, ProseMirror transforms them using a derived data structure called a position map. 

## Rebasing Positions

- If changes from a peer come in, all of the locally buffered changes have to be moved on top of those changes.

## Mapping Bias

- Whenever content gets inserted, a position at the exact insertion point can be meaningfully mapped to two different positions: before the inserted content, or after it. 
  - Sometimes the first is appropriate, sometimes the second. 
  - The system allows code that maps a position to choose what bias it prefers.

## Types of Changes

- An atomic change in ProseMirror is called a step.
- These are the step types that exist in ProseMirror:
  - addStyle, split, join, ancestor, replace
- The last type is more complex than the other ones, and my initial impulse was to split it up into steps that remove and insert content. 
  - But because the position map created by a replace step needs to treat the step as atomic (positions have to be pushed out of all replaced content), I got better results with making it a single step.

## Intention

- I've tried to define the steps and the way in which they are rebased in so that rebasing yields unsurprising behavior. 
  - Most of the time, changes don't overlap, and thus don't really interact. 
  - But when they overlap, we must make sure that their combined effect remains sane.

## Offline Work

- Silently reinterpreting or dropping changes is fine for real-time collaboration, where the feedback is more or less immediate
- In cases like offline work, I think a diff-based approach is more appropriate.

## Undo History

- How should the undo history work in a collaborative system? 
  - The widely accepted answer to that question is that it definitely should not use a single, shared history. 
  - If you undo, the last edit that you made should be undone, not the last edit in the document.
- To be able to implement this, I had to define changes (steps) in such a way that they can be inverted, producing a new step that represents the change that cancels out the original step.
- ProseMirror's undo history accumulates inverted steps, and also keeps track of all position maps between them and the current document version. These are needed to be able to map the inverted steps to the current document version.
- A downside of this is that if a user has made a change but is now idle while other people are editing the document, the position maps needed to move this user's change to the current document version pile up without bound. 
  - To address this, the history periodically compacts itself, mapping the inverted changes forward so that they start at the current document again. 
  - It can then discard the intermediate position maps.
