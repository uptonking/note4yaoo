---
title: toc-lib-editor-builder-designer
tags: [builder, editor, lib, toc]
created: 2020-09-09T06:26:47.069Z
modified: 2020-11-17T13:38:19.107Z
---

# toc-lib-editor-builder-designer

# guide
- designer侧重编辑器、图形、样式布局，产物偏向静态组件
  - 将可拖拽编辑器用于界面设计、交互设计、产品原型设计

- ui-prototype
  - https://uigenerator.org/
# popular
- grida /2.2kStar/apache2/202508/ts/design2code
  - https://github.com/gridaco/grida
  - https://grida.co/
  - Skia based performant live design collaboration & workspace app - redesigned for both designers and developers
  - Grida is a platform that will automatically transform your Figma design to developer-friendly code for Web & Mobile apps.
  - Grida is a open source Canvas platform where you can manage your database, design websites, and create forms in one place. Designed for Supabase.
  - Database / CMS
    - View in list/gallery/charts View
    - Connect your Supabase Project (Table, Views, Storage, Auth)
    - Filter, Sort, Search (Locally and FTS).
  - Forms
    - 30+ Inputs (file upload, signature, richtext, sms verification, etc)
    - Logic blocks & Computed Fields
    - Grida-Database or Supabase-Table Integration
    - Headless Usage - API-only usage
  - Canvas
    - ✅已实现 DOM Backend, WebGL Backend (Skia), SVG Editor (TP), Infinite Canvas
    - Import from Figma
    - 未实现  WebGPU Backend (Skia Graphite)
  - studio is built upon skia graphics library
  - studio's surface is built on react
  - https://github.com/gridaco/grida/tree/main/editor
    - 依赖rxdb.v10、pouchdb-idb、rxjs、recoil、firebase、mui.v5
  - https://github.com/gridaco/design-server
  - https://github.com/gridaco/nothing
    - everything drawable graphics engine. Built for Grida
    - Open source UI graphics tool
  - https://github.com/gridaco/code
    - Grida's Design to code core library. 
    - Convert your figma, sketch and adobe xd design to flutter, react, vue and more.

- craft.js /7kStar/MIT/202410/ts/偏设计
  - https://github.com/prevwong/craft.js
  - https://craft.js.org/
  - A React Framework for building extensible drag and drop page editors
  - core依赖react、lodash，layers依赖react-contenteditable、s-c
  - 富文本编辑器和页面编辑器的区别，主要在是否使用conetenteditable
  - 支持分栏布局，支持容器嵌套，支持layers图层显示
  - 🐛 
    - 拖拽移动改变分栏内的顺序时，不会自动调整宽度和布局
  - 支持undo
  - Craft.js solves this problem by modularising the building blocks of a page editor. It ships with a drag-n-drop system and handles the way user components should be rendered, updated and moved
  - Craft.js is an abstraction where you implement your own page editor upon. 
    - For example, it does not come with a ready-made user interface.
    - However, you could still consider using the examples as a starting point.
  - many aspects of Craft.js are written with `react-dnd` as a reference. 但未使用
  - The element positioning logic used in Craft.js is borrowed from Grape.js
  - [Can this be extended to be used on other JS framework like Vue or Svelte?](https://github.com/prevwong/craft.js/issues/101)
    - whole code is React dependend
  - [Future of Craft.js - taking it to the next level _202304](https://github.com/prevwong/craft.js/issues/507)
    - 📡 Reka is not a replacement for Craft. It's simply intended to replace the internal state management system in Craft
    - The current Craft's `EditorState` is essentially the equivalent of building a single UI component without states and props; and with the ability of adding/reordering JSX templates and mutating simple prop values of those JSX templates.
    - I spent the past couple of months trying to build a new state management system for Craft; one that could allow end-users of your page editors to build UI components that could be as complex as ones that developers could write in React code. 
    - The current Craft EditorState is a simple implicit tree data structure, whereas Reka is an AST. As such, a Reka AST for an equivalent EditorState is expected to be larger
- https://github.com/prevwong/reka.js /437Star/MIT/202404/ts/yjs/暂未用在craft
  - https://reka.js.org/
  - https://reka.js.org/docs/introduction
  - ✨ Reka is a state management system for building no-code editors
  - Reka solves this by providing an AST-powered state system that enables end-users to create UI components that are nearly as complex as ones that developers could write in code
  - along with an interpreter to efficiently compute an output that could be rendered on the browser.
  - core依赖mobx、nanoid, 周边依赖mobx-react-lite、codemirror6、@lezer/highlight、acorn-jsx、yjs
  - 示例使用unist-ast
  - It's primarily built to serve as the new state management system to power `Craft.js` and its page builders.
  - Reka computes a Component instance from its State by generating a `View` tree
    - Whenever there's a change made to the State, Reka efficiently recomputes the updated View.
    - The View tree is a simple serializable JSON structure.
    - So regardless of what UI framework you're working with to build your page builder - whether it's React, Vue or Svelte; building a renderer for Reka simply means taking this JSON structure and rendering it in your preferred UI framework.
  - Reka provides an external package that allows real-time collaboration via a fully-featured CRDT backed by `Yjs`.
  - [Show HN: Build your own no-code editor with Reka.js | Hacker News](https://news.ycombinator.com/item?id=35399384)

- webstudio-designer /172Star/MIT>AGPLv3/202212/ts
  - https://github.com/webstudio-is/webstudio-designer
  - https://webstudio.is/
  - Webstudio Designer is a NoCode Visual Tool inspired by Webflow
  - block块级元素不支持拖拽
  - 依赖lexical-editor、radix-ui、stitches、remix-auth、downshift
  - [Change license from MIT to AGPL V3 _202307](https://github.com/webstudio-is/webstudio/pull/1980)

- silex /1.8kStar/AGPLv3/202404/ts
  - https://github.com/silexlabs/Silex
  - http://www.silex.me/
  - https://editor.silex.me/
  - https://v3.silex.me/en/
  - a no-code tool for building websites. 
  - 基于dom实现
  - It can be used online, offline or in a JAMStack project.
  - Silex lets you create websites without coding, but it also has built-in editors for HTML, CSS, and JavaScript for when you need more control
  - it has a plugin system and can integrate with headless CMS and static site generators, it is part of the JSAMStack ecosystem since the v3
  - [Feature: storage connectors _202307](https://github.com/silexlabs/Silex/issues/1515)
    - Silex v3 aims to focus on free and open-source services to align with the principles of open data, user privacy, and freedom of choice. 
    - Gitlab is now implemented (v3.silex.me) _202309

- https://github.com/app-generator/free-site-builder /Free4NonCommercial/202310/ts/inactive
  - https://www.simpllo.com/
  - Free & Open-Source Site Builder that uses Vanilla JS and a Remote Server for components injection - Actively supported by AppSeed.
  - 一个ui厂商开源的编辑器
  - 支持在弹窗中预览

- https://github.com/QuiiBz/ogstudio /MIT/202403/ts
  - https://ogstudio.app/
  - Figma-like OG (Open Graph) Image builder
  - 依赖drizzle-orm、libsql、nextjs、lucia-auth、vercel/kv、tanstack-query、dnd-kit、zustand

- https://github.com/plantain-00/schema-based-json-editor
  - https://plantain-00.github.io/schema-based-json-editor/packages/react/demo/
  - A reactjs and vuejs component of schema based json editor.
- https://github.com/plantain-00/template-editor-demo /ts/vue3
  - https://plantain-00.github.io/template-editor-demo/
  - A poster template edit and generation design document and demo
  - 依赖vue-schema-based-json-editor、fast-json-patch
  - 根据 typescript 代码中定义的数据结构模型来生成 json schema，并用于验证数据合法性。
  - 海报模板也可以使用模版引擎来简化生成逻辑，只不过操作的是设计元素而不是 html 标签。
  - 可以通过创建、websocket 转发、应用 json patch 的方式，实现简单的多人协同编辑模板功能。

- brick-design/react-visual-editor /2.3kStar/MIT/202310/ts/inactive
  - https://github.com/brick-design/brick-design
  - https://brick-design.github.io/brick-design/
  - 组件可视化拖拽，页面搭建，源码生成工具, 自由拖拽嵌套
  - 低代码框架，支持流式布局与自由布局拖拽编排，可视化拖拽、随意嵌套组合
  - 拖拽不流畅
  - 基于antd
  - old-repo
    - https://github.com/brick-design/react-visual-editor

- https://github.com/plasmicapp/plasmic /AGPL + MIT/202402/ts/python
  - https://www.plasmic.app/
  - Visual page builder and web design tool for any website or web app tech stack
  - Plasmic is a platform
    - Visual builder / web design tool--this is the heart of Plasmic
    - Headless CMS for structured content (or bring your own CMS)
    - Growth optimization tools (A/B testing, personalization, analytics)
  - 前端依赖react-aria、quill
  - 后端依赖python、fastapi、sqlalchemy、ipdb、pydynamodb
  - 后端代码很少
  - [Does this repository include the designer UI?](https://github.com/plasmicapp/plasmic/issues/23)
    - It currently doesn't; will add clarification on this.

- blocks /MIT/4.6kStar/202006/js/inactive
  - https://github.com/blocks/blocks
  - https://blocks-ui.com/
  - A JSX-based page builder for creating websites without writing code
- openchakra /MIT/1.6kStar/202209/inactive
  - https://github.com/premieroctet/openchakra
  - https://openchakra.app/
  - 画布编辑区全部基于dom实现
  - visual editor and code generator for React using Chakra UI

- VvvebJs /apache2/3.3kStar/202403/js
  - https://github.com/givanz/VvvebJs
  - http://www.vvveb.com/vvvebjs/editor.html
  - Drag and drop website builder javascript library.
  - 依赖jquery、bootstrap4

- grapesjs /25.1kStar/BSD/202510/ts/依赖少
  - https://github.com/GrapesJS/grapesjs
  - https://github.com/artf/grapesjs
  - https://grapesjs.com/
  - a free and open source Web Builder Framework 
  - 依赖backbone.v1、backbone-undo、codemirror5、underscore
  - GrapesJS was designed to be used inside a CMS to speed up the creation of dynamic templates. 
  - [Proprietary VS open source _202508](https://github.com/GrapesJS/grapesjs/discussions/6586)
    - This whole repo still has the same exact license so nothing has changed from that perspective.
    - we added SDK docs on top

- react-page /8.3kStar/MIT/202304/ts/redux/inactive
  - https://github.com/react-page/react-page
  - https://react-page.github.io/
  - 画布编辑区全部基于dom实现，拖拽不够流畅
  - content editor for the browser - based on React and Redux and written in TypeScript. WYSIWYG on steroids.
  - 依赖react-redux、redux-undo、mui.v5、react-dnd、uniforms
  - 12-column grid responsive grid layout
  - Undo & Redo, copy and hotkey support
  - LGPLv3 to MIT_202010

- https://github.com/sitebud
  - https://sitebudcms.com/documentation
  - https://github.com/ipselon/sitebud-libs
  - SiteBud CMS, a content management system tailored for both content creators and developers, leverages the power of NextJS and seamless GitHub integration.
- react-ui-builder-editor /GPL/12Star/202006
  - https://github.com/react-ui-builder/react-ui-builder-editor
  - An online editor of the Interactive Platform for React Component Libraries
  - Based on Webcodesk version 2.0.3
- Webcodesk /201907/MIT/40star
  - https://github.com/webcodesk/webcodesk-app
  - https://webcodesk.com/documentation/tutorial/create_main_page
  - 依赖electron，d3js
  - 直接拖拽现有组件生成项目，基于 react-app-framework
- UI-Builder /Apache2/19Star/201901
  - https://github.com/iwangbowen/UI-Builder
  - 基于 bootstrap 4和jquery实现

- react-design-editor /1.4kStar/MIT/202401/ts
  - https://github.com/salgum1114/react-design-editor
  - https://salgum1114.github.io/react-design-editor/
  - a module for React, written in Javascript/Typescript which provides two primary features: image-editor, bpm-workflow
  - 画布区是canvas，其余地方是dom，直接导出图片或json
  - developed direct manipulation of editable design tools like Powerpoint
  - primarily uses the Ant Design, Fabric.js and React, React-Ace
- https://github.com/bharathreddyza/react-design-editor /MIT/202105/ts/inactive
  - React Design Editor using Fabric.js
  - provides functionality similar to canva.com
  - 很多功能未完成
  - https://github.com/bazooka720/scenify-editor /MIT/202110/ts/inactive
- react-design-editor /1.6kStar/MIT/202304/ts
  - https://github.com/layerhub-io/react-design-editor
  - https://editor.layerhub.io/
  - https://github.com/layerhub-io/layerhub-io/tree/main/packages
  - Image, Presentation and Video editor. Canva clone
  - React design editor using fabric.js. 
  - [Show HN: Open Source Canva Clone | Hacker News _202208](https://news.ycombinator.com/item?id=32568423)
    - Reposting my comment here for better visibility. To put it gently, this is a fork of other people's work without proper attribution. 
    - Looks like this project was derivative work 
    - All you need to create/customize your graphic/presentation editor should be there. There are some other private packages that are optional: Exporting content in server side: PNG, pdf, etc.

- react-designer /1.7kStar/MIT > CC-BY/201905/js/inactive
  - https://github.com/react-designer/react-designer
  - http://react-designer.github.io/react-designer/
  - Editable vector graphics in your react apps
  - 形状基于svg
  - 依赖react-color、lodash
  - https://github.com/fritz-c/react-shape-editor
    - /49Star/MIT/202002
    - Simple shape editor component with React and SVG

- antd-visual-editor /443SStar/201904
  - https://github.com/yu-tou/antd-visual-editor
  - https://yu-tou.github.io/antd-visual-editor/index.html

- pagedraw /2.8kStar/MIT/201906/CoffeeScript/inactive
  - https://github.com/Pagedraw/pagedraw
  - https://pagedraw.io/
  - a UI builder for React web apps
  - It works like a Sketch or Figma style design tool, but emits good quality JSX code. 
  - Pagedraw is shutting down. Ultimately, we think Pagedraw is the wrong product. 
  - We think you can get 90% of the benefits of Pagedraw by just using JSX better. 
  - 产品的ui类似codepen的三栏编辑器，分别是可拖拽组件编辑器editor、入口处源码code、预览视图preview, 其中code和preview都基于stackblitz实现
- misc
  - https://github.com/cerner/kaiju
    - A drag and drop web editor for React components.
  - https://github.com/ascoders/gaea-editor
    - Design websites in your browser. A smart web editor!
  - https://ant-extensions.herokuapp.com/?path=/story/page-maker-example--example
  - https://github.com/wrannaman/mui-scaffold
    - Drag and drop material ui components on to the page.

- https://github.com/components-ai/css.gui /ts
  - https://components.ai/css-gui
  - Visual development environment for CSS
  - 效果类似page-builder
# designer-prototype
- https://github.com/penpot/penpot /MPLv2/202503/Clojure
  - https://penpot.app/
  - The open-source solution for design and prototyping. 
  - Penpot works with SVG, a standard format, for all your designs and prototypes . 
    - This means that all your stuff in Penpot is portable and editable in many other vector tools and easy to use on the web.

- alva /MIT/3.5kStar/201907/ts
  - https://github.com/meetalva/alva
  - https://meetalva.io/
  - Create living prototypes with code components.
- Framer /MIT/5.6kStar/201905
  - https://github.com/koenbok/Framer
  - We are in the process of open sourcing our new Framer Library for React. Come back soon.

- react-proto
- ReacType

- 基于vue
  - https://github.com/fireyy/vue-page-designer
  - https://github.com/baianat/vuse
- misc
  - https://github.com/uxbox/uxbox
  - https://github.com/elementor/elementor
    - Requires PHP: 5.6
  - 稿定设计
    - 在线PS、自动抠图、海量素材

- https://github.com/Imam-Abubakar/mural /MIT/202304/ts/inactive
  - https://mural-one.vercel.app/
  - a simple design editor built using FabricJS and React
  - offers features akin to canva.com 
  - Fabric: provides interactive object model on top of canvas element
  - Scenify: for rich features added atop the image designer
  - Base-UI(From MUI) and Styletron: for styling

- https://github.com/lidojs/canva-clone /202311/ts/inactive/paid
  - https://demo.lidojs.com/
  - a design tool based on Reactjs. UX almost the same canva.
  - developed from scratch with ReactJS
  - 依赖dnd-kit、prosemirror、immer、html-to-image、react-responsive-masonry
  - 画布基于dom实现，支持缩放
  - 支持下载png
  - to run lidojs you have to get pro license
# page/site/ui-builder
- https://github.com/measuredco/puck /MIT/202404/ts
  - https://puckeditor.com/
  - https://demo.puckeditor.com/edit
  - The visual editor for React.
  - 不能直接在预览图上修改，需要在侧边栏属性上修改
  - 依赖react-spinners、@measured/dnd、auto-frame-component
  - https://github.com/measuredco/auto-frame-component
    - An iframe component that automatically syncs styles from the host.
    - An implementation of react-frame-component.
    - Shares an API with react-frame-component, and exposes some additional props.
  - https://github.com/measuredco/dnd
    - fork of hello-pangea/dnd

- page-builder /NALic/77Star/202008
  - https://github.com/cqm1994617/page-builder
  - 依赖：antd4, braft-editor, koa, react-dnd, redux-thunk2, styled-components, swiper 
  - 一个页面构建平台demo，项目以展示思路为主，只有打包和预览部分运用了node，并未使用数据库
  - 当前项目中所包含的页面以及页面中的组件和组件中的状态，均以json格式存在redux store当中

- https://github.com/belastrittmatter/Framely /MIT/202503/ts
  - https://framely.site/
  - The open-source drag-and-drop website builder boilerplate.
  - offering multi-tenancy, custom domain support, and a flexible drag-and-drop web editor.
  - Authentication: User authentication powered by Clerk.
  - Multi-Tenancy: Full support for subdomains
  - Prisma & MySQL: Database ORM and relational database.
# h5-editor
- h5-dooring /7kStar/GPLv3/202312/ts
  - https://github.com/MrXujiang/h5-Dooring
  - http://h5.dooring.cn/
  - https://dooring.vip/
  - 轻松搭建H5页面, H5网站
  - https://github.com/H5-Dooring/dooringx
    - 快速高效搭建可视化拖拽平台
  - https://github.com/MrXujiang/pc-Dooring
    - 轻松搭建PC页面, Web网站, PC端网站. lowcode
  - H5可视化页面配置解决方案
  - 技术栈以react和typescript为主， 后台采用nodejs开发, 正在探索h5-lowcode解决方案
  - editor依赖antd4、braft-editor、react-dnd
  - ui依赖umi、antd-pro、react-grid-layout
  - https://github.com/MrXujiang/lowcode-cms /MIT/202305/js/inactive
    - 基于dooring低代码社区的开源cms系统
    - 后端依赖koa-session、koa-views、pug、qiniu
    - 前端依赖antd-pro-layout、umi.v3、braft-editor、turndown
    - server基于nodejs的服务端, 启动后可直接访问3000 端口, 也就是内容SSR端
    - admin CMS的管理后台, 集成了用户管理, 内容审核, 内容发布, 数据统计等模块

- luban-h5 /5.6kStar/GPLv3/202209/js/vue
  - https://github.com/ly525/luban-h5
  - https://ly525.gitee.io/luban-h5
  - 鲁班H5是基于Vue2.0开发、通过拖拽快速生成页面的平台
  - 类似 易企秀、Maka、百度 H5 等平台

- https://github.com/lzuntalented/lz-h5-edit
  - /289Star/NALic/202009
  - http://show.lzuntalented.cn/
  - react版h5微场景编辑器，一款类似【易企秀】【兔展】的H5微场景编辑器
- https://github.com/react-ui-builder/wcd-ant-design
  - /4Star/MIT/202006
  - Since React UI Builder is based on a visual Web application builder - Webcodesk
  - we use Webcodesk to create the component library locally.
# d2c/design-to-code
- https://github.com/BigFishTeam/dream-builder /MIT/202205/ts/inactive
  - 轻量级中后台前端可视化搭建平台，不限制任何组件库和框架，插件化集成，拥有强大的页面编排能力
  - 不限制任何 react 组件库，默认内置常用业务组件: sui-components、antd
  - core: 底层数据结构，主要包括：AST 树、执行引擎、request 请求等基类

- https://github.com/zuoyanart/lens /apache2/202206/js/inactive
  - 一个通过智能算法将设计稿转换为前端页面的产品（design to code），是`低代码`平台的一个分支方向， 
  - 他的输入是设计稿产出是前端页面，中间无需值守即可自动完成
  - 此项目可以一键将 Sketch、Photoshop 的设计稿转换为可维护的前端代码

- https://github.com/winyh/astx /202003/js
  - 基于React技术栈构建一个可视化搭建平台，通过拖拽的方式构建中台
  - 代码自动生成底层技术原理是AST, DSL做功能辅助
  - 很多大的平台在开始做这样的可视化搭建平台，节约项目开发成本。在目前来看，没有特别好的系统解决方案。微软的power，阿里云的云凤蝶，金蝉等

- https://github.com/abi/screenshot-to-code /MIT/202410/python
  - https://screenshottocode.com/
  - Drop in a screenshot and convert it to clean code (HTML/Tailwind/React/Vue)
  - Now supporting Claude Sonnet 3.5 and GPT-4o!
  - https://github.com/liseami/screenshot-to-code
    - Fork了Screenshot to Code这个项目，修改了前端和后端的Dockerfile，解决了国内Docker源、pip源、npm源拉取不了的问题。你只需要下载源码，在根目录docker-compose up -d --build，一键部署在本地
# json-ui-editor
- https://github.com/acrodata/gui /MIT/202406/ts/angular
  - https://acrodata.github.io/gui/
  - JSON powered GUI for configurable panels
  - Built on top of Angular Reactive Forms
  - Uses Angular Material as basic UI library
# more
- react-drag-drop-layout-builder /NALic/172Star/201904/ts
  - https://github.com/chriskitson/react-drag-drop-layout-builder
  - 依赖material-ui.v3、immutablejs4、react-dnd7
  - [Build a Drag and Drop (DnD) layout builder with React and ImmutableJS](https://javascript.plainenglish.io/build-a-drag-and-drop-dnd-layout-builder-with-react-and-immutablejs-78a0797259a6)

- react-dnd-example /45Star/NALic/202106/js
  - https://github.com/kustomer/react-dnd-example
  - https://codesandbox.io/s/github/annezhou920/react-dnd-example/
  - [Building Complex Nested Drag and Drop User Interfaces With React DnD](https://medium.com/kustomerengineering/building-complex-nested-drag-and-drop-user-interfaces-with-react-dnd-87ae5b72c803)
  - ref
    - https://github.com/annezhou920/react-dnd-example

- https://github.com/h5ds/h5ds /201912/js/inactive
  - 只开源了编辑器(v5.x版本)页面的代码，如需获取最新版本的（v6.x）源码请购买商业授权

- https://visly.app/

- https://github.com/swagger-api/swagger-editor
  - Swagger Editor lets you edit Swagger API specifications in YAML inside your browser and to preview documentations in real time. 

- https://github.com/lovasoa/SQLpage /MIT/202404/rust
  - https://sql.ophir.dev/
  - SQL-only webapp builder, empowering data analysts to build websites and applications quickly
  - you write simple .sql files containing queries to your database to select, group, update, insert, and delete your data, and you get good-looking clean webpages 

- [List of drag & drop React UI builders_202003](https://www.reddit.com/r/reactjs/comments/flz4t9/list_of_drag_drop_react_ui_builders/)
