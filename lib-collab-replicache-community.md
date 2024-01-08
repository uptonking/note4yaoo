---
title: lib-collab-replicache-community
tags: [collaboration, community, crdt, replicache]
created: 2024-01-07T05:08:43.395Z
modified: 2024-01-07T05:09:14.413Z
---

# lib-collab-replicache-community

# guide

# dev

# discuss-stars

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## Replicache is closer to a db than you’d think. 
- https://twitter.com/aboodman/status/1743829055827546152
  - We built on what we learned from https://github.com/attic-labs/noms and built Replicache on an immutable b tree. 
  - So technically it’s a fast key value store, which is the basis for many popular dbs.
  - This is also why Replicache is so fast while being backed by idb. 
  - We don’t use idb as a kv store itself. It only stores pages of our custom b tree.

- SQLite is unfortunately too slow in the browser to be used as a reactive database.

- ## 🕹️✨ @hello_reflect is the only multiplayer system that supports database-style interactive transactions.
- https://twitter.com/aboodman/status/1732484354637709507
  - People sometimes ask if they really need that though. Aren't CRDTs or json-patch enough?
  - With a CRDT like Yjs, you could have each row be a map entry. The same approach could work with JSON-patch bases systems.
  - When we were playing with early versions of this demo, I wanted to see a version where you could pick multiple cells (so that you could "draw" songs. But this doesn't work with the data model above, you'd need a different schema where each cell can be selected
  - Note the problem here: With a map CRDT we need an entirely different schema if we change our business logic even slightly. The schema that works for selecting only one cell per row does not work for selecting multiple cells. And vice versa!
- This isn't a problem in Reflect. We start out with a nice flexible schema, a map of enabled cells.
  - We can even choose at runtime with a flag.
  - All easy to implement on this basic schema in Reflect using transactions, but difficult or impossible with other systems.
- So while you can do some things without transactions, when your project gets even a little interesting, you invariably need custom business logic. Where does that logic go? It can't go on the client, for the same reasons we can never rely solely on client-side validation.
  - But it also can't go on the client because there are multiple clients running. A rule like "only one cell in this row can be selected" can't be implemented client-side – two clients could decide they got the only slot at the same time.
  - 💡 Reflect's Transactional Conflict Resolution gives you an elegant way to implement any kind of custom business logic. Your mutators run twice – once on the client, optimistically, for responsiveness, but then again on the server to compute the authoritative result.

- In an op-based CRDT, you can only send the discrete set of ops that are built into that CRDT. In TCR, you can implement any op you want using JavaScript. The core idea of linearization on an authoritative server is a pretty good general purpose sync system.
  - The reason this generalization isn't possible in general in op-based CRDTs is that the system must converge.
  - This implies that the ops on all clients must be (a) pure and (b) identical. But how could this be guaranteed in common programming environments?
  - It can be done in specialized systems. @tanglesync is a very cool exploration of this idea using a rewindable wasm sandbox.
  - @tantaman has also explored this here: https://vlcn.io/blog/crdt-substrate
  - Another challenge with doing this as a pure CRDT is of course finalization. You can never know when the effect of an op is final because some earlier op can always be received.
- I don't really see it as that similar to an op-based CRDT but I guess that's dependent on your point of reference! Other people say "isn't this similar to OT?". And I guess all of these are ideas are not that far apart in the big picture. But the details are why we give things different names
  - The ability to provide your own mutators is a massive different in usability, making it feel like a completely different thing from a crdt from a dx pov.

- ## We are studying @replicache 's awesome blog post at @taktile_org 's internal reading group. We built a somewhat similar linearized serverside reconciliation algorithm. 
- https://twitter.com/tomlarkworthy/status/1727986810238697837
  - Main diff is we send JSON-merge-PATCHes not mutator calls.
  - JSON-merge-patch is the RESTful dual of operational based sync. 
  - Main drawback is it does not work with arrays or nulls and its not as expressive as arbitrary functions, but it has some nice composability when you want a change log or combine writes

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

- > One plus point compared to CRDTs is that you get to decide how you want to deal with conflicts yourself, with simple, sequential code. I'm not up to date with the latest in CRDT-land but I believe it can be complicated to add application specific conflict resolution if the built-in rules don't fit your needs.
  - I agree wholeheartedly — we took the same approach for PowerSync with a server reconciliation architecture over CRDTs, which is also mentioned elsewhere in the comments here. For applications that have a central server, I think the simplicity of this kind of architecture is very appealing.
- We had similar conclusions around the implementation of PowerSync (sync engine enabling offline-first applications). Instead of CRDTs we went with the architecture of a central server authority and a form of server reconciliation for consistency.

- ## 🚀 Announcing Reflect – A new way to build multiplayer apps like Figma or Notion._202310
- https://twitter.com/aboodman/status/1714682920495919520
  - Rather than CRDTs, Reflect syncs the way video games do.
  - Reflect isn't open source. We're considering that, but in the meantime a source license and on-prem is available.
  - [Ready Player Two – Bringing Game-Style State Synchronization to the Web_202310](https://rocicorp.dev/blog/ready-player-two)
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

- ### **4/ On-”Prem”**
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
