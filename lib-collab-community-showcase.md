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

- ## 🚀👥 [Reflect – Multiplayer web app framework with game-style synchronization | Hacker News_202310](https://news.ycombinator.com/item?id=37931373)
- Reflect adds a fully managed, incredibly fast sync server.
  - One plus point compared to CRDTs is that you get to decide how you want to deal with conflicts yourself, with simple, sequential code. I'm not up to date with the latest in CRDT-land but I believe it can be complicated to add application specific conflict resolution if the built-in rules don't fit your needs.
- I agree wholeheartedly — we took the same approach for PowerSync with a server reconciliation architecture over CRDTs, which is also mentioned elsewhere in the comments here. For applications that have a central server, I think the simplicity of this kind of architecture is very appealing.

- Congrats! I've been watching this space for a while, having built a couple multiplayer sync systems in the past in private codebases, including a "redux-pubsub" library with rebasing and server canonicity that is (IIUC?) TCR-like. There's a lot to like about this model, and I find the linked article quite clear - thank you for writing and releasing this!
  - Do you have a recommendation for use-cases that involve substantial shared text editing in a TCR system? I'd usually default to Yjs and Tiptap/Prosemirror here (and am watching Automerge Prosemirror with interest). The best idea I've come up with is running two data stores in parallel: a CRDT doc that is a flat key/value identifying a set of text docs keyed by UUID, and a TCR doc representing the data, which occasionally mentions CRDT text UUIDs.
- What does this mean for Replicache development, is the client-side codebase mostly shared and can expect continued updates, or more likely to replace the primary focus for you?
  - The clients are almost entirely shared. We will continue to develop Replicache.
- What is the maximum number of users that can be concurrently in a room?
  - There's no max enforced. Right now, it will fall apart pretty quick around 25-50, depending on how much work is going on. For the GA, we plan to implement a scheme that will allow the room to support up to ~100 concurrent active users (actually doing things) and thousands just watching.

- 🆚️ Curious what your thoughts are on ElectricSQL?
  - It seems really interesting. The key thing to understand is that there are deep architectural choices made in each of these systems that really influence what you can do. There is "mechanical sympathy" with certain kinds of applications.
  - ElectricSQL is a distributed database. It's not going to run anywhere near 60fps with tons of users, because it's not running in memory on the server like Reflect/PartyKit/Liveblocks do. OTOH it will allow you to filter/query interact with much more data at the same time than Reflect/PartyKit/Liveblocks do – Reflect has a limit currently of 50MB per room and it's not practical to have dozens of rooms open at one time to get around this.
  - Systems in the Reflect room/document based model are well suited for applications where you primarily interact with one "document" at a time and you want that to be as realtime as possible. Figma is the canonical example. You want the entire document to move together at 60 FPS, completely fluidly. It's not going to be possible to do this well in the ElectricSQL model IMO. Spreadsheets, presentations and documents are other examples. Systems in the ElectricSQL model are more suited for applications where you are interacting with lots of documents at the same time. Think CRMs, bug trackers, etc.
  - Both types of systems are going to track toward the other to support the needs of real applications.

- 🆚️ Is this in a similar vein to https://partykit.io/?
  - Yes they are in the same space. The key difference is in how opinionated each is.
  - PartyKit is extremely unopinionated. It's essentially lightweight javascript server, that launches fast and autoscales (I don't say this as as a bad thing, it's a useful primitive). Most people seem to run yjs in PartyKit, but you can also run automerge or even Replicache – my company's other project.
  - Reflect is entirely focused on providing the best possible multiplayer experience. We make a lot of choices up and down the stack to tightly integrate everything so that multiplayer just works and you can focus on building your app.

- 
- 
- 

- ## 🚀 Announcing Reflect – A new way to build multiplayer apps like Figma or Notion._202310
- https://twitter.com/aboodman/status/1714682920495919520
  - Rather than CRDTs, Reflect syncs the way video games do.
  - Reflect isn't open source. We're considering that, but in the meantime a source license and on-prem is available.
  - [Ready Player Two – Bringing Game-Style State Synchronization to the Web](https://rocicorp.dev/blog/ready-player-two)
- Super interesting! One drawback I see is that syncing stops working when the server is down. The extra authority on the server makes all clients dependent. I understood CRDTs enabled p2p syncing, which allows collaboration on a local network.
  - Yes, that's true. Although this approach can continue to work *locally* offline and resync when server comes back, it can't sync just within the local network. That's a tradeoff that matters in some cases, but we find that it is a relatively rare need.
- Looks cool! Is this a framework I can run myself for free on my own infra?
  - No, it's a managed service. We do have an on-prem option and a generous free tier.

- Looks amazing! Client-side prediction technique along with the linearization of transactions by arrival time on the server is exactly how the sync engine of Pitch works.
  - We also greatly benefited from the immutable data structures that you get for free in Clojure(Script) to rollback to the canonical snapshot in a performant way. I think you briefly mentioned on HN that you're  using persistent data structures under the hood as well which is cool

- You picked one CRDT that Yjs didn't implement ; ) But don't worry, here's the implementation that's relatively perf-wise and doesn't loose updates
  - Well it depends on how many clients you have right? Each unique instance of Y. Doc is a client ID. That can really add up over time. And I think this suffers the same problem that it's not really an intuitive solution to a counter.

- ## 🚀 Announcing Reflect – high-performance sync for the multiplayer web_202305
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
