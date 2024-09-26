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

- ## 

- ## 🌰 [Example of onchange for CodeMirror6? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/example-of-onchange-for-codemirror6/3151)
- `let updateListenerExtension = EditorView.updateListener.of((update) => { if (update.docChanged) { // Handle the event here } });`

- 🌰 [CodeMirror 6: Proper way to listen for changes - discuss. CodeMirror](https://discuss.codemirror.net/t/codemirror-6-proper-way-to-listen-for-changes/2395)
  - See `EditorView.updateListener` for a shorthand way to do this.
  - You provide EditorView.updateListener.of(update => ...) as an extension, and your function gets called with a view update object every time the view is updated.
  - There’s only a single type of editor state update in version 6, so you use an `updateListener` and inspect the updates/transactions to see if they match the kind of change you are looking for (‘cursorActivity’ is roughly equivalent to update.docChanged || update.selectionSet).

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

- ## 🆚 [Difference between state field and facet? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/difference-between-state-field-and-facet/3650)
- How do you update the facet’s content? The way these are designed, fields are useful for independent bits of state, and facets are more applicable for derived state and inter-module communication.

# discuss-cm-nested/multi
- ## 

- ## [Problems when binding with codemirror6 - discuss. ProseMirror _202111](https://discuss.prosemirror.net/t/problems-when-binding-with-codemirror6/4214)
  - I am trying to bind codemirror6 to prosemirror and I’ve had some complicated problems

- Don’t use history stack of codemirror. So we can’t directly use @codemirror/basic-setup.
- When the content or selection of codemirror change, synchronize them to prosemirror. Check the forwardSelection and handleValueChange function.
- When execute redo or undo, the changes will synchronize to codemirror through the update method of CodemirrorView.
- When the codemirror lose focus, reset its selection to zero position.

- ## 🏠 [Partial views of documents - v6 - discuss. CodeMirror _202105](https://discuss.codemirror.net/t/partial-views-of-documents/3160)
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

- ## [Dispatch changes without redrawing the widget - v6 - discuss. CodeMirror _202304](https://discuss.codemirror.net/t/dispatch-changes-without-redrawing-the-widget/6320)
  - 3 levels of CM6 is working
  - a new instance of CM6 is embedded into replacing decoration.
  - How to mutate the data without recreating the widget?
  - Here one child editor mutate the data, which is covered by the replacement decoration (atomic). However, it causes each time dispatch, that destroys everything and creates again.
  - I was wondering, if there is a way to mutate the text underneath without redrawing, but just reassigning the widget range to a new one (if a new text is larger or shorter).
- `updateDOM` should be called if a widget of the same type (but non-eq) appears in the same position in the document

- [Remove blinking cursor inside the widget with CM instance - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/remove-blinking-cursor-inside-the-widget-with-cm-instance/6284)

- ## 🌰 [Strange cursor behavior when nesting editors - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/strange-cursor-behavior-when-nesting-editors/7101)
- I found this behavior to be due to bad CSS settings for the Dom in the widget, so it’s an oops. I’m sorry if this wasted your time.

# discuss-switch-files
- ## 

- ## [Cursor isn't behaving when saving and reloading states - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/cursor-isnt-behaving-when-saving-and-reloading-states/3913)
- Doing preventDefault will cause the editor to not further handle the event. It doesn’t look at stopPropagation.

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

- ## 💡 [swapDoc v6 equivalent - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/swapdoc-v6-equivalent/5973)
- Store the editor states of the docs not in the view, and use `setState` to put a new state into an editor view.

# discuss-transaction
- ## 

- ## [How to Compress transactions - discuss. CodeMirror _202409](https://discuss.codemirror.net/t/how-to-compress-transactions/8624)
  - I’m using the collab feature from CodeMirror and I’m saving the transactions in one of my DBs. I’m running into an issue where the amount of data being read and stored into my DB is excessive and I’m trying to see how to cut back. 
  - One thing I thought of instantly is that there should be a way to compress the transactions. 
  - Another idea I had was to have a way to eliminate non-critical transactions from the array list like cursor transactions. Or even is there a way to easily take an array of transactions and say that we want to combine the first 100 transactions into a single transaction? I’m also open to any other way to make the whole system more efficient/compressed.

- What you need to save depends entirely on what you are doing with the data. If you want collab clients to be able to re-sync from any point in history, you do need precise changes since the point where they last synced. 
  - But it is entirely reasonable to disallow that for old points in history, and keep less fine-grained information (or no information at all) for older updates.
  - Changesets can be combined with `compose` , if you want to reduce the number of checkpoints you save.
- I see, you’re storing a shared effect to track remote selections, and then just directly dumping the JSON (which adds the useless `{"type":{"map":{}}` property to the output, since StateEffect objects don’t implement a toJSON method) and, I guess, using a custom deserializer to parse that back to an effect.
  - So I guess you can already cut down on JSON size by being more careful about how you serialize these objects.

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

- ## 🏠 [Codemirror 6: reference to EditorView from EditorState - discuss. CodeMirror](https://discuss.codemirror.net/t/codemirror-6-reference-to-editorview-from-editorstate/2554)
- This might work better at a level above the view/state, since it needs to orchestrate between multiple views.
  - The editor state intentionally lives in its own ‘world’, away from the view, so there is no function that takes a state and returns a view. 
  - But you can pass in something like a view getter function when creating a state, and arrange things so that that gets access to the view when one has been created.
- I figured out how to give the state a facet that I can populate with a reference to the view. This seems to be working so far.

- ## [line background layer - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/line-background-layer/7666)
- It looks like the newlines are not part of the LineBlock items returned by view.viewportLineBlocks. I’ve verified that by looking at view.state.doc.toString().slice(block.from, block.to)

# discuss-readonly
- ## 

- ## 

- ## [Switch between editor being editable or not - v6 ](https://discuss.codemirror.net/t/switch-between-editor-being-editable-or-not/2745)
- reuse the Compartment instance to alter the editable state
  - Looking more into Configuration example

- [Implement some kind of read-only mode ](https://github.com/codemirror/dev/issues/173)
  - By default, if the editor isn't focusable, it also won't receive key events, so you can't ctrl-v on it. But I guess if you add a `tabindex` attribute to make it focusable you will have key bindings firing on the editor.
  - Since @codemirror/state 0.19.2, there's also a `readOnly` facet, on the state, which controls whether the content is supposed to be read-only (and is respected by commands and such). This is separate from the editable facet, which only controls whether the DOM for the content is focusable/editable.

- ## [How to make certain ranges readonly in CodeMirror6 - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-make-certain-ranges-readonly-in-codemirror6/3400)
  - I just released codemirror-readonly-ranges extension that easy allow to work with read-only ranges on CodeMirror6.

- The recommended way to do this is to create a transaction filter that stops transactions which affect those ranges.
- don’t use undocumented properties like RangeSet.chunk, those may break on any release. Also, you’ll want to use a consistent coordinate system, so using the read-only ranges from tr.startState and the original-document coordinates in the change set seems safer. 

- ## 🧩 [Read-only Facets? - discuss. CodeMirror _202310](https://discuss.codemirror.net/t/read-only-facets/7175)
  - Somewhere else in the codebase I want to read the value of MySpecialNumber. But I don’t want anywhere else in the codebase to register MySpecialNumber.of(...). Its value should be defined internally in this module only.
  - Perhaps like a wrapper class
- There is also the use case of values which are just derived from something else

- Regarding computed values, given that defining an extra facet for them already allows you to do that, I don’t think that really warrants another library feature.
  - As for facet handles that don’t allow you to set the facet, this patch adds something like that purely on the type level. Introduce `FacetReader`
