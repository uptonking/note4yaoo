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
# discuss-collab
- ## 

- ## 
# discuss-ipfs-ssb
- ## 

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
