---
title: lib-editor-prosemirror-collab
tags: [collaboration, editor, prosemirror]
created: 2021-10-14T05:02:01.304Z
modified: 2021-10-14T05:03:19.234Z
---

# lib-editor-prosemirror-collab

# [Collaborative Editing in ProseMirror__201507](https://marijnhaverbeke.nl/blog/collaborative-editing.html)

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
  - I am, to be honest, extremely bewildered by Google's decision to use OT for their Google Docs—a centralized system.

- **ProseMirror's algorithm is centralized**, 
  - in that it has a single node (that all users are connected to) making decisions about the order in which changes are applied. 
  - This makes it relatively easy to implement and to reason about.
- And I don't actually believe that this property represents a huge barrier to actually running the algorithm in a distributed way. 
  - Instead of a central server calling the shots, you could use a consensus algorithm like Raft to pick an arbiter.

## Centralization

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
