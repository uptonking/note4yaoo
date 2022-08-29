---
title: lib-editor-atlaskit-dev
tags: [atlaskit-editor, editor]
created: 2021-06-30T19:29:35.962Z
modified: 2021-07-14T15:36:09.702Z
---

# lib-editor-atlaskit-dev

# guide

- watching
  - nodeViews: code-block, width, card, emoji, hyperlink, placeholder-text, text-color
    - 所有NodeView组件的实现都很复杂！！！
    - 大量依赖atlassian design system中的react组件
  - 使用atlassian editor重写outline，抽象出替换可编辑器的接口，考虑可替换的协作同步方案
# examples-repos
- https://github.com/jungpaeng/playground-test-atlaskit-editor
  - /202002
  - Verify that atlaskit editor is active in CRA
- https://github.com/haniplanet/editor-core
  - /201912
  - Atlaskit Custom Editor

- https://github.com/jonnokata/wilbur
  - 代码实现简单，但展现了用法，有很多登录验证firebase的逻辑
  - Beautifully simple notes with AtlasKit
  - As this app was built as more of a technical exploration, the real-world use case was less important to me

- guidu /13Star/MIT/202105/ts/react
  - https://github.com/uidu-org/guidu
  - https://uidu.design/
  - Guidu is uidu's design system library
  - 完全复制了atlassian-editor，并将组件替换成了自己的design system组件
  - 提供了专门的数据类别组件：list, table, data manager, data views, timeline, dashlet, dashboard
  - 依赖styled-components、@amcharts/amcharts4、d3、@cubejs-client/react、react-table、twin.macro
  - These components are Atlassian Design Guidelines(ADG) compliant

- yana /175Star/MIT/202201/ts/electron/atlaskit
  - https://github.com/lukasbach/yana
  - https://yana.js.org/
  - 依赖electron、sqlite3
  - 可选编辑器 atlaskit/monaco
  - 文章内容保存在本地sqlite，而不是markdown文件
  - 产品功能简洁，体验友好
  - note-taking app with nested documents, full-text search, rich-text editor, code snippet editor
  - a powerful notebook app which allows you to manage local workspaces of hierarchically structured taggable and searchable notes.
  - Rich notes editor powered by the Atlassian editor core
  - Multiple local workspaces

- https://github.com/yeojono/goji /201909
  - 依赖@atlaskit/editor-core@90.3.4, emotion9, react-intl2, unstated2
  - another notes app. The difference is the power of the Atlassian Editor.

- https://github.com/yjs/yjs-demos
  - https://demos.yjs.dev/
  - yjs和主流编辑器集成实现协作编辑的示例集合
  - 示例包括prosemirror, codemirror, tiptap, atlaskit, monaco, quill

- https://github.com/b-yond-infinite-network/md-to-adf
  - Markdown to Atlassian Document Format translation/traduction

- https://github.com/portfoolio/dashboard
  - Portfolio dashboard built with atlaskit-eidtor, rxjs
