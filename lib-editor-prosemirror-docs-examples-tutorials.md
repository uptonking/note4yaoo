---
title: lib-editor-prosemirror-docs-examples-tutorials
tags: [docs, examples, prosemirror, tutorials]
created: 2022-09-05T03:47:52.679Z
modified: 2022-09-05T03:48:18.133Z
---

# lib-editor-prosemirror-docs-examples-tutorials

# guide

# examples-tutorials
- examples-repos
  - [prosemirror-example-setup](https://github.com/ProseMirror/prosemirror-example-setup)
  - [official website examples](https://github.com/ProseMirror/website/tree/master/example)
  - [prosemirror-codemirror-basic](https://codesandbox.io/s/prosemirror-codemirror-basic-forked-78jbk)
  - [ProseMirror + CodeMirror 6](https://github.com/sibiraj-s/prosemirror-codemirror-6)
  - [prosemirror-tables-lib-example](https://codesandbox.io/s/prosemirror-tables-lib-example-dij6m)
    - handsontable官方和CKEditor进行了合作，但不支持prosemirror

## [basic example](https://prosemirror.net/examples/basic/)

- `prosemirror-example-setup` package creates an array of plugins
- These plugins are created by the example setup:
  - Input rules, which are input macros that fire when certain patterns are typed. 
    - In this case, it is set up to provide things like smart quotes and some Markdown-like behavior, such as starting a blockquote when you type “> ”.
  - Keymaps with the base bindings and custom bindings for common mark and node types, 
    - such as mod-i to enable emphasis and ctrl-shift-1 to make the current textblock a heading.
  - The drop cursor and gap cursor plugins.
  - The undo history.
  - A menu bar, with menu items for common tasks and schema elements.

## [Dinos in the document](https://prosemirror.net/examples/dino/)

- ProseMirror allows you to define your own schemas, which includes defining custom document elements.
- First, define a command that handles dinosaur insertion.
- Next, create menu items that call our command.

## [Friendly Markdown](https://prosemirror.net/examples/markdown/)

- you can drop in ProseMirror as an alternative input editor. 
  - People can even switch between both views as they are editing!

## [Tooltip](https://prosemirror.net/examples/tooltip/)

- I'm using ‘tooltip’ to mean a small interface element hovering over the rest of the interface. 
- There are two common ways to implement tooltips in ProseMirror. 
- The easiest is to insert widget decorations and absolutely position them, relying on the fact that if you don't specify an explicit position (as in a `left` or `bottom` property), such elements are positioned at the point in the document flow where they are placed. 
  - This works well for tooltips that correspond to a specific position.
- If you want to position something above the selection, or you want to animate transitions, or you need to be able to allow the tooltips to stick out of the editor when the editor's overflow property isn't visible (for example to make it scroll), then decorations are probably not practical. 
  - In such a case, you'll have to ‘manually’ position your tooltips.
- you can still make use of ProseMirror's update cycle to make sure the tooltip stays in sync with the editor state. 
  - u can use a **plugin view** to create a view component tied to the editor's life cycle.

## [Upload handling](https://prosemirror.net/examples/upload/)

- prosemirror图片上传的示例，上传较大图片如90k时点击图片会出现卡顿，但官方示例无此问题
  - 最后发现是自己添加pm-dev-toolkit导致的

- 在实现上传图片demo时，发现图片上传完成后，从点击图片到点击的图片出现蓝框即选中状态，耗时很长，体验很卡
  - 通过浏览器perf面板分析调用栈定位到问题
  - mouseup > selectClickedLeaf > updateSelection > dispatch > appendNewHistoryEntry(来自prosemirror-dev-toolkit)
  - `appendNewHistoryEntry`并不来自prosemirror源码，而是开发者工具引入的，这也解释了官网案例不卡的原因

- Some types of editing involve asynchronous operations, but you want to present them to your users as a single action. 
  - For example, when inserting an image from the user's local filesystem, you won't have access to the actual image until you've uploaded it and created a URL for it.
- Since the upload might take a moment, and the user might make more changes while waiting for it, 
  - the placeholder should move along with its context as the document is edited, 
  - and when the final image is inserted, it should be put where the placeholder has ended up by that time.
- The easiest way to do this is to make the placeholder a decoration, so that it only exists in the user's interface.

## [Schemas from scratch](https://prosemirror.net/examples/schema/)

- ProseMirror schemas provide something like a syntax for documents—they set down which structures are valid.
- A ProseMirror view can be mounted on any node, including inline nodes.

## [Writing your own menu](https://prosemirror.net/examples/menu/)

- The idea is, roughly, to create a number of user interface elements and tie them to commands. 
- One question is how to deal with commands that aren't always applicable—when you are in a paragraph, should the control for ‘make this a paragraph’ be shown? If so, should it be grayed out?
  - Depending on the number of items in your menu, and the amount of work required for determining whether they are applicable, this can get expensive. 
  - There's no real solution for this, except either keeping the number and complexity of the commands low, or not changing the look of your menu depending on state.
- The prosemirror-menu package works similarly, but adds support for things like simple drop-down menus and active/inactive icons (to highlight the strong button when strong text is selected).

## [Embedded code editor](https://prosemirror.net/examples/codemirror/)

- It can be useful to have the in-document representation of some node, such as a code block, math formula, or image, show up as a custom editor control specifically for such content. 
- **Node view**s are a ProseMirror feature that make this possible.
- In this example, we set up code blocks, as they exist in the basic schema, to be rendered as instances of CodeMirror, a code editor component. 
  - The general idea is quite similar to the footnote example, but instead of popping up the node-specific editor when the user selects the node, it is always visible.
- The adaptor code in the node view gets a bit more involved, because we are translating between two different document concepts—ProseMirror's tree versus CodeMirror's plain text.
- When the code editor is focused, we can keep the selection of the outer editor synchronized with the inner one, so that any commands executed on the outer editor see an accurate selection.
- Selections are also synchronized the other way, from ProseMirror to CodeMirror, using the view's `setSelection` method.
- A somewhat tricky aspect of nesting editor like this is handling cursor motion across the edges of the inner editor. 
  - This node view will have to take care of allowing the user to move the selection out of the code editor. 
  - For that purpose, it binds the arrow keys to handlers that check if further motion would ‘escape’ the editor, and if so, return the selection and focus to the outer editor.

## [Linter](https://prosemirror.net/examples/lint/)

- A document model that represents a smaller set of documents can be easier to reason about.
- The first part of this example is a function that, given a document, produces an array of problems found in that document.
  - We'll use the `descendants` method to easily iterate over all nodes in a document. 
  - Depending on the type of node, different types of problems are checked for.
- Each problem is represented as an object with a message, a start, and an end, so that they can be displayed and highlighted. 
  - The objects may also optionally have a fix method, which can be called (passing the view) to fix the problem.
- The way the plugin will work is that it'll keep a set of decorations that highlight problems and inserts an icon next to them. 
  - CSS is used to position the icon on the right side of the editor, so that it doesn't interfere with the document flow.
- Recomputing the whole set of problems, and recreating the set of decorations, on every change isn't very efficient

## [Editing footnotes](https://prosemirror.net/examples/footnote/)

- Footnotes seem like they should be inline nodes with content—they appear in between other inline content, but their content isn't really part of the textblock around them. 
- **Inline nodes with content are not handled well by the library**, at least not by default. 
  - You are required to write a **node view** for them, which somehow manages the way they appear in the editor.
- Footnotes in this example are drawn as numbers.
  - we'll rely on CSS to add the numbers.
  - Only when the node view is selected does the user get to see and interact with its content 
- What we'll do is pop up a little sub-editor, which is itself a ProseMirror view, with the node's content.
  - Transactions in this sub-editor are handled specially, in the `dispatchInner` method.
- What should happen when the content of the sub-editor changes? 
  - We could just take its content and reset the content of the footnote in the outer document to it, but that wouldn't play well with the undo history or collaborative editing.
  - A nicer approach is to simply apply the steps from the inner editor, with an appropriate offset, to the outer document.
  - We have to be careful to handle appended transactions, and to be able to handle updates from the outside editor without creating an infinite loop

## [Tracking changes](https://prosemirror.net/examples/track/)

- The first thing we need is a way to track the commit history. 
  - An editor plugin works well for this, since it can observe changes as they come in. 

## [Collaborative editing](https://prosemirror.net/examples/collab/#edit-Example)

- The editor below talks to a simple server-side service to allow real-time collaborative editing.
- The demo also (crudely) shows how ProseMirror can be used to implement something like out-of-line annotations. 
