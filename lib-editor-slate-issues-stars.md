---
title: lib-editor-slate-issues-stars
tags: [issues, slate]
created: '2022-05-15T18:48:42.427Z'
modified: '2022-05-15T18:48:53.816Z'
---

# lib-editor-slate-issues-stars

# guide

# faq

## [onKeyDown not fired for editable elements nested inside non-editables](https://github.com/ianstormtaylor/slate/issues/468)

- [Keydown event on contenteditable div and child span](https://stackoverflow.com/questions/22895124)
  - I have a contenteditable div containing a span and would like to trace the keydown events when typing in both the div itself and the span within the div.
  - Everything seems to work fine so far in firefox but in webkit browsers the div keydown event seems to override the span event. 
- it seems to happen because it is the div element that catches the keydown events, not the inner span elements. To make them catch the keydown events, you would need to set contenteditable=true for each of them while setting contenteditable=false for the div container.
  - To make both the div container AND the inner span catch the keydown events, you can wrap your span in a non-editable span

- [Focusing on nested contenteditable element](https://stackoverflow.com/questions/40907091)
  - I have two contenteditable divs nested inside of another. When it is focused, nested should be focused but using console.log(document.activeElement); it shows that the top is focused and it doesn't recognize the nested div.
- 👀 The way [contenteditable] elements are handled by browser made any nested [contenteditable] not handling any event, the editing host is the former editable parent. See spec:
  - If an element is editable and its parent element is not, or if an element is editable and it has no parent element, then the element is an editing host. Editable elements can be nested. User agents must make editing hosts focusable (which typically means they enter the tab order). An editing host can contain non-editable sections, these are handled as described below. An editing host can contain non-editable sections that contain further editing hosts.
- Now as a workaround, you could make focused nested editable element the hosting host by setting any of its editable parent temporarily not editable
- Give `tabindex=-1` to the nested div, than can be focused
  - 👀 `contenteditable` is inherited, so there is no need to specify it again.
  - it only works with mouse focus. Moving the caret (cursor left/right) over the nested div, will not focus the nested div. Similarly, leaving a focused nested div with the caret, will not does not give the focus back to the parent div. Handling might need workarounds with keydown listener, range and selection.

## [What is the purpose of onDOMBeforeInput?](https://github.com/ianstormtaylor/slate/issues/3302)

- It's an event handler for the native DOM `beforeinput` event, because sadly React's synthetic events don't properly expose it. 
  - In this case it's listening for specific inputTypes that browsers fire for context menus, etc.

## [Only use Slate Provider's value prop as initial state](https://github.com/ianstormtaylor/slate/pull/4540)

- The value prop is now only used on the initial render to initialize the value prop. On subsequent changes it is ignored.
- slate used to offer an API similar to any generic input, whereby it exposed props such as value and onChange. This enabled users to interact and maintain the value of the input with a useState hook

## [onDocumentChange and onSelectionChange](https://github.com/ianstormtaylor/slate/issues/4687)

- Currently the onChange event of slate is fired for changes on the document structure but also for changes on the selection. 
- you can distinguish in the onChange event like:
  - if (editor.operations.every(op => op.type === "set_selection"))

## [Why is content pasted as plain text?](https://docs.slatejs.org/general/faq)

- One of Slate's core principles is that, unlike most other editors, it does not prescribe a specific "schema" to the content you are editing.
  - For the most part, this leads to increased flexibility without many downsides, but there are certain cases where you have to do a bit more work. Pasting is one of those cases.
  - Since Slate knows nothing about your domain, it can't know how to parse pasted HTML content (or other content). So, by default whenever a user pastes content into a Slate editor, it will parse it as plain text. 
  - If you want it to be smarter about pasted content, you need to override the insert_data command and deserialize the `DataTransfer` object's `text/html` data as you wish.
