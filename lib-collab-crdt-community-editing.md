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

- ## 🤔 [Lies I was told about collab editing, Part 1: Algorithms for offline editing | Hacker News _202412](https://news.ycombinator.com/item?id=42343953)
- 👷🏻 Author of Eg-walker & ShareJS here, both of which are referenced by this post.
  - when users edit content offline, or in long lived branches, you probably want the option to add conflict markers & do manual review when merging. (Especially for code.)
  - algorithms like egwalker have access to all the information they need to do that. We store character-by-character editing traces from all users. And we store when all changes happened (in causal order, like a git DAG). This is far more information than git has. So it should be very possible to build a CRDT which uses this information to detects & mark conflict ranges when branches are merged. Then we can allow users to manually resolve conflicts.
  - Algorithmically, this is an interesting problem but it should be quite solvable. Just, for some reason, nobody has worked on this yet

- 👷🏻(chronofold): The author describes the case of overlapping concurrent splices. 
  - It is a known funky corner case, yes. 
  - If we speak of editing program code, the rabbit hole is deeper as we ideally expect a valid program as a result of a merge. There was a project at JetBrains trying to solve this problem through AST-based merge. 
  - After delving into the rabbit hole much much deeper, the guys decided it is not worth it. This is what I was told.

- I would simply argue that the “offline” editing is a people-problem and hence van not be solved using automation. People shall find a way to break/bypass the automation/system.
  - The only “offline editing” that I allow on human text documents is having people add comments. So not editing, no automated merging.
  - For “offline editing” that I allow on automation (source code) is GIT which intentionally does not pretend to solve the merge, it just shows revisions. The merge is an action supervised by humans or specialised automation on a “best guess” effort and still needs reviews and testing to verify success.
- Yes I agree. But remember: but git will automatically merge concurrent changes in most cases - since most concurrent changes aren’t in conflict. You’re arguing you want to see & review the merged output anyway - which I agree with.
  - right now CRDTs are too optimistic. If two branches edit the same line, we do a best-effort merge and move on. Instead in this case, the algorithm should explicitly mark the region as “in conflict” and needing human review, just like git does. 

- I want a tool with the best parts of both git and a crdt:
  - From CRDTs I want support for realtime collaborative editing. This could even include non-code content (like databases). And some developer tools could use the stream of code changes to implement hot-module reloading and live typechecking.
  - From git I want .. well, everything git does. Branches. Pull requests. Conflict detection when branches merge. Issue tracking. (This isn't part of git, but it would be easy to add using json-like CRDTs!)

- 🤔🤔 The other dark side of implementations using CRDTs is the infrastructure load. I wrote about this in depth previously, and Supabase wrote an article a couple of years ago about a CRDT extension for Postgres which I'm happy to discover agrees with my empirical findings.
  - If you're going to use CRDTs, do yourself a favor and either use Redis or similar (though the amount of memory being consumed is painful to think about), or MyRocks (or anything else based on RocksDB / LevelDB). Whatever you do, do _not_ back it with an RDBMS, and especially not Postgres.
- PowerSync has an article on using Postgres with Yjs (and perhaps look into Yrs, the Rust implementation, as well as other Rust crates like Loro and Automerge that are much faster) and they use a table in the database that stores the changes, is that what you are doing too

- One challenge is that the algorithms typically used for collaborative text editing (CRDTs and OT) have strict algebraic requirements for what the edit operations do & how they interact. So even if your server is smart enough to process the "Colour" example in a UX-reasonable way, it's very hard to design a corresponding CRDT/OT, for optimistic client-side edits.
  - You can work around this by not using CRDTs/OT. E.g., the server processes operations in receipt order, applying whatever UX logic it wants; clients use a rebase/prediction strategy to still allow optimistic edits on top

- I implemented differential sync mostly because I couldn’t understand anything else and seemed simplest in my grugnotes.com app 

- A gramatically aware text CRDT? At least aware of words and sentences? I'd be curious to hear whether that's been tried, and if it solves any issues or produces new ones.

- ## [Building Document-Centric, CRDT-Native Editors | Hacker News _202410](https://news.ycombinator.com/item?id=41923693)
- Document-centric workflows were once the great promise of the future, and inspired Microsoft's OLE, Apple's "Publish and Subscribe", and then OpenDoc.
  - You would in essence be able to build your own perfect word processing environment (for example), by bringing Company X's editing tools, Company Y's grammar checking and spelling tools, perhaps some embedded spreadsheet tables from Company Z if you were writing business reports, and so on.
  - We kind of have this a little today with browser extensions, in that we can extend functionality onto a webpage we're viewing, but our environments are still very application-centric and not workflow or content-centric at all.

- 💡 I just recently put into production a large scale document centric CRDT editor using yjs and Vue3/Vuetify. This is a platform agnostic WYSIWYG editor that supports around 30M daily users. It was a really intense experience writing this software! It uses YJS as the document, then creates an event sourced change stream (ydoc changes) that is streamed in via a websocket (APIGWV2) lambda into a dynamodb, then projected into S3 as plain old JSON for service load. The editor presents "what the web sees" for platform preview and is interpreted from the ydoc. All serverless. Multi user is awesome! History is awesome! The whole thing is just really cool!
  - I ran into two major issues: 
  - upstream updates being too large for a websocket which I fixed with signed URLs to a S3 YJS triggered lambda that inserted these very large events - which are exceptionally rare, like when I user copies/pastes a giant doc. 
  - That and multi user hierarchical updates, like where a user updates a parent node and that triggers an update of the children messing up the other user. 
  - The trick was to flatten the hierarchy into a linked list on save and save the doc as a flat ymap structure in the DB. I had to chunk serialized strings into dynamodb because of the ~400k row limit, but no regrets, loads are very fast over WS even when chunked. Lots of learning. Really fun system to write.

- I was very excited about the "Document-Centric" mention in the title, but the article does not really deliver in that regard (other than indicating that separating content from editor logic is important).
  - What I expected instead: a way to consider the document as the first-class citizen in people's workflows (especially local-first flows, since CRDT is mentioned), which is a big challenge considering that all filesystems are still file-oriented (ie. if you want two versions of a document, you end up with two files, which then become two documents since there's nothing binding them).

- I'm completely into the idea that your data should be document-centric, this I've seen working at a very large scale (i.e. 100+ MB JSON blobs being updated at 60 FPS with a large team of people editing at the same time) with the structure we built at Framer.

- I think we already standardized with the file as the unit of document exchange. You can make a CRDT interface to that file if you want, but CRDT is should not be the authority. There are too many competing implementations and what is best is too context specific and we already have the file as the standard everywhere so it's never gonna catch on

- By putting all the state into a single CRDT then yes, you're going to get conflict resolution across the entire document. But you might also want to think about how big that CRDT state is going to get.
  - There's no splitting or isolation available here, you need to load the entire Y. Doc to get any of the content of the page. The content of the Y. Doc is opaque bytes, and if you dump it to some other representation (like JSON) then you lose the internal Y. Doc counters that make conflict resolution work.
- Yjs had a “subdocument” facility for dividing up content for lazy loading, although I’m not exactly sure if or how cross-doc transactions would work.
  - If you compare Ydoc for a very large page with many items to a web API maybe it seems like it could be a bit big, but traditional file document in an editor like Pages are frequently several megabytes, it really doesn’t seem spooky to me in a truly local first app where you will delta sync.

- ## [Cola: A text CRDT for real-time collaborative editing | Hacker News _202309](https://news.ycombinator.com/item?id=37373796)
- I would guess a G-tree is still a B-tree with additional parent pointers, the fact that it is stored in an array is a matter of representation but does not fundamentally change the structure. This still stores pointers, they are just in units of the node size instead of bytes and relative to the first array element instead of the beginning of the address space. A complete binary tree stored in a array without any explicit references, i.e. an implicit representation with the children of the node at index x stored at indices 2x + 1 and 2x + 2, is still referred to as a binary tree, just with an implicit representation.
  - A quite clever representation of a tree that I read about is to store nodes in DFS order in a flat array. Given that it’s read only and the readers want to traverse it depth first anyway, this can be quite efficient. S-expressions and HTML come to mind.

- This doesn’t appear to support rich text formatting ranges like bold, italic, etc - unless I’m missing something in the API. AFAIK Peritext is still the state of the art in rich text CRDT algorithms 
- 
- 
- 

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
