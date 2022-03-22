---
title: toc-lib-editor-live-doc-knobs
tags: [doc, editor, live, toc]
created: '2021-01-17T07:13:51.223Z'
modified: '2021-03-03T21:48:48.379Z'
---

# toc-lib-editor-live-doc-knobs
- guide
  - react组件的实现偏向all in js，所以实现在线编辑只需一个编辑器
  - 传统ui组件如bootstrap/web-comp，需要考虑html, css, js三部分，所以实现在线编辑需要多个编辑器，类似codepen
  - react-live进一步的研发方向可以考虑类似storybook的controls
  - 考虑支持多种实现的切换，如react/vue/vanillajs，此时可考虑仅展示不编辑

- react-live 在线编辑代码是伪需求
  - 对于简单的情况，不需要，直接提供需求文本或选项的按钮就可以了
  - 对于复杂的场景，短小的输入框和提示功能太弱了，更推荐嵌入codesandbox的方案
  - 关注observable notebook的发展变化，特别是对于代码的支持力度

- ref
  - [search: react live editor](https://github.com/search?o=desc&q=react+live+editor+stars%3A%3E0&s=updated&type=Repositories)
# markdown-live-doc
- react-view /558Star/MIT/202105/ts
  - https://github.com/uber/react-view
  - https://react-view.netlify.com/
  - 优点是除了支持直接编辑源码，还支持类似storybook的knobs，通过复选框直接设置属性值，甚至能直接输入函数形式的字符串作为属性值
  - Prior Art: react-live, sb-knobs, playroom
  - The first prototype of React View was even using react-live internally 
  - but eventually we needed a finer-grained control over the compilation process and a more flexible API. 
  - We also rely on babel and babel-parser instead of buble.
  - React View aims to make documentation more interactive and useful.
- react-live /2.9kStar/MIT/202011/js
  - https://github.com/FormidableLabs/react-live
  - https://react-live.netlify.com/
  - 依赖react-simple-code-editor, bubble, prism
  - 只支持直接编辑源码
  - render React components with editable source code and live preview.
  - https://github.com/FormidableLabs/component-playground
    - A component for rendering React components with editable source and live preview
- react-runner /25Star/MIT/201908
  - https://github.com/nihgwu/react-runner
  - https://nihgwu.github.io/react-runner/
  - Run your React code on the go
  - 被Autodesk/react-base-table用来展示示例
  - react-runner is inspired by react-live heavily, I love it, but I love arrow functions for event handlers instead of bind them manually 
  - use Sucrase instead of Bublé to transpile the code.
  - If you are using react-live and want a smooth transition, react-live-runner is there for you which provide the identical way

- https://github.com/jquense/jarle
  - https://jquense.github.io/jarle/
  - JARLE only looks at the last thing you return, so write whatever you need in front of it.
  - Jarle removes boilerplate code in your examples, by rendering the last expression in your code block
  - Differences from React Live
    - No extra compiling. Jarle only packages a JSX transformer, making it lighter than alternatives.
    - Smart rendering

- https://github.com/axe312ger/mdx-live-editor
  - mdx editor to edit mdx and preview live in your browser.
  - Based on EasyMDE and MDX Runtime
- https://github.com/PolymerLabs/playground-elements
  - Playground Elements are a set of components for creating interactive editable code experiences on the web
  - Embed editable code examples in your documentation.
  - Playground never sends code to a backend server. Instead, Playground uses a Service Worker to create a virtual URL-space that runs 100% within the browser.
  - Playground automatically compiles .ts files using TypeScript. Compilation happens in a Web Worker on a separate thread
  - Playground uses Web Components, so it doesn't require a framework. But it will play nicely with any framework you're already using, like React, Vue, and Angular.
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
# props-edit-control
- openchakra /MIT/1.6kStar/202008
  - https://github.com/premieroctet/openchakra
  - https://openchakra.app/
  - visual editor and code generator for React using Chakra UI
- https://github.com/malerba118/react-handoff
  - https://codesandbox.io/s/async-night-7kyrq?file=/src/App.tsx
  - 依赖chakra-ui, emotion
  - aimed to turn any react app into a visual editor where you can visually tweak and persist props from the browser.
  - enables designers and developers to work in parallel
  - 修改后组件的配置可以导出为json，而组件的默认值从json初始化

- https://github.com/grommet/grommet-designer
  - https://designer.grommet.io/
  - A tool to design screens using grommet components.
- https://github.com/grommet/grommet-theme-designer
  - https://theme-designer.grommet.io/
  - A tool to design grommet themes.
  - 提供了dashboard、list、form、document4个示例

- https://github.com/Raathigesh/retoggle
  - https://retoggle.netlify.app/
  - https://codesandbox.io/s/kw21kn3063?file=/src/index.js
  - 只能修改state，不能修改props
  - Retoggle is a collection of React hooks which provides UI toggles to manipulate your component state from outside. 
  - This library is inspired by [ideas from Dan Abramov](https://twitter.com/dan_abramov/status/1058834904207761409).
  - A wide range of knobs
  - Themeable components

- https://github.com/jeremyckahn/props-editor
  - https://jeremyckahn.github.io/props-editor/
  - A UI for modifying React component props
  - 直接在json中编辑属性值

- https://github.com/yairEO/knobs
  - https://codepen.io/uptonking/pen/gOwNyON
  - UI knobs controllers for JS/CSS live manipulation of various parameters
  - 支持compact view，样式友好

- https://github.com/one-gourd/ide-props-editor
  - https://one-gourd.github.io/ide-props-editor/
  - 可以根据实际业务场景定制任何类型的属性编辑器，输出json
- https://github.com/code-easy-platform/properties-editor
  - Element to edit properties in the platform.

- https://github.com/ItsJonQ/controls
  - https://codesandbox.io/s/controls-demo-jjw83
  - A control panel for developing/prototyping React UI
- https://github.com/Ameobea/react-control-panel
  - https://control-panel.ameo.design/
  - This is a React port of control-panel that aims to replicate the functionality of the original 
  - ref
    - https://github.com/freeman-lab/control-panel
      - embeddable panel of inputs for parameter setting
- https://github.com/ekros/react-play-editor
  - Create React components and play with props and state using auto-generated forms.
  - 基于react15

- https://github.com/Garphild/react-state-panel-dev
  - Simple React component for show and change current state/props/content of component.

- https://github.com/cocopon/tweakpane
  - https://cocopon.github.io/tweakpane/getting-started.html
  - Compact GUI for fine-tuning parameters and monitoring value changes
  - You can add various components to Tweakpane. 
    - Inputs for fine-tuning parameters
    - Monitors for checking values
- https://github.com/maslick/radiaSlider /NoDeps
  - https://maslick.github.io/radiaSlider/demo/circular.html
  - a pure JavaScript circular/linear knob-style slider

- https://github.com/react-cosmos/react-cosmos
  - https://reactcosmos.org/
  - https://reactcosmos.org/live-demo/
  - An isolated component environment
  - Automatic UI controls for React component props

- https://github.com/pmndrs/leva
  - https://leva.pmnd.rs/
  - React-first components GUI
  - More than 12 different kinds of inputs available
# json-object-editor
- https://github.com/YMFE/json-schema-editor-visual
  - https://hellosean1025.github.io/json-schema-visual-editor/
  - A json-schema editor of high efficient and easy-to-use, base on React
  - 该工具已被用于开源接口管理平台： YApi
- https://github.com/matteobruni/object-gui
  - https://codepen.io/matteobruni/pen/oNxNvja
  - Object GUI is your fully customizable Javascript Object GUI Editor

- https://github.com/b-gran/object-editor-react
  - https://b-gran.github.io/object-editor-react/githubExample.html
  - Schema-aware editor for structured JSON objects (drop-in React component)
- https://github.com/BomdiZane/EditorJS-React-Renderer
  - https://err.bomdisoft.com/
  - A library for rendering flexible React components from block style data objects like those generated by codex editors like Editor.js.
  - This package works well with output from the Editor.js rich text editor library. However, there is no dependency on Editor.js. 
# react-live-code
- live-example /4Star/MIT/202012/js
  - https://github.com/mytecor/live-example
  - https://mytecor.github.io/live-example/
  - 依赖sucrase-browser
  - Like react-live, but much faster, smaller and customizable
- react-simple-code-editor /691Star/MIT/202001/js
  - https://github.com/satya164/react-simple-code-editor
  - http://satya164.xyz/react-simple-code-editor/
  - Simple code editor with syntax highlighting
- https://github.com/conorhastings/react-component-demo
  - A React Component To make live editable demos of other React Components
- https://github.com/styleguidist/react-styleguidist
  - /9.2kStar/MIT/202009
  - Isolated React component development environment with a living style guide
- https://github.com/milankinen/livereactload /201904
  - Live code editing with Browserify and React
# more
- examples
  - https://generative.parts/flag

- https://github.com/Khan/live-editor /202009/inactive
  - http://khan.github.io/live-editor/demos/simple/
  - This is the live coding environment developed for the Khan Academy Computer Programming curriculum. 
  - It gives learners an editor on the left (either ACE or our Blocks-based drag-and-drop editor) and an output on the right (either JS+ProcessingJS, HTML, or SQL).
- https://github.com/sofish/pen /201809
  - https://sofish.github.io/pen
  - enjoy live editing (+markdown)

- openchakra /MIT/1.6kStar/202008
  - https://github.com/premieroctet/openchakra
  - https://openchakra.app/
  - visual editor and code generator for React using Chakra UI

- https://github.com/sueddeutsche/editron
  - Editron is a JSON-Editor, which takes a JSON-Schema to generate an HTML form for user input and live validation

- [JavaScript Editor from Scratch to live-edit CSS Values in your Browser](https://dev.to/typo3freelancer/javascript-editor-from-scratch-to-live-edit-css-values-in-your-browser-244)
  - https://codepen.io/uptonking/pen/PoWmWEd
  - 基于css vars实现
