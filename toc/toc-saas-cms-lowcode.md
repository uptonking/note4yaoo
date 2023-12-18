---
title: toc-saas-cms-lowcode
tags: [cms, lowcode, saas, toc]
created: 2023-01-20T21:58:47.061Z
modified: 2023-01-20T21:59:47.792Z
---

# toc-saas-cms-lowcode

# guide

- cms-dev
  - cms业务架构一般分为 服务端、管理端、展示端
  - 管理端交互的核心通常是编辑器

- [什么是比较好的低代码产品_Tw93](https://zhuanlan.zhihu.com/p/596474809)
  - platform, baas, cms, workflow, airtable-like
  - 流程自动化
  - notion-like

- [w3techs: Usage Statistics and Market Share of Content Management Systems](https://w3techs.com/technologies/overview/content_management)
  - WordPress, Wix, Squarespace, Joomla, Drupal, Adobe, PrestaShop, Webflow, TYPO3, Weebly, Gatsby, Hugo, Zendesk, Ghost, Odoo, MediaWiki, Gitbook, Jekyll, Salesforce

- ref
  - https://github.com/postlight/awesome-cms
  - [Headless CMS - Top Content Management Systems | Jamstack](https://jamstack.org/headless-cms/)
  - crm, erp
# lowcode-products
- [AppMaster - The no-code platform for building web & mobile apps](https://appmaster.io/)
# popular
- strapi /57.5kStar/MIT+EE/202311/ts
  - https://github.com/strapi/strapi
  - https://strapi.io/
  - the leading open-source headless CMS
  - 核心功能是提供了通过ui操作实现rest api的功能
    - 系统内容通过ui操作编写
    - 系统前端strapi没有限制，strapi只提供了api
  - The original purpose of the project was to help Bootstrap your API
  - Now, Strapi is an open-source headless CMS that gives developers the freedom to choose their favorite tools and frameworks and allows editors to manage and distribute their content using their application's admin panel.

- payloadcms /9.1kStar/MIT/202301/ts/slate
  - https://github.com/payloadcms/payload
  - https://payloadcms.com/
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

- directus /19.5kStar/GPLv3>BSL/202301/ts/vue
  - https://github.com/directus/directus
  - https://directus.io/
  - Directus is a real-time API and App dashboard for managing SQL database content.
  - REST & GraphQL API. Instantly layers a blazingly fast Node.js API on top of any SQL database.
  - 后端依赖express、knex、async
  - 前端依赖vue3、tinymce5、p-queue、apexcharts
  - [Change license to BSL-1.1_202304](https://github.com/directus/directus/pull/18330)
    - Non-production use of Directus is still completely free for everyone
    - Code released under this new license converts to GPLv3 (OSS) after 3 years
  - [Running Locally | Directus Docs](https://docs.directus.io/contributing/running-locally.html)
    - pnpm --dir api cli bootstrap 
    - 注意在.env中配置初始用户名密码
  - Directus uses TinyMCE, which stores content as a string of HTML. 
  - Directus is SQL-based which requires overhead like migrations and more.
  - Payload allows bringing your own Express server.
  - Directus only supports role-based access control (RBAC). However, Payload supports function-based access control which can be used on either a document or field-by-field basis 
  - dev-xp
  - 登录界面一直白屏，排查了很久未定位到原因，但firefox可正常打开，chrome体系都是白屏
    - [Unable to run Directus locally](https://github.com/directus/directus/issues/17786)
    - You have to set SERVE_APP=true in your .env file in order to run the api in dev mode with the build app.
    - 最终发现配置server_app后要访问的是服务端:8055/admin，而不是前端:8080/admin

- vrite /1kStar/AGPLv3/202307/ts
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

- tinacms /8.3kStar/apache2/202301/ts/git
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

- https://github.com/burdy-io/burdy /202202/ts/inactive
  - Headless CMS built in NodeJS and React. Written in Typescript
  - Node.js, TypeORM, Express
  - React, Fluent UI
  - Content types - 16 fields types out of the box, and you can easily extend it with your custom

- https://github.com/microfeed/microfeed
  - a lightweight content management system (CMS) self-hosted on Cloudflare. 
  - microfeed is built by Listen Notes and is hosted on Cloudflare's Pages, R2, D1, and Zero Trust.

- https://github.com/Thinkmill/keystatic /MIT/202311/ts
  - https://keystatic.com/
  - First-class CMS experience, TypeScript API, Markdown & YAML/JSON based, no DB.
  - Built with DNA from Keystone, connects directly to GitHub and doesn’t mess with your source code. 
  - Conceived(构想；设想) for modern front-end frameworks like Next.js, Remix and Astro, designed to fit into your workflow.

- https://github.com/tryghost/Ghost /js/MIT
  - Turn your audience into a business. 
  - Publishing, memberships, subscriptions and newsletters.

- alinea /654Star/MIT/202311/ts/query、tiptap
  - https://github.com/alineacms/alinea
  - https://alinea.sh/
  - https://demo.alinea.sh/
  - an open source headless CMS written in Typescript.
  - 非wysiwyg，左侧编辑块数据，右侧预览
  - 依赖dnd-kit、yjs、react-query、tiptap
  - Content is stored in flat files and committed to your repository
  - 👉🏻 Content is easily queryable through an in-memory SQLite database
  - Content is fully typed
  - Content is available during static site generation and when server side querying. Content is bundled with your code and can be queried with zero network overhead.
  - Alinea supports custom backends that can be hosted as a simple Node.js process or on serverless runtimes.
    - Hosting an Alinea backend requires several services such as storing and retrieving drafts, publishing changes and authenticating users

- https://github.com/MrXujiang/lowcode-cms
  - 基于dooring低台, 代码社区的开源cms系统
  - 后端依赖koa-session、koa-views、pug、qiniu
  - 前端依赖antd-pro-layout、umi.v3、braft-editor、turndown
  - server基于nodejs的服务端, 启动后可直接访问3000端口, 也就是内容SSR端
  - admin CMS的管理后 集成了用户管理, 内容审核, 内容发布, 数据统计等模块

- https://github.com/twentyhq/twenty /AGPLv3/ts
  - https://twenty.com/
  - We are building an Open Source CRM designed to be: enjoyable to use, easily extendable, and perfectly in-sync with your data.
  - 后端依赖nestjs、prisma、graphql、apollo/server
  - 前端依赖recoil、blocknote、chakra-ui、afterframe(raf)

- https://github.com/odoo/odoo /LGPLv3/python/js
  - https://www.odoo.com/
  - a suite of web based open source business apps.
  - The main Odoo Apps include an Open Source CRM, Website Builder, eCommerce, Warehouse Management, Project Management, Billing & Accounting, Point of Sale, Human Resources, Marketing, Manufacturing, ...

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

- https://github.com/atomicdata-dev/atomic-server /587Star/MIT/202311/rust/ts
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
  - forks
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
# cms
- netlify/decap-cms /16kStar/MIT/202204/js
  - https://github.com/netlify/netlify-cms
  - https://github.com/decaporg/decap-cms /js
  - https://decapcms.org/
  - A Git-based CMS for Static Site Generators
  - 依赖redux、react-dnd、immutable3、react15
  - 核心功能是提供了通过ui操作执行读写github的能力、文件编辑器、自动构建和发布
    - 文件内容可保存在本地或github
    - 文件内容的样式主题由dev控制

- https://github.com/StaticJsCMS/static-cms
  - https://www.staticcms.org/
  - A Git-based CMS for Static Site Generators

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
  - forks
  - https://github.com/Dynalon/mdwiki /GPLv3/201810/ts/js
  - https://github.com/unmacaque/mdwiki
    - marked was updated to support more GFM syntax
  - https://github.com/stephanedenis/mdwiki

- https://github.com/Ulbora/ulboracms /MIT/202303/go/js
  - http://ulbora.github.io/ulboracms
  - a self-contained CMS (no database needed) written in Golang. 
  - It uses a JSON datastore with content saved in both json files and in memory.
  - You can download and upload a single binary backup file containing content, images, and templates as needed.

- https://github.com/CromwellCMS/Cromwell /600Star/MIT/202308/ts
  - https://cromwellcms.com/docs/overview/intro/#examples
  - open source headless TypeScript CMS for creating lightning-fast websites with React and Next.js. 
  - It has a powerful plugin/theming system while providing extensive Admin panel GUI for WordPress-like user experience. 
  - Free full-featured online store and blog themes with multiple plugins.
  - Integrated Database. SQLite, MySQL, MariaDB, PostgreSQL are supported to use.
  - Use all power of Next.js, Nest.js, TypeORM, TypeGraphQL along with CMS API to build any type of website.
# more
- https://github.com/FactorJS/factor
  - Factor is an expressive & modular framework for JavaScript applications.
