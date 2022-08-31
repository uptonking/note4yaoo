---
title: lib-editor-prosemirror-community-model-storage
tags: [community, data-model, prosemirror, storage]
created: 2022-08-30T21:49:04.687Z
modified: 2022-08-30T22:00:29.366Z
---

# lib-editor-prosemirror-community-model-storage

# guide

# discuss
- ## 

- ## 

- ## 

- ## Theoretical saving question
- https://discuss.prosemirror.net/t/theoretical-saving-question/656
  - Better to save a user document from ProseMirror in a whole file on the database or as separate individual changes?
  - Currently a user creates a written document here in the editor. We save the entire doc locally every 1/3 of sec for them and then save a backup copy on the server on doc close or page close. Always running on the local copy.
  - But realized we can’t reconstitute a document later as a document can be overwritten on the server from the local.

- This very much depends on your use case and the features you wish to support. 
  - For my use case, I store a single record for the document. So, I’m writing over the previous document with the newly saved document (and then rails auto updates the updated_at timestamp for me).
  - If you want to support change history (which I do but am not tackling yet), you’ll need to either A. store every version of the document or B. store the diffs (I believe ProseMirror can output some json representation of the changes). Again, I haven’t tackled this part yet so my understanding is a little vague.

- 👉🏻 Both are valid approaches – I know several users are saving all steps, in order to be able to later display or revert changes, and to be able to go back to earlier versions. Whether you need that complexity depends on what you want to do.

- what I’m trying to achieve is saving all steps on the server but compact old steps using Step.merge and replace large chunks of very old steps with checkpoints (docs), this is quite difficult in an implementation using a NOSQL DB where a client will be doing this compacting. It needs to find a safe version to compact to that all current clients have already used and there is the issue of offline clients coming back online.

- You can use `prosemirror-compress` to merge consecutive steps and then compress their JSON representations before sending them to the server.
- The steps can be merged and compressed before they are sent to the server. If not, maybe merging can be done after a checkpoint is created?
