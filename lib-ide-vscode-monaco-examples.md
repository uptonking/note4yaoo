---
title: lib-ide-vscode-monaco-examples
tags: [examples, monaco-editor]
created: 2023-01-21T18:57:24.677Z
modified: 2024-08-24T16:17:47.677Z
---

# lib-ide-vscode-monaco-examples

# guide

# popular
- https://github.com/microsoft/monaco-editor /MIT/202411/ts/基于dom实现
  - https://microsoft.github.io/monaco-editor/
  - https://microsoft.github.io/monaco-editor/playground.html
  - Monaco Editor is the code editor that powers VS Code.
  - The Monaco Editor is generated straight from VS Code's sources with some shims around services the code needs to make it run in a web browser
  - supports Edge, Chrome, Firefox, Safari and Opera.
  - The Monaco editor is not supported in mobile browsers or mobile web frameworks.

- https://github.com/judge0/ide /MIT/202403/js
  - https://ide.judge0.com/
  - free and open-source online code editor that allows you to write and execute code from a rich set of languages.
  - Judge0 IDE is using Judge0 for executing user's source code.
  - 依赖monaco-editor

- https://github.com/ast-grep/ast-grep /MIT/202406/rust
  - https://ast-grep.github.io/
  - https://ast-grep.github.io/playground.html
  - A CLI tool for code structural search, lint and rewriting. Written in Rust
  - playground的diff视图基于monaco实现
# monaco-based-editors
- https://github.com/versyxdigital/mkeditor /MIT/202407/ts/inactive
  - https://versyxdigital.github.io/mkeditor
  - The simple markdown editor. Use it through your browser, or download for desktop.
  - MKEditor fully supports the CommonMark spec  
  - MKEditor also includes a built-in, resizable preview renderer and support for exporting your markdown to HTML, with or without styles 
# extensions
- https://github.com/trofimander/monaco-markdown /MIT/202111/ts/inactive
  - Port of vscode-markdown extension for Monaco web editor
# examples
- yn /3.6kStar/AGPLv3/202501/ts/vue/网页版+桌面版
  - https://github.com/purocean/yn
  - https://yank-note.vercel.app/
  - 一款面向程序员的Markdown笔记应用
  - 使用 vscode-Monaco 内核，专为 Markdown 优化
  - 支持历史版本回溯；可在文档中嵌入小工具、可运行的代码块、表格、PlantUML图形、Drawio图形、宏替换等；支持接入 OpenAI 自动补全。
  - 兼容性强：数据保存为本地Markdown文件；拓展功能尽量用 Markdown 原有的语法实现。
  - 支持用户编写自己的插件来拓展编辑器的功能。
  - 加密文件的加密解密操作均在前端完成，请务必牢记自己的密码。一旦密码丢失，只能暴力破解了。

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
# playground
- https://github.com/romannurik/SlidesCodeHighlighter /apache2/202205/js/inactive
  - https://romannurik.github.io/SlidesCodeHighlighter/
  - A little web app that helps you copy+paste syntax-highlighted code into slide decks
  - 依赖monaco、jquery、webfontloader
# more
