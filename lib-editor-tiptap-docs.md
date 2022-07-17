---
title: lib-editor-tiptap-docs
tags: [docs, editor, headless, tiptap]
created: 2021-06-02T17:11:49.645Z
modified: 2021-06-02T17:12:12.347Z
---

# lib-editor-tiptap-docs

> A headless, framework-agnostic and extendable WYSIWYG rich text editor, based on ProseMirror.

# docs

## quickstart-minimal

```JS
import { Editor as TiptapEditor } from 'https://cdn.skypack.dev/@tiptap/core?min';
import StarterKit from 'https://cdn.skypack.dev/@tiptap/starter-kit?min';

const editor = new TipTapEditor({
  element: document.querySelector('.element'),
  extensions: [
    StarterKit,
  ],
  content: '<p>Hello World :-)</p>',
});
```

## output

- You can store your content as a JSON object or as a good old HTML string.
- **tiptap doesn’t support Markdown as an input or output format**. 
  - Both, HTML and JSON, can have deeply nested structures, Markdown is flat.
  - tiptap’s strength is customization, that doesn’t work very well with Markdown.
  - Markdown standards vary.
  - There are enough packages to convert HTML to Markdown and vice-versa.

## styling

- tiptap is headless, that means there is no styling provided. 
  - That also means, you are in full control of how your editor looks. 
- Option 1: Style the plain HTML
- Option 2: Add custom classes with `HTMLAttributes` prop
- Option 3: Customize the HTML markup for extensions

## Custom extensions

- Every extension has an `extend()` method, which takes an object with everything you want to change or add to it.
- With the `renderHTML` function you can control how an extension is rendered to HTML.

- What’s available in `this`?
  - Those extensions aren’t classes, but you still have a few important things available in `this` everywhere in the extension
  - this.name/editor/type/option/parent

- addProseMirrorPlugins()
  - ProseMirror has a pretty powerful plugin API
  - You can wrap existing ProseMirror plugins in tiptap extensions with it

- NodeView
  - For advanced use cases, where you need to execute JavaScript inside your nodes, for example to render a sophisticated link preview, you need to learn about node views.
  - you need to return a parent DOM element, and a DOM element where the content should be rendered in. 

## Interactive node views

- Different types of node views
- Editable text
  - node views can have editable text, just like a regular node. 
  - The cursor will exactly behave like you would expect it from a regular node. 
  - Existing commands work very well with those nodes.
- Non-editable text
  - Nodes can also have text, which is not editable. 
  - The cursor can’t jump into those, but you don’t want that anyway. Users can add or delete them, but not delete single characters.
  - Statamic uses those for their Bard editor, which renders complex modules inside tiptap, which can have their own text inputs.
- Mixed content
  - You can even mix non-editable and editable text. 
  - That’s great to build complex things, and still use marks like bold and italic inside the editable content.
  - BUT, if there are other elements with non-editable text in your node view, the cursor can jump there. You can improve that with manually adding contenteditable="false" 

- Render a node view with JavaScript
  - Create a node extension
  - Register a new node view with `addNodeView()` function
  - Write your render function
  - Configure tiptap to use your new node extension

- Render a React component
- Create a node extension
- Create a React component
- Pass that component to the provided `ReactNodeViewRenderer(ReactComp)` (createPortal)
- Register it with `addNodeView()` function
- Configure tiptap to use your new node extension

- Even if you’re node view is pretty complex, the rendered HTML can be simple
  - Make sure it’s something distinguishable, so it’s easier to restore the content from the HTML. 
- The same applies to restoring the content. 
  - You can configure what markup you expect, that can be something completely unrelated to the node view markup. 
  - It just needs to contain all the information you want to restore.

- You can even update node attributes from your node view, with the help of the `getPos` prop passed to your render function
  - Dispatch a new transaction`state.tr.setNodeMarkup()` with an object of the updated attributes
- To add editable content to your node view, you need to pass a `contentDOM`, a container element for the content.
# api
- ProseMirror works with a strict Schema, which defines the allowed structure of a document. 
  - A document is a tree of headings, paragraphs and others elements, so called nodes. 
  - Marks can be attached to a node, e. g. to emphasize part of it. 
  - Commands change that document programmatically.

- The document is stored in a state. 
  - All changes are applied as transactions to the state. 
  - The state has details about the current content, cursor position and selection. 

- The editor provides a ton of commands to programmatically add or change content or alter the selection.

- nodes are just a type of content in that tree. 
  - Examples of nodes are paragraphs, headings, or code blocks. 
  - But nodes don’t have to be blocks. 
  - They can also be rendered inline with the text, for example for @mentions.

- Extensions add new capabilities to tiptap
  - Those can’t add to the schema, but can add functionality or change the behaviour of the editor.
  - There are also some extensions with more capabilities. We call them nodes and marks which can render content in the editor.
- We recommend to start with customizing existing extensions first, and create your own extensions with the gained knowledge later.

- The `content` attribute defines exactly what kind of content the node can have. 
  - ProseMirror is really strict with that. 
  - That means, content which doesn’t fit the schema is thrown away. It expects a name or group as a string. 

- Nodes can be rendered inline, too. 
  - When setting `inline: true`, nodes are rendered in line with the text. 
  - That’s the case for mentions. The result is more like a mark, but with the functionality of a node. 
  - One difference is the resulting JSON document. 
  - Multiple marks are applied at once, inline nodes would result in a nested structure.

- Nodes with `atom: true` aren’t directly editable and should be treated as a single unit.
  - One example is the Mention extension, which somehow looks like text, but behaves more like a single unit. 
  - As this doesn’t have editable text content, it’s empty when you copy such node. Good news though, you can control that. 
