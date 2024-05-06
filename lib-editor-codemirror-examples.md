---
title: lib-editor-codemirror-examples
tags: [code-editor, codemirror, examples]
created: 2023-06-23T12:46:36.949Z
modified: 2023-06-23T12:46:53.288Z
---

# lib-editor-codemirror-examples

# guide

# popular
- https://github.com/justinfagnani/codemirror-elements /ts
  - A set of HTML custom elements for editing source code with CodeMirror.

- https://github.com/expressive-code/expressive-code /ts
  - Expressive Code is an engine for presenting source code on the web, aiming to make your code easy to understand and visually stunning.
  - On top of accurate syntax highlighting powered by the same engine as VS Code, Expressive Code allows you to annotate code blocks using text markers, diff highlighting, code editor & terminal window frames, and more.
  - All annotations are based on a powerful plugin architecture 

- https://github.com/exuanbo/codemirror-toolkit /MIT/202312/ts
  - A batteries-included toolset for efficient development of CodeMirror 6 based editors (w/o React).
# collab
- https://github.com/yjs/y-codemirror.next /MIT/202403/js
  - https://demos.yjs.dev/codemirror/codemirror.html
  - Collaborative extensions for CodeMirror6
  - This binding binds a `Y.Text` to a CodeMirror editor.
  - Awareness: Render remote selection ranges and cursors - as a separate plugin
  - Shared Undo/Redo (each client has its own undo-/redo-history) - as a separate plugin

- https://github.com/ekzhang/rushlight /MIT/202306/ts
  - https://github.com/ekzhang/cm-collab /ts
  - A tiny collaborative Markdown editor based on CodeMirror, communicating with a minimal server and database.
  - Make collaborative code editors that run on your own infrastructure: just Redis and a database.
  - Supports multiple real-time documents, with live cursors. 
  - 👉🏻 Based on CodeMirror 6 and operational transformation, so all changes are resolved by server code.
  - The backend is stateless, and you can bring your own transport; even a single HTTP handler is enough.
  - Unlike most toy examples, Rushlight supports persistence in any durable database you choose. Real-time updates are replicated in-memory by Redis, with automatic log compaction.
# extensions
- https://github.com/val-town/codemirror-ts /ISC/ts
  - https://val-town.github.io/codemirror-ts/
  - a set of extensions for CodeMirror 6 that add support for TypeScript.
  - Hover hints for types 
  - Autocomplete 
  - Diagnostics (lints, in CodeMirror's terminology)

- https://github.com/replit/codemirror-vscode-keymap /202212/ts/inactive
  - Ports VSCode's keyboard shortcuts to CodeMirror 6.
# utils
- https://github.com/PuruVJ/neocodemirror /202311/ts
  - Aims to provide Codemirror 6 as an easy to use codemirror action.
# examples
- https://github.com/vizhub-core/vzcode /MIT/202405/ts
  - VZCode: Multiplayer Code Editor
  - VZCode offers a multiplayer code editing environment that caters to a real-time collaborative development experience. It's the code editor component of VizHub, and can also be used independently from VizHub.
  - Browser-based editing environment
  - Real-time collaboration via LAN or using services like NGrok
  - A known shortcoming of VZCode is that it does not (yet) watch for changes from the file system. VZCode assumes that no other programs are modifying the same files.
  - You can also expose your VZCode instance publicly using a tunneling service such as NGrok.
  - Auto-save, debounced after code changes
  - https://github.com/vizhub-core/vizhub
    - https://vizhub.community/
    - Self Hosted CMS for Web-based Dataviz
    - VizHub 2 has been used in Data Visualization Course 2018, Datavis 2020
    - iFrame-based code execution environment.
  - VizHub 3
    - possible to self-host your own instance
    - possible to extend the core with plugins
# diff
- https://github.com/MrWangJustToDo/git-diff-view /MIT/202404/ts
  - https://mrwangjusttodo.github.io/git-diff-view/
  - A Diff View component for React/Vue, just like Github
  - core只依赖lowlight
  - https://github.com/wooorm/lowlight /MIT/202310/js
    - Virtual syntax highlighting for virtual DOMs and non-HTML things
    - This package uses `highlight.js` for syntax highlighting and outputs objects (ASTs) instead of a string of HTML.
    - This package is useful when you want to perform syntax highlighting in a place where serialized HTML wouldn’t work or wouldn’t work well. 
    - You can use the similar `refractor` if you want to use `Prism` grammars instead. 
    - If you’re looking for a really good (but rather heavy) alternative, use `starry-night`.
# more
- https://github.com/datavis-tech/codearea /MIT/201908/js
  - A proof-of-concept code editor with syntax highlighting that uses
    - highlighted-pre-over-textarea approach (like react-simple-code-editor)
    - web-tree-sitter for incremental parsing
    - diff-match-patch via json0-ot-diff for computing text diffs (needed for using tree-sitter)
    - React for DOM updates
