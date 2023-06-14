---
title: lib-editor-gutenberg-dev
tags: [dnd-builder, editor, gutunberg, lib]
created: 2021-07-11T09:05:27.066Z
modified: 2023-02-05T19:12:13.098Z
---

# lib-editor-gutenberg-dev

# guide

- usecase
  - 开源建站编辑器工具可参考gutenberg、wix
# docs
- gutenberg /8.1kStar/GPL.v2/202208/js
  - https://github.com/WordPress/gutenberg
  - https://wordpress.org/gutenberg/
  - The Block Editor project for WordPress and beyond
  - 第三方的插件特别丰富

- Gutenberg’s all-encompassing goal is a post- and page-building experience that makes it easy to create rich layouts. 
  - The block editor was the first product launched following this methodology for working with content.

- principles
  - Authoring rich posts is a key strength of WordPress.
  - Blocks will unify features and types of interaction under a single interface. 
  - Make core features more discoverable

- vision
  - Everything on a WordPress website becomes a block.
  - All blocks are created equal.
  - Drag-and-drop is secondary. 
  - Placeholders are key to predefine editable layouts.
  - Direct manipulation is intuitive. 
  - Code editing shouldn’t be necessary for customization. 
# discuss-collaboration
- ## 

- ## 💡 [Block Collab: New package, a framework for collaborative editing_202006](https://github.com/WordPress/gutenberg/pull/23129)
- I have not seen any progress since Sep 2021.

- [[WIP] Draft: Sync Editor React state with Yjs](https://github.com/WordPress/gutenberg/pull/18357)

- ## [Collaborative editing using WebRTC](https://github.com/WordPress/gutenberg/issues/1930)

- ## 💡 p2p Real Time Collaborative Core Data Entity Editing
- https://github.com/WordPress/gutenberg/pull/17964
- I’ve been thinking a lot about full collaborative editing for Gutenberg, Google Docs style.
  - I know this was explored in a few PRs with per-block locking, because “full collaborative” seemed too hard without relying on the WordPress host being able to run and keep up long running syncing processes and what not. 
- Here is the minimum code/effort approach that I think would work:
  - Convert block edits into conflict-free replicated data types (CRDT). This should be pretty straight forward because they are mostly Redux action POJOs. We would need to add a version vector for them and a new relative index based abstraction for storing block position, i.e. inserting a block between block 1 and block 2 should yield a new block at position 1.5 and not change the others’ indexes.
  - This would essentially mean that all block edits would become idempotent and commutative. We would also need to implement undo in block-editor, instead of relying on core-data, so that we can keep the undo stack specific to the client.
- For RichText, things will be a bit more complex and a CRDT refactor might be too costly, but we could easily implement diff-sync for it or use a compatible library.
  - Diff-sync, in short, is when the client keeps a copy of what the server has and the server keeps a copy of what each client has. When the client wants to sync, it can easily send a diff, the server then applies that diff both to its copy of the client’s contents and to itself. 
  - The only issue with diff-sync is that you need a host, now although not ideal, if the WordPress instance does not support being a host for this, we could fallback to a client acting as the host. Otherwise, we could embark on the RichText refactor or just lock RichText fields and send CRDT edits for their whole value.
- This PR explores a Conflict-free Replicated Data Type (CRDT) based p2p approach to collaborative core-data entity (#17368) editing.
  - The p2p layer uses the Gun engine which automatically converts JSON objects without arrays into CRDTs
- The main difference from a user's perspective is that instead of locking blocks, we do conflict resolution down to the individual block property level. We can do this easily because JSON objects without arrays are generally convertible to CRDTs through adding some type of vector clock system to make deep merge style updates commutative.

- The better engine to use for free and open source collaborative rich text editing is github.com/yjs/yjs.
  - Similar to GUN Yjs can work completely peer2peer and also uses CRDTs (as would Automerge).
  - The server code is also rather trivial for Yjs —- it’s basically passing messages from client to client - when WebETC is not available / reliable.
- CKEditor did build a great commercial product, which they use to make money with (good for them), 
  - but implementing OT for OSS projects is not so great as there are a lot of rules to implement
  - Building upon CRDTs has the added advantage that Eg collaboratively configuring Components becomes a breeze - similar to how it was implemented here with gun.eco.

- Gun is an awesome project and I'm inspired by some their concepts. 
  - Yjs and Gun share similar goals - mainly providing observable shared data types. 
  - But Yjs really focuses on providing an efficient backend for collaborative editing, offline editing, and showing differences between different states. 
  - Basically everything that you would expect from Google Docs - but p2p and OSS. 
  - To my knowledge, Yjs is the first CRDT implementation that is suited for rich-text editing on large documents. Yjs implements a CRDT algorithm that is highly optimized for collaborative (rich)-text editing
- Gun doesn't really provide a method to model text for concurrent operations. As you mentioned above, you simply replace the whole text-field so that only one user can work at a single section at a time. This might lead to a very bad user-experience when working offline or with a slow connection.
  - Yjs is really great at manipulating large lists. As @LionsAd mentioned, you can even use the Yjs Text type to assign ranges on text attributes (like bold, italic, ..).

- The single point where Yjs is better than gun.eco is that it supports the text editing.
  - While it's pretty simple to implement text editing with CRDTs, it's hard to do that efficiently for long texts and also for rich-text editing (e.g. bold, italic, etc.).

- If I'm correct, Gutenberg has an immutable data structure - similar to ProseMirror (another editor that Yjs supports)
  - yes

- ## [Concurrency control in core-data](https://github.com/WordPress/gutenberg/issues/26325)
- I discovered what appears to be a massive problem with API interactions in core-data.
  - There seems to be no concept of concurrency control

- Possible solutions
- Atomic operations
  - We could prevent concurrent conflicting operations:
  - By not resolving while write operation is in progress
  - Using locking (shared lock and exclusive lock maybe?).
  - Stacking multiple conflicting operations may take a long time to process
- Re-use fetched data

- [[core data] State locks for concurrency control_202011](https://github.com/WordPress/gutenberg/pull/26389)
  - it addressed the bulk of this problem. It would still be amazing to implement a lock-less solution or be more "optimistic" about different operations
# discuss
- ## 

- ## 

- ## [Thoughts on RichText & Performance](https://github.com/WordPress/gutenberg/issues/15033)
- Perhaps we can do something like AsyncMode in #13056, but instead of just the page AND the selected block re-rendering (correct me if I'm wrong), re-render only the selected RichText instance, and the rest of the page and block lazily.

- ## I don't need to make much content in WordPress much anymore but wow the blocks editor is a PAINFUL experience.
- https://twitter.com/dan_shure/status/1331012849968230400
- I'm still on the classic editor but toying with the idea of swapping to the block editor. I'm familiar with the general approach of using content blocks from Drupal etc
- WP is the best sales person sometimes for Divi & Elementor
- You can't easily copy content from one post to another; when you do, you often lose links, alignment, & other settings; 
  - I can't even adjust where I place a graphic within a block of text. 
  - It's absolutely awful, but I've had my blog w/ Wordpress since 2012 so I feel stuck with it.

- ## I realize the #WordPress Gutenberg block editor isn't perfect. 
- https://twitter.com/karks88/status/1364553379167494145
  - But there have been so many times when an older site (with Classic Editor) needs a particular feature and I think: "Wow, I could do that so much easier in Gutenberg".
  - Once you get the hang of it, it saves time.
- I agree completely, although there are still places where it’s too complex for basic content creation and not sophisticated enough for rich layout building
- For a one-off page, using custom fields works just great. The blocks are an extra step and could be overkill for those cases. Still find myself doing this quite a bit.
