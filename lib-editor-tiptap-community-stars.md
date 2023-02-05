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
- The notion style inline autocomplete dialog is becoming standard for text editors and I love it :)
