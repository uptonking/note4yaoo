---
title: lib-editor-codemirror-docs-examples-tutorials
tags: [codemirror, docs, examples, tutorials]
created: 2024-05-02T07:47:42.128Z
modified: 2024-05-02T07:48:04.213Z
---

# lib-editor-codemirror-docs-examples-tutorials

# guide

- docs-examples
  - huge document with several million lines
  - Decoration: influence the way the editor content is drawn
  - Undoable Effects
  - Split View: create multiple views from a single editor state
  - Extension: Zebra Stripes
  - Autocompletion: displaying input suggestions
  - Editor Panels: UI element shown above or below the editor
  - Gutters: vertical bars in front of the code
  - Tooltips: widgets floating over the content, aligned to some position in that content
  - Linter: it will call this source function when changes are made to the document
  - collab
  - moving selection
  - custom completion
  - single-line editor
  - markdown code-block syntax highlighting
  - merge view

- examples-repos
  - a
# examples

## [Configuration Example](https://codemirror.net/examples/config/)

- A CodeMirror editor's configuration lives in its state object.
- With facet inputs, order matters. 
  - The configuration resolves them in a specific order, and for most facets, that order matters. 
  - For example with event handlers, transaction filters, or keymaps, it determines which gets called first. 
  - With settings like the line separator or indentation unit, the value with the highest precedence wins.
- When a configuration is resolved, by default, the tree of nested arrays of extensions are simply flattened into a sequence. Inputs to a given facet are then collected in the order they appear in that sequence.

- all extensions in a higher-precedence bucket come before all extensions in a lower-precedence one.

- In order to be able to partially reconfigure a tree of extensions, we need to divide it into compartments. 
  - Transactions can update the configuration by replacing the content of individual compartments.

- compartments may nest, and the extension tree produced by some plugin may use its own compartments to dynamically en- or disable some extensions.

- If you just need to dynamically derive the value of some facet from other aspects of the state, it is preferable to use `computed facets` instead of `reconfiguration`, since those are more efficient and easier to keep track of (they are a form of derived state, rather than adding new fundamental state).
  - if you have something like an extension that wants to conditionally enable another extension, locally declaring a compartment and reconfiguring that as needed works well.

- how to do a top-level reconfiguration. 
  - This is slightly different from just creating a new editor state, in that it'll preserve the content of state fields and compartments that exist in both the old and the new configuration.

- add extension with the appendConfig effect. Extensions added in this way are added to the end of the top-level configuration, and stay there until a full reconfiguration happens.
  - This can be useful to inject extensions on demand. For example, snippet completion, the first time it is activated, adds a state field that tracks which snippet field the user is in.

## [Styling Example](https://codemirror.net/examples/styling/)

- CodeMirror uses a CSS-in-JS system to be able to include its styles directly in the script files.
  - both the editor view's own styling and any styling defined for dependencies are automatically pulled in through the JavaScript module system.
  - Themes are simply extensions that tell the editor to mount an additional style module and add the (generated) class name that enables those styles to its outer DOM element.

- The important elements in the editor have regular (non-generated) CSS class names, which can be targeted with manually written style sheets.
  - the injected rules are placed before any other style sheets, and will thus have a lower default precedence than your rules.
- there are limits to how you can style the editor. Things like making the editor lines `display: inline` or the cursor `position: fixed` will just break stuff. But within reasonable bounds, the library tries to be robust when it comes to styling.
- By default, the editor adjusts to the height of its content, but you can make cm-scroller `overflow: auto`, and assign a height or max-height to cm-editor, to make the editor scrollable.

- ☄️ The library supports having CSS transforms applied to its parent elements that do 2D scaling and translation. Anything else (rotation, 3D transformation, shearing) will break the editor.

- there are two ways of showing the selection in CodeMirror (the native selection and the `drawSelection` extension), themes will usually want to style both—the caret-color and ::selection rules apply to the native selection, whereas the `.cm-cursor` and `.cm-selectionBackground` rules style the library-drawn selection.

- ✨ Code highlighting uses a somewhat different system from editor-wide theming. 
  - Code styles are also created with JavaScript and enabled with an editor extension. 
  - But by default they don't use stable, non-generated class names. 
  - A highlight style directly returns the class names for the syntactic tokens.
  - Highlight associate highlighting tags with styles

- Without any custom styling, a CodeMirror editor grows vertically, scrolls (rather than wraps) long lines, and doesn't have any border except a focus ring when focused.

- To enable line wrapping, add the `EditorView.lineWrapping` extension to your configuration. 
  - It is also possible to adjust the white-space style of the content element in some other way, but only `pre` and `pre-wrap` are supported by the library, and wrapping can be unreliable if you don't also set overflow-wrap: anywhere, so it is recommended to just use this extension to enable wrapping.

- Adjusting the vertical behavior of the editor can be done by giving its outer element a height, and setting overflow: auto on the scroller element.

## [Autocompletion Example](https://codemirror.net/examples/autocompletion/)

- By default, the plugin will look for completions whenever the user types something, but you can configure it to only run when activated explicitly via a command.

- 
- 
- 

## [Tooltip Example](https://codemirror.net/examples/tooltip/)

- The @codemirror/view package provides functionality for displaying tooltips over the editor—widgets floating over the content, aligned to some position in that content.

- tooltips are not added and removed to an editor through side effects, but instead controlled by the content of a facet. 

- 
- 
- 

## ⌛️ [Undoable Effects Example](https://codemirror.net/examples/inverted-effect/)

- By default, the history extension only tracks changes to the document and selection, and undoing will only roll back those, not any other part of the editor state.
- Sometimes, you do need other actions on that state to be undoable. 
  - If you model those actions as state effects, it is possible to wire such functionality into the core history module. 
  - The way you do that is by registering your effect to be invertable. When the history sees a transaction with such an effect, it'll store its inverse, and apply that when the transaction is undone.

- 
- 
- 
- 

## 🔀 [Collaborative Example](https://codemirror.net/examples/collab/)

- Real-time collaborative editing is a technique where multiple people on different machines can edit the same document at the same time.
  - The main difficulty with this style of editing is handling of conflicting edits—since network communication isn't instantaneous, it is possible for people to make changes at the same time, which have to be reconciled in some way when synchronizing everybody up again.
- CodeMirror comes with utilities for collaborative editing based on operational transformation with a central authority (server) that assigns a definite order to the changes. 

- It is also possible to wire up different collaborative editing algorithms to CodeMirror. See for example Yjs.

- There is one thing to keep in mind though. As described in more detail in the collaborative-editing blog post, the kind of position mapping done in the effect's `map` function is not guaranteed to converge to the same positions when applied in different order by different peers. 
  - For some use cases (such as showing other people's cursor), this may be harmless. 
  - For others, you might need to set up a separate mechanism to periodically synchronize the positions.

- 
- 
- 

# more
- [Revisiting our CodeMirror 6 implementation in React after the official release _202210](https://codiga.io/blog/revisiting-codemirror-6-react-implementation/)
