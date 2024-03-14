---
title: lib-saas-directus-examples
tags: [cms, directus, examples]
created: 2024-03-14T13:50:55.256Z
modified: 2024-03-14T13:51:11.429Z
---

# lib-saas-directus-examples

# guide

- https://github.com/directus-labs/awesome-directus
  - Extensions, Examples/Showcases

- [Directus extensions](https://directusextensions.com/browse)
  - Directus Extensions includes all Directus Extensions available on npm that adhere to the `directus-extension-*` naming strategy
# popular
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

- https://github.com/gremo/react-directus /ISC/202403/ts
  - A set of React components and utilities for Directus
  - The `<DirectusProvider>` component makes the Directus JavaScript SDK available to any nested components that need to access it.

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
# extensions
- https://github.com/resauce-dev/directus-image-scout /GPLv3/202310/js/vue
  - A clean interface is provided allowing you to search multiple online image libraries to find images that suit your needs.
  - Confirmed Support for v10-10.6.1

- https://github.com/rezo-labs/directus-extension-schema-management-module /202308/vue
  - Tired of creating the same collection all over again? This module extension can make it easier to share schema between Directus instances. 
  - Simply copy the schema code from one Directus and paste it to the other

- https://github.com/u12206050/directus-extension-global-search /MIT/202311/ts/vue
  - A module for searching across multiple collections at once
  - returning results to allow you to navigate directly to the item page.

- https://github.com/dimitrov-adrian/directus-extension-searchsync /MIT/202112/js
  - Simple Directus 9 extension that sync content with remote search engine
  - Supported engines: MeiliSearch, ElasticSearch, Algolia

- https://github.com/utomic-media/directus-extension-field-actions /GPLv3/202403/ts/vue
  - Add link & copy to clipboard functionalities to your directus fields. 
  - Supports interfaces as well as displays.
  - The actions can be performed by a button next to the items or by clicking on the value. 

- https://github.com/codihaus/directus-extension-grid-layout /202312/ts/vue
  - https://directus-extension.codihaus.io/
  - Directus Extension to display items as grid with customizable, flexible display.
  - allows users to present data in a grid layout 

- https://github.com/shocota/directus-extension-board-layout /GPLv3/202301/ts/vue/inactive
  - a layout extension for Directus, that allows you to display items in a Kanban-style layout.

- https://github.com/seymoe/directus-extension-vgrid-interface /MIT/202402/js/vue
  - A directus extension with @revolist/vue3-datagrid, specify fixed columns to generate an editable table field.

- https://github.com/u12206050/directus-extension-api-viewer-module /MIT/202310/vue
  - A module for displaying your Directus api documentation directly within the App

- https://github.com/dimitrov-adrian/directus-extension-wpslug-interface /GPLv3/202301/ts/vue
  - WordPress alike slug interface for 
  - Directus 9

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

- https://github.com/sacconazzo/directus-extension-api-docs /MIT/202310/ts
  - Directus Extension to include a Swagger interface and custom endpoints definitions

## flows

- https://github.com/baguse/directus-extension-flow-manager /202311/ts/vue
  - A directus custom module extension for managing directus flow includes backup/restore, duplication and grouping the flow.

- https://github.com/euryecetelecom/directus-extension-operation-download-store-file /MIT/202403/ts
  - Directus flows operation extension allowing to download and save external files. 
  - Authentication via headers is supported. 
  - Can be used to download huge files without storing them locally or in RAM as it is based on axios Stream capabilities.

- https://github.com/ComfortablyCoding/directus-operation-slugify /MIT/202403/ts
  - A Directus slugify operation for Flows. 
  - It automatically handles most major languages, including German (umlauts), Vietnamese, Arabic, Russian, and more.
  - https://github.com/muratgozel/directus-operation-slugify

- https://github.com/karamokoisrael/directus-extension-flow2pdf /202402/js/vue
  - The flow2pdf extension is a bundle that allows directus to print data from flow results and liquid templates.
  - The extension will add a new interface and endpoint to your directus instance. All configurations are available in the pdf manager interface.

## ui

- https://github.com/formfcw/directus-extension-flexible-editor /GPLv3/202403/ts
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

## db

- https://github.com/7span/directus-extension-custom-query-panel /202311/js/vue
  - easy to use insight panel to see custom raw query data from database
  - Execute custom SQL queries directly from the panel.
  - Display query results in a simple tabular structure for easy readability.

- https://github.com/bcc-code/directus-sql-query-panel /MIT/202402/ts/vue
  - Insights Panel for viewing results for dynamic sql queries

- https://github.com/ChappIO/directus-extension-schema-merge /202402/ts
  - This extension adds the cli command schema-merge to the directus except it uses a modified .yml format which should cause fewer merge conflicts during `git merge`s.

- https://github.com/FireboltCasters/directus-extension-auto-backup /202402/js
  - This extension automatically makes backups of your database for you.
  - Automatically backups (with directus flows)
  - 支持SQLite

## utils

- https://github.com/br41nslug/directus-extension-block-endpoints /MIT/202403/ts
  - this extension will allow you to block any endpoint with a custom message.

- https://github.com/Attacler/directus-extension-jsc-encrypt /202301/ts/inactive
  - This package is designed for encrypting and decrypting data within Directus. 
  - It ensures that data is always stored in an encrypted form inside your database, and targets specific collection fields.

- https://github.com/Deveosys/directus-extension-public-folders /GPLv3/202402/ts
  - This Directus extension grants public read access to all folders created with the name 'public' or under a 'public' folder. It also cleans up permissions when a folder is deleted.

## integrations

- https://github.com/Attacler/TextToAnything-Directus /202402/ts/vue
  - This extension allows you to generate PDFs, QRCodes and Barcodes within Directus trough TextToAnyThing API

- https://github.com/Intevel/directus-logsnag /MIT/202207/ts/inactive
  - Get notified when something in Directus happens.
  - LogSnag is a simple event tracking tool. It helps you keep track what is happening within your projects, creates custom feeds, and notifies you of important events.
  - 依赖LogSnag在线服务
# starter
- https://github.com/shubshinde/NexTusPlate /MIT/202402/ts
  - Admin Dashboard Starter with Directus, Nextjs 14, NextAuth and ShadCn UI
  - Authentication with NextAuth supports Social logins and email logins

- https://github.com/linefusion/directus-container /MIT/202402/ts
  - Directus Docker Images
  - Alternative container image for Directus with support for extensions.
# examples
- https://github.com/NxtNinja/AlteraX /202402/ts
  - a full stack social media application built with NextJs as frontend and Directus as Backend

- https://github.com/d135-1r43/bandlinks /202401/js/svelte
  - A simple link tree for bands with Directus as backend
  - written in Svelte with SvelteKit and uses Tailwind with DaisyUI. 
  - All content is fetched from a self-hosted instance of Directus.
# utils
- https://github.com/ctholho/qryo /202304/ts/inactive
  - Testing if offline first CRUD applications with Directus are possible
  - Qryo helps you build offline-first web apps. It concerns itself with server requests like CRUD REST calls or RPCs. 
  - Qryo is totally not functional yet. This is a proof of concept 
  - Stack: Tanstack/query, Nuxt and Directus
  - persist the mutation in IndexedDB

- https://github.com/tractr/directus-sync /MIT/202403/ts
  - A CLI tool for synchronizing the schema and configuration of Directus across various environments.
  - By leveraging Directus's REST API, it aligns closely with the native actions performed within the application
  - Updates are granular, focusing on differential data changes rather than blunt table overwrites, which means only the necessary changes are applied, preserving the integrity and history of your data.
  - directus-sync organizes backups into multiple files, significantly improving readability and making it easier to track and review changes. 
  - directus-sync operates on a tagging system similar to Terraform, where each trackable element within Directus is assigned a unique synchronization identifier (SyncID). This system is key to enabling version control for the configurations and schema within Directus.

- https://github.com/bcc-code/directus-schema-sync /apache2/202402/ts
  - The better way to sync your Directus schema, configuration and selected data between environments.
  - Automatically export and import both the schema and data when you make changes via Directus or in the json data files

- https://github.com/fabian-hiller/directus-sdk /202306/ts
  - This repository can be seen as an alternative proposal to the current Directus SDK.
  - Modular design
  - This SDK builds on existing web APIs like the Fetch API and therefore has no dependencies and can run in any environment. 

- https://github.com/erdemozveren/directus-realtime-extension /MIT/202201/js/inactive
  - Add realtime capabilities to your Directus App over WebSockets
  - 官方已支持此功能，没必要用第三方了
  - Any Pusher-maintained or compatible client can connect to it. You have total control of your channels (What to publish or who to authorize) with pure javascript that you can edit in your admin panel per channel.

- https://github.com/formfcw/directus-hook-library /GPLv3/202403/ts
  - A collection of customizable hooks for Directus. 
  - This is not an extension, but a library of scripts that could be used inside a Directus hook extension.

- https://github.com/directus-labs/directus-templates /202402
  - Community maintained Directus instance templates to help you jump start your next project.
  - npx directus-template-cli@latest apply
# more
