---
title: lib-editor-prosemirror-community-server-backend
tags: [backend, community, prosemirror]
created: '2022-10-03T10:14:22.925Z'
modified: '2022-10-03T10:15:05.904Z'
---

# lib-editor-prosemirror-community-server-backend

# guide

# discuss-transform-operation
- ## 

- ## 

- ## 

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
