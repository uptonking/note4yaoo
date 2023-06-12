---
title: lib-editor-prosemirror-community-block-editor
tags: [block-editor, community, prosemirror]
created: 2022-08-30T19:03:53.024Z
modified: 2022-08-30T19:04:37.774Z
---

# lib-editor-prosemirror-community-block-editor

# guide

# discuss
- ## 

- ## 

- ## Data structure with ids
- https://discuss.prosemirror.net/t/data-structure-with-ids/33
  - We have a data structure where blocks need to remain associated with ids (and metadata). 
  - Is there a way to keep the edited html tied to a specific id, so we can convert back to the original data structure?
  - Now we’re using a `data-grid-id` attribute on each top-level child of our editable. We have a function to make a new id if new blocks are made by the editor.

- I see this is a very old thread, I’d like to know going down this road with Prosemirror is a good solution. 
  - My company is looking to switch over to Prosemirror from another rich text editor, but we need to keep our existing data structure and update system. 
  - Basically like above, 👉🏻 we store each top level node by a unique key, and we persist updates to the doc by a transaction with the key of the top level node that was changed, and the new data within. 
  - Will this mesh ok with Prosemirror or should I look at other editors?
- You should be able to map between such a system and ProseMirror transactions, if you really want to. Getting collaborative editing working with such a representation is another issue, but maybe that’s not a requirement for you.

- There are very concrete plans to add the ability to modularly define new attributes for node types, but that doesn’t exist yet. So you could kludge something up that attaches ids to nodes after parsing (node.attrs.id = 100), and those will survive editing and stay present in the document. You could even (though again, the API sucks) extend serializers to somehow include these IDs in a given document output format. But to be able to do this in a clean and modular way, you’ll have to wait for the schema work to materialize. I’ll keep this specific use case in mind as I work on that.

- You could try putting your data directly into attributes, but you’ll have many of the same issues: what happens when the node is split? what happens when it is copied? You no longer have to worry about uniqueness though, which might be helpful.

- ## how to turn the current paragraph into a heading and wraps it into a section.
- https://discuss.prosemirror.net/t/how-to-make-changes-that-temporarily-violate-the-schema/4836
  - `tr.setNodeMarkup(pos, HeadingType).wrap(paragraph, {type: SectionType})` does not work

- It may be a more productive direction to relax your schema constraints, also for ease of editing (so users don’t have to understand a set of complicated transformation commands to create the documents they are interested in), and treat the desired structure more like a lint than a hard constraint.

- ## Nested draggable editors behave differently in all browsers_202111
- https://discuss.prosemirror.net/t/nested-draggable-editors-behave-differently-in-all-browsers/3807
- This got me interested in how Prosemirror implements dragging of nodes that are editable since this is similar to that in a way. 
  - PM adds a draggable attribute on demand to such nodes (compare that to the example in glitch with a permanent draggable attribute), when it deems the user might be interested in drag. 
  - This makes me feel that a draggable attribute messes with an editable element and to solve the problem we might need to do something similar to what pm-view has done in src code

- I’d argue they are browser issues—👉🏻there’s no consensus on how draggable+editable text should work, and browsers do different things (even Chrome’s behavior isn’t ideal I think). It’s usually better to use drag handles separate from the editable text.

- I’ve kept the custom view using `draggable: true` as without it, we’d lose dragging functionality. Instead, after initialization, I’m removing the `draggable="true"` attribute from the DOM element. This doesn’t seem to affect draggability, but does fix Firefox’s inability to select text.

- ## Detect block changes to manage blocks as separate data in backend
- https://discuss.prosemirror.net/t/detect-block-changes-to-manage-blocks-as-separate-data-in-backend/4870
- Background
  - We are using Firestore (which is a NoSQL Database) to store data
  - Every first-level block of content(direct children of “doc”) should be stored as a single data(precisely, document in Firestore). So if the editor has two paragraphs, each paragraph is saved as two different data.
- Question - Is there a good way to detect ; 
  - when a new block content is added
  - when an existing block content is updated
  - when an existing block content is deleted
- 

- ## Block structure editor by prosemirror_202003
- https://discuss.prosemirror.net/t/block-structure-editor-by-prosemirror/2620
  - notion’s block is an independent contenteditable dom, which only has an independent node (table/calendar or other nodeType)
  - I am wandering if separate all my schema into each mini-prosemirror editor and have a doc container that holds all the mini-prosemirror, can i achieve the block structure style new editor as notion.
  - besides, doc contains too many prosemirror instance will affect performance severely ？

- You can, but I don’t see why you’d want that. **Separating your document into multiple editors breaks things like cross-block selections**. This type of setup complicates user interaction, and I never really understood what advantage it brings.
  - in my opinion, notion block structure makes it flexible to save the data, cus doc can be described as two part: block-id-list, block-content-data-hashmap
  - besides, each block has it's own menubar popover, so user don't need move mouse up to top menubar and down to editor frequently, make user experience better.
  - in my project, i want treat table as database to make table data accessable and sharable between different user's docs, maybe block style can be a little bit easier.
  - Notion’s solution to this is quite nice: dragging a selection across two blocks creates a selection containing the whole of both blocks.

- Presumably it allows for larger documents without scaling issues, as the editor only needs to run calculations for the block currently being edited.

- Notion style block editor can be done using Prosemirror without multiple editors as you can hook into hover events and get all the information you need using `posAtCoords`.

- ## [I’m building a heavily-customized editor like roam-research](https://discuss.prosemirror.net/t/im-building-a-heavily-customized-editor-like-roam-research/3006)
- https://github.com/namiwang/fiber-note /ruby/ts/inactive
  - [building a roam-like, networked, heavily-customized realtime editor, part 1](https://namiwang.github.io/2020/11/12/building-a-roam-like-networked-heavily-customized-realtime-editor-part-1.html)
