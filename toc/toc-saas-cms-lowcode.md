---
title: toc-saas-cms-lowcode
tags: [cms, lowcode, saas, toc]
created: 2023-01-20T21:58:47.061Z
modified: 2023-01-20T21:59:47.792Z
---

# toc-saas-cms-lowcode

# guide

- file-first
  - 缺点
    - 不支持user/auth/permission
  - 优点
    - 个人使用方便
  - DecapCMS/NetlifyCMS
  - tinacms
  - keystatic
  - flowershow
  - mkdocs

- db-first
  - strapi, directus
  - Ghost, payloadcms
  - wagtail
  - emdash
  - Wiki.js

- cms-pm
  - 考虑以calendar/timeline/project/chat为核心，而不是editor
  - notion-like

- cms-dev
  - cms和admin管理系统的界限不是互斥的，可在一个框架fwk上实现cms或admin
  - cms业务架构一般分为 服务端、管理端、展示端
  - 管理端交互的核心通常是编辑器

- tips
  - alternatives: cms, crm, documentation, static-site-generator

- [w3techs: Usage Statistics and Market Share of Content Management Systems](https://w3techs.com/technologies/overview/content_management)
  - WordPress, Wix, Squarespace, Joomla, Drupal, Adobe, PrestaShop, Webflow, TYPO3, Weebly, Gatsby, Hugo, Zendesk, Ghost, 🔥 Odoo, 🔥 MediaWiki, Gitbook, Jekyll, Salesforce

- resources
  - https://github.com/postlight/awesome-cms
  - [Headless CMS - Top Content Management Systems | Jamstack](https://jamstack.org/headless-cms/)
  - [什么是比较好的低代码产品_Tw93](https://zhuanlan.zhihu.com/p/596474809): platform, baas, cms, workflow, airtable-like
# lowcode-products
- [AppMaster - The no-code platform for building web & mobile apps](https://appmaster.io/)
# popular
- strapi /57.5kStar/MIT+EE/202311/ts
  - https://github.com/strapi/strapi
  - https://docs.strapi.io/dev-docs/intro
  - https://strapi.io/
  - https://strapi.io/demo 一定时长后数据会清除
  - the leading open-source headless CMS
  - 后端依赖knex、umzug、koa、koa-static、commander、node-schedule
  - 前端依赖@reduxjs/toolkit、immer、codemirror5、date-fns、formik、markdown-it、react-dnd、sift、slate-react
  - 在admin添加新的content-type时，数据库会创建对应的表，同时后端src/api下面会自动生成对应的schema/router/controller/service，prod生产环境下不支持动态添加新的content-type
  - 核心功能是提供了通过ui操作实现rest api的功能
    - 系统内容通过ui操作编写
    - 系统前端strapi没有限制，strapi只提供了api
  - 未实现: versioning, draft/publish

- payloadcms /9.1kStar/MIT/202301/ts/slate
  - https://github.com/payloadcms/payload
  - https://payloadcms.com/
  - https://payloadcms.com/docs/getting-started/what-is-payload
  - https://demo.payloadcms.com/admin
  - Code-first Headless CMS and Application Framework built with TypeScript, Node.js, React and MongoDB
  - cms只提供管理界面来拖拽生成数据对应的api，不提供预览内容的前端
  - 不是典型的block-editor，富文本作为字段block
  - 后端依赖express、mongoose、passport
  - 前端依赖dnd-kit、monaco-editor、slate、react-beautiful-dnd、react-router5、webpack5、swc
  - 支持Version History and Drafts, Automatically maintain a history of changes to any given collection document
  - Block-based Layout Builder
  - Extensible SlateJS rich text editor
  - Extremely granular Access Control
  - A Mongo database to store your data
  - retrieve, and manipulate data of any shape via full REST and GraphQL APIs
  - Local file storage & upload
  - Payload dynamically generates a React admin panel to manage your data. 
    - Admin panel is built with Webpack, code-split, highly performant (even with 100+ fields), and written fully in TypeScript.
  - [Compare Payload against other headless CMS: strapi, directus](https://payloadcms.com/compare)
  - [Roadmap Discussions](https://github.com/payloadcms/payload/discussions/categories/roadmap)
  - [Roadmap: Multiple Database Support](https://github.com/payloadcms/payload/discussions/287)
  - [Payload (YC S22) – Headless CMS for Developers | Hacker News_202208](https://news.ycombinator.com/item?id=32665325)
  - Our business model is based on two things:
    - Enterprise features like SSO, audit logs, publication workflows, and translation workflows. 
    - Cloud hosting. 
- https://github.com/AlessioGr/payload-plugin-lexical
  - Extends payload CMS with Meta's lexical RichText editor - a much more advanced and customizable richtext editor
- https://github.com/NouanceLabs/payload-dashboard-analytics
  - A plugin for Payload CMS to connect analytics data to your Payload dashboard.

- directus /25kStar/GPLv3 > BSL/202403/ts/vue
  - https://github.com/directus/directus
  - https://directus.io/
  - https://docs.directus.io/
  - Directus is an instant REST+GraphQL API and intuitive no-code data collaboration app for any SQL database.
  - 后端依赖express、knex、async、commander、graphql、ioredis、keyv、marked、micromustache、node-cron、rate-limiter-flexible、sharp、vm2
  - 前端依赖vue3、tinymce5、p-queue、apexcharts
  - 涉及graphql的代码不多，可以尝试移除
  - 在admin添加新的data-model时，数据库会创建对应的表
  - [Change license to BSL-1.1_20230427](https://github.com/directus/directus/pull/18330)
    - Code released under this new license converts to GPLv3 (OSS) after 3 years
  - [Running Locally | Directus Docs](https://docs.directus.io/contributing/running-locally.html)
    - pnpm --dir api cli bootstrap 
    - 注意在.env中配置初始用户名密码
  - Directus uses TinyMCE, which stores content as a string of HTML
  - Directus is SQL-based which requires overhead like migrations
  - Directus only supports role-based access control (RBAC). However, Payload supports function-based access control which can be used on either a document or field-by-field basis 
  - dev-xp
  - 登录界面一直白屏，排查了很久未定位到原因，但firefox可正常打开，chrome体系都是白屏
    - [Unable to run Directus locally](https://github.com/directus/directus/issues/17786)
    - You have to set `SERVE_APP=true` in your .env file in order to run the api in dev mode with the build app.
    - 最终发现配置server_app后要访问的是服务端:8055/admin，而不是前端:8080/admin
  - https://github.com/directus-labs/agency-os /MIT/202402/ts/vue/nuxt
    - https://agencyos.dev/
    - https://agency-os.vercel.app/
    - 管理后台在 https://directus.pizza/
    - The open source operating system for digital agencies. 
    - Built with Nuxt 3 Website/Application + Directus Backend.
    - Brought to you by partnership magic between Directus and NuxtLabs.
    - [Introducing AgencyOS: The All-In-One Operating System for Digital Agencies _20231025](https://directus.io/blog/announcing-agencyos)
      - we’re releasing AgencyOS as the first example of a purpose-built system to show off the incredible functionality that you can build in record time with Directus.
  - forks
  - https://github.com/LaWebcapsule/directus9 /GPLv3/202402/ts/vue
    - a fork of the Directus 9
    - Directus 10 is now a premium open-source software
  - https://github.com/ctholho/qryo /202304/ts/inactive
    - Testing if offline first CRUD applications with Directus are possible
    - Qryo helps you build offline-first web apps. It concerns itself with server requests like CRUD REST calls or RPCs. 
    - Qryo is totally not functional yet. This is a proof of concept 
    - Stack: Tanstack/query, Nuxt and Directus
    - persist the mutation in IndexedDB
  - https://github.com/directus-community/awesome-directus
    - Extensions, Examples/Showcases
  - [Directus extensions](https://directusextensions.com/browse)
    - Directus Extensions includes all Directus Extensions available on npm that adhere to the `directus-extension-*` naming strategy

- vrite /1kStar/AGPLv3+Elastic/202403/ts
  - https://github.com/vriteio/vrite
  - https://vrite.io/
  - https://editor.vrite.io/
  - headless CMS intended for technical content like programming blogs or documentation
  - 后端依赖trpc-server/openapi、fastify、yjs、zod、open-graph-scraper
  - 协作依赖mongodb、hocuspocus
  - 前端依赖solid-js、solid-primitives、tiptap、trpc-client、yjs
  - editor包不依赖solid-js
  - Built-in Kanban dashboard for managing content production and delivery; 
  - Versitile API and Extension System for customizing your experience and delivering content to any frontend; 
  - https://x.com/vriteio/status/1809492361086451846
    - 202407: v0.4.4 introduces version history to Vrite
    - Version snapshots are taken automatically and stored for up to 30 days
    - You can preview, restore, and assign labels to specific versions;
    - You can use the diff view to see differences between different versions

- tinacms /13.6kStar/apache2/202606/ts/git
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

- https://github.com/Thinkmill/keystatic /2.2kStar/MIT/202605/ts
  - https://keystatic.com/
  - First-class CMS experience, TypeScript API, Markdown & YAML/JSON based, no DB.
  - Built with DNA from Keystone, connects directly to GitHub and doesn’t mess with your source code. 
  - Conceived(构想；设想) for modern front-end frameworks like Next.js, Remix and Astro, designed to fit into your workflow.
  - keystatic is not built on top of Keystone. they are "sibling" projects. Both are created and maintained by Thinkmill, an Australian software consultancy. Because they are built by the same team, they share a lot of "DNA" and design philosophies. For instance, they share similar developer ergonomics (like using a TypeScript API to define your content schema), and Keystatic's modern Admin UI uses a design system (Keystar UI) that is also being integrated into Keystone.
  - [What are Thinkmill's plans for Keystatic in 2025 _202508](https://github.com/Thinkmill/keystatic/discussions/1442)
    - Thinkmill is applying Keystatic in several behind-the-scenes projects, including Thinkmill's own public website and Keystone's documentation. Keystar UI (it's design system) is also now integrated directly into Keystone 6's new Admin UI.
  - [Any plans for GraphQL API?  _202403](https://github.com/Thinkmill/keystatic/discussions/979)
    - As of now there are no concrete plans for this. Worth mentioning, what you're describing (having a DB + API) sounds a lot like Keystatic's older cousin Keystone, built by the same team.
    - For more ambitious and CRUD-capable projects, you might want to look into that as well!

- https://github.com/mdcms-ai/mdcms /MIT/202606/ts
  - https://www.mdcms.ai/
  - https://docs.mdcms.ai/
  - open-source CMS that's Markdown-first.
  - MDCMS treats a PostgreSQL database as the source of truth. Content files are synced between the database and your local filesystem via CLI commands (mdcms push / mdcms pull), keeping your repository clean and your content workflow independent of your deployment pipeline.
  - Developers define schemas in code and sync via CLI. Editors get a visual Studio they never have to leave. AI agents process content through the same API. 
  - Author content in Markdown or MDX with custom component support
  - ⏳ Versioning and publishing: Full draft/publish lifecycle with immutable version history
  - Extensible modules	First-party module system for extending server and CLI behavior
  - Code-first schema: Define content types, fields, and references in TypeScript with Zod validation
  - Embeddable React admin interface with a rich document editor, schema browser, and environment management
  - Auth and RBAC	Session auth, OIDC/SAML SSO, API keys, and role-based access control
  - 📡 roadmap
    - Live preview - Real-time content preview in your frontend
    - Live collaboration - Live co-editing with conflict resolution
    - Media management - Upload, organize, and serve media assets via MinIO/S3
    - Full-text search - Search across content with indexing and ranking
    - Bulk operations - Batch publish, unpublish, and delete actions
  - [Self-Hosting - MDCMS ](https://docs.mdcms.ai/guide/self-hosting)
    - starts the MDCMS server along with PostgreSQL, Redis, MinIO, and Mailhog. Migrations run automatically on first boot.

- https://github.com/flowershow/flowershow /1.1kStar/AGPL/202606/ts
  - https://flowershow.app/docs/getting-started
  - https://flowershow.app/
  - Publish markdown (and html) websites, docs, wikis and websites in seconds. Integrates with your AI.
  - https://flowershow.app itself is built and published with Flowershow
  - 类似 git-based cms, 不依赖git
  - 输入文件 ob-vault/github-repo/dnd-upload/cli
  - 🐛
    - 在线编辑不方便
    - 更新是全量

- webiny-js /6.3kStar/MIT/202301/ts/graphql/文档清晰/代码量大(很多包)
  - https://github.com/webiny/webiny-js
  - a headless CMS, page builder, form builder, and file manager, admin-area
  - Multi-tenant SaaS applications
  - build a GraphQL API using the Headless CMS
  - ui包依赖editorjs、rmwc、downshift
  - 产品定位明确，业务思路明确，文档简明
  - Webiny comes in 2 database options, DynamoDB + Elasticsearch and DynamoDB only. 
  - [How to use other databases with Webiny?](https://github.com/webiny/webiny-js/discussions/2156)
    - In theory, it’s possible, but you would have to implement the storage operations packages yourself.
    - since Webiny is a Serverless product, using MySQL or MongoDB is far from recommended, as they don’t have serverless implementations.

- https://github.com/tryghost/Ghost /MIT/202402/js
  - https://ghost.org/
  - Independent technology for modern publishing, memberships, subscriptions and newsletters.
  - core依赖bookshelf-relations、knex2、express-hbs、mysql2、yjs
  - admin依赖ember、lexical
  - [Initial setup for Lexical multiplayer websockets service _202304](https://github.com/TryGhost/Ghost/commit/b286faf011c6e487198e93f0b6cab11f2cae7486)
    - Docs are in-memory only, YJS state will be lost on server restart
    - **No tie-in with saved lexical state** . Lexical state is updated in the post model via normal API requests from Admin which can mean the multiplayer doc and the saved lexical state become out of sync but there's no detection/indication of that state at present. Will also trigger the "someone else is editing" errors because multiplayer doesn't yet override the default post update collision detection

- https://github.com/burdy-io/burdy /234Star/MIT/202202/ts/inactive
  - Headless CMS built in NodeJS and React. Written in Typescript
  - Node.js, TypeORM, Express
  - React, Fluent UI
  - Content types - 16 fields types out of the box, and you can easily extend it with your custom

- https://github.com/microfeed/microfeed
  - a lightweight content management system (CMS) self-hosted on Cloudflare. 
  - microfeed is built by Listen Notes and is hosted on Cloudflare's Pages, R2, D1, and Zero Trust.

- alinea /654Star/MIT/202403/ts/tiptap
  - https://github.com/alineacms/alinea
  - https://alinea.sh/
  - https://demo.alinea.sh/
  - modern content management system
  - 非wysiwyg，左侧编辑块数据，右侧预览
  - 依赖dnd-kit、yjs、react-query、tiptap
  - Content is stored in flat files and committed to your repository
  - 🛢️ Content is easily queryable through an in-memory SQLite database
  - Content is version controlled in your git repository. Easily branch and feature test content changes.
  - Content is available during static site generation and when server side querying. 
    - Content is bundled with your code and can be queried with zero network overhead.
    - Content is bundled with deploys so it can be retrieved without network roundtrips.
  - Alinea supports custom backends that can be hosted as a simple Node.js process or on serverless runtimes.
    - Hosting an Alinea backend requires several services such as storing and retrieving drafts, publishing changes and authenticating users
  - 🚀 [Introducing Alinea _202209](https://alinea.sh/blog/introducing-alinea)

- https://github.com/MrXujiang/lowcode-cms
  - 基于dooring低台, 代码社区的开源cms系统
  - 后端依赖koa-session、koa-views、pug、qiniu
  - 前端依赖antd-pro-layout、umi.v3、braft-editor、turndown
  - server基于nodejs的服务端, 启动后可直接访问3000端口, 也就是内容SSR端
  - admin CMS的管理后 集成了用户管理, 内容审核, 内容发布, 数据统计等模块

- https://github.com/apstanisic/zmaj /ts
  - https://zmaj.vercel.app/
  - a headless CMS with RESTful API for your database and admin panel to easily manage your data
  - Built on top of React and React Admin for admin panel, and NestJS and Sequelize for API.
  - 依赖nestjs-passport、knex、sequelize

- refine /6.5kStar/MIT/202212/ts
  - https://github.com/refinedev/refine
  - https://refine.dev/
  - headless web application framework developed with flexibility in mind.
  - 非典型cms
  - It eliminates repetitive tasks demanded by CRUD operations and provides industry standard solutions for critical parts like authentication, access control, routing, networking, state management, and i18n.
  - Connectors for 15+ backend services including REST API
  - For convenience, it ships with ready-made integrations for Ant Design System, Material UI, Mantine, and Chakra UI.
  - Auto-generated CRUD UIs from your API data structure
  - state management & mutations with React Query
  - Out-of-the-box support for live/real-time applications

- https://github.com/atomicdata-dev/atomic-server /587Star/MIT/202401/rust/ts
  - https://atomicserver.eu/
  - a lightweight, yet powerful CMS / Graph Database
  - powered by actix-web and sled database
  - Documents, collaborative, rich text, similar to Google Docs / Notion.
  - Tables, with strict schema validation, keyboard support, copy / paste support. Similar to Airtable.
  - Event-sourced versioning / history powered by Atomic Commits
  - Synchronization using websockets
  - Full-text search with fuzzy search and various operators, often <3ms responses. Powered by tantivy.
  - [Atomic Data is a modular specification for sharing, modifying and modeling graph data](https://docs.atomicdata.dev/)
    - It combines the ease of use of JSON, the connectivity of RDF (linked data) and the reliability of type-safety.
    - Atomic Data is Linked Data, as it is a strict subset of RDF.
    - The default serialization format for Atomic Data is JSON-AD

- https://github.com/wagtail/wagtail /19.7kStar/BSD/202510/python/django
  - https://wagtail.org/
  - A Django content management system focused on flexibility and user experience
  - Content API for 'headless' sites with decoupled front-end
  - StreamField encourages flexible content without compromising structure
  - integrated search, using Elasticsearch or PostgreSQL
  - Excellent support for images and embedded content
  - Runs on a Raspberry Pi or a multi-datacenter cloud platform

- https://github.com/openstax/openstax-cms /AGPLv3/202501/python
  - https://openstax.org/
  - The OpenStax CMS, built using Wagtail on top of Django.
  - SQLite is supported as an alternative to PostgreSQL
# erp/crm
- https://github.com/twentyhq/twenty /AGPLv3+EE/202411/ts
  - https://twenty.com/
  - https://demo.twenty.com/
  - Building a modern alternative to Salesforce, powered by the community
  - We are building an Open Source CRM designed to be: enjoyable to use, easily extendable, and perfectly in-sync with your data.
  - a modern alternative to Salesforce
  - 后端依赖nestjs、prisma、graphql、apollo/server
  - 前端依赖recoil、blocknote、chakra-ui、afterframe(raf)

- https://github.com/odoo/odoo /LGPLv3/python/js
  - https://www.odoo.com/
  - a suite of web based open source business apps.
  - The main Odoo Apps include an Open Source CRM, Website Builder, eCommerce, Warehouse Management, Project Management, Billing & Accounting, Point of Sale, Human Resources, Marketing, Manufacturing
- https://github.com/tryton/tryton /GPL/202505/python
  - https://foss.heptapod.net/tryton/tryton
  - Tryton is business software, ideal for companies of any size, easy to use, complete and 100% Open Source.
  - [GNU Health | Hacker News _201611](https://news.ycombinator.com/item?id=12984383)
    - 👷(founder/CEO of Odoo):tryton is a fork of OpenERP. OpenERP is now known as Odoo
    - Tryton's fork was motivated by disagreements on the technical and business directions.
    - Odoo moved to the web, Tryton was attached to the GTK/rich client.
    - The Tryton founders were 2 ex-employees of Odoo back in 2008 before the fork. Odoo had 5 employees at that time.

- https://github.com/frappe/erpnext /25kStar/GPLv3/202505/python
  - https://frappe.io/erpnext
  - 100% Open-Source ERP system to help you run your business.
  - Projects
  - Asset Management
  - Order Management
  - Accounting
  - 🆚 [Here's why Open Source ERPNext is better than Odoo](https://frappe.io/erpnext/comparisons/erpnext-vs-odoo)
    - odoo: Only some of the core modules are available for the public
    - you can use ERPNext for free if you want to. You only have to pay if you need hosting, and even then, it’s significantly cheaper than alternatives like Odoo which make you pay per user.
    - Odoo lets you customize applications without coding through Odoo Studio, but it’s only available on its most expensive plan.
  - https://github.com/frappe/frappe /MIT/202505/python/js
    - https://frappeframework.com/
    - https://erpnext.com/
    - Low code web framework for real world applications, in Python and Javascript
    - Full-stack web application framework that uses Python and MariaDB on the server side and a tightly integrated client side library. Built for ERPNext.
  - https://github.com/frappe/frappe-ui /MIT/202505/ts/vue
    - a set of components and utilities for rapid UI development. 
    - Components are built using Vue 3 and Tailwind
    - Headless UI, tiptap, dayjs

- https://github.com/ever-co/ever-gauzy /2.6kStar/AGPL/202505/ts
  - https://gauzy.co/
  - Open Business Management Platform (ERP/CRM/HRM/ATS/PM)
  - Ever® Gauzy™ - Open Business Management Platform for Collaborative, On-Demand and Sharing Economies.

- https://github.com/erxes/erxes /3.6kStar/AGPL+EE/202505/ts
  - https://erxes.io/
  - source available experience management infrastructure.
  - erxes is composed of 2 main components: XOS & Plugins
# in-memory/json-cms/dashboard
- TiddlyWiki5 /7.5kStar/BSD/202311/js
  - https://github.com/Jermolene/TiddlyWiki5
  - https://tiddlywiki.com/
  - https://tiddlywiki.com/dev/ Developer documentation
  - A self-contained JavaScript wiki for the browser, Node.js, AWS Lambda etc.
  - a non-linear personal web notebook that anyone can use and keep forever
  - It can be used as a single HTML file in the browser or as a powerful Node.js application. 
  - Except of a micro-kernel written in JavaScript the whole application consist of a own data-structure called tiddlers and a own markup language called wikiText.
  - view层基于tid文件

- https://github.com/amelki/cms-json /133Star/MIT/201810/ts
  - http://tenorcms.com/
  - A lightweight CMS loading and saving its data from/to a json file
  - 依赖react-router.v4、react-redux、react-dnd、markdown-it、express
  - It runs the CMS with a default JSON and Schema files. 
  - 🍴 forks
  - https://github.com/luke-lewandowski/cms-json

- https://github.com/sidharthmenon/simple-json-flat-file-cms /201807/js
  - https://sidharthmenon.github.io/simple-json-flat-file-cms/
  - https://sidharthmenon.github.io/simple-json-flat-file-cms/example-website/
  - Simple and dirty flat file CMS with data saved on JSON file.
  - No Backend No Database
  - 依赖vue-markdown，在线编辑后保存会下载json

- https://github.com/mikelinden1/crayon-cms /202309/js
  - a Frontend CMS written in React + Redux + Reselect that is completely configurable with a JSON files and works with any REST API.
  - Rename src/config-sample to src/config and configure cms modules.

- https://github.com/chrisdiana/cms.js /3kStar/MIT/202103/js/NoDeps/inactive
  - CMS.js is a fully Client-side, JavaScript Markdown Site generator in the spirit of Jekyll that uses plain ol' HTML, CSS and JavaScript to generate your website. 
  - CMS.js is like a file-based CMS. It takes your content, renders Markdown and delivers a complete website in Single-Page App
  - CMS.js supports two website modes, Github and Server. 
  - [Server Mode](https://github.com/chrisdiana/cms.js/wiki/Server-Mode)
    - In Server mode, CMS.js takes advantage of the Server's Directory Indexing feature. 
    - By allowing indexes, CMS.js sends an AJAX call to your specified fo

- https://github.com/servuscms/servus /26Star/GPLv3/202311/rust
  - a simple CMS / blogging engine that is fully self-contained within one executable file.
  - rendered HTML files are stored in memory and served directly by Servus.
  - Posting can be done using the Nostr protocol's Long-form Content event kind, so any Nostr client compatible with NIP-23 can be used for posting.
  - all content and settings are stored in a local directory (on the machine running Servus).a full backup is just a rsync command
  - All content served to the readers is plain HTML served over HTTP(S). No Javascript that generates the UI elements on the client side
  - Multiple websites in one instance, that can be separately administered. 
  - All web pages are pre-rendered so they can immediately be served when a HTTP request is received.
# cloud-cms
- https://github.com/jadeallencook/gdoc-js /202110/js
  - http://jadeallencook.github.io/gDoc.js/
  - Use Google Spreadsheets as your CMS & to save your inputs!
  - 基于第三方服务的cms可参考基于git的cms

- https://github.com/misterfresh/react-drive-cms /202204/js
  - http://misterfresh.github.io/react-drive-cms/
  - Publish articles directly from Google Drive to your blog with React JS

- https://github.com/jansmolders86/github-pages-cms /202002/js/inactive
  - https://jansmolders86.github.io/github-pages-cms/
  - A simple CMS for Github Pages
  - 未实现数据的更新和保存
  - The content is exported as a base64 encoded .bin file but is in fact, a simple JSON file 
  - On the client side you can retrieve the data and assign it to elements using, for example; data attributes
  - convert the initial content.json to a base64 Blob and save that as a bin file. 
    - do an AJAX call, get the Blob, convert it back to a JSON and substitute or fill html with said content
  - You can use a Schema JSON file to control the way the CMS is rendering the fields.
  - The "CMS" grabs the JSON, renders the contents using jdorn's
    - https://github.com/jdorn/json-editor
  - https://github.com/jansmolders86/gh-cms-starter-template
    - https://jansmolders86.github.io/gh-cms-starter-template/
    - A starter template for a website managed with GH-CMS
# git-based-cms
- decap/netlify-cms /19.2kStar/MIT/202606/js
  - https://github.com/decaporg/decap-cms
  - https://github.com/netlify/netlify-cms
  - https://decapcms.org/
  - A Git-based CMS for Static Site Generators
  - It presents a clean UI for editing content stored in a Git repository.
  - 依赖redux、react-dnd、immutable3、react15
  - 核心功能是提供了通过ui操作执行读写github的能力、文件编辑器、自动构建和发布
    - 文件内容可保存在本地或github
    - 文件内容的样式主题由dev控制

- https://github.com/StaticJsCMS/static-cms
  - https://www.staticcms.org/
  - A Git-based CMS for Static Site Generators

- https://github.com/avitorio/outstatic /3.1kStar/MIT > FSL/202606/ts
  - https://outstatic.com/
  - A static CMS for Next.js
  - No need for databases, external services, or complicated setups. 
  - It allows you to create, edit and save content that is automatically committed to your repository and deployed to your live website.
  - [Show HN: I made a CMS that uses Git to store your data | Hacker News _20221023](https://news.ycombinator.com/item?id=33306029)
# cms
- https://github.com/skelpo/cms /MIT/202605/ts
  - https://skelpo.com/
  - https://beta.perryts.com/
  - A blazingly fast, opinionated, native TypeScript CMS. 
  - Designed for Perry AOT, runs on Node and Bun.
  - https://x.com/realamlug/status/2057337901432684712
    - compiles to a ~10 MB binary via Perry
    - role-aware UI by construction
    - CLI ≡ API ≡ Admin

- https://github.com/emdash-cms/emdash /10.9kStar/MIT/202606/ts/astro
  - https://emdashcms.com/
  - a full-stack TypeScript CMS based on Astro and Cloudflare; the spiritual successor to WordPress
  - EmDash takes the ideas that made WordPress dominant -- extensibility, admin UX, a plugin ecosystem -- and rebuilds them on serverless, type-safe foundations. Plugins run in sandboxed Worker isolates
  - EmDash depends on Dynamic Workers to run secure sandboxed plugins. Dynamic Workers are currently only available on paid accounts
  - WordPress stores rich text as `HTML` with metadata embedded in comments -- tying your content to its DOM representation. 
    - EmDash uses Portable Text, a structured JSON format that decouples content from presentation. Your content can render as a web page, a mobile app, an email, or an API response without parsing HTML.
  - EmDash ships with agent skills for building plugins and themes, a CLI that lets agents manage content and schema programmatically, and a built-in MCP server so AI tools like Claude and ChatGPT can interact with your site directly.
  - EmDash uses portable abstractions at every layer -- Kysely for SQL, S3 API for storage -- that work with SQLite, D1, Turso, PostgreSQL, R2, AWS S3, or local files. It runs best on Cloudflare, but it's not locked to it.
  - Content types are defined in the database, not in code. Non-developers create and modify collections through the admin UI. Each collection gets a real SQL table with typed columns.

- https://github.com/fiatjaf/coisas /317Star/MIT/201907/js/inactive
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

- https://github.com/hashicorp-forge/hermes
  - An Open Source Document Management System
  - [Introducing Hermes, An Open Source Document Management System](https://www.hashicorp.com/blog/introducing-hermes-an-open-source-document-management-system)
  - Hermes uses Golang for the backend and Ember.js for the front end. 
  - It uses a PostgreSQL database for storage and Algolia to power its search capabilities. 
  - It also leverages several Google Workspace services for creating and modifying documents, sending email, etc.

- https://github.com/ganskef/mdwiki /202310/js
  - CMS/Wiki using Markdown - 100% client side single-page application 
  - No special software installation or server side processing is required. Just upload the mdwiki.html into the same directory as your Markdown files and you are good to go!
  - This is a fork of the stable Dynalon MDwiki release branch v0.6.x containing updated dependencies with all the beloved features (like Markdown include which is missed in the master branch). The original repository is unmaintained and archived (read-only).
  - 🍴 forks
  - https://github.com/Dynalon/mdwiki /GPLv3/201810/ts/js
  - https://github.com/unmacaque/mdwiki
    - marked was updated to support more GFM syntax
  - https://github.com/stephanedenis/mdwiki

- https://github.com/Ulbora/ulboracms /MIT/202303/go/js
  - http://ulbora.github.io/ulboracms
  - a self-contained CMS (no database needed) written in Golang. 
  - It uses a JSON datastore with content saved in both json files and in memory.
  - You can download and upload a single binary backup file containing content, images, and templates as needed.

- https://github.com/CromwellCMS/Cromwell /600Star/MIT/202308/ts/inactive
  - https://cromwellcms.com/docs/overview/intro/#examples
  - open source headless TypeScript CMS for creating lightning-fast websites with React and Next.js. 
  - It has a powerful plugin/theming system while providing extensive Admin panel GUI for WordPress-like user experience. 
  - Free full-featured online store and blog themes with multiple plugins.
  - Integrated Database. SQLite, MySQL, MariaDB, PostgreSQL are supported to use.
  - Use all power of Next.js, Nest.js, TypeORM, TypeGraphQL along with CMS API to build any type of website.

- https://github.com/DominateAi/Dominate-AI /202312/js
  - open source CRM for Tech Founders
  - 依赖MongoDB、ag-grid-react、xlsx

- https://github.com/avored/avored-rust-cms /GPLv3/202401/rust/js
  - https://avored.github.io/avored-rust-cms/
  - AvoRed Rust CMS implement with the help of axum web framework and surrealdb as database.

- https://github.com/power-cms/power-cms /201903/ts/inactive
  - a Domain Driven, CQRS based CMS project in Microservices architecture, written for developers.
# blogging
- https://github.com/LetTTGACO/elog /MIT/202401/ts
  - https://elog.1874.cool/
  - Markdown 批量导出工具、开放式跨平台博客解决方案
  - 随意组合写作平台(语雀/飞书/Notion/FlowUs)和部署平台(Hexo/Vitepress/Halo/Confluence/WordPress等)
  - Elog支持了在生成MD文件之前，将扫描到的图片上传到图床上，并对文档中的图片链接进行替换。 当前支持的图床有： 本地/阿里云oss/腾讯云cos/Github图床

- https://github.com/getgridea/gridea /MIT/202302/ts/vue
  - https://open.gridea.dev/
  - 一个静态博客写作客户端
  - 你可以自定义源文件夹，利用 OneDrive、百度网盘、iCloud、Dropbox 等进行多设备同步
  - [Gridea - Build your digital garden, Make writing the best way to talk](https://gridea.dev/)
    - 开源了客户端
# more
- https://github.com/FactorJS/factor
  - Factor is an expressive & modular framework for JavaScript applications.
