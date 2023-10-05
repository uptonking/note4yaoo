---
title: lib-db-hypercore-blog
tags: [blog, hypercore]
created: 2023-09-07T15:58:51.492Z
modified: 2023-09-07T15:59:12.947Z
---

# lib-db-hypercore-blog

# guide

# blogs

## [A New Direction for Iroh_202302](https://n0.computer/blog/a-new-direction-for-iroh/)

- Iroh has been built as an implementation of the InterPlanetary File System (IPFS) focused on interoperability with Kubo, the reference implementation of IPFS. 
  - In the near future Iroh will break interoperability with Kubo, with the goal of moving the IPFS project forward.
- IPFS is a bunch of specs, and we're not breaking from all of them. Iroh is still an IPFS implementation: it continues to use CIDs.

## [You Don't Need A Blockchain](https://gist.github.com/joepie91/a90e21e3d06e1ad924a1bfdfe3c16902)

- Blockchains aren't a desirable thing; they're defined by having trustless consensus, which necessarily has to involve some form of costly signaling to work; that's what prevents attacks like sybil attacks.

- If you just need to provide authenticity for a piece of data: A cryptographic signature. 
- If you need an immutable chain of data: Something simple that uses a merkle tree. A well-known example of this application is Git, especially in combination with signed commits.
- If that immutable chain of data needs to be added to by multiple parties (eg. companies) that mutually distrust each other: A cryptographically signed, append-only, replicated log.
- If that immutable chain of data needs to be added to by multiple parties (eg. companies) that mutually distrust each other: A cryptographically signed, append-only, replicated log.

- 
- 

## [Beaker Browser is now archived_202212](https://github.com/beakerbrowser/beaker/blob/master/archive-notice.md)

- The backstory to Beaker starts with Secure Scuttlebutt (SSB). I had been working on applications for SSB for about two years (2014-2016) and really getting my feet wet with decentralized tech.
- With SSB, we had made a social-networking protocol that was local first (meaning it ran mostly on-device) and was therefore extremely hackable. 
- The problem as I saw it was that app-distribution was too hard. Most of the SSB clients at the time were built on Electron or were local-hosted web servers. I wanted apps to be as easy to load as websites.
- This is how the idea for Beaker started. If apps could be distributed with one of these bittorrent-variants, I figured, and then run within a safe sandbox, then we'd be able to create a flourishing ecosystem of apps on shared decentralized network. That was the big premise.
  - with electron, I was able to produce a demo of Beaker hosting websites via dat/hypercore within 2 weeks. This got a positive response from folks
  - After I ran out of ideas for making Beaker work, I decided to give a p2p + servers hybrid a shot with a project called CTZN, another stab at a social network. 
  - The smartest thing I did there was live stream every day of development
  - That live-stream ultimately caught the attention of Jay Graber as she was forming the Bluesky team, and at the start of 2022 I began working with Bluesky. 
- A smattering of additional lessons I learned over the years.
- Don't be too proud to follow people with inspiration. 
  - Every time things went better for me, it's because I followed someone who was already doing something great.
- With Bluesky we've opted for using p2p structures (IPLD) on a federated network, giving us some of the key advantages of p2p like account portability while retaining the performance and reliability advantages of servers. 
  - but I think it's a bad fit for large scale social networks and sticking with it for Bluesky would've been a mistake.
- Never go negative with competiting projects. 
  - Stay focused on the shared mission if there is one.
  - As I ended up more in the dat/hyper ecosystem, IPFS was often raised as a competing technology and I was frequently asked to comment on the differences. I never went negative, and thank goodness I didn't because one of my colleagues at Bluesky is a core contributor on IPFS, and we've become exceedingly good friends. Besides, going negative is a bad look.
# blogs-comparisons

## [Comparing Peer to Peer Protocols_202203](https://blog.mauve.moe/posts/protocol-comparisons)

- BitTorrent, IPFS, Secure Scuttlebutt (SSB) and Hypercore

### Content and Data Model

- IPFS is similar to bittorent in that it operates on Merkle Trees, but instead of grouping data together under a single infohash, it focuses on addressing each chunk of data individually.
  - IPFS uses a data format called IPLD (Interplanetary Linked Data) which takes Merkle Dags to the next level by creating a powerful data model with different "types" and ways of traversing data.
  - IPFS builds on top of IPLD by describing a format for data to represent files and combines it with it's p2p network to publish and load files.
  - Another advantage of IPFS over BitTorrent is that large datasets can be handled by sparsely loading just the chunks that you need as you traverse the merkle dag. 
  - IPFS stores data with "repositories" or "block stores" which can be configured to store data in various formats.
  - Generally, the "blockstore" handles storing binary data which represents the encoded IPLD nodes or raw buffers so it can be very space efficient whe combined with deduplication.

- Hypercore deviates a bit away from content addressability in that it uses Merkle Dags to represent an "append-only log" where you can add new blocks to the end of the log but not change any earlier ones.
  - This log is represented using the SLEEP file format.
  - On top of this append only log abstraction, the Hypercore community uses the Hyperdrive filesystem abstraction which stores a tree of file metadata (using Hash Array Mapped Trie (HAMT) data structure) where each node in the "tree" is appended to the log, and individual nodes are referenced by their index within the log.
  - This enables very fast lookup since you can exchange bitfields with remote peers to download the subsets of the trie that you need
  - The actual file data is stored in a separate hypercore log so that you can easily stream files into it and link to just the range within the log in the file metadata rather than needing the whole merkle tree or to mix data with the HAMT information.
  - Hypercore also suffers from the same limitations of BitTorrent in that data isn't shared between datasets, but the tradeoff is that data within the dataset is a lot faster to discover and load.
  - Similar to IPFS hypercores store arbitrary binary data and uses encoding just for the nodes within the HAMT structure from Hyperdrive.

- SSB takes a similar approach to Hypercore in that it uses append only logs (called Feeds) to represent data.
  - A difference from Hypercore is that instead of using SLEEP files to store logs, it uses **JSON** files with "backlinks" that point to previous entries within the append only log.
  - These messages are typically traversed and processed into local databases along the lines of the Kappa Architecture for processing ordered streams of data.
  - 👉🏻 The actual messages themselves are typically stored along side the indexes within the local SSB database rather than needing extra files to store data like in Hypercore.
  - Since JSON isn't the best for storing large chunks of binary data, SSB implementations also have a method of exchaging arbitrary blobs of data which are content-addressible. 

### Mutability

- IPFS has had mutability from early on in the form of IPNS (InterPlanetary Name System).
  - This had the same limitations of BitTorrent's BEP46 where you would need to periodically poll the DHT to find updates and was generally prone to errors.
  - The latest version of IPNS can make use of an experimental Pubsub APIs. 

- Since Hypercore uses public keys for identifying content, it can be very fast for getting the "latest" version of a dataset.
  - Even though the append-only-log is immutable, modifying a file within a Hyperdrive can propogate out pretty quickly to other peers and is viable for distributing data in the form of JSON files.
  - In my experience, hypercore mutability has been the most reliable and fastest of the protocols described here.

- Similarly to Hypercore, SSB's public keys and active replication streams mean that data can propagate fairly quickly via peers.
  - One difference is that the network topology of SSB relies more on central "pub" servers and "rooms" to discover peers

### conclusion

- a series of tradeoffs to choose from
- For those that don't want to settle on a single protocol, check out useful cross-protocol projects such as Distributed Press or the Agregore Browser.

### ref

## [IPFS and Friends: A Qualitative Comparison of Next Generation Peer-to-Peer Data Networks](https://arxiv.org/abs/2102.12737)

### ipfs

- concepts such as content addressing and deduplication are promising as they have the potential to improve retrieval times and storage overhead.
- different subprotocols like libp2p for man- aging the peer discovery and connection handling, and Bitswap for exchanging data are great developments, that provide many opportunities for other P2P networks.
- The wide support of different protocols increases the difficulty to grasp the finer details of IPFS, though.
- IPFS could have similar privacy problems to BitTorrent. 
- Further more, for good and bad it is not possible to prevent replication or enforce deletion of content once released.

### hypercore

- supports incremental versioning of the content and meta data similar to Git. 
- supports different storage modes
- supports subscription to live changes of all/any files in a directory
- All communication in the protocol is encrypted. 
- The protocol is designed to share large amounts of mutable data. 
- Hypercore allows sharing of data by exchanging a public key. 
  - It is possible to acquire a specific version and only specific regions of the data. 
  - This makes it simple, especially for large datasets, and allows mutable data.

- but it is not possible to reverse the public key. 
- lack of additional authentication mechanisms beyond the public key, which prevents additional fine-grained access control
- Hypercore has no incentive structure for replicating data and the data persistence relies on its participants.

## [Paul explains the difference between IPFS and Hypercore - YouTube_202012](https://www.youtube.com/watch?v=Sfi3KewTGQM)

- Jerry Green made very well articulated points:
  1. Dat/Hypercore indeed is "for geeks interested in p2p" now, but I feel it is nearing the point where it can explode in usage. I am making this point in the above github repo https://github.com/tradle/why-hypercore
  2. The most interesting point you make, Jerry, is that the path to mainstream is in  "decoupling apps from data". I am working exactly on that right now!! 

## [Exploring Alternatives to the Centralized Web: ipfs/hypercore/ssb/bitTorrent](https://hypha.coop/dripline/p2p-primer-part-1/)

- [Exploring Data Models and Mutability](https://hypha.coop/dripline/p2p-primer-part-2/)

- IPFS has been building buzz among blockchain communities by acting as a decentralized file storage alternative to central file servers for things like Non-Fungible Tokens (NFT) and various bits of web content such as COMPOST. 
  - Its high level APIs have also been used with tools like WebRecorder to make it easier to archive content and preserve it in immutable records while deduplicating file content whenever possible.

- Most content on SSB is locked away in people’s social graphs and can only be accessed if you get introduced into these networks

- IPFS has a couple of approaches to links. Primarily they use Content Identifiers, a.k.a. CIDs, with two ways of turning them into links.

## [How a Hypercore P2P innovation could bring more privacy to IPFS_202201](https://www.ctrl.blog/entry/dht-privacy-discovery-hash.html)

- https://twitter.com/serapath/status/1488308553177829380
  - Via the Hypercore Protocol it is necessary to know the CID and Discovery hash for every file request. This added layer protects hosts from being asked for everything & anything they've got from curious snoopers.
  - In my opinion the latest DHT (hyperswarm) improvements are even more important. A DHT node does not share the IP of a peer if does not consent. And I's all E2EE(!)
- What the blogpost gets a little bit wrong is that hypercore does NOT use content addressing, instead it uses the public key used for signing the data address (which is then hashed for discovery).
# more
