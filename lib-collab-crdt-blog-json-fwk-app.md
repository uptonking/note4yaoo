---
title: lib-collab-crdt-blog-json-fwk-app
tags: [automerge, blog, collaboration, crdt, json, yjs]
created: 2023-10-28T09:12:44.281Z
modified: 2023-10-28T12:54:25.048Z
---

# lib-collab-crdt-blog-json-fwk-app

# guide

# blogs

# 📝 [Building a BFT JSON CRDT](https://jzhao.xyz/posts/bft-json-crdt/)
- CRDTs are a family of data structures that are designed to be replicated across multiple computers without needing to worry about conflicts when people write data to the same place. 
- Traditional databases focus on a property called linearizability, which guarantees that all operations behave as if executed on a single copy of the data. 
  - Linearizability is a strong correctness condition, which constrains what outputs are possible when an object is accessed by multiple processes concurrently. It is a safety property which ensures that operations do not complete in an unexpected or unpredictable manner.
  - We call this canonical view the primary site.
  - Every read in a linearizable system, no matter what database node you read from, gives you an up to date value.
- Achieving this property adds a lot of overhead because both writes and reads need to coordinate across all database nodes to ensure consistency. 
  - This creates an availability problem: if you can’t reach a majority of your nodes, you can’t process any operations.
- using CRDT, we trade linearizability for a property called strong eventual consistency:
  - All updates will eventually reach every node
  - Every node that has received the same updates will have the same state

- CRDTs are a family of data structures.
  - A fundamental limitation here is that there are certain types of data structures (like sets) that cannot be made into CRDTs

- we can use Lamport timestamps. 
  - These track logical time rather than actual wall time, meaning we count number of events that have occurred rather than seconds elapsed.
  - This timestamp is just a simple counter. 
- For the rest of the blog post, we refer to this counter as the sequence number `seq`.
  - All nodes start their counter at 0
  - Everytime we perform an operation locally, we increment our counter by one
  - Everytime we broadcast a message to our peers, we attach this counter
  - Everytime we receive a message, we set our timer to `max(self.seq, incoming.seq) + 1`

- Lamport timestamps only give us a partial ordering, which means two identical sequence numbers might not correspond to the same unique event. 
  - we can actually create a total ordering of events in a distributed system by using some arbitrary (but deterministic) mechanism to break ties. 
  - For CRDTs, if we give each node a unique ID, we can actually tie-break on this ID to provide a deterministic way to order concurrent events.

- But we can’t figure out this causality information from just sequence numbers alone.
  - It turns out the fix for this is actually quite easy.
  - As we have a unique way of identifying each operation, we can just send along a list of operations it causally depends on. 
  - That way, if we receive a message and we know we’ve received all of its causal dependencies, it should be safe to deliver.
  - If we receive a message where we haven’t received all of its causal dependencies, then we can add it to a queue so that when the message does get delivered, we can apply it afterwards. 
  - This means that as long as we declare the right causal dependencies, we can make certain things that don’t seem commutative (like list operations) actually commute.

- make a distinction between the data in the CRDT itself and the view of that data.
  - The data itself are the operations that are coming in
  - The view is the data structure we compute from it (and what applications end up seeing)

- we never4 delete any operations from the internal data representation. 
  - The best we can do is mark them as deleted using a tombstone. 
  - Because a peer could technically reference any past operation as a causal dependency, we need to keep that metadata around.

## List CRDTs (RGA Explained)

- When you think of the API for a list, most operations are normally done by indexing.
- The key insight here is that instead of using relative addressing (e.g. positional indexing), we can use absolute addressing (e.g. using IDs).
  - Every time we insert an element into the list, we need to know the ID of the character we are inserting after. 
  - Then, we just place it somewhere between that element and the element following it.
  - So instead of saying “insert ‘A’ after the character at position 4” we say “insert ‘A’, with ID 5, and insert it after the character with ID 4”.
- Conveniently, we can encode this causality by making the causal parent of each item the character it was inserted after. 
  - This forms a sort of causal tree and this is effectively how RGA, a list CRDT, structures its data internally.
- When inserting a character we
  - Find the origin (causal dependency). If it doesn’t exist, we queue it up for later.
  - Starting at this node, all of its siblings were inserted concurrently. We look through the list of siblings until we reach a node that we are greater determined by the happens-before comparison we defined

- To get the actual list this CRDT represents, we perform an in-order traversal over the tree and only keep nodes that are not marked as deleted.

## Adding Byzantine Fault Tolerance for free (almost)

- Up to this point, the CRDTs we’ve covered all work in trusted scenarios. 
  - These are scenarios in which you know all of the people participating and you trust them to not screw up the system for everyone else.
- However, most of the interactions we have online are not in trusted scenarios. 
  - Luckily, we have servers to help mediate(调停；调解) these interactions, dictate what is and what isn’t possible. 
- The CRDTs we have been exploring so far do not work in these untrusted scenarios. 
  - That is, any one node can do something bad and cause state to diverge permanently. Not good.
- To be more concrete, here are some examples of what a malicious actor can do:
  - Send malformed updates
  - Not forward information from honest nodes (an eclipse attack)
  - Send invalid updates
    - Messages that have duplicate IDs
    - Send incorrect sequence numbers (an equivocation attack)
    - Claim to be another user
- To borrow a term from distributed systems, we want to make our CRDTs Byzantine fault-tolerant
  - The ‘Byzantine’ part of the name comes from the Byzantine Generals Problem, a situation where, in order to avoid catastrophic failure of the system, the system’s actors must agree on a concerted strategy, but some of these actors are unreliable and potentially malicious.
- Notation wise, we denote the total number of nodes in the system `n`. 
  - We denote the number of faulty/Byzantine nodes `f`. 
  - Most consensus algorithms claim a tolerance of up to `f < n/3`, which means they can tolerate up to 33% Impossibility Result
- However, CRDTs require an even weaker bound. Remember that we are not trying to achieve consensus! 
  - All we really need to do is make sure that Byzantine actors can’t interrupt honest nodes from functioning properly.

- In fact, we can reduce this to a problem called Byzantine Broadcast
  - Dolev-Strong, back in 1983, showed that it was possible to tolerate up to $f < n$ faulty nodes! 
  - This means that, as long as there are honest nodes and they are connected to each other, they can still function properly
- Kleppmann detailed an approach in his paper Making CRDTs Byzantine Fault Tolerant that works without changing the internals of most CRDTs; it can be fully retrofit on top of it. 
  - We can create a ‘BFT adapter’ layer between the transport and application layer that is responsible for filtering out any Byzantine operations.

## A JSON CRDT

- Ok, we’ve seen now how we can create a Byzantine Fault Tolerant list CRDT. How can we make a JSON CRDT out of this?
- Normally with JSON CRDTs, we just have a bunch of nested CRDTs.
  - Values are LWW registers
  - Lists are RGA lists
  - Maps are lists of key-value pairs
- Each nested CRDT also keeps track of its path (e.g. inventory[0].properties.damage) so that when CRDTs produce an event, this information is also included. 
- However, we have to be careful about how we store this path. We can’t naively just use the index into the list as we saw earlier how this is unstable. A small workaround here is having the `OpID` be the index.

- There is one last challenge to account for: JSON has no schema; data types can change!
  - The way Automerge and Yjs resolve this is by essentially using a multi-value register: they keep both values and punts the responsibility to the application choose the right answer.
- With most applications, allowing users to set arbitrary JSON is not actually desirable. We can somewhat mitigate these problems by allowing the application developers to define a fixed schema ahead of time and validating all operations through this
# blogs-crdt-apps

## [Designing Data Structures for Collaborative Apps - Matthew Weidner](https://mattweidner.com/2022/02/10/collaborative-data-design.html)

- A good starting point is to design an ordinary (non-CRDT) data model, using ordinary objects, collections, etc., then convert it to a CRDT version. 
  - So variables become Registers, objects become CRDT Objects, lists become List CRDTs, sets become Unique Sets or Add-Wins Sets, etc

## [Collaborative and Offline Editing Using CRDTs • Decipad's Blog_202309](https://www.decipad.com/blog/decipads-innovative-method-collaborative-and-offline-editing-using-crdts)

# more
