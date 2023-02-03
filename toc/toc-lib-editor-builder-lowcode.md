---
title: toc-lib-editor-builder-lowcode
tags: [builder, lowcode, toc]
created: 2020-12-13T15:59:43.778Z
modified: 2020-12-28T12:24:09.275Z
---

# toc-lib-editor-builder-lowcode

# guide

- ali-LowCodeEngine目前仅支持生成React的前端代码
  - 制作成本固然低了，造出来的代码维护成本太高了
  - 这种东西，不会编程的人对他来说太复杂了，会编程的人来说太繁琐了。

- [什么是比较好的低代码产品_Tw93](https://zhuanlan.zhihu.com/p/596474809)
  - platform, baas, cms建站, airtable-like, workflow
  - 流程自动化

- workflow类低代码
  - 简单场景类似表单，支持根据不同评分显示不同内容，如投诉/不足

- lowcode vs builder
  - 建站侧重于自动生成并发布页面，而不是编辑器
# popular
- ref
  - https://github.com/taowen/awesome-lowcode

- payload /9.1kStar/MIT/202301/ts/slate
  - https://github.com/payloadcms/payload
  - https://payloadcms.com/
  - https://demo.payloadcms.com/admin
  - Headless CMS and Application Framework built with TypeScript, Node.js, React and MongoDB
  - cms只提供管理界面来拖拽生成数据对应的api，不提供预览内容的前端
  - 不是典型的block-editor，富文本作为字段block
  - 后端依赖express、mongoose、passport
  - 前端依赖dnd-kit、monaco-editor、slate、react-beautiful-dnd、react-router5、webpack5、swc
  - 支持多个versions，Automatically maintain a history of changes to any given collection document
  - Block-based Layout Builder
  - Extensible SlateJS rich text editor
  - A Mongo database to store your data
  - retrieve, and manipulate data of any shape via full REST and GraphQL APIs
  - File storage and access control
  - Payload dynamically generates a React admin panel to manage your data. 
    - Admin panel is built with Webpack, code-split, highly performant (even with 100+ fields), and written fully in TypeScript.
  - [Roadmap Discussions](https://github.com/payloadcms/payload/discussions/categories/roadmap)

- baidu-amis /12.9kStar//apache2/202301/ts/编辑器未开源
  - https://github.com/baidu/amis
  - 依赖mobx、react、jquery、sortablejs、tinymce
  - 前端低代码框架，通过JSON配置就能生成各种后台页面，不适合大量交互、定制ui
  - https://github.com/aisuda/amis-editor-demo
    - http://aisuda.github.io/amis-editor-demo
    - amis 可视化编辑器示例
    - 目前 amis-editor 未开源，但可以免费使用（包括商用）。
 - [请问@fex/amis-editor 有开源计划吗？](https://github.com/aisuda/amis-editor-demo/issues/12)
    - 目前amis-editor已将内置的plugin源码开放出来了

- alibaba-lowcode-engine /8.9kStar/MIT/202212/ts
  - https://github.com/alibaba/lowcode-engine
  - 一套面向扩展设计的企业级低代码技术体系
  - 依赖react、mobx、power-di
  - 引擎完整实现了 低代码引擎 搭建协议、物料协议、资产包协议
  - LowCodeEngine目前仅支持生成React的前端代码
    - 制作成本固然低了，造出来的代码维护成本太高了
    - 这种东西，不会编程的人对他来说太复杂了，会编程的人来说太繁琐了。
  - [阿里低代码引擎简介](https://lowcode-engine.cn/site/docs/guide/quickStart/intro)

- jd-drip-table /677Star/MIT/202301/ts/仅表格
  - https://github.com/JDFED/drip-table
  - https://drip-table.jd.com/
  - 依赖viewerjs-image-viewer, rc-*组件，react-window、moment
  - 京东零售推出的一款用于企业级中后台的动态列表解决方案
  - 抛弃繁重难以维护的JSX堆砌表格列，采用无需开发的低代码拖拽搭建模式。
  - 专注于可视化搭建、组件渲染分发，底层渲染逻辑由组件库处理，因此不依赖指定界面框架，可支持多种主流界面组件库。
  - 全家桶
    - https://jdfed.github.io/drip-form/

- apitable /2.3kStar/AGPLv3/202301/ts/java/维格表团队开源
  - https://github.com/apitable/apitable
  - https://apitable.com/
  - API-oriented low-code platform for building collaborative apps and better than all other Airtable open-source alternatives
  - 后端依赖spring-boot、mybatis、easyexcel、grpc、protobuf
  - 前端依赖antd、ahooks、redux、exceljs、konva、markdown-it、react-quill、react-dnd、slate
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

- nocobase /3.7kStar/apache2/202212/ts/国内
  - https://github.com/nocobase/nocobase
  - https://www.nocobase.com/
  - 易扩展的开源无代码开发平台。
  - NocoBase is a scalability-first, open-source no-code/low-code development platform.
  - server依赖koa、sequelize.v6
  - client依赖antd、g2plot、ahooks、dnd-kit、formily、marked、react-iframe、react-quill、react-router5
  - 采用数据结构与使用界面分离的设计思路
    - 可以为数据表创建任意数量、任意形态的区块（数据视图），
    - 每个区块里可以定义不同的样式、文案、操作
  - you can configure the user interface directly with WYSIWYG operations.
  - Everything is a plugin, all new features can be implemented by developing and installing plugins

- webstudio-designer /172Star/MIT/202212/ts
  - https://github.com/webstudio-is/webstudio-designer
  - https://webstudio.is/
  - Webstudio Designer is a NoCode Visual Tool inspired by Webflow
  - an open source visual development tool
  - simplify collaboration between designers and developers on any type of site or web app.
  - With Webstudio you can use any headless CMS or e-commerce back-end. 
  - Webstudio features a UI to create API bindings. You can add a GraphQL binding to any component and choose which endpoint and data properties to bind to each component property. 
  - block块级元素不支持拖拽
  - 依赖lexical-editor、radix-ui、stitches、remix-auth、downshift

- https://github.com/page-pipepline/pipeline-editor /201910/js
  - 页面可视化搭建框架的 web 编辑器
  - 实现了编辑器和页面前端框架的分离, 可以支持不同的前端框架.
  - 目前已经支持 Vue, React, 和 Omi, 理论上可以支持任意前端框架.

- ToolJet /17.1kStar/AGPLv3/202301/前端js+后端ts
  - https://github.com/ToolJet/ToolJet
  - https://tooljet.com/
  - low-code framework to build and deploy internal tools
  - ToolJet's drag and drop frontend builder allows you to build complicated responsive frontends within minutes
# lowcode
- lowdefy /2.1kStar/apache2/202301/js/json/yaml
  - https://github.com/lowdefy/lowdefy
  - low-code framework that lets you build web apps with YAML or JSON configuration files
  - It is great for building admin panels, BI dashboards, workflows, and CRUD apps.
  - Advantages of writing internal tools in YAML or JSON

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

- appsmith /340Star/Apache2/202009/ts/java
  - https://github.com/appsmithorg/appsmith
  - open source alternative to Power Apps, Salesforce Lightning
  - A low code way to build dashboards, workflows, forms, and any internal tool.

- https://github.com/merico-dev/table /apache2/202301/ts
  - Build your own data presentation using SQL and multiple data sources including big data. 
  - It is a natural integration with Dev Lake and Dev Analysis.

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

- illa-builder /2.7kStar/apache2/202212/ts/go
  - https://github.com/illacloud/illa-builder
  - https://www.illacloud.com/
  - https://fast-try.illacloud.com/
  - ILLA is a robust open source low-code platform for developers to build internal tools. 
  - 实时协作： 我们可以一起实时创建内容
  - https://github.com/illacloud/builder-backend

- https://github.com/jet-admin/jet-bridge /python
  - Jet Admin is a SaaS service that automatically generates extendable back office for your application
  - Jet Bridge is a standalone app which generates REST API thought which your SQL database is connected to Jet Admin.

- https://github.com/openblocks-dev/openblocks /ts/java
  - The Open Source Retool Alternative
  - An all-in-one IDE to create internal or customer-facing apps.
  - A place to create, build and share building blocks of web applications.

- https://github.com/node-red/node-red /js
  - Low-code programming for event-driven applications

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

- https://github.com/sparrow-js/sparrow /vue/inactive
  - 场景化低代码（LowCode）搭建工作台

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

- https://github.com/steedos/steedos-platform
  - 华炎魔方是Salesforce低代码平台的开源替代方案
  - 华炎魔方前端使用 React 开发表单、列表视图控件，并基于 Meteor 实现完整界面。
# workflow-automation-tasks-pipeline
- tips
  - 考虑跨平台/系统的task兼容性、分享，主流的airflow/ifttt

- n8n /28kStar/FairCode/202301/ts/vue/依赖少
  - https://github.com/n8n-io/
  - https://n8n.io/
  - an extendable workflow automation tool
  - Easily automate tasks across different services.
  - 前端依赖vue2、jsplumb、codemirror6、jquery、monaco-editor、prismjs
  - 提供了自动化任务模版中心 Workflow templates，类似可复用的工具函数
    - Convert JSON to an Excel file
    - Creating an API endpoint
    - 内置了600+个任务

- https://github.com/automatisch/automatisch /ts/graphql
  - open source Zapier alternative. 
  - Build workflow automation without spending time and money.

- https://github.com/elyra-ai/pipeline-editor
  - A react component for editing pipeline files. 
  - Used across all Elyra applications and browser extensions.
  - Elyra is a set of AI-centric extensions to JupyterLab Notebooks.
  - Currently, pipelines can be executed locally in JupyterLab, on Kubeflow Pipelines, or with Apache Airflow.

- https://github.com/alibaba/dawn
  - Lightweight task management and build tool.
  - 通过 pipeline 和 middleware 将开发过程抽象为相对固定的阶段和有限的操作，简化并统一了开发人员的日常构建与开发相关的工作。

- https://github.com/Budibase/budibase /GPLv3/svelte
  - Low code platform for creating internal tools, workflows, and admin panels in minutes. 
  - 前端依赖svelte
  - unlike other platforms, with Budibase you can start from scratch and create business apps with no datasources
  - Budibase integrates with a number of popular tools allowing you to build apps
  - the Budibase API enables Budibase as a backend

- https://github.com/krn0x2/microflow
  - Microservice orchestration inspired by AWS Step functions and Apache Airflow

- https://github.com/dataplane-app/dataplane /go
  - an Airflow inspired data platform with additional data mesh capability to automate, schedule and design data pipelines and workflows.
  - Written in Golang and compiled to machine code to achieve extreme performance with a low memory and CPU footprint.

- https://github.com/jitsucom/jitsu /go
  - open source high-performance data collection service.
  - Capture events your application generates and stream to Data Warehouse; 
  - Pull data from APIs and save it to Data Warehouse
# more-lowcode
- corteza /go/vue
  - https://github.com/cortezaproject/corteza
  - https://github.com/cortezaproject/corteza-webapp-one
  - https://cortezaproject.org/
  - fully standardized low-code app development, business process, integration and data harmonization platform.

- https://github.com/centerofci/mathesar /python/svelte
  - https://wiki.mathesar.org/en/home
  - Web application providing an intuitive user experience to databases.
  - Mathesar directly operates on PostgreSQL databases
