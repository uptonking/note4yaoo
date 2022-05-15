---
title: lib-editor-slate-examples
tags: [examples, slate, toc]
created: '2022-05-15T18:45:14.380Z'
modified: '2022-05-15T18:45:27.570Z'
---

# lib-editor-slate-examples

# popular-slate

- wangEditor.v5 /13.6kStar/MIT/202005/ts
  - https://github.com/wangeditor-team/wangEditor
  - https://www.wangeditor.com/
  - core依赖slate、snabbdom、dom7、is-hotkey、lodash、uppy(file uploader)、event-emitter、i18next
  - 开源 Web 富文本编辑器，开箱即用，配置简单。支持 JS Vue React 。
  - features
    - L1级编辑器
      - 弃用了 document.execCommand API ，使用 slate.js（但不依赖 React）为内核，升级为 L1 能力。
    - 使用vdom
      - 使用 vdom 技术（基于 snabbdom.js ）做视图更新，model 和 view 分离，增加稳定性
    - 扩展性
      - 使用扩展插件和模块的机制，保证扩展性
      - 现在 wangEditor 内置的各个功能，也都是通过扩展插件和模块的形式搭建起来的

- plate
  - https://github.com/udecode/plate
  - https://plate.udecode.io/
  - `slate-plugins` repo has been renamed to `plate`.
  - The library formerly known as @udecode/slate-plugins is now available as @udecode/plate
  - Slate is a low-level editor framework that helps you deal with difficult parts when building an editor, such as events handlers, elements, formatting, commands, rendering, serializing, normalizing, etc.
  - @udecode/plate is built on top of slate to handle plugins and state management for an optimal development experience. 
  - This repository comes with a lot of plugins as elements, marks, serializers, normalizers, queries, transforms, components and so on.
  - [Generic typescript for slate](https://github.com/ianstormtaylor/slate/pull/4177)
    - I unfortunately don't have the time to complete that PR, so I've forked that PR into Plate.
- plate-repos
  - https://www.npmjs.com/package/@frontify/arcade
    - Design System of Frontify

- https://github.com/coniel/whim 
  - /6Star/MIT/202108/ts
  - A highly customisable block based rich text editor inspired by Notion.

- https://github.com/eea/volto-slate
  - /23Star/MIT/202203/js
  - An alternative text editor for Volto, capable of completely replacing the default richtext editor
  - Some of the main reasons that drove us to create volto-slate instead of enhancing Volto's draftjs implementation
# slate-based-editors
- https://github.com/Quadrats/quadrats
  - https://quadrats.github.io/quadrats
  - A complete rich text editor. Currently based on Slate framework.

- https://github.com/tiddly-gittly/slate-write
  - A WYSIWYG editor for TiddlyWiki. (WIP)
  - 一个用于 太微TiddlyWiki 的所见即所得编辑器。 

- @tinacms/toolkit
  - https://github.com/tinacms/tinacms/blob/main/packages/%40tinacms/toolkit
  - 依赖 @udecode/plate、headlessui、floating-ui

- https://github.com/Yan-Boogie/highlighter
  - A complete rich text editor based on Slate framework with extended 'Highlighting' functionality.

- https://github.com/sympto-health/slate-rte
  - Pre-built rich text editor for Slate in React.

- https://github.com/React-Artibox/artibox
  - Artibox - A complete rich text editor based on Slate framework.
  - /202011

- https://github.com/rojer95/dslate
  - https://rojer95.github.io/dslate/#/
  - https://rojer95.github.io/dslate/#/docs/getting-started
  - DSlate 是一个基于 Slate 构建的 Ant Design 风格的富文本编辑器

- https://github.com/slatable/slate
  - 基于 slatejs 封装富文本编辑器
  - /202006

- https://github.com/gwwyn/react-editor
  - https://gwwyn.github.io/react-editor/
  - Rich-text editor build with React and Slate

- https://github.com/rs-pro/rocket-slate
  - A rich text editor based on SlateJS framework and slate-plugin-next
  - Supports slate 0.57 only
# slate-plugins
- https://github.com/inokawa/remark-slate-transformer
  - remark plugin to transform remark syntax tree (mdast) to Slate document tree, and vice versa. Made for WYSIWYG markdown editor.

- https://github.com/afeiship/next-slate-plugin
  - Slate plugin manager.

- https://github.com/cudr/slate-collaborative
  - slatejs collaborative plugin & microservice

- https://github.com/BitPhinix/slate-yjs
  - Yjs binding for Slate
# more-repos-slate
- https://github.com/Dev-CasperTheGhost/full-slate-editor-example
  - A full Slate editor example with many features such as text formatting, block formatting (quotes, headers, lists) and text alignment

- https://github.com/johnsonandjohnson/bodiless-js
  - Framework for building editable websites on the JAMStack

- https://github.com/react-page/react-page
  - 使用redux作为状态管理
  - 提供了 @react-page/plugins-slate

- https://github.com/grafana/grafana
  - ui依赖slate.v0.47.8

- https://github.com/wowlusitong/re-editor
  - 一个开箱即用的React富文本编辑器
  - /201908

- https://github.com/concord-consortium/slate-editor
  - Rich text editor based on Slate 0.47
