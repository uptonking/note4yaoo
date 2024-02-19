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

- https://github.com/judge0/ide /MIT/202312/js
  - https://ide.judge0.com/
  - free and open-source online code editor that allows you to write and execute code from a rich set of languages. 
  - Judge0 IDE is using Judge0 for executing user's source code.
# extensions

# monaco-based

- 

# apps
- https://github.com/SamsungInternet/web-code /201910/js
  - A text editor for the web based around monaco
  - deprecated: I've recently started using cdr/code-server which is a full VS Code instance which now runs on Android. The same way this does.
# collab
- https://github.com/Kshitiz1403/Collaborative-IDE
  - Run code in your browser and start collaborating with peers. 
  - User project files are stored & managed using Azure File Storage. A file share is mounted on a linux machine using the SMB protocol.

- https://github.com/convergencelabs/monaco-collab-ext
  - Adds collaborative editing capabilities to the Monaco Editor
  - uses Convergence to handle the synchronization of data and user actions

- https://github.com/kehshiba/serengeti /202401/js
  - crdt-websockets based code collaboration.
  - 服务端只转发op，没有其他逻辑
  - 客户端依赖@monaco-editor/react.v4、yjs、socket.io、zustand
# more
