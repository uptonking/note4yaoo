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

- ## 

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
