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

- tips
  - 如果关注的重点是表格和markdown，那就将更多的工作放在prosemirror层，增强通用性，将react wrapper层的工作尽量减少，方便迁移
  - 分析一个产品或框架，需要考虑的方面：存储的数据结构、状态管理(更新转换)、视图渲染、样式主题

- prosemirror-renderer
  - `<canvas>`是标准的html元素，考虑实现nodeViews将特殊文本渲染到canvas，如表格、图表
  - tiptap的drawing示例，可以在空svg元素上画路径
  - atlaskit-editor开源了自定义renderer可以参考

- prosemirror-markdown

- prosemirror-table

- prosemirror-examples
  - tiptap, rich-markdown-editor, @atlaskit/editor-core, remirror
  - atlaskit-editor实现了layout多列插件和图片排版插件
# pieces

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
  - Allows using EditorView props as React props.
- https://github.com/TeemuKoivisto/prosemirror-react-typescript-example
  - copy the approach by Atlassian editor
  - https://github.com/TeemuKoivisto/prosemirror-track-changes-example

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

- https://github.com/paperbits/paperbits-prosemirror
  - https://demo.paperbits.io/
  - https://github.com/paperbits/paperbits-demo
  - https://github.com/paperbits/paperbits-core
  - Paperbits HTML editor based on ProseMirror.
