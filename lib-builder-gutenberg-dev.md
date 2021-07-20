---
title: lib-builder-gutenberg-dev
tags: [builder, gutunberg, lib]
created: '2021-07-11T09:05:27.066Z'
modified: '2021-07-11T09:59:06.221Z'
---

# lib-builder-gutenberg-dev

# guide

- usecase
  - 开源建站编辑器工具可参考gutenberg、wix
# docs
- https://github.com/WordPress/gutenberg
  - The Block Editor project for WordPress

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
# discuss
- ## 

- ## 

- ## 

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

- ## p2p Real Time Collaborative Core Data Entity Editing
- https://github.com/WordPress/gutenberg/pull/17964
- The better engine to use for free and open source collaborative rich text editing is github.com/yjs/yjs.
  - Similar to GUN Yjs can work completely peer2peer and also uses CRDTs (as would Automerge).
  - The server code is also rather trivial for Yjs —- it’s basically passing messages from client to client - when WebETC is not available / reliable.
- CKEditor did build a great commercial product, which they use to make money with (good for them), 
  - but implementing OT for OSS projects is not so great as there are a lot of rules to implement
  - Building upon CRDTs has the added advantage that Eg collaboratively configuring Components becomes a breeze - similar to how it was implemented here with gun.eco.
- I investigated Gun a bit and I'm not sure if I can fairly compare gun with the other CRDTs. 
  - The benchmark mocks the network layer and Gun has its network layer deeply integrated.
  - If I'm correct, Gutenberg has an immutable data structure - similar to ProseMirror (another editor that Yjs supports).
