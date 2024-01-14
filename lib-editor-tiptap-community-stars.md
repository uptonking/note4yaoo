---
title: lib-editor-tiptap-community-stars
tags: [community, editor, prosemirror, tiptap-editor]
created: 2022-09-10T02:54:58.721Z
modified: 2023-02-05T19:03:27.729Z
---

# lib-editor-tiptap-community-stars

# guide

# discuss
- ## 

- ## 

- ## Collaborative Editing
- https://github.com/ueberdosis/tiptap/issues/74

- ## Excited to release BlockNote, an open source Notion/Coda style block-based text editor component__20220908
- https://twitter.com/YousefED/status/1567855632237137921

- What’s the underlying data model here: separate object per block? Or one prosemirror doc for the whole doc?
  - One prosemirror for the whole doc! Going for separate editors felt like cheating, would hinder certain features like cross-block textselection and I think also less ideal in terms of performance. What’s your experience with this / what’d be your approach?
- Makes sense! Is there any way to stably address an individual block with an ID? (I don’t think either way is better necessarily, just big tradeoffs either way)
  - Yes, every block gets assigned a unique ID
  - Also, another tradeoff we made is dropping some of the Prosemirror "semantic" node types. 👉🏻 In BlockNote, every node is a "block" (instead of p, li, h1, etc), with styling and type attrs. This made it possible to create animations, nesting and simplifies working with lists

- we have the same base structure on our editor in @mintterteam , but in Slate. Looking forward to review the code, compare and share ideas!
- Great work, is there already an api for creating custom Components?
  - It's certainly possible to create a custom component, but should work on a tutorial / clearer API. What kind of component are you looking forward to to build?
  - Different defined UI Components with predefined fields to render. for example Galleries, Banners, .. You know how Storyblok handles their inline Components? Thinking of on click edit the fields in the form and then on save render it in the editor.
- You should work for @Odoo They built something very similar.
  - Yes, its default from Odoo v15 and will be further enhanced with v16.
  - It is open source. Part of https://github.com/odoo/odoo so not standalone.

- ### [Show HN: BlockNote – a “Notion-style” block-based text editor](https://news.ycombinator.com/item?id=32764493)

- have you looked at what Liveblocks has done in their example. It looks a lot to what you've done, but I really like the collaborative aspect.
  - I think the Liveblocks demo is quite impressive as well! It looks pretty smooth. 
  - 👉🏻 One of the main things I'm missing is the ability to nest (indent) blocks similarly to how Notion / BlockNote allows this. This was quite a bit of work to get right in BlockNote.
  - BlockNote's live collaboration is powered by Yjs, or (y-prosemirror to be exact).
- I really appreciate your efforts. There are many text editor but most of them lack some features critical for detail writing.
  - Full featured image, video, embed, math, table, symboll support will put BlockNote in a good position.
  - Agree those components are important. Some of them are already available for the Prosemirror ecosystem, so it should be straightforward to add them. Focus so far for BlockNote has been to get the “block” system right (including nesting, drag and drop, etc) and the basic UX elements (placeholders, menus, etc). Now I think we can continue working on more block types!
- I don't think I could ever use a Notion-like product without their database/table feature. I'm addicted to it now. And toggles too. I feel like toggles are a way for detail oriented people to detail everything they feel they should, but at the same time deliver a document that anyone can read haha
  - Toggles are on the roadmap to add! They are definitely a basic kind of block that should be built-in. Databases/tables are a whole different ball game of course. I’d like to focus on building an open source, reusable text/block editor on par with Notion’s editor, not to build a clone of their entire product :)
- The notion style inline autocomplete dialog is becoming standard for text editors and I love it

- ## 🚀 [Launch HN: Tiptap (YC S23) – Toolkit for developing collaborative editors | Hacker News_202308](https://news.ycombinator.com/item?id=36957204)
- Substack uses Tiptap for their editor that allows creators to write content on substack.com, and YC uses Tiptap in their Bookface forum
  - With the Tiptap Cloud, we offer managed backend services if you don't want to build and maintain every feature yourself

- jitl/notion: Having more batteries included is good, but I’ve found that layers of abstraction can really get in the way. 
  - For example if I need to fix a bug with Android Gboard input, without a framework I can exactly control the DOM structure and input handling, but the downside is no one fixes the bug for me. 
  - Ultimately I decided adopting a library was too risky, and opted to improve our native ComtentEditable handling. Because our product’s selling point is an editor, we want to control our own destiny.

- Out-of-the-box libraries like Tiptap are great when their extensions or components fully cover your use case. But when you need to customize or own the code itself, the secondary abstraction becomes leaky and you start to fight against it.
  - That being said, the journey of moving off Tiptap to ProseMirror took a couple of months for a junior dev. So I can understand how a market for it exists.
  - My only wish for Tiptap now is for it to reduce its API overhead on ProseMirror, and instead build more advanced ProseMirror-compatible plugins that require a backend. 
  - Collaborative editing (comments, annotations), version control and schema migration, etc are all exercises normally left up to the developer that can be solved by Tiptap well.

- I spent quite a bit of time as an FTE building out a robust-ish and efficient Yjs backend POC. 
  - At the end of it all my personal takeaways were:
  * State-based CRDT isn't great when you want a central authority in the mix anyway and are fundamentally trying to work with operations
  * The exchange rate between ProseMirror's currency, steps, and some other replication strategies building blocks is too high
  * ProseMirror should add the concept of range-relocation to its mappings; this is a bit of an aside but it would help retain user intent when reconciling concurrent edits involved in block relocations
  - As a concrete example for others imagine a knowledge base editor. You want allow certain users ONLY to comment and you want to enforce this on the backend
  - Yjs just cares about syncing state so the documents end up equivalent, and its efficient diff format doesn't really have the info you'd need to determine what's going on. You'd need to have the actual document model loaded, and then diff the docs before/after to figure out exactly what happened. And/or patch into the Yjs binding diff algorithm which works surprisingly well but doesn't produce minimal changes and can often "over edit" the document model.
  - So something that was relatively simple with ProseMirror steps has become a huge thing with Yjs. And for what?
  - Automerge is supposedly operation based so in theory it sounds like a better route for use cases involving a central authority and want to do extra processing on document operations.. But it'd need to bring a lot to the table to offset the time investment

- We have been using Tiptap in production for more than a year in Notesnook
  - Tiptap is a good choice if you are looking for a framework agnostic and thin abstraction over Prosemirror. However, if you are primarily working with React you should go with Remirror. Tiptap's APIs are heavily inspired by Remirror (almost a duplicate in some places). Remirror takes the edge on the maturity and stability of the API and extensions. The sheer number of utilities offered by them to simplify Prosemirror's APIs is astounding
  - In the end, though, its Prosemirror that's doing all the heavy lifting. And no matter how many abstractions you put on it, you will have to get really, really close in with Prosemirror's internals. Tiptap or Remirror do not make that any easier or harder aside from the initial bootstrapping.

- As we continue to improve Tiptap, we would be interested in more details about the "rough corners". Do you have any examples?
  - The main problem had to do with fields inside a custom component not updating the tree (document JSON?) properly. These components could be nested, they had each a title and another variable-content field into which other components could be nested into. 
  - It might be somewhat similar to the "details" extension, but they were also drag and droppable. The drag and drop support was also somewhat subpar compared with TinyMCE, I ended up using vue.draggable.next to solve the issues, but this added a layer of huge complexity.

- Out of the ContentEditable libraries I’ve tested, ProseMirror did the best on Android, which is the most challenging platform to support. His CodeMirror is by far the best code editor for mobile too. Monaco, the VS Code editor component, is pretty broken on mobile.

- Schema versioning is something I would really like to see in Hocuspocus, but it is currently not scheduled. So it will be a while before we tackle this topic. 
  - Currently we are building version history so that you can have a Google Docs-like history of your documents. Version history will not be available in the freeplan.
