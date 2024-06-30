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

- ## ✏️ [Using CRDTs for multiplayer text editing | Hacker News _202212](https://news.ycombinator.com/item?id=33820975)
- One common failure mode is that two people start typing at the beginning of the same line, and rather than getting two lines, it alternates characters. At least, Etherpad did this.
  - This is called the “interleaving problem”. It shows up with simple list algorithms like fractional indexing.
  - All the main text editing CRDT algorithms around today solve this no problem. (Yjs, automerge, diamond types, etc).

- Peritext is the only one that came close to solving rich-text, but even that one left out important aspect of rich-text editing like handling list & table operations as "work to be done later".

- 
- 
- 

- ## 🧮✏️ [investigate sequence/text crdts _202211](https://github.com/vlcn-io/cr-sqlite/issues/65)
- If we don't target WASM I think adding diamond types will be easy.
  - Targeting WASM makes everything harder since WASM binaries currently can not load other binaries (AFAIK) so we have to compile Rust code with C code. 
  - Maybe I'm worried about nothing and that is actually an easy thing to do?

- We've (iver & myself) been discussing this a bunch offline and here is a summary of where we're at so far:
  - 💡 **Queries that order by a recursive relationship in SQLite are actually rather performant** 
  - Because of (1), _we can represent any tree-based CRDT in a table_
  - A proposed table structure is something like below

- If you're interested, one alternative is to use a "CRDT-quality" version of fractional indices. 
  - These will never be as storage-efficient as a dedicated list CRDT, but you can generate the strings in <100 LOC and put them in a "position" column that you ORDER BY.
- 🤔 I still haven't seen any fractional indexing string which didn't have interleaving problems.. Has that been solved?
  - Yeah, it was also my impression that you couldn't fix the interleaving problem with fractional indexing.
  - btw -- we have implemented fractional indexing in cr-sqlite. 

- It should be non-interleaving in both directions. 
  - The total order is equivalent to a tree walk over a binary-ish tree; concurrently-inserted sequences end up in different subtrees, which don't interleave.
  - **You do pay for this with longer strings**, though: "averaging" two neighboring strings adds a UID (~13 chars) instead of a single bit, except when the in-order optimization kicks in.

- Is there an approach with fractional indices that does not require tombstones for character removals?
  - You don't need tombstones - just the positions of present characters. It's okay to call d = source.createBetween(a, b) even if there used to some other a < c < b where c was deleted. You can even "restore" c later and it will compare to d in a reasonable way (though I'm not sure about non-interleaving).
  - Fractional indexing in general also shouldn't need tombstones, except for the usual uniqueness issues.
- 🌲 In general, for any tree-based list CRDT, you can choose if you want "no-tombstone mode" with longer positions (= whole paths in the tree), or "tombstone mode" with shorter positions (= pointers to nodes in the tree). 
  - The former lets you compare two positions directly, without consulting some external tree state; so position-strings (and fractional indexing) uses this mode. 
  - But tombstone mode is usually more memory-efficient, so that's what the slides recommend, and what libraries like Yjs do.
- I think it would be possible to re-implement that optimization within a database table (e.g. columns "position" and "substring", instead of "position" and "char"), but it could be hard to query.

- I think we can implement a variant of Fugue that stores multiple chars per row. (Untested)

- Closing this as I think enough research has been done and I'm ready to start implementing

- ## 🌵📄 I'm presenting some early ideas about CRDTs & branch-and-merge documents.
- https://twitter.com/MatthewWeidner3/status/1715023602976764299
  - [Proposal: Versioned Collaborative Documents (PLF 2023 - Programming Local-first Software) - SPLASH 2023](https://2023.splashcon.org/details/plf-2023-papers/4/Proposal-Versioned-Collaborative-Documents)

- One compromise is to use a git-like arch (full history, merge reviews) but store CRDT updates instead of git's patches. The CRDT enables live collaboration, and first-pass merges for non-code data (e.g. spreadsheets).
# discuss
- ## 

- ## 

- ## 

- ## [Cola: A text CRDT for real-time collaborative editing | Hacker News _202309](https://news.ycombinator.com/item?id=37373796)

- ## [Overleaf: An open-source online real-time collaborative LaTeX editor | Hacker News](https://news.ycombinator.com/item?id=40832930)

- ## 🧮 CRDT: Text Buffer
- https://news.ycombinator.com/item?id=40414435

- ## Using "index" to denote cursor positions can be unstable, as positions may shift with document edits. 
- https://twitter.com/zxch3n/status/1777341492467847650
  - We can use characters' IDs to represent positions stably in a Text CRDT. What should we call them?
  - Relative positions
  - Stable positions
  - Cursors
- While Yjs keeps a "relative position" for historical reasons, after some discussion we actually started to call it "sticky index" (this name is used in Yrs). 
- Other proposals were:
  - cursor position: given cursor is another concept used in yrs/yjs
  - bookmark
- using character ids as anchors feels like relative positions, stable positions feels more like ‘position strings’ or ‘fractional indexing’.
- If I remember correctly, in Automerge there were cursorId and it was pretty clear

- ## [SQLite Forum: [novice] Handling edit conflicts with wiki-style editing _202207](https://sqlite.org/forum/info/e26a268fe9a411ad48d4e192436d529856081129c7ddafc5bee53de6ff4bbada)
- > Fossil's wiki system works on a "last one wins" principle.

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
