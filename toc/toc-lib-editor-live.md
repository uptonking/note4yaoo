---
title: toc-lib-editor-live
tags: [editor, live, toc]
created: '2021-01-17T07:13:51.223Z'
modified: '2021-01-17T07:14:21.293Z'
---

# toc-lib-editor-live

# live-editing

# markdown-live-doc

- react-live /2.5kStar/MIT/202007
  - https://github.com/FormidableLabs/react-live
  - https://react-live.netlify.com/
  - render React components with editable source code and live preview.
  - 依赖react-simple-code-editor, bubble, prism
  - https://github.com/uber/react-view
    - /438Star/MIT/202009
    - The first prototype of React View was even using react-live internally 
    - but eventually we needed a finer-grained control over the compilation process and a more flexible API. 
    - We also rely on babel and babel-parser instead of buble.
- https://github.com/axe312ger/mdx-live-editor
  - mdx editor to edit mdx and preview live in your browser.
  - Based on EasyMDE and MDX Runtime
- https://github.com/JReinhold/mdx-deck-live-code
  - A component for mdx-deck to live code in your slides
- jxnblk
  - https://github.com/jxnblk/live-doc
    - Convert markdown to live React demos
  - https://github.com/jxnblk/ok-mdx
    - Browser-based MDX editor
  - https://github.com/jxnblk/mdx-go
    - fast MDX-based dev server for progressive documentation
    - 依赖@mdx-js/mdx、mdx-live/style
  - https://github.com/c8r/x0
    - Document & develop React components without breaking a sweat
    - 依赖@mdx-js/mdx、react-router、react-live、styled-comp

- https://github.com/XiaoMi/hiui
  - 依赖react-redux、react-live渲染mdx文档
  - 组件展示区的上下结构：预览块、描述块、可折叠代码块
  - 组件文档基于react-live，在代码块外部提供了code、copy、reset这3个按钮
  - 代码块支持高亮
- https://github.com/youzan/zent
  - 依赖react-loadable、react-router、prismjs、react-beautiful-dnd渲染mdx文档
  - markdown顶部存放本文档内容的元信息，包括路由
- https://github.com/wilsson/papyrum
  - a tool that will help you document your design system or library of components based on React.
  - Zero config, MDX based, Typescript support, Syntax highlighting with Prism React Renderer
  - 依赖redux、remark-parse、unified、webpack、babel
  - 组件展示区的上下结构：预览块、代码块
  - 代码块支持高亮，代码显示支持dark模式
  - 且鼠标hover到代码块右上角时显示copy悬浮按钮(鼠标移出右上角时移除悬浮按钮)
- https://github.com/coralproject/mdx-book
  - a docz inspired documentation generator with a playground and without gatsby and ssr.
  - 实现结果较简单
  - 依赖@mdx-js/mdx、gray-matter、prism-react-renderer
- https://github.com/artsy/palette
  - 组件展示区的结构左右：预览块、代码块；rmwc组件库的文档也是左右结构
  - 依赖gatsby
- https://github.com/SoftwareBrothers/better-docs
  - 提供了组件api及组件预览展示
  - 依赖vue-docgen-api、vue2-ace-editor、react-frame-component(创建iframe)
- https://github.com/dfosco/design-system-sandbox
  - an in-browser editor to prototype with design systems in React. Based on react-live.
- https://github.com/Adslot/adslot-ui
  - A library of core components used to develop our Adslot and Symphony products.
  - 依赖react-docgen、react-redux、react-bootstrap
  - 包括组件展示、代码编辑、api类型说明 
  - 实现不复杂，但功能完整
- https://github.com/cratebind/minerva-ui
  - 依赖@mdx-js/react、@reach/component、styled-system、react-docgen-typescript-loader
- https://github.com/wangdicoder/tiny-ui
  - 依赖popperjs、webpack
  - 每个组件都有一个index.md，开头会import各种依赖，然后显示各demo预览，最后纯手写api类型说明
- https://github.com/thomaswang/react-live-playground
  - Playground wrapper around React Live
- https://github.com/shine-design/shine-design
  - 依赖docz
  - 使用tab形式切换显示组件预览和代码，还提供modal弹窗显示组件，可参考ag-grid的组件示例
- https://github.com/xsky-fe/wizard-ui
  - 依赖gatsby，文档默认只显示组件预览，点击展开代码时会给出现深色背景然后预览区域变大下方出现代码
- https://github.com/moosend/mooskin-ui
  - 默认只显示组件预览，点击代码会出现侧边栏提供编辑
- https://github.com/UNDataForum/design-system
  - 点击copy按钮后会显示打勾，过一会儿自动恢复copy按钮
  - 文档基于gatsby实现，模仿github primer的文档
- https://github.com/uber/baseweb
  - 组件展示区上下结构，按钮有copy、reset、format、api、openWithCodePen/sandbox
- https://github.com/auth0/cosmos
  - 将 `import { Button } from '@auth0/cosmos';` 写在页面最上方，而不是写在组件展示块

## react-playgrounds

- react-live /2.5kStar/MIT/202007
  - https://github.com/FormidableLabs/react-live
  - https://react-live.netlify.com/
  - render React components with editable source code and live preview.
  - depends on react-simple-code-editor, bubble, prism
- react-runner /25Star/MIT/201908
  - https://github.com/nihgwu/react-runner
  - https://nihgwu.github.io/react-runner/
  - Run your React code on the go
  - 被Autodesk/react-base-table用来展示示例
  - react-runner is inspired by react-live heavily, I love it, but I love arrow functions for event handlers instead of bind them manually 
  - use Sucrase instead of Bublé to transpile the code.
  - If you are using react-live and want a smooth transition, react-live-runner is there for you which provide the identical way
- react-view /438Star/MIT/202009
  - https://github.com/uber/react-view
  - The first prototype of React View was even using react-live internally 
  - but eventually we needed a finer-grained control over the compilation process and a more flexible API. 
  - We also rely on babel and babel-parser instead of buble.

# more
