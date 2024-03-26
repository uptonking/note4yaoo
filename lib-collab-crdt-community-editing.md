---
title: lib-collab-crdt-community-editing
tags: [collaboration, community, crdt, editor]
created: 2023-10-28T09:00:20.182Z
modified: 2023-10-28T09:00:45.811Z
---

# lib-collab-crdt-community-editing

# guide

# discuss-stars
- ## 

- ## 

- ## 🌵📄 I'm presenting some early ideas about CRDTs & branch-and-merge documents.
- https://twitter.com/MatthewWeidner3/status/1715023602976764299
  - [Proposal: Versioned Collaborative Documents (PLF 2023 - Programming Local-first Software) - SPLASH 2023](https://2023.splashcon.org/details/plf-2023-papers/4/Proposal-Versioned-Collaborative-Documents)

- One compromise is to use a git-like arch (full history, merge reviews) but store CRDT updates instead of git's patches. The CRDT enables live collaboration, and first-pass merges for non-code data (e.g. spreadsheets).
# discuss
- ## 

- ## 

- ## 🔀 [You Might Not Need a CRDT: Document Sync in the Wild [video] | Hacker News _202403](https://news.ycombinator.com/item?id=39615987)
- 👷🏻 jitl: Maybe you don’t need it for shapes and what not, but for collaborative text documents it’s really hard to have a good experience without convergent intention preserving async merges on text - you’re gonna want OT or CRDT for collaborative text editing eventually.
  - I work on Notion, a collaborate editor that (famously?) doesn’t merge text updates. 
  - Our editor predates the popular CRDT libraries. We’ve taken the last write wins optimistic model about as far as it will go, 
  - and now we’re building CRDT text as the basis for a bunch of new features. It’s challenging to integrate with our existing model but I think the end result will be well worth it.
- You can merge text, preserving intention, without CRDTs. In fact, you can do a better job of preserving a history log without CRDTs.
  - For an app like Notion you don't have direct peer-to-peer syncing: you have a star topology with a central service able to create a canonical total ordering of events, so you really don't need CRDTs at all.
  - For most SaaS apps even offline is going to sync with the central service and not with other peers. Direct peer-to-peer without a intermediating server is so rare for SaaS that I don't even know of an example.
- Even with a star topology, how do you go about preserving user intent for text insertions without CRDTs and without rewriting (transforming) mutations so that client and server result in same state (basically OT)?
  - When inserting text, you can either use mutations that insert the text relative to some reference character(s) or at some index. The former is basically the approach of most text CRDTs. I'm having a hard time imagining the latter without modifying the insertion index relative to concurrent insertions or deletions. I believe that Jupiter based OT imposes a global order, but uses it to determine how concurrent mutations are transformed against one another.

- 
- 
- 

- ## BlueSky uses standoff markup to represent rich text. They call them facets
- https://twitter.com/jessmartin/status/1750543829868916797
  - [Why RichText facets in Bluesky | Paul's Dev Notes _202401](https://www.pfrazee.com/blog/why-facets)

- ## The representation of comments in rich text Delta is awkward, because multiple styles cannot be merged like bold/link. Which solution do you prefer?
- https://twitter.com/zxch3n/status/1719578599517556748

- ## While CRDT algorithms go over and beyond to let conflict resolution keep user's intent in mind, most of the rich text editors don't even try to represent it in their APIs. 
- https://mastodon.social/@horusiath@fosstodon.org/111293175245189294
  - So you want to *quote* that *paragraph*? What a weird way to say "insert formatted text at this index".

- ## GPT-4 as a viable alternative to text CRDTs? 
- https://twitter.com/geoffreylitt/status/1645961623289438208
- Yes I think this is promising for async merges!
  - Probably still want tools to review what it did, but in simple cases like this can just be a ✅
  - Auto-merging code seems easier than prose since easier to verify...
- For more synchronous workflows you probably still want something fast and deterministic, but CRDTs are already good at that part; it's these "semantic merges" that are harder

- ## [Open source collaborative text editors _201905](https://news.ycombinator.com/item?id=19845776)
