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

- ## 

- ## [Question about drop cursor's position - discuss. ProseMirror](https://discuss.prosemirror.net/t/question-about-drop-cursors-position/5891)
- The drop cursor has nothing to do with `state.selection` . It is just an indicator displayed to show where the dragged content will be dropped.
  - There is currently no way to find the position of the drop cursor.

- ondragstart: `e.dataTransfer.setData("text/html", "<img src='xxx.png'/>")` the html will insert into the pos cursor drop

- ## [Drag a node with custom data out of text editor - discuss. ProseMirror](https://discuss.prosemirror.net/t/drag-a-node-with-custom-data-out-of-text-editor/5397/4)
- You’ll have to create a plugin that handles the drag events before the view does

- ## [Support for Multiple, Discontinuous Selections?](https://discuss.prosemirror.net/t/support-for-multiple-discontinuous-selections/1560)
  - Is there a clean, established way to create multiple selections and/or a selection with multiple, discontinuous ranges?
  - I notice that `Selection` contains a `ranges` array, but I don’t see any constructors or static helper methods for creating multiple ranges.

- Yes, creating a new `Selection` subclass, along with all the user interactions that go with it, would be the way to do this. You can see the `CellSelection` class in the tables module for an example.

- ## Prosemirror-virtual-cursor
- https://discuss.prosemirror.net/t/prosemirror-virtual-cursor/5044
  - When the cursor is right between two different marks, it will show a little tail to indicate the mark of following input. 
- Under the hood, I hide the native cursor and use `Decoration.widget` to insert a `<span>` element to the cursor position. 
  - Another approach would be calculate the coordinate of the cursor and put an element at that coordinate. 
  - 👉🏻 I refactored prosemirror-virtual-cursor and overlay the cursor over the editor.

- ## Marquee Selection & Selecting Multiple Nodes for Dragging
- https://discuss.prosemirror.net/t/help-marquee-selection-selecting-multiple-nodes-for-dragging/2569
  - This mimics the behavior of selections in a software called Notion.

- I implemented BlockSelection as a plugin that doesn’t use the window’s selection at all.
  - https://ccorcos.github.io/prosemirror-examples/#/block-selection-plugin
