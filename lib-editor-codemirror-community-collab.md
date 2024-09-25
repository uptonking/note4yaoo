---
title: lib-editor-codemirror-community-collab
tags: [codemirror, collaboration, community]
created: 2024-05-02T05:50:24.220Z
modified: 2024-05-02T05:51:12.370Z
---

# lib-editor-codemirror-community-collab

# guide

# discuss-stars
- ## 

- ## 
# discuss-compatibility
- ## 

- ## [What is the browser undoing when the editor is unfocused? - v6 - discuss. CodeMirror _202207](https://discuss.codemirror.net/t/what-is-the-browser-undoing-when-the-editor-is-unfocused/4645)
  - What steps is the browser running through when the user presses Undo while the editor isn’t focused?

- Chrome (and possibly Safari? you didn’t mention what you’re testing with) has some weird page-global undo history concept, which as far as I know no one uses or expects, but that seems to be what’s kicking in here. 
  - Because focus isn’t on the editor, keys are handled by the native browser history feature, which then mutates the editor content. 
  - To make things worse, it inexplicably doesn’t fire a `beforeInput` the way it normally does for history actions, so I haven’t found a way for the library to recognize or capture these.

- ## 🤼 [More conventional undo behaviour? - v6 - discuss. CodeMirror _202301](https://discuss.codemirror.net/t/more-conventional-undo-behaviour/5565)
  - I noticed the undo behaviour is based on grouping events after an idle delay. For example if I start typing a lot of text (quickly), make a typo and press Ctrl+Z it will delete all of the text that I typed.
  - Other editors tend to make Ctrl+Z either delete one character at a time (for example this forum) or one word at a time (VS Code, Mousepad etc.). The former behaviour can be achieved in CodeMirror by setting `newGroupDelay` to a small value such as 50. But I was wondering if undoing by word is possible?
- I don’t think there is anything like a consensus on that. 
  - This forum seems to rely on the browser’s native behavior, which for (tried Firefox and Chrome Linux) seems to undo all text typed together in one go. 
  - Google Docs seems to use a similar system to CodeMirror.
  - Would an option that allows you to specify a function taking two changesets (the current history event and the new changes) and allows you to determine whether they should be combined work for you?
  - This patch adds such a configuration option `joinToEvent` .
- That approach sounds great. So I could choose not to combine if the user is adding whitespace to a non-whitespace string.

# discuss-undo/history
- ## 

- ## 

- ## 🤔 [How to detect whether an update comes from history - v6 - discuss. CodeMirror _ 202107](https://discuss.codemirror.net/t/how-to-detect-whether-an-update-comes-from-history/3393)
  - I am trying to integrate the CM6 history with an outer app undo stack.
  - For that purpose, I am looking for a way to detect whether a view update is coming from an undo/redo command.
- Not currently, but it would probably be a good idea to make the history annotate the transactions it produces. Would having a `userEvent` annotation for this be useful for you?
  - So the view would automatically set the userEvent to type "undo" or "redo", right? That would make a lot of sense, and solve the problem I am facing.

- I saw that this change landed in 0.19, so thanks a lot!
  - I wonder why you opted not to prefix the undo and redo events with history, so that we could more easily match using transaction.isUserEvent('history'). It works well as is, but a prefixed version would’ve been a bit more convenient.
  - I just saw that you also added select.undo and select.redo, which would explain why there’s no history. prefix.

- ## [An event emitted for undo. - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/an-event-emitted-for-undo/4753)
- You can check for transactions with an "undo" user event, but you can’t modify undo transactions, since that would break the history state.

- ## [Undo History for Widgets - v6 - discuss. CodeMirror _202105](https://discuss.codemirror.net/t/undo-history-for-widgets/3200)
  - I am building a rich-media code editor where users can insert images, video
  - I am trying to use CM6 to achieve this, via a StateField and StateEffects. 
  - To insert an image for example, I create a transaction with the appropriate StateEffect to create the image. This transaction also inserts a character at the location to insert the image. Then, I construct a replacement widget and replace the character I just inserted. This is done so that the cursor can correctly move around the image.
  - The problem I am having is integrating this with CM6’s undo history. I have tried using the invertedEffects facet to generate the appropriate inverse effect to add/remove the widget.
  - when the widget is deleted the user must press undo twice to recover the widget. Once to undo the deleted character and once again to undo the deleted widget.
- Effects and changes created by a single transaction should always be grouped together into the same history ‘event’. So this might be a bug. 

- ## [Problems with redoing an effect - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/problems-with-redoing-an-effect/5283)
- `invertedEffects` functions should be called for every transaction that doesn’t have `addToHistory` set to false. Maybe your effects being mapped to nothing by going through the change-invertedchange steps? 
  - I’d recommend using a transaction filter, rather than a separately created transaction that reverts the previous one, for this. 
  - Or, possibly even less problematic, don’t keep deleted text in the document, but store it alongside it and display it as widgets.

- ## [Serialize and save undo history? - discuss. CodeMirror](https://discuss.codemirror.net/t/serialize-and-save-undo-history/4254)
  - Has anyone had success serializing the undo and redo histories to save and load along with the document?
- Use the last argument to `EditorState.toJSON/fromJSON` , with a value like `{history: historyField}` .

- ## [How to undo on button press? - v6 - discuss. CodeMirror _202103](https://discuss.codemirror.net/t/how-to-undo-on-button-press/3034)

```JS
import { undo } from "@codemirror/history"

myButton.onmousedown = e => {
  undo(view)
  e.preventDefault()
}
```

- Uncaught RangeError: Trying to update state with a transaction that doesn't start from the previous state.
  - I’m not really sure why the error happend, but it seems it was due to Vue. EditorView was reactive, after I made it not reactive, everything worked again
- I got the same problem in vue, and finally solved it using `shallowRef`.

- ## [Detect history undo - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/detect-history-undo/7653)
  - Is it possible to detect wether an update was dispatched via undo (or redo)?
  - My use case: I want to react to document changes, but not if undo is dispatched.
- You can use `Transaction.isUserEvent` for this, passing "undo" or "redo".

```ts
const detectChangeWithoutUndoRedo = StateField.define<boolean>({
    create: (_state: EditorState) => false,
    update: (v: boolean, tr: Transaction) => {
        if (tr.docChanged && !tr.isUserEvent("undo") && !tr.isUserEvent("redo")) {
            console.log("changed");
        }
        return v;
    }
});
// use `detectChangeWithoutUndoRedo.extension`
```

- ## [Is there a way to customize the undo history list? - v6 - discuss. CodeMirror _202310](https://discuss.codemirror.net/t/is-there-a-way-to-customize-the-undo-history-list/7343)
  - I don’t want to add this insert operation to the undo history list. When using “Mod-z” for an undo operation, I want to skip this text insertion and directly return to an earlier historical state. What should I do?
- There’s an annotation you can add to transactions to get this effect.

- ## [Disable CTRL-Z (undo) for the very first change - v6 - discuss. CodeMirror _202203](https://discuss.codemirror.net/t/disable-ctrl-z-undo-for-the-very-first-change/4202)
  - The problem I have is that if a user presses CTRL-Z after the initial setting of the value, the whole content disappears. 
- If you create the new state with the content already in it, instead of firing a separate transaction that sets it, undo won’t delete it.
- You can also annotate your transaction with an `AddToHistory.of(false)` , can be any change.

- ## 💡 [editor.setHistory(), clearHistory() equivalent in Codemirror #6 - v6 - discuss. CodeMirror _202304](https://discuss.codemirror.net/t/editor-sethistory-clearhistory-equivalent-in-codemirror-6/6291)
  - each file has its own undo-redo history. We store history of each file by calling editor.getHistory() and storing in a Map. Whenever you switch the files, we load the history for that file and call editor.setHistory. This worked well in CM 5
  - in CM 6, the history API changed, and I’m not sure how to do it anymore. 
- Usually, in situations like this, you just want to store the entire editor state (either as a JS object, or, if you need to serialize it, via EditorState.toJSON) rather than storing the document and history separately.
  - You can’t clear history. Just create a new state. When creating a new state with fromJSON, you can provide your serialized history in the JSON object.

- https://x.com/puruvjdev/status/1780560310547436002  
  - Anytime you change documentId, it stores the state in a map, and when the documentID changes back to the one stored, we apply the history. It's quite neat
# discuss-crdt/yjs 🔀
- ## 

- ## 

- ## [How is UndoManager being used? - Yjs Community _202305](https://discuss.yjs.dev/t/how-is-undomanager-being-used/1851)
- We are using y-codemirror.next 5. We want each client to be able to undo only their own input. Is there a good way to add origin?
  - How to do each client to be able to undo only their own input. Still undoes another client’s changes also. I am wondering if YSyncConfig is the cause.
  - I had been using react-codemirror and it seemed to conflict with the history feature of react-codemirror, so I disabled the history feature of `react-codemirror` and used `Y.UndoManager` , so it worked as expected.

- ## 🔀 [CRDTs & Positions in CodeMirror 6 __202008](https://discuss.codemirror.net/t/crdts-positions-in-codemirror-6/2571)

- ProseMirror and CodeMirror 6 now both implement a similar approach for transforming positions. 
  - From a developer experience, this is great. This allows third-party plugins to provide features such as commenting on ranges of the document to unique map positions while accounting for remote changes.
- the current position mapping approach is unsuitable for yjs/CRDT-bindings to *Mirror editors. So third-party plugins won’t work with CRDT approaches to provide shared editing.

- I think there are several good arguments to reconsider using a CRDT for shared editing in CodeMirror.
  - Better position handling
  - The author of ShareJS and ShareDB openly speaks out against OT: https://news.ycombinator.com/item?id=24194091
  - The web has evolved to a point where web applications do work peer-to-peer over WebRTC. One of many real-world examples is room.sh 13. They use Yjs & CodeMirror 5 to provide collaboration in peer-to-peer WebRTC sessions.

- My goal is to power shared editing on the web with Yjs. Different editors can use the same technology to provide shared editing over different backends. 
- I think the Y. Text type would be a great data model for CodeMirror 6. 
  - If you are interested, I’d love to help you to integrate the Y. Text type into CodeMirror 6 and work with you on a better approach for position mapping. 
  - Another advantage of Yjs is that it supports selective Undo/Redo for free (no additional data structure to hold operations, just ranges on the vector clocks).
- Alternatively, it would be helpful if CodeMirror 6 would allow CRDT editor bindings to hijack position mappings. 
  - Although, as you explained, index positions don’t always accurately describe ranges in collaborative documents. 
  - With CRDTs, it is possible to refer to deleted characters. This is not possible if positions are described as index positions. With any change around the mapped position, some information gets lost. 
- Another alternative is to abstract positions in CodeMirror. 
  - A CRDT implementation could add markers to the abstract position to describe the position relative to the CRDT model without doing index transformations (i.e. map to the unique ID of the character).

- I just realized that the example in your blog post shows that positions in OT also don’t always converge. This was surprising to me. 
  - I’m currently educating people using y-prosemirror not to use the default position mapping because they don’t work in peer-to-peer scenarios. 
  - If this is the expected behavior for CodeMirror & ProseMirror, I can be more lenient(宽容的) to the fact they they also don’t converge with Yjs.
  - Although, I still think that in some cases this behavior is not acceptable. For example when implementing a shared-cursor plugin, or when implementing a commenting plugin.

- If it was possible to hijack the position mapping and provide a custom mapping based on the CRDT model, it would be possible to have positions converge.
  - If your input is still a plain (and thus ambiguous in the face of deletions) position, I don’t see how you can provide a better mapping. A position next to a deletion will correspond to multiple CRDT character IDs, and you don’t have information to disambiguate that.
- You are right… this wouldn’t work either. For the few cases when convergence is required I will provide a different position abstraction that doesn’t need to be native to CodeMirror. Thanks for your feedback.
# discuss-ot
- ## 

- ## 

- ## 
# discuss-user-cursor
- ## 

- ## 

- ## [How to show peers' cursors on CM6 collab editor? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-show-peers-cursors-on-cm6-collab-editor/3996)
- This isn’t a feature that any of the core modules provides—you’ll have to implement it yourself, by sharing the cursor positions over the network and displaying some widget or tooltip at those locations.

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 
