---
title: lib-saas-strapi-examples
tags: [examples, strapi]
created: 2023-12-15T19:30:11.399Z
modified: 2023-12-15T19:30:23.094Z
---

# lib-saas-strapi-examples

# guide

# popular
- https://github.com/strapi-community/awesome-strapi
  - A curated list of awesome things related to Strapi
  - https://github.com/strapi/design-system
  - https://github.com/strapi-community/strapi-tool-deployify

- https://github.com/strapi/strapi-examples /202311
  - List of examples using Strapi
  - https://github.com/strapi/nextjs-corporate-starter /202312/ts

- https://github.com/strapi/foodadvisor /202309/js
  - the official Strapi demo application
  - Strapi project with existing Content-types and data (/api)
  - Next.js client ready to fetch the content of the Strapi application (/client)
  - You can also fork this repository and deploy it on Strapi Cloud

- https://github.com/strapi/blocks-react-renderer /202312/ts
  - A React renderer for the Strapi's Blocks rich text editor
- https://github.com/sinkng/strapi-custom-field-type-renderer /202201/js
  - v4

- https://github.com/ShariqAnsari88/strapi-simple-one-client /202212/js
  - Create React App
  - https://github.com/ShariqAnsari88/strapi-simple-one /js

- https://github.com/iopanda/strapi-crack-ee /202310/js
  - only for technique testing, DO NOT use this package in any production environment
# integrations
- https://github.com/tldr-devops/startpack
  - Selfhosted tech starter pack for development of new project or startup
  - This is a basic setup of services for faster startup development. You can run it via docker-compose or docker swarm.
  - https://github.com/strapi/strapi-docker /202208/js/v3

- https://github.com/marmelab/ra-strapi-demo /202210/前端ts/后端js
  - [Building a B2B app with Strapi and React-Admin_202211](https://marmelab.com/blog/2022/11/28/building-a-crud-app-with-strapi-and-react-admin.html)

- https://github.com/nazirov91/ra-strapi-rest /MIT/202304/ts
  - React Admin data provider for Strapi.js
  - 旧版支持v3
  - https://github.com/nazirov91/ra-strapi-rest-demo

- https://github.com/garridorafa/ra-strapi-v4-rest /MIT/202308/ts
  - React Admin REST data provider for Strapi.js v4

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
# plugins
- https://github.com/offset-dev/strapi-calendar /202311/js
  - Visualize your Strapi content in month, week or daily view

- https://github.com/anetaj/strapi-plugin-multi-tenant /202303/js
  - A Strapi plugin to make Strapi a full-fledged backend for your SaaS
  - Have multiple SaaS customers use the same Strapi instance.
  - Isolate content per organization or, more granularly, per user group.
  - The plugin adds `Organization` and `UserGroup` content types. Also, it provides middleware and policies that keep data isolated between tenants.

- https://github.com/VirtusLab-Open-Source/strapi-examples /202304/ts
  - Strapi plugins usage examples

- https://github.com/bn-digital/strapi /202305/ts
  - Additional Strapi plugins, hooks, providers collection
  - Field UUID, Email Emitter, Website

## ui-ext

- https://github.com/VirtusLab-Open-Source/strapi-plugin-navigation /202311/ts
  - A plugin for Strapi Headless CMS that provides navigation/menu builder feature with their possibility to control the audience and different output structure renderers like (flat, tree and RFR - ready for handling by Redux First Router)

- https://github.com/mattmilburn/strapi-plugin-menus /202312/js
  - A plugin for Strapi CMS to customize the structure of menus and menu items.

- https://github.com/remidej/strapi-plugin-todo /202312/js
  - This plugin adds a todo list next to your content in Strapi. 
  - It makes it easy for admin users to keep track of their content management.

- https://github.com/ckeditor/strapi-plugin-ckeditor /202310/js
  - This package provides a custom field for Strapi that lets you use and configure CKEditor in no time.
  - Custom fields are supported since Strapi 4.4+ and offer powerful API to create highly customizable fields.
- https://github.com/nshenderov/strapi-plugin-ckeditor /202303/js
  - Integrates CKEditor 5 into your Strapi project as a fully customizable custom field. (Unofficial integration)
  - Strapi v4.4.0+
  - https://github.com/rajatdangat/strapi-plugin-ckeditor5 /202111/js
- https://github.com/Roslovets-Inc/strapi-plugin-ckeditor5 /202303/js/v3
  - Replace default Strapi markdown WYSIWYG editor with enhanced build of HTML CKEditor 5.
  - Automatic translation of UI into selected in Strapi language (Strapi v3)
  - Strapi v4 (work in progress)
  - https://github.com/Roslovets-Inc/ckeditor5-build-strapi-wysiwyg /202203/js

- https://github.com/dasmikko/strapi-tiptap-editor /202303/js
  - A drop-in replacement for the strapi editor
  - It's build for Strapi v4. It has been tested to work with v4.5.5

- https://github.com/SKLINET/strapi-plugin-tinymce /202304/js
  - Replaces the default Strapi WYSIWYG editor with a customized build of TinyMCE editor.

- https://github.com/melishev/strapi-plugin-react-editorjs /202209/js
  - Plugin for Strapi Headless CMS, hiding the standard WYSIWYG editor on Editor.js
  - This is the Strapi v4 version of this plugin

- https://github.com/fagbokforlaget/strapi-plugin-wysiwyg-toastui /202201/js
  - This plugin replaces strapi wysiwyg draft editor with toastui editor.
  - https://github.com/wizcas/strapi-plugin-wysiwyg-tui-editor /js

- https://github.com/kwinyyyc/strapi-plugin-wysiwyg-react-md-editor /202301/js
  - This is a strapi rich text editor plugin based on react md editor

- https://github.com/plantagoIT/strapi-drag-drop-content-type-plugin /202312/js
  - plugin that provides a drag and droppable menu for ordering content types in a somewhat userfriendly way.

- https://github.com/mattmilburn/strapi-plugin-preview-button /202311/js
  - A plugin for Strapi CMS that adds a preview button and live view button to the content manager edit view.
  - https://github.com/danestves/strapi-plugin-preview-content /v3

- https://github.com/lautr/strapi-plugin-duplicate-button /202311/js
  - Adds a Duplicate Button to the edit view

- https://github.com/excl-networks/strapi-plugin-ezforms /202312/js
  - This plugin allows you to easily consume forms from your front end and automatically reject spam, send out notifications, and store the data in your database.

- https://github.com/Zaydme/strapi-plugin-multi-select /202307/js
  - A strapi custom field for selecting multiple options from a provided list of items.
  - https://github.com/zaydme/strapi-plugin-multi-country-select /202307/js
  - https://github.com/ChrisEbert/strapi-plugin-country-select /202310/js

- https://github.com/alexzaganelli/strapi-plugin-email-designer /202312/js
  - Design your own email templates w/ visual composer directly inside the Strapi admin panel and send composed emails programmatically from your controllers / services.

- https://github.com/canopas/strapi-plugin-tagsinput /202311/js
  - This plugin is used to add tagsinput in your strapi admin panel. 

- https://github.com/raykeating/strapi-location-field-plugin /202310/js
  - A Strapi plugin to enable a custom location field with autocomplete input

- https://github.com/MattieBelt/strapi-plugin-international-fields /202109/js
  - Strapi plugin that adds international fields with i18n support.

- https://github.com/TomaszPilch/strapi-code-editor-custom-field /202308/ts
  - Code editor plugin for strapi CMS. 
  - It uses the monaco editor (vscode).

- https://github.com/WalkingPizza/strapi-plugin-placeholder /202305/js
  - Serve placeholders with your Strapi images
  - Generate base64 placeholders for Strapi images.

- https://github.com/boazpoolman/strapi-code-themes /202207/ts
  - Some IDE inspired color schemes for Strapi v4 admin UI

- https://github.com/nicolashmln/strapi-plugin-responsive-image /202312/js
  - Custom responsive image formats for https://strapi.io v4 (For strapi v3 use v0.5.0)

- https://github.com/strapi-community/strapi-plugin-local-image-sharp /202307/js
  - Dynamically resize, format and optimize images based on url modifiers.

- https://github.com/kwinyyyc/strapi-plugin-zeasy-image-api /202101/js
  - helps you to search for images on Unsplash and Giphy, import it to your media library and insert to your Rich Text content with appropriate attribution.

- https://github.com/emil-petras/strapi-blurhash /202304/js
  - A plugin for Strapi CMS that generates blurhash for your uploaded images

- https://github.com/darron1217/strapi-plugin-video-thumbnail /202203/js
  - Video thumbnail plugin for Strapi
- https://github.com/apivideo/api.video-strapi-plugin /202310/ts
  - A Strapi plugin for managing uploads to api.video.

- https://github.com/flyce/strapi-provider-upload-minio-ce /202307/js
  - This upload provider uses the JavaScript Minio. Client to upload files to a (self hosted) instance of Minio.
  - https://github.com/floreabogdan/strapi-upload-minio

- https://github.com/alexkainzinger/strapi-middleware-upload-plugin-cache /202208/js
  - Adds middleware for caching uploaded assets when using strapi-provider-upload-local
  - https://github.com/merijnponzo/strapi-provider-upload-local-resize

- https://github.com/alexbakers/strapi-provider-upload-ipfs-storage /202301/js
  - IPFS (Filebase, Pinata, Fleek, Web3, Lighthouse) provider for Strapi uploads.

## features-ext

- https://github.com/vivmagarwal/strapi-plugin-custom-api-builder /202304/js
  - Design your custom API's (or custom reports / or custom views) directly from the Strapi CMS admin panel.
  -  Auto compose Routes, Controllers and Services

- https://github.com/PenguinOfWar/strapi-plugin-paper-trail /202310/js
  - Accountability and content versioning for strapi v4+
  - Automatic revision history and auditing with support for all major strapi content types including relations, media, components, and dynamic zones via the admin panel.
  - Roll-back capabilities with the option to select specific fields to restore via the admin panel.
  - Tracks revision history by both admins and users.
  - Internationalization (i18n) plugin support.

- https://github.com/antokhio/strapi-plugin-categorizer /202308/ts
  - A plugin that lets you categorize content quickly.
  - supports multiple categorizer fields per collection
  - feature: multiple categorizers on one target*

- https://github.com/DomDew/strapi-plugin-fuzzy-search /202311/ts
  - Register a weighted fuzzy search endpoint for Strapi Headless CMS you can add your content types to in no time
  - Uses fuzzysort under the hood: Simple, quick and easy. No need to worry about setting up an instance for a complex search engine.
  - https://github.com/farzher/fuzzysort /202211/js

- https://github.com/MattieBelt/mattie-strapi-bundle /202202/js/inactive
  - https://mattie-bundle.mattiebelt.com/
  - Mattie plugin bundle for Strapi
  - Search Plugin, Algolia Search Provider

- https://github.com/creazy231/strapi-plugin-raw-query /202310/js
  - Raw Query allows you to send raw query strings to the database within Strapi CMS backend. 

- https://github.com/strapi/strapi-plugin-seo /202311/js
  - The official plugin to make your Strapi content SEO friendly
  - Manage the important tags for your SEO (metatitle, metadescription) and preview your content in the SERP
  - Manage your meta social tags (Facebook & Twitter) and preview your post.

- https://github.com/nicolashmln/strapi-plugin-oembed /202312/js
  - Embed content from third party sites (Youtube, Vimeo, Tiktok, Soundcloud, Spotify, CodePen...) for https://strapi.io v4 (For strapi v3 use v0.4.0)

- https://github.com/ComfortablyCoding/strapi-plugin-notes /202311/js
  - A plugin for Strapi Headless CMS that provides the ability to add notes to entity records.

- https://github.com/strapi-community/strapi-plugin-rest-cache /202310/js
  - https://strapi-community.github.io/strapi-plugin-rest-cache/
  - This plugin provide a way to cache HTTP requests in order to improve performance. 
  - It's get inspired by varnish cache which is a popular caching solution.
  - The cache content is stored by a provider, which can be either an in-memory provider, a redis connection, a file system, or any other custom provider. You can set a strategy to tell what to cache and how much time responses should be cached. The cache will be invalidated when the related Content-Type is updated, so you never have to worry about stale data.

- https://github.com/VirtusLab-Open-Source/strapi-plugin-comments /202310/ts
  - A plugin for Strapi Headless CMS that provides end to end comments feature with their moderation panel, bad words filtering, abuse reporting and much more.

- https://github.com/msoler75/strapi4author /202206/js
  - I made this example to show a policy/middleware/controller to manage ownership of content.

- https://github.com/boazpoolman/strapi-plugin-sitemap /202312/js
  - Generate a highly customizable sitemap XML in Strapi CMS

- https://github.com/kucherenko/strapi-plugin-passwordless /202312/js
  - A plugin for Strapi Headless CMS that provides ability to sign-in/sign-up to an application by link had sent to email. 
  - A plugin works together with Strapi User Permissions Plugin and extends it functionality. 
  - For working with emails a plugin use Strapi Email Plugin.

- https://github.com/ComfortablyCoding/strapi-plugin-publisher /202311/js
  - A plugin for Strapi that provides the ability to easily schedule publishing and unpublishing of any content type.

- https://github.com/webbio/strapi-plugin-scheduler /202308/ts
  - Strapi Plugin to schedule publish and depublish actions for any collection type.
  - Schedule when you want to publish your content

- https://github.com/phantomstudios/strapi-plugin-github-publish /202211/js
  - This is a plugin for Strapi headless CMS. It lets you trigger a GitHub Action workflow when the site is ready to be published.
  - https://github.com/everythinginjs/strapi-plugin-update-static-content

- https://github.com/Fekide/strapi-plugin-translate /202311/js
  - https://market.strapi.io/plugins/strapi-plugin-translate
  - Strapi plugin for automated translations using different Translate Providers
- https://github.com/manishkatyan/strapi-google-translator /202301/js
  - Translate Strapi collections into multiple languages using Google Cloud Translation

- https://github.com/surgeharb/strapi-plugin-graphs-builder /202203/js
  - A plugin for Strapi Headless CMS that provides graphs building tool to generate custom dashboards and reports with the data inside Strapi's database.
  - https://github.com/surgeharb/strapi-plugins

- https://github.com/strapi-community/strapi-plugin-url-alias /202312/ts
  - Unique, flexible and autogenerated URL aliases for your Strapi managed web content.
  - Automatically generated based on a pattern
  - Public endpoint Get your page by path with the /get endpoint
  - Auto slugify The URLs will automatically be slugified to ensure valid paths

- https://github.com/notum-cz/strapi-plugin-record-locking /202312/js
  - This plugin provides the functionality to prevent data loss in cases where multiple users are simultaneously editing the same record within STRAPI v4.
  - When a user attempts to edit a record that is already being edited, a warning will be displayed.

- https://github.com/Edwin-Luijten/strapi-encryptable-field /202310/ts
  - Encrypts values on save, and decrypts on fetch.

- https://github.com/minzig/strapi-plugin-init-admin-user /202311/js
  - Creates a strapi admin user on startup. 
  - Simplifies working with multiple strapi environments.

- https://github.com/PaulRichez/strapi4-plugin-route-permission /202310/js
  - Strapi4 plugin server route permission
  - A plugin for Strapi that provides the ability to config roles on server route for generate permissions.

- https://github.com/strapi-community/strapi-plugin-protected-populate /202311/js
  - The purpose of this plugin is to have a easy way to protect your get endpoints from getting to much information out of them. I made this plugin since I got sick and tired of writing complex policies to do this exact thing.
  - Protected your Get request populates and fields

- https://github.com/gravitybv/strapi-plugin-permissions /202307/js
  - Permissions plugin for Strapi v4 - Permissions by config file

- https://github.com/eigengrau-ch/strapi-plugin-cookie-manager /202309/js
  - Manage categorized cookies directly within the Strapi CMS admin panel at one place and use the predefined plugin API to provide GDPR consent cookies.

- https://github.com/bwyx/strapi-jwt-cookies /202301/js
  - Securely use users-permissions's JWT on cookies. Compatible with Strapi v4 and requires @strapi/plugin-users-permissions

- https://github.com/olyphotographer/strapi-refresh-tokens /202202/js
  - Strapi V4 with refresh tokens/cookies

- https://github.com/wfzong/strapi-wechat-miniprogram-auth /202303/js
  - WeChat MiniProgram Auth helps you to easily create WeChat MiniProgram authentication available for your user. 
  - It uses the official USER LOGIN REQUEST to get the authorization, you can get it working in under 5 minutes in your WeChat MiniProgram application.

- https://github.com/yasudacloud/strapi-plugin-sso /202311/js
  - This plugin can provide single sign-on.
  - You will be able to log in to the administration screen using one of the following providers: Google, Cognito, Azure, OIDC

## integrations-ext

- https://github.com/strapi/strapi-plugin-open-ai /202311/js
  - The official plugin that allows you to create Open AI completion from a prompt
  - https://github.com/AsyncWeb/strapi-chatgpt /js
  - https://github.com/thirdrocktechno/strapi-plugin-chatgpt
- https://github.com/malgamves/strapi-open-ai-text-generation /202301/js
  - A Strapi Custom Field to generate text content with Open AI Text generation API

- https://github.com/am2222/strapi-plugin-postgis /202305/js
  - https://am2222.github.io/strapi-plugin-postgis/
  - Add native postgis support to strapi.
  - Since Strapi does not support native database formats, I convert requests before they being sent to the querybuilder and convert all the geometry objects to the geojson.
  - https://github.com/notum-cz/strapi-plugin-location /ts

- https://github.com/meilisearch/strapi-plugin-meilisearch /202312/js
  - A strapi plugin to add your collections to Meilisearch
  - Add your Strapi content-types into a Meilisearch instance. The plugin listens to modifications made on your content-types and updates Meilisearch accordingly.

- https://github.com/strapi-community/strapi-provider-upload-google-cloud-storage /js
  - Google Cloud Storage Upload Provider for Strapi

- https://github.com/jakeFeldman/strapi-provider-upload-azure-storage /202311/ts
  - Strapi Provider Upload Azure Storage
  - Plugin enabling image uploading to azure storage from strapi.

- https://github.com/zoomoid/strapi-provider-upload-aws-s3-advanced /202212/ts
  - extend the S3 Upload Provider to support path prefixes inside a bucket

- https://github.com/hezzze/strapi-provider-upload-oss /202310/js
  - A provider for strapi server to upload file to Aliyun OSS
  - https://github.com/yclgkd/strapi-provider-upload-tencent-cloud-storage /ts

- https://github.com/manishkatyan/strapi-stripe /202307/js
  - Stripe Plugin for Strapi CMS

- https://github.com/ComfortablyCoding/strapi-plugin-website-builder /202311/js
  - A plugin for Strapi that provides the ability to trigger website builds manually, periodically or through model events.

- https://github.com/strapi-community/strapi-plugin-redis /202303/js
  - Plugin used to centralize management of Redis connections in Strapi

- https://github.com/bass3l/strapi-provider-email-smtp /202204/js
  - A third-party SMTP email provider for Strapi, tested with Gmail SMTP.

## utils-ext

- https://github.com/ShahriarKh/strapi-content-type-explorer /202307/js
  - plugin that visualizes your content types and their relationships like an ERD (Entity Relationship Diagram).

- https://github.com/TonyDeplanque/strapi-plugin-migrations /202309/js
  - If you want to initialize or update automatically your data in Strapi for all of your environments, this plugin is made for you.

- https://github.com/Baboo7/strapi-plugin-import-export-entries /202312/js
  - Import/Export data from and to your database in just few clicks.
  - Import/Export data directly from the Content Manager
  - Control which roles can import/export data from the admin UI.
  - https://github.com/jbeuckm/strapi-plugin-import-content /v3

- https://github.com/Barelydead/strapi-plugin-populate-deep /202311/js
  - This plugin allows for easier population of deep content structures using the rest API.
  - The default max depth is 5 levels deep.
  - The populate deep option is available for all collections and single types using the findOne and findMany methods.

- https://github.com/ComfortablyCoding/strapi-plugin-transformer /202309/js
  - A plugin for Strapi that provides the ability to transform the API request and/or response.
  - GraphQL is not supported

- https://github.com/Eomm/fastify-raw-body /202311/ts
  - Adds the raw body to the Fastify request object.

- https://github.com/MaksZhukov/strapi-plugin-generate-data /202310/ts
  - This plugin is for generating data for your content-types.
  - It supports only string with RegExp pattern, email, richtext, integer, decimal, date, media(videos, images, audios, files), boolean enumeration, password, UID, relation, json fields of your content types.
  - It creates content in draft if the content type has draft & publish option

- https://github.com/ComfortablyCoding/strapi-plugin-io /202311/js
  - https://strapi-plugin-io.netlify.app/
  - A plugin for Strapi CMS that provides the ability for Socket IO integration
- https://github.com/larsonnn/strapio /202201/js
  - Socket. IO Implementation for Strapi
  - module for working with socket.io with predefined rules. StrapIO will look at Role permission on each action. StrapIO is looking for all roles which have access to the given contenttype and action type.

- https://github.com/node-vision/strapi-plugin-entity-relationship-chart /202310/js
  - Strapi Plugin displays Entity Relationship Diagram of all models, fields and relations.
  - this plugin was tested with stable Strapi - 4.0.6

- https://github.com/boazpoolman/strapi-plugin-config-sync /202312/js
  - CLI & GUI for continuous migration of config data across environments
  - This plugin is a multi-purpose tool to manage your Strapi database records through JSON files. 
  - Mostly used to version control config data for automated deployment, automated tests and data sharing for collaboration purposes.

- https://github.com/mancku/strapi-plugin-schemas-to-ts /202312/ts
  - plugin for Strapi v4 that automatically converts your Strapi schemas into Typescript interfaces.

- https://github.com/akcyp/strapi-plugin-point-list /202210/ts
  - A plugin for Strapi CMS that provides point list field (when drawing on image)

## v3-ext

- https://github.com/alan2207/strapi-plugin-sync-roles-permissions /202107/js
  - Store user roles and permissions configuration as a JSON file and then import and reuse it any time.

- https://github.com/8byr0/strapi-plugin-backup-restore /202112/js
  - Plugin to backup & restore your strapi installation (database + uploads) from admin panel.
  - Compatibility with strapi v4 is not available (only v3 is currently supported)

- https://github.com/Radrw/strapi-pro /201802/js
  - Strapi.io with image upload, location, wysiwyg input

- https://github.com/alexdevmotion/strapi-faker /202008/js
  - Fill your strapi models with faker.js
# examples
- https://github.com/canopas/canopas-blog /202311/js
  - https://canopas.com/resources
  - Feature-Rich blogs platform built with strapi and next.js

- https://github.com/ElektronPlus/school-website /202210/ts/v4
  - https://dev.elektronplus.pl/
  - Accessible and extremely user-friendly website template for schools in Poland, built on fun and modern stack.
  - backend: headless CMS (API) that uses Strapi.
  - queries: GraphQL queries. Just create a .graphql that you will want to use.

- https://github.com/sandiprb/strapi-forum /202011/js
  - Strapi CMS based forum

- https://github.com/marmelab/strapi-beerdex /202103/js
  - StrapiJS Example Application For Beer Management
  - [Building A Web Application In 15 Minutes Using StrapiJS And NextJS_202006](https://marmelab.com/blog/2020/06/18/build-an-application-in-fiften-minutes-using-strapijs.html)

- https://github.com/jurkian/react-bank /202107/ts/inactive
  - Banking app built in React, Redux, TypeScript, Node, Strapi.v3

- https://github.com/EOS-uiux-Solutions/user-story /202301/js/v3
  - https://userstory.site/
  - POST stories. GET features.
  - https://github.com/EOS-uiux-Solutions/strapi
# utils
- https://github.com/qunabu/strapi-unit-test-example /202306/js
  - Example of jest integration/functional tests with Strapi.
  - https://github.com/Antoine-lb/strapi-plugin-testing /v3

- https://github.com/frankdev0428/node-express-strapi /202310/js
  - Strapi comes with a full featured Command Line Interface

- https://github.com/Stun3R/strapi-sdk-js /202308/ts
  - Javascript SDK for your Strapi API
  - Simplified request responses

- https://github.com/render-examples/strapi-sqlite /202209/js
  - Deploy Strapi with SQLite on Render
  - https://github.com/render-examples/strapi-postgres
  - https://github.com/naruhitokaide/strapi-postgres
# v5
- https://github.com/strapi/v5-experiments
  - /202307/ts
# more
- https://github.com/strapi-support-demo-apps/strapi-example-v4-custom-db /202111/js
  - Example Strapi v4 app showing how the custom v4 migrations work
