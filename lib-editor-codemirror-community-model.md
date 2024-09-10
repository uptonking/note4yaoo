---
title: lib-editor-codemirror-community-model
tags: [codemirror, data-model, editor]
created: 2024-08-11T03:29:01.246Z
modified: 2024-08-11T03:29:17.282Z
---

# lib-editor-codemirror-community-model

# guide

# discuss-stars
- ## 

- ## [how to get selected content in v6](https://discuss.codemirror.net/t/how-to-get-selected-content-in-v6/4888)

```JS
view.state.sliceDoc(v.state.selection.main.from, v.state.selection.main.to)

// How to get all the content of the selected line and replace it no matter where the cursor is in the line
// Exchange `from` with `to`, `anchor`, or `head`, depending on your needs
const line = view.state.doc.lineAt(view.state.selection.main.from)
// Get line contents
const lineContents = view.state.sliceDoc(line.from, line.to)
// Exchange line contents
view.dispatch({ changes: { from: line.from, to: line.to, insert: 'New text for the line' } })
```

- ## [Updating block-widgets // What is the order of the state update cycle, exactly? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/updating-block-widgets-what-is-the-order-of-the-state-update-cycle-exactly/8365)
- I suspect, from your message, that you’re mutating your decorations, and expecting the method to run then? That’s not how these work—they are immutable like everything else you store in your state. You replace them with a widget of the same type to have updateDOM called.

- 
- 

# discuss-cm-nested/multi
- ## 

- ## 

- ## [Dispatch changes without redrawing the widget - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/dispatch-changes-without-redrawing-the-widget/6320)
  - 3 levels of CM6 is working
- updateDOM should be called if a widget of the same type (but non-eq) appears in the same position in the document

- [Remove blinking cursor inside the widget with CM instance - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/remove-blinking-cursor-inside-the-widget-with-cm-instance/6284)

- ## 🌰 [Strange cursor behavior when nesting editors - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/strange-cursor-behavior-when-nesting-editors/7101)
- I found this behavior to be due to bad CSS settings for the Dom in the widget, so it’s an oops. I’m sorry if this wasted your time.

# discuss-transaction
- ## 

- ## 

- ## 
# discuss-state-field
- ## 

- ## 

- ## [Using `EditorView.scrollIntoView` in `transactionExtender` breaks `StateField` updates - discuss. CodeMirror](https://discuss.codemirror.net/t/using-editorview-scrollintoview-in-transactionextender-breaks-statefield-updates/7476)
- Editor states, including any values attached to them, should be immutable.

# discuss-gutter/line-number
- ## 

- ## 💡 [Line number height problem. - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/line-number-height-problem/6146)
- Try calling requestMeasure on your editor when the animation that pops it up finishes should help.

- ## [Line number after wrapping - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/line-number-after-wrapping/7779)
- Is there a way I could determine the visual line number after wrapping 
  - No. Use direct screen coordinates for that kind of thing.
- I’m trying to generate the tooltips in the update function of a StateField based on the current selection. Is it reasonable to read screen coordinates from the view there?
  - No. But you can’t know about line wrapping there in general, since that happens on the view level.

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [line background layer - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/line-background-layer/7666)
- It looks like the newlines are not part of the LineBlock items returned by view.viewportLineBlocks. I’ve verified that by looking at view.state.doc.toString().slice(block.from, block.to)
