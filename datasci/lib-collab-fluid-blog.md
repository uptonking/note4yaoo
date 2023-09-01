---
title: lib-collab-fluid-blog
tags: [blog, fluid-framework]
created: 2023-02-11T14:38:08.532Z
modified: 2023-02-11T14:38:16.451Z
---

# lib-collab-fluid-blog

# guide

- [Fluid Framework - Microsoft 365 Developer Blog](https://devblogs.microsoft.com/microsoft365dev/category/fluid-framework/)
# blogs

## [Collabs: Composable Collaborative Data Structures](https://arxiv.org/abs/2212.02618)

- Replicated data types (RDTs), such as CRDTs, provide an abstraction for reasoning about replication and consistency in distributed systems. 
  - To make them as useful as ordinary, local data structures, RDTs need to be both modular and composable, 
  - However, no existing RDT libraries combine these properties; either they use monolithic architectures that rule out new RDTs or they do not support composition techniques.
- In this work, we introduce the Collab (collaborative data structure), a novel abstraction for modular and composable RDTs. 
- Modular
  - Each data structure is its own unit, independent of other data structures in the same library. 
  - Thus the library is extensible: programmers are free to add their own data structures, with arbitrary APIs and implementations. 
- Composable 
  - Simple data structures can be composed to create more complex ones. 
  - This makes it easy for app programmers to model their own data (e.g., using classes), and it also lets complex data structures inherit behavior and correctness guarantees from their components (e.g., a hash set can internally use a hash map).
- However, no existing RDT libraries combine these properties. 
- 👉🏻 Yjs [Jahns 2022; Nicolaescu et al. 2016], Automerge [contributors 2022], and OWebSync [Jannes et al. 2021] support either composable maps and lists or JSON-formatted data, but they use monolithic architectures that rule out programmer- added data structures; 
- ShareDB [Smith and Gentle 2022] and Fluid Framework [Fluid Framework 2022] allow modular custom RDTs but do not support composition techniques.

## [Solving real time collaboration using Eventual Consistency_202009](https://matt.aimonetti.net/posts/2020-09-solving-real-time-collaboration-using-eventual-consistency/)

## [Fluid Framework is now open source_202009](https://devblogs.microsoft.com/microsoft365dev/fluid-framework-is-now-open-source/)

- With Fluid Framework, developers can easily add multi-user interactivity to their apps — powered by **the same code that drives collaboration in Microsoft 365 experiences** for millions of users. 
- Fluid Framework is built from the ground up for very low latency collaboration and synchronization. 
  - Developers using Fluid’s distributed data structures can build powerful collaborative applications using familiar programming patterns.
- To get this level of performance, Fluid Framework pushes synchronization logic to the edge and keeps the service simple. 
  - Each Fluid client is responsible for managing its own state while the Fluid service is only responsible for relaying changes to the connected clients.  
- With this technology, the Fluid Framework offers developers: 
  - A client-centric application model with data persistence requiring no custom server code 
  - Distributed data structures with familiar programming patterns 
  - Very low latency
# more
- [Announcing general availability of Azure Fluid Relay service_202208](https://devblogs.microsoft.com/microsoft365dev/announcing-general-availability-of-azure-fluid-relay-service/)
- [Stay in sync with Microsoft Loop_202112](https://devblogs.microsoft.com/microsoft365dev/stay-in-sync-with-microsoft-loop/)
  - Microsoft Loop is built and powered by Fluid Framework which is the core technology that enables seamless data synchronization, real time collaboration
