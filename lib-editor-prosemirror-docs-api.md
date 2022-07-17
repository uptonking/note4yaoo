---
title: lib-editor-prosemirror-docs-api
tags: [api, docs, editor, prosemirror]
created: 2021-06-13T07:56:30.857Z
modified: 2021-06-13T07:57:01.122Z
---

# lib-editor-prosemirror-docs-api

# guide

- 注意数据的区别
  - doc.content, state, view

- 文档内容的更新
  - transformations

- EditorState的更新
  - apply(tr)
  - applyTransaction(tr)

- EditorView的更新
  - update(props), setProps(props)
  - DecorationSet
  - nodeViews, update()

- EditorView的配置参数
  - dispatchTransaction()方法内会调用updateState()
# state
- ProseMirror keeps all editor state (the things, basically, that would be required to create an editor just like the current one) in a single object.
  - That object is updated (creating a new state) by applying transactions to it.

- EditorState
  - doc
  - selection
  - storedMarks
  - plugins
  - schema
  - apply(tr: Transaction) → EditorState
    - Apply the given transaction to produce a new state.
  - applyTransaction(rootTr: Transaction) → {state: EditorState, transactions: [Transaction]}
    - Verbose variant of `apply` that returns the precise transactions that were applied along with the new state.

- Selection
  - ranges
    - The ranges covered by the selection.
  - from
  - to
  - anchorhead
  - map()
  - content()
- SelectionBookmark
  - A lightweight, document-independent representation of a selection. 
  - You can define a custom bookmark type for a custom selection class to make the history handle it well.

- PluginSpec: It provides a definition for a plugin.
  - props
    - The view props added by this plugin
  - state: ?⁠StateField
    - an extra slot in the state object in which it can keep its own data.
  - key
    - Can be used to make this a keyed plugin. You can have only one plugin with a given key in a given state
  - view()
    - When the plugin needs to interact with the editor view, or set something up in the DOM, use this field. 
    - The function will be called when the plugin's state is associated with an editor view.
  - filterTransaction
  - appendTransaction

- StateField
  - init(config: Object, instance: EditorState) → T
    - Initialize the value of the field.
  - apply(tr, value, oldState, newState)
    - Apply the given transaction to this state field, producing a new field value. 
    - Note that the newState argument is again a partially constructed state does not yet contain the state from plugins coming after this one.

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
  - props: DirectEditorProps
    - The view's current props.
  - state: EditorState
    - The view's current state.
  - dom
    - An editable DOM node containing the document.
    - You probably should not directly interfere with its content.
  - root
    - Get the document root in which the editor exists. 
  - editable: boolean
    - Indicates whether the editor is currently editable.
  - update(props: DirectEditorProps)
    - Update the view's props. 
    - Will immediately cause an update to the DOM.
  - setProps(props: DirectEditorProps)
    - Equivalent to `view.update(Object.assign({}, view.props, props))`.
  - updateState(state: EditorState)
    - Update the editor's state prop, without touching any of the other props.
  - dispatch(tr: Transaction)
    - Will call `dispatchTransaction` when given, 
    - and otherwise defaults to applying the transaction to the current state and calling `updateState` with the result. 
    - This method is bound to the view instance, so that it can be easily passed around.
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
- The various event-handling functions may all `return true` to indicate that they handled the given event. 
  - The view will then take care to call `preventDefault` on the event, except with `handleDOMEvents`, where the handler itself is responsible for that.

- EditorProps
  - handleEvents
  - domParser
    - The parser to use when reading editor changes from the DOM. 
    - Defaults to calling `DOMParser.fromSchema` on the editor's schema.
  - nodeViews: fn(node, view, getPos, decorations, innerDecorations)
    - Allows you to pass custom rendering and behavior logic for nodes and marks. 
    - Should map node and mark names to constructor functions that produce a `NodeView` object implementing the node's display behavior. 
    - For nodes, the third argument `getPos` is a function that can be called to get the node's current position, which can be useful when creating transactions to update it. 
    - For marks, the third argument is a boolean that indicates whether the mark's content is inline.
  - decorations
    - A set of document decorations to show in the view.
  - scrollThreshold
- DirectEditorProps(extends EditorProps)
  - state: EditorState
    - The current state of the editor.
  - dispatchTransaction: ?⁠fn(tr: Transaction)
    - The callback over which to send transactions (state updates) produced by the view. 
    - If you specify this, you probably want to make sure this ends up calling the view's `updateState` method with a new state that has the transaction applied. 

- By default, document nodes are rendered using the result of the `toDOM` method of their spec, and managed entirely by the editor. 
  - For some use cases, such as embedded node-specific editing interfaces, you want more control over the behavior of a node's in-editor representation, and need to define a custom node view.
- Mark views only support `dom` and `contentDOM`, and don't support any of the node view methods.

- NodeView
  - dom: ?⁠domNode
    - The outer DOM node that represents the document node. 
    - When not given, the default strategy is used to create a DOM node.
  - contentDOM: ?⁠domNode
    - The DOM node that should hold the node's content. 
    - Only meaningful if the node view also defines a `dom` property and if its node type is not a leaf node type.
    - When this is present, ProseMirror will take care of rendering the node's children into it. 
    - When it is not present, the node view itself is responsible for rendering (or deciding not to render) its child nodes.
  - update(node, decorations, innerDecorations)
    - When given, this will be called when the view is updating itself
    - If the node view has a `contentDOM` property (or no dom property), updating its child nodes will be handled by ProseMirror.
  - selectNode
    - Can be used to override the way the node's selected status (as a node selection) is displayed.
  - setSelection
    - This will be called to handle setting the selection inside the node.
  - stopEvent: ?⁠fn(event: dom. Event) → bool
    - Can be used to prevent the editor view from trying to handle some or all DOM events that bubble up from the node view. 
    - Events for which this returns true are not handled by the editor.
  - ignoreMutation: ?⁠fn(dom. MutationRecord) → bool
    - Called when a DOM mutation or a selection change happens within the view. 

- Decorations make it possible to influence the way the document is drawn, without actually changing the document.

- Decoration
  - static widget(pos, toDOM, spec)
    - Creates a widget decoration, which is a DOM node that's shown in the document at the given position. 
    - It is recommended that you delay rendering the widget by passing a function that will be called when the widget is actually drawn in a view, but you can also directly pass a DOM node. 
    - getPos can be used to find the widget's current document position.
# transform
- This module defines a way of modifying documents that allows changes to be recorded, replayed, and reordered
- Transforming happens in Steps, which are atomic, well-defined modifications to a document. 
  - Applying a step produces a new document.
- Each step provides a change map that maps positions in the old document to position in the transformed document. 
  - Steps can be inverted to create a step that undoes their effect, and chained together in a convenience object called a `Transform`.

- A step object represents an atomic change. 
  - It generally applies only to the document it was created for, since the positions stored in it will only make sense for that document.

- Step
  - apply(doc: Node) → StepResult
    - Applies this step to the given document, returning a result object that either indicates failure
  - getMap() → StepMap
    - Get the step map that represents the changes made by this step
  - invert(doc: Node) → Step
    - Create an inverted version of this step. 
    - Needs the document as it was before the step as argument.
  - map(mapping: Mappable) → ?⁠Step
    - Map this step through a mappable thing
  - merge(other: Step) → ?⁠Step
    - Try to merge this step with another one
  - static jsonID(id: string, stepClass: constructorStep)
    - To be able to serialize steps to JSON, each step needs a string ID to attach to its JSON representation. 
    - Use this method to register an ID for your step classes. 

- Mapping positions from one document to another by running through the step maps produced by steps is an important operation in ProseMirror. 
  - It is used, for example, for updating the selection when the document changes.

- StepMap is a map describing the deletions and insertions made by a step, 
  -  which can be used to find the correspondence between positions in the pre-step version of a document and the same position in the post-step version.

- A mapping represents a pipeline of zero or more step maps

- Transfrom is an abstraction to build up and track an array of steps representing a document transformation.
  - Most transforming methods return the Transform object itself, so that they can be chained.

- Transform
  - doc
    - The current document (the result of applying the steps in the transform).
  - steps: [Step]
    - The steps in this transform.
  - docs: [Node]
    - The documents before each of the steps.
  - mapping: Mapping
    - A mapping with the maps for each of the steps in this transform.
  - step(step: Step) → this
    - Apply a new step in this transform, saving the result. Throws an error when the step fails.
  - replace(from, to, slice)
    - Replace the part of the document between from and to with the given slice.
  - replaceWith(from, to, content)
    - Replace the given range with the given content, which may be a fragment, node, or array of nodes
  - replaceRange(from: number, to: number, slice: Slice) → this
    - Replace a range of the document with a given slice, using from, to, and the slice's openStart property as hints, rather than fixed start and end points. 
    - This method may grow the replaced area or close open nodes in the slice in order to get a fit that is more in line with WYSIWYG expectations
    - The similar `replace` method is a more primitive tool which will not move the start and end of its given range, and is useful in situations where you need more precise control over what happens.
  - split(pos, depth, typesAfter)
    - Split the node at the given position, and optionally, if depth is greater than one, any number of nodes above that. 
    - By default, the parts split off will inherit the node type of the original node. 
    - This can be changed by passing an array of types and attributes to use after the split.
  - join(pos, depth)
    - Join the blocks around the given position. 
    - If depth is 2, their last and first siblings are also joined, and so on.
# model
- This module defines ProseMirror's content model, the data structures used to represent and work with documents.
- A ProseMirror document is a tree. 
  - At each level, a `node` describes the type of the content, and holds a `fragment` containing its children.

- Node
  - type
  - content
  - attrs
  - marks
  - text
    - For text nodes, this contains the node's text content.
  - nodeSize
    - The size of this node, as defined by the integer-based indexing scheme. 
    - For text nodes, this is the amount of characters. 
    - For other leaf nodes, it is 1. 
    - For non-leaf nodes, it is the size of the content plus two (the start and end token).

- NodeType
  - name
  - schema
  - spec
  - isBlock
  - isInline
  - isLeaf
  - ...

- Fragment

- Mark

- Slice
  - content
  - openStart
  - openEnd

- Schema
  - spec
  - nodes
  - marks
  - topNodeType
  - cached
  - node(type, attrs, content)
    - Create a node in this schema.
  - text(text, marks)
    - Create a text node in the schema. 
    - Empty text nodes are not allowed.
  - mark
  - nodeFronJSON(json)
  - markFromJSON(json)

- NodeSpec
  - content
  - nodes
  - attrs
  - group
  - inline
# schema-basic
- This schema roughly corresponds to the document schema used by CommonMark, minus the list elements
  - To reuse elements from this schema, extend or read from its `spec.nodes` and `spec.marks` properties.

- schema.nodes
  - doc
  - paragraph
  - blockquote
  - horizontal_rule
  - heading
  - code_block
  - text
  - image
  - hard_break
    - represented in the DOM as `<br>`.

- schema.marks
  - link
  - em
  - strong
  - code
# schema-list
- This module exports list-related schema elements and commands. 
  - The commands assume lists to be nestable, with the restriction that the first child of a list item is a plain paragraph.

- node specs
  - orderedList
  - bulletList
  - listItem
  - addListNodes
    - adding list-related node types to a map specifying the nodes for a schema.

- commands
  - wrapInList
  - splitListItem
  - liftListItem
  - sinkListItem
