---
title: lib-editor-codemirror-community-collab
tags: [codemirror, collaboration, community]
created: 2024-05-02T05:50:24.220Z
modified: 2024-05-02T05:51:12.370Z
---

# lib-editor-codemirror-community-collab

# guide

- tips
  - 与外部系统集成undo/collab可参考 yjs, prosemirror-codemirror
# discuss-stars
- ## 

- ## 

- ## 

- ## [integrating CodeMirror history with app-wide history - discuss. CodeMirror _201509](https://discuss.codemirror.net/t/integrating-codemirror-history-with-app-wide-history/465)
  - I want to use a CodeMirror editor as a component in a larger web app, where the user can do actions that CodeMirror doesn’t know about. What is the best way to have undo/redo work in a way that makes the CodeMirror/non-CodeMirror distinction invisible to the user?
  - My first thought was to manage all history in a model I would maintain outside of CodeMirror and just use CodeMirror as much as a kind of view layer. But as I started to implement this, I felt that CodeMirror really wants to be top dog, and I was making things harder for myself by fighting that.

- 👷 There is no convenient functionality for this, but you might be able to override the "undo" and "redo" commands, wrapping them with your own history functionality, and falling through to the default implementation when appropriate. Something like this

```JS
const original = CodeMirror.commands.undo

CodeMirror.commands.undo = function(cm) {
  if (myOwnEventOnTop())
    undoOwnEvent()
  else
    original(cm)
}
```

- ## [Is dirty flag available in codemirror? - discuss. CodeMirror](https://discuss.codemirror.net/t/is-dirty-flag-available-in-codemirror/2716)
- is there something similar in v6?
  - No, but documents are structure-sharing persistent values, and comparing them is optimized to make use of this, 
  - so if you just want to check whether a the current document is the same as some previous one, keep a reference to that previous `state.doc` , and compare with `cleanDoc.eq(state.doc)` later.

- ## ⏳ [Recording and replaying code changes. - v6 - discuss. CodeMirror _202109](https://discuss.codemirror.net/t/recording-and-replaying-code-changes/3502)
  - I am trying to figure out how can record and replay an array of ChangeSet
- you can use change sets to move forward and backward through history like this. The error you’re getting happens when you somehow try to apply a changeset to a document that doesn’t match the document it was created for (in length), which suggests some issue in your implementation.

- ## 💡 [Reconfigure doesn't re-run `StateField` 's `create` - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/reconfigure-doesnt-re-run-statefield-s-create/8548)
  - “state field create” is only printed once, and “state field recreate” is never printed, even though the reconfigure effect is being dispatched.

- I am still curious if excluding StateField create from reconfiguration is intended.
  - Yes. Reconfiguring the editor preserves the value of state fields that are present in both the old and new configuration (so that you don’t, say, lose your undo history every time you reconfigure something).

- ## 🌰 [CodeMirror 6: How to set up collaborative editing with clients and server? - discuss. CodeMirror _202008](https://discuss.codemirror.net/t/codemirror-6-how-to-set-up-collaborative-editing-with-clients-and-server/2583)
  - In the end I sidestepped the collab extension, and used a system similar to the split view example (except sending the ChangeSets over the network), using the map function on the ChangeSets as necessary and using the EditorView.dispatch() function to apply the change sets.

- I think I have the collab module working. Here’s some (partial) example code and some refelections.
  - Overall the collab module is very helpful. It’s awesome that undo just works, for example!
  - Update: After some more testing, it turns out that the above approach is not sound, because our OT and CodeMirror’s OT resolve at least one class of conflicts differently.

- I think if you’re not going to use the OT built into ChangeSet, you will indeed have a hard time using the collab module, and setting up something separate is the way to go, yes.
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

# discuss-changeset
- ## 

- ## 

- ## 🌰 [debouncing / merging docChanged transactions? - discuss. CodeMirror](https://discuss.codemirror.net/t/debouncing-merging-docchanged-transactions/8268)
- You cannot merge transactions, but you can merge change set with `ChangeSet.compose` . You could set up a thing that accumulates changes and runs some code on the result only after a given period of inactivity.
- My “solution” was to have a debounce listener on document changes and just literally diff the document with its previous version. That’s probably a really bad plan for huge documents, but for my use-case it works quite well
  - with `createPatch` being the standard “get me the diff between these two strings” that you can find loads of libraries for

- ## [CodeMirror Empty Changes Array - discuss. CodeMirror _202403](https://discuss.codemirror.net/t/codemirror-empty-changes-array/7980)
  - `{"clientID":"CLIENT_ID","changes":[],"effects":[{"type":{"map":{}},"value":{"id":"FIRST_ID","from":0,"to":0}}]}`

- Assuming these are the JSON representation of `ChangeSet` objects, the empty array represents no changes made to a zero-length document, and as such wouldn’t be valid for applying to a non-empty document. The numbers in these arrays encode changed and unchanged pieces of the document, and are not something you want to manipulate or read directly in your code.

- ## [Iterators can be hard to work with for beginners - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/iterators-can-be-hard-to-work-with-for-beginners/3533)
- TextIterators are CM6 iterators. It’s just that Array.from takes an iterable, not an iterator, which is a little awkward. This patch fixes that.
  - The RangeCursor docs say right there that this isn’t an ES6 iterator. For practical reasons, those don’t have a non-started state and don’t conform to the ES6 protocols.
- Does `ChangeSet.iterChanges()` iterate through changes in order from the start of the document til the end? From the implementation it looks like the order is based on the ordering of `ChangeDesc.section` , but I can’t tell what ordering is preserved there.
  - Yes, change sets are ordered by document position.

- ## [How can I get Position from Document before the change? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-can-i-get-position-from-document-before-the-change/7226)
- If you have the transaction, its `changes` property gives you precisely this. If you don’t, then no, there’s no concept of a ‘last document’.
- `ViewUpdate.transactions` may be empty. It may also hold more than one transaction. So loop over them or use `ViewUpdate.changes` , which combines them into a single changeset.

- ## [Specification for serialised changset? - v6 - discuss. CodeMirror _202402](https://discuss.codemirror.net/t/specification-for-serialised-changset/7827)
  - I’m currently sending only the serialised changes to the server using something along the lines of: `EditorView.updateListener.of((e) => send("update", e.changes.toJSON()))` .
  - I need to implement the application on the server (not js/ts, elixir). But I couldn’t find documentation for the format. The common [insertion, [removal, new_string]] is sorta obvious
  - The tests use a format like over("2 2:2 2", "0:2 6", "4 2:2 2") and I’m not quite sure how they relate to one another.

- There’s no specification for these, but they won’t change, because that would break things for people. 
  - The elements in the array represent sections of the old document. 
  - Plain numbers are unchanged ranges. Arrays are replacements, where the number at the start of the array is the amount of deleted text, and the strings following that is the inserted text, split by line. 
  - So [0, "", ""] inserts a line break, [1] deletes a character, etc.
  - `[5, [0, "new "], 7]` is a change that, inserts “new ” at position 5 in a length-12 document. “skip 5, replace 0 with the string ‘new’, skip 7”. If the change is at the very end of the document, the skip at the end will not be there.
- While most editing changes will, obviously, make only a single modification to the document. it’s not hard to create a transaction that makes several changes.
# discuss-undo/history
- ## 

- ## 

- ## [Best way to manage 'doc-has-changed' status - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/best-way-to-manage-doc-has-changed-status/6557)
  - sing code mirror for a text editor. When loading the editor content from a file, I want to display if the editor text has been changed or is still/again the same as the file content
  - Broadly having 2 approaches in mind:
  - (1) Create a checksum of the files content when loading and on update.docChanged calculate a new one and see if they differ
  - (2) Use the change descriptions / history structure
  - (1) should be doable, just worry about the performance/extra load.
  - For (2) haven’t found an exact way yet. Looked at the serializable history field which I extract anyway, but don’t see an obvious way to reuse (also since a save shouldn’t wipe out history).

- Store `state.doc` for the version you are interested in, and do `baseDoc.eq(state.doc)` at any time to see if the given state has the same document.

- Thanks, that works! However since I’m having potentially a lot of open/modified documents and don’t want to keep a lot of copies I decided for the following: 
  - When loading from file, track its amount of characters and a md5 
  - on changes compare for the amount of characters and if those are equal tale another md5 and compare it with the baseline

- ## [Listen for new history state? - v6 - discuss. CodeMirror _202212](https://discuss.codemirror.net/t/listen-for-new-history-state/5468)
  - I would like to be notified when a new history state is generated. For example, when I type “Hello world!” I would like to be notified just once; whereas, when I type “Hello” (wait a couple of second) “world!”, I would like to be notified two times, one after “Hello” and one at the end. Is there a proper way to listen for that?
  - I need this feature to stay synced with the Visual Studio Code History API. I’m trying to publish a Visual Studio Code extension on a project based on Codemirror6, and it’s way easier to handle the history from Codemirror6 and just notify Visual Studio when a new state is available.

- This doesn’t exist, and would be difficult to provide in the form you describe, since whether new changes are included in the same event is determined only when the new change comes in, so an event is only really ‘closed’ when a new event is started.
  - I came to the same conclusion, however I managed to find a solution by relaxing the problem: I realized I do not need to know the history state content, but just when a new state is created.

- ## 🤔 [Restoring history without blowing up extensions state - v6 - discuss. CodeMirror _202306](https://discuss.codemirror.net/t/restoring-history-without-blowing-up-extensions-state/6712)
  - When switching from one tab to another i keep track of the EditorState inside a map and i restore that state whenever the user switch again to that tab. This is to keep the history related to a specific tab.
  - However if i set the new state without reconfiguring the extensions every extension is removed.
  - But reconfiguring the extensions also means that every state associated with a specific extension is lost. 
  - The example i proposed is the best one. The vim plugin stores the mode (either normal, insert or visual) and that get’s reset whenever we reset the state on tab switch.

- Do you need to serialize the state in order to put it on the server? If not, just don’t do the fromJSON/toJSON stuff. If you do, you’re responsible for adding back the extensions when calling `EditorState.fromJSON`, and for extensions that don’t support serialization of their state you will indeed lose the state.

- i think i found what the problem is…the package we are using seems to not store the state for the Extension in a facet (and hence in the codemirror state). 

- ## 💡 [Import / Export Transaction History - v6 - discuss. CodeMirror _202308](https://discuss.codemirror.net/t/import-export-transaction-history/7041)
  - Is there a way to export the transaction history / import it again?
- The library itself doesn’t keep a transaction history, so you’ll have to arrange that yourself. 
  - Also, there’s no way to serialize annotations and effects, so you can only store part of it (document and selection changes).

- ## [Cannot get history depth and serialized historyField - v6 - discuss. CodeMirror _202301](https://discuss.codemirror.net/t/cannot-get-history-depth-and-serialized-historyfield/5597)
  - I’m trying to serialize historyField in update method of ViewPlugin class
- The problem was that history methods were imported from @codemirror/history, which is deprecated package that comes from @emmetio/codemirror6-plugin dependencies.
  - this package is deprecated and would conflict with @codemirror/commands imports (where all the history related stuff should be actually imported from).

- `undoDepth` gives you the amount of undoable edits in the state. So after some changes have been made, it will yield a non-zero value.
  - undoDepth is tested in the test suite and known to work. If it’s returning 0 for your state, I suspect that state has no undo events.

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

- ## [Problems with redoing an effect - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/problems-with-redoing-an-effect/5283)
- `invertedEffects` functions should be called for every transaction that doesn’t have `addToHistory` set to false. Maybe your effects being mapped to nothing by going through the change-invertedchange steps? 
  - I’d recommend using a transaction filter, rather than a separately created transaction that reverts the previous one, for this. 
  - Or, possibly even less problematic, don’t keep deleted text in the document, but store it alongside it and display it as widgets.

- ## [Serialize and save undo history? - discuss. CodeMirror _202204](https://discuss.codemirror.net/t/serialize-and-save-undo-history/4254)
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

- ## [Is there a way to customize the undo history list? - v6 - discuss. CodeMirror _202310](https://discuss.codemirror.net/t/is-there-a-way-to-customize-the-undo-history-list/7343)
  - I don’t want to add this insert operation to the undo history list. When using “Mod-z” for an undo operation, I want to skip this text insertion and directly return to an earlier historical state. What should I do?
- There’s an annotation you can add to transactions to get this effect.

- ## [Disable CTRL-Z (undo) for the very first change - v6 - discuss. CodeMirror _202203](https://discuss.codemirror.net/t/disable-ctrl-z-undo-for-the-very-first-change/4202)
  - The problem I have is that if a user presses CTRL-Z after the initial setting of the value, the whole content disappears. 
- If you create the new state with the content already in it, instead of firing a separate transaction that sets it, undo won’t delete it.
- You can also annotate your transaction with an `AddToHistory.of(false)` , can be any change.

- ## 💄 [Undo History for Widgets - v6 - discuss. CodeMirror _202105](https://discuss.codemirror.net/t/undo-history-for-widgets/3200)
  - I am building a rich-media code editor where users can insert images, video
  - I am trying to use CM6 to achieve this, via a StateField and StateEffects. 
  - To insert an image for example, I create a transaction with the appropriate StateEffect to create the image. This transaction also inserts a character at the location to insert the image. Then, I construct a replacement widget and replace the character I just inserted. This is done so that the cursor can correctly move around the image.
  - The problem I am having is integrating this with CM6’s undo history. I have tried using the invertedEffects facet to generate the appropriate inverse effect to add/remove the widget.
  - when the widget is deleted the user must press undo twice to recover the widget. Once to undo the deleted character and once again to undo the deleted widget.
- Effects and changes created by a single transaction should always be grouped together into the same history ‘event’. So this might be a bug. 

- ## [CodeMirror 6 cm.clearHistory() equivalent - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/codemirror-6-cm-clearhistory-equivalent/2851)
- There is no such thing, directly. If you’re loading a new document, the recommendation is to create a fresh EditorState, which will start with an empty history. 
- as Excel has a lot of cells - every one of them has its own functions. When a user selects one of them - we can change the value and use one set for everyone. In this case, when we can not clear the history - it is not possible - need every time to run a new code mirror.
  - No, just a new editor state, which, if I understand what you’re doing correctly, would be a reasonable thing to create anyway.

- One use case is an external component keeping track of physical characteristics of the editor, such as its height, which is independent of the document being edited. For that, it’s useful to have an update listener that survives the loading of a new document.

- ## 💡 [editor.setHistory(), clearHistory() equivalent in Codemirror #6 - v6 - discuss. CodeMirror _202304](https://discuss.codemirror.net/t/editor-sethistory-clearhistory-equivalent-in-codemirror-6/6291)
  - each file has its own undo-redo history. We store history of each file by calling editor.getHistory() and storing in a Map. Whenever you switch the files, we load the history for that file and call editor.setHistory. This worked well in CM 5
  - in CM 6, the history API changed, and I’m not sure how to do it anymore. 
- Usually, in situations like this, you just want to store the entire editor state (either as a JS object, or, if you need to serialize it, via EditorState.toJSON) rather than storing the document and history separately.
  - You can’t clear history. Just create a new state. When creating a new state with fromJSON, you can provide your serialized history in the JSON object.

- 🌰 [How to clear undo history in CodeMirror 6? - Stack Overflow](https://stackoverflow.com/questions/72754532/how-to-clear-undo-history-in-codemirror-6)

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

- ## [Question when peer networks differ during collaborative editing? - v6 - discuss. CodeMirror _202308](https://discuss.codemirror.net/t/question-when-peer-networks-differ-during-collaborative-editing/7008)
- This is a good point (and a similar issue was recently brough up for ProseMirror, which uses a comparable collab system). 
  - I’ve added a `rebaseUpdates` function to @codemirror/collab 6.1.0 which allows a server to accept updates when the client’s version doesn’t match the current server document. The website example has been updated to make use of this.
- If my understanding is correct, this excerpt from the website example is outdated after the addition of rebaseUpdates
  - Thanks for spotting that. That is indeed no longer safe if you are using rebaseUpdates. I’ve removed it.

# discuss-user-cursor
- ## 

- ## 

- ## [How to show peers' cursors on CM6 collab editor? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/how-to-show-peers-cursors-on-cm6-collab-editor/3996)
- This isn’t a feature that any of the core modules provides—you’ll have to implement it yourself, by sharing the cursor positions over the network and displaying some widget or tooltip at those locations.

# discuss
- ## 

- ## 

- ## 

- ## [Rebuilding code file in backend does not match frontend - discuss. CodeMirror _202403](https://discuss.codemirror.net/t/rebuilding-code-file-in-backend-does-not-match-frontend/7928)
  - I’m noticing that sometimes my backend is not able to rebuild the code the same way as the frontend. I think this is because codemirror uses dispatch to implement updates on the frontend, but in the backend you are stuck manipulating the document directly.

- The difference in approach between the frontend and backend might indeed be causing the inconsistency.
  - In the frontend, you’re using dispatch to apply updates to the CodeMirror instance. This is the recommended way to make changes to the editor’s state because it ensures that the changes are applied correctly and consistently with respect to the editor’s internal state.
  - In the backend, however, you’re directly manipulating the document without using dispatch. This could indeed lead to inconsistencies because you’re bypassing the mechanism that CodeMirror provides for applying updates safely.
  - To address this issue, you should try to mimic the frontend behavior in the backend as closely as possible. Since you’re using the @codemirror/collab package in the frontend, you should also use it in the backend to ensure consistency in how updates are applied.

- ## [Adding new line for other users - v6 - discuss. CodeMirror _202404](https://discuss.codemirror.net/t/adding-new-line-for-other-users/8077)
- You’ll want to follow this example if you want robust collaborative editing. Input handlers are indeed a terrible place to try and capture document changes. Update listeners work better, but you’ll still have issues with concurrent edits if you use those the naive way. This is why @codemirror/collab exists.
