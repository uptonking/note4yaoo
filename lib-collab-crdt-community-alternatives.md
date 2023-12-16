---
title: lib-collab-crdt-community-alternatives
tags: [alternatives, collaboration, community, crdt]
created: 2023-12-16T17:36:30.516Z
modified: 2023-12-16T17:36:57.942Z
---

# lib-collab-crdt-community-alternatives

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 🤔 [You don't need a CRDT to build a collaborative experience | Hacker News_202311](https://news.ycombinator.com/item?id=38289327)
- jitl(notion-dev): I agree broadly with the article’s position but I think locks are more harmful than helpful. 
  - Instead just allow LWW overwrites. If users have contention and your sync & presence is fast, they’ll figure it out pretty quick, and at most lose 1-2 keystrokes, or one drag gesture, or one color pick.
  - 💡 Notion is “collaborative” and we don’t use a CRDT for text, it’s all last-write-wins decided by the server. However our LWW texts are individually small - one block/paragraph in size - and adding/moving/removing blocks is intention-preserving if not perfectly convergent.
  - As the article says, the downside for LWW is that “offline” / async collaboration isn’t so great. That’s why we’re working on switching to CRDT for our texts. If you’re interested in bringing CRDTs to a product with a lot of users, consider joining Notion’s Docs team

- Are you considering having a CRDT for each text block individually, or moving to a CRDT for the entire data model for a document? Really curious about the design approach here, especially insofar(在这个范围；到这种程度 ) as there's now an external API that the data models need to service!
  - It’s Complicated (tm), a hybrid of the two. Text content across multiple CRDT enabled blocks may be connected in a single logical CRDT, but the segment visible in any given block is stored in that block object, which maintains our permission system invariants. We’ll still support moving blocks to different pages, so one page may have a few different CRDTs visually interleaved.
  - All the edge cases are very interesting, like what happens if I use backspace to join a block of CRDT B into block of CRDT A.
  - 💡 API consumers are unaffected. Likely we’ll support API updates of text as best-effort `diff-match-patch` of the text on our side applied as CRDT ops.

- So Last-Write-Wins (LWW) basically _is_ a CRDT, but not in the sense that anyone really expects, because they aren't that useful or intention preserving. Especially if the two writes happen in very quick succession / concurrently.
  - LWW becomes useful if you can:
    - a) help humans to see who is doing what on a doc
    - b) reduce the size of the change that is LWW
  - > However our LWW texts are individually small - one block/paragraph in size
  - This is really important, because by reducing the size of the individual element that any single user is updating you can also reduce the chance of conflicts. With a small amount of contextual feedback (like the notion icon next to the block) a lot of the problem cases are just avoided.
  - Clearly locking and updating the entire document would be terrible, but if you can do it on a small enough scope that others can change other elements, it can work really well.

- You can have a LWW CRDT, but not every LWW is a CRDT. LWW CRDTs generally pick a winner based on causal order which is convergent, the C in CRDT, because every peer receiving the same ops in any order would pick the same winner.
  - Picking a winner based on wall clock time order (as suggested in the article, and implemented by Notion) is not convergent; if peers used that algorithm to apply ops I they would not converge to the same state. 
  - Instead you need an authority (your server) to essentially pick an arbitrary order of ops and clients just have to deal with it.

- google docs works not because they somehow figured out how to converge OT edits with as much precision as CRDTs do, but simply because they have a central server which orders edits anyway and don't need true leader-less convergence.
  - In fact, I agree not many things don't need a CRDT. CRDTs help with mathematical rigidity of convergence when you want true peer-2-peer collaboration which works without any central authority.
  - However, most apps anyway work on top of a central authority (example SaaS apps) so there is no real reason to accommodate all the complexity that comes with CRDT. They might get far with a simpler OT based model + central server based ordering.
  - For example even Figma doesn't call its model a 100% pure CRDT. It's a partial, simpler CRDT implemented with an assumption that there's going to be a server that understands ordering.
- 🌰 Yeah. Text based OT is pretty simple to implement, too. It’s about 200 lines of code, plus a simple network protocol. It’s fast and relatively straightforward to code up, and unlike text CRDTs it’s pretty fast by default. I use it as my standard test when trying out a new programming language. It was unexpectedly ugly in go because of go’s lack of enums & unions, and that’s one of the big reasons I never got in to programming Go.
- Just for clarification, while OT for plain-text (linear model) might be simple to implement, OT for typical rich-text editors (like Google Docs) that need to rely on a tree-structured data model is a whole different story
  - I'm actually part of the team that built real-time collaboration for CKEditor 5. As the article says, we use a tree-structured representation for rich-text data and decided (many years ago) to go with OT. My guess always was that GDocs also uses a tree structure as the internal data model or that at least Google Wave did. I think I based this on a comment from a Google employee who summed up their OT implementation as hard to stabilize, even over many years.
  - I know it's possible to kind of represent rich-text data in form of a linear structure. This makes the implementation of the OT much much simpler. But then the editor itself becomes much more limited or you need to combine multiple instances of its model to represent more complex data. E.g., AFAIK Quill (mentioned in the other comment) does not offer stable tables implementation. Something that wasn't that big of a deal for us.
- Google Docs actually uses a flat array representation of the whole document. Tables/lists and other structures are encoded using control-characters in the plain string. This makes index calculations for OT a bit easier.
  - How do I know? I work on Zoho Writer - a google docs alternative and we use the same technique
- have a look at `rich-text` which allows for transforms on metadata in a separate stream from the main content. it’s the same basic algo used for OT on plain text. 
- you can build a rich text editor with simple ot. no tree necessary.
  - I agree. Yes, you can. Quill is the example here.
  - Actually, back in 2015 when we started prototyping CKEditor 5, we started with this approach as well. Our goal from the beginning was to combine real-time editing capabilities with an engine capable of storing and rendering complex rich-text structures (nested tables, complex nested lists, other rich widgets, etc.). We quickly realized that a linear structure is going to be a huge bottleneck. In the end, if you want to represent trees, storing them as a linear structure is counterproductive.
  - So, we went for a tree model. That got many things in the engine an order of magnitude harder (OT being one). But I choose to encapsulate this complexity in the model rather than make it leak to particular plugins.
  - So, yes. You can implement a rich-text editor based on a linear model. But it has its immediate limitations that you need to take into consideration.

- One of the main points of this article is to "just use locks", which glosses over a lot of technical complications about locking elements within a document. How long is the lock held?
  - locking is a hard problem. Especially when you get into the edge cases of clients not disconnecting cleanly.
- For however long the user has a browser focus state on the element seems like a reasonable answer, and submit changes as they are made. However, I don't know how you resolve conflicts of two users simultaneously attempting to acquire a lock.
  - The server must keep track of the locks, and it can only know about the lock being released if the client tells it. E.g by sending a message that the field is not focused any more. The tricky thing is in the "edge" cases, or really the non-perfect cases, which there are plenty of (as I think GP described).
- Having used an app with locks like this (Quip) I can tell you it really sucks to have a lock lease >10s after the last edit. The “lock” should be a UI level concept anyways - clients should broadcast “hey I’m taking field X”; if you have two users submit a write+lock request concurrently you’ll need to pick a winner anyways.

- By exploring that locking and unlocking mechanism, you will find that the logical conclusion in the end, when enough complexity and edge cases get covered/fixed as bugs, that it turns into a crude form of "CRDT" (where it's not actually consistent, but merges within reason for 99% of use cases). It might as well have been CRDT from the get go.

- I don't think you need a pure CRDT either but I think locking and presence is a bit of an oversimplification.
  - LWW is a good place to start, and updating the smallest piece of information possible is the right idea in general but there is a lot more nuance to handling complex applications like a spreadsheet (I'm working on one) and whiteboard apps.
  - Things like reparenting or grouping shapes, or updating elements that aren't at the lowest scale like deleting a row or column in a spreadsheet make locking challenging to implement. Do you lock the entire row while I'm moving it? Do you lock the entire group of shapes?
  - With the exception of text editing, the popular libraries like Yjs don't just give you a perfect CRDT out of the box. You still have to construct your data model in a way that enables small scale updates, and CRDT libraries and literature are the best source of thinking for these problems that I've found.

- 💡 For offline first apps, or for applications where very high degree of control for the content is needed (e.g. legal docs) and realtime collaboration isn't that valuable, there is also the option to use 3-way merge instead.
  - The benefit is that you can even allow the user to resolve conflicts in a satisfactory way.
  - Another benefit is that the document doesn't even have to be derived from the original, it could go through exports and re-imports and it will still be possible to run a 3-way merge as long as a common base version is declared. This can be especially convenient for systems that involve e.g. MS Word.

- Ever-growing state: for CRDTs to work well they need to keep a record of both what exists, and what has been deleted (so that the deletes aren’t accidentally added back in later). This means that CRDT state will continually expand.
  - State-based CRDTs don't need to keep history and don't need causal ordering of messages, but internal bookkeeping grows with the number of replicas. And for large states (like sets and maps), it can be prohibitive to send the state all over the wire for an idempotent merge.
  - That's why in practice, people implement Op-based CRDTs, which makes the trade: in order to send small ops over the wire, we now need causal ordering of messages. To make sure we can sync with replicas long offline, we keep as much history so that they can catch up.
  - There are other variations, such as delta-state based CRDTs that send diffs, and merkle CRDTs, which use merkle data structures to calculate diffs and detect concurrency, which have different growth characteristics.

- We all regularly use Git and it keeps a history of everything. Our disks are huge, and having an immutable record is great for lots of things (providing you can access it).

- > Opaque state: ...you’re generally left with an opaque blob of binary encoded data.
  - Most CRDT libraries take a document-orientated angle. It assumes that you can contain the entire "unit of work", like a document, inside of a CRDT. However, if your data is more relational, it doesn't quite fit. And while there's immutable data in a CRDT, I do wish it was more accessible and queryable. In addition, being a binary blob, it's not exactly composable. I think CRDT libraries should be composable with each other.

- I've seen locks used at the CMSes of large news organizations. It's fine, but they all need a mechanism to kick out an editor who has an idle tab left open. For my own small scale CMS, I just wrapped Google Docs and let them handle all the syncing headaches.

- We took a super simple (IMO) approach to collaborative editing in my current project: 
  - Each block of text has a version number which must be incremented by one by the client at the time of submission. The database provides conflict prevention by uniqueness constraint which bubbles up to the API code. The frontend is informed of conflict, so that the user can be notified and let the human being perform conflict resolution. 
  - Because most concurrent users are working on different blocks, this works great
- How do you handle getting the changes that one client makes onto the other clients? Are you pushing it from the server to the clients with websockets, or waiting for the clients to ask for new info, or waiting for the conflict to happen when someone else tries to make a change, or something else?
  - When the client gets HTTP 409 Conflict, it asks for the current version and presents to the user for manual resolution

- That's not gonna work for real-world projects. Real-world apps often have larger edits than locking individual cells/cards e.g. Move columns or replace large chunks of spreadsheets in Google Sheets, or Ctrl-A to select all and then drag to move. Also, if you consider latency, locking does not work well because client B might do operations before he/she even acknowledges the lock from client A because of latency.

- > Opaque State: You can’t inspect your model represented by the CRDT without using the CRDT library to decode the blob, and you can’t just store the underlying model state because the CRDT needs its change history also. You’re left with an opaque blob of data in your database.
- 💡 As someone who works on a CRDT library with opaque state, I agree that this is a big barrier to adoption. Features like partial loading, per-paragraph permissions, and accept/reject suggestions seem pretty easy to implement if each text char is just a row in your server's DB, but I would have trouble implementing them on top of e.g. Yjs.
  - For text editing, one idea is to separate the CRDT "positions" from the text itself, which you can then store as a map (position -> char) in your own data structures. 
  - I've made a simple (but inefficient) library along these lines and would be interested in ideas for further development.

- 💡 We are addressing the CRDT downsides mentioned in the article at Loro:
  - Ever-growing state. This is no longer an issue. With OT-like CRDTs, you can discard unnecessary historical data at any time. This is theoretically feasible, and we are moving towards this goal. 
  - Complex implementation. The complexity is internal within the package, and it's written in Rust, making it universally applicable. 
  - Opaque state. We aim to expose these internal states through improved DevTools, making them easier to control and observe. This is one of the essential steps in enhancing our DX.

- It's true that a CRDT is often not the right thing for a classic client/server application. But this doesn't mean we should just give up on ux and use locking.
  - There are approaches to multiplayer that are client/server native. By leveraging the authoritative server they can offer features that CRDTs can't, while preserving the great ux.
  - I'm partial to server reconciliation
  - My product, Reflect, implements server reconciliation as a service.

- > Ever-growing state
  - A) This is only the case for certain CRDTs, such as sets that support deletion - so, if you want Set semantics with deletion support, you need two sets, one to that tracks all deletions and one that tracks all insertions.
  - B) You can garbage collection your sets. They don't have to grow forever.
- > Complex implementations
  - Personally, I've never done this. I've just added a merge(&mut self, other: &Self) method to structs in Rust. Guaranteeing CRDT properties is often trivial, or at least it was in my case.
- > Opaque state: Because the CRDT has to represent both the underlying state and the updates that led to that state
  - Again, this is only if you need specific operations on your CRDTs and if your CRDTs are encoded in specific ways.

- I think the most important part of designing collaborative software, which this touches on a bit, is having a the right granularity and scope of a given change.
  - Last-writer-wins is only bad when the granularity of what you're editing is too big. 
  - The other key thing (that's also a common mistake) is to only consider realtime collaboration. In practice, there's always some delay (maybe just milliseconds but could be be hours or days) in how events propagate so solutions like locking don't work.
  - The reality is that any client-server system that needs to be highly interactive and robust to unreliable network conditions is undeniably a distributed system and therefore warrants using distributed system solutions like vector clocks, Lamport timestamps, CRDTs, etc.
  - Last thing is that I think many people only think of operation-based CRDTs when they think about CRDTs. You can (and we have at my company) created a fairly traditional feeling database that relies on a state-based CRDT solution that doesn't need to maintain a log of every operation that has every happened.
  - So yes, you might not need to reach for a fancy library like Yjs or Automerge, but it's worth understanding how these things thinks basically work because many of them are extremely simple and easy to grok - the complicated parts of Yjs and Automerge are the sophisticated data-structures and algorithms that are pretty much only needed for large document text editing.

- Wrote about something similar a while ago 
  - [A Pragmatic Approach to Live Collaboration | Hex_202009](https://hex.tech/blog/a-pragmatic-approach-to-live-collaboration/)
  - Using a server to tie break and locking has worked pretty well for us
# discuss
- ## 

- ## 

- ## 
