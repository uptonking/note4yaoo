---
title: toc-saas-cms-lowcode
tags: [cms, lowcode, saas, toc]
created: 2023-01-20T21:58:47.061Z
modified: 2023-01-20T21:59:47.792Z
---

# toc-saas-cms-lowcode

# guide

- cms-dev
  - 交互的核心通常是编辑器

- [什么是比较好的低代码产品_Tw93](https://zhuanlan.zhihu.com/p/596474809)
  - platform, baas, cms, workflow, airtable-like
  - 流程自动化
  - notion-like

- ref
  - https://github.com/postlight/awesome-cms
# popular
- payload /9.1kStar/MIT/202301/ts/slate
  - https://github.com/payloadcms/payload
  - https://payloadcms.com/
  - https://demo.payloadcms.com/admin
  - Headless CMS and Application Framework built with TypeScript, Node.js, React and MongoDB
  - cms只提供管理界面来拖拽生成数据对应的api，不提供预览内容的前端
  - 不是典型的block-editor，富文本作为字段block
  - 后端依赖express、mongoose、passport
  - 前端依赖dnd-kit、monaco-editor、slate、react-beautiful-dnd、react-router5、webpack5、swc
  - Block-based Layout Builder
  - Extensible SlateJS rich text editor
  - A Mongo database to store your data
  - retrieve, and manipulate data of any shape via full REST and GraphQL APIs
  - File storage and access control
  - Payload dynamically generates a React admin panel to manage your data. 
    - Admin panel is built with Webpack, code-split, highly performant (even with 100+ fields), and written fully in TypeScript.
  - [Roadmap Discussions](https://github.com/payloadcms/payload/discussions/categories/roadmap)
  - [2023 Payload Roadmap](https://github.com/payloadcms/payload/discussions/1539)
  - [Payload (YC S22) – Headless CMS for Developers | Hacker News_202208](https://news.ycombinator.com/item?id=32665325)
    - v2 is coming and that will 100% be open-source!
  - Our business model is based on two things:
    - Enterprise features like SSO, audit logs, publication workflows, and translation workflows. 
    - Cloud hosting. 

- tinacms /8.3kStar/apache2/202301/ts
  - https://github.com/tinacms/tinacms
  - https://tina.io/
  - headless CMS for Markdown, MDX, and JSON.
  - 编辑器从prosemirror迁移到slate
  - Tina is a Git-backed headless cms
  - ui界面并不是wysiwyg
    - 而是侧边栏修改内容块，预览区显示效果，点击save会提交到github
    - 用户修改内容块后会触发代码更新进而执行cicd
  - 基于git实现cms的缺点
    - 每次提交+action构建时间很长，不如基于后端db的方案
    - 内容必须以文本/md的方式保存到github
  - Both developers and editors collaborate on a single source of truth git
  - Collaborate on content in real-time with live multi-user editing and change tracking.
  - Block-based editing
    - build out full pages using your pre-defined blocks
    - need to manually import the react-tinacms-editor(依赖prosemirror) plugin
  - [Unify .md & .mdx implementations](https://github.com/tinacms/tinacms/discussions/2869)
    - react-tinacms-editor editor also uses prosemirror, while the default rich-text editor uses slate.

- directus /19.5kStar/GPLv3/202301/ts/vue
  - https://github.com/directus/directus
  - https://directus.io/
  - Directus is a real-time API and App dashboard for managing SQL database content.
  - REST & GraphQL API. Instantly layers a blazingly fast Node.js API on top of any SQL database.
  - 后端依赖express、knex、async
  - 前端依赖vue3、tinymce5、p-queue、apexcharts

- webiny-js /6.3kStar/MIT/202301/ts/graphql
  - https://github.com/webiny/webiny-js
  - a headless CMS, page builder, form builder, and file manager, admin-area
  - Multi-tenant SaaS applications
  - build a GraphQL API using the Headless CMS
  - ui包依赖editorjs、rmwc、downshift
  - 产品定位明确，业务思路明确，文档简明
# cms-framework
- refine /6.5kStar/MIT/202212/ts
  - https://github.com/refinedev/refine
  - https://refine.dev/
  - headless web application framework developed with flexibility in mind.
  - It eliminates repetitive tasks demanded by CRUD operations and provides industry standard solutions for critical parts like authentication, access control, routing, networking, state management, and i18n.
  - Connectors for 15+ backend services including REST API
  - For convenience, it ships with ready-made integrations for Ant Design System, Material UI, Mantine, and Chakra UI.
  - Auto-generated CRUD UIs from your API data structure
  - state management & mutations with React Query
  - Out-of-the-box support for live/real-time applications
# cms
- netlify-cms /16kStar/MIT/202204/js
  - https://github.com/netlify/netlify-cms
  - A Git-based CMS for Static Site Generators
  - 依赖redux、react-dnd、immutable3、react15
  - 核心功能是提供了通过ui操作执行读写github的能力、文件编辑器、自动构建和发布
    - 文件内容可保存在本地或github
    - 文件内容的样式主题由dev控制

- https://github.com/fiatjaf/coisas /201907/js/inactive
  - a headless CMS specifically designed to let you edit files hosted in a GitHub repository. 
  - It is similar to Netlify CMS and Prose. 
  - 依赖prosemirror、mobx

- https://github.com/BuilderIO/builder /编辑器未开源
  - Drag and drop Visual CMS for React, Vue, Angular, and more
  - [Scope of the opensource project](https://github.com/BuilderIO/builder/issues/379)
    - open JSON format for describing applications (composed of components) as pure JSON and rendering them with our SDKs
  - What is closed source:
    - Our drag and drop editor. You can use it for free at buidler.io/fiddle
    - Our APIs - aka the ability to add multiple users to an account

- https://github.com/apostrophecms/apostrophe /js
  - full-featured, open source CMS built with Node.js that seeks to empower organizations by combining in-context editing and headless architecture in a full-stack JS environment.

- https://github.com/contember/engine /ts/graphql
  - Contember is an open-source, headless CMS without limits. It gives you full control over the administration interface and data structure. 
  - Contember Engine is a standalone server providing GraphQL API for your PostgreSQL database.
# more
- https://github.com/FactorJS/factor
  - Factor is an expressive & modular framework for JavaScript applications.
