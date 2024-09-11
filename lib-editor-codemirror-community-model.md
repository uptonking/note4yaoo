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

- ## 

- ## [Nested editors, kind of. - v6 - discuss. CodeMirror _202207](https://discuss.codemirror.net/t/nested-editors-kind-of/4654)
- This should be possible (if somewhat messy) using a technique similar to the split view example. But you’ll have to offset your change sets by the current position of the sub-document when forwarding them between the cell editors and the main editor (which should be possible by iterating over them with iterChanges and building up a new changeset with the same insertions but offset position).

- ## [Syntax Highlighting inside widget decoration - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/syntax-highlighting-inside-widget-decoration/6160)
- Is it possible to apply syntax highlighting inside the widget’s content?
  - Not directly using the editor’s syntax highlighting. Though I guess you could run `highlightTree` on the subtree for the text inside the widget, feeding it the same highlighters that your editor uses, and then construct the highlighted DOM directly and put that in the widget.
- You could apply marker widgets to the content you want to alter, and put empty replace widgets on the stuff you want to hide, skiping the whole need to redecorate it inside a new widget.

- To fully support the recursion for widgets I was thinking, would it be a bad idea to start a separate instances of CM6 view inside the widget? For example of I have a widget of a matrix, where each cell is a separate CM6 editor. Then I can make matrixes inside matrixes and so one. I tried, not too bad I would say

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

- ## 

- ## 

- ## [Custom gutter for specific lines only? - discuss. CodeMirror](https://discuss.codemirror.net/t/custom-gutter-for-specific-lines-only/5530)
- you really don’t want to be doing that much work in formatNumber (or lineMarker, for that matter). 
  - The best approach here would probably be to not use lineNumbers at all, but create a custom gutter, with markers only at the lines where you need them, and only recompute them when necessary.

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
