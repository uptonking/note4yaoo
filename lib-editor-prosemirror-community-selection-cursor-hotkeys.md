---
title: lib-editor-prosemirror-community-selection-cursor-hotkeys
tags: [community, hotkeys, prossemirror, selection]
created: 2022-08-30T22:08:40.911Z
modified: 2022-08-30T22:09:32.804Z
---

# lib-editor-prosemirror-community-selection-cursor-hotkeys

# guide

# discuss
- ## 

- ## Prosemirror-virtual-cursor
- https://discuss.prosemirror.net/t/prosemirror-virtual-cursor/5044
  - When the cursor is right between two different marks, it will show a little tail to indicate the mark of following input. 
- Under the hood, I hide the native cursor and use `Decoration.widget` to insert a `<span>` element to the cursor position. 
  - Another approach would be calculate the coordinate of the cursor and put an element at that coordinate. 
  - 👉🏻 I refactored prosemirror-virtual-cursor and overlay the cursor over the editor.
- 
- 

- ## Marquee Selection & Selecting Multiple Nodes for Dragging
- https://discuss.prosemirror.net/t/help-marquee-selection-selecting-multiple-nodes-for-dragging/2569
  - This mimics the behavior of selections in a software called Notion.

- I implemented BlockSelection as a plugin that doesn’t use the window’s selection at all.
  - https://ccorcos.github.io/prosemirror-examples/#/block-selection-plugin
