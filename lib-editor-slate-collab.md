---
title: lib-editor-slate-collab
tags: [collaboration, slate-editor]
created: 2022-05-15T18:46:21.529Z
modified: 2023-02-05T19:03:12.722Z
---

# lib-editor-slate-collab

# guide

- why use binding to implement collab?
  - flexibility over performance

- not-yet-基于crdt实现text文本协作的问题
  - 对不同分支的文档在相同位置粘贴相同的文本时，crdt会保留重复的文本
# collaboration solutions

## [logux crdt Conflict Resolution](https://logux.io/guide/concepts/state/)

- Logux Redux and Logux Vuex uses time travel to keep the same order of actions on all machines. 
  - It uses ID and time from meta to detect order and time travel to insert action in the right moment of history. 
- Time travel is a technique when Logux Redux reverts recent actions, apply new action, and then re-apply recent actions.

- As a result, if the developer used atomic actions, conflict actions will override each other (“the last write wins” model). 
  - In complicated cases, you can define merge logic in reducers.
  - We recommend keeping actions atomic. It means that action should not contain current state. 
  - For instance, it is better to generate likes/add and likes/remove on the client, rather than likes/set with the exact number.

- In any moment server can send logux/undo action and client will revert changes of this action. 
  - Logux Redux will load the closest state snapshot and then re-apply all actions without reverted action.

## [o-spreadsheet](https://github.com/odoo/o-spreadsheet/blob/saas-16.3/doc/integrating/collaborative/collaborative.md)

- based on Operational Transformation
- In order to identify and resolve which operations conflict, we need a way to detect two concurrent actions, and a way to order them.
  - To detect concurrency, we introduce a revision log, which is a unique identifier to indicate on which state the action is executed. 
  - Each time an action is received and accepted by the server (the revision log of the server is the same as the action), the revision log is incremented.
- When a client executes an action, it's locally executed, sent to the server and kept in the pending actions of the user. 
  - If the action is accepted by the server, the action is removed from the pending ones. 
  - In the other case, the pending actions are reverted, transformed with the action received from the server, re-applied locally and resent to the server until they are accepted.

- cons
  - We need to write a transformation function for each command we create
  - Undo/Redo is synchronous, i.e. it should be accepted by the server before being executed locally.
# collab
- 支持响应式移动端时，如何支持小屏元素的鼠标位置
# [slate-yjs](https://docs.slate-yjs.dev/)
- Why a CRDT over OT? 
  - While many current collaborative text editing applications rely on OT (e.g., google docs with ShareJS), it only provides a subset of the functionally CRDTs offer due to the dependence on a central server. 
  - In other words: CRDTS can do everything OT can, but OT simply can't.

- While @slate-yjs/core doesn't contain all by slate-yjs provided functionality, it contains everything you need to set up a basic **2 way binding between a slate editor and a yjs shared type**.
  - The binding should keep slate and the yjs document in sync.

- Slate-yjs will overwrite the current editor value with the state contained in the shared type. 

- When collaborating with other users the asynchronous nature of applying changes can result in a state where slate has no children. 
  - Rendering this state will result in a crash. 
  - To avoid the issue we have to add a normalization rule to ensure the slate state is always valid.

- Due to current limitations in yjs, slate-yjs "translates" `move_node` and some `split_node` operations into inserts and deletes. 
  - This might cause some unexpected behavior when it comes to relative positions
- 🚨 Since there is currently no way to **move ranges** of text inside yjs, this operation is performed as a delete of "ome text" and an insert of a new paragraph (= a Y. XmlText). 
  - This is where stored positions come in.
  - In the future, yjs might introduce a way of moving ranges of text making stored positions obsolete

- Stored positions are in fact backed by relative positions but are updated by slate-yjs on certain operations (like move_node and some split_node operations).
  - Once you store a position, slate-yjs encodes it as a relative position and stores it in the shared root under a prefixed version of the provided storage key.
  - If you now perform a specific split_node or move_node operation, the binding checks if there are any stored positions in the moved range and updates them accordingly by encoding the position where the stored position should point to after the operation and overwriting the value in the shared root.

- In comparison to relative positions, stored positions add a minimal overhead when applying changes to the shared root. While this overhead is tiny, it might cause a noticeable delay if the document contains thousands of stored locations.

- Displaying remote cursors using **overlays** has a few tradeoffs to keep in mind:
- Pros:
  - Since cursors overlays aren't part of the by slate rendered content, they don't change the underlying dom structure causing e.g. different line breaks when a remote user changes his selection.
  - They don't mess with autocorrect
  - Animating them is easier
  - They potentially provide better performance since they don't require re-rendering of parts of the editor content on remote cursor change
- Cons:
  - They are not part of the actual editor content which makes them harder to keep in sync leading to them visually lagging behind in some scenarios on slower devices.
  - It's harder to customize node rendering/behavior based on remote selection since changes of them don't cause node re-renders.

- Displaying remote cursors using **decorations** has a few tradeoffs to keep in mind:
- Pros:
  - They are part of the actual editor content which makes them easier to keep in sync leading to them never visually lagging behind.
  - It's easier to customize node rendering/behavior based on remote selection since changes of them cause node re-renders.
- Cons:
  - Since cursors overlays are part of the by slate rendered content, they change the underlying dom structure causing e.g. different line breaks when a remote user changes his selection.
  - They potentially mess with autocorrect
  - Animating them is harder
  - They potentially provide worse performance since they require re-rendering of parts of the editor content on remote cursor change
