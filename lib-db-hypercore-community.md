---
title: lib-db-hypercore-community
tags: [community, hypercore]
created: 2023-09-07T15:58:12.036Z
modified: 2023-09-07T15:58:27.967Z
---

# lib-db-hypercore-community

# guide

- forums
  - [ipfs hypercore - Search / Twitter](https://twitter.com/search?q=ipfs%20hypercore&f=live)
# discuss-stars
- ## 

- ## 

- ## 🎯 Is the Holepunch team still planning to open source Keet at some point? _202310
- https://discord.com/channels/985129863348371516/985894366910509127/1159496428301865042
- Yes, it's planned for the next year

- ## [Hypercore Protocol: Peer-to-peer data sharing | Hacker News_202205](https://news.ycombinator.com/item?id=31384268)
- The issue I have with hypercore is that it's neither fully mutable, nor multiwriter.
  - As far as I know, you can't fully have both(Because of the tombstone problem and source of truth issues), but either one individually can be implemented.
  - True deletion, or multiwriter within one DB would have been nice to have.
  - Other than that, it looks to be a great thing. 
  - I think it is more practical than IPFS at the moment because IPFS lacks any top level concept of feeds or collections, just one giant DAG with random access.
- The are working on multi-writer for Hypercore 10! https://github.com/hypercore-protocol/autobase

- ## 💡 [Merklizing the key/value store for fun and profit | Hacker News_202306](https://news.ycombinator.com/item?id=36265429)
- What’s worth mentioning is that IPFS is built on top of a data model named IPLD.
  - If you are planning on doing your own experiments with Merkle tree and such, I can strongly recommend using IPLD as well. The IPLD project has standard libraries for a bunch of programming languages.
  - The advantage of using IPLD is that you can use regular IPFS tooling to inspect the data and make backups/restores. Regardless of your desire to share the data over IPFS.

- Wouldn't it be simpler to use a trie over the hashes instead? It seems to me like it would have the properties desired here. I think the parent/child rule described here might actually result in some kind of trie.
  - The difference is that a trie over the hashes doesn't preserve lexicographical key ordering or support range queries, which are typically expected from key/value stores. But you're right - if you just need get / set / delete, you could just do that!

- I read this with great interest. Sometimes technologies come around that make me seriously wonder if I should embrace them or continue on the path I’ve already designed.
  - They include: CRDTs, PouchDB, hypercore, etc.
  - What I currently have is my own, PHP-based implementation of essentially a history of “collaborative documents that evolve through time” — with each document having one machine as a source of truth
- I think that 🤼🏻 syncing and CRDTs (y.js and automerge) can be excellent for collaborating on documents, but not so great for chatrooms and smart contracts/crypto where order of operations matters. 
  - For those, you can implement optimistic interface updates but when conflicts (rarely) arise, your interface may roll back changes it displayed. This is especially true after a netsplit(网络断裂).
  - I thought about using PouchDB but the thing is that CouchDB is an extra process people have to run and we want our stuff to run anywhere Wordpress does. Ditto for hypercore. These are great technologies, but it seems what we have is great for fhe very reason tht it’s in PHP - still the most widely supported commodity hosting environment in the world by far. 
- 👉🏻 Automerge and y.js are absolutely great for collaboration on blocks of text or structured documents (or anything that can be modelled as such). 
  - They are purely for conflict resolution, so if you don't have conflicts, or your use case manages to make the impact of conflicts negligible, don't bother with them. 
  - They are very easy to implement if you do need them - the barrier most people face is understanding them enough to decide if and how to use them. Just keep it simple.
- 👉🏻 Hypercore is a p2p solution for synchronising streams of data. It can be used raw, for streaming updates, or you can use the abstractions over it to keep filesystems or databases in sync. 
  - There's a significant difference between the decision about hypercore vs CRDTs - hypercore can potentially remove the need for you to maintain and operate a specific server, allowing all clients to be servers. This also reduces the dependency of the user on infrastructure - your servers, the Internet, a friendly government, etc. If that might be useful to you or your users, it's worth considering. 
  - Unlike PouchDB, it's a low level abstraction that can open up really new ways of thinking about shared information. PouchDB by contrast is 'just' a p2p syncing database. 
  - Also important: hypercore doesn't require its own process - you can roll it into your code directly, or have it in a separate process if you want.
  - Of all the things you mentioned, I'd say that hypercore is the only one worth diving into regardless of whether you seem to need it. You'll be a better systems designer and engineer once you understand it, and will have an expanded landscape of possibility when you can leverage it.

- Question:since doing this requires hashing your entire tree, what are the implications of doing this hashing operation on possibly millions of entries (which I'm estimating is the scale at which comparing linearly really start being noticably slow)?
  - The merkle tree is persisted, and updating it is only log(n). You only have to "hash 2n elements" once, and then incrementally maintain it. It's negligible overhead for free log(n) diffing.
# discuss-keet
- ## 

- ## When will Keet be fully open sourced?_202312
- https://discord.com/channels/985129863348371516/985129863348371519/1186957837767823370
- I think it's in February... Or something like that.

- how does keet compare to discord and teamspeak with regard to latency and audio quality?
  - for calls? Its better imo.
- Keet is better than Signal too for calls. Udx is the transport layer I believe
  - https://github.com/holepunchto/libudx

- https://discord.com/channels/985129863348371516/985894366910509127/1159496428301865042
  - Is the Holepunch team still planning to open source Keet at some point?_202310
  - Yes, it's planned for the next year
# discuss-collab
- ## 

- ## 
# discuss-holochain
- ## 

- ## 

- ## What is the best use case of #Holochain?
- https://twitter.com/amig_gomes/status/1650123710890754053
- Anything. List of apps being built right now in the link.
  - Me and our team are building 4 projects on Holochain and I don't see any of the problems you are telling about here.
  - https://airtable.com/app0AdzRsynFEsD9z/shrRojl48GW5te3ap/tblWsBn3J5hyOVOUv

- https://twitter.com/helioscomm/status/1750592919420170502
- #Holochain and unforkability
- I believe there has been given a definition to 'forking' in a Holo team very narrow technically way.  But forgetting that words can have meaning outside that scope. If I build a UI around my personal archive on my Holoport. People can copy it and alter it? Without my permission?
  - you're right, we kind of have muddied that term. To build on GitHub's popularisation of forking to mean "make your own copy of a publicly accessible resource and modify it", HC treats hApp backend code (not the UI) as a public resource, along with the data shared by people who run that backend code and communicate with each other.
  - So if you built your own little personal UI to access the hApp code you share in common w/ others, no, there's no reason you have to share the UI too. Sthg can only be forked if it's been shared.
# discuss-ipfs-ssb
- ## 

- ## 

- ## 

- ## To date, IPFS has been a project focused on data. 
- https://twitter.com/FISSIONcodes/status/1719685936068391232
  - IPVM is a spec for bringing content-addressed execution to content-addressed data on IPFS. 
  - To this end, the IPVM standard aims to be the easiest, fastest, most secure, and open way to run decentralized compute jobs everywhere.
- All without a token
  - It's all self-hosted. It's very rare that you have state is globally contested and needs consensus. Instead you (the client running in your browser) runs the compute and publishes a verifiable proof to the IFPS network. Anyone who cares about the same stuff you do can gossip.
  - And ofc, your browser is also self-hosting. User never knows about it. 100% verifiable, recoverable, decentralized, however you wanna call it.

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

- ## [Quiet – Encrypted P2P team chat with no servers, just Tor | Hacker News_202309](https://news.ycombinator.com/item?id=37477512)
- While I do like the idea behind a P2P E2EE chat, I believe that unless you're willing to invest heavily into OrbitDB and IPFS, this project will stay niche at best.
  - The performance issues that come along with running OrbitDB/IPFS on a machine, let alone a mobile device, are still significant unfortunately. Adding Electron on top of what is already a heavy-weight application is probably going to make people's devices go brrrrr all the time. Not only that, but I would argue that for instant communication this stack might not be the best idea in terms of performance in first place.
  - Besides, the way IPFS has been (and still keeps) changing their dozens of libraries doesn't make development particularly smooth either. OrbitDB is always behind the latest IPFS version due to all these changes that are being introduced. 
  - The integration with Tor is another thing that will likely be a time drain for developers, as other people here already pointed out, and that will lead to even more performance issues down the line.

- ## I am struggling to get libp2p to holepunch out of the box in the first place so it seems few massive steps are skipped here! 
- https://twitter.com/ArNazeh/status/1584522803449323520
  - I share their goal for a p2p alternative to Google drive that can be the backend of distributed local first apps
- Yup, we’ve felt the networking pain too! We’re working on new transports for the browser that operate over mature channels like HTTPS. 
  - We have given up on browsers and use a websocket connection to a full DHT node that still doesn't hold the relayed node keys. Seems the best possible compromise and keep the burden on the user or their app provider instead of tangling the rest of the DHT with multiple transports
- Outside of browsers, Hyperswarm DHT is as perfect as it gets honestly, only failed me in ridiculous situations like a WSL in a windows VM in the cloud :) 
- The only reason I checked Libp2p with its over abstraction tendency, is that Hyperswarm is JS only still
- Also, while I am inspired by wnfs, I think it would be much better served by Hypercore, Hyperbee, and Hyperdrive. The only reason I can't argue for that stack over IPFS is that it is also JS only.
- Lots of examples of wiser and more focused design decisions made on the Hyper stack, even if it is not implemented in a language that helps its adoption, and even if the devs involved are not investing as much as protocol labs in marketing and DX for quick wide adoption.

- ## I'm a bit bummed the BitTorrent mutable torrents proposal (BEP-46) never got standardised. 
- https://twitter.com/liamzebedee/status/1537347394613878784
  - That would have been so useful for building easy p2p apps.
  - Like imagine a decentralized sequencer where you can just join a p2p swarm and mirror the txs for the chain, contributing bandwidth. Probably someone would write some form of airdrop for nodes that share bandwidth (a la private trackers).
- The sad thing is @libp2p and @IPFS just don't have this functionality, the focus seems to be on pinning but it's realistically a very clunky UX. IPFS is like boomer centralized orderbooks compared to bittorrents's uniswap-like ux (just join and seed, easy)
- hypercore has swarming, mutability, and generally seems very clean
- Hey! `ipfs add {file}` starts "seeding" right away. `pin add` does the same, and persists it. Let me know if you have ideas for making that simpler or easier, I'm happy to file an issue.
- Yeah the API’s make sense, it’s the opaqueness that gets me - how do you know how well replicated your IPFS file is? And when you start your node, how well connected is it? (Eg to cloudflare)
  - different trade-offs really. libp2p is designed around transport agnosticism. maybe could build a torrent transport for it 

- ## [Storing users data into ipfs : ipfs](https://www.reddit.com/r/ipfs/comments/wk5wph/storing_users_data_into_ipfs/)
- If you do a little research, you will find a decent number of projects that are experimenting with ideas for distributed social media, some using ipfs. There's a paper on a project called plebbit. 
- There are distributed database solutions, but nearly all of them require the user to "own" some part if not all of the database. I find gun database fascinating, but it requires everyone to run a node.js client iirc. 
- There's also non ipfs tech that is peer to peer such as hypercore protocol (not to be confused with hypercore networks).
- GUN does not require everyone run NodeJS. GUN is one of the few that runs in-browser.

- ## [Quiet – Encrypted P2P team chat with no servers, just Tor | Hacker News_202309](https://news.ycombinator.com/item?id=37477512)
- The performance issues that come along with running OrbitDB/IPFS on a machine, let alone a mobile device, are still significant unfortunately. Adding Electron on top of what is already a heavy-weight application is probably going to make people's devices go brrrrr all the time. Not only that, but I would argue that for instant communication this stack might not be the best idea in terms of performance in first place.
  - Besides, the way IPFS has been (and still keeps) changing their dozens of libraries doesn't make development particularly smooth either. OrbitDB is always behind the latest IPFS version due to all these changes that are being introduced. Hence unless you're planning to allocate developer time on these two things as well, my guess is that you probably won't have too much fun with your back-end.
  - The integration with Tor is another thing that will likely be a time drain for developers, as other people here already pointed out, and that will lead to even more performance issues down the line.
- All of these things are true and it's clear you know the problem space well! We avoid the primary "go brrrrr" performance issue with IPFS by using small private IPFS networks and never touching the noisy, CPU-intensive global network.

- I think far more interesting these days would be projects like Veilid, Hyphanet's Locutus and ultimately Nostr -- even though not truly P2P in that sense -- which already happens to have a first try going with nostrchat.io. If P2P is something that is truly desired, I feel like projects like Briar (https://briarproject.org/how-it-works/) have solved this with Bramble (https://code.briarproject.org/briar/briar-spec/blob/master/p...) more eloquently than it could be done on top of IPFS.

- The hard part about making a new P2P protocol is that first you have to invent the internet.

- Isn't orbitdb mostly abandoned now by the core team? I looked into it a few months ago and read that it's in a maintenance state.
  - OrbitDB is not well-funded, but there's fresh work happening recently by some dedicated volunteers

- ## 💡 [Peer-to-peer social networking with Rotonde and Beaker | Hacker News_201710](https://news.ycombinator.com/item?id=15463721)
  
- Hypercore has realtime sync, but is limited to log structured data. Dat can do diffs on data, but is meant for large datasets, not realtime changes. This sounds like it would be difficult (or not scalable) to build something like a Wiki, features in social networks, Trello, or other apps (i.e., anything with shared mutable state). How would you do this?
- The reason I ask is that me, Mafintosh, Juan at IPFS, Dominic with Scuttlebutt, Feross at WebTorrent, Substack, and others all met back in 2014 for our different P2P projects. 
  - All of us had slightly different approaches. 
  - Juan and others seemed mostly interested in hash addressing, which I think is great but doesn't solve the end problem of data sync. 
  - Seems like Dat deals with that fairly well, but not for highly mutable data (versus large scientific files). 
  - Meanwhile we ( https://github.com/amark/gun ) tackled that problem first, because it seems like CRDTs are the most relevant for killing traditional centralized Facebook/Twitter/Reddit/gDocs like apps, and hashing is more applicable for killing centralized YouTube/imgur like apps. 
  - Both are necessary, but it certainly seems harder/easier based on which underlying P2P tools you use.
- 👉🏻 **The real-time syncing immutable, append-only log that hypercore provides can also be accessed randomly, allowing for lots of cool parallel/distributed log processing architectures (Kappa architecture)**, similar to Kafka (which is also based on immutable, append-only logs). 
  - We have just focused on syncing a filesystem at first because we had a strong use case there, but you could totally build a CRDT on top of an append only log.

- Is dat more-or-less in the same domain as IPFS?
  - at least strongly related domains, yes.
- They are both BitTorrent variants. **I liked Dat's design a little better, and it's more focused on mutable data streams which is better for Web content**. 
  - IPFS is good though and may end up getting supported in Beaker again at some point. 
  - Dat's the protocol we chose to start with.

- How is Dat different than IPFS?
- Dat keeps a secure version log of changes to a dataset over time which allows Dat to act as a version control tool. 
  - The type of Merkle tree used by Dat lets peers compare which pieces of a specific version of a dataset they each have and efficiently exchange the deltas to complete a full sync. 
  - It is not possible to synchronize or version a dataset in this way in IPFS without implementing such functionality yourself, as **IPFS provides a CDN and/or filesystem interface but not a synchronization mechanism**
- Dat has also prioritized efficiency and speed for the most basic use cases, especially when sharing large datasets. 
  - **Dat does not make a duplicate of the data on the filesystem, unlike IPFS in which storage is duplicated upon import**. 
  - Dat's pieces can also be easily decoupled for implementing lower-level object stores. See hypercore and hyperdb for more information.
- In order for IPFS to provide guarantees about interoperability, **IPFS applications must use only the IPFS network stack**. 
  - In contrast, Dat is only an application protocol and is agnostic to which network protocols (transports and naming systems) are used.

- it appears to me that IPFS really pulls in a lot of stuff about the network layer, because it's trying to be, well, an Interplanetary (distributed) File System.
- DAT is fundamentally a portable, self-contained, data repository. Replicating DAT archives across a broad network and whatnot is definitely a problem that needs to be solved, but IMO that should be solved at a different layer, without rolling in all sorts of complecting concerns such as network ports, routing, and payments for storage and whatnot.
- Yes, agreed. Of course overlap among projects is inevitable and it would be nice if there was more effort to coordinate and collaborate as this would allow for potential dev efficiencies (not guaranteed though). In this case, DAT is a practical and pragmatic approach where IPFS is more hinged in the crypto blockchain token space which can be a turn-off and add unnecessary baggage.
- Ya, we've thought about that. Dat's storage is pretty flexible and we have a content-addressed storage library. A lot of our users do not want or need to storage data in IPFS though so it adds unnecessary complexity to do that by default.
  - Someone could built a storage that uses IPFS, similar to our dat-http storage.

- ## To be clear: IPFS itself won't work because it is ridiculous, but the promise of P2P addressable databases will materialize and will be so easy and performant that even Fiatjaf will use it._202302
- https://twitter.com/ArNazeh/status/1627299193533390850
  - more people realizing the problems with IPFS and they are finding each other.

- I'm curious what aspect you think doesn't work. Certainly can't treat it as a magical db in the sky that does things for free, but if a significant number of people care about a piece of data, the protocols work really well for making that data available.
- I can't even access my own data from a IPFS machine running in a computer in the same room with the IPFS daemon running at 80% of the CPU
- In the meantime Hyperswarm hole-punches with a single line of code and zero config. It shouldn't be that hard.
- Addressing every god damn block of the data structure separately as if you don't know they all belong to the same thing and should colocate, is a sign of systemic silliness and over-abstraction.
  - Content-addressed storage is fundamentally very simple. Put in data, get hash. Put in hash, get data.
- We are converging here, I am hell-bent on using blake3 and bao for files/values of the database entry too, but I don't see the point of making 1000s of DHT queries for 1000s of files that all belong to the same author, you should assume that data will colocate at same peers.
  - IMO, I wouldn't view it as needing to be one or the other, because there are some valid reasons to have the chunks distributed, but to ensure you can stream the chunks of one logical record without requiring a bunch of connections when the/a peer you are connected to has it all.
- So the question is, why the hell announce on blocks instead of files, since no one can use a shard of a file anyway. The answer as I imagine is deduplication and imagined benefits for cdns. Clearly that was a bad tradeoff and people are moving away from it now, luckily

- Even Iroh folks gave up on it [A New Direction for Iroh_202302](https://n0.computer/blog/a-new-direction-for-iroh/)
  - It is an infinite pile of bad design decisions, over-abstraction, and ridiculous choices.
  - I have yet to @#@!% manage to establish a connection between two home devices with it, something I can do with one line in Hyperswarm.
- Don't get me wrong, I'm definitely interested in other similar systems. I would love to see a doc on the Hyper* stuff that provided a 1:1 mapping of IPFS features/APIs. If they provided 1:1 parity that's just better, they certainly haven't communicated that effectively.
  - Not only they can do the same shit, they are 100x easier to learn, zero config, works everytime, just like magic. Most IPFS idiocy is in discovering peers for CIDs individually instead of @#%!#% finding peer for the whole damn data structure.
- I am aware of their goal: filecoin, will never fucking work.
  - DHTs can be good alternative to DNS.
  - DHTs can NOT be a performant alternative to the cloud.

- Do you say that based on what? It would probably require some breakthrough discovery in computing that we can't even imagine
  - 1- Hyperswarm is already working like a charm, and can only get better with more caching, TTL, and tolerance to occasional churned data (max ~10 minutes).
  - 2- Agent-based addressing (max one topic per identity) makes the problem _much_ more manageable.
- Hyperswarm's Rust efforts are individual and it is not my only bet, more likely, Iroh from @n0computer folks will become as good as Hyperswarm as it abandons IPFS compatibility.
- From what I read they still want to make each chunk of bytes content-addressable, they just think they can do better than 10 years of dedicated IPFS development.
  - The biggest harm IPFS has brought to the world was to say something (p2p content-addressable global filesystem) is not only possible but already done and working -- and then waste the time and resources of anyone who is convinced enough to try to make it work for some use case.
- We do plan to content address all data within the system, and that creates some very real scaling constraints. That will naturally rule out use cases, like, uh, replacing the Internet. But doing fewer things well will hopefully add up to an improvement.

- ## After researching decentralized systems for the last months, I’m sure IPFS was the chosen one protocol, destroyed by implementation by committee. libp2p fuels my nightmares._202303
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

- ## 🆚️ [Just today I was looking into IPFS vs DAT_201906](https://news.ycombinator.com/item?id=20162171)
- I was looking into IPFS vs DAT, does anybody have any insights about the similarities/differences other than the ones listed here
  - From far away, DAT looks smaller and better documented (perhaps less ambitious, too?) Apparently the best IPFS overview is the 2015 paper which looks pretty daunting and does not seem to cover any practical considerations.
- I consider dat:// to be the better protocol, in part because of what you mentioned. 
  - 👉🏻 Other advantages are the lack of duplicating data on disk (IPFS makes a copy of all data it shares) as well as having a versioned history of all changes. That way app owners can't publish malicious versions while preventing people from using the non-malicious ones.
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

- ## [A Hypercore P2P innovation could bring more privacy to IPFS | Hacker News_202201](https://news.ycombinator.com/item?id=30072543)
- Hypercore (Dat) doesn't use content hashes, it uses ed25519 public keys (which work more like IPNS—the data they refer to can be changed). 
  - The discovery hash is a hash of the public key, which isn't sent to the peer as part of the request, it's looked up on the data provider's side using the discovery hash. 
  - If the provider doesn't already know the public key then it can't negotiate a successful connection since all subsequent messages are supposed to be encrypted with that key.
- If the public key (or IPFS content ID) were sent to the peer as part of the request then one could learn the content IDs for "interesting" discovery hashes simply by pretending to have the content, announcing the discovery hash to the network, and waiting for peers to show up and request the data by its content ID. At that point you could request the full content from other peers using the content ID.
- One could perhaps employ the Hypercore/Dat protocol for IPFS using the content ID for encryption instead of a public key, but it would be critical to avoid revealing the content ID itself as part of the request. Only the discovery hash can be sent to the peer. It might be safer to negotiate a session key with something like SRP, with the content ID as the "password".

- Hypercore/DAT is a really nice bit of tech for anyone who hasn't seen it. It's the basis for Beaker Browser. Or at least an older version is.

- I implemented a slightly different method for my prototype multimedia chat application (text/images/audio/video) over IPFS. I used an envelope format for permissioned encrypted content

- ## ⚖️ [Hypercore protocol: a distributed (P2P) append-only log | Hacker News_202012](https://news.ycombinator.com/item?id=25407193)
- The hyper* world seems to be very fragmented right now. 
  - There is the dat project, which started 2013 and shares files between computers p2p. 
  - In may 2020 the dat protocol was renamed to the hypercore protocol and dat "will continue as the collective of teams and projects that have evolved from the original Dat CLI project.". 
  - The tech looks pretty cool, but the vast amount of different projects makes it difficult to grasp. 

- Quick question: it's a distributed log, how do you establish consensus to keep its entries ordered? If it's not ordered, then it's a set, not a log. Still cool, but not as impressive.
  - Only one person using one device is allowed to add to the log. Each entry contains the hash of the entry before it (including that entry's field where it contains the previous hash, etc.). If you add entries that have a conflicting ordering, you're assumed to be a bad actor and get blocked by the network.
  - If you want to have multiple devices or multiple people editing the same data, you need to give them all a separate log and use some kind of CRDT system to combine them
- So, there's no consensus because writes are coming from a single process. I must say, I'm a little bit disappointed : that's not the world-changing algorithm I was hoping for.
  - They're working on it, with a rather elegant solution: https://www.datprotocol.com/deps/0008-multiwriter/

- It's pretty nice to see that there are now several P2P techs.
  - This one seems pretty good, but unless you have a single client and unless the protocol is defined to do a single thing and do it well, I can't see it thrive.
  - For example bittorrent is a good tech because it only does one thing and users can understand it. Same for IPFS. Softwares like limewire or kazaa thrived because they were simple enough to use. Same goes for protocols.
- In my view, decentralization requires:
  * a client that runs on user's hardware
  * a p2p database and filesystem, with this kind of append-only log and verification, that runs on the client
  * server can still accelerate access access time
- The only problem is being able to attract users and compete with popular platforms. If such a protocol+software can attract users who want a "privacy-aware" alternative to platforms like facebook, I could see it work.

- A related thing I'd love to see take off is companies offering log-based interactions instead of HTTP APIs only. Some apps are such a poor fit for HTTP that you end up with a convoluted mess of web-hooks as soon as some elements of async appear. Obviously, these web-hook contraptions are always home-grown and offer nothing near what you get with a proper log system.

- Has anyone used this enough to share perf characteristics? This is coming up twice today, but I’m interested in using a P2P append only log as a total order broadcast for use with (my day job) Fluid Framework. Decentralizing the broadcast would make Fluid more aligned with the Ink and Switch essays about offline first.

- ## We're happy to announce that NLnet will be funding Hyper Hyper Space development in the near future
- https://twitter.com/The_lolness/status/1496088630808485890
- any relation to the hypercore protocol?
  - Nope, we're unrelated

- ## do you have any hello-world type example of hypercore running in the browser?
- https://discord.com/channels/709519409932140575/709519410557222964/1068520819204051084
  - If it can run directly in the browser without the need of a proxy server, it would be even better
- the problem is the DHT won't run in the browser, so it isn't useful without the proxy to the DHT server
- You have to setup a public dht-relay on a server, and/or you could let users run their own local dht-relay and let them configure host and port on your web app
  - You could easily do this on any React project
  - [browser-dht.js](https://gist.github.com/LuKks/c144fa0f72ebfd303515d0ce7dadb477)

- ## blue sky is doing a lot of stuff and was born from jack/twitter who is also making "web5". theres motive there. 
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
