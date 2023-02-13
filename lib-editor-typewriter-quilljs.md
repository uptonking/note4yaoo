---
title: lib-editor-typewriter-quilljs
tags: [quill, typewriter]
created: 2023-02-09T12:25:01.120Z
modified: 2023-02-09T18:23:23.287Z
---

# lib-editor-typewriter-quilljs

# guide

# quill-delta
- Typewriter is influenced by Quill.js, being built on the same data model, but with differences
  - Typewriter uses tuples of indexes to describe ranges and selection
  - Typewriter’s rendering to the DOM is just a module. It can be left out or replaced with custom rendering (e.g. for virtualized rendering).
  - Typewriter provides a TextChange interface to roll up multiple change operations into one atomic change in the editor.
  - Typewriter’s single `insert` replaces Quill's `insertText` and `insertEmbed` methods and allows overwriting selected content in one operation.
  - Typewriter provides a module for decorations.
  - Typewriter has no stylesheet requirements. 
  - Typewriter renders lists correctly as HTML lists should be (UL > LI > UL > LI). Quill uses CSS to fake list indentation.
  - Typewriter allows paragraphs to be paragraphs! Without a required stylesheet which removes paragraph margins
  - Typewriter's History module works the same way your OS undo works, combining simliar actions (inserts, deletes) and breaking correctly when selection changes. 
