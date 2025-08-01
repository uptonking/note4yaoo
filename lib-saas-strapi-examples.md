---
title: lib-saas-strapi-examples
tags: [examples, strapi]
created: 2023-12-15T19:30:11.399Z
modified: 2023-12-15T19:30:23.094Z
---

# lib-saas-strapi-examples

# guide

- examples: shop, form-builder

- fans-strapi
  - https://github.com/notum-cz/strapi-plugin-content-versioning
  - https://github.com/VirtusLab-Open-Source/strapi-plugin-reactions
  - https://github.com/ComfortablyCoding/strapi-plugin-io

- providers: storage, email, translate

- resources
  - [Strapi showcases, 很多案例的官网但非开源](https://strapi.io/showcases)
  - [Websites using Strapi](https://trends.builtwith.com/websitelist/Strapi)
  - https://www.npmjs.com/org/strapi
# popular
- strapi /57.5kStar/MIT+EE/202403/ts
  - https://github.com/strapi/strapi
  - https://strapi.io/
  - https://strapi.io/demo 一定时长后数据会清除
  - the leading open-source headless CMS
  - 核心功能是提供了通过ui操作实现rest api的功能，系统前端没有限制，strapi只提供了api
  - 后端依赖koa、knex、umzug、commander、passport-local、node-schedule、casl
  - 前端依赖@reduxjs/toolkit、immer、slate、markdown-it、codemirror5、formik、react-dnd、react-window、sift、vite、react-intl
  - The original purpose of the project was to help Bootstrap your API
  - Now, Strapi is an open-source headless CMS that gives developers the freedom to choose their favorite tools and frameworks and allows editors to manage and distribute their content using their application's admin panel.

- https://github.com/strapi-community/awesome-strapi
  - A curated list of awesome things related to Strapi
  - https://github.com/strapi/design-system

- https://github.com/Stun3R/isstrapiready
  - https://isstrapiready.com/
  - Discover the advancement of Strapi for the latest Strapi version and the list of compatible plugins. (Current: v4)
  - https://github.com/strapi-community/isstrapiready
    - v5

- https://github.com/strapi/strapi-examples /202311
  - List of examples using Strapi
  - https://github.com/strapi/nextjs-corporate-starter /202312/ts
  - https://github.com/ghoshnirmalya/nextjs-strapi-boilerplate /202210/ts

- https://github.com/strapi/starters-and-templates /202307/js
  - Monorepo for all official Strapi v4 starters and templates.
  - As you may have noticed, a lot of the Starters are out of date and given constraints in bandwidth and other priorities, we've decided to sunset all Starters and only actively maintain a single Next.js Starter.

- https://github.com/strapi/best-practices-samples /202304/js
  - Sample project code for Strapi Best Practice calls

- https://github.com/strapi/foodadvisor /MIT/202309/js
  - the official Strapi demo application
  - Strapi project with existing Content-types and data (/api)
  - Next.js client ready to fetch the content of the Strapi application (/client)
  - You can also fork this repository and deploy it on Strapi Cloud

- https://github.com/strapi/blocks-react-renderer /MIT/202403/ts
  - A React renderer for the Strapi's Blocks rich text editor
  - https://github.com/klammerzu/blocks-html-renderer /202401/ts
    - Render the content of Strapi's Blocks rich text editor as HTML
  - https://github.com/niklasfjeldberg/vue-strapi-blocks-renderer /202404/ts/vue
    - Easily render the content of Strapi's new Blocks rich text editor in your Vue frontend.
  - https://github.com/freb97/nuxt-strapi-blocks-renderer /MIT/202404/ts
    - Nuxt 3 module for rendering text with the new Blocks rich text editor from Strapi CMS
  - https://github.com/sinkng/strapi-custom-field-type-renderer /202201/js
    - v4

- https://github.com/iopanda/strapi-crack-ee /202310/js
  - only for technique testing, DO NOT use this package in any production environment
  - 在本地生成lic文件 `fs.writeFileSync(fx, publicKey)`

- https://github.com/liveblocks/strapi-demo /202310/ts
  - Strapi + Liveblocks demo

- https://github.com/its-devtastic/curator /MIT/202402/ts
  - https://www.curatorjs.org/
  - An alternative Strapi admin
  - 依赖zustand、dnd-kit、tiptap2、antd5、formik、i18next
  - 去掉了content-type-builder，可看做重内容的web app
  - mobile-friendly admin
  - Content versioning*
  - Audit logs*
  - Flexible plugin system
  - Curator offers a Strapi plugin that adds those features, and an alternative admin app that is easier to customize.
  - customizable admin built with React, Ant Design and Tailwind.
  - ❌ 不支持: Role management, Content-type builder(对终端用户不重要)

- https://github.com/Stun3R/strapi-sdk-js /MIT/202308/ts/inactive
  - https://strapi-sdk-js.netlify.app/
  - Javascript SDK for your Strapi API
  - Simplified request responses
  - https://github.com/strapi/strapi-sdk-javascript /201910/archived
    - We stopped to maintained it because the features provided by this SDK are the same as a good HTTP client well configured

- https://github.com/Prototypr/prototypr-frontend /150Star/NALic/202501/js
  - https://prototypr.io/
  - https://prototypr-frontend.vercel.app/
  - Open source publishing platform, built with Next.js and Strapi CMS backend. 
  - Uses Tiptap/Prose-mirror editor.
  - This site uses Next.js's Static Generation feature using `Strapi` as the data source.
  - https://github.com/Prototypr/prototypr-backend /MIT/202403/js
    - 依赖strapi.v4、strapi-plugin-meilisearch、radix-ui、tiptap、novel(editor)
  - https://open.prototypr.io/
    - develop Prototypr as an inclusive and open source Web Monetized publishing platform for designers

- https://github.com/losol/converto /GPLv3/202311/ts/inactive
  - a Strapi base solution for converting HTML to PDF
  - 依赖puppeteer、zod
  - 输入html内容或url，返回pdf, 实现简单
  - 🧐 其实无需使用数据库相关功能，直接用nodejs+puppeteer更简单，未持久化到数据库
  - It can take either raw HTML or an URL as input, and will return an PDF generated on headless Chrome (Puppeteer).
  - This solution does no checks on the html sent for conversion, make sure you trust HTML sent in to the solution.
  - This solution exposes an API, which takes html as an input, and returns an pdf generated by headless Chrome (Puppeteer).
  - https://github.com/isneezy/pdf-generator-service /MIT/202301/ts/无strapi
    - simple express service that generates a pdf based on the submitted HTML using Chromium and Puppeteer.

- https://github.com/strapify-dev/Strapify /MIT/202310/js/inactive
  - https://www.strapify.dev/
  - https://www.strapify.dev/docs/
  - Strapify is a javascript tool for the automatic client side injection of Strapi CMS data into a website.
  - The goal of the Strapify project is to enable the integration of a free open source CMS (Strapi) into an otherwise static website, without requiring additional code

- https://github.com/meetqy/aspoem /AGPLv3/202407/ts
  - https://github.com/meetqy/aspoem/tree/v1/admin
  - https://github.com/meetqy/aspoem-strapi /MIT/202405/ts
  - https://aspoem.com/
  - 现代化诗词学习网站，一个更加注重 UI和阅读体验 的诗词网站
  - https://x.com/meetqy
  - https://github.com/javayhu/haitang /MIT/202407/ts/astro
    - https://haitang.vercel.app/
    - https://haitang.app/
    - 海棠诗社，古诗词的数字桃源
    - 海棠诗社按诗集、朝代、诗人、诗词等方式检索，内容丰富，信息齐全
    - Frontend: Astro + Tailwind + Shadcn/ui
    - Analytics: Umami + Google Analytics
    - Database: SQLite + Drizzle
    - Comment: Giscus
# integrations
- https://github.com/ONLYOFFICE/onlyoffice-strapi /MIT/202211/js/inactive
  - The app which enables the users to edit office documents from Strapi using ONLYOFFICE Document Server, allows multiple users to collaborate in real time and to save back those changes to Strapi
  - Users are able to view, edit, and co-author documents added to the Strapi Media Library.
  - 未使用socket; 协作的逻辑感觉在onlyoffice-server，而不是strapi
  - [Collaborate in Strapi with ONLYOFFICE Docs | ONLYOFFICE Blog _202205](https://www.onlyoffice.com/blog/2022/05/strapi-connector-for-onlyoffice)

- https://github.com/nazirov91/ra-strapi-rest /MIT/202304/ts/inactive
  - React Admin data provider for Strapi.js
  - 旧版支持v3
  - https://github.com/nazirov91/ra-strapi-rest-demo
  - forks
  - https://github.com/szynek99/ra-strapi-rest
    - fix: create & update
  - https://github.com/chris-heney/ra-strapi-rest
    - Fixed ability to parse the field name and operator from the filters 

- https://github.com/garridorafa/ra-strapi-v4-rest /MIT/202403/ts
  - React Admin REST data provider for Strapi.js v4

- https://github.com/marmelab/ra-strapi-demo /202210/前端ts/后端js
  - [Building a B2B app with Strapi and React-Admin_202211](https://marmelab.com/blog/2022/11/28/building-a-crud-app-with-strapi-and-react-admin.html)
  - 依赖strapi.v3、knex、pg、ra-strapi-rest、react-admin.v4

- https://github.com/marmelab/strapi-beerdex /202103/js/v3
  - StrapiJS Example Application For Beer Management
  - [Building A Web Application In 15 Minutes Using StrapiJS And NextJS_202006](https://marmelab.com/blog/2020/06/18/build-an-application-in-fiften-minutes-using-strapijs.html)

- https://github.com/sant3001/ra-strapi-v4-graphql /202310/ts
  - GraphQL Strapi v4 Provider for React Admin.

- https://github.com/kevinadhiguna/antdpro-strapi-auth /202209/ts
  - Implementation of authentication in Ant Design Pro v5 with Strapi API powered by Apollo GraphQL client

- https://github.com/refinedev/refine/tree/master/packages/strapi-v4 /202312/ts
  - [Strapi v4 | refine docs](https://refine.dev/docs/packages/data-providers/strapi-v4/)
  - refine is an open-source, headless React framework for developers building enterprise internal tools, admin panels
  - Strapi is a headless CMS used to develop websites and APIs.
  - refine has connectors for 15+ backend services, including REST API, GraphQL, and popular services like Airtable, Strapi, Supabase, Firebase, and NestJS.
  - [Comparison | Refine vs React-Admin vs AdminBro vs Retool vs Redwood | refine](https://refine.dev/docs/further-readings/comparison/)

- https://github.com/ly525/luban-h5 /202209/js/vue
  - https://ly525.gitee.io/luban-h5
  - 基于Vue2.0开发、通过拖拽快速生成页面的平台，类似易企秀的H5制作、建站工具、可视化搭建系统
  - 后端集成: Strapi.js (官方后端API), SpringBoot2-JPA, SpringBoot2-Mybatis-plus

- https://github.com/Azure-Samples/contoso-real-estate /202312/js
  - Intelligent enterprise-grade reference architecture for JavaScript, featuring OpenAI integration, Azure Developer CLI template and Playwright tests.
  - This repository contains the reference architecture and components for building enterprise-grade modern composable frontends (or micro-frontends) and cloud-native applications. 
  - It is a collection of best practices, architecture patterns, and functional components that can be used to build and deploy modern JavaScript applications to Azure.

- https://github.com/strapi/strapi-plugin-open-ai /202311/js
  - The official plugin that allows you to create Open AI completion from a prompt
  - https://github.com/AsyncWeb/strapi-chatgpt /js
  - https://github.com/thirdrocktechno/strapi-plugin-chatgpt /js
  - https://github.com/strabot/strabot-docs /NonOpen
- https://github.com/malgamves/strapi-open-ai-text-generation /202301/js
  - A Strapi Custom Field to generate text content with Open AI Text generation API

- https://github.com/gabriel-mend/strapi-chat-genius /MIT/202401/ts
  - a plugin for strapi to add the text generation field with the chatgpt api.

- https://github.com/PaulBratslavsky/strapi-plugin-open-ai-embeddings /202308/js
  - Plugin is designed to bridge the gap between your Strapi-managed content and your OpenAI chatbot.
- https://github.com/perzeuss/strapi-plugin-embeddings /202307/ts
  - A Strapi plugin for embedding support, utilizing Chroma as the database for embeddings. Use strapi as your CMS for Embeddings!

- https://github.com/Kcepriu/telegram-bot-strapi /202308/ts
  - Plugin Strapi for sending messages to a Telegram bot.

- https://github.com/am2222/strapi-plugin-postgis /202305/js
  - https://am2222.github.io/strapi-plugin-postgis/
  - Add native postgis support to strapi.
  - Since Strapi does not support native database formats, I convert requests before they being sent to the querybuilder and convert all the geometry objects to the geojson.
- https://github.com/notum-cz/strapi-plugin-location /ts
  - This plugin allows users to create location inputs and store latitude and longitude values as geometry types in a PostGIS database. 
  - It also provides functionality to filter items based on their location.
  - This plugin requires a PostgreSQL database with the PostGIS extension enabled

- https://github.com/meilisearch/strapi-plugin-meilisearch /202312/js
  - A strapi plugin to add your collections to Meilisearch
  - Add your Strapi content-types into a Meilisearch instance. The plugin listens to modifications made on your content-types and updates Meilisearch accordingly.

- https://github.com/geeky-biz/strapi-plugin-elasticsearch /202310/js
  - A plugin to enable integrating Elasticsearch with Strapi CMS.
  - https://github.com/geeky-biz/strapi-integrate-elasticsearch /js

- https://github.com/trieb-work/strapi-neon-tech-db-branches /202307/ts
  - Strapi plugin to connect the neon.tech Postgres database using the neon API

- https://github.com/jclaveau/strapi-provider-upload-google-drive /MIT/202209/js
  - Store your Strapi uploads on Google Drive
  - This plugin is meant to store the content of your medialibrary on Google Drive. While accessed those files are copied locally to avoid massive slow calls on the Google Drive API. This allows to spawn Strapi instances not having persistent storage for free.

- https://github.com/ddlogical/uploads-duplicator /MIT/202312/js
  - This plugin allows you to seamlessly synchronize your Strapi CMS uploads folder with Google Drive. 
  - It utilizes OAuth for secure authorization and provides a straightforward way to automate the backup and storage of your media assets.
  - If you delete files in Media Library, you also should manually delete this files(all versions) on Google Drive
  - To completely delete files in the "uploads" folder, please, restart strapi

- https://github.com/strapi-community/strapi-provider-upload-google-cloud-storage /MIT/202305/js/inactive
  - Google Cloud Storage Upload Provider for Strapi

- https://github.com/jakeFeldman/strapi-provider-upload-azure-storage /202311/ts
  - Strapi Provider Upload Azure Storage
  - Plugin enabling image uploading to azure storage from strapi.

- https://github.com/zoomoid/strapi-provider-upload-aws-s3-advanced /202212/ts
  - extend the S3 Upload Provider to support path prefixes inside a bucket

- https://github.com/hezzze/strapi-provider-upload-oss /202310/js
  - A provider for strapi server to upload file to Aliyun OSS
  - https://github.com/yclgkd/strapi-provider-upload-tencent-cloud-storage /ts

- https://github.com/krishnakairi/strapi-provider-upload-github /202009/js
  - Github/Github-Pages provider for Strapi CMS file upload

- https://github.com/manishkatyan/strapi-stripe /202307/js
  - Stripe Plugin for Strapi CMS

- https://github.com/strapi-community/strapi-plugin-website-builder /MIT/202311/js
  - A plugin for Strapi that provides the ability to trigger website builds manually, periodically or through model events.
  - Trigger builds manually via the strapi admin.
  - Trigger builds periodically through cron jobs.
  - Trigger builds based on content type actions.

- https://github.com/taskworld/strapi-plugin-github-action-dispatch /202311/ts
  - This plugin provides a web ui to trigger a Github workflow run from strapi's admin panel as well as a list of the latest run status and results.

- https://github.com/bass3l/strapi-provider-email-smtp /202204/js
  - A third-party SMTP email provider for Strapi, tested with Gmail SMTP.

- https://github.com/artcoded-net/strapi-plugin-github-projects /202305/js
  - This plugin allows to automatically generate "Projects" from public Github repositories, meant to be then exposed via a public API, e.g. to be shown on a front-end application with the aim to showcase a developer's portfolio. 
  - It is meant mostly for educational purposes, being built step by step in the "Strapi Complete Course" 
  - https://github.com/minhtran241/strapi-plugin-github-projects

- https://github.com/Sur-un-nuage/strapi-plugin-expo-notifications /202312/js
  - plugin that allows a Strapi user to send notifications via the Expo API directly from the Strapi admin panel. 

- https://github.com/localazy/strapi-plugin /202311/js
  - Strapi localization doesn't have to be a headache! 
  - Install the Strapi localization plugin and seamlessly translate your content into multiple languages with Localazy

- https://github.com/SGFGOV/medusa-strapi-repo /MIT/202401/js/ts
  - Monorepo for all Strapi components to sync with medusa

- https://github.com/MarleneJiang/strapi-db /202208/js/vue/inactive
  - 一个专用于Strapi的Restful API查询组件
  - 前端通过组件方式直接获取strapi的接口的数据，并绑定在界面上进行渲染。
  - 有了strapi和strapi-db，就不再需要编写增删查改的接口和前端请求代码，这些工作，只需要一行代码。
  - 灵感主要来自于UniCloudDb

- https://github.com/treblle/treblle-strapi /MIT/202403/js
  - allows Strapi users to use Treblle — a lightweight SDK that helps engineering and product teams build, ship, and maintain REST-based APIs faster.
  - API Monitoring and Observability

- https://github.com/CinquinAndy/notes-to-strapi-export-article-ai /MIT/202404/ts
  - Strapi Exporter: Supercharge Your Obsidian-to-Strapi Workflow, export an obsidian notes directly to your Strapi API
  - a game-changing Obsidian plugin that streamlines your content creation process by seamlessly exporting your notes to Strapi CMS. 
  - With its AI-powered image handling and SEO optimization features, you can take your content to the next level with just a few clicks.
- https://github.com/CinquinAndy/plugin-auto-alt-caption-title-on-images-ai-enhanced /MIT/202404/js
  - A Strapi plugin that automatically generates alternative text (alt), caption, and name for images using AI-powered image analysis. 
  - require An OpenAI API key. You can sign up for an API key at OpenAI.
# plugins
- https://github.com/offset-dev/strapi-calendar /MIT/202311/js
  - Visualize your Strapi content in month, week or daily view
  - select which collection and fields to use

- https://github.com/VirtusLab-Open-Source/strapi-examples /202304/ts/js
  - Strapi plugins usage examples: comments/navigation

- https://github.com/VirtusLab-Open-Source/strapi-plugin-comments /MIT/202402/ts
  - A plugin for Strapi Headless CMS that provides end to end comments feature with their moderation panel, bad words filtering, abuse reporting and much more.
  - Comments can be linked to any of your Content Types by default. Simply, you're controlling it.
  - [New Community Plugin: Content Moderation_202202](https://strapi.io/blog/new-community-plugin-content-moderation)

- https://github.com/luisguve/strapi-plugin-comment-manager /202208/js/inactive
  - Enable and manage comments for your content very easily
  - https://github.com/luisguve/strapi-comments-client
  - https://github.com/luisguve/strapi-comments-client-example
    - showcases how to use the library strapi-comment-client from start to finish, using authenticated users to post comments and a router to group comments on their own pages.

- https://github.com/rixw/strapi-utils /202311/ts
  - A collection of utilities that I've created to make my life easier in working with Strapi.
  - strapi-plugin-search-index: an updated and improved version of Mattie Belt's plugin
  - strapi-provider-search-index-algolia: an updated and improved version of Mattie Belt's provider

- https://github.com/MattieBelt/mattie-strapi-bundle /202202/js/inactive
  - https://mattie-bundle.mattiebelt.com/
  - Mattie plugin bundle for Strapi
  - Search Plugin, Algolia Search Provider

- https://github.com/bn-digital/strapi /202305/ts
  - Additional Strapi plugins, hooks, providers collection
  - Field UUID, Email Emitter, Website

- https://github.com/omomcode/omcommerce /MIT/202403/ts
  - The most customizable and user-friendly ecommerce plugin for Strapi.
  - Seamless integration with a developer-friendly API for any frontend app.
  - Shipping, Taxes, Payment gateway, Analytics

- https://github.com/joshuaellis/strapi-plugin-media-browser /MIT/202304/ts/inactive
  - 🎞️ A new look at what the media library _could be_
  - 上传文件后文件保存在`public/uploads`文件夹
  - 拖拽操作不流畅
  - 只能拖拽上传，没有单独的上传按钮
  - A convenient way to browse, manage and select all your Strapi assets, inspired by MacOS🍎.
  - Support for batch uploads with drag and drop support
  - Tag your assets individually or in bulk
  - Complete control of your folder structure (incl. nested)
  - Virtualized grid for super speedy browsing, even with thousands of assets and tags
  - Refine your search with any combination of search facets such as filtering by tag name, asset usage, file size, orientation
  - https://github.com/kodermax/strapi-plugin-media-api /202311/ts/inactive
  - https://github.com/BaptisteAg/strapi4-ftp-provider /202309/js

- https://github.com/isneezy/strapi-media-preview /202312/ts
  - Automatically generates thumbnails and responsive formats for PDF files upon upload
  - 只生成缩略图却没有使用
  - Create responsive image formats (small, medium, large) for supported files upon upload

- https://github.com/yasudacloud/strapi-plugin-csv-upload /202209/js
  - API calls are made per line, it cannot be rolled back. If drafts are enabled, they will be registered as drafts.
  - https://github.com/afonsobspinto/strapi-plugin-import-csv /202111/js

- https://github.com/reveilleaum/strapi-bulk-operator /202304/js
  - This plugin allows you to create and update multiple entries from .xls or .xlsx file
  - 支持导出导入excel文件

- https://github.com/sat8ndra/import-excel /202311/js/未实现
  - A strapi plugin to import excel bulk import into content of strapi
- https://github.com/vinubabu323/strapi-plugin-excel-export /MIT/202403/js
  - This plugin allows users to generate and download excel files 
  - 使用麻烦但支持配置导出字段
  - 依赖exceljs、react-data-table-component
  - Create an `excel.js` file in the config folder. This file is used to provide tables and columns that need to be in the excel file
  - You can't extract data from dynamic zone or nested components.
  - Relational fields need to be specified in the relation. Currently one level of relation is supported.

- https://github.com/gustomedialab/strapi-csv-export /202304/js
  - plugin csv-export

- https://github.com/weilaiqishi/strapi-upload-big-file /202207/ts
  - 学习一下实现大文件上传
  - 前端: React + Antd, 服务端: Nodejs@16 + strapi

- https://github.com/strapi-community/strapi-plugin-notes /MIT/202402/js
  - A plugin for Strapi Headless CMS that provides the ability to add notes to entity records.
  - a notes section will be added to the `informations` sections of the edit view for all content types.

- https://github.com/remidej/strapi-plugin-todo /MIT/202312/js
  - This plugin adds a todo list next to your content in Strapi. 
  - It makes it easy for admin users to keep track of their content management.

- https://github.com/alexzaganelli/strapi-plugin-email-designer /202312/js
  - Design your own email templates w/ visual composer directly inside the Strapi admin panel and send composed emails programmatically from your controllers / services.
  - 依赖外部embed editor.unlayer.com
- https://github.com/SomeDevelopper/strapi-pdf-designer /202308/js
  - a fork of the Strapi Plugin Email Designer. 
  - It is used to create a single-one-page PDF using drag-and-drop.
  - The plugin return a Buffer in base64.

- https://github.com/vivmagarwal/strapi-plugin-custom-api-builder /202403/js
  - ✨ Build an API Visually from the Admin UI
  - Design your custom API's (or custom reports / or custom views) directly from the Strapi CMS admin panel.
  - Auto compose Routes, Controllers and Services
  - Support for media & multiple media added
  - Support for multiple relationships at the same level added

- https://github.com/priyanshiisingh/React-Form-Strapi /202204/ts/app
  - This form is created using React hook form
  - it accepts user information and uploads it to the strapi database. 
  - It also involves react captcha verification
  - https://github.com/BirinderSingh2410/ReactForm-Strapi

- https://github.com/daandegooijer/strapi-api-forms /202402/ts
  - a plugin for Strapi that allows you to generate API forms with multiple input fields and email handling capabilities.
- https://github.com/dan-micro/Strapi-Form-Builder-plugin /202209/ts
  - Form Builder Plugin
- https://github.com/zekerzichtbaar/formzz /202303/js/inactive
  - a Strapi plugin that allows you to create forms through collection types
  - automatically install input-field components

- https://github.com/nicolashmln/strapi-plugin-oembed /202312/js
  - Embed content from third party sites (Youtube, Vimeo, Tiktok, Soundcloud, Spotify, CodePen...) for https://strapi.io v4 (For strapi v3 use v0.4.0)
  - 需要手改代码 Go to your model and add the `oembed` field
  - The data is fetched and stored in the content
  - Supported: Youtube, Vimeo, Tiktok, Soundcloud, Spotify, CodePen, Twitter

- https://github.com/Ahmed-Adel3/Demo-Next-js-strapi-plasmic /202309/ts/inactive
  - a simple demo for an integration between Next.js, Strapi Headless CMS and Plasmic as a visual page builder
- https://github.com/silexlabs/silex-strapi-11ty /MIT/202403/js
  - a simple example of how to integrate Silex with 11ty and strapi
  - Silex: AGPLv3

- https://github.com/kauedavila/kanban-strapi /202309/js/inactive
  - https://github.com/kauedavila/kanban
  - This is a Next.js project bootstrapped with create-next-app.

## ui-ext

- https://github.com/VirtusLab-Open-Source/strapi-plugin-navigation /MIT/202402/ts
  - 帮助构造树形结构的api，可用于导航菜单等
  - A plugin for Strapi Headless CMS that provides navigation/menu builder feature with their possibility to control the audience and different output structure renderers like (flat, tree and RFR - ready for handling by Redux First Router)

- https://github.com/mattmilburn/strapi-plugin-menus /202312/js
  - A plugin for Strapi CMS to customize the structure of menus and menu items.
  - Consumable menu data which can be used to render navigation
  - Easily manage menus with either a flat or nested structure.

- https://github.com/EsGeh/strapi-plugin-sghp-nav /202310/ts
  - Plugin for Strapi to create, edit and retrieve website navigation structure.
  - Strapi conformant REST API to fetch hierarchical menu data
  - Import/Export of navigation structure via strapis native command line tools

- https://github.com/strapi-fan/strapi-grapesjs-plugin /202309/js
  - provides a custom field for Strapi that lets you use and configure GrapeJs in no time.
- https://github.com/wisdomwebsolution/strapi-grapesjs-plugin /202210/js/inactive
  - Strapi plugin for GrapesJS web builder custom field
  - https://github.com/landofcoder/strapi-pagebuilder /202112/js/GrapesJS
- https://github.com/JensUweB/strapi-plugin-page-builder /MIT/202208/ts/inactive
  - Web page builder for strapi 4.3 or later

- https://github.com/habilelabs/strapi-html-editor /202208/js
  - Presenting an alternative to standard wysiwyg editor in Strapi in the form of this HTML-editor that facilitates easier and hussle-free data customization to use with various frontends.

- https://github.com/surgeharb/strapi-plugin-graphs-builder /202203/js/inactive
  - A plugin for Strapi Headless CMS that provides graphs building tool to generate custom dashboards and reports with the data inside Strapi's database.
  - https://github.com/surgeharb/strapi-plugins

- https://github.com/ef2-digital/strapi-plugin-bold-title-editor /202310/js
  - A bold title/text editor to accentuate certain parts through HTML or Markdown.
  - Different output options: choose between HTML and Markdown.

- https://github.com/konstantinmuenster/strapi-plugin-rich-text /MIT/202402/ts/tiptap2
  - A WYSIWYG editor for your rich text fields
  - This Strapi plugin replaces the Markdown editor with a visual, easy-to-use text editor.
  - 依赖tiptap2、markdown-it
  - The plugin stores the content in `HTML` format. When querying content on the frontend, you can simply render the received HTML string.
- https://github.com/dasmikko/strapi-tiptap-editor /MIT/202303/js/inactive
  - A drop-in replacement for the strapi editor
  - It's build for Strapi v4. It has been tested to work with v4.5.5
- https://github.com/itsrifat/strapi-plugin-blocknote /202402/ts
  - plugin to replace the default markdown editor with BlockNote wysiwyg editor
  - https://github.com/coderdiaz/strapi-novel

- https://github.com/hubertnare/strapi4-wysiwyg-replacement /202202/js
  - change the default WYSIWYG to Quill Editor
  - [How to change the default WYSIWYG in Strapi v4 to Quill Editor_202203](https://strapi.io/blog/how-to-change-the-default-wysiwy-to-quill-editor)
- https://github.com/osadavc/strapi-newsletter /MIT/202206/js/archived
  - a plugin that makes it easy to send newsletters to your users when you publish a post
  - You have two available providers to use: Mailchimp, ConvertKit
  - 依赖react-quill、showdown

- https://github.com/SKLINET/strapi-plugin-tinymce /202304/js
  - Replaces the default Strapi WYSIWYG editor with a customized build of TinyMCE editor.

- https://github.com/ckeditor/strapi-plugin-ckeditor /MIT/202403/js
  - This package provides a custom field for Strapi that lets you use and configure CKEditor in no time.
  - Custom fields are supported since Strapi 4.4+ and offer powerful API to create highly customizable fields.
- https://github.com/nshenderov/strapi-plugin-ckeditor /202303/js
  - Integrates CKEditor 5 into your Strapi project as a fully customizable custom field. (Unofficial integration)
  - Strapi v4.4.0+
  - https://github.com/rajatdangat/strapi-plugin-ckeditor5 /202111/js
- https://github.com/nominedisorder/ckeditor5-build-strapi-wysiwyg-with-style /202307/js
  - Enhanced build of CKEditor 5 to replace default Strapi WYSIWYG editor.
  - Automatically upload Inserted images to Strapi Media Library (thanks to ckeditor5-strapi-upload-plugin)
  - Access Strapi Media Library directly from the editor toolbar
- https://github.com/Roslovets-Inc/strapi-plugin-ckeditor5 /202303/js/v3
  - Replace default Strapi markdown WYSIWYG editor with enhanced build of HTML CKEditor 5
  - Automatic translation of UI into selected in Strapi language (Strapi v3)
  - Strapi v4 (work in progress)
  - https://github.com/Roslovets-Inc/ckeditor5-build-strapi-wysiwyg /202203/js/inactive

- https://github.com/spalz/strapi-plugin-editorjs-field /MIT/202401/ts
  - This code was developed based on the strapi-plugin-react-editorjs
  - Add custom field in collection type or single type
  - This code was developed based on the strapi-plugin-react-editorjs 
- https://github.com/melishev/strapi-plugin-react-editorjs /202209/js/archived
  - Plugin for Strapi Headless CMS, hiding the standard WYSIWYG editor on Editor.js
  - This is the Strapi v4 version of this plugin
  - https://github.com/softkitit/strapi-plugin-react-editorjs /202403/js
    - Fork of unmaintained editorjs for strapi
- https://github.com/GregorSondermeier/strapi-plugin-editorjs /202212/js
  - A Strapi v4 compatible plugin that provides a custom field for Editor.js rich text content

- https://github.com/fagbokforlaget/strapi-plugin-wysiwyg-toastui /202201/js
  - This plugin replaces strapi wysiwyg draft editor with toastui editor.
  - https://github.com/wizcas/strapi-plugin-wysiwyg-tui-editor /js

- https://github.com/floatrx/strapi-wysiwyg-mdxeditor-plugin /202403/js
  - https://mdxeditor.dev/editor/demo
  - This plugin is a WYSIWYG editor for Strapi. It uses the @mdxeditor/editor to provide a rich text editor for Strapi.
  - Allows you to replace default Strapi WYSIWYG editor with a MdxEditor

- https://github.com/kwinyyyc/strapi-plugin-wysiwyg-react-md-editor /MIT/202403/ts
  - This is a strapi rich text editor plugin based on react md editor
  - 源码和预览的分栏视图

- https://github.com/TomaszPilch/strapi-code-editor-custom-field /202308/ts/inactive
  - Code editor plugin for strapi CMS. 
  - It uses the monaco editor (vscode).
  - When you add the plugin you will see two new custom fields. One for javascript (and other languages) and one for json.
  - Editor is using two different types for strapi field. When you select JSON editor it will be `json` type. When you select different language, it will be `text` type.

- https://github.com/mattmilburn/strapi-plugin-preview-button /MIT/202402/js
  - A plugin for Strapi CMS that adds a preview button and live view button to the content manager edit view.
  - Optional column in a collection's list view containing "preview" and "copy link" buttons.
  - https://github.com/danestves/strapi-plugin-preview-content /v3

- https://github.com/its-devtastic/strapi-plugin-previewable /202207/js
  - A plugin for Strapi that embeds your site in Strapi. 
  - The use case for this is to allow content editors to easily enter Preview Mode.

- https://github.com/vinubabu323/strapi-plugin-component-preview /202304/js
  - plugin helps to give a live preview the component we are using
  - 用来给字段添加preview
- https://github.com/abhishek1020N/strapi-plugin-multi-component-preview /202404/js
  - plugin used to view the actual component through a custom field in strapi. This plugin helps to give a live preview the component we are using. 
  - This plugin is based on https://www.npmjs.com/package/strapi-plugin-component-preview

- https://github.com/lautr/strapi-plugin-duplicate-button /202311/js
  - Adds a Duplicate Button to the edit view

- https://github.com/excl-networks/strapi-plugin-ezforms /202312/js
  - This plugin allows you to easily consume forms from your front end and automatically reject spam, send out notifications, and store the data in your database.
  - features like server side form validation and heavy customiztations will most likely never be added to this forms plugin. 
    - If you need something more customized you should look into making a custom controller.

- https://github.com/Zaydme/strapi-plugin-multi-select /MIT/202312/js/inactive
  - A strapi custom field for selecting multiple options from a provided list of items.
  - https://github.com/zaydme/strapi-plugin-multi-country-select /202307/js
    - A strapi custom field for selecting any country based on the ISO 3166-1 country code standard.
  - https://github.com/ChrisEbert/strapi-plugin-country-select /202310/js

- https://github.com/alanzdr/strapi-plugin-dynamic-enumeration-field /MIT/202403/js
  - This plugin adds a new type of enumeration that works like a combobox, where you can get data already registered in the enumeration previously, or add a new item to the select options.
  - New field Dynamic Enumeration appears in admin content-type-builder page, in the custom tab.
  - Works inside Components and Dynamic Zones.

- https://github.com/Freyb/strapi-plugin-content-tags /202306/js
  - A Strapi plugin that allows you to add custom tags to your content.

- https://github.com/canopas/strapi-plugin-tagsinput /MIT/202402/js
  - This plugin is used to add tagsinput in your strapi admin panel. 

- https://github.com/raykeating/strapi-location-field-plugin /202310/js
  - A Strapi plugin to enable a custom location field with autocomplete input

- https://github.com/MattieBelt/strapi-plugin-international-fields /202109/js
  - Strapi plugin that adds international fields with i18n support.

- https://github.com/DanielPantle/strapi-plugin-react-icons /202310/ts
  - plugin for strapi to select react icons
  - Add `react-icon` as custom field to your content type.
- https://github.com/rgomeztinoco/strapi-plugin-heroicons-field /202311/js
  - Strapi plugin. Adds a heroicon picker custom field to your content types. 
  - Don't need to install any frontend library - it returns the SVG code of the icon and the name as a stringified JSON

- https://github.com/play14team/strapi-plugin-map-field /202311/js
  - plugin allows to add a Mapbox map custom field in your content-types.

- https://github.com/BorysShulyak/strapi-plugin-field-formula /MIT/202310/js/inactive
  - A plugin for Strapi Headless CMS that provides an integration with powerful `mathjs` library.
  - Is compatible with JavaScript’s built-in Math library.
  - Calculating the `formula` with the provided `scope` using the powerful `mathjs.evaluate` method.
  - https://github.com/quyen1708/strapi-4-custom-field-math-type /202311/ts
  - https://github.com/UnillanosMath/unillanos-math-strapi /202311/js

- https://github.com/LottieFiles/plugin-strapi /202312/ts
  - A plugin for Strapi CMS, that allows creating a custom input field for adding lottie animations seamlessly via `LottieFiles` public animation repository.
  - Custom field creation in Strapi models
  - Keyword based search

- https://github.com/am2222/strapi-custom-fields /202205/js/inactive
  - Adds different field renderers to the strapi admin page.
  - ColorPicker Field

- https://github.com/Studio-Parkers/strapi-datetimepicker /202310/ts
  - A user-friendly alternative for Strapi's build-in datetime picker
  - For now only supports English (not American/Simplified English) date format
- https://github.com/everythinginjs/strapi-better-datepicker /202312/ts
  - A quick description of strapi-better-datepicker.

- https://github.com/muammerkeles/strapi-date-range-picker-plugin /202312/js
  - Custom Date Range Picker field for Strapi admin

- https://github.com/play14team/strapi-plugin-timezone-select /202303/js
  - A strapi custom field for selecting any timezone based on the moment.js timezones.

- https://github.com/boazpoolman/strapi-code-themes /202207/ts
  - Some IDE inspired color schemes for Strapi v4 admin UI

- https://github.com/Gaylord-Julien/strapi-plugin-qrcode-generator /202311/js
  - plugin that allows you to generate QR Codes based on specific fields or generate QR Codes with Rest API.
  - Adds a button to the content manager that allows users to generate a qr code.
  - Output svg qr code with rest api parameters.

- https://github.com/WalkingPizza/strapi-plugin-placeholder /202305/js
  - Serve placeholders with your Strapi images
  - Generate base64 placeholders for Strapi images.

- https://github.com/emil-petras/strapi-blurhash /202304/js
  - A plugin for Strapi CMS that generates blurhash for your uploaded images
- https://github.com/viktordanov/strapi-thumbhash /202306/js
  -  a fork of Strapi blurhash to implement the superior Thumbhash
- https://github.com/akhmadshin/strapi-plugin-thumbhash /202311/js
  - A plugin for Strapi CMS that generates thumbhash for your uploaded images
  - [ThumbHash: A very compact representation of an image placeholder](https://evanw.github.io/thumbhash/)

- https://github.com/nicolashmln/strapi-plugin-responsive-image /202312/js
  - Custom responsive image formats for https://strapi.io v4 (For strapi v3 use v0.5.0)

- https://github.com/strapi-community/strapi-plugin-local-image-sharp /202307/js
  - Dynamically resize, format and optimize images based on url modifiers.
  - Convert any uploaded images with local provider using sharp modifier. 
  - No extra configuration needed, the modifiers will be applied based on the url.

- https://github.com/marlokessler/strapi-plugin-image-optimizer /202307/ts
  - Optimize your images for desktop, tablet and mobile and different image formats.
  - This plugin uses sharp provided via strapi core. 

- https://github.com/kwinyyyc/strapi-plugin-zeasy-image-api /202101/js
  - helps you to search for images on Unsplash and Giphy, import it to your media library and insert to your Rich Text content with appropriate attribution.

- https://github.com/quiloos39/next-strapi-image-loader /202306/ts
  - This custom image loader seamlessly integrates Strapi apps with Next.js, handling image optimization through Strapi.

- https://github.com/akcyp/strapi-plugin-point-list /202210/ts
  - A plugin for Strapi CMS that provides point list field (when drawing on image)

- https://github.com/darron1217/strapi-plugin-video-thumbnail /202203/js
  - Video thumbnail plugin for Strapi

- https://github.com/SKLINET/strapi-plugin-video-field /202304/js
  - This plugin adds custom video field into your Strapi application 
  - Plugin currently supports YouTube, Vimeo, and Facebook videos.

- https://github.com/apivideo/api.video-strapi-plugin /202310/ts
  - A Strapi plugin for managing uploads to api.video.
  - Upload videos using a file to api.video inside of Strapi
  - Manage assets with the plugin's asset grid and pagination capabilities
  - Preview content using our player (powered by the api.video-player-react package)

- https://github.com/flyce/strapi-provider-upload-minio-ce /202307/js
  - This upload provider uses the JavaScript Minio. Client to upload files to a (self hosted) instance of Minio.
  - https://github.com/ericCHxia/strapi-provider-upload-minio /202312/ts
- https://github.com/isuvorov/strapi-provider-upload-ts-minio /202207/js/v3
  - This upload provider for Strapi uses the JavaScript Minio. Client to upload files to a (self hosted) instance of Minio.
  - It's compatible with the the strapi 3.1.1.

- https://github.com/Studio123ca/strapi-plugin-image-color-palette /202304/js
  - plugin that extends image uploads to generate and attach a color palette to the schema when uploaded.
  - It uses GraphicsMagick to extract the colors from the image after it's uploaded, and stores them in the database schema. 

- https://github.com/alexkainzinger/strapi-middleware-upload-plugin-cache /202208/js/inactive
  - Adds middleware for caching uploaded assets when using strapi-provider-upload-local

- https://github.com/andreciornavei/strapi-provider-upload-local-url /202201/js
  - This provider reflects the strapi-provider-upload-local but with an additional option to set the `baseurl` on upload url data as prefix.

- https://github.com/alexbakers/strapi-provider-upload-ipfs-storage /202301/js
  - IPFS (Filebase, Pinata, Fleek, Web3, Lighthouse) provider for Strapi uploads.

- https://github.com/fabimc/strapi-provider-upload-ftp /202208/js
  - FTP provider for Strapi v4 file upload.
  - https://github.com/mmattosr/strapi-provider-upload-sftp /202002/js

- https://github.com/SannadB/strapi-drag-drop /202212/js/inactive
  - this plugin adds a panel, which allow sort content via drag-and-drop. This is not a very intuitive way

## features-ext

- https://github.com/obafunmiso-olufemi/strapi-plugin-review-workflow /202401/ts/wip
  - workflow

- https://github.com/notum-cz/strapi-plugin-content-versioning /117Star/MIT/202403/js/deprecated
  - This plugin enables content versioning in Strapi
  - Enables you to have multiple draft versions
  - Keeps a history of all changes, providing the ability to time travel (revert back to previous versions).
  - 🐛 实现原理是每次update都create新的entry插入到对应表，disable本插件会导致数据被污染，但可通过额外字段区分有效数据
  - Gives you the ability to have different published and draft data
  - Does not work well with GraphQL
  - Not working with UID and unique fields
  - With Strapi version 5 introducing support for draft content versions, the majority of features offered by this plugin repository will become available as core features. 
  - [Advanced Strapi Enhancement: Notum's Open-Source Plugins_202312](https://strapi.io/blog/elevating-strapi-notum-s-journey-in-creating-three-open-source-plugins)
    - the plugin still has some limitations like the inability to support unique fields and relations inside components
    - 🧐 the entities are still stored in the same database table but each of them is assigned a unique versioning identifier and a link to relevant locale.
    - one of the most challenging parts derives from the fact that when the content has multiple locales and each locale has multiple versions

- https://github.com/PenguinOfWar/strapi-plugin-paper-trail /MIT/202402/js
  - Accountability and content versioning for strapi v4+
  - ⌛️ Automatic revision history and auditing with support for all major strapi content types including relations, media, components, and dynamic zones via the admin panel.
  - Support for collection and single content types
  - Roll-back capabilities with the option to select specific fields to restore via the admin panel.
  - Tracks revision history by both admins and users.
  - the plugin will differentiate `CREATE` from `UPDATE` and will display which user made the change
  - Internationalization (i18n) plugin support.
  - The plugin relies on the content type plugin `UID` property to identify the correct content type and associate the revision history. 
  - 🧐 The plugin is a middleware listening on the admin and user content management endpoints. Making changes directly to the records outside of this scope (e.g. from a custom service or controller) will not be logged as a revision by the plugin, however it shouldn't be difficult to manually implement it
  - `password` type is not supported for security reasons.
  - roadmap
    - Better support for only logging changed fields (currently the strapi admin sends the entire record back and not just the changes fields) to reduce revision noise
    - Plugin management panel for purging revision history.
  - https://github.com/JoeriDamme/strapi-plugin-revisions /v3-only

- https://github.com/strapi-community/strapi-plugin-audit /MIT/202208/js/inactive
  - Audit Log plugin for Strapi v4
  - One of this package's co-maintainers is an employee of Strapi however this package is not officially maintained by Strapi

- https://github.com/Marje3PSUT/strapi-plugin-audit-log-marje3 /202309/js/inactive
  - A plugin that logs all user interactions, fully-equipped with permissions and settings.
  - This plugin aims to store all user interactions as logs that can be accessed easily and securely through the use of permissions.

- https://github.com/NarKarapetyan93/strapi-audit-log /202307/ts/inactive
  - This plugin allows you to log all the actions performed by the users
  - For external changes if ctx.state.user is empty, it shows "External Change" instead of user name.
  - This plugin only visible for users with Super Admin role. However, you can give access to other users

- https://github.com/10Life/strapi-plugin-audit-trail /MIT/202401/js
  - A comprehensive audit trail plugin for Strapi that tracks user activities.
  - This plugin utilizes a middleware to create an audit log of user activities. 
  - The audit log is accessible in the `Audit Trail` content type. The admin page provides a functionality to clear audit trails.

- https://github.com/Madde22/strapi-plugin-audit-history /202310/js/inactive
  - A plugin to log all the changes made to the content-types. 
  - It will log the following actions: before create/update/delete
- https://github.com/jeremyProwseYS/strapi-audit-logs /202302/js/inactive
  - Plugin that adds very basic audit functionality to strapi sites.

- https://github.com/antokhio/strapi-plugin-categorizer /202308/ts
  - A plugin that lets you categorize content quickly.
  - supports multiple categorizer fields per collection
  - feature: multiple categorizers on one target*

- https://github.com/luisguve/strapi-plugin-ratings /202211/js
  - Strapi plugin to enable and manage reviews for your content
  - Reviews can be displayed in the frontend in two ways: 
    - Using the React components library strapi-ratings-client (recommended)
    - Build your custom frontend using the API endpoints
  - https://github.com/luisguve/strapi-ratings-client

- https://github.com/VirtusLab-Open-Source/strapi-plugin-reactions /202311/ts
  - A plugin for Strapi that provides flexible & configurable reactions experience to any Content Types.
  - Reactions can be used to any of your Content Types without any special configuration.

- https://github.com/Cogitoergo/strapi-voting /202311/js
  - A plugin for Strapi Headless CMS that provides a simple voting system together with a moderation panel and logs.
  - Search and filter through the logs and see various voting statistics.

- https://github.com/DomDew/strapi-plugin-fuzzy-search /MIT/202403/ts
  - Register a weighted fuzzy search endpoint for Strapi
  - Uses `fuzzysort` under the hood: Simple, quick and easy. No need to worry about setting up an instance for a complex search engine.
  - Since we had issues with `Fuse.js` and it's underlying algorithm, we opted for `fuzzysearch` to do the heavy lifting instead.
  - https://github.com/farzher/fuzzysort /202211/js

- https://github.com/strapi-community/strapi-plugin-search /MIT/202310/ts
  - A Strapi CMS plugin that provides search engine agnostic sync support
  - Coming soon

- https://github.com/pdalvi1893/strapi-global-search /202309/js
  - Working on Strapi version: v4.0.3
  - Support JSON export & import
  - Include the following lines to allows large excel imports in middelware.js

- https://github.com/pdalvi1893/strapi-indexed-search-multilingual /202403/js
  - Simple search plugin

- https://github.com/wizbii/strapi-plugin-strapi-algolia /202404/ts
  - A strapi plugin that index items to algolia

- https://github.com/strapi/strapi-plugin-seo /202311/js
  - The official plugin to make your Strapi content SEO friendly
  - Manage the important tags for your SEO (metatitle, metadescription) and preview your content in the SERP
  - Manage your meta social tags (Facebook & Twitter) and preview your post.
  - https://github.com/Oak-Digital/nextjs-strapi-plugin-seo
    - Nextjs component for adding head tags from [strapi-plugin-seo]

- https://github.com/ExFabrica/strapi-plugin-awesome-seo /202309/js
  - Awesome SEO allows your content manager in one click to get the results of your website SEO analysis directly available in Strapi.

- https://github.com/strapi-community/strapi-plugin-rest-cache /105Star/MIT/202310/js
  - https://strapi-community.github.io/strapi-plugin-rest-cache/
  - This plugin provide a way to cache HTTP requests in order to improve performance. 
  - It's get inspired by varnish cache which is a popular caching solution.
  - The cache content is stored by a provider, which can be either an `in-memory` provider, a `redis` connection, a `filesystem`, or any other custom provider. 
  - You can set a strategy to tell what to cache and how much time responses should be cached. The cache will be invalidated when the related Content-Type is updated, so you never have to worry about stale data.

- https://github.com/strapi-community/strapi-plugin-redis /202303/js
  - Plugin used to centralize management of Redis connections in Strapi

- https://github.com/10Life/strapi-plugin-advanced-cache-manager /202312/js
  - This plugin allows Strapi users to invalidate the cache according to the cache time defined in the plugin options. Besides, it also provides a way for users to clear AWS CDN cache.

- https://github.com/msoler75/strapi4author /202206/js
  - I made this example to show a policy/middleware/controller to manage ownership of content.

- https://github.com/boazpoolman/strapi-plugin-sitemap /202312/js
  - Generate a highly customizable sitemap XML in Strapi CMS

- https://github.com/kucherenko/strapi-plugin-passwordless /202312/js
  - A plugin for Strapi Headless CMS that provides ability to sign-in/sign-up to an application by link had sent to email. 
  - A plugin works together with Strapi User Permissions Plugin and extends it functionality. 
  - For working with emails a plugin use Strapi Email Plugin.

- https://github.com/arellaTV/strapi-plugin-invite-email /202209/js
  - A plugin for Strapi that sends a templated email with a magic link whenever an admin user is invited.

- https://github.com/devwithmaya/strapi-plugin-emailing /202308/ts
  - A plugin for Strapi Headless CMS that provides end to end emailing feature with their moderation panel, usable for notifications, newsletter, custom email compose…

- https://github.com/colibris-xyz/strapi-plugin-site-publisher /202312/js
  - a plugin for Strapi headless CMS. 
  - It lets you trigger a GitHub Action workflow when the site is ready to be published.

- https://github.com/ComfortablyCoding/strapi-plugin-publisher /202311/js
  - A plugin for Strapi that provides the ability to easily schedule publishing and unpublishing of any content type.

- https://github.com/NovaGaia/strapi-plugin-generic-publisher /202307/js
  - A flexible and generic plugin for triggering publications on multiple instances and hosting
  - Allows you to publish to multiple instances (Prod, Preview, etc.); 
  - Adds a publishing component to override Strapi's state management, useful with CRON in particular (no obligation to use); 

- https://github.com/phantomstudios/strapi-plugin-github-publish /202211/js
  - This is a plugin for Strapi headless CMS. It lets you trigger a GitHub Action workflow when the site is ready to be published.
- https://github.com/everythinginjs/strapi-plugin-update-static-content /202306/js
  - An Strapi plugin for rebuilding and deploying your static website via Github Actions.

- https://github.com/webbio/strapi-plugin-scheduler /202308/ts
  - Strapi Plugin to schedule publish and depublish actions for any collection type.
  - Schedule when you want to publish your content

- https://github.com/innovato/strapi-plugin-cron /202402/ts
  - Manage and monitor cron jobs from Strapi admin panel.
  - tasks scheduling tool incorporating start/end dates and iterations counter

- https://github.com/excl-networks/strapi-plugin-redcron /MIT/202311/js/inactive
  - A drop in replacement for the Strapi cron plugin that uses Redlock to prevent multiple instances of Strapi from running the same cron job at the same time.

- https://github.com/Fekide/strapi-plugin-translate /202311/js
  - https://market.strapi.io/plugins/strapi-plugin-translate
  - Strapi plugin for automated translations using different Translate Providers
- https://github.com/manishkatyan/strapi-google-translator /202301/js
  - Translate Strapi collections into multiple languages using Google Cloud Translation
- https://github.com/shawnvogt/strapi-provider-translate-gct /202211/js
  - Google Cloud Translate provider for Strapi Translate Plugin

- https://github.com/Braunmann/strapi-provider-translate-chatgpt /202304/ts
  - ChatGPT provider for translate plugin in Strapi 4

- https://github.com/Webbist-dev/strapi-redirects /202307/js
  - This plugin allows a user to manage redirects from the admin panel.
  - Inside this plugin you can add redirects, each redirect requires the following fields `[to, from, type]`.

- https://github.com/pluginpal/strapi-webtools /MIT/202403/ts
  - https://www.pluginpal.io/plugin/webtools
  - Unique, flexible and autogenerated URLs for your Strapi managed web content.
  - Unique URLs: Every page will get their own unique path
  - Auto slugify: The URLs will automatically be slugified to ensure valid paths

- https://github.com/ComfortablyCoding/strapi-plugin-slugify /202310/js
  - A plugin for Strapi Headless CMS that provides the ability to auto slugify a field for any content type.
  - It also provides a findOne by slug endpoint as a utility.

- https://github.com/anastasiiaxfr/strapi-plugin-field-slug /202303/js
  - This plugin adds a Slug field to Strapi. 
  - Slug has autocomplete default generated value in format: post-year-month-day-hours-minutes-seconds, same for all locales.
  - Also we can add KeyWord and/or pattern, which will be used to generate slug.

- https://github.com/strapi-community/strapi-plugin-url-alias /202312/ts
  - Unique, flexible and autogenerated URL aliases for your Strapi managed web content.
  - Automatically generated based on a pattern
  - Public endpoint Get your page by path with the /get endpoint
  - Auto slugify The URLs will automatically be slugified to ensure valid paths

- https://github.com/lachoseparis/lachose-strapi-plugins /202307/js
  - strapi-plugin-custom-links: A plugin to enable cross content-types URI

- https://github.com/x3m-group/strapi-plugin-auto-links /202307/ts
  - A plugin for Strapi that auto generate links for resources (self, canonical, alternates, ...)

- https://github.com/kmertozen/strapi-cdn-prefix /202308/js
  - plugin allows you to automatically prepend a CDN link to your image URLs on both Admin Panel and API's.

- https://github.com/mattmilburn/strapi-plugin-permalinks /202311/js
  - A plugin for Strapi CMS to enable a URL path field for content types with nested relationships.
  - Use a custom field to manage a chain of URL paths to build a unique permalink.
  - Customize which content types should use permalinks.
  - Parent/child relations can use different collection types.
  - Child relations automatically sync when parents change.

- https://github.com/webbio/strapi-plugin-internal-links /202311/ts
  - wip

- https://github.com/Webbist-dev/strapi-redirects /MIT/202404/js
  - This plugin provides a convenient way to manage URL redirects within a dedicated collection type in Strapi
  - While it does not automatically handle redirects on the server side, it offers a structured endpoint from which frontend applications can fetch redirect rules and implement redirection logic as needed.
  - Redirects are made available through the `api/redirects` endpoint as a JSON object. This endpoint is accessible to authenticated users

- https://github.com/Edwin-Luijten/strapi-encryptable-field /202310/ts
  - Encrypts values on save, and decrypts on fetch.

- https://github.com/minzig/strapi-plugin-init-admin-user /202311/js
  - Creates a strapi admin user on startup. 
  - Simplifies working with multiple strapi environments.
- https://github.com/sunnysonx/strapi-plugin-bootstrap-admin-user /202012/js
  - Automatically creates an admin user in development mode.

- https://github.com/Fekide/strapi-plugin-impersonation /202308/js
  - This plugin allows all admin users with sufficient permissions to impersonate(扮演，饰演) any user on your site! So use it with caution!

- https://github.com/beyowi/strapi-plugin-content-moderation /202303/js
  - This plugin enables your team to moderate other users' new content entries for any of your content types and also users.
  - Permissions: Add administrators and control which role can set content pending for moderation

- https://github.com/BretCameron/strapi-plugin-public-permissions /202309/ts
  - A plugin to automate the creation of public permissions for your chosen API content types and plugins.

- https://github.com/gravitybv/strapi-plugin-permissions /202307/js
  - Permissions plugin for Strapi v4 - Permissions by config file
  - https://github.com/PaulBratslavsky/strapi-example-user-permissions-policy /wip

- https://github.com/PaulRichez/strapi4-plugin-route-permission /202310/js
  - Strapi4 plugin server route permission
  - A plugin for Strapi that provides the ability to config roles on server route for generate permissions.

- https://github.com/andreciornavei/strapi-plugin-route-permission /202205/js
  - This plugin implements a simple way to seed strapi permission::users-permissions table from routes configuration. 
  - It means that you can define your routes permissions direcly on yours routes.json files.

- https://github.com/strapi-community/strapi-plugin-protected-populate /MIT/202403/js
  - The purpose of this plugin is to have a easy way to protect your get endpoints from getting to much information out of them. I made this plugin since I got sick and tired of writing complex policies to do this exact thing.
  - Protected your Get request populates and fields

- https://github.com/eigengrau-ch/strapi-plugin-cookie-manager /202309/js
  - Manage categorized cookies directly within the Strapi CMS admin panel at one place and use the predefined plugin API to provide GDPR consent cookies.

- https://github.com/bwyx/strapi-jwt-cookies /202301/js
  - Securely use users-permissions's JWT on cookies. Compatible with Strapi v4 and requires @strapi/plugin-users-permissions

- https://github.com/olyphotographer/strapi-refresh-tokens /202202/js
  - Strapi V4 with refresh tokens/cookies
- https://github.com/Marienoir/Strapi-Refresh-Token-v4 /202302/js/vue
  - Strapi-Refresh-Token-v4

- https://github.com/arjusmoon860/strapi-google-auth /202310/js
  - GoogleAuth helps you to easily create google authentication available for your users. 
  - It uses the official `google-auth` library to execute the actions. You can get it working in under 2 minutes in your application.

- https://github.com/mancku/Strapi-custom-sendEmailConfirmation-workflow /202210/js
  - Re-doing the register method with almost a copy-paste to be able to call your own sendConfirmationEmail method that can be (again) almost a copy-paste but getting the URL from the environment
  - [How to configure email confirmation redirection URL dynamically?_202210](https://forum.strapi.io/t/how-to-configure-email-confirmation-redirection-url-dynamically/22671)

- https://github.com/vaxr/strapi-provider-email-mock /202305/js
  - A simple in-memory mock mail provider for strapi.io

- https://github.com/bztes/strapi-provider-email-gmail-api /202307/js
  - Yet another Strapi email provider for Gmail using OAuth 2.0

- https://github.com/wfzong/strapi-wechat-miniprogram-auth /202303/js
  - WeChat MiniProgram Auth helps you to easily create WeChat MiniProgram authentication available for your user. 
  - It uses the official USER LOGIN REQUEST to get the authorization, you can get it working in under 5 minutes in your WeChat MiniProgram application.

- https://github.com/wave909/strapi-auth-extensions /202206/js
  - Plugins for TFA, SMS, magic links in Strapi

- https://github.com/yasudacloud/strapi-plugin-sso /202401/js
  - This plugin can provide single sign-on.
  - You will be able to log in to the administration screen using one of the following providers: Google, Cognito, Azure, OIDC
- https://github.com/chordata-insight/strapi-plugin-sso /202305/js
  - The plugin provides single sign-on for strapi >=4.
  - Makes possible to login strapi via oauth provider, currently only implemented for keycloak

- https://github.com/dej10/strapi-plugin-file-system /202312/js
  - a plugin for Strapi that provides endpoints to interact with the media library, allowing you to retrieve folders and files

- https://github.com/ChristopheCVB/strapi-plugin-soft-delete /202312/ts
  - Powerful Strapi based Soft Delete feature, never loose content again

- https://github.com/mattmilburn/strapi-plugin-do-not-delete /202311/js
  - A plugin for Strapi CMS that protects certain entries from being deleted.
  - Use various comparators to match against protection rules.

- https://github.com/pakoc/strapi-plugin-html-media /202402/ts
  - Plugin provides a customField that allows you to upload zip archives with html pages to the Strapi CMS
  - These zip archives contain mini web applications with an index.html launch file
  - Upon uploading a mini application archive, the server unpacks the archive and saves information about it in a separate table called html-media in the database.

## utils-ext

- https://github.com/strapi-community/strapi-plugin-multitenancy /202311/js
  - COMING SOON

- https://github.com/anetaj/strapi-plugin-multi-tenant /202303/js
  - A Strapi plugin to make Strapi a full-fledged backend for your SaaS
  - Have multiple SaaS customers use the same Strapi instance.
  - Isolate content per organization or, more granularly, per user group.
  - The plugin adds `Organization` and `UserGroup` content types. Also, it provides middleware and policies that keep data isolated between tenants.
  - https://github.com/SVronskiy/strapi-plugin-multi-tenant-example /202305/js
  - https://github.com/bikramkawan/strapi-multitenancy-v4 /202302/js

- https://github.com/smoothdvd/strapi-plugin-bull /MIT/202401/ts
  - strapi-plugin-bull

- https://github.com/WGR-SA/strapi-plugin-collection-tree /MIT/202402/ts
  - Plugin allows for simple sorting of your collections. 
  - It incorporates a view that lets you easily drag and drop your items, supporting nested compatibility.
  - Go to the Collection Tree page, select the collection you wish to sort, and use drag and drop to arrange items. Remember to save your changes

- https://github.com/plantagoIT/strapi-drag-drop-content-type-plugin /202402/js
  - plugin that provides a drag and droppable menu for ordering content types in a somewhat userfriendly way

- https://github.com/ShahriarKh/strapi-content-type-explorer /MIT/202401/js
  - plugin that visualizes your content types and their relationships like an ERD (Entity Relationship Diagram).

- https://github.com/node-vision/strapi-plugin-entity-relationship-chart /202310/js
  - Strapi Plugin displays Entity Relationship Diagram of all models, fields and relations.
  - this plugin was tested with stable Strapi - 4.0.6

- https://github.com/pluginpal/strapi-plugin-config-sync /MIT/202401/js
  - CLI & GUI for continuous migration of config data across environments
  - This plugin is a multi-purpose tool to manage your Strapi database records through JSON files. Mostly used to version control config data for automated deployment, automated tests

- https://github.com/TonyDeplanque/strapi-plugin-migrations /202309/js
  - If you want to initialize or update automatically your data in Strapi for all of your environments, this plugin is made for you.

- https://github.com/Baboo7/strapi-plugin-import-export-entries /202312/js
  - Import/Export data from and to your database in just few clicks.
  - Import/Export data directly from the Content Manager
  - Control which roles can import/export data from the admin UI.
  - https://github.com/jbeuckm/strapi-plugin-import-content /v3

- https://github.com/UIGStudio/strapi-plugin-export-import-form /202210/ts
  - Export/import plugin that works entirely on client side. 
  - Supports single types, copying media, matching page relations and locales.

- https://github.com/NovaGaia/strapi-plugin-mock-datas /202310/js
  - This plugin aims to temporarily replace API responses with full mocks

- https://github.com/ARTM2000/x-openapi-document /202309/ts
  - This project created to make documentation automate as possible, in addition to improving developers experience who will work with these services.
  - Strapi (v4), Nextjs (v13)

- https://github.com/Barelydead/strapi-plugin-populate-deep /202311/js
  - This plugin allows for easier population of deep content structures using the rest API.
  - The default max depth is 5 levels deep.
  - The populate deep option is available for all collections and single types using the findOne and findMany methods.

- https://github.com/ComfortablyCoding/strapi-plugin-transformer /202309/js
  - A plugin for Strapi that provides the ability to transform the API request and/or response.
  - GraphQL is not supported

- https://github.com/antokhio/strapi-plugin-untransform-response /202310/ts
  - Efficiently removes all the unnecessary data/attributes tags.

- https://github.com/mattmilburn/strapi-plugin-snippets /202311/js
  - A plugin for Strapi CMS that populates custom snippets into API response data.
  - Create variables to use throughout your content, which are replaced in API response data.
  - Supports API models, plugin models, components, and dynamic zones.

- https://github.com/Eomm/fastify-raw-body /202311/ts
  - Adds the raw body to the Fastify request object.

- https://github.com/MaksZhukov/strapi-plugin-generate-data /202310/ts
  - This plugin is for generating data for your content-types.
  - It supports only string with RegExp pattern, email, richtext, integer, decimal, date, media(videos, images, audios, files), boolean enumeration, password, UID, relation, json fields of your content types.
  - It creates content in draft if the content type has draft & publish option

- https://github.com/Four-Lights-NL/strapi-plugin-deepcopy /202312/ts
  - A strapi plugin providing a deep copy functionality for nested entities.
  - The default behaviour in Strapi is to create a shallow copy when duplicating an entity. This means that any relations are lost and have to be duplicated separately and connected manually to the newly created entities.

- https://github.com/Freyb/strapi-plugin-copy-component /202306/js
  - A Strapi plugin that allows you to copy components from another entity.

- https://github.com/boazpoolman/strapi-plugin-config-sync /202312/js
  - CLI & GUI for continuous migration of config data across environments
  - This plugin is a multi-purpose tool to manage your Strapi database records through JSON files. 
  - Mostly used to version control config data for automated deployment, automated tests and data sharing for collaboration purposes.

- https://github.com/mancku/strapi-plugin-schemas-to-ts /202312/ts
  - plugin for Strapi v4 that automatically converts your Strapi schemas into Typescript interfaces.

- https://github.com/excl-networks/strapi-plugin-generate-schema /202206/js
  - A plugin to dynamically map your database to a Schema.org JSON-LD schema. 
  - When you access your collection row with a specific query parameter (i.e `?schemaOrg=true`), it will add the json-ld for that data.
  - After you have mapped your fields you can add the `?schemaOrg=true` query parameter to your collection row to generate the json-ld for that row.

- https://github.com/Palmabit-IT/strapi-app-version /202211/js
  - plugin for Strapi 4 to show the app version from package.json in the Settings page.

- https://github.com/SotaProject/rss-feed /202208/js
  - This plugin will help you create RSS feed from your data in strapi

- https://github.com/Oak-Digital/strapi-plugin-revalidator /202308/ts
  - This plugin is meant to create webhooks, but specifically for cache invalidations or page revalidations of your frontend applications.
  - This plugin is meant to create webhooks, but specifically for cache invalidations or page revalidations of your frontend applications.

- https://github.com/DudiKaplan/strapi-plugin-revalidate-button /202308/js
  - The plugin comes as a solution to the problem that Webhook does not have a solution for a manual run, and we want to allow the user to first check his content in Preview.
  - The button takes the link from Strapi's webhooks. You must add a line in the webhooks called Revalidate. Our recommendation is to enable the trigger of the Webhooks only to perform Publish or Unpublish.

- https://github.com/adebayohountondji/strapi-plugin-backup /202311/js
  - Automate the backup of uploads and database to the cloud.
  - Database backup
  - Uploads files backup

- https://github.com/thetribeio/strapi-plugin-export /202307/js
  - A plugin that allows to export collection-types and single-types with the option to provide specific formatting for the fields. 
  - Add permissions & roles
  - Use list view filters in exported data like created_at range, order by, etc.

- https://github.com/PaulBratslavsky/strapi-show-plugin /202212/js/inactive
  - Shows list of middlewares, policies, controllers, services

- https://github.com/Dulajdeshan/strapi-advanced-uuid /MIT/202402/ts
  - plugin for Strapi that automatically generates a unique UUID for your content. 
  - It also allows you to generate UUID based on your regular expressions.

- https://github.com/soranoo/strapi-ulid /MIT/202404/ts
  - This plugin adds support for ULID field type to Strapi as a Custom field. 
  - The field will be automatically generated when creating a new entry.
  - This plugin is inspired and based on strapi-auto-uuid by Cringe Studio.

- https://github.com/Cringe-Studio/strapi-auto-uuid /202306/ts
  - Custom field plugin to automatically add manage uuid for your content types, inspired by @strapi-plugin-field-uuid

- https://github.com/taskworld/strapi-plugin-import-export-web /202311/ts
  - This plugin provides a web ui for the strapi import and strapi export commands, so that you can backup/restore your strapi easily.

- https://github.com/skynettechnologies/strapi-plugin-all-in-one-accessibility /202402/js
  - https://www.skynettechnologies.com/all-in-one-accessibility
  - Website accessibility widget for improving WCAG 2.0, 2.1, 2.2 and ADA compliance!

- https://github.com/x-team/strapi-plugin-webhooks /202308/js/inactive
  - A slightly better version of strapi's built-in webhooks.

## themes

- https://github.com/ShahriarKh/strapi-admin-tailwind-theme /202308/js/inactive
  - This extension replaces Strapi Design System colors with Tailwind colors.

## v3-ext

- https://github.com/uwizy/strapi-plugin-webpage-builder /MIT/202006/js
  - Add GrapesJS builder to your own strapi application

- https://github.com/autom8-apps/strapi--form-builder /202009/js
  - form-builder

- https://github.com/alan2207/strapi-plugin-sync-roles-permissions /202107/js
  - Store user roles and permissions configuration as a JSON file and then import and reuse it any time.

- https://github.com/8byr0/strapi-plugin-backup-restore /202112/js
  - Plugin to backup & restore your strapi installation (database + uploads) from admin panel.
  - Compatibility with strapi v4 is not available (only v3 is currently supported)

- https://github.com/Radrw/strapi-pro /201802/js
  - Strapi.io with image upload, location, wysiwyg input

- https://github.com/alexdevmotion/strapi-faker /202008/js
  - Fill your strapi models with faker.js
# starter
- https://github.com/timelessco/strapi-ts-monorepo /MIT/202307/ts/inactive
  - StrapiCMS-focused monorepo concepts, tips and strategies
  - 仅模版，无业务案例

- https://github.com/samMeow/strapi-v4-custom-field-example /202206/js
  - a demo for creating a custom field in content manager in admin panel, but it doesnt cover changing underlying DB structure.

- https://github.com/strapi-community/strapi-tool-dockerize /202311/js
  - Easy add support for docker to your strapi project
  - https://github.com/strapi-community/strapi-tool-deployify
    - Easily deploy a Strapi Project to cloud platforms 
    - Automatic - Creating apps, databases, setting up env variables

- https://github.com/naskio/docker-strapi /202312/shell
  - Docker image for strapi version 4 
  - https://github.com/strapi/strapi-docker /202208/js/v3/inactive

- https://github.com/tldr-devops/startpack /yml
  - Selfhosted tech starter pack for development of new project or startup
  - This is a basic setup of services for faster startup development. You can run it via docker-compose or docker swarm.

- https://github.com/ExFabrica/strapi-plugin-awesome-help /202309/js
  - This plugin enable creation of contextual helps for your Strapi documents
  - [A Strapi V4 plugin from scratch to production | by exFabrica | Medium](https://medium.com/@exfabrica/a-strapi-v4-plugin-from-scratch-to-production-a6deeaf553de)

- https://github.com/strapi/strapi-next-14-dashboard-demo /202311/ts
  - Next 14 and Strapi Dashboard Example.

- https://github.com/the-unknown/strapi4-react-boilerplate /202212/shell
  - This boilerplate will setup Docker container with React and Strapi 4. 
  - During the setup process you can choose between to following options:
  - NextJS or React
  - SQLite or MariaDB

- https://github.com/il4b/strapi-postgres-pgadmin-boilerplate /202304/ts
  - This open-source boilerplate provides a minimal setup to start a project using Strapi 4, PostgreSQL, and pgAdmin4 with Docker Compose.

- https://github.com/letanure/strapi-boilerplate /202311/ts
  - mostly update deps

- https://github.com/matheus-rodrigues00/strapi_overwriting_user_permission /202303/js
  - Application to demonstrate how to overwrite Strapi user-permission, using Strapi 4.x

- https://github.com/YAKOO-HK/yakoo-strapi-local-starter /MIT/202402/ts
  - Yakoo Strapi + NEXT.js local-hosting starter template

- https://github.com/hoangnhatfe/strapi_nextjs_template /202306/ts/inactive
  - https://strapi-nextjs-template.vercel.app/
  - boilerplate for building SEO-friendly and internationalized (i18n) web applications using Strapi 4.9 and Next.js 13.4. 
  - The project utilizes Next.js with app routing, Server-Side Rendering (SSR) support, and Tailwind CSS for flexible styling.

- https://github.com/appsforyoou/strapi-basic-web /202312/ts
  - Strapi boilerplate for basic landing page builds.

- https://github.com/DarekMazur/react-content-manager /202402/ts
  - a minimal setup to get React working in Vite with HMR 

- https://github.com/david-rodgiquez/LandingPage /202401/ts
  - Jobs page

- https://github.com/ShariqAnsari88/strapi-simple-one-client /202212/js
  - Create React App
  - https://github.com/ShariqAnsari88/strapi-simple-one /js

- https://github.com/SKLINET/strapi-boilerplate /202403/ts/fe+be
  - 依赖graphql、relay

- https://github.com/praveen-1995/strapi-submenus-react-project-v2 /202309/js
  - https://react-strapi-submenus-v2-prod.netlify.app/
  - 纯前端介绍页
  - https://github.com/glitton/strapi-submenus /202311/js

- https://github.com/mparramont/strapi-starter /202404/ts
  - Strapi Starter with PostgreSQL, Typescript and test setup
  - Simple Access Role setup as a Strapi Content-Type

## auth/register

- https://github.com/Kazdan1994/strapi-custom-register-endpoint /202312/js
  - You can overwrite strapi register and / or login endpoint
  - https://github.com/PaulBratslavsky/strapi-register-and-get-github-repos
# examples
- https://github.com/sawden/turbostrapi /202311/ts
  - https://turbostrapi.vercel.app/
  - The Strapi & Next.js Monorepo Starter
  - combining the powers of Strapi, Next.js, and Turborepo in a monorepo setup

- https://github.com/malgamves/modern-cms-apps-course-v2 /202306/js
  - Building Modern CMS Driven Web Applications with Next.js and Strapi
  - [Modern CMS Driven Web Applications with Strapi and Next 13 | egghead.io](https://egghead.io/courses/modern-cms-driven-web-applications-with-strapi-and-next-13-e923dbd8)

- https://github.com/hubertnare/notion-clone-strapi-backend /202205/js
  - https://github.com/hubertnare/notion-clone-strapi-frontend /nextjs
  - https://github.com/mariesta/mariesta-notion-strapi-nextjs /202109/js

- https://github.com/AlirezaBs/twitter-clone /202306/ts/inactive
  - https://tweethub.vercel.app/
  - twitter clone, nextjs

- https://github.com/Dmuasya/SchoolWebsiteStrapi /202301/js/inactive
  - build the frontend and backend of a school website using Strapi, HTML, CSS, and standard JavaScript.
  - [Build a School Website with Strapi and Vanilla JavaScript _202303](https://strapi.io/blog/how-to-build-a-school-website-with-strapi-cms-using-vanilla-javascript)

- https://github.com/aungchanmyaethaw/social-media-app-strapi /202212/js/fe+be/inactive
  - This is a social media app. 
  - Strapi is used to handle database. 
  - UseContext hook is used to store client side data. 

- https://github.com/Ernestoc14/Ecommerce-React-Strapi /202403/js
  - https://ecommerce-react-strapi.vercel.app/
  - a FullStack E-commerce Website build with React, Strapi and Tailwind CSS.
  - using React, Material UI, Stripe, Formik and Yup, Strapi CMS and Redux Toolkit 

- https://github.com/hubertnare/pet-adoption /202204/js/仅前端/inactive
  - For the Pet List, Add Pet, Update Pet, and Delete Pet features from the application, you will use React with a Context API. 
  - [Building a CRUD App with React and a Headless CMS _202205](https://strapi.io/blog/how-to-build-a-crud-app-with-react-and-a-headless-cms)

- https://github.com/satnaing/next-bookstore /MIT/202309/ts
  - https://nextbookstore.vercel.app/
  - online bookstore developed using NextJS 13 with appDir and StrapiCMS. (Still in Beta)
  - Frontend UI is crafted with radix-ui and TailwindCSS. 
  - To manage server and client state, TanStack Query and Zustand are used respectively.

- https://github.com/ClimateCompatibleGrowth/teaching-kit-backend /202403/ts
  - https://github.com/ClimateCompatibleGrowth/teaching-kit-frontend
  - the consumer site for the Teaching Kit. The data displayed is kept on a Strapi service

- https://github.com/JungRama/strapi-ecommerce-cms /202312/ts
  - Starter ecommerce Integration for NextJS and Strapi

- https://github.com/learlab/strapi /202403/js
  - https://github.com/learlab/itell-strapi-demo
  - This repository contains our Strapi configuration for iTELL. It includes several custom or modified plugins in ./src/plugins. 
  - https://github.com/learlab/think-python-cms

- https://github.com/deevanych/keyscenter.backend /202401/ts
  - https://www.keyscenter.ru/
  - Strapi ecommerce backend
  - https://github.com/deevanych/keyscenter.frontend /nuxt

- https://github.com/GabrielLeandroBS/avion /202311/ts
  - https://avion.vercel.app/
  - Project frontend for e-commerce using Strapi for CMS headless and Stripe for payment integration.

- https://github.com/ielmar/strapi-puppeteer-parser-cron /202211/js
  - 🕷️ This is a web scraper which uses Strapi as a headless backend with Sqlite as a database and Puppeteer for scraping data. 
  - It is used for scraping latest added news to the news site https://sabah.az. 
  - Cron is used to run Puppeteer in interval and parse the website for any newly added post.

- https://github.com/psparsa/AlphaGallery /202310/ts
  - A minimal image uploading website built with Next.js and Strapi, styled with Tailwind CSS and tested with Jest/RTL.

- https://github.com/emanuelefavero/strapi-markdown-blog /202303/fe-ts/be-js/nextjs/inactive
  - This is a blog starter project that uses the Strapi Rich Text Data Type and react-markdown to render the content.

- https://github.com/anshu4sharma/blog /202306/ts
  - Next js blog created using tailwind css typescript and strapi

- https://github.com/canopas/canopas-blog-admin /MIT/202402/js/依赖少
  - https://canopas.com/blog
  - Feature-Rich blogs admin panel built with strapi CMS
  - admin依赖strapi-plugin-ckeditor、puppeteer
  - 网站依赖nextjs、markdown-it
  - designed to help bloggers and content creators build and manage their online presence with an emphasis on search engine optimization (SEO)
  - Automatic previews: We created custom previews like medium 
  - suggests relevant content based on the user's reading history

- https://github.com/nicklima/strapi-blog-frontend-next /MIT/202312/ts
  - Next.js Blog with Strapi Headless CMS
  - frontend application (next.js hosted on Vercel) of a Headless blog using Strapi as CMS (hosted on Heroku), including image management.

- https://github.com/Marktawa/blog-strapi /202308/ts
  - Blog website using Strapi for the backend and Next.js for the frontend

- https://github.com/Tammibriggs/strapi-book-app /202208/js
  - Repo for the article on Build a Book App With Infinite Scrolling and Meilisearch Strapi Plugin in React written on Strapi blog
  - [How to Build a Book App With Infinite Scrolling and Meilisearch Strapi Plugin in React_202208](https://strapi.io/blog/build-a-book-app-with-infinite-scrolling-and-meilisearch-strapi-plugin-in-react)

- https://github.com/canopas/canopas-blog /MIT/202402/js
  - https://canopas.com/resources
  - Feature-Rich blogs platform built with strapi and next.js

- https://github.com/NenoSann/picnia /MIT/202403/js/vue
  - https://picnia.vercel.app/
  - a Image post & share platform written in Vue3

- https://github.com/maqi1520/strapi-weibo /202209/ts
  - [使用 Strapi 和 Next.js 开发一个简易微博 - 掘金](https://juejin.cn/post/7145269546465624078)

- https://github.com/ElektronPlus/school-website /202210/ts/v4
  - https://dev.elektronplus.pl/
  - Accessible and extremely user-friendly website template for schools in Poland, built on fun and modern stack.
  - backend: headless CMS (API) that uses Strapi.
  - queries: GraphQL queries. Just create a .graphql that you will want to use.

- https://github.com/sandiprb/strapi-forum /202011/js
  - Strapi CMS based forum

- https://github.com/jurkian/react-bank /202107/ts/inactive
  - Banking app built in React, Redux, TypeScript, Node, Strapi.v3

- https://github.com/For-Hives/api-formenu /202312/js
  - https://github.com/For-Hives/formenu
  - A digital menu for a whole new experience
  - API ForMenu application
  - Strapi, PostgreSQL, NextJs 

- https://github.com/cbgaindia/strapi4-dashboard /202206/js/inactive
  - Built as a documentation platform, it provides the content in easily digestible form. This is the back end of the platform built using Strapi CMS.
  - https://github.com/cbgaindia/budget-basic-next
    - Frontend for Budget Basics developed using Next.js. 
    - Search is handled using Meilisearch.

- https://github.com/h4zan/pottery-studio /202403/ts
  - Project to revisit a pottery shop project, reminiscent of an earlier creation during my HTML and CSS learning phase.
  - currently paused but will be revisited in the near future.

- https://github.com/SadmanYasar/prompt-treasure /202307/ts
  - https://prompt-treasure.vercel.app/
  - Marketplace for Prompts

- https://github.com/nc1z/demo-strapi-rest-backend /202308/ts
  - Strapi CMS (REST) example with custom endpoints and policy setup

- https://github.com/EOS-uiux-Solutions/user-story /202301/js/v3/inactive
  - https://userstory.site/
  - POST stories. GET features.
  - https://github.com/EOS-uiux-Solutions/strapi /202211/js/inactive

- https://github.com/platformsh-templates/strapi4 /202403/js
  - This template builds a Strapi backend for Platform.sh, which can be used to quickly create an API that can be served by itself or as a Headless CMS data source for another frontend app
  - This repository does not include a frontend application

- https://github.com/Akash-shah-cis/ChromoX /202402/js
  - a creative platform where art and technology converge to provide a seamless experience for both creators and art enthusiasts. 
  - This project is built with React, managed effortlessly with Strapi, and transactions powered by Stripe.

- https://github.com/dhzdhd/bidwave /GPLv3/202311/ts/svelte
  - https://bidwave.vercel.app/
  - A realtime auction platform built on SvelteKit and Strapi

- https://github.com/RocketChat/RC4Community /apache2/202406/js
  - https://community.rocket.chat/
  - Full-stack components for building, engaging, and growing your massive on-line community
  - During development, our data provider is a headless CMS, strapi.
# realtime/collab
- https://github.com/strapi-community/strapi-plugin-io /MIT/202312/js
  - https://strapi-plugin-io.netlify.app/
  - A plugin for Strapi CMS that provides the ability for Socket IO integration

- https://github.com/genjudev/strapio /202201/js/inactive
  - Socket. IO Implementation for Strapi
  - module for working with socket.io with predefined rules. StrapIO will look at Role permission on each action. StrapIO is looking for all roles which have access to the given contenttype and action type.
  - https://github.com/genjudev/strapio-example-project /202109/js

- https://github.com/notum-cz/strapi-plugin-record-locking /202312/js/协作简化
  - This plugin provides the functionality to prevent data loss in cases where multiple users are simultaneously editing the same record within STRAPI v4.
  - When a user attempts to edit a record that is already being edited, a warning will be displayed.
  - 依赖socket.io
  - The plugin features its own collection of currently edited entities which is essential for it to work.
    - it sends a web socket event to the Strapi backend with the details of the opened entity
    - When the backend receives this event it adds this entity to the collection of opened entities
    - Why did we use a web socket instead of rest to achieve this?
    - when the user just closes the browser, the web socket receives an event informing the connection was closed

- https://github.com/jenniferokafor/collaborative-code-editor /202306/ts
  - client依赖codemirror.v6、@uiw/react-codemirror

- https://github.com/frontcodelover/iloveshare /202208/js/inactive
  - Just an webapp like dev.to. but in french language only 
  - Users can be connected and add articles, tags, pictures.

- https://github.com/ashish-adhikaree/VetGhat /202303/ts
  - a simple social media app that provides means to connect to your loved ones.

- https://github.com/misstarn/chatstrapi /202310/js/inactive
  - 使用strapi+socketio作为chatapp的后端
  - https://github.com/misstarn/chatapp
    - 使用socket.io+nuxt3+vuetify+tailwindcss制作的聊天软件

- https://github.com/divofred/strapi-chat-app /202205/js
  - Complete Strapified chat application
  - strapi v4 + nextjs
  - [Building a Real-time Chat Application Using Strapi, Next, Socket.io, and PostgreSQL_202206](https://strapi.io/blog/real-time-chat-application-using-strapi-next-socket-io-and-postgre-sql)

- https://github.com/divofred/strapi-chat-app /202205/js
  - chat application

- https://github.com/akashyap25/chat-it /202309/js
  - fe + be
  - https://github.com/akashyap25/chat-it-host

- https://github.com/purnima-strapi-blogs /202101/js
  - self-hostable chat app. Built using ReactJS, Strapi and Socket.io
  - https://github.com/purnima-strapi-blogs/strapi-chat-ui

- https://github.com/ShalomGoodman/chatapp-api /202308/js
  - v4
  - https://github.com/ShalomGoodman/chatapp-frontend

- https://github.com/i1d9/strapi-bids-frontend /202206/js/vue
  - Bid/Auction Application made with strapi, socket-io-client and bootstrap 5
  - https://github.com/i1d9/strapi-bids-backend
  - [Creating a Real-Time Bidding App Using Strapi v4, Vue and Socket IO_202208](https://strapi.io/blog/how-to-create-a-real-time-bidding-app-using-strapi-v4-vue-and-socket-io)

- https://github.com/mervinapiag/room-app-backend-server /202307/ts/1commit
  - Real Time Room App (Create and Join Room)
  - https://github.com/mervinapiag/room-app-frontend-server /202307/js
    - A simple frontend to test only the realtime room creation, joining

- https://github.com/mervinapiag/Realtime-Memory-Game /202307/js
  - Exploring Socket IO using NextJS + Strapi CMS

- https://github.com/Nikoxx99/laniakea /202401/js/vue
  - A solution for watching videos with your friends in sync using WebSockets

- https://github.com/jempool/Strapi-WebSocket-Server /MIT/202312/js
  - 依赖strapi.v3

- https://github.com/dhzdhd/bidwave /GPLv3/202311/ts/svelte
  - https://bidwave.vercel.app/
  - A realtime auction platform built on SvelteKit and Strapi
# client-mobile/pc
- https://github.com/shahednasser/strapi-react-native /202202/js
  - Code for Create a Notes App with Strapi and React Native
# utils
- https://github.com/kristinacowan/wordpress-2-strapi /202005/js
  - Wordpress to strapi one-time conversion code

- https://github.com/qunabu/strapi-unit-test-example /202306/js
  - Example of jest integration/functional tests with Strapi.
  - https://github.com/Antoine-lb/strapi-plugin-testing /v3

- https://github.com/emahuni/strapi-plugin-vitest /202209/ts
  - This plugin provides a Vitest testing harness to enable easier testing with Strapi.

- https://github.com/rogwild/strapi-utils /202310/js/提交多
  - Strapi Utils For Bootstraping Development

- https://github.com/marcusmcb/datasheet-conversion /202312/js
  - Utility app to convert CSV to JSON for Strapi CMS data collection imports

- https://github.com/luca-soda/strapi-handler /202303/ts
  - composing certain types of queries with Strapi can be cumbersome and time-consuming. The complexity of URLs required for these queries can quickly become a developer's worst nightmare
  - Strapi-Handler was developed as a comprehensive solution to streamline REST calls for Collections (excluding single types) in Strapi. By employing simple method chaining, developers can now craft the perfect query within seconds and maintain a clear, readable structure for their code.

- https://github.com/frankdev0428/node-express-strapi /202310/js
  - Strapi comes with a full featured Command Line Interface

- https://github.com/HNTQ/strapi-dynamic-zone /202301/js
  - This a is a partial solution to handle dynamic zone in components. but there is a lot of work to do to make it work in all cases and properly.
  - Do not hesitate to contribute to this repository and try to develop a functional "pluggin" (improvement) for strapi.

- https://github.com/jch-code/strapi-parse /202204/js
  - Parse Strapi V4 API responses into easier to work with objects

- https://github.com/weisrc/strapi-reader /202308/ts
  - Type-safe Reader for Strapi API.

- https://github.com/render-examples/strapi-sqlite /202209/js
  - Deploy Strapi with SQLite on Render
  - https://github.com/render-examples/strapi-postgres
  - https://github.com/naruhitokaide/strapi-postgres

- https://github.com/Refrezsh/strapi-query-builder /202308/ts
  - Utility for type safe queries for Strapi
  - Strapi has flexible syntax for building queries, as the project grows the logic of the queries becomes complex it becomes difficult to keep track of errors in syntax.

- https://github.com/DigiTailsBR/strapiQueryBuilder /202403/js
  - provides a convenient way to construct queries for interacting with a Strapi API.

- https://github.com/FlokiTV/strapi-ez /202309/js
  - provides a convenient way to construct queries for interacting with a Strapi API. 
  - It offers various methods to set filters, specify fields, sort results, paginate data, and more. Here's an overview of the features and usage of the StrapiEz class

- https://github.com/creazy231/strapi-plugin-raw-query /202310/js
  - Raw Query allows you to send raw query strings to the database within Strapi CMS backend. 

- https://github.com/ravgeetdhillon/custom-controllers-strapi /202204/js
  - Implementation Custom Controllers in Strapi using the example of a simple Messaging application.

- https://github.com/mohammadGh/strapi-js /MIT/202404/ts
  - A minimal node / browser / edge, Typescript / Javascript SDK for Strapi headless CMS
  - based on Ofetch and Works with Node.js / Browser / Edge

- https://github.com/LittleBadBad/strapi-common-api /202308/ts
  - provide a "strapi client SDK" wrapped some common request api service functions and strapi types support for strapi based frontend apps, and provide some key typescript types hint help, which is something that is not yet officially implemented by strapi

- https://github.com/liondj0/strapi-orm /202305/ts
  - a package that makes creating requests and mapping responses from strapi cms easy.

- https://github.com/tsarrB/strapi-webshell /202303/js
  - Integrate web shell into your Strapi application
# devops
- https://github.com/acomagu/strapi-payload-model-migrator /202306/ts
  - Import models/components from Strapi V3 to Payload CMS

- https://github.com/jabali2004/strapi-data-replicator /apache2/202404/rust
  - https://jabali2004.github.io/strapi-data-replicator/strapi_data_replicator/index.html
  - Simple command line utility for replicating and migrating persistent tables or collections for Strapi applications
  - The main goal is to simplify development with Strapi and enable easy and automated deployment.
  - Supported databases: MySQL, MongoDB (3.x.x)

- https://github.com/chepeftw/strapi-k8s-blog-post /202302
  - [How to Deploy and Scale Strapi on a Kubernetes Cluster 1/2 _202302](https://strapi.io/blog/how-to-deploy-and-scale-strapi-on-a-kubernetes-cluster-1-2)

- https://github.com/TaitoUnited/strapi-template /2202401
  - https://taitounited.github.io/taito-cli/templates
  - Template for Strapi CMS running on Kubernetes or Docker Compose.
  - This template is a subset of full-stack-template. Use the full-stack-template instead, if you need more than just a Strapi CMS.
  - https://github.com/TaitoUnited/full-stack-template
    - Template for cloud-native applications and microservices running as containers/functions on Kubernetes, Docker Compose, or cloud. 
    - The template can be used with both public cloud and on-premise private cloud.
    - The example implementation is based on React, Node.js, PostgreSQL, and S3 compatible storage, but you can choose the stack during project creation from multiple alternatives, or just write the implementation from scratch.

- https://github.com/ryuheiyokokawa/strapi-helm /202003
  - An example of how you might deploy Strapi to Kubernetes (just an example!)
  - Strapi doesn't exactly deploy super well on Kubernetes without a persistent storage so this shows how you can do it with an NFS mount. BTW, this is mostly for demo use so use with your own caution.

- https://github.com/joellord/strapi /202104
  - Running Strapi with containers
  - To use Strapi in a containerized development environment, you will need three independent containers. One will run the database, another one will have Strapi, and finally, the front-end will have its own container.
# more
- https://github.com/mgmgpyaesonewin/strapi-upptime
  - https://upptime.github.io/upptime
  - https://demo.upptime.js.org/
  - Strapi CMS API Monitoring Page Powered by: Upptime
  - This repository contains the open-source uptime monitor and status page for Upptime, powered by Upptime.
  - With Upptime, you can get your own unlimited and free uptime monitor and status page, powered entirely by a GitHub repository. 

- https://github.com/strapi-support-demo-apps/strapi-example-v4-custom-db /202111/js
  - Example Strapi v4 app showing how the custom v4 migrations work

- https://github.com/klaudsol/klaudsol-cms /MIT/202307/js
  - https://cms-demo.klaudsol.app/
  - a Headless and Serverless CMS (Content Management System). 
  - A great alternative to WordPress and Strapi.
  - 依赖@coreui/react、nivo、nextjs、react-redux、react-bootstrap、react-quill
  - Deploys seamlessly to AWS Amplify Hosting + AWS Aurora Serverless
