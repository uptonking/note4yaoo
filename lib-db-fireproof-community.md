---
title: lib-db-fireproof-community
tags: [collaboration, community, crdt, fireproof]
created: 2023-12-24T10:48:12.614Z
modified: 2023-12-24T10:49:01.941Z
---

# lib-db-fireproof-community

# guide

# blogs
- [Why Verifiable CRDTs Are the Future of Web Data_201309](https://fireproof.storage/posts/why-verifiable-crdts-are-the-future-of-web-data/)
# discuss-stars
- ## 

- ## 

- ## 

- ## 💡🤔 The meaning of the term "CRDT" is really starting to drift.
- https://twitter.com/LewisCTech/status/1719807159217844603
  - Libraries like automerge and yjs are just *implementations* that happen to be a CRDT. 
  - But the idea of a CRDT itself is much older. I've seen "proto-CRDTs" described as far back as 4 decades.
- CRDTs are just abstract data types with operations that follow some algebraic laws, that guarantee they will converge in a sensible way. That's really it. They don't need to be complicated. They don't even need to be single record - a whole DB could itself constitute a CRDT.
  - Agree. 🛋️ @CouchDB is a CRDT at the database level and at the document level. @FireproofStorge is one at the database level. Also, all Merkle-diffs are CRDTs.

- ## 💡 One of the biggest challenges in creating @FireproofStorge is that I refused to take on infrastructure operations. 
- https://twitter.com/jchris/status/1717195946822660289
  - This means the entire database has to be built to run anywhere. (It eats trash, so you don’t have to.)
  - Fireproof is like SQLite, it runs embedded in your application. This means it’s my job to make it so nobody has to worry about compiling dependencies, or making a misconfiguration that loses data.
  - I could have created a minimal backend that runs in a container or some other abstraction layer. But that is not the path of simplicity, and simplicity is one of the competitive advantages someone like me can offer.
  - Instead, the focus is on making it work with any backend from S3 to the file system to @IPFS and @partykit_io — this requires a level of focus on the storage engine that I haven’t seen in other browser databases.
  - Because we use content addressed data, our files are self-verifying. But that is only half the battle, because a database that stores files anywhere could be putting your data everywhere. I couldn’t in good conscience be writing app data to random public buckets, in the clear for anyone to read.
  - Fireproof is end-to-end encrypted by default. This means if you manage your keys correctly, it can be as secure as you want. And if you don’t know what you are doing, at least you’re not spraying clear data all over the place.
  - The result is a database that any front-end developer will feel at home with, but also lets them get work done without asking for anything from the backend team.

- 🤔 why do u choose ipfs instead of hypercore ?
  - If hypercore can shuffle binary blobs, then they work the same for Fireproof.  I started with IPFS because of the IPLD data structures, which are the center of interesting research for immutability. But that stuff is independent of the actual transport.
  - The content addressable trees and CRDTs that come from @mikeal , @_alanshaw and friends are at the forefront of the industry. I saw my opportunity to package that fundamental advancement for the masses.
# discuss
- ## 

- ## 

- ## 

- ## 🚀 fireproof.storage Light up your data!_202303
- https://twitter.com/jchris/status/1633113469179314179
  - check out my new project, a real-time database that runs in any page, with indexes, event feeds, automatic replication, and cryptographic verifiability. 
- It either took me two weeks to write this JSON database, or 14 years.
  - Part of what makes it so easy to use is that it’s an embedded database with network support, like PouchDB or Couchbase Lite. So developers don’t have to worry about setting it up, nor do they have to worry about where the data is stored.
  - The current version just keeps data in browser local storage, but it manages transactions and blocks using the immutable IPFS protocol. This means you can save and load data from almost anywhere.
  - The combination of lightweight runtime, and the ability to reach across the network for blocks, makes me tell my kids I’m making an “infinite database.”
- Limitations: currently encryption is living on a branch that I will merge as soon as I figure out the last webpack issues
- Some of the prime use cases for this sort of technology:
  - adding dynamic features to static pages 
  - saving/memoizing pure functional transforms in a verifiable way (cough: prompt, model, params) 
  - serving as a content-addressed oracle for smart-contract execution 
  - games!

- Are the indexes local-only or also synced? For integration in non-JS codebases, is there a spec to interoperate?
  - The indexes use the same block store as the database, so when you activate replication, they also sync to @Web3Storage , but I think this will be optional, as you’d rather rebuild than copy when you’re on a slow connection.
  - Another option I’ll be adding soon is the ability to serialize the current state as a single car file so that you can embed it in your app for instant preload
  - As far as a spec, not yet. I plan to swap out some of the core data structures with more nuanced implementations, at which point that will be front of mind.

- 🆚️ How does it differ from Pouch?
  - One of the stand-out use cases for this is adding features to Web3 style link in profile pages. Because if you’re deploying HTML that has its content hash in a block chain somewhere, and the html contains the root hash of your database. Merkle!
