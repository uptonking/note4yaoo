---
title: lib-editor-bangle-dev
tags: [bangle-editor, editor, lib]
created: '2021-06-27T18:43:46.836Z'
modified: '2021-06-27T18:44:15.023Z'
---

# lib-editor-bangle-dev

# guide

- features
  - plenty of components to help you get started
  - uses Prosemirror to provide a powerful API which can help you build the next google docs including collaboration.
  - Bangle is written in a framework agnostic way
  - Bangle comes with first party React support and React components
  - fast for rendering long documents
# discuss
- ## Bangle.dev: higher level Prosemirror components
- https://discuss.prosemirror.net/t/bangle-dev-higher-level-prosemirror-components/3363
- I am super excited to share with you all something I have been working as a side project for the past 1.5 years.
- highlights of bangle.dev
  - React support: While the core is written in vanillaJS, I built a React wrapper to create some pretty UI using NodeViews without much friction.
  - Doesn’t add more abstractions: Looking at other libraries which try to blanket Prosemirror’s API with their own, I realized that it is not a great approach, as the moment you try to write a moderately complex app, you end up hitting the walls of these libraries. BangleJS focuses on providing code as components with minimal abstraction over Prosemirror.
  - There are tons of components within @banglejs 
- Do I understand correctly that the core is mostly a set of tools for composing configurations more easily than with raw ProseMirror, or is there more going on? How does a `BangleEditorState` differ from a raw `EditorState`?
  - The goal of BangleJS is to provide pluggable opinionated components to build a reasonably good editor quickly. As soon as you hit the wall with these components, BangleJS doesn’t stand in your way to build complex components that leverages Prosemirror’s API.
- `BangleEditorState`  is a thin wrapper which does the following:
- Accepts:
  - Nested array of PM Plugins
  - Array of objects where one of the field is schema this is where you put the Prosemirror Node/Mark spec of the component.
  - Initial content of the doc
  - pipes anything else directly to the PM `EditorState.create` static method
- Processes:
  - Flattens the deeply nested array of plugins.
  - does same basic sanity checks and adds some reasonable default like doc, paragraph, text, history etc
- Outputs:
  - An instance where the field pmState points to the PM EditorState instance built using the inputs.
- I have intentionally kept the `EditorState` initialization separate from `EditorView`, just like Prosemirror so that if one fancies a Bangle component to be used in an existing Prosemirror app, they can do.
  - This has only been possible due to amazing level of modularity in Prosemirror 

- ## Feedback on an ideal React interface
- https://discuss.prosemirror.net/t/feedback-on-an-ideal-react-interface/3345
- I have been working on a higher level tool kit for Prosemirror and wanted to get some feedback on some ideas.
  - Separation of schema and plugins
  - Using React hooks
  - This is not really related to React but would love to bounce some ideas on this. The plugin architecture of PM works great, but PM leaves ambiguity on how to extend and share specs and plugins.
# docs
- Each of the core component of Bangle comes baked in with markdown shortcuts (you can disable them if you want).
  - 支持export markdown

- Try dragging the image around.

- Bangle allows exporting the editor state in different ways:
  - markdown, json, html

- Collapsing of a Heading component allows you to reduce the visual clutter in your document. 
  - Bangle implements it by hiding every node after the selected heading until a heading of the same level or higher is not encountered.

- Bangle component
  - A component is an object which hold smaller related things to form the building block of your editor.
- SpecRegistry
  - an object that declaratively defines how your editor behaves, looks, its relationship with other entities and the parsing/serialization aspect of it.

- Custom Rendering
  - The simplest option is to look at the `style.css` of a component and override it with your own.
  - If you only care about the HTML semantics you can modify the `toDOM` and `parseDOM` in your `spec.schema`. 
  - If you want all the bells and whistles, do it with the help of the `NodeView` API

- Bangle uses the concept of Commands which is borrowed from Prosemirror to allow for making controlled changes to your editor.
