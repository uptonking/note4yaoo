---
title: toc-lib-editor-builder-lowcode
tags: [builder, lowcode, toc]
created: 2020-12-13T15:59:43.778Z
modified: 2020-12-28T12:24:09.275Z
---

# toc-lib-editor-builder-lowcode

# guide

- features
  - preview pc/mobile
  - toggle views: designer view, code view
  - 是否基于iframe

- tips
  - 通用型builder价值不大，但针对业务平台特别是app-store的builder对平台方和开发者的价值都很大
  - lowcode重逻辑轻设计，侧重给页面元素添加事件和逻辑，而不是样式布局，产物偏向非静态前端工程
  - 使用代码生成器的方式(tango/strapi)，优点是功能强，但不如配置方式性能高、体验好

- 基于ast实现lowcode的方案
  - craft/reka
  - tango, sparrow
  - vue

- cms-dev
  - cms业务架构一般分为 服务端、管理端、展示端
  - 管理端交互的核心通常是编辑器

- ali-LowCodeEngine目前仅支持生成React的前端代码
  - 制作成本固然低了，造出来的代码维护成本太高了
  - 这种东西，不会编程的人对他来说太复杂了，会编程的人来说太繁琐了。

- [什么是比较好的低代码产品_Tw93](https://zhuanlan.zhihu.com/p/596474809)
  - platform, baas, cms建站, airtable-like, workflow
  - 流程自动化
  - [对于低代码技术库的选型](https://blog.csdn.net/nihaio25/article/details/126517143)

- workflow类低代码
  - 简单场景类似表单，支持根据不同评分显示不同内容，如投诉/不足

- lowcode vs builder
  - 建站侧重于自动生成并发布页面，而不是编辑器

- resources
  - https://github.com/taowen/awesome-lowcode
# popular
- payloadcms /9.1kStar/MIT/202301/ts/slate
  - https://github.com/payloadcms/payload
  - https://payloadcms.com/
  - https://demo.payloadcms.com/admin
  - Headless CMS and Application Framework built with TypeScript, Node.js, React and MongoDB
  - cms只提供管理界面来拖拽生成数据对应的api，不提供预览内容的前端
  - 后端依赖express、mongoose、passport
  - 前端依赖dnd-kit、monaco-editor、slate、react-beautiful-dnd、faceless-ui、react-router5、webpack5、swc
  - 主要功能模块
    - 总体设计
      - 丰富的字段类型 fields
      - 管理后台、控制台界面
      - 权限控制、api
      - 版本管理
    - 内容管理
      - 类别标签 Categories
      - 文章内容
      - 媒体资源
      - 表单收集
    - 用户与设置
      - 用户列表
      - 通知与警告
      - 表单事件
      - 主页菜单配置
  - 支持Version History and Drafts, Automatically maintain a history of changes to any given collection document
  - 支持seo, auto-generate SEO meta data based on the content of your documents.
  - Block-based Layout Builder
    - 不是典型的block-editor，富文本作为字段block
  - Extensible SlateJS rich text editor
  - Extremely granular Access Control to your data, based on document or field-level functions
  - A Mongo database to store your data
  - store, retrieve, and manipulate data of any shape via full REST and GraphQL APIs
  - Local file storage & upload
  - Payload dynamically generates a React admin panel to manage your data. 
    - Admin panel is built with Webpack, code-split, highly performant (even with 100+ fields), and written fully in TypeScript.
  - A headless CMS is a system that sticks to what it's good at—managing content. 
    - It concentrates solely on granting administrators an effective way to author and maintain content, but doesn't control how and where that content is used.
  - [Compare Payload against other headless CMS: strapi, directus](https://payloadcms.com/compare)
  - [Roadmap Discussions](https://github.com/payloadcms/payload/discussions/categories/roadmap)
  - [Roadmap: Multiple Database Support](https://github.com/payloadcms/payload/discussions/287)

- n8n /28kStar/apache2+CC > FairCode/202301/ts/vue/依赖少
  - https://github.com/n8n-io/n8n
  - https://n8n.io/
  - Easily automate tasks across different services.
  - helps to connect any app with an API with any other, and manipulate its data with little or no code.
  - 后端依赖express、typeorm、pg、convict(config)、handlebars
  - 前端依赖vue2、jsplumb、codemirror6、jquery、monaco-editor、prismjs
  - 提供了自动化任务模版中心 Workflow templates，类似可复用的工具函数
    - Convert JSON to an Excel file
    - Creating an API endpoint
    - 内置了600+个任务
  - 主要功能模块
    - task-node, workflow, execution
    - tags
    - templates
    - sharing
  - [Change to the Sustainable Use License _202203](https://github.com/n8n-io/n8n/commit/521cf51e7cfb73ad60650b72206083d4c2666d29)
    - [n8n is not open source and your project is gaslighting its users _201910](https://github.com/n8n-io/n8n/issues/40)
  - https://github.com/drudge/n8n-nodes-puppeteer
    - n8n node for requesting webpages using Puppeteer, a Node library which provides a high-level API to control Chrome or Chromium over the DevTools Protocol.
- https://github.com/windmill-labs/windmill /5.9kStar/AGPLv3/22405/rust/svelte/js
  - https://windmill.dev/
  - Open-source developer platform to turn scripts into workflows and UIs. 
  - Open-source alternative to Airplane/Retool/pipedream.
  - 依赖svelte-headlessui、d3-dag
- https://github.com/PipedreamHQ/pipedream /7.1kStar/Paid/202309/ts
  - https://pipedream.com/
  - an integration platform for developers.
  - provides a free, hosted platform for connecting apps and developing event-driven automations. 
  - The platform has over 1, 000 fully-integrated applications, so you can use pre-built components to quickly send messages to Slack, add a new row to Google Sheets, and more.
  - This repo contains: The code for all pre-built integration components
  - Pipedream imposes limits on source and workflow execution, the events you send to Pipedream, and other properties by free/paid tier
  - [If Pipedream doesn't support Self-Host, what's the repo for?_202305](https://github.com/PipedreamHQ/pipedream/issues/6365)
    - contains all the code for Pipedream's app, actions and triggers. The code is deployed to Pipedream system.
    - Currently, Pipedream does NOT offer self-host option.

- baidu-amis /12.9kStar//apache2/202404/ts/偏前端工程
  - https://github.com/baidu/amis
  - https://baidu.github.io/amis/
  - https://aisuda.github.io/amis-editor-demo
  - amis是一个低代码前端框架，它使用 JSON 配置来生成页面，可以减少开发工作量，提升效率
  - core依赖mobx-state-tree、mobx-react、amis-formula、papaparse、react-json-view、uncontrollable
  - editor-core依赖json-ast-comments、react-frame-component、sortablejs
  - 依赖downshift、rc-menu、mobx、sortablejs、tinymce、codemirror5、echarts5
  - 支持切换pc/mobile视图
  - 🔡 支持查看源码json
  - 当为移动模式时，将采用 iframe 来预览
  - 🐛 配置产物与平台耦合
  - 默认JSSDK不是 hash 路由，但可改成 hash 路由模式
  - 可以 完全 使用 可视化页面编辑器 来制作页面：一般前端可视化编辑器只能用来做静态原型，而 amis 可视化编辑器做出的页面是可以直接上线的
  - amis只需 JSON 配置就能完成完整功能开发，包括数据获取、表单提交及验证等功能，做出来的页面不需要经过二次开发就能直接上线；
  - 除了低代码模式，还可以通过 自定义组件 来扩充组件，实际上 amis 可以当成普通 UI 库来使用
  - amis在百度内部得到了广泛使用，在 6 年多的时间里创建了 5 万页面
  - 在以下场合并不适合amis：大量定制UI、复杂或特殊的交互
  - 目前富文本编辑器基于两个库 froala 和 tinymce，默认使用 tinymce
  - https://github.com/aisuda/amis-editor-demo /202403/ts
    - amis可视化编辑器
  - [feat: 模板替换成新版本的 amis-formula v1.5.0 _202111](https://github.com/baidu/amis/pull/3057)
    - 新版直接使用ast转义
  - [我不明白这个 amis 低代码意义何在?](https://github.com/baidu/amis/issues/9156)
    - 低代码有一个很大的优势，就是在线运维，用amis配置的页面可以在线调整，不需要前端修改打包升级

- alibaba-lowcode-engine /8.9kStar/MIT/202212/ts/偏页面
  - https://github.com/alibaba/lowcode-engine
  - https://lowcode-engine.cn/
  - https://lowcode-engine.cn/demo/demo-general/index.html
  - 一套面向扩展设计的企业级低代码技术体系
  - 引擎完整实现了低代码引擎 搭建协议、物料协议、资产包协议
  - engine依赖fusion-next-ui、自研plugins
  - editor依赖mobx-react、power-di、fusion-next-ui
  - renderer依赖fetch-jsonp、socket.io
  - 支持切换pc/mobile
  - 🔡 支持查看源码js工程并下载zip
  - 画布渲染使用了设计态与渲染态的双层架构。设计器和渲染器其实处在不同的 Frame 下，渲染器以单独的 iframe 嵌入。这样做的好处，一是为了给渲染器一个更纯净的运行环境，更贴近生产环境，二是扩展性考虑，让用户基于接口约束自定义自己的渲染器。
  - 🐛 不支持配置路由
  - 主要功能模块
    - 页面与大纲
    - 组件与资源
    - 数据源
    - 源码面板
    - 搭建编辑器、属性面板
  - LowCodeEngine目前仅支持生成React的前端代码
    - 制作成本固然低了，造出来的代码维护成本太高了
    - 这种东西，不会编程的人对他来说太复杂了，会编程的人来说太繁琐了。
  - 不支持在editor拖拽修改block顺序，只能在大纲拖拽
  - [阿里低代码引擎简介](https://lowcode-engine.cn/site/docs/guide/quickStart/intro)
  - https://github.com/alibaba/lowcode-demo
  - [关于编辑器怎么整合到，业务系统中 _202306](https://github.com/alibaba/lowcode-engine/issues/21s t r a p60)
    - 现在的编辑器，没有登录和路由，怎么整合到日常的业务系统里呢
    - 登录要自己写插件及服务端去处理，路由不建议，本项目by design是作为独立页面使用，如果要嵌入其他页面或spa需要iframe方式

- tmagic-editor /3.9kStar/apache2/202311/ts/偏页面
  - https://github.com/Tencent/tmagic-editor
  - https://tencent.github.io/tmagic-editor/docs/index.html
  - https://tencent.github.io/tmagic-editor/playground/index.html#/form-editor
  - 页面可视化平台
  - 不支持切换pc/mobile，但可缩放画布
  - 🔡 支持查看源码类似json的js-dsl
  - 编辑器是使用 vue3 开发的，但使用编辑器的业务可以不限框架，可以用 vue2、react 等开发业务组件。
    - 编辑器中最终保存得到的配置结果，同时也是tmagic-editor页面最终渲染的描述文件，就是一份 JS schema 形式的 DSL。
    - 在tmagic-editor编辑器中，所有的操作和配置信息，最终都保存成这一份 DSL。
    - 这份配置在tmagic-editor runtime 中被加载和渲染
  - 由于tmagic-editor在编辑器中的模拟器是通过 iframe 渲染的，和tmagic-editor平台本身可以做到框架解耦，所以 runtime 也可以用不同框架开发。目前tmagic-editor提供了 vue2/vue3 和 react 的 runtime 示例。
  - runtime 概念，tmagic-editor编辑器中心的模拟器画布，是一个 iframe（这里的 runtimeUrl 配置的，就是你提供的 iframe 的 url），其中渲染了一个 runtime，用来响应编辑器中的组件增删改等操作。

- https://github.com/NetEase/tango /1.8kStar/MIT/202404/ts/ast/偏前端工程
  - https://netease.github.io/tango-site/
  - https://tango-demo.musicfe.com/designer/
  - 一个源码驱动的低代码设计器框架
  - 支持切换pc和mobile
  - 🔡 支持查看源码react项目
  - Sandpack提供了一个独立的 iframe 运行代码，可实现代码的运行时环境隔离，避免污染全局变量
  - 支持配置路由
  - 🐛 缺点是codesandbox实时将ast生成业务框架代码再运行性能低、体验差
    - 未开放源码产物下载
  - 使用代码生成器的方式，优点是功能强大，但不如配置方式性能高
  - 经历网易云音乐内网生产环境的实际检验，可灵活集成应用于低代码平台，本地开发工具等
  - 基于源码 AST 驱动，无私有 DSL 和协议
  - 提供实时出码能力，支持源码进，源码出
  - 提供灵活易用的设计器 React 组件
  - 感谢 CodeSandbox 提供的 Sandpack 项目，为 Tango 提供了强大的基于浏览器的代码构建与执行能力
  - 主要包括 3 个核心组成部分，分别是：
    - 引擎内核：负责建立文件，节点模型，提供输入输出能力。
    - 拖拽引擎和可视化面板：提供可视化开发能力
    - 渲染沙箱：提供源码在浏览器上的编译执行能力。
  - [技术架构概览 | 基于源码的低代码引擎](https://netease.github.io/tango-site/docs/designer/design/overview)
    - 我们在 2023年8月底正式开源了 Tango 低代码引擎
    - 传统的低代码搭建方案往往采用定义私有 Schema 协议来可视化表达视图逻辑，也就是将代码逻辑转换为私有的描述, 这类方案很容易面临不断膨胀的私有 JSON 协议
    - ESTree规范作为主流的处理 JavaScript 源代码的标准社区协议，被广泛用于浏览器 JavaScript Parser 的实现。借助于 ESTree 协议，可以完美的实现对源码逻辑的描述
    - 借助于 ESTree 规范，我们无需定义私有的渲染描述协议，并且可以低成本的实现代码到协议，协议到代码到互转
    - 首先将源代码解析为 AST。用户的拖拉拽等操作则映射为对 AST 的遍历和修改。最后将新的 AST 重新生成代码，交给设计器沙箱去渲染执行
    - 对 AST 的解析、遍历、修改、生成，则可以借助大量的社区工具，这里我们选择的是 babel
    - 首先是引擎初始化。源码文件会被引擎内核解析进行状态初始化。接下来，对于用户的操作，会触发浏览器事件，引擎接收到相应的事件，触发内核中的状态变更，更新 AST。
    - 然后，内核会基于新的 AST 的同步生成代码，由引擎将代码同步给渲染沙箱。渲染沙箱感知到代码变化后，会触发页面重新渲染，也就是沙箱的 HMR 过程。
    - sandpack，它是由 CodeSandbox 开源的可以在浏览器中实时运行 JavaScript 项目的的工具库
  - [关于服务端API的问题 _202404](https://github.com/NetEase/tango/issues/130)
    - 我是否可以通过定义代理来拉取业务的api接口描述，达到快否集成目的 目前，API Server端并没有开放，那只能自己编写或生成API GetWay这层的封装。
    - 可以的，目前我们内部也是这么实践的，可以直接后端的 java 代码生成对应的前端 UI 代码。
  - [大佬这个可以生成vue2或者vue3源码么？ _202308](https://github.com/NetEase/tango/issues/2)
    - 目前只适配了react的ast解析和操纵逻辑。vue后续可以考虑社区共建下，逻辑上是一样的
    - codesandbox-client 支持react 热更新， 不支持 vue 热更新
  - [能否提供一个 vitesandbox-client 类似 www 的产物  _202402](https://github.com/NetEase/tango/issues/109)
    - 我们已经废弃了该方案，所以这套沙箱方案已经不在 Tango 体系的范围内。而且该沙箱的 api 与 Tango 目前使用的 CodeSandbox 方案不是完全兼容的，所以不一定能直接使用
  - [沙箱运行起来了 但是报错 _202312](https://github.com/NetEase/tango/issues/80)
    - codesandbox-client运行的是源码，其本身是有 vue-cli 的模板的，所以理论上可以运行 Vue
    - Tango 目前只适配了 React 的场景，还未适配 Vue，后续可以考虑通过社区共建的形式支持
    - AST 未传递到沙箱中，沙箱运行的是项目的源代码。设计模式下与沙箱交互时，沙箱会触发事件传递当前操作的节点。引擎根据节点信息到 AST 树上查找节点，然后高亮节点并展示组件的配置信息。节点修改配置后映射为 AST 上的修改，AST 还原为源码，再将更新后的源码传入沙箱渲染
  - [tango面向的目标用户是哪些群体？ _202403](https://github.com/NetEase/tango/discussions/115)
    - 开源版本只包括了最核心的搭建引擎部分。你说的大部分问题都指向了物料的封装程度和易用性上，本身和搭建引擎的能力并不相关。
    - 对于低代码物料部分，因为工作量较大，目前并不在我们的开源范围。
  - [演示项目出现的问题 _202402](https://github.com/NetEase/tango/issues/108)
    - 开源版本目前只提供了一个组件库的接入示例，没有提供完整的组件库，内部的组件库节藕工作工作量比较大，我们会在合适的时机将组件库部分合并到开源代码中。
    - RN 部分涉及到 Native 的相关能力，此部分不在开源范围
  - [codesandbox-client协议是GPLv3，如何进行商业化？ ](https://github.com/NetEase/tango/issues/34)
    - Tango 主要使用的是 codesandbox 的 Sandpack 能力，而 Sandpack 部分使用的协议是 Apache 2.0
  - [本地已有沙箱，如何接入？](https://github.com/NetEase/tango/issues/29)
    - 由于 codesandbox 构建的产物的一些限制，其必须从一个域名的根路径下加载，否则一些静态资源或 web worker 会无法正常加载。而这也意味着 playground 的 origin 和 sandbox 会不一致
    - 为了解决跨域交互的问题，我们采用了经典解决方案，通过修改 `document.domain` 让设计器与沙箱落在相同的二级域名下，来实现 iframe 的跨域交互。但是 Chrome 在 115 对上述逻辑做了默认限制，因此需要追加 Origin-Agent-Cluster: ?0 这一响应头来绕过 Chrome 的限制。
  - [网易云音乐 Tango 低代码引擎正式开源！ - 掘金 _202308](https://juejin.cn/post/7273051203562749971)
    - 优点：基于 AST作为 DSL，视图和代码表现一致性，值得学习借鉴。
    - 缺点：对比 schema 直接以组件渲染，AST 多了层转换到 runtime，拖拽之后展示略有点卡，需要进一步优化转换算法
    - 后端部分不在本次开源范围
  - https://github.com/NetEase/tango-playground

- jd-drip-table /1.2kStar/MIT/202403/ts/仅前端的表格无需后端
  - https://github.com/jd-opensource/drip-table
  - https://github.com/JDFED/drip-table
  - https://drip-table.jd.com/
  - https://drip-table.jd.com/demo
  - 京东零售推出的一款用于企业级中后台的动态列表解决方案
  - 项目基于 React 和 JSON Schema，旨在通过简单配置快速生成页面动态列表来降低列表开发难度、提高工作效率。
  - 依赖antd4、viewerjs-image-viewer、react-window、sortablejs、react-quill、react-monaco、rc-*组件、moment
  - 抛弃繁重难以维护的JSX堆砌表格列，采用无需开发的低代码拖拽搭建模式。
  - 专注于可视化搭建、组件渲染分发，底层渲染逻辑由组件库处理，因此不依赖指定界面框架，可支持多种主流界面组件库。
  - [插件的应用范围](https://github.com/jd-opensource/drip-table/discussions/21)
    - antd-table旨在简化前端Table的开发，封装了HTML原生Table；而drip-table是为了解决实际业务中Table的逻辑复杂难以维护的痛点，让用户通过低代码开发Table。
    - drip-table面向的使用者是产品人员和开发人员。
  - 全家桶
    - https://jdfed.github.io/drip-form/

- https://github.com/hlerenow/chameleon /apache2/202403/ts
  - https://hlerenow.github.io/chameleon/documents/docs/tutorial/quickStart
  - https://hlerenow.github.io/chameleon/
  - Web visual programming engine. (lowcode)
  - 基于灵活的插件机制，所有功能均可二次开发
  - 不支持切换pc/mobile
  - 🔡 支持查看源码json
  - 使用 React 作为基础运行时，丰富的第三方组件供您使用
  - 通过页面编辑，最终倒出后可以得到一个页面的 schema json 协议，如何将协议重新渲染为一个可以运行的 React 页面呢?
  - 引擎内置只提供了基础的 HTML Tag 组件以及对应的物料, 如: div、p、video... 等等，可扩展使用自定义的物料
  - 组件物料包括两部分: 组件库, 组件描述, 组件库和组件描述之间通过componentName一一对应
  - [震惊和我想做的低码出奇的一致  · NetEase/tango](https://github.com/NetEase/tango/issues/3)
    - 做前端的增强开发工具，并且可以导出源码，给其他系统做集成

- apitable /2.3kStar/AGPLv3/202301/ts/java/维格表团队开源
  - https://github.com/apitable/apitable
  - https://apitable.com/
  - API-oriented low-code platform for building collaborative apps and better than all other Airtable open-source alternatives
  - 后端依赖spring-boot、mybatis、easyexcel、grpc、protobuf
  - 前端依赖antd、ahooks、redux、exceljs、konva、markdown-it、react-quill、react-dnd、slate
  - 主要功能模块
    - 基于canvas渲染的表格ui
    - 实时协作
    - 数据库本地架构：变更集/操作/动作/快照等
    - 跨表关联
    - 自动生成api
    - 表单
    - 强大的行/列权限
    - Shareable and embeddable page
  - Realtime collaboration allows multiple users to edit together in real time, or simultaneously with the Operational Transformation (OT) Algorithm.
  - super-fast database-spreadsheet interface in `<canvas>` Rendering Engine.
  - Database native architecture: Changeset / Operation / Action / Snapshot and so on.
  - Full-stack API access, from Data to Metadata.
  - One-direction / Bi-direction Table Link and Infinite Cross Links
  - 7 View Types: Grid View (Datasheet) / Gallery View / Mindmap View / Kanban View / Full-Feature Gantt View / Calendar View
  - Embed-friendly: Share your datasheet table or folder. Embed them by copying and pasting HTML scripts.
  - Community-friendly programming languages and framework, TypeScript (NextJS + NestJS) and Java (Spring Boot)
  - APITable will provides a Datasheet Query Language (DQL) to query your database-spreadsheet contents.
  - 落地页glassmorphism风格
  - [apitable 和 vika.cn 是有啥关系吗？怎么两个产品看起来一模一样？](https://discord.com/channels/1016320471010115666/1062551587718959224/1062555700246618193)
    - APITable is the open-source and community version of Vika.
    - Vika is a SaaS distribution for China mainland built on APITable open-source core

- nocobase /3.7kStar/apache2(core)🌹 > AGPL/202404/ts
  - https://github.com/nocobase/nocobase
  - https://www.nocobase.com/
  - [features](https://docs-cn.nocobase.com/welcome/introduction/features)
  - 易扩展的开源无代码开发平台
  - NocoBase is a scalability-first, open-source no-code/low-code development platform.
  - server依赖koa、sequelize.v6
  - client依赖antd、g2plot、ahooks、dnd-kit、formily、marked、react-iframe、react-quill、react-router5
  - 提供了tree结构的4种存储方式，邻接表、闭包表、路径枚举、嵌套集
  - 主要功能模块
    - 微内核，灵活易扩展，具备健全的插件体系、内置插件市场
    - fields: 使用文本、数字、附件等数十种字段类型
    - blocks: 使用表格、表单、看板、日历、详情等区块
    - 操作: 支持筛选、导出、添加、删除、修改、查看等操作对数据进行处理，可以扩展更多类型
    - 权限: 基于角色控制用户的系统配置权限、数据操作权限和菜单访问权限
    - Workflow: 重复性的任务由自动化代替
  - 采用数据结构与使用界面分离的设计思路
    - 可以为数据表创建任意数量、任意形态的区块（数据视图），
    - 每个区块里可以定义不同的样式、文案、操作
  - you can configure the user interface directly with WYSIWYG operations.
  - Everything is a plugin, all new features can be implemented by developing and installing plugins
  - [change license of plugins-AGPLv3_20230111, v0.8.1 > v0.9.0](https://github.com/nocobase/nocobase/pull/1350)
  - [change license to AGPLv3 or commercial _2024-03-30](https://github.com/nocobase/nocobase/commit/e2763b332286affb7cfd9c6a9fb90d656226e3fb)

- fast-crud /512Star/MIT/202402/ts/vue/仅前端
  - https://github.com/fast-crud/fast-crud
  - http://fast-crud.docmirror.cn/
  - 面向配置的crud开发框架，快速开发crud功能，可作为低代码平台的基础框架
  - 目标是实现一个fs-crud组件，帮助快速开发crud功能，admin脚手架并不是本项目的重点
  - 可以直接使用示例中的fs-admin，特点是简单
  - 也可以采用其他的admin开源项目，然后集成fast-crud
  - 基于目前市面上开源的高星admin项目fork，集成fast-crud，Antdv 3x 、Element-Plus 、NaiveUI 三选一
    - https://github.com/fast-crud/fs-admin-antdv /vue

- directus /25kStar/GPLv3 > BSL/202403/ts/vue
  - https://github.com/directus/directus
  - https://directus.io/
  - https://docs.directus.io/
  - Directus is an instant REST+GraphQL API and intuitive no-code data collaboration app for any SQL database
  - 后端依赖express、knex、async、commander、graphql、ioredis、keyv、marked、micromustache、eventemitter2、node-cron、rate-limiter-flexible、sharp、vm2、ws
  - 前端依赖vue3、vueuse、vuedraggable、editorjs、tinymce.v6、tinymce-vue.v5、fullcalendar、p-queue、apexcharts、codemirror.v5、cropperjs(img)、maplibre-gl、marked、mitt
  - 涉及graphql的代码不多，可以尝试移除
  - 在admin添加新的data-model时，数据库会创建对应的表
  - [Change license to BSL-1.1_20230427](https://github.com/directus/directus/pull/18330)

- webstudio-designer /172Star/MIT>AGPLv3/202212/ts
  - https://github.com/webstudio-is/webstudio
  - https://github.com/webstudio-is/webstudio-designer
  - https://webstudio.is/
  - Webstudio Designer is a NoCode Visual Tool inspired by Webflow
  - an open source visual development tool
  - 依赖lexical-editor、radix-ui、stitches、remix-auth、downshift
  - simplify collaboration between designers and developers on any type of site or web app.
  - With Webstudio you can use any headless CMS or e-commerce back-end.
  - Webstudio features a UI to create API bindings. You can add a GraphQL binding to any component and choose which endpoint and data properties to bind to each component property. 
  - block块级元素不支持拖拽
  - [Change license from MIT to AGPL V3_202307](https://github.com/webstudio-is/webstudio/pull/1980)
  - [Apps Marketplace](https://github.com/webstudio-is/webstudio/issues/2648)
    - Similar thing to figma apps, they are effectively standalone web apps loaded via iframe, hosted by the 3rd-party provider but with access to project data and api to change it

- https://github.com/dotenx/dotenx /apache2/202402/ts/go
  - No-code and Low-code all-in-one platform to build landing pages, websites, web applications, APIs, automations. 
  - An alternative for Wix, Webflow

- https://github.com/sparrow-js/sparrow /MIT/202107/ts/vue/ast/inactive
  - https://sparrow-js.github.io/sparrow-vue-site/
  - 场景化低代码（LowCode）搭建工作台，实时输出源代码
  - 基于vue、element-ui组件库中后台项目的实践，实时输出源代码
  - 易于扩展，通过AST读取组件源代码，进行组合
  - [理论上能否支持 React 组件 & React 代码模式？ _202110](https://github.com/sparrow-js/sparrow/issues/38)
    - 可以，理论上啥框架都一样
    - 我看生成的代码是有 lifecycle 之类的控制的，但这样生成的代码，可能对于开发来说维护性不一定合适？ 需要依赖最终生产出来代码的这种模式
    - 这种就需要提供扩展能力了，需要自定义写插件，这个项目还有一些别的问题比如目前生成的代码不能二次开发，正在开发一个在“不破坏源代码”的基础上实现可视化的开发能力的工具
    - 目前只有组件部分写了自定义的能力，更多的扩展能力没有写，代码部分是解析成ast的，理论上开放ast就可以自己往里加自定义的

- https://github.com/codebdy/rxdrag /MIT/202401/ts/antd
  - https://rxdrag.vercel.app/
  - https://github.com/codebdy/minions-go /golang/逻辑编排go引擎
  - 可视化编辑， 带逻辑引擎的低代码前端
  - editor-core依赖redux-toolkit、lodash
  - react-runner依赖react-router.v6、@monaco-editor/react、styled-components
  - 侧边栏模块: 页面、组件资源、大纲、历史记录
  - [实战，一个高扩展、可视化低代码前端，详实、完整 - 掘金 _202303](https://juejin.cn/post/7205361008272326716)
    - RxEditor是一款开源企业级可视化低代码前端，目标是可以编辑所有 HTML 基础的组件。比如支持 React、VUE、小程序等，目前仅实现了 React 版
    - 编辑器（RxEditor）要维护一个树形模型，这个模型描述的是组件的隶属关系，以及 props。同时还能跟 dom 树交互，通过各种 dom 事件，操作组件模型树。
    - 编辑器操作的是JSON格式的组件树，设计时，设计引擎根据这个组件树渲染画布。这个组件树是设计器的数据模型，通常会被叫做 Schema。
    - 项目中的前端组件，要在两个地方渲染，一是设计引擎的画布，另一处是预览页面。这两处使用的是不同渲染引擎
    - 设计形态的组件跟预览形态的组件，对应的是同一份schema，只是在渲染时，使用不同的组件实现
    - Material，物料的定义。一个Schema，只是用来描述一个组件，这个组件相关的配置，比如多语言信息、在工具箱中的图标、编辑规则
    - 软件架构,软件被划分为两个比较独立的部分：
      - 设计器，用于设计页面，消费的是设计形态的组件。生成页面Schema。
      - 运行时，把设计器生成的页面Schema，渲染为正常运行的页面，消费的是预览形态的组件。 
      - core包是整个设计器的基础，包含了 Redux 状态树、页面互动逻辑，编辑器的各种状态等。
      - 运行时包含三个包：ComponentRender、fieldy跟minions，前者依赖后两者
  - [挑战零代码：可视化逻辑编排 - 掘金 _202307](https://juejin.cn/post/7257814347463671863)
    - 逻辑编排的目的，是用最少代码来实现软件的业务逻辑，包括前端业务逻辑跟后端业务逻辑
    - 本文前端代码基于typescript、react技术栈，后端基于golang。
    - 涵盖内容：数据流驱动的逻辑编排原理，业务编排编辑器的实现，页面控件联动，前端业务逻辑与UI层的分离，子编排的复用、自定义循环等嵌入式子编排的处理、事务处理等
    - 逻辑编排编辑器，顾名思义，可视化编辑器，根据物料提供的元件信息，编辑生成JSON格式的“编排描述数据”。
- https://github.com/codebdy/dingflow /202402/ts
  - https://dingflow.vercel.app/
  - React 仿钉钉审批流、工作流
  - 依赖@reduxjs/toolkit、antd5
  - [css-in-js、React Redux经典案例：仿钉钉审批流 - 掘金 _202308](https://juejin.cn/post/7263858443329191996)
    - 只包含审批流设计部分，不包含表单的设计，表单的设计请参考作者另一个可视化前端项目rxdrag
    - workflow-editor 是编辑器核心，未来要作为独立的npm package来发布；example 是演示如何使用workflow-editor来把审批流集成入自己的项目。
    - 画布区是通过嵌套的`div`实现的，连线、箭头通过css的border、伪类before跟after实现
    - UI虽然是树形结构，但是项目内部的数据结构可以是树形，也可以是扁平的。最后选择了树形数据结构,因为后端是树形结构，跟div的结构一致
    - redux基于immutable的方式，可以保留状态快照，易于回溯，很容易就完成撤销、重做功能
    - EditorEngine。编辑器的绝大多数业务逻辑，都在这部分实现，主要功能就是操作Redux store
    - 物料就是节点的定义，包括节点的图标、颜色、缺省配置等信息。把这些信息独立出来的好处，是让代码更容易扩展，方便后期添加新的节点类型。作者自己开源低代码前端RxDrag，也用了类似的设计方式
    - workflow-editor对外提供两个组件：FlowEditorScope，FlowEditorCanvas。前者负责接收各种配置资源，比如物料、物料ui、多语言资源。FlowEditorCanvas是画布区

- https://github.com/deco-cx/deco /apache2/202404/ts
  - https://deno.land/x/deco
  - Open-Source web editor based on Preact, Tailwind and TypeScript. 
  - It's focused on reusability and composability of UI components (Sections) and API integrations (Loaders and Actions).
  - 依赖deno
  - Deco combines the best of visual page editing (like Webflow) and the ability for app composition at the admin level (like Wordpress)
  - Sections, Loaders and Actions can be packaged and installed with one click as Apps.
  - Deco Blocks are interoperable: one's output can be visually configured as another's input in the visual editor, based on matching TypeScript types.

- https://github.com/opentiny/tiny-engine /MIT/202404/js/vue
  - https://opentiny.design/tiny-engine
  - 华为低代码引擎，基于这个引擎可以构建或者开发出不同领域的低代码平台
  - 跨端跨框架前端组件
  - 直接生成可部署的源码，运行时无需引擎支撑
  - https://github.com/opentiny/tiny-engine/tree/develop/mockServer
    - mock服务，koa + nedb
  - [谁在使用 TinyEngine 低代码引擎](https://github.com/opentiny/tiny-engine/issues/334)
  - [Q&A：常见问题答疑 ](https://github.com/opentiny/tiny-engine/issues/78)

- https://github.com/mybricks/designer-spa /202308/demos/json
  - https://github.com/mybricks/designer-spa-demo /isc
  - https://mybricks.world/
  - mybricks-SPA 是mybricks引擎家族面向页面应用的企业级低代码设计引擎。
  - MyBricks 开源了平台、渲染引擎、插件、编辑库、组件库等源代码。
  - [生成源代码 | MyBricks 文档中心](https://docs.mybricks.world/docs/publish-integration/to-sourcecode/)
    - 搭建产物目前是一份 JSON 作为页面标准协议，所需要做的就是基于这份协议进行解析生成所需要的源代码
    - 👉🏻 生成后产物为一份普通的 React 代码工程，可以基于此工程之上再进行业务开发
    - 代码生成器：理论上可以由页面协议解析生成任意技术栈源代码
    - MyBricks通过搭建过程生成一份 JSON 描述，这份描述详细地反映了页面内的组件以及它们之间的交互。

- https://github.com/page-pipepline/pipeline-editor /201910/js/inactive
  - 页面可视化搭建框架的 web 编辑器
  - 实现了编辑器和页面前端框架的分离, 可以支持不同的前端框架.
  - 目前已经支持 Vue, React, 和 Omi, 理论上可以支持任意前端框架.

- ToolJet /17.1kStar/AGPLv3/202403/前端js+后端nestjs
  - https://github.com/ToolJet/ToolJet
  - https://tooljet.com/
  - low-code framework to build and deploy internal tools
  - 后端依赖nestjs、typeorm、ws、handlebars
  - 前端依赖react-plotly.js、rxjs、yjs
  - 功能模块设计
    - 数据表设计与录入
    - 仪表板
    - 成员与权限
  - ToolJet's drag and drop frontend builder allows you to build complicated responsive frontends within minutes
  - [Add realtime collaboration _202203](https://github.com/ToolJet/ToolJet/issues/2516)
    - Use yjs as the barebone library for adding the collaborative feature
# lowcode
- lowdefy /2.1kStar/apache2 > BSL/202401/js/json/yaml
  - https://github.com/lowdefy/lowdefy
  - low-code framework that lets you build web apps with YAML or JSON configuration files
  - 依赖knex
  - It is great for building admin panels, BI dashboards, workflows, and CRUD apps.
  - Advantages of writing internal tools in YAML or JSON
  - [chore: Initialise @lowdefy/server-enterprise package _202310](https://github.com/lowdefy/lowdefy/commit/a0a30d99685a7df211b93eb576d6953a35cc372a)
    - packages/servers/server-enterprise

- sunmao-ui /apache2/202301/ts
  - https://github.com/smartxworks/sunmao-ui
  - Sunmao(榫卯)是一个前端低代码框架。
  - Sunmao 内置了低代码工具的 GUI 编辑器

- cube /89Star/NALic/202009/ts/inactive
  - https://github.com/fantasticit/cube
  - https://blog.wipi.tech/odin/editor
  - 中后台页面搭建低代码平台
    - 通过 JSON 配置描述页面信息
    - 通过配置初始化 Store
    - 通过配置渲染页面
    - 通过交互组件修改 Store 数据，重新渲染页面
  - 依赖antd4、mobx5、codemirror5、showdown、nextjs

- https://github.com/alibaba/formily 
  - /MIT/2.9kStar/202009
  - 表单状态核心管理包(不依赖任何第三方UI框架，但依赖immer、cool-path)
    - 管理 Form 状态、Field 状态、Validator 状态、Form/Field/Validator 之间的依赖关系
    - 借助首创Observable Graph，可记录任意时刻的全量状态，也可将状态回滚至任意时刻
  - https://github.com/alibaba/formily-editor

- appsmith /340Star/apache2/202009/ts/java
  - https://github.com/appsmithorg/appsmith
  - open source alternative to Power Apps, Salesforce Lightning
  - A low code way to build dashboards, workflows, forms, and any internal tool.
  - 服务端依赖spring-boot、mongodb

- merico-dev-table /15Star/apache2/202401/ts
  - https://github.com/merico-dev/table
  - Dev Table offers a most flexible and powerful low-code data workflow loved by developers.
  - Build your own data presentation using SQL and multiple data sources including big data.

- https://github.com/Dashibase/dashibase /202207/ts/vue/inactive
  - https://dashibase.com/
  - Build your admin panels with a Notion-like UI
  - Super simple user dashboards for Supabase users.

- saltcorn /1kStar/MIT/202301/js/ts
  - https://github.com/saltcorn/saltcorn
  - Saltcorn is an extensible open source no-code database application builder.
  - This repository contains the core codebase, including the code necessary to self-host an instance and to host a multitenant instance.
  - 后端依赖express、passport、pg、socket.io
  - 前端采用script标签导入，依赖ckeditor4、codemirror5、jquery、jsgrid、tabulator、bootstrap4

- illa-builder /10.5kStar/apache2/202403/ts/go
  - https://github.com/illacloud/illa-builder
  - https://www.illacloud.com/
  - https://fast-try.illacloud.com/
  - 一个强大的开源低代码平台
  - 本地部署： 支持Docker和k8s 
  - 实时协作： 我们可以一起实时创建内容
  - https://github.com/illacloud/builder-backend /go

- https://github.com/jet-admin/jet-bridge /python
  - Jet Admin is a SaaS service that automatically generates extendable back office for your application
  - Jet Bridge is a standalone app which generates REST API thought which your SQL database is connected to Jet Admin.

- https://github.com/openblocks-dev/openblocks /AGPLv3/202303/ts/java/inactive
  - The Open Source Retool Alternative
  - An all-in-one IDE to create internal or customer-facing apps.
  - A place to create, build and share building blocks of web applications.
- https://github.com/lowcoder-org/lowcoder /AGPLv3/202401/java/ts
  - Lowcoder continues from the abandoned Openblocks project
  - The Open Source Retool, Tooljet and Appsmith Alternative

- https://github.com/basetool-io/basetool /apache2/202202/ts/archived
  - https://basetool.io/
  - Open-source internal tool framework. 
  - Empower your team and collaborators to view and manage the data you already own in a nice easy-to-use protected tool.
  - 依赖chakra-ui.v1、codemirror6、@reduxjs/toolkit、prisma、next-auth
  - Basetool is organized in data sources that belong to organizations. When you create your account an organization will be created for you.

- https://github.com/jet-admin/jet-bridge /MIT/202402/python
  - https://www.jetadmin.io/
  - No-code Business App builder
  - Jet Admin is a SaaS service that automatically generates extendable back office for your application.
  - Jet Bridge is a standalone app which generates REST API through which your SQL database is connected to Jet Admin.
  - This is a complete remake of our popular Django Jet admin interface.
  - https://github.com/geex-arts/django-jet /201810/python/inactive

- https://github.com/polterguy/magic
  - a Low-Code CRUD generator with machine learning and artificial intelligence allowing you to generate most of your code 100% automatically.
  - In addition it is a complete open source cloud platform and IDE

- https://github.com/umijs/sula /202109/ts/inactive
  - Pluggable enterprise-level configurable framework based on antd and umi.
  - sula-builder：可视化搭建平台
  - sula-cooker：在线配置化工具

- https://github.com/elis/djit.su /202102/js/inactive
  - https://djit.su/
  - 依赖react、redux、styled-components、razzle、d3-require、@mdx-js/runtime、@editorjs、antd.v4、ahooks
  - Djitsu is an editor, application, and an execution platform all rolled into one

- https://github.com/icodebetter/icodebetter /js/inactive
  - An opinionated low code platform that helps you code business applications

- https://github.com/crossjs/cofe /ts/inactive
  - No-Code System
  - core依赖unist-builder

- https://github.com/kontenbase/kontenbase /202209/ts/inactive
  - https://kontenbase.com/
  - no code backend API platform/Backend as a Service (BaaS)
  - 依赖 centrifuge(类似 RabbitMQ)

- https://github.com/ngx-lazy-admin/lazy-admin /angular
  - http://lazy-admin-pro.com/
  - Low code production-ready solution for admin business components packages
  - Built on the design principles developed by Ant Design And Formly

- https://github.com/steedos/steedos-platform /MIT/202403/ts/meteor
  - https://www.steedos.org/
  - 炎魔方低代码PaaS平台是一款基于 Salesforce Platform 的开源替代方案
  - 华炎魔方前端使用 React 开发表单、列表视图控件，并基于 Meteor 实现完整界面。
  - 华炎魔方支持以插件的方式与第三方开源项目无缝融合，包括统一身份认证、数据分析、微应用、流程自动化，为客户构建一体化的企业PaaS平台。

- https://github.com/alibaba/designable /MIT/202204/ts/inactive
  - https://designable.netlify.app/
  - If you are worrying about something builder, Such as form builder/table builder/chart builder/app builder etc. Designable is your perfect choice.
  - [Designable2.0详细规划&任务分解](https://github.com/alibaba/designable/discussions/240)
    - 目前暂停维护中，未来会重启，感谢大家的支持

- https://github.com/AnsGoo/openDataV /ts/vue
  - http://datav.byteportrait.com/
  - OpenDataV 是一个纯前端的拖拽式、可视化、低代码数据可视化开发平台，同时支持用户方便的开发自己的组件并接入平台
  - 支持用户操作记录的恢复、撤销功能
  - 本项目采用Vue3 + vite + TypeScript开发，界面库使用NaiveUI，使用面向对象方式封装了路由、请求、存储，组件采用自动扫描注册、异步加载，提升渲染速度；
  - 使用IndexDB存储快照数据，减少快照数据内存占用，加快访问速度；
  - 组件独立依赖，解耦了组件和基础框架的依赖库，方便后续独立开发组件。
  - https://gitee.com/small_bud_star/open-data-backend
    - 低代码可拖拽前端库OpenDataV的Python后端实现

- https://github.com/Atri-Labs/atrilabs-engine /GPLv3/ts
  - https://atrilabs.com/
  - Open-source no-code & code web app builder
  - a suite of productivity tools such as visual editor, asset management tools, etc
  - developers do not need to write and document REST APIs. Instead, they rely upon the object model which acts as a single source of truth.
# workflow-automation-tasks-pipeline
- tips
  - 考虑跨平台/系统的task兼容性、分享，主流的airflow/ifttt
  - https://github.com/pditommaso/awesome-pipeline

- https://github.com/meirwah/awesome-workflow-engines /md
  - A curated list of awesome open source workflow engines
  - saas, bpm, embedded

- https://github.com/node-red/node-red /apache2/js
  - Low-code programming for event-driven applications

- https://github.com/triggerdotdev/trigger.dev
  - https://trigger.dev/
  - The developer-first open source Zapier alternative.
  - Trigger.dev is an open source platform that makes it easy for developers to create event-driven background tasks directly in their code. 
  - open-source platform to create long-running jobs directly in your Next.js project, with features like API integrations, webhooks, scheduling and delays.
  - 后端依赖remix、prisma
  - 前端依赖headless/react、codemirror6、json-query、keyv、pulsar

- https://github.com/automatisch/automatisch /3.8kStar/AGPLv3/202403/js/graphql
  - open source Zapier alternative. 
  - Build workflow automation without spending time and money.
  - 前端依赖mui5、apollo、graphql、slate
  - 后端依赖express、knex、pg、graphql

- https://github.com/elyra-ai/pipeline-editor
  - A react component for editing pipeline files. 
  - Used across all Elyra applications and browser extensions.
  - Elyra is a set of AI-centric extensions to JupyterLab Notebooks.
  - Currently, pipelines can be executed locally in JupyterLab, on Kubeflow Pipelines, or with Apache Airflow.

- https://github.com/alibaba/dawn
  - Lightweight task management and build tool.
  - 通过 pipeline 和 middleware 将开发过程抽象为相对固定的阶段和有限的操作，简化并统一了开发人员的日常构建与开发相关的工作。

- budibase /19.5kStar/GPLv3/202312/ts/svelte
  - https://github.com/Budibase/budibase
  - https://budibase.com/
  - Low code platform for creating internal tools, workflows, and admin panels in minutes.
  - 后端依赖koa、knex、pouchdb
  - 前端依赖svelte
  - unlike other platforms, with Budibase you can start from scratch and create business apps with no datasources
  - Budibase integrates with a number of popular tools allowing you to build apps
  - the Budibase API enables Budibase as a backend
  - At Budibase we use CouchDB as the underlying technology of our internal Budibase DB.

- https://github.com/krn0x2/microflow
  - Microservice orchestration inspired by AWS Step functions and Apache Airflow

- https://github.com/dataplane-app/dataplane /BSL/202310/go/js/inactive
  - https://dataplane.app/
  - an Airflow inspired data platform with additional data mesh capability to automate, schedule and design data pipelines and workflows.
  - Written in Golang and compiled to machine code to achieve extreme performance with a low memory and CPU footprint.
  - Built in Python code editor.
  - Drag drop data pipeline builder.

- https://github.com/jitsucom/jitsu /MIT/202401/go/ts
  - a tool for collecting event data from your websites, apps and stream them to your data warehouse or other services. 
  - It is a self-hosted, open-source alternative to Segment.
  - Jitsu is based on Bulker(golang), an open-source data warehouse ingestion engine. Bulker can be used as a standalone tool

- https://github.com/cptn-io/el-cptn /java
  - an open source platform that helps develop and deploy integrations and data pipelines quickly and easily.
  - 发现个比 n8n 更适合开发者使用的 workflow 平台 https://cptn.io。核心概念非常简单清晰：
    - Source: 接收数据的 HTTP entrypoint
    - Destination: 存放/写入数据的目的地，对接各种数据库和线上存储
    - Transformation: 转化数据的 code block
    - Pipeline: 将以上组合起来的工作流

- https://github.com/activepieces/activepieces /MIT+EE/202503/ts
  - https://www.activepieces.com/
  - Your friendliest open source all-in-one automation tool 
  - Workflow automation tool 100+ integration / Enterprise automation tool / Zapier Alternative

- https://github.com/riccardoperra/pipelineui /MIT/202411/ts
  - https://pipelineui.dev/
  - Open source editor for visualizing, creating and managing GitHub Actions workflows. 
  - Built with SolidStart and Appwrite

## ai-workflow

# json-builder
- https://github.com/redgeoff/mson /apache2/202401/js
  - The MSON compiler allows you to generate apps from JSON
  - MSON supports validation, inheritance, composition, pub/sub, access control, templating and various other features.
  - MSON is particularly useful in software that generates other software, e.g. a form builder. This is because MSON is just JSON, so it is easy to consume, modify and store.
  - MSON is framework agnostic, but the default `mson-react` rendering layer uses React and Material-UI to generate a UI. 
  - The rendering layer is pluggable and can be written to support any framework and UI library.
  - The MSON library can also be used without any UI dependecies, which makes it great for things like data validation in both the front and back ends.
  - https://github.com/redgeoff/mson-react
# app-builder
- https://github.com/AmruthPillai/Reactive-Resume /28.3kStar/MIT/202501/ts
  - https://rxresu.me/
  - A one-of-a-kind resume builder that keeps your privacy in mind. 
  - Completely secure, customizable, portable, open-source and free forever. 
  - A free and open-source resume builder that simplifies the process of creating, updating, and sharing your resume.
  - With zero user tracking or advertising, your privacy is a top priority. 
  - The platform is extremely user-friendly and can be self-hosted in less than 30 seconds 
  - Bring your own OpenAI API key and unlock features 
  - React (Vite), for the frontend
  - NestJS, for the backend
  - Postgres (primary database)
  - Prisma ORM
  - Minio (for object storage: to store avatars, resume PDFs and previews)
  - Browserless (for headless chrome, to print PDFs and generate previews)
  - GitHub/Google OAuth (for quickly authenticating users)
  - LinguiJS and Crowdin (for translation management and localization)

- https://github.com/JOYCEQL/magic-resume /apache2/202502/ts
  - https://magicv.art/
  - 魔方简历是一款基于现代技术栈构建的免费在线简历编辑器，提供清爽的 UI 和流畅的用户体验。
  - Built with Next.js and Framer Motion, it supports real-time preview and custom themes.
  - 集成 DeepSeekV3 和 豆包，提供 AI 驱动的简历润色和诊断功能。
# more-lowcode
- corteza /go/vue
  - https://github.com/cortezaproject/corteza
  - https://github.com/cortezaproject/corteza-webapp-one
  - https://cortezaproject.org/
  - fully standardized low-code app development, business process, integration and data harmonization platform.

- https://github.com/centerofci/mathesar /python/svelte
  - https://wiki.mathesar.org/en/home
  - provides a spreadsheet-like interface to a PostgreSQL database.
  - directly operates on PostgreSQL databases
  - You can use to build data models, enter data, and even build reports
  - [Show HN: Visual DB – Airtable alternative for your own database | Hacker News _202308](https://news.ycombinator.com/item?id=37223019)
