---
title: lib-collab-vlcn-dev
tags: [collaboration, crdt, vlcn]
created: 2023-06-03T14:43:07.242Z
modified: 2023-06-03T14:43:26.987Z
---

# lib-collab-vlcn-dev

# guide

# dev

# blogs

##  [vlcn: A Framework for Convergence](https://vlcn.io/articles/crdt-substrate)

- While CRDTs and other structures may meet the mathematical definition of convergence, it is likely that they will not meet the user's expectations of convergence.
- The problem with both examples is that we're using array index (or alias) to indirectly reference what we are actually talking about.
- Many types of intent (delete, move to, insert at) can be preserved by knowing a few principles and following them when writing mutations.

- ### Intent Preserving Principles
- Refer to items by their identity
  - When you're operating on something, you need to refer to that thing exactly rather than using an indirect reference.
  - This is most clearly illustrated in the mutations that used array indices to talk about what to remove. 
  - If, instead, each element had a unique ID and we passed that to mutations when deleting / moving / etc., the user's intent would be preserved.
  - The updated mutations. Note that the item id must be passed in to the mutation. Generating a random uuid within the mutation would make the mutation non-deterministic.
- Position is Relative
  - If you need to prevent interleaving of sequences, use relative positions.
  - Our addItem mutation is implicitly using array index as the sort order for items. This is fine for many use cases but for other use cases, such as text insertion, this is problem. 
  - The reason is that concurrent edits in the same location will end up interleaving characters.
  - We can fix this by making the notion of position relative. That is, the position an item was inserted at is identified by what is to the left or right of that item.
  - There could still be a problem here, however. What if another user concurrently deleted something you were inserting next to?
  - You could fix this with invariants (do not allow deletion of these sorts of things) or soft deletion & tombstoning. 
  - In addition to the problems outlined for sequences, we can run into issues when moving structures around that have pointers to one another. E.g., moving folders inside a file tree. Concurrent edits of this tree can create cycles such as a folder that contains itself.

- Other Options for Intent
  - A different approach to preserving intent is to reach for an existing CRDT(opens in a new tab) that has the intention preserving properties you'd like. This where we're headed with Vulcan.
- Framework Implementation
  - A log of mutations
  - Machinery to merge and apply the log to the application's state
- Every time one of the named mutations is run, we log it.
- In a system that isn't distributed the log would be linear.
- In our case, however, we need to account for concurrent edits happening in other processes. 
  - This is where ParentIDs comes in. 
  - ParentIDs refers to all the mutations that happened immediately before the current mutation.
- Thus the log, rather than being linear, is a DAG. 
  - The relationships in the DAG express time.
- each process can locally write to its log without coordinating with others. 
- Syncing state between processes is a matter of merging these logs together and merging these DAGs is trivial. 
  - Since each node in the DAG is completely unique and immutable, all we have to do is union the sets of nodes. 
  - This unioning can happen in any order and is idempotent meaning convergence does not rely on the order the DAGs are merged and duplicate syncs are not a problem.
- Meaning **the DAG is a CRDT**. 
  - Since we know that DAG will always converge across all peers we can use it to order and drive mutations against application state.

- Updating application state after a merge is a matter of:
  - rewinding to a certain snapshot of application state (or all the way back to initial state)
  - Replaying the mutation log against that state
- But how do you replay a log that is not linear? 
  - You make it linear. Each process does a deterministic **breadth first traversal** of the DAG to create a single sequence of events. 
  - This interpretation of events is what is applied to the state snapshot.

- The area where this gets tricky is when handling concurrent branches. 
  - Since there is no ordering between concurrent events we just have to pick one and stick with it. 
  - A common way to order concurrent events is to **order them by process id or value**.

- While toy versions of all ideas seem to be able to be implemented in 100 lines of JavaScript(opens in a new tab), a production grade version that:
  - Scales to hundreds or thousands of transactions per second (no matter how large the transaction logs become)
  - Shares structure and compresses well
- For the general case you'll need:
  - A data structure that can rewind to arbitrary versions easily
  - A way to calculate the deltas between DAGs on different nodes so as not to require sending the entire dag on sync
  - Something to prevent mistakes such as mutations being non-deterministic
  - A way to compress the log while still supporting random access to it
  - A way to know when it is safe to prune events out of the log
# docs

# more
