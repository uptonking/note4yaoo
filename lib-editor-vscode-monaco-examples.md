---
title: lib-editor-vscode-monaco-examples
tags: [examples, monaco-editor]
created: 2023-01-21T18:57:24.677Z
modified: 2023-01-21T18:57:47.811Z
---

# lib-editor-vscode-monaco-examples

# guide

# popular
- https://github.com/microsoft/monaco-editor /基于dom实现
  - https://microsoft.github.io/monaco-editor/
  - Monaco Editor is the code editor that powers VS Code.
  - supports Edge, Chrome, Firefox, Safari and Opera. 
  - The Monaco editor is not supported in mobile browsers or mobile web frameworks.

- https://github.com/judge0/ide /MIT/202403/js
  - https://ide.judge0.com/
  - free and open-source online code editor that allows you to write and execute code from a rich set of languages. 
  - Judge0 IDE is using Judge0 for executing user's source code.
# extensions

# monaco-based

- 

# examples
- https://github.com/SamsungInternet/web-code /201910/js
  - A text editor for the web based around monaco
  - deprecated: I've recently started using cdr/code-server which is a full VS Code instance which now runs on Android. The same way this does.

- https://github.com/shubhangii0324/quill-editor /202404/ts
  - https://quill-editor-three.vercel.app/
  - a Next.js project
# collab
- https://github.com/Kshitiz1403/Collaborative-IDE /202401/ts/yjs
  - a full stack system supporting collaborative code editing, compiling & shared shell.
  - Monaco editor is the internal implementation of VSCode's editor. I am using the React port of it Monaco for React.
  - I am using Yjs for providing CRDT & conflict free collaborative editing

- https://github.com/convergencelabs/monaco-collab-ext
  - Adds collaborative editing capabilities to the Monaco Editor
  - uses Convergence to handle the synchronization of data and user actions

- https://github.com/kehshiba/serengeti /202401/js
  - crdt-websockets based code collaboration.
  - 服务端只转发op，没有其他逻辑
  - 客户端依赖@monaco-editor/react.v4、yjs、socket.io、zustand

- https://github.com/interviewstreet/firepad-x /202401/ts
  - We have rewritten all the modules and few extras using TypeScript while enhancing earlier implemented Adapter Pattern to integrate with external modules, such as Database (preferably Firebase) and editors (as of now only Monaco is supported, but PRs are welcomed). 
# more
