---
title: lib-editor-prosemirror-docs
tags: [docs, editor, prosemirror]
created: '2021-06-02T17:12:26.261Z'
modified: '2021-06-02T17:12:56.049Z'
---

# lib-editor-prosemirror-docs

> A toolkit for building rich-text editors on the web

# guide
- features
  - Unopinionated
    - core is small and generic, allowing different types of editors
  - Customizable schemas
    - Document schemas allow editing documents with a custom structure
  - Modular
    - only load the code you need
  - Pluggable/Extensible
    - easily enable additional functionality
  - Collaborative editing
    - multiple people can work on the same document in real time
  - Functional
    - largely functional and immutable architecture to implement complex behavior

- tips
  - cursor-motion, mouse-actions, typing都由browsers处理

- **repeat**
- prosemirror state updates happen by applying a transaction to an existing state, producing a new state.
  - pm-state的更新一般都是这一种方式
  - 所以外部更新pm-state的事件处理函数一般都要注册到这个流程中
- `NodeView.stopEvent()`; 
  - Can be used to prevent the editor view from trying to handle some or all DOM events that bubble up from the node view. 
  - Events for which this returns true are not handled by the editor.
- When a given prop is declared multiple times, how it is handled depends on the prop. 
  - In general, directly provided props take precedence, after which each plugin gets a turn, in order. 
  - For some props, such as `domParser`, the first value that is found is used, and others are ignored. 
  - For **handler functions** that return a boolean to indicate whether they handled the event, **the first one that returns `true` gets to handle the event**. 
  - And finally, for some props, such as attributes and decorations, the union of all provided values is used.

- ref
  - [Marijn Haverbeke's blog](https://marijnhaverbeke.nl/blog/)
  - [Pragmatic ProseMirror guide/cookbook](https://github.com/PierBover/prosemirror-cookbook)
# overview
- ProseMirror tries to bridge the gap between editing explicit, unambiguous content like Markdown or XML, and classical WYSIWYG editors.
  - It does this by implementing a WYSIWYG-style editing interface for documents more constrained and structured than plain HTML. 
  - You can customize the shape and structure of the documents your editor creates, and tailor them to your application's needs.
# examples-tutorials

## [basic example](https://prosemirror.net/examples/basic/)

- prosemirror-example-setup package creates an array of plugins
- These plugins are created by the example setup:
  - Input rules, which are input macros that fire when certain patterns are typed. 
    - In this case, it is set up to provide things like smart quotes and some Markdown-like behavior, such as starting a blockquote when you type “> ”.
  - Keymaps with the base bindings and custom bindings for common mark and node types, 
    - such as mod-i to enable emphasis and ctrl-shift-1 to make the current textblock a heading.
  - The drop cursor and gap cursor plugins.
  - The undo history.
  - A menu bar, with menu items for common tasks and schema elements.

## [Dinos in the document](https://prosemirror.net/examples/dino/)

- ProseMirror allows you to define your own schemas, which includes defining custom document elements.
- First, define a command that handles dinosaur insertion.
- Next, create menu items that call our command.

## [Friendly Markdown](https://prosemirror.net/examples/markdown/)

- you can drop in ProseMirror as an alternative input editor. 
  - People can even switch between both views as they are editing!

## [Tooltip](https://prosemirror.net/examples/tooltip/)

- I'm using ‘tooltip’ to mean a small interface element hovering over the rest of the interface. 
- There are two common ways to implement tooltips in ProseMirror. 
- The easiest is to insert widget decorations and absolutely position them, relying on the fact that if you don't specify an explicit position (as in a `left` or `bottom` property), such elements are positioned at the point in the document flow where they are placed. 
  - This works well for tooltips that correspond to a specific position.
- If you want to position something above the selection, or you want to animate transitions, or you need to be able to allow the tooltips to stick out of the editor when the editor's overflow property isn't visible (for example to make it scroll), then decorations are probably not practical. 
  - In such a case, you'll have to ‘manually’ position your tooltips.
- you can still make use of ProseMirror's update cycle to make sure the tooltip stays in sync with the editor state. 
  - u can use a **plugin view** to create a view component tied to the editor's life cycle.

## [Upload handling](https://prosemirror.net/examples/upload/)

- Some types of editing involve asynchronous operations, but you want to present them to your users as a single action. 
  - For example, when inserting an image from the user's local filesystem, you won't have access to the actual image until you've uploaded it and created a URL for it.
- Since the upload might take a moment, and the user might make more changes while waiting for it, 
  - the placeholder should move along with its context as the document is edited, 
  - and when the final image is inserted, it should be put where the placeholder has ended up by that time.
- The easiest way to do this is to make the placeholder a decoration, so that it only exists in the user's interface.

## [Schemas from scratch](https://prosemirror.net/examples/schema/)

- ProseMirror schemas provide something like a syntax for documents—they set down which structures are valid.
- A ProseMirror view can be mounted on any node, including inline nodes.

## [Writing your own menu](https://prosemirror.net/examples/menu/)

- The idea is, roughly, to create a number of user interface elements and tie them to commands. 
- One question is how to deal with commands that aren't always applicable—when you are in a paragraph, should the control for ‘make this a paragraph’ be shown? If so, should it be grayed out?
  - Depending on the number of items in your menu, and the amount of work required for determining whether they are applicable, this can get expensive. 
  - There's no real solution for this, except either keeping the number and complexity of the commands low, or not changing the look of your menu depending on state.
- The prosemirror-menu package works similarly, but adds support for things like simple drop-down menus and active/inactive icons (to highlight the strong button when strong text is selected).

## [Embedded code editor](https://prosemirror.net/examples/codemirror/)

- It can be useful to have the in-document representation of some node, such as a code block, math formula, or image, show up as a custom editor control specifically for such content. 
- **Node view**s are a ProseMirror feature that make this possible.
- In this example, we set up code blocks, as they exist in the basic schema, to be rendered as instances of CodeMirror, a code editor component. 
  - The general idea is quite similar to the footnote example, but instead of popping up the node-specific editor when the user selects the node, it is always visible.
- The adaptor code in the node view gets a bit more involved, because we are translating between two different document concepts—ProseMirror's tree versus CodeMirror's plain text.
- When the code editor is focused, we can keep the selection of the outer editor synchronized with the inner one, so that any commands executed on the outer editor see an accurate selection.
- Selections are also synchronized the other way, from ProseMirror to CodeMirror, using the view's `setSelection` method.
- A somewhat tricky aspect of nesting editor like this is handling cursor motion across the edges of the inner editor. 
  - This node view will have to take care of allowing the user to move the selection out of the code editor. 
  - For that purpose, it binds the arrow keys to handlers that check if further motion would ‘escape’ the editor, and if so, return the selection and focus to the outer editor.

## [Linter](https://prosemirror.net/examples/lint/)

- A document model that represents a smaller set of documents can be easier to reason about.
- The first part of this example is a function that, given a document, produces an array of problems found in that document.
  - We'll use the `descendants` method to easily iterate over all nodes in a document. 
  - Depending on the type of node, different types of problems are checked for.
- Each problem is represented as an object with a message, a start, and an end, so that they can be displayed and highlighted. 
  - The objects may also optionally have a fix method, which can be called (passing the view) to fix the problem.
- The way the plugin will work is that it'll keep a set of decorations that highlight problems and inserts an icon next to them. 
  - CSS is used to position the icon on the right side of the editor, so that it doesn't interfere with the document flow.
- Recomputing the whole set of problems, and recreating the set of decorations, on every change isn't very efficient

## [Editing footnotes](https://prosemirror.net/examples/footnote/)

- Footnotes seem like they should be inline nodes with content—they appear in between other inline content, but their content isn't really part of the textblock around them. 
- **Inline nodes with content are not handled well by the library**, at least not by default. 
  - You are required to write a **node view** for them, which somehow manages the way they appear in the editor.
- Footnotes in this example are drawn as numbers.
  - we'll rely on CSS to add the numbers.
  - Only when the node view is selected does the user get to see and interact with its content 
- What we'll do is pop up a little sub-editor, which is itself a ProseMirror view, with the node's content.
  - Transactions in this sub-editor are handled specially, in the `dispatchInner` method.
- What should happen when the content of the sub-editor changes? 
  - We could just take its content and reset the content of the footnote in the outer document to it, but that wouldn't play well with the undo history or collaborative editing.
  - A nicer approach is to simply apply the steps from the inner editor, with an appropriate offset, to the outer document.
  - We have to be careful to handle appended transactions, and to be able to handle updates from the outside editor without creating an infinite loop

## [Tracking changes](https://prosemirror.net/examples/track/)

- The first thing we need is a way to track the commit history. 
  - An editor plugin works well for this, since it can observe changes as they come in. 

## [Collaborative editing](https://prosemirror.net/examples/collab/#edit-Example)

- The editor below talks to a simple server-side service to allow real-time collaborative editing.
- The demo also (crudely) shows how ProseMirror can be used to implement something like out-of-line annotations. 
# library guide

## Introduction

- ProseMirror provides a set of tools and concepts for building rich text editors, using user interface inspired by WYSIWYG, but trying to avoid the pitfalls of that style of editing.
- The **main principle of ProseMirror** is that your code gets full control over the document and what happens to it. 
  - This document isn't a blob of HTML, but a custom data structure that only contains elements that you explicitly allow it to contain, in relations that you specified. 
  - All updates go through a single point, where you can inspect them and react to them.
- The core library is not an easy drop-in component
  - we are prioritizing modularity and customizability over simplicity
- There are four essential modules, which are required to do any editing at all, and a number of extension modules
  - model, state, view, transform

```JS
// my first editor
import { schema } from "prosemirror-schema-basic"
import { EditorState } from "prosemirror-state"
import { EditorView } from "prosemirror-view"

let state = EditorState.create({ schema })
let view = new EditorView(document.body, { state })
```

- ProseMirror requires you to specify a `schema` that your document conforms to, so the first thing this does is import a module with a basic schema in it.
  - That schema is then used to create a state, which will generate an empty document conforming to the schema, and a default selection at the start of that document. 
- Finally, a view is created for the state, and appended to `document.body`. 
  - This will render the state's document as an editable DOM node, and generate state transactions whenever the user types into it.
  - 但这个例子过于简单，按enter键不会换行

- Transactions/updating
- When the user types, or otherwise interacts with the view, it generates ‘state transactions’. 
  - What that means is that it does not just modify the document in-place and implicitly update its state in that way. 
  - Instead, **every change causes a transaction to be created**, which describes the changes that are made to the state, and can be applied to create a new state, which is then used to update the view.
- By default this all happens under the cover, but you can hook into by writing plugins or configuring your view.
- Every state update has to go through `updateState()`, 
  - and every normal editing update will happen by dispatching a transaction.

- Plugins/extending
- Plugins are used to extend the behavior of the editor and editor state in various ways. 
  - Some are relatively simple, like the keymap plugin
  - Others are more involved, like the history plugins
  - Plugins are registered when creating a state (because they get access to state transactions). 

- Commands/editing
- Most editing actions are written as commands which can be bound to keys, hooked up to menus, or otherwise exposed to the user.
  - prosemirror-commands package provides a number of basic editing commands, along with a minimal keymap that you'll probably want to enable to have things like enter and delete do the expected thing in your editor.

- Content/doc
- A state's document lives under its `doc` property. 
  - This is a read-only data structure, representing the document as a hierarchy of nodes, somewhat like the browser DOM. 
- When initializing a state, you can give it an initial document to use. 
  - In that case, the `schema` field is optional, since the schema can be taken from the document.
  - 初始化创建state对象时，若提供了doc，就可以不提供schema
  - doc: DOMParser.fromSchema(schema).parse(content)

## Documents

- ProseMirror defines its own data structure to represent content documents. 

- Structure
- A ProseMirror document is a node, which holds a fragment containing zero or more child nodes.
  - This is a lot like the browser DOM, in that it is recursive and tree-shaped. 
  - But it differs from the DOM in the way it stores inline content.
- in ProseMirror, the **inline content is modeled as a flat sequence, with the markup attached as metadata to the nodes**.
  - It allows us to represent positions in a paragraph using a character offset rather than a path in a tree, 
  - and makes it easier to perform operations like splitting or changing the style of the content without performing awkward tree manipulation.
- This also means **each document has one valid representation**. 
  - Adjacent text nodes with the same set of marks are always combined together, 
  - and empty text nodes are not allowed. 
  - The order in which marks appear is specified by the schema.
- So **a ProseMirror document is a tree of block nodes**, 
  - with most of the leaf nodes being `textblocks`, which are block nodes that contain text. 
  - You can also have leaf blocks that are simply empty, for example a horizontal rule or a video element.
- Node objects come with a number of properties that reflect the role they play in the document
  - `isBlock` and `isInline` tell you whether a given node is a block or inline node.
  - `inlineContent` is true for nodes that expect inline nodes as content.
  - `isTextblock` is true for block nodes with inline content.
  - `isLeaf` tells you that a node doesn't allow any content.
- So a typical `paragraph` node will be a textblock, 
  - whereas a `blockquote` might be a block element whose content consists of other blocks. 
  - Text, hard breaks, and inline images are inline leaf nodes, 
  - and a horizontal rule node would be an example of a block leaf node.

- Identity and persistence
- Another important difference between a DOM tree and a ProseMirror document is the way the objects that represent nodes behave.
  - In the DOM, nodes are mutable objects with an identity, which means that a node can only appear in one parent node, and that the node object is mutated when it is updated.
  - In ProseMirror, nodes are simply values, and should be approached much as you'd approach the value
- So it is with pieces of ProseMirror documents. 
  - They don't change, but can be used as a starting value to compute a modified piece of document. 
  - They don't know what data structures they are part of, but can be part of multiple structures, or even occur multiple times in a single structure. 
  - They are values, not stateful objects.
- This means that **every time you update a document, you get a new document value**. 
  - That document value will share all sub-nodes that didn't change with the original document value, making it relatively cheap to create.
  - It makes it impossible to have an editor in an invalid in-between state during an update
  - It also makes it easier to reason about documents in a somewhat mathematical way

- Data structures
- Each node is represented by an instance of the `Node` class. 
  - It is tagged with a type, which knows the node's name, the attributes that are valid for it, and so on. 
  - Node types (and mark types) are created once per schema, and know which schema they are part of.
- The content of a node is stored in an instance of `Fragment`, which holds a sequence of nodes. 
  - Even for nodes that don't have or don't allow content, this field is filled (with the shared empty fragment).
- Some node types allow attributes, which are extra values stored with each node.
- inline nodes hold a set of active marks—things like emphasis or being a link—which are represented as an array of `Mark` instances.
- A full document is just a node. 
  - The document content is represented as the top-level node's child nodes. 
  - Typically, it'll contain a series of block nodes, some of which may be textblocks that contain inline content. 
  - But the top-level node may also be a textblock itself, so that the document contains only inline content.
- What kind of node is allowed where is determined by the document's schema. 
  - To programmatically create nodes, you must go through the schema

```JS
// 手动创建Node对象

import { schema } from "prosemirror-schema-basic"

// (The null arguments are where you can specify attributes, if necessary.)

// node(type, attrs, content) Create a node in this schema

let doc = schema.node("doc", null, [
  schema.node("paragraph", null, [schema.text("One.")]),
  schema.node("horizontal_rule"),
  schema.node("paragraph", null, [schema.text("Two!")])
])
```

- Indexing
- ProseMirror nodes support two types of indexing
  - they can be treated as trees, using offsets into individual nodes, 
  - or they can be treated as a flat sequence of tokens.
- tree allows you to do things similar to what you'd do with the DOM
  - interacting with single nodes, directly accessing child nodes using the `child` method and `childCount`, writing recursive functions that scan through a document(`descendants/nodesBetween`)
- flat tokens are more useful when addressing a specific position in the document. 
  - It allows any document position to be represented as an integer—the index in the token sequence. 
  - These tokens don't actually exist as objects in memory—they are just a counting convention
  - but the document's tree shape, along with the fact that each node knows its size, is used to make by-position access cheap.
- Each node has a `nodeSize` property that gives you the size of the entire node, and you can access `.content.size` to get the size of the node's content. 
  - TextNode的`content`为空数组`[]`，文本内容保存在`text`属性中
  - text nodes are different from other nodes, and don’t have a `type` or `attrs`. You’ll have to wrap them in some node if you want to use `setNodeMarkup`, or use mark add/remove steps if you want to change the set of marks on the text.
- Interpreting such position manually involves quite a lot of counting. 
  - You can call `Node.resolve` to get a more descriptive data structure for a position.
  - This data structure will tell you what the parent node of the position is, what its offset into that parent is, what ancestors the parent has, and a few other things.
- Take care to distinguish between child indices (as per `childCount`), document-wide positions, and node-local offsets.

- Slices 测试索引
- To handle things like copy-paste and drag-drop, it is necessary to be able to talk about a slice of document, i.e. the content between two positions. 
- The `Slice` data structure stores a fragment along with an open depth on both sides. 
  - You can use the slice method on nodes to cut a slice out of a document.

- Since nodes and fragments are persistent, you should never mutate them. 
- Most of the time, you'll **use transformations to update documents, and won't have to directly touch the nodes**. 
  - These also leave a record of the changes, which is necessary when the document is part of an editor state.
- To manually create an updated version of a whole document, you'll usually want to use `Node.replace`, which replaces a given range of the document with a slice of new content. 
  - To update a node shallowly, you can use its `copy` method, which creates a similar node with new content. 
  - `Fragment`s also have various updating methods, such as `replaceChild` or `append`.

## Schemas

- Each ProseMirror document has a `schema` associated with it. 
  - The `schema` describes the kind of nodes that may occur in the document, and the way they are nested. 
  - 描述了文档中允许的nodes、marks、serialize、deserialize

- Node Types
- Every node in a document has a `type`, which represents its semantic meaning and its properties, such as the way it is rendered in the editor.
- When you define a `schema`, you enumerate the node types that may occur within it, describing each with a `spec` object
- Every `schema` must at least define a top-level node type (defaults to `doc`), and a `text` type for text content.

- Content Expressions
- The strings in the `content` fields are called content expressions.
  - They control what sequences of child nodes are valid for this node type.
  - Such expressions can be combined to create a sequence
- Some groups of element types will appear multiple times in your schema
  -  You can create a node group by giving your node specs a `group` property, and then refer to that group by its name in your expressions.

```JS
// Here "block+" is equivalent to "(paragraph | blockquote)+".

const groupSchema = new Schema({
  nodes: {
    doc: { content: "block+" },
    paragraph: { group: "block", content: "text*" },
    blockquote: { group: "block", content: "block+" },
    text: {}
  }
})
```

- It is recommended to always require at least one child node in nodes that have block content, 
  - because browsers will completely collapse the node when it's empty, making it rather hard to edit.
- The order in which your nodes appear in an or-expression is significant. 
  - When creating a default instance for a non-optional node, the first type in the expression will be used.
- Not every node-manipulating function in the library checks that it is dealing with valid content—higher level concepts like transforms do, 
  - but primitive node-creation methods usually don't and instead put the responsibility for providing sane input on their caller.
  - It is perfectly possible to use, for example `NodeType.create`, to create a node with invalid content. 

- Marks
- Marks are used to add extra styling or other information to inline content. 
  - A schema must declare all mark types it allows in its schema. 
  - Mark types are objects much like node types, used to tag mark objects and provide additional information about them.
- By default, nodes with inline content allow all marks defined in the schema to be applied to their children.

- Attributes
- The document schema also defines which attributes each node or mark has. 
  - If your node type requires extra node-specific information to be stored, such as the level of a heading node, that is best done with an attribute.
- Attribute sets are represented as plain objects with a predefined (per node or mark) set of properties holding any JSON-serializeable values.
- When you don't give a default value for an attribute, an error will be raised when you attempt to create such a node without specifying that attribute.
  - That will also make it impossible for the library to generate such nodes as filler to satisfy schema constraints during a transform or when calling createAndFill.
- in order to be able to enforce the schema constraints, the editor needs to be able to generate empty nodes to fill missing pieces in the content.

- Serialization and Parsing
- In order to be able to edit them in the browser, it must be possible to represent document nodes in the browser DOM. 
  - The easiest way to do that is to include information about each node's DOM representation in the schema using the `toDOM` field in the node spec.
  - This field should hold a function that, when called with the node as argument, returns a description of the DOM structure for that node. 
  - This may either be a direct DOM node or an array describing it
- Mark specs allow a similar `toDOM` method, 
  - but they are required to render as a single tag that directly wraps the content, so the content always goes directly in the returned node, and the hole doesn't need to be specified.

- You'll also often need to parse a document from DOM data, for example when the user pastes or drags something into the editor. 
  - you are encouraged to include parsing information directly in your schema with the `parseDOM` property.
- This may list an array of parse rules, which describe DOM constructs that map to a given node or mark.
- When a schema includes `parseDOM` annotations, you can create a `DOMParser` object for it with `DOMParser.fromSchema`. 
  - This is done by the editor to create the default clipboard parser, but you can also override that.
- Documents also come with a built-in JSON serialization format.

- Extending a schema
- The `nodes` and `marks` options passed to the Schema constructor take `OrderedMap` objects as well as plain JavaScript objects. 
  - Such maps support a number of methods to conveniently create updated versions.

## Document transformations

- Transforms are central to the way ProseMirror works. 
  - They form the basis for transactions, and are what makes history tracking and collaborative editing possible.
- Immutable data structures really do lead to simpler code
  - the main thing the transform system does is to leave a trail of updates, in the form of values that represent the individual steps taken to go from an old version of the document to a new one.
- More generally, it is very useful for editor plugins to be able to inspect and react to each change as it comes in, in order to keep their own state consistent with the rest of the editor state.

- Steps
- Updates to documents are decomposed into steps that describe an update. 
  - Examples of steps are `ReplaceStep` to replace a piece of a document, or `AddMarkStep` to add a mark to a given range.
- A step can be applied to a document to produce a new document.
- Applying a step is a relatively straightforward process
  - That means applying a step can fail, for example if you try to delete just the opening token of a node, that would leave the tokens unbalanced, which isn't a meaningful thing you can do. 
  - This is why `apply` returns a result object, which holds either a new document, or an error message.

- Transforms
- An editing action may produce one or more steps. 
- The most convenient way to work with a sequence of steps is to create a `Transform` object 
  - (or, if you're working with a full editor state, a `Transaction`, which is a subclass of `Transform`).
- Most transform methods return the transform itself, for convenient chaining

```JS
// 创建Step对象然后返回一个新的document
console.log(myDoc.toString()); // → p("hello")
// A step that deletes the content between positions 3 and 5
let step = new ReplaceStep(3, 5, Slice.empty);
let result = step.apply(myDoc);
console.log(result.doc.toString()) // → p("heo")

// 应用transform执行一系列的steps，返回新的document
let tr = new Transform(myDoc);
tr.delete(5, 7); // Delete between position 5 and 7
tr.split(5); // Split the parent node at position 5
console.log(tr.doc.toString()) // The modified document
console.log(tr.steps.length) // → 2

tr.delete(5, 7).split(5) // ok too
```

- Mapping
- When you make a change to a document, positions pointing into that document may become invalid or change meaning. 
- We often do need to preserve positions across document changes, 
  - steps can give you a `map()` that can convert between positions in the document before and after applying the step.
  - map(old-pos) will return new-pos
- Transform objects automatically accumulate a set of maps for the steps in them, using an abstraction called Mapping, 
  - which collects a series of step maps and allows you to `map` through them in one go.
- There are cases where it's not entirely clear what a given position should be mapped to. 
  - `map` method on step maps and mappings accepts a second parameter, `bias`, which you can set to `-1` to keep your position in place when content is inserted on top of it.
- The reason that individual steps are defined as small, straightforward things is that it makes this kind of mapping possible, along with inverting steps in a lossless way, and mapping steps through each other's position maps.

- Rebasing
- Rebasing, in the simple case, is the process of taking two steps that start with the same document, and transform one of them so that it can be applied to the document created by the other instead. 

```JS
stepA(doc) = docA
stepB(doc) = docB
stepB(docA) = MISMATCH!
  rebase(stepB, mapA) = stepB '
stepB '(docA) = docAB
```

- Steps have a `map` method, which, given a mapping, maps the whole step through it. 
- Even if you have rebased a step, there is no guarantee that it can still be validly applied to the current document. 
  - The appropriate response to this is usually just to drop the step.

## The editor state

- There are the three main components of a ProseMirror state, and exist on state objects as `doc`, `selection`, and `storedMarks`.
  - But plugins may also need to store state
  - This is why the set of active plugins is also stored in the state, and these plugins can define additional slots for storing their own state.

- Selection
- ProseMirror supports several types of selection (and allows 3rd-party code to define new selection types).
- Selections are represented by instances of (subclasses of) the `Selection` class. 
  - Like documents and other state-related values, they are immutable
  - to change the selection, you create a new selection object and a new state to hold it.
- Selections have, at the very least, a start (`.from`) and an end (`.to`), as positions pointing into the current document. 
  - Many selection types also distinguish between the `anchor` (unmoveable) and `head` (moveable) side of the selection, so those are also required to exist on every selection object.
- The most common type of selection is a text selection, 
  - which is used for regular cursors (when `anchor` and `head` are the same) or selected text. 
  - Both endpoints of a text selection are required to be in inline positions, i.e. pointing into nodes that allow inline content.
- The core library also supports node selections, where a single document node is selected, which you get, for example, when you ctrl/cmd-click a node. 
  - Such a selection ranges from the position directly before the node to the position directly after it.

- Transactions
- During normal editing, new states will be derived from the state before them.
- **State updates happen by applying a transaction** to an existing state, producing a new state. 
  - Conceptually, they happen in a single shot: given the old state and the transaction, a new value is computed for each component of the state, 
  - and those are put together in a new state value.
- `Transaction` is a subclass of `Transform`, and inherits the way it builds up a new document by applying steps to an initial document. 
  - In addition to this, transactions track selection and other state-related components, and get some selection-related convenience methods such as `replaceSelection`.
- By default, the old selection is mapped through each step to produce a new selection, 
  - but it is possible to use `setSelection` to explicitly set a new selection.
- Similarly, the set of active marks is automatically cleared after a document or selection change, and can be set using the `setStoredMarks` or `ensureMarks` methods.
- `scrollIntoView` method can be used to ensure that, the next time the state is drawn, the selection is scrolled into view. 
- Like `Transform` methods, many `Transaction` methods return the transaction itself, for convenient chaining.

- ### Plugins
- When creating a new state, you can provide an array of plugins to use. 
  - These will be stored in the state and any state that is derived from it, and can influence both the way transactions are applied and the way an editor based on this state behaves.
- When a plugin needs its own state slot, that is defined with a `state` property
- Because the editor state is a persistent (immutable) object, and plugin state is part of that object, plugin state values must be immutable. 
  - I.e. their `apply` method must return a new value, rather than changing the old
- It is often useful for plugins to add some extra information to a transaction. 
  - For this purpose, transactions allow `metadata` to be attached to them. 

```JS
let transactionCounter = new Plugin({
  state: {
    init() { return 0 },
    apply(tr, value) {
      if (tr.getMeta(transactionCounter)) return value
      else return value + 1
    }
  }
})

function markAsUncounted(tr) {
  tr.setMeta(transactionCounter, true)
}
```

## The view component

- A ProseMirror editor view is a user interface component that displays an editor state to the user, and allows them to perform editing actions on it.
- The definition of editing actions used by the core view component is rather narrow, such as typing, clicking, copying, pasting, and dragging
  - things like displaying a menu, or even providing a full set of key bindings, lie outside of the responsibility of the core view component, and have to be arranged through plugins.

- Editable DOM
- Browsers allow us to specify that some parts of the DOM are editable, which has the effect of allowing focus and a selection in them, and making it possible to type into them. 
- The view creates a DOM representation of its document (using your schema's `toDOM` methods by default), and makes it editable. 
  - When the editable element is focused, ProseMirror makes sure that the DOM selection corresponds to the selection in the editor state.
- It also registers event handlers for many DOM events, which translate the events into the appropriate transactions.
- Many events are also let through as they are, and only then reinterpreted in terms of ProseMirror's data model. 
- The browser is quite good at cursor and selection placement 
  - so most cursor-motion related keys and mouse actions are handled by the browser, after which ProseMirror checks what kind of text selection the current DOM selection would correspond to. 
  - If that selection is different from the current selection, a transaction that updates the selection is dispatched.
- Even typing is usually left to the browser, 
  - because interfering with that tends to break spell-checking, autocapitalizing on some mobile interfaces, and other native features. 
  - When the browser updates the DOM, the editor notices, re-parses the changed part of the document, and translates the difference into a transaction.

- ### data flow
- the editor view displays a given editor state, 
- and when something happens, it creates a transaction and broadcasts this. 
- This transaction is then, typically, used to create a new state, which is given to the view using its `updateState` method.
- This creates a straightforward, cyclic data flow, 
  - as opposed to the classic approach (in the JavaScript world) of a host of imperative event handlers, which tends to create a much more complex web of data flows.
- It is possible to ‘intercept’ transactions as they are dispatched with the `dispatchTransaction` prop, in order to wire this cyclic data flow into a larger cycle—if your whole app is using a data flow model like this, 
  - as with Redux and similar architectures, you can integrate ProseMirror's transactions in your main action-dispatching cycle, and keep ProseMirror's state in your application ‘store’.

```JS
// The app's state
let appState = {
  editor: EditorState.create({ schema }),
  score: 0
};

let view = new EditorView(document.body, {
  state: appState.editor,
  dispatchTransaction(transaction) {

    // 这里会更新appState
    dispatchUpdate({ type: "EDITOR_TRANSACTION", transaction })
  }
});

// A crude app state update function, which takes an update object, updates the `appState`, and then refreshes the UI.
function dispatchUpdate(event) {
  if (event.type == "EDITOR_TRANSACTION") {
    appState.editor = appState.editor.apply(event.transaction)
  } else if (event.type == "SCORE_POINT") {
    appState.score++
  }

  draw();
}

// An even cruder drawing function
function draw() {
  document.querySelector("#score").textContent = appState.score

  // 用最新的appState更新view
  view.updateState(appState.editor)
}
```

- Efficient updating
- One way to implement `updateState` would be to simply redraw the document every time it is called. 
  - But for large documents, that would be really slow.
- Since, at the time of updating, the view has access to both the old document and the new, it can compare them, and leave the parts of the DOM that correspond to unchanged nodes alone. 
  - ProseMirror does this, allowing it to do very little work for typical updates.
- In some cases, like updates that correspond to typed text, which was already added to the DOM by the browser's own editing actions, ensuring the DOM and state are coherent(在一起的，条理分明的) doesn't require any DOM changes at all. (When such a transaction is canceled or modified somehow, the view will undo the DOM change to make sure the DOM and the state remain synchronized.)
- the DOM selection is only updated when it is actually out of sync with the selection in the state, to avoid disrupting the various pieces of ‘hidden’ state that browsers keep along with the selection (such as that feature where when you arrow down or up past a short line, your horizontal position goes back to where it was when you enter the next long line).

- Props
- Props are like parameters to a UI component. 
  - Ideally, the set of props that the component gets completely defines its behavior.
-  The `updateState` method is just a shorthand to updating the `state` prop.
- Plugins are also allowed to declare props, except for `state` and `dispatchTransaction`, which can only be provided directly to the view.
- When a given prop is declared multiple times, how it is handled depends on the prop. 
  - In general, directly provided props take precedence, after which each plugin gets a turn, in order. 
  - For some props, such as `domParser`, the first value that is found is used, and others are ignored. 
  - For handler functions that return a boolean to indicate whether they handled the event, the first one that returns `true` gets to handle the event. 
  - And finally, for some props, such as attributes (which can be used to set attributes on the editable DOM node) and decorations (which we'll get to in the next section), the union of all provided values is used.

- ### Decorations
- Decorations give you some control over the way the view draws your document. 
- They are created by returning values from the `decorations` prop, and come in three types
  - Node decorations 
    - add styling or other DOM attributes to a single node's DOM representation.
  - Inline decorations 
    - add styling or attributes, much like node decorations, but to all inline nodes in a given range.
  - Widget decorations 
    - insert a DOM node, which isn't part of the actual document, at a given position.
- In order to be able to efficiently draw and compare decorations, they need to be provided as a decoration set (which is a data structure that mimics the tree shape of the actual document)
- When you have a lot of decorations, recreating the set on the fly for every redraw is likely to be too expensive.
  - the **recommended way to maintain your decorations is to put the decoration set in your plugin's `state`**, map it forward through changes, and only change it when you need to.
- When a transaction is applied to the state, the plugin state's `apply` method maps the decoration set forward, causing the decorations to stay in place and ‘fit’ the new document shape. 
  - The mapping method is (for typical, local changes) made efficient by exploiting the tree shape of the decoration set
  - only the parts of the tree that are actually touched by the changes need to be rebuilt.
- In a real-world plugin, the `apply` method would also be the place where you add or remove decorations based on new events, 
  - possibly by inspecting the changes in the transaction, or based on plugin-specific metadata attached to the transaction.
- the `decorations` prop simply returns the plugin state, causing the decorations to show up in the view.

- ### Node views
- There is one more way in which you can influence the way the editor view draws your document. 
- Node views make it possible to define a sort of miniature UI components for individual nodes in your document. 
  - They allow you to render their DOM, define the way they are updated, and write custom code to react to events.

```JS
let view = new EditorView({
  state,
  nodeViews: {
    // image(node) { return new ImageView(node) }
    image(node, view, getPos) { return new ImageView2(node, view, getPos) }
  }
})

class ImageView {
  constructor(node) {
    // The editor will use this as the node's DOM representation
    this.dom = document.createElement("img")
    this.dom.src = node.attrs.src
    this.dom.addEventListener("click", e => {
      console.log("You clicked me!")
      e.preventDefault()
    })
  }

  stopEvent() { return true }
}

class ImageView2 {
  constructor(node, view, getPos) {
    this.dom = document.createElement("img")
    this.dom.src = node.attrs.src
    this.dom.alt = node.attrs.alt
    this.dom.addEventListener("click", e => {
      e.preventDefault()
      let alt = prompt("New alt text:", "")
      if (alt) view.dispatch(view.state.tr.setNodeMarkup(getPos(), null, {
        src: node.attrs.src,
        alt
      }))
    })
  }

  stopEvent() { return true }
}
```

- to create a transaction that changes a node, you first need to know where that node is. 
  - To help with that, node views get passed a getter function that can be used to query their current position in the document. 
  - `setNodeMarkup` is a method that can be used to change the type or set of attributes for the node at a given position. 
- When a node is updated, the default behavior is to leave its outer DOM structure intact and compare its children to the new set of children, updating or replacing those as needed.
  - A node view can override this with custom behavior, which allows us to do something like changing the class of a paragraph based on its content.
  - Images never have content, so no need to handle
- Node views support two approaches to handling content: 
  - you can let the ProseMirror library manage it, or you can manage it entirely yourself. 
  - If you provide a `contentDOM` property, the library will render the node's content into that, and handle content updates. 
  - If you don't, the content becomes a black box to the editor, and how you display it and let the user interact with it is entirely up to you.

```JS
let view = new EditorView({
  state,
  nodeViews: {
    paragraph(node) { return new ParagraphView(node) }
  }
})

class ParagraphView {
  constructor(node) {

    // editor会将content渲染到contentDOM之中
    this.dom = this.contentDOM = document.createElement("p");
    if (node.content.size == 0) this.dom.classList.add("empty")
  }

  update(node) {
    // 先判断是要更新的node类型
    if (node.type.name != "paragraph") { return false }
    if (node.content.size > 0) {
      this.dom.classList.remove("empty");
    } else {
      this.dom.classList.add("empty");
    }

    // 确认要更新node
    return true
  }
}
```

## Commands

- a command is a function that implements an editing action, 
  - which the user can perform by pressing some key combination or interacting with the menu.
- For practical reasons, commands have a slightly convoluted(复杂的，晦涩难懂的) interface. 
- In their simple form, they are functions taking an editor state and a dispatch function (`EditorView.dispatch` or some other function that takes transactions), and return a boolean.
  - When a command isn't applicable, it should return false and do nothing. 
  - When it is, it should dispatch a transaction and return true. 
  - This is used, for example, by the keymap plugin to stop further handling of key events when the command bound to that key has been applied.

- To be able to query whether a command is applicable for a given state, without actually executing it, the `dispatch` argument is optional—commands should simply return true without doing anything when they are applicable but no `dispatch` argument is given. 
  - To figure out whether a selection can currently be deleted, you'd call `deleteSelection(view.state, null)`
  - In this form, commands do not get access to the actual editor view—most commands don't need that

```JS
function deleteSelection(state, dispatch) {
  if (state.selection.empty) return false;
  if (dispatch) dispatch(state.tr.deleteSelection());
  return true;
}
```

- But some commands do need to interact with the DOM—they might need to query whether a given position is at the end of a textblock, or want to open a dialog positioned relative to the view. 
  - For this purpose, most plugins that call commands will give them a third argument, which is the whole view.
- **commands don't have to dispatch a transaction**
  - they are called for their side effect, which is usually to dispatch a transaction, but may also be something else, such as popping up a dialog.
- When possible, different behavior, even when usually bound to a single key, is put in different commands. 
- The utility function `chainCommands` can be used to combine a number of commands—they will be tried one after the other until one return true.
- The commands module also exports a number of command constructors, such as `toggleMark`, 
  - which takes a mark type and optionally a set of attributes, and returns a command function that toggles that mark on the current selection.

## Collaborative editing

- Real-time collaborative editing allows multiple people to edit the same document at the same time.
- Changes they make are applied immediately to their local document, 
  - and then sent to peers, which merge in these changes automatically (without manual conflict resolution), 
  - so that editing can proceed uninterrupted, and the documents keep converging.
- ProseMirror's collaborative editing system employs a central authority which determines in which order changes are applied.
- The role of the central authority is actually rather simple. 
  - Track a current document version
  - Accept changes from editors, and when these can be applied, add them to its list of changes
  - Provide a way for editors to receive changes since a given version
- The `collab` module exports a `collab` function which returns a plugin that takes care of tracking local changes, receiving remote changes, and indicating when something has to be sent to the central authority.
- Of course, with asynchronous data channels (such as long polling in the collab demo or web sockets), you'll need somewhat more complicated communication and synchronization code. 
- And you'll probably also want your authority to start throwing away steps at some point, so that its memory consumption doesn't grow without bound. 
- But the general approach is fully described by this little example.
# prosemirror-keymap
- Create a keymap plugin for the given set of bindings.
- Key identifiers are based on the strings that can appear in KeyEvent.key
- Modifiers can be given in any order. 
  - Shift- (or s-), Alt- (or a-), Ctrl- (or c- or Control-) and Cmd- (or m- or Meta-) are recognized. 
  - For characters that are created by holding shift, the Shift- prefix is implied, and should not be added explicitly.
- You can use `Mod-` as a shorthand for `Cmd-` on Mac and `Ctrl-` on other platforms.
- You can add multiple keymap plugins to an editor. 
  - The order in which they appear determines their precedence (the ones early in the array get to dispatch first).
# prosemirror-gapcursor
- By default, gap cursor are only allowed in places where the default content node (in the schema content constraints) is a textblock node. 
  - You can customize this by adding an `allowGapCursor` property to your node specs
- The cursor is drawn as an element with class `ProseMirror-gapcursor`. 
  - You can either include `style/gapcursor.css` from the package's directory or add your own styles to make it visible.
- Gap cursor selections are represented using `GapCursor` class. 
  - Its `$anchor` and `$head` properties both point at the cursor position.
# remirror-docs

## overview

- remirror was started as a personal challenge. Would it be possible to build an editor that combined great performance with ease of use?
  - ProseMirror was picked as the best choice for the core editor layer.
  - The second decision was to base the structure of the editor on blocks of functionality called Extensions
- Every single part of the editor is controlled by extensions. 
  - For example, the core (Schema) is managed by a built-in extension.
- Multi-framework support is being added in the future. 
  - Currently the focus is on React and the DOM.

- Features
  - A11y focused and ARIA compatible.
  - I18n support via lingui.
  - Collaborative editing with yjs.
  - 30+ extensions for creating fully customized editing experiences.
  - Zero configuration support for Server Side Rendering (SSR).
  - Cross platform and cross-framework, with an Angular solution coming later this year.
# ref
