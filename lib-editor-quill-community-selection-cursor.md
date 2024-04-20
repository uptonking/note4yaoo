---
title: lib-editor-quill-community-selection-cursor
tags: [community, cursor, quill, selection]
created: 2024-04-15T15:55:12.944Z
modified: 2024-04-15T15:55:29.732Z
---

# lib-editor-quill-community-selection-cursor

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## [quill.getSelection() doesn't always return correct current position when called in text-change handler _201606](https://github.com/quilljs/quill/issues/763)
- The issue is the cursor is not yet synced. For some text changes an external function is saving and restoring the cursor position, in this case the keyboard module. Using _.defer (if using lodash or underscore) or a setTimeout of 1 in your handler should fix this.

- What are you using the cursor location for in the text-change handler? The challenge is some text changes will incorrectly move the cursor or lose it completely in some browsers so it is sometimes saved and restored before making changes. The text-change event fires before this restore step.

- ## [Off-by-one error in selection index _201710](https://github.com/quilljs/quill/issues/1763)
- The editor-change event is just a combination of text and selection change. So what is meant by "Use selection-change or editor-change for reliable selection updates" is that you should look at the selection-change events inside of editor-change. It does not change text-change's behavior.
  - The simple workaround is wrap your handler with a setTimeout or _.defer.

- Do you think it would be possible to change the lifecycle
  - Text changes can cause selection changes so it would make sense for it to get fired first. Quill has a modular architecture so the selection and editor modules has limited control over one another

- ## [Inconsistent selection after insert between browsers _201609](https://github.com/quilljs/quill/issues/1007)
- 💡 When a DOM node that the selection is in is modified, browsers are unpredictable in what they do. So Quill calculates what the selection should be and restores it. The problem it seems it this restoration happens after the `text-change` event is emitted. So the workaround at the moment is to set a `timeout` or defer in the `text-change` handler before querying the selection.

- ## [Method setSelection not working after user input _201801](https://github.com/quilljs/quill/issues/1908)
- The workaround I have discovered is to wrap setSelection call into a setTimeout with a timeout of 0: `setTimeout(() => quill.setSelection(2, 5), 0)`

- ## [Selection change not triggered when focus changed to button _201704](https://github.com/quilljs/quill/issues/1397)
- This is happening because replaced elements can't have selection. So `selectionchange` isn't going to fire, and Quill doesn't know that the editor doesn't have focus anymore since that's how it checks.
  - This fiddle compares focus/blur event listeners with selectionchange listeners. 
  - Since focus state can change independently from selection state, it looks like there's no way around it - Quill might have to add listeners for `blur` or `focusout` to fix this.
  - the work-around for this is: `quill.root.addEventListener('blur', e => quill.setSelection(null));`

- ## [Setting the cursor position after setting a new delta in Quill - Stack Overflow](https://stackoverflow.com/questions/48678236/setting-the-cursor-position-after-setting-a-new-delta-in-quill)
- I recommend using quill.updateContents() and constructing a new Delta as opposed to using quill.getContents() and quill.setContents().

- ## [Cursor position is reset after calling setContents(delta) _201805](https://github.com/quilljs/quill/issues/2106)
- You have to either restore the cursor position programmatically, or use `updateContents()` , I end up switching to `updateContents()` .
