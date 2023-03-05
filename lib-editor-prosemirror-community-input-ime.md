---
title: lib-editor-prosemirror-community-input-ime
tags: [community, ime, input-method, prosemirror]
created: 2022-09-17T09:30:19.022Z
modified: 2022-09-17T09:31:16.310Z
---

# lib-editor-prosemirror-community-input-ime

# guide
- 目前prosemirror对beforeinput使用很少
# discuss
- ## 

- ## 

- ## 

- ## I noticed that the native undo / redo input events historyUndo / historyRedo events do not work as expected in ProseMirror._201903
- https://discuss.prosemirror.net/t/native-undo-history/1823
- the problem is that browser makers have a very different view of how undo/redo work than how the web works. 
- In the browsers’ view, there should just be one undo/redo stack for everything on the same webpage. So say you have two different textareas on the same page, or some form elements and an editor, the browsers believe that they should all share the same undo stack. 
- In the case of Safari, they go a step further in that for them it’s a “platform behavior” that has to be preserved so that web apps work the same as native apps.
  - There is a little bit of hope right now though in that Safari has been experimenting with an API that will allow JavaScript to add items to the global undo stack programmatically 
