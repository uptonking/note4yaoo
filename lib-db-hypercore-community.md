---
title: lib-db-hypercore-community
tags: [community, hypercore]
created: 2023-09-07T15:58:12.036Z
modified: 2023-09-07T15:58:27.967Z
---

# lib-db-hypercore-community

# guide

# discuss-collab
- ## 

- ## 
# discuss-ipfs-ssb
- ## 

- ## After researching decentralized systems for the last months, I’m sure IPFS was the chosen one protocol, destroyed by implementation by committee. libp2p fuels my nightmares.
- https://twitter.com/LuaSolDel/status/1630663906946326552
  - An over complex stack of modular libraries that you have to pray for to work together. 
  - The TS/JS implementation is mainly focused on node. So much bloat, so little documentation. Things are changing slowly through yet some new slow moving working groups.
  - Also the associations to crypto and web3 did not seem to help in building a good community.

- But I wouldn’t be surprised if protocols like earthstar or hyperhyperspace will overtake IPFS one day. Small projects that explore the space of p2p way better imo. Or maybe holepunch can resurrect Hypercore aka dat and bring it to the web.

- ## [Hypercore Protocol](https://www.reddit.com/r/ipfs/comments/glnra9/hypercore_protocol/)
- dat offers mutability whereas IPFS doesn't
  - It's a _major_ flaw in IPFS currently for a widespread adoption. IPNS is still far from being production ready.
- But IPFS has a vibrant community, with all resulting benefits: many implementations, clients libs, nice and quite exhaustive docs

- ## [The Internet needs the InterPlanetary File System | Hacker News_202210](https://news.ycombinator.com/item?id=33147071)
- TLDR: people whose salary depends on selling IPFS think everyone needs IPFS

- Content addressing is a great idea and it's reliable. Distributed hash tables are on the weaker technology spectrum. I'm rooting for IPFS to replace bittorrent, not IPNS/Hypercore, which I think will have serious scalability/security /privacy problems.
- The most important part of IPFS is Content Based Addressing, not p2p. Content Based addressing provides a natural way for data to be portable, because it's not tied to a storage location or to a transport protocol.

- ## Is there an explanation comparing hypercore to IPFS for example?_20230101
- https://discord.com/channels/709519409932140575/709519410557222964/1059091338261446716
- ipfs is more like hyperdrive but it doesnt use an append only log/blockchain. you want to compare libp2p to hypercore 
- gun.js also does work but I had to dump it because how mark writes his code makes it impossible to maintain/debug

- ## [Just today I was looking into IPFS vs DAT_201906](https://news.ycombinator.com/item?id=20162171)
- I consider dat:// to be the better protocol, in part because of what you mentioned. Other advantages are the lack of duplicating data on disk (IPFS makes a copy of all data it shares) as well as having a versioned history of all changes. That way app owners can't publish malicious versions while preventing people from using the non-malicious ones.
  - Essentially, dat:// behaves like BitTorrent but the torrent data can change.
  - The only downside for both protocols I can think of is that the integration story outside the browser and CLI tools is very poor (there is no FFI/C lib Ic an bind my Rust app to)

- I think DAT is the more likely to succeed. It seems hard to reconcile the longevity of a truly distributed protocol with the need of a private company to retain control.

- There are a bunch of differences but the important ones (imho) are:
  - Dat doesn't use immutable addressing (addresses stay the same when content changes) while IPFS does.
  - Dat at the lowest layers is stream-oriented, allowing stream-oriented services and applications that are near-real-time. IPFS is static blob/object oriented.
- IPFS has a better developed "discovery" network at present (if you use Dat today you are typically in your own island whereas with IPFS you're part of "the" IPFS network). This is being worked on however.

- IPFS doesn't have any concept of file or directory versioning

- ## I'd rather they use hypercore stack which is faster than IPFS and doesn't require a token.
- https://twitter.com/AileenD0ver/status/1571899131656015873
- IPFS doesn't need a token, you are referring to Filecoin
  - Yea should've specified. Was referring to filecoin. 
  - But I still think hypercore is a better solution for a social media platform considering its not organizing block storage at the base level. Its not fast enough

- ## P2P, distributed data networks like Hypercore and IPFS are basically BitTorrent variants
- https://twitter.com/pfrazee/status/1465729030192312326
  - The whole idea is you can share files, databases, and logs using 1) a cryptographic URL, and 2) bandwidth-sharing, where downloaders can become seeders

- In contrast to HTTP, Hyper and IPFS don't associate data with a particular service or dot-com. The URLs use public keys or content hashes instead of IP addresses.
  - It's also possible for anybody to rehost ("seed") the data. 
  - It's a network of data, not hosts. A data mesh.
- This can be really useful for decentralized networks. Data created by FooSky .com could be synced, used, and rehosted by BlueSky .com as if they were a part of the same service.
  - These networks are basically a backbone for syncing datasets between systems.
- Let's look at some limitations.
- First, confidentiality is coarse-grained at this stage. 
  - Unlike normal filesystems, a p2p filesystem often won't have per-file read & write permissions. 
  - To solve that, you either encrypt the files at-rest or move the file to a separate dataset -- or add some separate protocol
- Second, while some really incredible work has been done for performance, these networks will probably never be as fast as HTTP for your first "visit" to a resource. 
  - Peers have to be found, and additional data has to be synced.
- Third, when public keys are used for the URLs, key management becomes a thing.
- Fourth, when multiple devices collaborate on a p2p dataset, you need to use CRDTs. 
  - ( @HypercoreProto is doing some great work on that front.)
- Fifth, even with bandwidth sharing you get no uptime guarantee. *Somebody* has to be the peer of last resort. Users have a habit of turning off their devices, so pinning services may be needed.
- Applying distributed data networks to Bluesky would probably look like this:
  🔹Each user has their own p2p database
  🔹Each tweet, like, follow, and public action would go in their database
  🔹User profiles would point to the user's DB
  - Bluesky providers would use the networks to sync with each other.

- P2P databases are inherently "pull-based, " meaning that you need to ask for the data to receive it.
  - That means Bluesky providers would need a "push-based" model to tell each other about events they aren't already seeing, similar to how ActivityPub uses mailboxes
- P2P data networks are essentially an Internet of Databases. They transfer records in their original, canonical form.
- For public media like tweets, the answer is that everybody has your data because it lives in a commons: the data mesh!

- ## how complex is the interop between IPFS and hypercore?
- https://twitter.com/hhg2288/status/1499486596592287751
- that is easy, there is no interop whatsoever
  - I think hypercore is buus+friends looking at ipfs and doing it right. IPFS is not going anywhere though
- for my stuff, atacama, i can add an adapter for whatever datastore and let it do it's thing. using ipfs+hypercore for off tangle content yeah

- ## Some non-blockchain protocols with self-certifying properties:
- https://twitter.com/arcalinea/status/1474137030204407808
  - Pre-Bitcoin: Git, PGP, BitTorrent, Tahoe-LAFs...
  - Post-Bitcoin: IPFS, Hypercore, SSB, Peergos, Spritely...

- ## 202X's digital service shapes
- https://twitter.com/Stu_B22/status/1331966316165492743
- anonymous content-addressed P2P filesystems 
  - ipfs, dat, hypercore, beaker
- decentralized private data, W3 authenticated 
  - solidproject.org, WebID, dokie.li
- managed cloud services:  GitHub, AWS

- beaker using hypercore
- brave using ipfs
- https://github.com/AgregoreWeb/agregore-browser /js
  - https://agregore.mauve.moe/
  - experimental P2P browser supporting BitTorrent, IPFS, and Hypercore Protocol
  - The web contents are rendered via Chromium using the Electron framework. 

- http://beakerbrowser.com and http://dokie.li each allow authoring and sharing of content directly from the browser.
  - Beaker uses the distributed P2P approach of http://hypercore-protocol.org
  - Dokieli uses the web-standards approach of http://solidproject.org
- These two approaches to user content creation are  complimentary. They are coexistent patterns from different niches of the same unfolding ecosystem.
- P2P content blossoms(兴盛) at creative edge, while Solid content offers fair authenticity.
# discuss
- ## 

- ## 

- ## do you have any hello-world type example of hypercore running in the browser?
- https://discord.com/channels/709519409932140575/709519410557222964/1068520819204051084
  - If it can run directly in the browser without the need of a proxy server, it would be even better
- the problem is the DHT won't run in the browser, so it isn't useful without the proxy to the DHT server
- You have to setup a public dht-relay on a server, and/or you could let users run their own local dht-relay and let them configure host and port on your web app
  - You could easily do this on any React project
  - [browser-dht.js](https://gist.github.com/LuKks/c144fa0f72ebfd303515d0ce7dadb477)

- ## 💰 blue sky is doing a lot of stuff and was born from jack/twitter who is also making "web5". theres motive there. 
- https://discord.com/channels/985129863348371516/1057659276778274986/1085946345031995495
  - ipfs/filecoin have their own VC's. 
  - every pure p2p project has no real funding. 
  - hypercore is in an interesting spot as it has a lot of funding but its almost more grass roots and aligning with BTC, and not creating another blockchain 
  - as for lume, the answer is hosting services and web3 domains 
- So my hope is lume can bridge divides and do things better since I have no puppet master.
  - and libp2p and hyper are becoming the primary 2 nets. and tbh you could prob get hyper chains running over libp2p. they use a similar DHT, same key curve, and both use noise. So they are building in parallel in a way
  - and libp2p and hyper are becoming the primary 2 nets. and tbh you could prob get hyper chains running over libp2p. they use a similar DHT, same key curve, and both use noise. So they are building in parallel in a way
  - to me though libp2p feels like they built IPFS then went backwards to generalize
  - hyper is generalized 1st and not overengineered

- ## In the past, Hypercore has used a daemon called "hyperspace."_202111
- https://twitter.com/pfrazee/status/1456017050074234889
  - This was used to centralize all the data and networking logic, which apps would then share. 
  - Well: It looks like that won't be necessary anymore! Apps can just run Hypercore and its network themselves.
- That's possible because the networking layer has gotten a lot "cheaper" to use.
  - The upside: no cumbersome daemon management, and  local apps share data the same way that remote apps share data. It's all down to "do you have the keys" and "are you in the multiwriter pool"
- Now about the new multiwriter (Autobase):
  - It's looking like the pattern is simply `oplogs + autobase` .
  - "Oplogs" are operations logs, meaning they're a log of the actions you take. (Each oplog is a hypercore with a vector clock)
  - E.g. A key-value database would be `PUT foo="bar` and `DEL foo`

- The "Autobase" has its own hypercore which is created by merging the oplogs together with some CRDT magic.
  - A naive merge would just write the oplogs to the autobase, meaning the autobase's core would just be a linear merge of the oplogs.
  - Autobase lets you specify a custom merge function where you can put your own business logic. This means you can build custom data structure on top of Autobase.
- In fact, if our oplog is for a key-value store, then we can use the Hyperbee K/V store on top of Autobase so that `PUT foo=bar` gets translated into a `bee.put('foo', 'bar')` .
  - When somebody reads an Autobase, they will (typically) use the autobase core created by somebody else, meaning they don't have to read the full oplog histories.
  - Fast random-reads over the network.
  - If we're using Hyperbee on top of our Autobase core, then reading that Hyperbee will be exactly as fast as reading a normal, non-autobased Hyperbee.

- Even more interesting: since your oplogs can be custom too, you can put lots of things in there.
  - You could make an (arguably better) version of Hyperdrive by doing `oplog + hyperbee-autobase`, where the binary data is stored in the oplog rather than another separate log.

- As a result, it's looking like `oplog + autobase` will be such a general pattern that it'll be useful for single writer too.
  - That's good because if you decide you need multiwriter later, your single-writer autobase will be able to smoothly upgrade.

- The one last *very insider* piece of info: the networking logic now optimistically replicates any hypercore in memory. 
  - That should hopefully mean we don't need any custom logic for replicating multi-core data structures.

- ## [Hypercore has realtime sync, but is limited to log structured data.| Hacker News](https://news.ycombinator.com/item?id=15467438)
- Hypercore has realtime sync, but is limited to log structured data. Dat can do diffs on data, but is meant for large datasets, not realtime changes. This sounds like it would be difficult (or not scalable) to build something like a Wiki, features in social networks, Trello, or other apps (i.e., anything with shared mutable state). How would you do this?
  - 👉🏻 The real-time syncing immutable, append-only log that hypercore provides can also be accessed randomly, allowing for lots of cool parallel/distributed log processing architectures (Kappa architecture), similar to Kafka (which is also based on immutable, append-only logs). 
  - We have just focused on syncing a filesystem at first because we had a strong use case there, but you could totally build a CRDT on top of an append only log.

- ## Hyperbee is just one writter. If you want "multiple writters" (which is multiple hypercores combined into one) then you can use autobase
- https://discord.com/channels/985129863348371516/985129863348371519/1034609699552776222
  - use the GitHub branch directly (npm i hypercore-protocol/autobase), because the npm package is outdated
- is autobase supposed to replace a regular database for hypercore?
  - Not necessarily, because you could use hyperbee without autobase

# discuss-networking
- ## 

- ## 

- ## IPFS has been working on gossipsub for years and years and it still only barely works 
- https://discord.com/channels/709519409932140575/912672739947585576/1079181966232006676
  - but maybe I really should use IPFS given they have a lot of it figured out...
  - these problems worry me because without a very very non trivial system to prevent it, it seems very trivial for someone to just spam gossip constantly and clog the network
  - I have ways of rate limiting posting, which involve actually scanning the posts, but that only stops it once they have already crossed the network. Rate limiting before that is more difficult
- yeah that's a valid concern. 
  - the autobase-manager might be improved a bit on this end to reduce messages. 
  - but generally this concern about a malicious actor on the network would be a communication layer (aka the means of acquiring a stream) combined with a app layer responsibility. 
  - If using hyperswarm, you have the ability to .ban() a peer when they are clogging the network. 
  - on the autobase-manager end, its main concern is gossiping core keys. the allow() argument puts the business logic for detecting and rejecting spam into the developers hands.
  - in the end autobase-manager doesn't make the connection, just uses it to distribute keys
- Yeah but it's the part that is using the gossip, so it has information to potentially determine who is being malicious, ie, sending things unnecessarily. That's really why it's complicated, this traverses multiple layers, as a problem.
  - At the communication layer, you might be able to tell if someone is using a lot of bandwidth, but that's not necessarily enough to determine if they are trying to attack you
  - I don't have a simple solution for this, though

- right that's why i was saying it was communication layer combined with app layer. 
  - So **let the app decide whats an actual abuse of the communication and then ban peers etc**. 
  - If its an autobase input or output thats abusing the system, then the allow() gives the app the choice to block the key from being added again.
  - a nice catch all for either scenario is letting the user ban a peer / hypercore. it wont mean that the user will catch the problem in time but it gives them the power.

- ## 🤔 To be clear: IPFS itself won't work because it is ridiculous, but the promise of P2P addressable databases will materialize and will be so easy and performant that even Fiatjaf will use it.
- https://twitter.com/ArNazeh/status/1628017292209451011
- Hyperswarm only does one thing: find peers even ones behind an aggressive firewall and connect them to each other, and that is the end as far as the DHT cares.
  - This is exactly why it actually works, and why IPFS is a mess, because that line is blurry as fuck in IPFS.

- https://twitter.com/n0computer/status/1627332856698617856
- Hyperswarm is already working like a charm, and can only get better with more caching, TTL, and tolerance to occasional churned data (max ~10 minutes).
  - Agent-based addressing (max one topic per identity) makes the problem _much_ more manageable.
- I don't care about hypercore, hyperswarm is already good enough.
- Hyperswarm's Rust efforts are individual and it is not my only bet, more likely, Iroh from @n0computer folks will become as good as Hyperswarm as it abandons IPFS compatibility.
  - From what I read they still want to make each chunk of bytes content-addressable, they just think they can do better than 10 years of dedicated IPFS development.
- The biggest harm IPFS has brought to the world was to say something (p2p content-addressable global filesystem) is not only possible but already done and working -- and then waste the time and resources of anyone who is convinced enough to try to make it work for some use case.
- All distributed systems are a game of faking a thing that isn’t possible. But we have all sorts of success stories that come from careful trade offs
  - I don't understand why isn't Agent addressability enough, it seems to me that replacing DNS is with a p2p alternative is already a monumental success. Content addressability (for deduplication) is fine, but content discovery for each entry in a database or file in website is why?
- Agent addressability is actually the thing we rely on most from IPFS in Peergos, and the critical thing enabling us to be independent of DNS. We address blocks by their cid, but that's not how we discover them. We've built on this p2p HTTP proxy from 2018
- We do plan to content address all data within the system, and that creates some very real scaling constraints. That will naturally rule out use cases, like, uh, replacing the Internet.

- I am pretty sure IPFS discover blocks individually, that is one reason why n0 folks are breaking compat

- We talked, he is not using IPFS at all, he is just using IPLD, and maybe Bitwise, both suck.
  - Thus, he doesn't need Hyperswarm, and even Hypercore is not the best fot for his use case either.
  - He needs Git for databases, but so do I.
# discuss-oplog
- ## 

- ## 


- ## [I've been developing high performance databases for the last five years | Hacker News](https://news.ycombinator.com/item?id=8979043)
- It's tough to beat MVCC for a database that wants isolated concurrent transactions. Append only designs seem attractive, but they don't actually help much with write throughput on SSDs (but avoiding in-place updates does, due to erase blocks.) And they often require writing much more information. E.g. writing 100 bytes in LMDB, which is an append only btree, requires copying all pages from the root to the leaf and writing them all out, typically 64k or more. Writing 100 bytes to a transaction log or WAL costs about 100 bytes. There's a huge write amplification going on.

- ## [A way to do atomic writes | Hacker News](https://news.ycombinator.com/item?id=20040779)
- Appending log based file system has a lot of appeals. A lot of hard problems, like atomic write, become trivial. A log based FS shares similar properties as the transaction log in RDBMS, making consistency and recovery easy. Write performance is fantastic. With enough cache memory, read performance should be good, too. The only down-size is the performance hit when doing garbage collection. 
  - Totally agree. Log based file system makes things much easier, such as atomic write, data consistency and failure recovery. Along with COW semantics, transaction isolation also becomes easier. By its append-only writing nature, file versioning is trivial as well. Garbage collection is performance downside indeed, but it can be mitigated by COW switching and delayed bulk collection IMHO. Overall, the cost is worthwhile and that is what I am currently doing in ZboxFS

- I think elements of that generationality are the foundations of the Log Structured Merge Trees used by KV Stores like LevelDB and RocksDB. Atleast I think that's the same concept, I'm not well read on filesystems.
- Yes, LSMT is a good example of pushing the idea of a hybrid append log and in memory data structure further.
- However, LSMT is for relatively smaller data set, i.e. ordered key-value. It has worse write amplification than a simple append log. There're 2~3 writes per change.
  - Also it doesn't offer help to address the frequent update block problem. All versions of a data change are written to disk. A merge is needed to get rid of the old versions.
  - But it has a number of good implementation ideas that can be borrowed.

- ## 🤔 [Immutable Data (2015) | Hacker News](https://news.ycombinator.com/item?id=36470739)
- Author here, 8 years on. Although the advantages are real, I can't say I have had much opportunity to implement schemas like this. The extra complexity is usually what gets in the way, and it can add difficulty to migrations.
  - I think it would be useful in certain scenarios, for specific parts of an application. Usually where the history is relevant to the user. I think using it more generally could be helped by some theoretical tooling for common patterns and data migrations.
- You can use Datomic for instance or SirixDB on which I'm working in my spare time.
  - The idea is an indexed append-only log-structure and to use a functional tree structure (sharing unchanged nodes between revisions) plus a novel algorithm to balance incremental and full dumps of database pages using a sliding window instead.

- 👉🏻 I agree this is **more of an application level concern than a database thing**. If you need to maintain a history for the user requirement then you will naturally land on a scheme like this.
- We also have help from other quarters nowadays.
- Databases often provide a time travel feature where we can query `AS OF` a certain date.
- Some people went down the whole event sourcing/CQRS/Kafka route where there is an immutable audit log of updates.
- Data warehousing has moved on such that we can implement “slowly changing data” there.
- All in all, complicating our application logic, migrations and GDPR in order to maintain history in line of business applications might not be worthwhile.

- Suppose that instead of a typical User table, you have a User_Revision table like suggested. If this information gets leaked, the user is exposed to more vectors of attack.
  - GDPR and the right to having your personal data deleted certainly puts a bit of a stopper on using an immutable database for anything personally identifying.

- I'll argue that this is bad design. It works as long as the amount of data is small, but even then taking a low-data scenario and building lots of views or triggers just seems a bit weird. 

- ## [Speaking of B-trees, I find CouchDB's implementation really interesting: the bac... | Hacker News](https://news.ycombinator.com/item?id=7522724)
- Speaking of B-trees, I find CouchDB's implementation really interesting: the backing file is append-only, meaning that modifying the tree implies appending the modified nodes at the end of the file (for example, if I change a leaf, than I rewrite it at the end of the file, and rewrite its parent so that it points to the leaf's new position, and so on until we reach the root node).
  - Sounds like a waste of space, but it solves a bunch of problems, like being crash-proof (since we never overwrite anything, it's always possible to just find the last root) and allowing reads concurrent with a write without any synchronizing necessary. Plus, it's actually optimized for SSD's due to its log-like structure!

- Massive waste of space though. LMDB is also copy-on-write and crash-proof but doesn't require compaction like CouchDB does

- ## [Building a Distributed Log from Scratch, Part 1: Storage Mechanics | Hacker News](https://news.ycombinator.com/item?id=15983185)
- [Building a Distributed Log from Scratch, Part 1: Storage Mechanics – Brave New Geek](https://bravenewgeek.com/building-a-distributed-log-from-scratch-part-1-storage-mechanics/)

- I have to admit that I only recently got familiar with logs. 
  - I was designing a B+Tree in Python for fun and was struggling to make it survive crashes: a single insertion in a tree often results in multiple page writes which is not atomic.
  - The solution to this problem is simple and elegant with a **Write-Ahead Log**. Every page write is appended to the log and only merged back into the tree file when it's sure that the log is safely written to storage.

- If you're interested in those, there are at least two other designs you should have a look at:
  - couchdb uses a single file for each db, which means the write ahead log _is_ the storage. The atomicity is guaranteed by saying that the latest root is the valid root. If writes are interrupted, everything since the last root is invalid and discarded upon restart. A simple design that just works, although it tends to be wasteful and requires frequent compactions
  - lmdb uses copy on write to make sure space is properly used, and atomicity is provided by sharing only the strict minimal pieces of information, so small in fact atomicity is guaranteed by the os.

- ## [The database I wish I had : programming](https://www.reddit.com/r/programming/comments/ijwz5b/the_database_i_wish_i_had/)
- technically PouchDB is also append-only, but its history tracking isn't as elaborate as git.
  - PouchDB's _rev field is a common pitfall for new people when starting with it.
  - I was trying to use those _revs for revision control myself, and I had to watch her say it a few times in order to convince myself to stop doing it

- ## The real-time syncing immutable, append-only log that hypercore provides can also be accessed randomly, 
- https://news.ycombinator.com/item?id=15468295
  - allowing for lots of cool parallel/distributed log processing architectures (**Kappa architecture**), similar to Kafka (which is also based on immutable, append-only logs). 
  - We have just focused on syncing a filesystem at first because we had a strong use case there, but **you could totally build a CRDT on top of an append only log**.

- ## I need a general term for a data structure that contains all its past revisions. Examples:
- https://twitter.com/gritzko/status/1156782170041700352
  - Immutable tree (like in git)
  - Weave (like in SCCS.. BitKeeper)
  - Append-only log (like everywhere)

- ## When explaining @apachekafka , most articles first discuss topics, then partitions. 
- https://twitter.com/gunnarmorling/status/1413401342840819714
  - I feel it's more intuitive to do it the other way around: first introduce partitions as the implementation of the append-only log concept, then topics as logical groups of partitions.
- I think it depends. From an RDBMS background, I found topics a much more natural parallel to ~= tables, and then getting into it from there. I agree about partitions being the natural entry point from the purely append-only log concept though
- Partitions are the building blocks that developers write code to, how Kafka scale, how it provides durability (hello replicas), and how it is administered. This became so clear to me when I was writing the bucket priority pattern

- ## Reflecting on the fact that I've built some flavor of the "immutable, append-only log + materialized views" pattern into every non-trivial software project I've built since 2006.
- https://twitter.com/neil_conway/status/994717227621347329
- Similar here, but not the same: My projects have always involved materialized views, not always append-only, and always with transparent rewrite.
- This is exactly what we do with our IoT commit logs. Let’s face it, once something is digitised, the world needs to accept that it can never be removed; it can only really become inaccessible.
