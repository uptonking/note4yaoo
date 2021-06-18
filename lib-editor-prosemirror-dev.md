---
title: lib-editor-prosemirror-dev
tags: [lib, prosemirror, text-editor]
created: '2021-05-06T09:39:21.604Z'
modified: '2021-05-06T09:39:53.522Z'
---

# lib-editor-prosemirror-dev

# guide
- 编辑器问题
  - 光标、选区、输入法、键盘事件
  - 首屏渲染完成后，用户输入文本时，是否还需要走一次完整的解析渲染流程

- plugin vs node view

- tips
  - 一个prosemirror document是一个无依赖的普通js object对象，所以实现第三方renderer也可行
  - 如果关注的重点是markdown和table，那就将更多的工作放在prosemirror层，增强通用性，将react wrapper层的工作尽量减少，方便迁移
  - 分析一个产品或框架，需要考虑的方面：存储的数据结构、状态管理(更新转换)、视图渲染、样式主题

- prosemirror-renderer
  - `<canvas>`是标准的html元素，考虑实现nodeViews将特殊文本渲染到canvas，如表格、图表
  - tiptap的drawing示例，可以在空svg元素上画路径
  - atlaskit-editor开源了自定义renderer可以参考

- prosemirror-examples
  - 大部分的方案是以vanillajs为core，react为wrapper
    - 尝试保留rich-markdown-editor的api，将core用tiptap重写
  - tiptap, rich-markdown-editor, @atlaskit/editor-core, remirror
  - atlaskit-editor实现了layout多列插件和图片排版插件
  - more-react: smartblock, curvenote(redux), nib-edit, xen-editor, czi-prosemirror, pubpub-editor, licit, Aditor
  - more-vanillajs: stacks-editor, milkdown, bangle.dev, tui.editor.v3, emirror, kangxi-editor, pageboard/client(页面搭建)
# pieces

# examples-remark-parse

- https://github.com/marionebl/prosemirror
  - A personal experiment libraries over prosemirror project
  - prosemirror + remark demos

- https://github.com/Novartis/mdx-utils
  - This package contains utilities for working with MDX syntax.
  - Parses an MDX document and its frontmatter into an AST.
  - Create a custom Prosemirror schema. 
    - This extends the Prosemirror Markdown schema with your custom elements, allowing its AST to represent your MDX document.
  - transforms an MDX syntax tree into a Prosemirror syntax tree. 
    - This way, you can load it into a Prosemirror editor and allow rich-text editing with your custom components.

- https://github.com/dxos/editor /AGPLv3
  - Collaborative editor
  - 依赖 remark-rehype、yjs、prosemirror、hightlight.js

- more-remark
  - notewothy
# examples-repos
- @atlaskit/editor-core /Apache2/ts
  - https://bitbucket.org/atlassian/atlassian-frontend-mirror/src/master/editor/
  - https://atlaskit.atlassian.com/packages/editor/editor-core
  - [kitchen-sink-example](https://atlaskit.atlassian.com/examples/editor/editor-core/kitchen-sink)
  - A package contains Atlassian editor core functionality
  - 基于react class组件实现
  - 提供了针对image/file的图文混排工具
  - 还提供了多列布局工具，包括两栏、三栏、按比例、居中
  - 提供了语法树ADF显示

- https://github.com/dminkovsky/use-prosemirror
  - This package lets you bootstrap a minimal, unopinionated React integration quickly
  - Separates state and presentation so you can keep your state as high up as necessary.
- https://github.com/TeemuKoivisto/prosemirror-react-typescript-example
  - copy the approach by Atlassian editor_v20201205
  - https://github.com/TeemuKoivisto/prosemirror-track-changes-example

- https://github.com/BlueMona/prosemirror-react-renderer
  - An alternative to ProseMirror's DOMSerializer that converts documents into React elements instead of DOM fragments.
- https://github.com/johnkueh/prosemirror-react-nodeviews
  - An example of how to use React components as NodeViews for ProseMirror
  - 原理是`ReactDOM.createPortal(<Component />, container, shortid.generate()); `，事件传播会根据组件在react tree中的位置，而不是根据在真实dom tree中的位置
- https://www.npmjs.com/package/@marduke182/prosemirror-react-view
  - This library is a full React implementation of the official prosemirror-view package. 
  - Aims to implement a simple React Component that uses ProseMirror Data Model to render the document and bind the right events to synchronize the user selection and created ProseMirror transaction based on user inputs.

- https://github.com/atlassian/prosemirror-utils
  - Utils library for ProseMirror

- https://github.com/d4rkr00t/prosemirror-dev-tools
  - Developer Tools for ProseMirror
  - Inspect document – all nodes and marks
  - Inspect selection – position, head, anchor and etc.
  - Inspect active marks
  - See document stats – size, child count

- https://github.com/ueberdosis/prosemirror-to-html
  - Takes ProseMirror JSON and outputs HTML. 基于php实现
- https://github.com/ueberdosis/html-to-prosemirror
  - Takes HTML and outputs ProseMirror compatible JSON. 基于php实现
- https://github.com/enVolt/html-to-prosemirror
  - Takes HTML and outputs ProseMirror JSON.originally written for PHP

- https://github.com/BrianHung/editor
  - 依赖prosemirror-markdown、codemirror6、katex，不依赖react、tiptap、rich-markdown-editor
  - a rich text editor built upon the ProseMirror framework. 
  - It is based off tiptap and rich-markdown-editor, but tries to stay agnostic to Vue and React.
- https://github.com/paperbits/paperbits-prosemirror
  - https://demo.paperbits.io/
  - https://github.com/paperbits/paperbits-demo
  - https://github.com/paperbits/paperbits-core
  - Paperbits HTML editor based on ProseMirror.
