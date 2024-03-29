---
title: pattern-local-first-spec-compatibility
tags: [compatibility, interoperability, local-first, protocol, spec]
created: 2022-11-14T20:08:46.332Z
modified: 2023-09-13T20:30:20.011Z
---

# pattern-local-first-spec-compatibility

# guide

- protocols
  - [decentralized social ecosystem structured by protocols](https://gitlab.com/bluesky-community1/decentralized-ecosystem/-/tree/master)
  - [The Software Package Data Exchange® (SPDX®)](https://spdx.dev/)
# usecase
- pwa
  - https://github.com/hemanth/awesome-pwa
  - [Appscope](https://appsco.pe/)
  - [zero data app](https://0data.app/)

## [zero data app](https://0data.app/)

- Protocols
  - [ActivityPub](https://github.com/BasixKOR/awesome-activitypub)
  - [remoteStorage](https://github.com/remotestorage/remotestorage.js)
  - [Solid](https://solidproject.org/about)
  - [fission](https://fission.codes/)
  - [m-ld](https://m-ld.org/)
  - [nostr(Notes and Other Stuff Transmitted by Relays): a truly censorship-resistant alternative to Twitter](https://github.com/nostr-protocol/nostr)
# protocol

## ActivityPub

- https://github.com/BasixKOR/awesome-activitypub
  - ActivityPub is W3C standard, decentralized social networking protocol.

- The ActivityPub protocol is a decentralized social networking protocol based upon the ActivityStreams 2.0 data format.

## Block Protocol

- https://github.com/blockprotocol/blockprotocol
  - https://blockprotocol.org/
  - The Block Protocol is an open standard for building and using data-driven blocks.
  - HASH is an example embedding application that uses the Block Protocol to enable users to insert arbitrary blocks from the Hub at runtime. 
- [Leonardo Losoviz: Would WordPress be better off by Joining the Block Protocol?_202205](https://masterwp.com/would-wordpress-be-better-off-by-joining-the-block-protocol/)
  - I can provide my answer: No, it will not be better off. Adopting the Block Protocol is not worth it
  - Treating the Block Protocol as an “idea”, not an “implementation”
  - I don't think we lack ways of passing structured data to components. We lack standardized interpretation that works for everyone's use cases.
    - If your use case is "building a rich-text editor", you might even be able to build something meaningful around this.
    - But everything that goes further away from the default HTML use case will need opinionated UI/UX.
    - Take Gutenberg as an example...
    - It has a more limited scope than your proposal, but already hitting major BC/FC issues even though it is not feature-complete yet.
    - As an example, how do you deal with intra-block(在...内) dependencies and their conflicts?
    - The web as we know it was always block-driven (divs vs spans).
    - However, it only provides (some) standardization for very low-level use cases (paragraphs, lists, ...)
    - For any higher-level use cases (gallery, slider), all prior standardization efforts have failed ...for a reason.
- hash /636Star/MIT+Elastic+AGPL/202211/ts/rust
  - https://github.com/hashintel/hash
  - https://hash.dev/
  - Data management, integration and modeling with blocks
  - The Block Protocol is an open-source standard and registry for sharing interactive blocks connected to structured data.
  - You can build your own blocks, embed them in a website, or allow your users to embed blocks directly within your application.
  - HASH is our forthcoming open-source, all-in-one workspace platform built around structured data and interactive blocks.

- https://github.com/githubnext/blocks
  - https://github.com/githubnext/blocks-examples
  - With Blocks, you can extend GitHub's interface in some pretty powerful ways! 
  - It could be as simple as a custom renderer for files or folders in your repository, and it can be as flexible as a full interface for editing content.

## solid-specification 

- solid-specification /371Star/MIT/202211/md
  - https://github.com/solid/specification
  - https://solidproject.org/about
  - Solid is a specification that lets people store their data securely in decentralized data stores called Pods. 
    - Pods are like secure personal web servers for your data.
    - To store and access data in your Pod, applications use standard, open, and interoperable data formats and protocols.
  - Solid Technical Reports (TR) of the W3C Solid Community Group (CG) to meet the needs of the Solid Project.
  - [Solid Protocol Spec Draft](https://solidproject.org/TR/protocol)
  - Solid adds to existing Web standards to realise a space where individuals can maintain their autonomy, control their data and privacy, and choose applications and services to fulfil their needs.

## fission

- https://fission.codes/
  - Building protocols for the future of the Internet
  - Protocol Labs pioneered decentralized storage with the introduction of IPFS. 
  - Protocol Labs is an open-source R&D lab. We build protocols, tools, and services to radically improve the internet

## Matrix protocol 

- [Matrix.org](https://www.matrix.org/)

- https://github.com/matrix-org/matrix-spec
  - https://spec.matrix.org/latest/

- Matrix defines a set of open APIs for decentralised communication, suitable for securely publishing, persisting and subscribing to data over a global open federation of servers with no single point of control
- Uses include Instant Messaging (IM), Voice over IP (VoIP) signalling, Internet of Things (IoT) communication, and bridging together existing communication silos - providing the basis of a new open real-time communication ecosystem.

## m-ld

- https://m-ld.org/
  - With m-ld, information is available where it's used—on mobiles, in browsers, in microservices, anywhere—and it stays up-to-date, automatically. It's live and sharable.
  - At the heart of m-ld is a decentralised protocol for distributing live information among clones. 
  - Using m-ld, every instance of an app has read-write access to the shared information via its local clone, with zero network latency. 
    - Changes to the information are propagated to all other app instances, so they are all eventually consistent.

- https://github.com/m-ld/m-ld-spec
  - m-ld is a decentralised live information sharing component with a JSON-based API.
- https://github.com/m-ld/m-ld-js
  - the code of the Javascript engine for m-ld, for node.js, modern browsers and other Javascript platforms

- https://github.com/m-ld/m-ld-todomvc-vanillajs /js
  - Collaborative TodoMVC with Modern (ES6+), Vanilla JavaScript and m-ld
  - This is a vanilla Javascript implementation of TodoMVC, with collaboration enabled using m-ld

## nostr(Notes and Other Stuff Transmitted by Relays)

- https://github.com/nostr-protocol/nostr
  - The simplest open protocol that is able to create a censorship-resistant global "social" network once and for all.
  - https://github.com/aljazceru/awesome-nostr

- The problem with Twitter
  - bans
  - ads
  - spams
- The problem with Mastodon and similar programs
  - User identities are attached to domain names controlled by third-parties
  - Server owners can ban you
  - For the specific example of video sharing, ActivityPub enthusiasts realized it would be completely impossible to transmit video from server to server the way text notes are, so they decided to keep the video hosted only from the single instance where it was posted to, which is similar to the Nostr approach.

- [nostr – a censorship-resistant alternative to Twitter_202201](https://news.ycombinator.com/item?id=29749061)
- In this case the content and accounts are independent of the node. 
  - In Mastodon as far as I can see both the account and the content are instance dependent and will disappear if the instance disappears.

- Nostr解析
- https://twitter.com/jianshubiji/status/1620729604167340032
- 1⃣Nostr是什么？
Nostr 不是区块链，也不是App， 是一个用于服务器和客户端通信的协议，应用程序可以基于 Nostr 构建。Nostr不依赖中央服务器，因此具有弹性；基于加密密钥，因此防篡改。
- 2⃣Nostr工作原理？
1. Nostr主要有两个组件：客户端，App等和 中继，类似简易服务器。任何人都可以运行中继器
2. 用户由公钥标识身份，发布内容时由私钥签名，客户端会验证签名并发送到多个中继器
3. 中继器只存储与转发内容，且中继器仅直接与用户通信
4. 查看内容时，向中继器发送请求以获得信息
- 3⃣Nostr解决什么问题？
1. 防止用户被禁止及服务器被关闭。虽然某个中继器可以阻止某个用户的发布内容和查询内容的请求，但该用户可以通过其它中继器完成操作，因此用户体验没影响。
2. 抗审查
3. 减少垃圾邮件
4. 降低数据存储成本

## Farcaster

- https://github.com/farcasterxyz/protocol
  - Farcaster is a community-created protocol for building decentralized social applications.

## Noosphere

- https://github.com/subconsciousnetwork/noosphere /rust
  - Noosphere, like its namesake, is a worldwide medium for thinking together. We like to think of it as a protocol for thought.
  - Noosphere is the foundational protocol that the Subconscious app builds upon to enable an open-ended, permissionless multiplayer experience.
