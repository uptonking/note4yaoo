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

## [vlcn: A Framework for Convergence](https://vlcn.io/articles/crdt-substrate)

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

# discuss-author
- ## 

- ## 

- ## 🚀🔀 [Crsql – Multi-writer and CRDT support for SQLite | Hacker News _202211](https://news.ycombinator.com/item?id=33606311)
- Does this support CRDTs other than last-write-wins registers?
  - Not yet. I was thinking of collaborating with Seph to bring DiamondTypes in for sequence crdt support. If that is even possible -- just an idea at the moment.

- 
- 
- 

- That isn't how CRDT's work though. In the example of mutating a bank balance, there would be addition operations and subtraction operations. So /eventually/ all nodes would arrive at the same balance. It's a bit like event sourcing but lower-level.
  - Depends on the type of CRDT. You can have a CRDT which supports setting a register (or column value in a row) to a particular value. This is what Crsql appears to do as one sibling comment indicated. There are a number of ways to resolve conflicting updates, but Crsql chooses LWW (last writer wins).

- The part i dont understand is as far as i understand, CRDT requires data types with commutative update functions, but SQL does not have that. The part i dont understand is how these two technologies that seem to have conflicting requirements are being joined.
  - Columns are LWW (last writer wins) registers within rows which are LWW maps. When concurrent writes occur because peers may not be communicating, there is typically an arbitrary but convergent selection based on peer id.
- There's different strategies for solving conflicts but CRDTs wouldn't be a good fit where you need a total ordering of all transactions -- such as bank deposits.


- 
- 
- 
- 

# discuss-stars
- ## 

- ## 🌰📝 A user hacked together a proof of concept for rich text merging in vulcan / cr-sqlite._202303
- https://discord.com/channels/989870439897653248/1084822114302967909/1084822114302967909
- Thats really cool! Do they use a separate text-crdt encoded into a column, or have they built one in sqlite?
  - I haven't read the code yet but -- https://github.com/mweidner037/vlcn-rich-text/blob/master/src/todomvc/TodoList.tsx
- Seems like they generate a sort of fractional index position for each char, and order by on it. So the text itself is a crr table with char and position columns. Very interesting.
- this is probably worth implementing as the first sequence crdt. So simple
  - Space is a concern of course. But it looks like you don't need to keep delete records and maybe we can assign short ids to participants in a document

- ## [investigate sequence/text crdts](https://github.com/vlcn-io/cr-sqlite/issues/65)
- If we don't target WASM I think adding diamond types will be easy.
  - Targeting WASM makes everything harder since WASM binaries currently can not load other binaries (AFAIK) so we have to compile Rust code with C code. 
  - Maybe I'm worried about nothing and that is actually an easy thing to do?

- We've (iver & myself) been discussing this a bunch offline and here is a summary of where we're at so far:
  - 💡 **Queries that order by a recursive relationship in SQLite are actually rather performant** 
  - Because of (1), _we can represent any tree-based CRDT in a table_
  - A proposed table structure is something like below

- If you're interested, one alternative is to use a "CRDT-quality" version of fractional indices. 
  - These will never be as storage-efficient as a dedicated list CRDT, but you can generate the strings in <100 LOC and put them in a "position" column that you ORDER BY.
- I still haven't seen any fractional indexing string which didn't have interleaving problems.. Has that been solved?
  - Yeah, it was also my impression that you couldn't fix the interleaving problem with fractional indexing.
  - btw -- we have implemented fractional indexing in cr-sqlite. 

- It should be non-interleaving in both directions. 
  - The total order is equivalent to a tree walk over a binary-ish tree; concurrently-inserted sequences end up in different subtrees, which don't interleave.
  - **You do pay for this with longer strings**, though: "averaging" two neighboring strings adds a UID (~13 chars) instead of a single bit, except when the in-order optimization kicks in.

- I think we can implement a variant of Fugue that stores multiple chars per row. (Untested)

- Closing this as I think enough research has been done and I'm ready to start implementing

- ## [Reactivity / Live Queries / Subscriptions / Database Observation · vlcn-io/cr-sqlite](https://github.com/vlcn-io/cr-sqlite/discussions/309)
- The SQLite bindings I currently provide to React re-run a query if/when any table that the query used changes. This is regardless of what columns the query happened to use. This works pretty well until there are > 50 live queries.
  - The GRDB approach seems to avoid these pitfalls.
  - For the reactive components of Vulcan I think following the same path as GRDB, maybe even porting their implementation of observability to Rust so we can compile to WASM for use in the browser, is the right medium term path.

# discuss
- ## 

- ## 

- ## 🔁 A browser extension has many different execution contexts (content/site, background) that don't have access to the same apis and permissions.
- https://discord.com/channels/989870439897653248/1195787026499371158/1195787028726566953
  - Any idea how could I sync a db relying only on `postMessage` like capabilities?
  - I'm working on a chrome extension that augments specific sites. 
  - It relies on mutation observers, event logging etc.
  - I'm trying to sync the data store I inject on the site context to the background context. So I can use another "admin" page to debug and implement the augmentation.
  - In you work with CRstore, did you have to do syncs that didn't rely on a server ? And only browser side.

- By default, if you don’t specify remote pull & push, CRStore would only sync locally between tabs via `BroadcastChannel`.
  - Also `pull` & `push` are just functions, so you can put any sync logic you want there (it doesn’t have to be with an actual remote)
  - Also by using the `subscribe` and `update` primitives, you can roll out a completely custom sync solution that will interop nicely with all the CRStore features

- you could post the sync message over a message channel following a similar setup to cr-sqlite-basic-setup

- ## Been pretty silent for a while. That's because `useQuery(...)` , while a great dev experience, has scaling problems.
- https://twitter.com/tantaman/status/1737903783496032671
  - So I'm scaling `useQuery` style hooks to 60fps response time when working with millions of items and keeping those queries up to date as data changes.

- ## [Yjs simple provider](https://github.com/vlcn-io/cr-sqlite/pull/120)
  - Adds a yjs provider that persists to crsqlite and syncs through crsqlite.

- going to shelve this for now.
  - crsqlite shouldn't concern itself with application layer integrations at this point in time.

- ## Primary key choices matter again once you start working with CRDT database.
- https://twitter.com/tantaman/status/1547954669250457600
  - Having a uuid for every row doesn't make sense when rows created by different peers can have the same identity and need to be merged.
  - E.g., a topic in a collaborative library. If we both create the "Science" topic independently, they should both represent the same thing and merge together.
