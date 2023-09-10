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

- ## 

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

- ## 

- ## 

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

- ## 

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
