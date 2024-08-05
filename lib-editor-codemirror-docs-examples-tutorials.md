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

## [Document Change Example](https://codemirror.net/examples/change/)

- Initiating an editor state change from a program is done by dispatching a transaction.
- When dispatching a transaction, you can also pass an array of changes. 
  - The from/to in each of these changes refer to positions in the start document, not to the document created by previously listed changes.

- When acting on the selection, you'll often want to create your transaction spec using the `replaceSelection` method. 
  - `view.dispatch(view.state.replaceSelection("★"))`; 
  - This replaces each selection range with a given string, and moves the selection ranges to the end of that string (by default, they'd stay in front of it)

## [Selection Example](https://codemirror.net/examples/selection/)

- Like any editor state change, moving the selection is done by dispatching a transaction
- When a transaction makes a document change as well as setting the selection, the new selection should point into the document as it is after the change
- When writing commands that act on the selection, you have to take some care to support multiple ranges.

## [Decoration Example](https://codemirror.net/examples/decoration/)

- Decorations are provided to the editor using the RangeSet data structure, which stores a collection of values (in this case the decorations) with ranges (start and end positions) associated with them.
- Decorations are provided to the editor view through a facet. 
- There are two ways to provide them—directly, or though a function that will be called with a view instance to produce a set of decorations. 
  - Decorations that significantly change the vertical layout of the editor, for example by replacing line breaks or inserting block widgets, must be provided directly, since indirect decorations are only retrieved after the viewport has been computed.
- Indirect decorations are appropriate for things like syntax highlighting or search match highlighting, where you might want to just render the decorations inside the viewport or the current visible ranges, which can help a lot with performance.

- Widget decorations don't directly contain their widget DOM. Apart from helping keep mutable objects out of the editor state, this additional level of indirection also makes it possible to recreate widgets without redrawing the DOM for them. 

- `EditorView.atomicRanges` facet can be provided range sets (usually the same set that we're using for the decorations) and will make sure cursor motion skips the ranges in that set.

## 🌵 [Merge View](https://github.com/codemirror/merge)

- A merge view manages two editors side-by-side, highlighting the difference between them and vertically aligning unchanged lines. 
  - If you want one of the editors to be read-only, you have to configure that in its extensions.
  - By default, views are not scrollable. Style them (.cm-mergeView) with a height and `overflow: auto` to make them scrollable.

- Side-by-side Merge View
  - config
    - collapseUnchanged⁠: When given, long stretches of unchanged text are collapsed

- Unified Merge View
  - Create an extension that causes the editor to display changes between its content and the given original document. 
  - Changed chunks will be highlighted, with uneditable widgets displaying the original text displayed above the new text.
  - config
    - mergeControls: Controls whether accept/reject buttons are displayed for each changed chunk. Defaults to true.

- A chunk describes a range of lines which have changed content in them. 
  - Either side (a/b) may either be empty (when its `to` is equal to its `from`), or points at a range starting at the start of the first changed line, to 1 past the end of the last changed line. 
  - Note that to positions may point past the end of the document. Use endA/endB if you need an end position that is certain to be a valid document position.

## [Split View Example](https://codemirror.net/examples/split/)

- to keep the content of two views in sync, you'll have to forward changes made in one view to the other. 
- A good place to do this is either an overridden `dispatch` function, or an `update` listener. In this example, we'll use the former.
- In order to be able to distinguish between regular transactions caused by the user and synchronizing transactions from the other editor, we define an annotation that will be used to tag such transactions.
- Whenever a transaction that makes document changes and isn't a synchronizing transaction comes in, it is also dispatched to the other editor.

- Note that non-document state (like selection) isn't shared between the editors. For most such state, it wouldn't be appropriate to share it.

- 
- 
- 

## [Autocompletion Example](https://codemirror.net/examples/autocompletion/)

- By default, the plugin will look for completions whenever the user types something, but you can configure it to only run when activated explicitly via a command.

- The default completion keymap binds Ctrl-Space to start completion, arrows to select a completion, Enter to pick it, and Escape to close the tooltip. 
  - It is activated by default when you add the extension, but you can disable that if you want to provide your own bindings.

- Some sources need to recompute their results on every keypress, but for many of them, this is unnecessary and inefficient. They return a full list of completions for a given construct, and as long as the user is typing (or backspacing) inside that construct, that same list can be used (filtered for the currently typed input) to populate the completion list.
  - This is why it is very much recommended to provide a `validFor` property on your completion result.

- it is often useful to inspect the syntax tree around the completion point, and use that to get a better picture of what kind of construct is being completed.

## [Tooltip Example](https://codemirror.net/examples/tooltip/)

- The @codemirror/view package provides functionality for displaying tooltips over the editor—widgets floating over the content, aligned to some position in that content.

- tooltips are not added and removed to an editor through side effects, but instead controlled by the content of a facet. 
  - by directly tying the tooltips to the state they reflect we avoid a whole class of potential synchronization problems.

- Tooltips are represented as objects that provide the position of the tooltip, its orientation relative to that position, whether to show a triangle-arrow on the tooltip, and a function that draws it.

- Active tooltips are displayed as fixed-position elements. 

- hoverTooltip can be used to define tooltips that show up when the user hovers over the document

## [Gutter Example](https://codemirror.net/examples/gutter/)

- The simplest use of gutters is to simply dump lineNumbers() into your configuration to get a line number gutter.
- To add a gutter, call the gutter function and include the result in your state configuration.
- As with decorations, gutter markers are represented by lightweight immutable values that know how to render themselves to DOM nodes, in order to allow updates to be represented in a declarative way without recreating a lot of DOM nodes on every transaction. 

## [Panel Example](https://codemirror.net/examples/panel/)

- A “panel”, as supported by the @codemirror/view package, is a UI element shown above or below the editor.
  - They will sit inside the editor's vertical space for editors with fixed height. 
  - When the editor is partially scrolled out of view, panels will be positioned to stay in view.

## 🌰 [Zebra Stipes Example](https://codemirror.net/examples/zebra/)

- This example defines an extension that styles every Nth line with a background.

- 
- 
- 

## 💥 [Huge Doc Demo](https://codemirror.net/examples/million/)

- This page loads a document of a few million lines
  - You'll notice that highlighting stops at some point if you scroll down far enough. The parser contains logic that limits the amount of work it does to avoid wasting too much battery and memory. 
  - If the editor is inactive, it'll stop doing work entirely. Otherwise, it should eventually get to your scroll position.

- 
- 

## ⌛️ [Undoable Effects Example](https://codemirror.net/examples/inverted-effect/)

- By default, the history extension only tracks changes to the document and selection, and undoing will only roll back those, not any other part of the editor state.
- Sometimes, you do need other actions on that state to be undoable. 
  - If you model those actions as state effects, it is possible to wire such functionality into the core history module. 
  - The way you do that is by registering your effect to be invertable. When the history sees a transaction with such an effect, it'll store its inverse, and apply that when the transaction is undone.

- 
- 

## [Lint Example](https://codemirror.net/examples/lint/)

- The @codemirror/lint package provides a way to display errors and warnings in your editor. 
  - If you give it a source function that, when given an editor, produces an array of problems, it will call this function when changes are made to the document, and display its result.

## 🤝🏻🔀 [Collaborative Example](https://codemirror.net/examples/collab/)

- Real-time collaborative editing is a technique where multiple people on different machines can edit the same document at the same time.
  - The main difficulty with this style of editing is handling of conflicting edits—since network communication isn't instantaneous, it is possible for people to make changes at the same time, which have to be reconciled in some way when synchronizing everybody up again.
- 🧮 CodeMirror comes with utilities for collaborative editing based on `operational transformation` with a central authority (server) that assigns a definite order to the changes. 

- By default, the only thing that is shared through such a collaborative-editing channel is document changes (the `changes` field in the update objects). 
- Sometimes it is useful to also use this mechanism to share other information that should be distributed between clients.
  - To do that, when calling the `collab` extension constructor, you can pass a `sharedEffects` function which produces an array of “shared effects” from a transaction. 
  - Shared effects are instances of `StateEffect` that should be applied in other peers as well. 
- The library doesn't provide any utilities for serializing effects, so in order to send them around as JSON you need your own custom serialization code for the effects field in updates.

- It is also possible to wire up different collaborative editing algorithms to CodeMirror. See for example Yjs.

- There is one thing to keep in mind though. As described in more detail in the collaborative-editing blog post, the kind of position mapping done in the effect's `map` function is not guaranteed to converge to the same positions when applied in different order by different peers. 
  - For some use cases (such as showing other people's cursor), this may be harmless. 
  - For others, you might need to set up a separate mechanism to periodically synchronize the positions.
# more
- [Revisiting our CodeMirror 6 implementation in React after the official release _202210](https://codiga.io/blog/revisiting-codemirror-6-react-implementation/)
