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

- plate /1.4kStar/MIT/202205/ts
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

- quadrats /4Star/MIT/202203/ts
  - https://github.com/Quadrats/quadrats
  - https://quadrats.github.io/quadrats
  - A complete rich text editor. Currently based on Slate framework.
  - storybook示例非常丰富

- whim-notion-like /6Star/MIT/202108/ts
  - https://github.com/coniel/whim 
  - A highly customisable block based rich text editor inspired by Notion.

- https://github.com/eea/volto-slate/tree/develop
  - /23Star/MIT/202203/js
  - An alternative text editor for Volto, capable of completely replacing the default richtext editor
  - Some of the main reasons that drove us to create volto-slate instead of enhancing Volto's draftjs implementation
  - 样式陈旧，编辑器和业务代码有联系
  - repos
    - https://github.com/eea/volto-slate-metadata-mentions
# slate-based-editors
- @tinacms/toolkit
  - https://github.com/tinacms/tinacms/blob/main/packages/%40tinacms/toolkit
  - 依赖 @udecode/plate、headlessui、floating-ui

- https://github.com/accordproject/web-components/tree/master/packages/ui-markdown-editor
  - https://ap-web-components.netlify.app/
  - a WYSIWYG editor for markdown that conforms to the CommonMark specification
  - 依赖markdown-it、slate、semantic-ui-react

- https://github.com/slatejsx/slatejsx
  - http://seditor.open.heyphp.com/
  - 项目基于slate.js框架开发，项目内所有图标，风格组件均使用antd

- https://github.com/Thinkei/hero-editor
  - Hero editor is a WYSIWYG built on top of Slate (v0.58.3). It's designed for mobile-first, hence all of the communications from plugins to the editor must go through message channel. 
  - This package also includes serializers and renderers for the Slate content.

- https://github.com/webkom/lego-editor
  - A React rich text editor written in TS with Slate.js for lego-webapp

- https://github.com/Yan-Boogie/highlighter
  - A complete rich text editor based on Slate framework with extended 'Highlighting' functionality.

- https://github.com/Rajatm544/react-rich-editor
  - https://reactricheditor.netlify.app/
  - A rich editor built using React and Slate. It has option to highlight text and show it as a tags beside the editor

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

- more-slate-editor
  - https://github.com/worktile/slate-angular
  - https://github.com/marsprince/slate-vue

- deprecated
  - https://github.com/kanweiwei/easy-editor
  - https://github.com/roast-cms/french-press-editor
  - https://github.com/Canner/canner-slate-editor
  - https://github.com/chatterbugapp/chatterslate
  - https://github.com/nossas/slate-editor
  - https://github.com/nareshbhatia/react-force/tree/master/packages/slate-editor
# slate-plugins
- https://github.com/hanford/remark-slate
  - Transform the contents of a slate 0.50+ editor into markdown and back again.
- https://github.com/inokawa/remark-slate-transformer
  - remark plugin to transform remark syntax tree (mdast) to Slate document tree, and vice versa. Made for WYSIWYG markdown editor.

- https://github.com/daibin0809/slate-table-demo
  - slate 编辑器完成的一个表格功能，能够进行表格的选区、单元格操作和行列操作等操作。
  - 表格中无法再添加表格；
  - 表格中右键唤起工具菜单
- https://github.com/lqs469/slate-table
  - A pretty Slate.js table plugin (Slate.js version > 0.5)
- https://github.com/whatever-company/slate-tables
  - https://whatever-company.github.io/slate-tables/
  - 依赖slate.v0.47
  - A Slate plugin to handle table edition.
  - The plugin supports nested tables natively.
  - Colspan and Rowspan are supported. All operations create a matrix containing all cells' positions.

- https://github.com/afeiship/next-slate-plugin
  - Slate plugin manager.

- https://github.com/mwood23/slate-test-utils
  - A toolkit to test Slate rich text editors with Jest, React Testing Library, and hyperscript! Write user centric integration tests with ease

- https://github.com/lukesmurray/use-slate-with-extensions
  - https://use-slate-with-extensions.netlify.app/
  - a simple, powerful, and tiny (< 2KB) hook which helps you build self contained and composable extensions for Slate. 

- https://github.com/enzoferey/slate-instant-replace
  - A Slate plugin that gives you full power on the last word your user typed.
  - This package is compatible with <= slate@0.47

- https://github.com/palerdot/react-slite
  - This react component provides a slack like rich text editing experience powered by slate.js
# slate-collab
- https://github.com/solidoc/slate-ot
  - Operation Transformations for slate 0.5x.

- https://github.com/BitPhinix/slate-yjs
  - Yjs binding for Slate

- https://github.com/6thfdwp/crdt-editor
  - A collaborating editor based on Slate and Yjs

- https://github.com/cudr/slate-collaborative
  - https://github.com/humandx/slate-automerge
  - A example of a collaborative editor using Slate and Automerge
# more-repos-slate
- https://github.com/tiddly-gittly/slate-write
  - A WYSIWYG editor for TiddlyWiki. (WIP)
  - 一个用于 太微TiddlyWiki 的所见即所得编辑器。 

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
