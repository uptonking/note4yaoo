---
title: lib-collab-fluid-community-stars
tags: [community, fluid-framework]
created: 2023-02-11T11:07:55.260Z
modified: 2023-02-11T11:08:04.779Z
---

# lib-collab-fluid-community-stars

# guide

# discuss
- ## 

- ## 

- ## Does Azure Fluid Relay support offline mode?
- https://learn.microsoft.com/en-us/azure/azure-fluid-relay/resources/faq
  - Offline mode is when end users of your application are disconnected from the network. 
  - The Fluid Framework client accumulates operations locally and sends them to the service when reconnected. 
  - 👉🏻 Currently, Azure Fluid Relay doesn't support extended periods of offline mode beyond 1 minute. 
  - We highly recommend that you listen to Disconnect signals and update your user experience to avoid accumulation of many ops that can get lost.

- ## [🤔 How to make on Fluid framework work offline?_202011](https://stackoverflow.com/questions/65004396)
- The Fluid Framework handles intermittent (short 断断续续的；间歇的) offline scenarios well as long as all the connected clients have the metadata necessary to merge the change in. 
  - When the user makes changes, she does so with respect to a minimum sequence number (MinSeq.) If the her offline changes get added to the total order broadcast such that they are above her change's MinSeq, they will be merged with no additional handling.
  - MinSeq deserves a whole post, but it's the sequence number beneath which all connected clients can garbage collect the metadata necessary to merge changes. Therefore, as long as every client has that metadata, even if you were offline, the merge is easy.

- 👉🏻 For longer offline scenarios, the reconnecting client could request to lower the MinSeq (probably to the last MinSeq of the offline client.) All clients would then fetch the ops since the requested MinSeq and recreate the metadata. At this point, new changes could easily go in as we have mimicked the scenario where the new changes are above the minimum sequence number.
  - This could cause temporary perf & memory issues, but hasn't been a problem in reasonable experiments. 
  - I don't believe this feature is currently implemented in the Fluid Framework code base, but has been designed as above. (A PR on this topic would be very interesting!)

- 👉🏻 For even longer offline scenarios, you would probably need a three-way merge. 
  - For example: Two users open a document. User A goes on an airplane (loses internet) and writes Macbeth and user B writes Pride & Prejudice, what is the expected behavior when user A rejoins the session? These are entirely incompatible document states, so we'd need to present the users with a dialogue of some sort.
  - This is not implemented, but we have discussed some of the framework ergonomics of handling the three-way merge (i.e. what APIs would the app developer need.)
- [三路合并](https://zh.wikipedia.org/wiki/%E5%90%88%E5%B9%B6_(%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6)#%E4%B8%89%E8%B7%AF%E5%90%88%E5%B9%B6)
  - 三路合并（three-way merge），首先考虑对文件A、文件B以及它们的共同祖先文件C做差异分析。对于文件中的每节(sector)，如果上述三个文件中有两个文件该节的内容一致，那么抛弃文件C中该节的内容，保留与文件C中不同的内容放到结果文件中。如果该节在三个文件中都不同，那么这个冲突需要手工合并。
- 三路合并被程序diff3实现，是基于文件锁的版本控制系统到基于合并的版本控制系统转变的核心。被CVS广泛使用

- ## 🚀 To celebrate the open sourcing of the Fluid, I wrote a quick blog post explaining how real time collaboration is addressed by using eventual consistency._202009
- https://twitter.com/TSteveLuc/status/1304130533073461248
  - For those already familiar with collab tech, Fluid uses distributed data structures (CRDT + OT)
- Lots of cool things in this tech, 
  - one is that most of the work is done client side with very low latency. 
  - The other is the data modeling is very flexible and you don't have to worry about syncing with a server while using data types you are familiar with
- It really looks incredibly cool. Centralizing the op store and using it to provide a distributed total ordering is a genius move, and one that I think too many people won't understand. So smart.
- On a high level this reads similar to what Google Wave presented a while back.
  - similar tech, but not packaged as a product but libraries.
- 👉🏻 Wave used multi-master OT, which proved hard to converge.  
  - Google Docs uses single-master OT, but the service must resolve conflicts.  
  - Fluid moves conflict-resolution logic to clients, reducing service latency and variability.  To do so Fluid needed to invent a way to merge.
  - To see how merge tree looks check out

    - packages/dds/sequence (the wrapper)
    - and packages/dds/merge-tree (the core data structure)
    - packages/dds/matrix uses multiple merge-trees to model a sparse matrix (like spreadsheet)

- it’s CRDT like with a clearer path to partial consensus and cheaper GC (check out packages/dds/merge-tree)

- The other thing to know is Fluid service has a way to kick tell clients when there is a consensus up to some sequence number of change operations (or think of a committed log of operations).  This enables single clients to summarize state of world and enables local GC.
  - And to kick clients out if they lag behind and don't keep up with consensus.  This simplifies the protocol for joining a session.
- 👉🏻 CRDT protocols proposed to date for sequences and trees do not have a way to avoid distributed GC, do not have a clear way to know a partial consensus, and require download of big indexing structures upon join.  Fluid fixes these.
- I assumed it must, and that’s what got my attention.  It’s so clever, in the best way - it makes great simplifying trade offs.
