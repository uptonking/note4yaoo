---
title: lib-editor-prosemirror-community-server-backend
tags: [backend, community, prosemirror]
created: 2022-10-03T10:14:22.925Z
modified: 2022-10-03T10:15:05.904Z
---

# lib-editor-prosemirror-community-server-backend

# guide

# discuss-transform-operation
- ## 

- ## 🔁 [Current state of the art on syncing data to backend](https://discuss.prosemirror.net/t/current-state-of-the-art-on-syncing-data-to-backend/5175)
- I am still torn on how to sync my data to backend
  - documents can be very big. Like, 10Mb JSONs. (P. S. Prosemirror handles those pretty well, actually impressive)
  - So sending entire JSON to backend is not good. 
  - I’d rather just send diffs.
  - Sending Steps occurred to me, but I have no way of applying this to my backend.

- I haven’t really heard of people working with 10mb documents—is there something like images-as-data-urls or something in your documents that makes them so big? In most setups, sending the documents back and forth is unproblematic, because they generally are not that big.

- I guess you could try something like JSON diffing to only send a small patch over, if you really need to.

- 💡 For anyone looking for a solution with this, we have successfully implemented a POC that is consisting of:
  - We then compare the reference state with the last captured state and calculate a JSON diff via this library and generate JSON patch array.
  - **For calculating patches, we are using a Web Worker**
  - Backend: Since we are doing JSON patches, most of backends support these patches, we then just patch the JSON and save it. For our particular setup, we translate the patches to MongoDB methods.
  - For an extra layer of security, we are thinking of sending a hash of state to backend, so the backend can compare it after applying the patch. If hashes don’t match, a reconciliation step should occur, we are still tinkering with this.

- How do you pass the editor state to that worker? As far as I’m aware, that involves serializing and deserializing the whole thing.
  - It(`calculatePatches`) sends the two JSONs to worker and gets the result back.

- ## Collab with a nosql db and without server side code
- https://discuss.prosemirror.net/t/collab-with-a-nosql-db-and-without-server-side-code/566
  - Has anyone looked into running collab with a nosql database (for example Firebase) without server side code ?
  - Is this feasible ? as far as I can tell it should be possible, as the authority is basically only doing set/get db transactions which can be fired directly from the client, but are there any other considerations 
- Your clients would need to make sure that they access a synced global version. To not overwrite each other, it probably makes sense to add a rule in the firebase backend that makes sure that a client update is based on the same version the current firebase (kinda like the _rev in couchdb). It’ll be a hack but probably workable.
- If your database allows some kind of compare-and-swap or if-not-matches header equivalent (to only increase a counter if the old value was the expected one), you can so this. But as Frederik noted, a lot of the intelligence will have to move to the client, which can not generally be trusted. And things like saving a whole snapshot of the document will have to be done out-of-band(频带外; 带外数据), alongside the step data, since the server won’t be able to compute a document from the steps.

- ## Is it possible to implement backend logic of the editor in some other technology?
- https://discuss.prosemirror.net/t/is-it-possible-to-implement-backend-logic-of-the-editor-in-some-other-technology/588
- You can implement a ‘dumb’ backend that just relays(转发；转播) editing steps between clients in any language, 
  - but if you want to keep a representation of the edited document on the server and check whether the steps the clients produce make sense, you will need to run JavaScript. 
  - Porting the whole document model and transform module would be a rather big and error-prone undertaking.
