---
title: lib-editor-prosemirror-community-data-model-storage
tags: [community, data-model, prosemirror, storage]
created: 2022-08-30T21:49:04.687Z
modified: 2022-09-05T03:25:02.690Z
---

# lib-editor-prosemirror-community-data-model-storage

# guide

# discuss
- ## 

- ## 

- ## [How to save to database in optimal way? _202307](https://discuss.prosemirror.net/t/how-to-save-to-database-in-optimal-way/5733)
- There are many ways to approach this, but one of the ways that comes to my mind quickly is to treat the database as something similar to another client that performs an occasional autosave to the database after multiple changes. This is kinda similar to how Figma works, I believe.
  - The way you store the documents to your databases is up to you, as there are many ways to approach that between serializing to HTML string or to JSON. 

- Consider just storing as plain text for now. If you have an issue with the size of the files stored, you can always migrate the data by adding a column or property like "encoding": "gzip", and gzip each text file up into a more space-efficient representation.
  - As well, it might sound inefficient to do fetching of the entire document, manipulation, and re-storage, but I would push you to try it out and see if there’s an issue with your users. All storage and synchronization should not block the socket connection, so it shouldn’t affect the user’s experience.
  - There are many solutions to making everything more efficient, and those solutions are easier to prioritize when you have many users who are complaining about something.
  - My suspicion is that if you have too many users, that you’re algorithm is causing back-pressure issues or something like that, then you have enough users and a valuable enough product to get a loan or pay for consultation to tackle the very specific performance problem.

- 
- 
- 

- ## [How can I listen to transactions and “translate” them to something more concrete like “moveNode”, “replaceNode” or “deleteNode”?](https://discuss.prosemirror.net/t/listen-and-categorize-changes/5606)
  - I’m starting to use PM for my startup https://mintter.com in our editor, we do not save the whole state value in the backend, but **we send the backend all the operations that happened at a specific node level**: we have a block-based editor similar to notion, and we are just storing changes at the block level (moves, replace and delete).
  - I’m finding really hard to translate transactions and steps into our changes types
  - From what I’ve seen, I need to always create a new state and compare both the oldState and the newState of the whole document to determine what changed and what block changed. This sounds to much considering that we might need to control this operations for long documents with thousands of blocks. not sure if this is the right approach?
- ProseMirror’s steps take a completely different approach to describing modifications than the vocabulary you’re using, so yeah, diffing is probably the best approach. I don’t believe it’ll be that slow—you can just skip over nodes that were reused between the documents with an object equality check.
- from the documentation provided, the transaction provides a docChange keyword, you can compare it with the next transaction. The creation of a plugin to handle the entire doc, I don’t see how is feasible

- ## [How can I select a node from the current doc?](https://discuss.prosemirror.net/t/how-can-i-select-a-node-from-the-current-doc/5297/3)
- A node object does not identify a node in the document. These don’t have a meaningful identity, they are just values—you can create a document containing the same node object multiple times. 
  - Thus, as you found, **the library uses positions to identify nodes**.

- ## [Data structure with ids](https://discuss.prosemirror.net/t/data-structure-with-ids/33?page=2)
  - Now we’re using a `data-grid-id` attribute on each top-level child of our editable. We have a function to make a new id if new blocks are made by the editor.

- Go through the transform interface if you want to change something about the document.

- Basically like above, we store each top level node by a unique key, and we persist updates to the doc by a transaction with the key of the top level node that was changed, and the new data within. Will this mesh ok with Prosemirror or should I look at other editors?
  - You should be able to map between such a system and ProseMirror transactions, if you really want to. Getting collaborative editing working with such a representation is another issue, but maybe that’s not a requirement for you.

- ## Store Document in memory
- https://discuss.prosemirror.net/t/store-document-in-memory/1238
- note that just because a step can be applied doesn’t mean that it is valid—the content of inserted nodes, for example, isn’t checked when they are inserted as a whole. So you might also want to call .check() on the resulting document to make sure it conforms to the schema. Are you already validating the JSON data against a schema? The fromJSON methods are not terribly defensive, and might create bogus nodes when given bad input.

- ## How to replace all images src from paste slice object?
- https://discuss.prosemirror.net/t/how-to-replace-all-images-src-from-paste-slice-object/3023
- One of possible solutions is to use Slice.toJSON / fromJSON and recursive JSON traversal in between.

- ## Update schema in collaborative editing
- https://discuss.prosemirror.net/t/update-schema-in-collaborative-editing/3112
  - How to send updated Schema on the client side to the (collab) server ?
- If you’re asking how to send a Schema object over the wire—you can’t really do that. Schema specs can contain functions, so even if you have to original spec
- I wonder if instead of sending a schema, you can keep two instances of Schema (generated by the same code) one on client side and other on server and add a plugin on both sides. This is possible since you need to anyway maintain an EditorState on the server side. With the reconfigure API, I am hoping most of your plugin state will be retained.

- ## Schema: move nested content to block-level?
- https://discuss.prosemirror.net/t/schema-move-nested-content-to-block-level/4922
- DOMParser will add wrapping nodes when necessary, but it won’t break content out of wrapping nodes. 
  - 👉🏻️ So yes, this is something that should be done with a pre-processor.

# discuss-saving
- ## 

- ## 

- ## 

- ## [How Edit/Save works in ProseMirror?](https://discuss.prosemirror.net/t/how-edit-save-works-in-prosemirror/5664)
- Depending on what you want in your database, you can store `state.doc.toJSON()` or use `DOMSerializer` and then `innerHTML` to convert the document to HTML.

- ## [Current state of the art on syncing data to backend](https://discuss.prosemirror.net/t/current-state-of-the-art-on-syncing-data-to-backend/5175)
- I am still torn on how to sync my data to backend
  - documents can be very big. Like, 10Mb JSONs. (P. S. Prosemirror handles those pretty well, actually impressive)
  - So sending entire JSON to backend is not good. 
  - I’d rather just send diffs.
  - Sending Steps occurred to me, but I have no way of applying this to my backend.

- I haven’t really heard of people working with 10mb documents—is there something like images-as-data-urls or something in your documents that makes them so big? In most setups, sending the documents back and forth is unproblematic, because they generally are not that big.

- I guess you could try something like JSON diffing to only send a small patch over, if you really need to.

- For anyone looking for a solution with this, we have successfully implemented a POC that is consisting of:
  - We then compare the reference state with the last captured state and calculate a JSON diff via this library and generate JSON patch array.
  - **For calculating patches, we are using a Web Worker**
  - Backend: Since we are doing JSON patches, most of backends support these patches, we then just patch the JSON and save it. For our particular setup, we translate the patches to MongoDB methods.
  - For an extra layer of security, we are thinking of sending a hash of state to backend, so the backend can compare it after applying the patch. If hashes don’t match, a reconciliation step should occur, we are still tinkering with this.

- How do you pass the editor state to that worker? As far as I’m aware, that involves serializing and deserializing the whole thing.
  - It(`calculatePatches`) sends the two JSONs to worker and gets the result back.

- ## [Saving content onchange](https://discuss.prosemirror.net/t/saving-content-onchange/3557)
  - We need to implement saving on change, but saving the whole document state seems expensive, even with debounce.
  - We tried to save changes in each “high level node”, and store them separately adding an attribute like “sortOrder” to restore the full state on first load. But is seems difficult in some cases. And also we save diffrent versions, so that we can apply diff in future.
  - May be you have ideas how to do this better? Save Steps instead of nodes?

- Saving steps (possibly compressing them with `merge`), along with occasional snapshots is what many people are doing, and seems to work well.

- ## [Theoretical saving question](https://discuss.prosemirror.net/t/theoretical-saving-question/656)
  - Better to save a user document from ProseMirror in a whole file on the database or as separate individual changes?
  - Currently a user creates a written document here in the editor. We save the entire doc locally every 1/3 of sec for them and then save a backup copy on the server on doc close or page close. Always running on the local copy.
  - But realized we can’t reconstitute a document later as a document can be overwritten on the server from the local.

- This very much depends on your use case and the features you wish to support. 
  - For my use case, I store a single record for the document. So, I’m writing over the previous document with the newly saved document (and then rails auto updates the updated_at timestamp for me).
  - 👉🏻 **If you want to support change history** (which I do but am not tackling yet), you’ll need to either A. store every version of the document or B. store the diffs (I believe ProseMirror can output some json representation of the changes). Again, I haven’t tackled this part yet so my understanding is a little vague.

- 👉🏻 Both are valid approaches – I know several users are saving all steps, in order to be able to later display or revert changes, and to be able to go back to earlier versions. Whether you need that complexity depends on what you want to do.

- what I’m trying to achieve is saving all steps on the server but compact old steps using Step.merge and replace large chunks of very old steps with checkpoints (docs), this is quite difficult in an implementation using a NOSQL DB where a client will be doing this compacting. It needs to find a safe version to compact to that all current clients have already used and there is the issue of offline clients coming back online.

- You can use `prosemirror-compress` to merge consecutive steps and then compress their JSON representations before sending them to the server.
- The steps can be merged and compressed before they are sent to the server. If not, maybe merging can be done after a checkpoint is created?
