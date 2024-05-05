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

## [CodeMirror Autocompletion Example](https://codemirror.net/examples/autocompletion/)

- By default, the plugin will look for completions whenever the user types something, but you can configure it to only run when activated explicitly via a command.

- 
- 
- 

## [CodeMirror Tooltip Example](https://codemirror.net/examples/tooltip/)

- The @codemirror/view package provides functionality for displaying tooltips over the editor—widgets floating over the content, aligned to some position in that content.

- tooltips are not added and removed to an editor through side effects, but instead controlled by the content of a facet. 

- 
- 
- 

## ⌛️ [CodeMirror Undoable Effects Example](https://codemirror.net/examples/inverted-effect/)

- By default, the history extension only tracks changes to the document and selection, and undoing will only roll back those, not any other part of the editor state.
- Sometimes, you do need other actions on that state to be undoable. 
  - If you model those actions as state effects, it is possible to wire such functionality into the core history module. 
  - The way you do that is by registering your effect to be invertable. When the history sees a transaction with such an effect, it'll store its inverse, and apply that when the transaction is undone.

- 
- 
- 
- 

## 🔀 [CodeMirror Collaborative Example](https://codemirror.net/examples/collab/)

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
