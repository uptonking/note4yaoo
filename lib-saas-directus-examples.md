---
title: lib-saas-directus-examples
tags: [cms, directus, examples]
created: 2024-03-14T13:50:55.256Z
modified: 2024-03-14T13:51:11.429Z
---

# lib-saas-directus-examples

# guide

- fans-directus
  - https://github.com/ptkio/directus-extension-group-layout-sidebar
  - https://github.com/codihaus/directus-extension-grid-layout
  - https://github.com/br41nslug/directus-extension-live-preview-sync
  - https://github.com/bcc-code/directus-sql-query-panel

- resources
  - [Directus extensions](https://directusextensions.com/browse)
    - includes all Directus Extensions available on npm that adhere to the `directus-extension-*` naming strategy
# popular
- https://github.com/directus-labs/awesome-directus
  - Extensions, Examples/Showcases

- directus /25kStar/GPLv3 > BSL/202403/ts/vue
  - https://github.com/directus/directus
  - https://directus.io/
  - https://docs.directus.io/
  - http://0.0.0.0:8055/admin
  - Directus is an instant REST+GraphQL API and intuitive no-code data collaboration app for any SQL database
  - 后端依赖express、knex、ioredis、keyv、async(很少用)、commander、graphql、marked、micromustache、eventemitter2、node-cron、rate-limiter-flexible、sharp、vm2、ws
  - 前端依赖vue3、pinia2、vueuse、vuedraggable、vue-i18n、editorjs、tinymce.v6、tinymce-vue.v5、fullcalendar、p-queue、apexcharts、codemirror.v5、cropperjs(img)、maplibre-gl、marked、mitt、histoire
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
 - 🍴 forks
  - https://github.com/LaWebcapsule/directus9 /GPLv3/202402/ts/vue
    - a fork of the Directus 9
    - Directus 10 is now a premium open-source software

- https://github.com/rezo-labs/directus-extension-computed-interface /GPLv3/202309/ts/vue/inactive
  - extension for 📈 automatically calculating the value of a field based on other fields of the same item, on the client side.
  - Support templating, arithmetic operations. Concat strings, sum, subtract, multiply, modulo, convert to slug, currency, etc.
  - Can be used as an alias field.
  - Calculation is performed on the client side, so it would not work if the item is created/updated via direct API calls or hooks.
  - Lightweight. No third-party libraries.
  - The template consists of 2 elements: plain strings & expressions.

- https://github.com/gremo/react-directus /ISC/202403/ts
  - A set of React components and utilities for Directus
  - The `<DirectusProvider>` component makes the Directus JavaScript SDK available to any nested components that need to access it.

- https://github.com/directus-labs/directus-templates /202402/全是json
  - https://github.com/directus-labs/directus-template-cli
  - Community maintained Directus instance templates to help you jump start your next project.
  - Templates are extracted and applied using the `directus-template-cli` command line utility.
  - What's Included in a Template?
    - They're examples of what you can build with Directus
    - Schema/Data Model
    - Users and Authentication
    - Flows
    - Dashboards
    - Files

- https://github.com/luochuanyuewu/nextus /MIT/202402/ts
  - https://nextus.vercel.app/
  - 多功能的现代化网站模板，基于Nextjs和Directus技术
  - Tailwind CSS and Daisyui
  - Dynamic Page Builder (M2A Interface) within Directus

- https://github.com/directus-labs/agency-os /MIT/202402/ts/vue/nuxt
  - https://agencyos.dev/
  - https://agency-os.vercel.app/
  - 管理后台在 https://directus.pizza/
  - The open source operating system for digital agencies. 
  - Built with Nuxt 3 Website/Application + Directus Backend.
  - Brought to you by partnership magic between Directus and NuxtLabs.
  - [Introducing AgencyOS: The All-In-One Operating System for Digital Agencies _20231025](https://directus.io/blog/announcing-agencyos)
    - we’re releasing AgencyOS as the first example of a purpose-built system to show off the incredible functionality that you can build in record time with Directus.

- https://github.com/fabian-hiller/directus-sdk /202306/ts
  - This repository can be seen as an alternative proposal to the current Directus SDK.
  - Modular design
  - This SDK builds on existing web APIs like the Fetch API and therefore has no dependencies and can run in any environment. 

- https://github.com/cesarsalesgomes/dna /202403/ts/svelte
  - Fullstack Typescript project with the objective of joining four well-regarded tools (back-end NestJS/Directus, front-end React or Svelte)

- https://github.com/domsen123/directus-extensions /202401/ts
  - SSR renders your own Vue/Vite Application into an self-hosted Directus Instance.
  - https://github.com/domsen123/directus-ssr-starter /202310/ts

- https://github.com/marmelab/ra-directus /MIT/202306/ts
  - Directus Data Provider & Auth Provider for react-admin
  - A simple demo app you can run locally to try out ra-directus with your own Directus app
# extensions
- https://github.com/resauce-dev/directus-image-scout /GPLv3/202310/js/vue
  - A clean interface is provided allowing you to search multiple online image libraries to find images that suit your needs.
  - Confirmed Support for v10-10.6.1

- https://github.com/rezo-labs/directus-extension-schema-management-module /202308/vue
  - Tired of creating the same collection all over again? This module extension can make it easier to share schema between Directus instances. 
  - Simply copy the schema code from one Directus and paste it to the other
  - https://github.com/alexvdvalk/directus-schema-tools
    - Enhanced version of schema loader which the schema through the /collections and /fields APIs.

- https://github.com/u12206050/directus-extension-global-search /MIT/202311/ts/vue
  - A module for searching across multiple collections at once
  - returning results to allow you to navigate directly to the item page.

- https://github.com/jee-r/directus-extension-base64 /MIT/202311/ts
  - extension that encodes uploaded images in base64 format. 
  - The extension takes an image file as input and returns its base64 encoded string.

- https://github.com/dimitrov-adrian/directus-extension-searchsync /MIT/202112/js
  - Simple Directus 9 extension that sync content with remote search engine
  - Supported engines: MeiliSearch, ElasticSearch, Algolia
  - https://github.com/Lukas-Sachse/directus-extension-searchsync-docker-demo

- https://github.com/codihaus/directus-extension-seo /MIT/202402/ts
  - https://directus-extensions.codihaus.io/
  - Extension enhance Directus with powerful SEO scoring and validator and AI SEO from ChatGPT

- https://github.com/utomic-media/directus-extension-field-actions /GPLv3/202403/ts/vue
  - Add link & copy to clipboard functionalities to your directus fields. 
  - Supports interfaces as well as displays.
  - The actions can be performed by a button next to the items or by clicking on the value. 

- https://github.com/seymoe/directus-extension-filepreview-interface /MIT/202402/js/vue
  - A file preview interface.
  - Create a field with File Preview, set field name that you want to preview, and set a static token

- https://github.com/codihaus/directus-extension-grid-layout /202312/ts/vue
  - https://directus-extension.codihaus.io/
  - Extension to display items as grid with customizable, flexible display.
  - allows users to present data in a grid layout 

- https://github.com/codihaus/directus-extension-kanboard /MIT/202401/ts/vue
  - Kanboard Layout Extension for Directus: customize your Kanban boards.

- https://github.com/shocota/directus-extension-board-layout /GPLv3/202301/ts/vue/inactive
  - a layout extension for Directus, that allows you to display items in a Kanban-style layout.

- https://github.com/seymoe/directus-extension-vgrid-interface /MIT/202402/js/vue
  - extension with @revolist/vue3-datagrid, specify fixed columns to generate an editable table field.
  - https://github.com/seymoe/directus-extension-vgrid

- https://github.com/br41nslug/directus-extension-live-preview-sync /MIT/202403/js/vue
  - An interface to push realtime updates to the live preview iframe.
  - Tested with Directus 10.10.4

- https://github.com/formfcw/directus-extension-tokenized-preview /GPLv3/202403/ts
  - An endpoint that adds an active auth token to your preview URL
  - The auth token, which has a limited TTL, allows you to to preview content that is not publicly available through the API.

- https://github.com/Attacler/directus-extension-admin-panels /202311/ts/vue
  - Adds panels to Directus to manage Directus more efficient.

- https://github.com/rezo-labs/directus-extension-api-trigger-interface /GPLv3/202209/ts/vue
  - A Directus interface extension for triggering API calls from the UI.
  - API calls are authenticated automatically.

- https://github.com/u12206050/directus-extension-api-viewer-module /MIT/202310/vue
  - A module for displaying your Directus api documentation directly within the App

- https://github.com/sacconazzo/directus-extension-api-docs /MIT/202310/ts
  - Extension to include a Swagger interface and custom endpoints definitions

- https://github.com/br41nslug/directus-extension-reference /MIT/202311/md
  - These docs are generated using TypeDoc for an easy reference of the Services exposed to backend extensions by Directus.

- https://github.com/repoerna/directus-extension-document-interface /202312/ts/vue
  - extension to preview document

- https://github.com/timio23/directus-panel-internal-chat /MIT/202310/js/vue
  - Native internal chat panel for communicating with other users from a dashboard.
  - This extension will solve internal communication issues by providing a customized chat that can be linked to a collection and be made persistant across dashboards
  - Uses the built-in comments feature in the activity table. Simply choose the collection and quote an item id or type a unique identifyer for the chat.
  - Directus 10.0.0+

## flows

- https://github.com/baguse/directus-extension-flow-manager /MIT/202311/ts/vue
  - A directus custom module extension for managing directus flow includes backup/restore, duplication and grouping the flow.
  - Feature for keeping original flow id when restore
  - Add feature to import directly to another directus instance
  - https://github.com/baguse/directus-extension-flow-manager-endpoint

- https://github.com/das-buro-am-draht/directus-flow-sync /GPLv3/202312/ts
  - extension to import and export directus flows and operations
  - This directus CLI extension allows you to sync your directus flows and operations with your local filesystem.

- https://github.com/timio23/directus-panel-manual-flows /MIT/202310/ts/vue
  - This extension will bring your manual flows from multiple collections together into a convenient panel or split them into several panels.
  - Uses the flows endpoint and native components to provide the same functionality. Simply choose the collections that you want to include.

- https://github.com/karamokoisrael/directus-extension-flow2pdf /202402/js/vue
  - The flow2pdf extension is a bundle that allows directus to print data from flow results and liquid templates.
  - The extension will add a new interface and endpoint to your directus instance. All configurations are available in the pdf manager interface.
  - 依赖liquidjs、html2pdf.js
- https://github.com/Skivholme/directus-extension-directus-opreation-base64pdf /202402/js
  - PDF to base64 converter, from file or from url
  - 依赖pdf-to-base64、buffer

- https://github.com/euryecetelecom/directus-extension-operation-download-store-file /MIT/202403/ts
  - Directus flows operation extension allowing to download and save external files. 
  - Authentication via headers is supported. 
  - Can be used to download huge files without storing them locally or in RAM as it is based on axios Stream capabilities.

- https://github.com/ComfortablyCoding/directus-operation-slugify /MIT/202403/ts
  - A Directus slugify operation for Flows. 
  - It automatically handles most major languages, including German (umlauts), Vietnamese, Arabic, Russian, and more.
- https://github.com/muratgozel/directus-operation-slugify /MIT/202402/ts
  - operation extension to generate language aware slugs.

- https://github.com/dimitrov-adrian/directus-extension-wpslug-interface /GPLv3/202301/ts/vue
  - WordPress alike slug interface for 
  - Directus 9

- https://github.com/samechikson/directus-extension-file-import-operation /202310/ts
  - This extension allows you to import images from external URLs in a Flow. 
  - It will download the image and store it in the Directus storage.

- https://github.com/Guiqft/directus-backup-operation /202301/ts/inactive
  - Custom Directus operation to backup Postgres database using `pg_dump` and upload the `.dump` file into Directus storage.

## ui

- https://github.com/formfcw/directus-extension-flexible-editor /GPLv3/202403/ts/tiptap
  - A Rich Text Editor (WYSIWYG) with JSON output, that allows to integrate M2A relations to make it extremely flexible.
  - 依赖tiptap2、tiptap-render-view

- https://github.com/gbicou/directus-extension-tiptap /MIT/202403/ts/vue
  - Tiptap rich text editor interface and display for directus

- https://github.com/ThijmenGThN/directus-themebuilder /MIT/202312/ts
  - https://heuve.link/directus-themebuilder
  - A Theme Builder for Directus

- https://github.com/dimitrov-adrian/directus-extension-group-modal-interface /GPLv2/202205/ts/vue
  - Group fields into modal dialog, accessible via button.

- https://github.com/jacoborus/directus-extension-display-link /202211/ts/vue
  - Display URLs as links in Directus 9

- https://github.com/programmarchy/directus-extension-render-template /MIT/202401/ts
  - extension that defines a flow which renders a mustache template given a template and scope
  - defines a flow which renders a mustache template using `micromustache render(...)`.

- https://github.com/u12206050/directus-extension-filters-interface /MIT/202402/ts/vue
  - This is a custom filter & rule interface for Directus 9&10. 
  - It allows you to setup an interface with defined properties that users can then select and add values and conditions for.
  - Using the Rule Filter Validator library you can validate and test the rules stored in your frontend and backend.

- https://github.com/luigigorlero/directus-extension-formatted-input /MIT/202403/ts/vue
  - A simple Rich String Editor interface to format short texts in Directus

- https://github.com/ptkio/directus-extension-input-multiline-with-rows /MIT/202403/ts/vue
  - Default Directus multiline interface with row number option. 
  - This allow you to choose the height of the textarea.

- https://github.com/ptkio/directus-extension-group-layout-sidebar /MIT/202403/ts/vue
  - Group layout sidebar is an interface for Directus that provides field organization with a docked sidebar.

- https://github.com/formfcw/directus-extension-classified-group /GPLv3/202403/ts
  - A group to which a class can be assigned for custom styling
  - https://github.com/formfcw/directus-extension-tab-group

- https://github.com/formfcw/directus-extension-drawer-notice /GPLv3/202403/ts
  - A notice field that is only visible in the drawer.
  - The main use case for this extension is to display a message when editing a related item in the drawer, to prevent users from accidentally overwriting the contents of an existing item.

- https://github.com/omkardedge011/directus-extension-collection-selector /GPLv3/202402/ts/vue
  - This extension enables effortlessly selecting the collections directly from the database within the Directus interface.

- https://github.com/rezo-labs/directus-extension-key-value-interface /MIT/202402/ts/vue
  - A custom interface for Directus that allows you to edit key-value pairs with schema and type inference.

- https://github.com/DavidDemory/directus-extension-parser /GPLv3/202402/js
  - extension that'll parse a string like `"key1=value1;key2=value2;"`, put each key and each value in input so that you can update them easier.

- https://github.com/felpsalvs/extension-custom-directus /202402/js
  - This package provides a boilerplate for creating custom layouts for Directus

- https://github.com/martabitbrain/directus-extension-sane-image-size /MIT/202401/js
  - Extension Hook that resizes an image to a maximum size on upload.
  - This extension modifies big images on upload to a preset maximum (width, height & quality).

- https://github.com/ameotoko/directus-extension-assets /MIT/202311/ts
  - extension for resizing images preserving focal_point
  - a port of the "Important part of an image" feature from Contao CMS.

- https://github.com/lucameusburger/directus-display-extensions /202312/js/vue
  - useful custom displays for directus 9 like hyperlinks and currency formats.

- https://github.com/renatomoor/directus-extension-iconify /202312/ts
  - This extension adds a field type to Directus that allows you to select an icon from the Iconify library.
  - It will save the icon name as string in the database.

## db

- https://github.com/7span/directus-extension-custom-query-panel /202311/js/vue
  - easy to use insight panel to see custom raw query data from database
  - Execute custom SQL queries directly from the panel.
  - Display query results in a simple tabular structure for easy readability.

- https://github.com/bcc-code/directus-sql-query-panel /MIT/202402/ts/vue
  - Insights Panel for viewing results for dynamic sql queries

- https://github.com/premieroctet/directus-extension-sql-panel /MIT/202311/ts/vue
  - a custom interface for Directus that allows you to display result of your SQL queries in a table

- https://github.com/programmarchy/directus-extension-sql-query /MIT/202401/ts
  - extension that defines a flow operation which executes SQL queries using `knex.raw(sql, bindings)`.

- https://github.com/ChappIO/directus-extension-schema-merge /202402/ts
  - This extension adds the cli command schema-merge to the directus except it uses a modified .yml format which should cause fewer merge conflicts during `git merge`s.

- https://github.com/FireboltCasters/directus-extension-auto-backup /202402/js
  - This extension automatically makes backups of your database for you.
  - Automatically backups (with directus flows)
  - 支持SQLite

- https://github.com/ChappIO/directus-extension-models /202310/ts
  - This extension lets you generate typescript types from your Schema, allowing you to more easily develop your custom extensions with type checking.

- https://github.com/freekrai/directus-extension-upsert /MIT/202306/js
  - extension for upserting records in a single API call, it will check if the record exists and if so, update it, otherwise it will create it.

- https://github.com/ChappIO/directus-extension-seed /202309/ts
  - Seed simple data into the database (useful for setting permissions and settings)

## utils

- https://github.com/TheRocketLab/directus-import-images-and-data /MIT/202307/js
  - This repo bulk uploads images and data and associates them with a collection in Directus
  - You have formatted your JSON file to match the collection you are trying to import to in Directus

- https://github.com/utomic-media/directus-extension-upload-limiter /202207/ts/inactive
  - extension which tracks the aggregated filesize of all uploads by a user and allows to set an project-wide upload limit. 
  - Hooks into create and delete actions of directus_files and calculates the upload-size

- https://github.com/FireboltCasters/directus-extension-auto-backup /202402/js
  - This extension automatically makes backups of your database for you.
  - Supported databases: SQLite

- https://github.com/directus-labs/schema-builder-kit /MIT/202201/ts/inactive
  - a proof of concept for creating data models for directus programmatically instead of with the admin UI

- https://github.com/br41nslug/directus-extension-block-endpoints /MIT/202403/ts
  - this extension will allow you to block any endpoint with a custom message.

- https://github.com/programmarchy/directus-extension-jwt-verify /MIT/202307/ts/inactive
  - extension that defines a flow operation which verifies a JWT using jsonwebtoken
- https://github.com/programmarchy/directus-extension-jwt-sign /MIT/202307/ts
  - extension that defines a flow operation which signs a JWT using jsonwebtoken.

- https://github.com/zerosubnet/directus-extension-external-jwt /GPLv3/202311/ts
  - This plugin serves as a way to make Directus trust externally signed JWT tokens from an `OIDC` or `OAuth2` provider.
  - The provider must issues Access tokens as JWT since this is used for verification right now. Might add support for general tokens later.

- https://github.com/ChappIO/directus-extension-static-auth /202401/ts
  - This simple extension lets you create users and roles with static access tokens from the command line. 
  - Very useful to provision your directus deployments and other backend when you're using CI/CD.

- https://github.com/Attacler/directus-extension-jsc-encrypt /202301/ts/inactive
  - This package is designed for encrypting and decrypting data within Directus. 
  - It ensures that data is always stored in an encrypted form inside your database, and targets specific collection fields.

- https://github.com/Deveosys/directus-extension-public-folders /GPLv3/202402/ts
  - This extension grants public read access to all folders created with the name 'public' or under a 'public' folder. It also cleans up permissions when a folder is deleted.

- https://github.com/br41nslug/directus-extension-increment /MIT/202403/ts
  - extension for incrementing fields in a single API call
  - This middleware will intercept any PATCH requests to `/items/:collection/:item` and replace any `increment(<number>)` or `increment(<float>)` value with an incremented value in the body before handing it over to the regular directus item handler.

- https://github.com/Skivholme/directus-extension-directus-endpoint-qrcode /202403/js
  - extension-directus-endpoint-qrcode
  - https://github.com/Skivholme/directus-extension-directus-interface-qrcode /202402/js/vue
  - https://github.com/Skivholme/directus-extension-directus-opreation-qrcode

- https://github.com/nuxtus/directus-extension-timesheet /202401/ts/vue
  - extension bundle for working with timesheet data and timers.
  - A project timer layout for timesheet collections in Directus. Allows users to start/stop a timer and record the times in a timesheet.

- https://github.com/ayasy-el/directus-extension-operation-killport /202312/js
  - Directus operation extension to terminate a specific port

- https://github.com/ayasy-el/directus-extension-operation-exec /202312/js
  - extension for custom execution command

- https://github.com/FloMaetschke/directus-extension-bundle-systeminfo /202311/ts/vue
  - extension provides a panel for displaying the system information of the Directus instance.
  - uses the npm package `systeminformation` to retrieve the informations.

- https://github.com/izoukhai/directus-extension-nanoid /202310/ts
  - Generate random IDs of any size and any shape with Nanoid directly in your Directus app

## integrations

- https://github.com/smokeyfro/directus-extension-bundle-api-fetch /202311/js/vue
  - Connect to the 3rd-party api's, then add them to your configured collection.

- https://github.com/Digital-Livonia/directus-iiif-endpoint /202402/js
  - adds IIIF presentation API support to Directus media files

- https://github.com/Arood/directus-extension-jira-panels /MIT/202311/ts
  - This extension contains panels for your Directus Insights dashboards that allow your users to see tasks in JIRA or even submit their own feedback.

- https://github.com/KITeGG-Node-Modules/directus-extension-gitlab-api-endpoint /202309/js
  - endpoint to fetch repositories from GitLab RLP through Directus.
  - To make this extension work you need to add a GitLab access token

- https://github.com/Attacler/TextToAnything-Directus /202402/ts/vue
  - This extension allows you to generate PDFs, QRCodes and Barcodes within Directus trough TextToAnyThing API

- https://github.com/directus-labs/extension-ai-writer-operation /202403/js
  - Generate text from a text input and prompt within Directus Flows with this custom operation, powered by GPT-4

- https://github.com/directus-labs/extension-ai-image-generation-operation /202403/js
  - Generate new images within Directus Flows with this custom operation, powered by OpenAI

- https://github.com/directus-labs/extension-ai-image-moderation-operation /202403/js
  - Moderate images within Directus Flows with this custom operation, powered by Clarifai.

- https://github.com/Intevel/directus-logsnag /MIT/202207/ts/inactive
  - Get notified when something in Directus happens.
  - LogSnag is a simple event tracking tool. It helps you keep track what is happening within your projects, creates custom feeds, and notifies you of important events.
  - 依赖LogSnag在线服务

- https://github.com/rhyst/directus-strava /202403/ts
  - extension to enable automatic and easy manual backup of Strava activities
  - The Strava activity endpoint does not allow access to private notes or original GPX data.

- https://github.com/kestraI/directus-extension-gh-stats /202310/js/vue
  - GitHub Repo Statistics Panels on Directus
  - Show statistics from a GitHub repository including stars, issues, and pull requests.
  - This panel uses the GitHub API to show data from a GitHub repository directly in an Directus dashboard.

- https://github.com/timio23/directus-operation-auto-translate /202309/js
  - Use ChatGPT language models to automatically translate your content through Directus Flows
# starter
- https://github.com/Jabat-Software/directus-typescript /202312/ts
  - Directus 10 project template in TypeScript
- https://github.com/ylivuoto/directus-nextjs-build-api /202308/ts/单文件
  - a basic build api for Directus and Next.js using Express.

- https://github.com/shubshinde/NexTusPlate /MIT/202402/ts
  - Admin Dashboard Starter with Directus, Nextjs 14, NextAuth and ShadCn UI
  - Authentication with NextAuth supports Social logins and email logins

- https://github.com/focusreactive/MVP-Directus-NextJS14 /202311/ts
  - https://mvp-directus-next-js-14.vercel.app/
  - The project is a Proof of Concept (POC) based on NextJS 14 as the front-end application and Directus as a Headless Content Management System (CMS).

- https://github.com/linefusion/directus-container /MIT/202402/ts
  - Directus Docker Images
  - Alternative container image for Directus with support for extensions.

- https://github.com/felpsalvs/directus-customization /202402/js/vue
  - This repository contains a docker file to run Directus, an open-source data management platform. 
  - It also contains a customizable extension that can be used to add new functionality to Directus.
# examples
- https://github.com/pintoderian/next-directus-auth-ts /202401/ts
  - Template for project structure with nextjs 13 - next auth - directus and typescript

- https://github.com/NxtNinja/AlteraX /202402/ts
  - a full stack social media application built with NextJs as frontend and Directus as Backend

- https://github.com/amaben2020/multi-lang-blog /202310/ts
  - https://multi-lang-blog.vercel.app/
  - A multi language blog app built with Next js, Directus, i18n, tailwind technologies

- https://github.com/codejagaban/nextjs-hotel-booking /202403/ts
  - hotel booking website built with Nextjs, Directus and Stripe

- https://github.com/YuliyaMinsk/directus-shop /202401/ts
  - a simple application designed to test the following technologies: Next14 (with TypeScript), Tailwind, TanStack Query.

- https://github.com/Icloudeng/directus-portal /202310/ts/inactive
  - A website builder and CMS that lets you create sites by combining pre-designed section templates.
  - CMS part powered by Directus
  - Web Part made with NextJs

- https://github.com/munichdeveloper/nextjs-directus-multitenant-starter /MIT/202312/ts
  - A nextjs Starter Template for directus CMS enriched with some multi tenancy features

- https://github.com/SeedWebs/seedx /MIT/202402/js
  - https://seedx.seedwebs.com/
  - The Open Source Starter Site with Next.js, Tailwind CSS & Directus

- https://github.com/zzacong/twitter-clone-next /202304/ts
  - https://tw.zzacong.com/
  - Twitter 2.0 with REACT. JS! (Next.js, Directus CMS, Typescript, SSR, TailwindCSS & NextAuth)

- https://github.com/funny2code/hackernews_clone /202308/js
  - NextJs and Directus

- https://github.com/d135-1r43/bandlinks /202401/js/svelte
  - A simple link tree for bands with Directus as backend
  - written in Svelte with SvelteKit and uses Tailwind with DaisyUI. 
  - All content is fetched from a self-hosted instance of Directus.

- https://github.com/Nana2929/discord-daily-task-bot /202401/python
  - Side project: discord bot for daily-task reminders
# utils
- https://github.com/utomic-media/directus-dev-utils /GPLv3/202401/ts
  - helpful utils when developing directus extensions.
  - Add migrations from an extension

- https://github.com/sacconazzo/directus-cicd /MIT/202402/js
  - Back-end server with web interface (byDirectus)

- https://github.com/timio23/directus-operation-add-comment /202307/js
  - Add comments in a Directus Flow

- https://github.com/ctholho/qryo /202304/ts/inactive
  - Testing if offline first CRUD applications with Directus are possible
  - Qryo helps you build offline-first web apps. It concerns itself with server requests like CRUD REST calls or RPCs. 
  - Qryo is totally not functional yet. This is a proof of concept 
  - Stack: Tanstack/query, Nuxt and Directus
  - persist the mutation in IndexedDB

- https://github.com/erdemozveren/directus-realtime-extension /MIT/202201/js/inactive
  - Add realtime capabilities to your Directus App over WebSockets
  - 官方已支持此功能，没必要用第三方了
  - Any Pusher-maintained or compatible client can connect to it. You have total control of your channels (What to publish or who to authorize) with pure javascript that you can edit in your admin panel per channel.

- https://github.com/formfcw/directus-hook-library /GPLv3/202403/ts
  - A collection of customizable hooks for Directus. 
  - This is not an extension, but a library of scripts that could be used inside a Directus hook extension.

- https://github.com/xu4wang/directools /GPLv3/202309/python
  - A set of tools for using directus in real world projects. 
  - Managing roles, permissions, flows and operations as code.
  - The idea is to keep the settings in the Directus admin APP into human readable JSON files, so it can be version controlled and re-deployed.
# devops
- https://github.com/ECL-Web-Design/directus-template-sql /GPLv3/202402/json
  - Single sql dump for a simple directus template including routing, pages, forms, and utility flows

- https://github.com/u12206050/directus-rbac-sync /MIT/202310/ts
  - Hooks and CLI tool for exporting and importing Directus roles and permissions.
  - The file based approach is also useful for tracking changes using git.

- https://github.com/tractr/directus-sync /MIT/202403/ts
  - A CLI tool for synchronizing the schema and configuration of Directus across various environments.
  - By leveraging Directus's REST API, it aligns closely with the native actions performed within the application
  - Updates are granular, focusing on differential data changes rather than blunt table overwrites, which means only the necessary changes are applied, preserving the integrity and history of your data.
  - directus-sync organizes backups into multiple files, significantly improving readability and making it easier to track and review changes. 
  - directus-sync operates on a tagging system similar to Terraform, where each trackable element within Directus is assigned a unique synchronization identifier (SyncID). This system is key to enabling version control for the configurations and schema within Directus.

- https://github.com/bcc-code/directus-schema-sync /apache2/202402/ts
  - The better way to sync your Directus schema, configuration and selected data between environments.
  - Automatically export and import both the schema and data when you make changes via Directus or in the json data files

- https://github.com/hamilton-lima/directus-sandbox /MIT/202401/js
  - This is a collection of assets and solutions to Directus real life problems
  - The plan is if you need to remove data, do it by creating a script, or manually so the risk of loosing data is minimum.
# more
- https://github.com/directus-labs/examples /202301/js/archived
  - These frontend examples showcase how to integrate Directus JavaScript SDK, GraphQL, or official Directus plugins/modules with other frameworks in order to use Directus as the data source.
  - This repository is unmaintained

- https://github.com/codihaus/live-editor /MIT/202309/仅文档
  - https://live-editor-seven.vercel.app/
  - real-time frontend content editing for instant, seamless updates.
