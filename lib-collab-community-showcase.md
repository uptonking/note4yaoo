---
title: lib-collab-community-showcase
tags: [community, crdt, showcase]
created: 2023-05-21T14:54:56.318Z
modified: 2023-05-21T15:46:35.896Z
---

# lib-collab-community-showcase

# guide

# discuss
- ## 

- ## 

- ## 

- ## Stellar example of the difficulty of maintaining global invariants with CRDTs. 
- https://twitter.com/tomlarkworthy/status/1660217410517979137
  - It's probably possible via a clever change of representation but if you have the option of a server authority, take it and save yourself the PhD work and keep the intuitive representation.
- Yeah, 100% I do think CRDTs are in a hype cycle and the enthusiasts will eventually have to reconsider that they are not a good choice for vanilla app development. They have unique strengths but huge drawbacks too so the problem has be matched for CRDTs to be the answer

- ## Announcing Reflect✨ – high-performance sync for the multiplayer web
- https://twitter.com/aboodman/status/1658251815929126913
  - This is the next step for @replicache and something we’ve been working on and dreaming of for some time.

- Some background: Our existing product, Replicache, is BYOB (bring your own backend).
  - Customers like this as it provides tons of flexibility and enables them to add sync to their existing apps. 
  - We will continue to support and improve Replicache (it’s an integral part of Reflect).
- But we did get a few bits of consistent feedback over the past year that led us to build Reflect:
  - First, people often ask us how to build experiences “like Figma”. With high-performance drag and drop interactivity and cursors flying around.
  - Second, many people loved Replicache and just wanted a complete stack from us. They didn’t want to run, scale, or monitor servers.
  - So we set out to do that!

- features

- ### **1/ Performance.** 
  - Reflect syncs at 60 FPS (120 FPS with device support).
  - If your multiplayer tech doesn’t deliver this, the UI dev will have to paper it over using interpolation.
  - And your app has much more than mouse motion: Users can move things, resize things, rotate things, group things. All these interactions would have to be interpolated.
  - And every single time you add a new interaction, you’ll have to interpolate that too.

- ### **2/ Built-in Persistence.**
  - Reflect isn't just ephemeral(短暂的；瞬息的) sync. Changes are continuously and automatically saved on our cloud service too.
  - You don’t need to wire anything together, copy data from ephemeral to persistent storage, or worry about how often to save.
  - Just write changes as they happen (yes, every mouse movement) and they are automatically saved and replicated to peers.

- ### **3/ Server Authority**
  - 💡 People are often surprised to learn that **Reflect isn’t a CRDT**. 
  - Although lovely computer science, CRDTs have a number of disadvantages for web apps:
    - There’s no good way to validate or enforce data constraints. In pithy terms: CRDTs converge, but to what??
    - For the same reason, fine-grained auth is difficult. It would be hard to implement inline comments that only the author can edit using a CRDT for example.
    - They turn every problem into a distributed systems problem. In the development of real world apps you often find places where it’s convenient to run code on a central server. Common examples are wanting to initialize data once, migrating data, or choosing a leader.
  - 👉🏻 Instead of CRDTs, Reflect uses a more flexible technique from the video game world known as **Server Reconciliation**
  - [Client-Side Prediction and Server Reconciliation - Gabriel Gambetta](https://www.gabrielgambetta.com/client-side-prediction-server-reconciliation.html)
  - This is a lot harder way to build sync, but it solves the above problems:
    - Validation is built-right in. It’s impossible for clients to make invalid changes.
    - Fine-grained auth comes for free. Write auth in plain JS, consulting any backend systems you want.
    - You get a server! You can run server-only code to coordinate clients whenever you want to.
  - At the same time, it's entirely **possible to run a CRDT inside Reflect**, and we even recommend this for text editing — where well developed libraries exist and do an amazing job.

- ### *4/ On-”Prem”**
  - Finally, and maybe most important, we offer the option to run Reflect within your own Cloudflare account.
  - Although customers do not usually want to build, scale, and maintain multiplayer servers, larger customers do often need control of the code and data.
  - We have carefully designed Reflect to enable this. You give us limited permissions to your Cloudflare account and we run Reflect for you.
  - You even get a source license, so even if we disappear, you can still run Reflect forever and gracefully migrate away.

- ### summing up:
  - We’re building multiplayer infrastructure for the next generation of great multiplayer apps. 
  - Everything you need to forget about sync and focus on your product.

- 🤔 How is it different from FluidFramework ?
  - Reflect is **server authoritative**, enabling easy validation and fine-grained authorization
  - Reflect has a **single general data model** (a map of key-value pairs), rather than specialized data structures for different problems.
  - Reflect has (will have) first-class support for running on-"prem".
  - Reflect provides 60 FPS sync so you don't need to interpolate

- Will you support non web-based clients?
  - We will support JS/non-web like React Native and Electron. But Reflect will be JS-first for the forseeable future.
