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

- ## 

- ## 🏘️🤔 [Request: View plugin method that runs at the same phase as update listeners - v6 - discuss. CodeMirror _202404](https://discuss.codemirror.net/t/request-view-plugin-method-that-runs-at-the-same-phase-as-update-listeners/8113)
  - At Replit, we have this pattern which is used in a lot of our plugins
  - postUpdate is helpful in a lot of situations. It enables you to make update listeners that have internal state, without using something like closures.
  - For us, it’s often needed because an extension needs to manage some part of the editor’s state, but that management logic just can’t go into something like a StateField.
  - This is our most common use case, e.g. our inline AI suggestions use this. Most of the suggestion state is in a StateField, but most of the logic for updating that field lives in a view plugin because that’s the only reasonable place to do asynchronous requests.
  - Another use case for us is updating things outside the editor, which then may have reactive effects which cause editor dispatches. It is desirable to avoid this entirely, but for our React-inside-of-CodeMirror library, we definitely needs this, or at least workarounds similar to this.
  - We could do something like `queueMicrotask(() => view.dispatch({ ... })` instead of using an update listener, but this has issues with making view updates sort of slightly asynchronous. 
  - if you called view.dispatch, and then immediately accessed view.state afterwards, that state won’t yet reflect anything queued up by queueMicrotask yet. 
  - Using update listeners avoids this, by basically letting a single dispatch turn into multiple dispatches.
  - So, our request here is pretty simple: add a method very similar to update that runs after update and only when it is safe to do dispatches to the view, just like update listeners. The only real drawback I can think of to adding this method is maybe confusion about what method to use when learning the API, and the possibility of infinite update loops. The latter is already possible with update listeners, so IMO it’s fine.

- In my own code I’ve been pretty successful at avoiding this pattern where a dispatch immediately triggers another dispatch. 
  - Cascading updates are a bit wasteful, in that they run through the view update logic multiple times for what should be an atomic update. 
  - You can often set things up so that the state update plans the asynchronous actions, and a plugin update method actually activates/schedules them, without updating the state. 
  - Or in some cases you can dispatch multiple transaction at once by passing them to dispatch as an array.
  - Note that even though the code after the dispatch would see the updated state if you had this feature, the update listeners or postUpdate hooks will have situations where the update they are looking at is not actually the most recent update anymore, because another such listener dispatched a transaction. I sort of feel that doing this kind of cascading dispatch asynchronously might be less error-prone than doing it synchronously.

- You can usually avoid it, and you should if you can. But it’s still useful for us. It feels like a missing lifecycle method with view plugins. I will say not every use case we have for this is just about dispatching.

- 
- 
- 
- 

- ## [Filtering input characters - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/filtering-input-characters/3968)
  - For legacy reasons, our OT algorithm doesn’t support characters outside the Basic Multilingual Plane (BMP) 
  - We plan to fix this limitation in the future, but this would require significant work. 
  - For now, we would like to migrate across our existing solution which replaces such characters with another dummy character.
  - It seems like a transactionFilter is the right tool for this and I’ve attempted it in this codesandbox. The replacement works as expected but it inserts in reverse and I’m not sure why.

- This approach where you replace all local transactions with a fresh one that has similar changes will strip all effects and annotations from the transactions, so that is probably not going to work (it’ll mess up the undo history, for example).
  - But I think the problem here is that the changes are all interpreted in the original document’s coordinate system. 
  - A filter that adds the the existing transaction by appending a change that deletes the astral characters, using sequential so that its coordinates are interpreted in the in-between coordinate system, might work (return [tr, {changes: ..., sequential: true}]).

- ## 🌰 [how to get selected content in v6 _202208](https://discuss.codemirror.net/t/how-to-get-selected-content-in-v6/4888)

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

# discuss-cm-nested/multi
- ## 

- ## 

- ## [Partial views of documents - v6 - discuss. CodeMirror _202105](https://discuss.codemirror.net/t/partial-views-of-documents/3160)
  - In codemirror 5 you can use `linkedDoc` to link two documents together so that changes to one document are reflected in the linked document automatically. 
  - Is there a way to achieve this behaviour in codemirror 6?
- I haven’t concretely tried something like that, but the idea would be to do it very differently from the CM5 approach. 
  - The split view example already points in the right direction. 
  - To provide only a subview of a document, you’d have to filter the changes so that only the parts that apply to the sub-range are applied to that view. In the process, you’d have to adjust your information about the line number where the subview starts, when the changes affect that. 
  - Actually changing the numbering of lines in a document isn’t going to be supported, but you can configure the line number gutter to show different numbers via the formatNumber option, and you could reconfigure that when the base number changes.

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

# discuss-switch-files
- ## 

- ## 

- ## [Programmatically clear the content? - v6 - discuss. CodeMirror _202202](https://discuss.codemirror.net/t/programmatically-clear-the-content/3967)
- You should usually just create a new state and use setState to reset the view to that. 
  - But if you really want to replace the content, keeping the old undo history and such intact, pass `{from: 0, to: editorView.current.state.doc.length, insert: value}` under changes.

- ## [Preserving state when switching between files - v6 - discuss. CodeMirror _202102](https://discuss.codemirror.net/t/preserving-state-when-switching-between-files/2946)
  - I’m trying to find the best way to switch between files so that changes and undo history are preserved. The goal is to emulate what you would expect form a traditional editor.
  - My initial approach was to reuse the same EditorView instance and keep and EditorState map in memory for each file and call view.setState(fileStateMap[filename]) when the file is changed. But it looks like setState resets the state itself.
  - Another approach could be to create an EditorView instance for each file and attach/detach to the DOM when the file is changed. Not sure how this would scale if many files are opened.
  - Another approach is to store the text content and the history extension in a map for each file and dispatch a ReconfigurationSpec with a tagged history extensions and changes to replace the text content.
  - Is there a “right” approach here or is there another approach that I’m missing?
- The technique of keeping a state per ‘buffer’ is how I’d approach this myself.

- ## 💡 [Document Changes in CM6 - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/document-changes-in-cm6/3284)
  - I want to replace all the code that is in the editor with another code. What is the best way to do this in CM6? 
- The recommended way to do this is to create a completely new state and call `setState` on the view.
  - If you’re moving to a new document that has nothing to do with the old, definitely do use `setState` . 
  - If you are just making changes to the existing document, `dispatch` transactions that make those changes.
- why not use dispatch to replace the entire content
  - Do keep in mind that that’ll mess up the undo history and any other metadata that’s being kept about the document content (marks, mapped positions). If practical, you could compute a minimal diff and just update the changed ranges.

# discuss-transaction
- ## 

- ## 

- ## [Keep original's annotation to an updated transaction - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/keep-originals-annotation-to-an-updated-transaction/4218)
  - How can I update a transaction keeping its annotation’s origin value?
  - How can I detect the current transaction’s annotation? 

- I just realized that if I use annotations:` Transaction.userEvent.of('delete.selection')` it works.

- You can’t copy all annotations when replacing a selection, currently. But I think that actually is a reasonable thing, since doing that wouldn’t be safe anyway (for example, the transactions created by undo/redo will include a new undo history object in an annotation, which would not be valid for a transaction that has different changes). 
  - You may be able to do what you’re trying to do with a change filter, or just add only userEvent and hope you’re not dropping any important annotations.
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
