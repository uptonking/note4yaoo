---
title: lib-db-hypercore-faq
tags: [faq, hypercore, issues]
created: 2023-09-09T19:03:44.602Z
modified: 2023-09-09T19:04:07.030Z
---

# lib-db-hypercore-faq

# guide
- [Hypercore universe FAQ](https://github.com/tradle/why-hypercore/blob/master/FAQ.md)
# faq-repeat

## 

## 

## 

## 🆚️ How is Hypercore different from ScuttleButt (SSB)?

- Secure Scuttlebutt (SSB) is a peer-to peer communication protocol, mesh network, and self-hosted social media ecosystem. 
- Hypercore has been growing towards a more generic model of structured data (file systems, databases) synchronized over many devices.

- **SSB is not well suited for streaming**, 
  - as it does not have a sparse data structure (enabled in Hypercore by Merkle trees, while SSB uses linked lists).
- **SSB uses a gossip protocol to sync data between peers**. 
  - It does not automate peer discovery for a given dataset (e.g. via DHT), so topology must be manually managed. 
  - Hypercore uses a DHT to automate discovery of peers for exchanging of data.

## 🆚️ How is Hypercore different from IPFS?

- [Hypercore Protocol](https://www.reddit.com/r/ipfs/comments/glnra9/hypercore_protocol/)

- Both are cool open source P2P data projects that have existed for roughly the same 5-7 years.

- IPFS
  - OrbitDB, ThreadDB, AvionDB
  - Content-based addressing
  - Dynamic address, changing as block changes
  - each block has unique address (block's hash)
  - Files are composed of lists of linked blocks, no notion of file directories, metadata
  - Same block can be reused on your machine, even between files. This is usually called deduplication, or dedup. But when block changes, old block remains in storage.
  - Originally developed for static content, but is being re-designed now. 
  - Change Data Capture - does not exist in IPFS, attempts are being made to create something for 4 years
  - IPFS team runs a number of public servers that help make the network more usable.
  - IPLD is IPFS's sub-system to define structured interlinked data. IPLD structures implemented on top are ipld-bitcoin or ipld-ethereum.

- Hypercore
  - Two variants: Key-value store (Hypertrie) and LevelUP-compatible DB (Hyperbee).
  - Public-key based addressing
  - Static stable address
  - Address (pub key) corresponds to a collection of objects / files, each consisting of many blocks
  - Files are managed as full-blown filesystem, with stable API and a daemon that provides REST API and POSIX-compliant OS extension
  - No block-level dedup. Change in one byte, creates a new version of the file. File-level dedup can be achieved with additional management level, called corestore.
  - editable content was a prime design objective, supported by the internal data structures
  - Granularity, not just files, e.g. with Hypercore you can do live updates in the UI

- IPFS has implementations in a number of languages, while Hypercore is only in JavaScript. Rust implementation of Hypercore was recently started 

- 
- 
- 

## Is Hypercore multi-process-safe?

- We know it is single-writer. 
  - But can the same writer accidentally screw up the Hypercore while being executed from a second processes on the same machine, like from a Nodejs cluster process or a Nodejs worker thread? If so, it will present a significant design challenge in Serverless environment.
- For reference, note that LevelDB is not multi-process safe, but LMDB is.
- Need help with this.

## What is the biggest gotcha with Hypercore?

- You can create conflicting forks of a hypercore log by first copying the hypercore feed directory to another machine along with its private key and then writing into hypercore copy while making updates in the original. 

- If you rewind the feed that is replicated, replicas will stop syncing.

## What is missing in Hypercore?

- Distributed Time / Clocks
  - Typical solutions include generation / causal clocks, and newer hybrid clocks like HLC.
  - Every message, including the heartbeat message needs to carry this time

- Multi-device editing with conflict resolution (CRDT)
  - CRDT must use the above clocks for structured data and for document editing (docs, slides).
- With multiple devices comes a need for per-device key management, key coordination and revocation. Key management in general is missing in Hypercore.

- Collaborative (team) editing with conflict resolution

- Topology management
  - Replication and storage management algorithms might take all above into account. 
  - For example, for sharing media from mobile, replication algorithm should only upload each block once, to the peers with a better connection.

- Schema / data model / data dictionary

- Multi-writer
  - Hypercore is engineered as a set of small single-purpose primitives (lego blocks) to be highly composable. 
  - To support such use cases multi-writer modules can be composed on top.
# faq

## 

## 

## 

## What is the USP (Unique Selling Proposition) of Hypercore?

- Hypercore's key USP is streaming.
  - You can think of it as video streaming, but now for videos and also filesystems, databases, messages, IoT signals, and any other structured data constructs. 
- Note, when reading Hypercore docs you will find many references to sparse replication. 
  - This is the capability used for streaming, allowing a peer to efficiently request individual blocks from remote peers, instead of loading the whole remote dataset, be it a video file or a database.

- Another USP of Hypercore is that it implements essential patterns of distributed systems in a reusable way
- WAL. 
  - All distributed systems need a Write Ahead Log (WAL), be it databases, orchestration engines, like Zookeeper or etcd, or event streaming systems like Kafka. 
  - Every system implements its own WAL today. 
  - Hypercore generalized this pattern as an append-only-log and consistently uses it in its higher-level data structures such as Hypertrie, Hyperbee, Hyperdrive.
- Time travel. 
  - Hypercore provides universal history for all data structures which work on top of it, which gives them a universal undo-redo, rewind-replay. 
  - This capability is common in editors, but now it can be used in any application including retracing actions in a filesystem and a database.
  - Same history capability can be used for classic database point-in-time recovery, DB and filesystem snapshots, and versioning for data integrity assurance, VM snapshots, filesystem and DB snapshots, container image layers, etc. etc.

- Google Docs only has support for offline work in Chrome, but not in other browsers. This is how these services tie you up.

- There is a new hot area in Big Data world for querying static databases. 
  - In AWS it is Athena, based on Apache Presto engine, and SQL SELECT. 
  - CSV Files (or files in JSON, Parquet, ORC, Avro formats) are shoved into S3 and then queried by Serverless applications and by Business Intelligence packages like Tableau.

- Database with data stored in S3 (or the like) is very tricky to make performant. 
  - AWS Athena uses above specific formats, helps split large files into smaller chunks
- Hyperbee provides a similar capability implemented in a completely different way. 
  - its underlying protocol is optimized to load byte-ranges from the [S3 object] offset, and efficiently traverses the btree (in Hyperbee) of the trie (in Hypertrie) to avoid extra round trips when executing queries for remote data (S3 in this case). 
  - This is a so called sparse mode in Hypercore.

- What other applications that can we think of that can be enabled by such a server-less DB
  - a P2P source control system Git that replaced SVN and CVS which used central server. please note that Microsoft bought Github for $7.5B.

## How is Hypercore different from BitTorrent, WebTorrent?

- Hypercore can do what BitTorrent does and more.
  - it is built as a data and communications framework for modern decentralized applications.
  - Applications need data structures. Hypercore provides append-only log, Hypertrie key-value store, Hyperbee database and Hyperdrive filesystem.
  - Hypercore supports data editing as a design principle
  - It provides full data add/edit version history which allows auditing, point-in-time-recovery, and state snapshots.
  - It provides sparse download like BitTorrent, but extends it to databases.
  - Hypercore has data access authentication, and network encryption

- WebTorrent's tech can be helpful to Hypercore, as it perfected peer discovery (via DHT) on the Web

## Is there a synergy between blockchain and Hypercore?

- Both blockchain and Hypercore provide verifiable data structures. 
- But blockchain is limited to very small storage 
  - and Hypercore is limited by absence of pubic timestamping and data history, and the absence of verifiable computations.

## Why Hypercore is not yet mainstream?

- Availability
  - once you close your laptop, your collaborators can't get your latest content
- Durability
  - Your peers may be good friends but there is no guarantee they will not lose your precious content.
- Networking
  - Current Internet, with its routing and firewalling system is just hostile to P2P connections. 
  - Although Hypercore's Hyperswarm offers an ingenious NAT hole punching, there are too many edge cases
  - Besides, if the user wants to send data to someone else, both devices need to be online simultaneously.
- Reliable P2P networking remains unsolved.

## Who is using Hypercore P2P framework today?

- Pushpin
- Peermaps
- Cobox community created a KappaDB and collaborative editing.
- Sonar, distributed media archives on Hypercore.

## Can Hypercore's author change history?

- An actor could decide to revert Hypercore to a previous state, and share this fork.
  - Another possibility is for the author to rewind and serve different version of the history to different peers
- The required protection can be achieved by sealing Hypercore's root on public blockchain, utilizing its immutability and secure timestamping properties.

## Does Hyperswarm work in browsers, on mobile?

- Not directly, but community solutions exist. 
- WebTorrent works in the browser, but "DHT in browser", even after 7 years of discussions, is still not realized.

## Can Hypercore network protocol be extended?

- Yes. The protocol is formalized with protobuf and supports defining extensions.

## Can data be deleted?

- Somewhat - you can clear() your content locally, 
  - but **if someone replicated it already, you can’t force them to clear**. 

## How does Hyperbee relate to Hypercore?

- Hyperbee uses Hypercore as an underlying storage and a replication mechanism. 
  - The cool thing is that one replication stream can carry many Hypercores, which can carry Hyperbees, Hypertries, and Hyperdrives.
- To manage multiple hypercore feeds, with permissions, use the corestore.

- Hyperbee, like any other Hypercore-based data structure is single-writer. 
  - That means when it is replicated, it is replicated as-is, and eventually reaches the same state. 

- hyperbee needs to be wrapped into Hyperbeedown and fed into LevelUP.

## How can Hyperdrive be shared?

- Hyperdrive itself is actually 2 hypercores for directory structure and metadata, and for file content. 
  - So to share it you use the above URL (need confirmation for that).

- Underlying mechanism is built into Hypercore, and works for all data structures that use it: Hyperdrive, Hypertrie and Hyperbee. 
  - You can share the read-only version of your whole hypercore with others, by giving them the public key of the Hypercore.

## [why-hypercore](https://github.com/tradle/why-hypercore)

- This article is covering the design for personal Data using our chosen framework, Hypercore
  - Tradle is evolving its MyCloud platform, designed for banks to manage their own data without giving this data away to SaaS companies

- P2P architectures and applications are much harder to create than centralized, they are often less efficient (BitTorrent's download super-speeds are an exception) and investors are less interested, as they do not produce monopolies that create outsized returns.

- Hypercore is designed for real-time, and works in time-sensitive video streaming and decentralized filesystems and database scenarios.

- So what if we built apps the other way around, in a way where all data would belong not to the app/website owner, but to the user.
  - Data would remain user's and never get exfiltrated, or possessed by the app. 
  - Later a different app can visit the same data
  - This does not mean we never share data, we do, with friends and teams, but not with apps and their owners.

- What makes Hypercore suitable for Tradle?
  - Hypercore has built-in capabilities for data replication/load-balancing/mobility.
  - Hyperbee is compliant to Level API, which allows it to become a drop-in replacement for AWS DynamoDB, with a Dynalite adapter.
  - Protects every data item from unauthorized modifications and assures that the old data is intact (Thus is similar to blockchain, where all transactions are added to a Merkle tree and new blocks linked to old ones).
# more
