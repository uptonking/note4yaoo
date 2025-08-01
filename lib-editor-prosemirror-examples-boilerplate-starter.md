---
title: lib-editor-prosemirror-examples-boilerplate-starter
tags: [boilerplate, examples, prosemirror]
created: 2022-09-05T03:40:38.434Z
modified: 2022-09-05T03:41:15.727Z
---

# lib-editor-prosemirror-examples-boilerplate-starter

# guide

- resources
  - [codesandbox prosemirror-state deps](https://codesandbox.io/examples/package/prosemirror-state)
  - [codesandbox tiptap deps](https://codesandbox.io/examples/package/@tiptap/core)
# prose-starter
- https://github.com/ocavue/prosemirror-playground
  - https://stackblitz.com/fork/github/ocavue/prosemirror-playground
  - A super simple ProseMirror demo repository. I use this repo to test out new ideas and report bugs.

- https://github.com/ueberdosis/tiptap/tree/main/packages/starter-kit
  - 官方提供了模版工具箱 `@tiptap/starter-kit` npm包
  - https://github.com/syfxlin/tiptap-starter-kit /MIT/202503/ts
    - 非官方套件，包含了常见的扩展，以及斜杠菜单，浮动菜单，Markdown解析、序列化等功能

- https://github.com/mfoitzik/prosemirror-breakout-starter-kit
  - This is a ProseMirror starter kit that uses Webpack.
  - 未使用prosemirror-example-setup包，提供了具体配置示例
  - https://github.com/buzz-software/prosemirror-webpack-project /201805
    - 只有单文件，过于简单，只依赖prosemirror-example-setup包
- https://github.com/KyleMit/prosemirror-sample
  - https://prosemirror-sample.netlify.app/
  - Interactive view of the basic example from the ProseMirror website.
  - 使用vite版和无需打包的js版

- https://github.com/TeemuKoivisto/prosemirror-bug-template /MIT/202410/js
  - Github template to reproduce ProseMirror bugs in simplest form possible
  - Loads the basic `prosemirror-example-setup` with `prosemirror-dev-toolkit` as ES modules using `importmap`

- https://github.com/hedgerwang/learn-prosemirror-typescript-react-app
  - https://hedgerwang.github.io/learn-prosemirror-typescript-react-app/
  - 案例

- https://github.com/ccorcos/prosemirror-examples /
  - https://ccorcos.github.io/prosemirror-examples/
  - ProseMirror rich text editor with @mentions with autocomplete and nested inline nodes.
  - Block Selection Plugin: Press escape, then arrow keys, then enter to navigate blocks

- DoX /6Star/NALic/202308/js/ejs
  - https://github.com/AlbertCerfeda/DoX
  - https://doxeditor.herokuapp.com/
  - 依赖 prosemirror-collab、express、passport、socket.io、bootstrap4、mongodb、html-to-image
  - features
    - 文档支持简单分享、权限设置
    - 协作支持显示光标
  - bugs
    - 协作时对方的光标会跳动然后恢复到正常位置
  - DoX Editor aims to be a web text editor application that allows users to create, edit, store and share several documents.
  - A web text editor application that allows users to create, edit, store and share several documents, with support for real-time collaborative editing.
  - DoX is clearly inspired to well known online word processors such as Google Docs

- https://github.com/vivaxy/examples/tree/master/libraries/prosemirror /MIT/202404/js
  - https://vivaxy.github.io/examples/libraries/prosemirror/
  - 日常积累的各种demo，包括prosemirror/yjs/算法

- https://github.com/lgmworks/prosemirror-with-es6-browser-modules
  - A working project with ES6 browser modules for the example in https://prosemirror.net/examples/basic/

- https://github.com/edp1096/hello-prosemirror /202505/ts
  - https://edp1096.github.io/hello-prosemirror/
  - 测试图片上传，服务端基于go
# play/tests
- https://github.com/amitavanath/prosemirror-uitest /202507/ts
  - transform-test.ts

- https://github.com/gliheng/pm-examples /202407/ts
  - Prosemirror examples

- https://github.com/wangyucode/vite-react-prosemirror /202507/ts
  - 重构分页插件并优化中文输入处理

- https://github.com/Madhawa97/prosemirror-next-demo /202506/ts
  - bootstrapped with create-next-app.

- https://github.com/nicolas-zozol/rsc-prosemirror /202501/ts
  - https://rsc-prosemirror.vercel.app/
  - ProseMirror demo, with React server components used

- https://github.com/i10416/prosemirror-experiment /202501/ts
  - This repository serves as a sandbox to understand ProseMirror internal step by step
  - the code focused on ProseMirror core concept without UI concerns.
  - Transforming ProseMirror data model to AST-like structure

- https://github.com/yoophoon/prosemirror-debug /202504/ts
  - for debugging prosemirror and learning
  - https://github.com/LiamLeeX/prosemirror-source /inactive

- https://github.com/davvidbaker/prosemirror-position-debugger /202210/js/inactive
  - use it in a prosemirror plugin or standalone
# example-online
- prosemirror-react-example-setup-js
  - https://codesandbox.io/s/prosemirror-react-hooks-6qvlfr
  - https://codesandbox.io/s/prosemirror-template-8vcykp

- prosemirror-example-setup-minimal-js
  - https://codesandbox.io/s/l9n6667ooz
  - https://codesandbox.io/s/prosemirror-drag-and-drop-forked-9kl4lr

- prosemirror-minimal-no-keymap-js
  - https://codesandbox.io/s/qzhtb
  - https://codesandbox.io/s/prosemirror-simple-nodeview-forked-r62bk8

- prosemirror-mui-v4-js
  - https://codesandbox.io/s/react-prosemirror-t3num

- prosemirror-collab
  - https://codesandbox.io/s/yjs-react-eb3n1

- prosemirror-table
  - https://codesandbox.io/s/condescending-kirch-3gmyc

- tiptap-react-minimal
  - https://codesandbox.io/s/tiptap-react-editor-y8zsg?

- tiptap-mui-v5-js
  - https://codesandbox.io/s/w75ob2
  - https://codesandbox.io/s/editor-w75ob2

- tiptap-codemirror5-ts
  - https://codesandbox.io/s/0jiqt

- tiptap-examples-list-cra-ts
  - https://codesandbox.io/s/tiptap-h56o9 示例列表

- prosemirror-react-custom-plugins-js
  - https://codesandbox.io/s/gcgwc

- tiptap-react
  - https://codesandbox.io/s/simple-text-editor-59z32

- tiptap-react-slash-command
  - https://codesandbox.io/s/tiptap-react-slash-command-e3j3u

- tiptap-collab
  - https://codesandbox.io/s/tiptap-react-forked-fuqvg

- tiptap-demo-tailwindcss
  - https://codesandbox.io/s/iqjz0
