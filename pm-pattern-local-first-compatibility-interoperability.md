---
title: pm-pattern-local-first-compatibility-interoperability
tags: [compatibility, interoperability, local-first]
created: 2022-11-14T20:08:46.332Z
modified: 2022-11-14T20:12:25.671Z
---

# pm-pattern-local-first-compatibility-interoperability

# guide

- protocols
  - [decentralized social ecosystem structured by protocols](https://gitlab.com/bluesky-community1/decentralized-ecosystem/-/tree/master)
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
