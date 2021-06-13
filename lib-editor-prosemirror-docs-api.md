---
title: lib-editor-prosemirror-docs-api
tags: [api, docs, editor, prosemirror]
created: '2021-06-13T07:56:30.857Z'
modified: '2021-06-13T07:57:01.122Z'
---

# lib-editor-prosemirror-docs-api

# guide

# state
- ProseMirror keeps all editor state (the things, basically, that would be required to create an editor just like the current one) in a single object.
  - That object is updated (creating a new state) by applying transactions to it.

- EditorState
  - doc
  - selection
  - storedMarks
  - plugins
  - schema
  - apply()
    - Apply the given transaction to produce a new state.
  - applyTransaction
    - Verbose variant of `apply` that returns the precise transactions that were applied along with the new state.

- Selection
  - ranges
    - The ranges covered by the selection.
  - from
  - to
  - anchorhead
  - map()
  - content()

- PluginSpec: It provides a definition for a plugin.
  - props
    - The view props added by this plugin
  - state
    - an extra slot in the state object in which it can keep its own data.
  - key
    - Can be used to make this a keyed plugin. You can have only one plugin with a given key in a given state
  - view()
    - When the plugin needs to interact with the editor view, or set something up in the DOM, use this field. 
    - The function will be called when the plugin's state is associated with an editor view.
  - filterTransaction
  - appendTransaction

- Plugins bundle functionality that can be added to an editor. 
  - They are part of the editor state and may influence that state and the view that contains it.

- Plugin
  - props
  - spec
  - getState()
    - Extract the plugin's state field from an editor state.
# view

- view module displays a given editor state in the DOM, and handles user events.


- `EditorView` manages the DOM structure that represents an editable document. 
  - Its state and behavior are determined by its `props`.




- EditorView
  - props
    - The view's current props.
  - state
    - The view's current state.
  - dom
    - An editable DOM node containing the document.
    - You probably should not directly interfere with its content.
  - update(props)
    - Update the view's props. 
    - Will immediately cause an update to the DOM.
  - updateState(state)
    - Update the editor's state prop, without touching any of the other props.
  - dispatch(tr: Transaction)
    - Will call `dispatchTransaction` when given, and otherwise defaults to applying the transaction to the current state and calling `updateState` with the result. 
    - This method is bound to the view instance, so that it can be easily passed around.
  - root
    - Get the document root in which the editor exists. 
    - This will usually be the top-level document, but might be a shadow DOM root if the editor is inside one.
  - editable
  - dragging
  - composing
    - Holds true when a composition IME is active.
  - focus()
  - posAtCoords()
    - Given a pair of viewport coordinates, return the document position that corresponds to them.
  - coordsAtPos
  - domAtPos
    - Find the DOM position that corresponds to the given document position.
  - nodeDOM(pos)
    - Find the DOM node that represents the document node after the given position.
  - posAtDOM()
  - endOfTextblock()
  - destroy()
    - Removes the editor from the DOM and destroys all node views.

- EditorProps are configuration values that can be passed to an editor view or included in a plugin.

- NodeView
- By default, document nodes are rendered using the result of the `toDOM` method of their spec, and managed entirely by the editor. 
- For some use cases, such as embedded node-specific editing interfaces, you want more control over the behavior of a node's in-editor representation, and need to define a custom node view.
- Mark views only support `dom` and `contentDOM`, and don't support any of the node view methods.


- Decorations make it possible to influence the way the document is drawn, without actually changing the document.


# transform
- This module defines a way of modifying documents that allows changes to be recorded, replayed, and reordered
- Transforming happens in Steps, which are atomic, well-defined modifications to a document. 
  - Applying a step produces a new document.
- Each step provides a change map that maps positions in the old document to position in the transformed document. 
  - Steps can be inverted to create a step that undoes their effect, and chained together in a convenience object called a Transform.


# model
- This module defines ProseMirror's content model, the data structures used to represent and work with documents.
- A ProseMirror document is a tree. 
  - At each level, a `node` describes the type of the content, and holds a `fragment` containing its children.
