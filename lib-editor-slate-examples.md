---
title: lib-editor-slate-examples
tags: [examples, slate, toc]
created: 2022-05-15T18:45:14.380Z
modified: 2022-05-15T18:45:27.570Z
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
  - A plugin framework for building rich text editors with slate.

- quadrats /4Star/MIT/202203/ts
  - https://github.com/Quadrats/quadrats
  - https://quadrats.github.io/quadrats
  - A complete rich text editor. Currently based on Slate framework.
  - storybook示例非常丰富
  - 依赖 slate.v0.75.0

- whim-notion-like /6Star/MIT/202108/ts
  - https://github.com/coniel/whim 
  - A highly customisable block based rich text editor inspired by Notion.
  - 依赖 slate.v0.65.3，fuse.js(fuzzy-search)
  - Whim is currently undergoing a complete re-write for version 2.0, with an initial release planned for the end of August 2022. 
    - Version 2.0 will include a much improved API, detailed docs, and solid test coverage.

- https://github.com/eea/volto-slate/tree/develop
  - /23Star/MIT/202203/js
  - https://6.demo.plone.org/
  - An alternative text editor for Volto, capable of completely replacing the default richtext editor
  - Some of the main reasons that drove us to create volto-slate instead of enhancing Volto's draftjs implementation
  - 样式陈旧，编辑器和业务代码有联系
  - repos
    - https://github.com/eea/volto-slate-metadata-mentions
    - https://github.com/eea/volto-slate-footnote
    - https://github.com/plone/volto

- slate-angular /93Star/MIT/202205/ts
  - https://github.com/worktile/slate-angular
  - http://slate-angular.ngnice.com/
  - Angular view layer for Slate

- https://github.com/prezly/slate
  - Prezly software built upon Slate

- https://github.com/seafileltd/seafile-editor
  - 项目是基于 react-slate 组件库的二次封装, 用于满足公司富文本编辑器的使用需求
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

- https://github.com/rojer95/dslate
  - https://rojer95.github.io/dslate/#/
  - https://rojer95.github.io/dslate/#/docs/getting-started
  - DSlate 是一个基于 Slate 构建的 Ant Design 风格的富文本编辑器

- https://github.com/slatable/slate
  - 基于 slatejs 封装富文本编辑器
  - /202006

- https://github.com/sanity-io/sanity/tree/next/packages/%40sanity/portable-text-editor
  - Sanity.io is the platform for structured content. 
  - It comes with an open-source editing environment called Sanity Studio that you can customize with JavaScript and a real-time hosted data store. 
  - 依赖slate.v0.72.3，自研slate-react
  - 包含test
  - 基于block进行设计

- https://github.com/payloadcms/payload
  - https://demo.payloadcms.com/admin
  - Headless CMS and Application Framework built with TypeScript, Node.js, React and MongoDB
  - Block-based Layout Builder
  - Extensible SlateJS rich text editor

- https://github.com/Thinkei/hero-editor
  - Hero editor is a WYSIWYG built on top of Slate (v0.58.3). It's designed for mobile-first, hence all of the communications from plugins to the editor must go through message channel. 
  - This package also includes serializers and renderers for the Slate content.

- https://github.com/webkom/lego-editor
  - A React rich text editor written in TS with Slate.js for lego-webapp

- https://github.com/contentful/field-editors/tree/master/packages/rich-text
  - https://contentful-field-editors.netlify.app/rich-text
  - This package contains a React RichTextEditor component that is used as default for RichText field type in the Contentful web application.
  -  Since these are developed using the App SDK, this will allow you to understand how each editor works, fork existing apps or create your own apps based on existing Contentful components' source rather than starting from scratch.

- https://github.com/Yan-Boogie/highlighter
  - A complete rich text editor based on Slate framework with extended 'Highlighting' functionality.

- https://github.com/Rajatm544/react-rich-editor
  - https://reactricheditor.netlify.app/
  - A rich editor built using React and Slate. It has option to highlight text and show it as a tags beside the editor

- https://github.com/sympto-health/slate-rte
  - Pre-built rich text editor for Slate in React.

- https://github.com/gwwyn/react-editor
  - https://gwwyn.github.io/react-editor/
  - Rich-text editor build with React and Slate

- https://github.com/rs-pro/rocket-slate
  - A rich text editor based on SlateJS framework and slate-plugin-next
  - Supports slate 0.57 only

- https://github.com/React-Artibox/artibox
  - Artibox - A complete rich text editor based on Slate framework.
  - /202011

- https://github.com/quillforms/quillforms
  - https://www.quillforms.com/
  - Open Source TypeForm Alternative Based on React JS and Typescript | Best Typeform Clone

- more-slate-editor
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
- https://github.com/accordproject/markdown-transform
  - A transformation and parsing framework for converting markdown content to HTML, Slate (for rich-text editing) and other structured document object models (DOMs).
  - 提供了很多子包，本身类似于remark

- https://github.com/cihad/slate-table  /202107/ts
  - https://cihad.github.io/slate-table/
  - Table Plugin for Slate (based on @udecode/slate-plugins above v1.0). Inspired by the Atlassian editor's table plugin.
  - 依赖 slate.v0.61, @udecode/slate-plugins-table(2021)
- https://github.com/lqs469/slate-table  /202003/ts
  - https://slate-table.vercel.app/
  - A pretty Slate.js table plugin (Slate.js version > 0.5)
- https://github.com/1build/leyden
  - https://1build-org.gitbook.io/leyden/
  - a data table framework powered by Slate.
  - Leyden's coordinate system is simple and fully interoperable with Slate's Path system.
  - Cells can access data from other cells using absolute coordinates and relative positions.
  - Leyden exposes several pre-built validators (such as numeric and integer) for your cell data
  - Slate requires users to define complicated render functions to detect different types of elements. Leyden handles this automatically
  - Leyden builds upon Slate's schema definition system, providing an interface for users to define table-shaped schemas with powerfully customization cells.
- https://github.com/daibin0809/slate-table-demo
  - 依赖event-emitter
  - slate 编辑器完成的一个表格功能，能够进行表格的选区、单元格操作和行列操作等操作。
  - 表格中无法再添加表格；
  - 表格中右键唤起工具菜单
- https://github.com/nod-engineering/slate-table
  - /202106/js

- https://github.com/whatever-company/slate-tables
  - https://whatever-company.github.io/slate-tables/
  - 依赖slate.v0.47
  - A Slate plugin to handle table edition.
  - The plugin supports nested tables natively.
  - Colspan and Rowspan are supported. All operations create a matrix containing all cells' positions.
- https://github.com/jasonphillips/slate-deep-table
  - https://jasonphillips.github.io/slate-deep-table/
  - /201910/js/v0.44
  - Forked from the slate-edit-table implementation, allowing for creation of tables with nested content
  - https://github.com/George-A-Payne/slate-tables
    - Forked from slate-deep-tables 

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

- https://github.com/vip-git/universal-json-schema
  - https://react-jsonschema-form-material-ui.github56.now.sh/
  - Universal JSON Schema Form - Currently Support for React - Material UI components for building Web forms from JSON Schema.
  - A Material UI port of jsonschema-form. (mui.v5)

- https://github.com/commercetools/ui-kit
  - Component library based on our design system

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

- https://github.com/Mirrorgo/slatejs
  - 基于slate.js实现一个富文本编辑器, 用以学习富文本编辑器相关知识

- https://github.com/gwwyn/react-editor
  - Rich-text editor build with React and Slate

- https://github.com/ccjr1120/story-editor_slate
  - 基于slate的文本编辑器

- https://www.npmjs.com/package/@nocobase/client
