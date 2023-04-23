---
title: lib-excel-tanstack-table-examples
tags: [examples, tanstack-table, toc]
created: 2021-07-20T12:42:45.044Z
modified: 2022-08-21T10:37:01.349Z
---

# lib-excel-tanstack-table-examples

# guide

- tips
  - react-table的问题在于没有成熟的使用案例，没有大公司案例支持，缺少样式主题、性能优化，特别是缺少在表格的单元格中显示图表的示例如ag-grid-charts
    - github最新的issues多维表格界面基于react-table实现
    - outline wiki使用了react-table和react-window
  - ✨ list和grid切换功能 需要自己实现

- usecase
  - rowy
  - 参考berry-admin
  - db浏览器、管理器

- dev-to
  - 基于css组件
  - 支持编辑
  - 支持import/export excel/csv，可参考habx-ui-table或mantain-table
  - collab，支持显示光标
  - more/rewrite
    - 重写ui-table
    - personal-kanban
    - pivot-table in v7
# popular-v8
- mantine/material-react-table /301Star/MIT/202212/ts
  - https://github.com/KevinVandy/material-react-table
    - https://www.material-react-table.com/
  - https://github.com/KevinVandy/mantine-react-table
    - https://www.mantine-react-table.com/
    - https://www.mantine-react-table.dev/
  - 依赖 mui5、emotion/styled、react-table.v8、react-virtual、match-sorter
  - 提供了group示例
  - A fully featured Material UI V5 implementation of Tanstack React Table V8
  - examples
    - [Aggregation and Grouping Example](https://www.material-react-table.com/docs/examples/aggregation-and-grouping)
    - [Remote Data Example](https://www.material-react-table.com/docs/examples/remote)
    - [React Query Example](https://www.material-react-table.com/docs/examples/react-query)
  - Inspired by material-table and the MUI X DataGrid
  - All internal Material UI components are easily customizable

- mantine-data-grid /117Star/MIT/202212/ts
  - https://github.com/Kuechlin/mantine-data-grid
  - https://kuechlin.github.io/mantine-data-grid/
  - 支持sort/filter/pagination，不支持group
  - 提供了一个类似storybook的属性开关工具，方便尝试示例各种交互
  - 依赖mantine、dayjs、transtack-virtual
  - Data Grid component with Mantine UI and react-table v8.
  - 样式非常友好

- mantine-datagrid /1Star/ISC/202208/ts/inactive
  - https://github.com/FabienDeborde/mantine-datagrid
  - https://mantine-datagrid.netlify.app/
  - A wrapper around React Table (TanStack Table v8) using Mantine.
  - I do not plan to really maintain or update this library

- https://github.com/Achaak/pikas-ui /MIT/ts
  - https://github.com/Achaak/pikas/tree/main/packages/ui/table
  - https://pikas-ui.vercel.app/components/table
  - Pikas-UI is a React UI library for building web applications with StitchesJS.
  - The library uses Stitches for styling and Radix for the accessibility.
  - table依赖dnd-kit、pikas-ui

- undb /20Star/AGPLv3/202304/ts
  - https://github.com/undb-xyz/undb
  - https://www.undb.xyz/
  - https://docs.undb.xyz/
  - Private first, unified, self-hosted no code database.
  - 前端依赖 undb, dnd-kit、tanstack-table, react-redux, emotion, @loadable/component, jotai, react-hook-form, trpc
    - 前端正迁移到svelte
  - 后端依赖 nestjs、mikro-orm、trpc、undb

- https://github.com/klassenl/react-grid /202210/ts/单击编辑单元格
  - https://subtle-muffin-372579.netlify.app/
  - Prototype for react table v8 editable table
  - Keyboard cell navigation Click or enter to edit data Error tooltips

- https://github.com/DavidCodina/tanstack-table-v8-demo-2023
  - https://davidcodina.github.io/tanstack-table-v8-demo-2023/
  - A configurable abstraction of TanStack Table v8.

- material-grid /2Star/MIT/202208/ts/inactive
  - https://github.com/zmrl010/material-grid
  - Feature-rich datagrid component
  - 依赖 mui5、emotion

- react-crud /2Star/MIT/202208/ts
  - https://github.com/sefirosweb/react-crud
  - https://sefirosweb.github.io/react-crud
  - It´s a React compononet to be used at multiple projets
  - 依赖tanstack-table/query、react-bootstrap
  - Normally you are interested to have a CRUD system for a lot of things, usually you want to make a fast and simple CRUD system
  - It is made by bootstrap (react-bootstrap) you can modify colors and styles for these components
  - ref
    - https://github.com/toofaniCoder/react-table-8.5-crud

- https://github.com/bilalzafarr0001/server-side-data-pagination-filtering-sorting-using-react-table-tanstack /v7
  - implement Pagination(Offset based and Cursor based) with Mongoose and Nodejs(Handling 1M records)

- https://github.com/Serkan-Ucakcioglu/React-Query-React-Table-Pagination /v7
  - Tanstack react query and react table and pagination.

- https://github.com/bgrins/data-ui-tests
  - https://bgrins.github.io/data-ui-tests/
  - benchmarks with vanilla-table/handsontable, revo-grid
- https://github.com/ganeshmani/react-ag-data-grid
  - https://react-ag-data-grid.vercel.app/
  - Using ag-grid-react in React: Guide and Alternatives

- @uidu/table /19Star/MIT/202212/ts/react
  - https://github.com/uidu-org/guidu
  - https://uidu.design/
  - https://uidu.design/packages/data/dashlets
  - https://github.com/uidu-org/guidu/tree/main/packages/data/table
    - 依赖react-table.v7、react-virtual、styled-components5、react-intl5、@uidu/popup
  - Guidu is uidu's design system library
    - 完全复制了atlassian-editor，并将组件替换成了自己的design system
    - dashlet会不会也是复制的？
    - 提供了专门的数据类别组件：list, table, data manager, data views, timeline, dashlet, dashboard
    - These components are Atlassian Design Guidelines(ADG) compliant
  - https://github.com/uidu-org/guidu/tree/main/packages/data/dashlets
    - 依赖@uidu/table、styled-components、@amcharts/amcharts4、d3、@cubejs-client/react、react-table、twin.macro

- https://github.com/devsayog/ui-dashboard
  - https://ui-dahboard.vercel.app/
  - Dashboard build with NextJs with kanban and calendar apps.
  - 依赖dnd-kit、headlessui、zustand、chartjs
  - https://github.com/devsayog/kanban-board /react-dnd
  - https://github.com/devsayog/MovieFLix
- https://github.com/devsayog/nextjs-ecommerce
  - https://fashion-lac.vercel.app/
  - Nextjs ecommerce is fullstack ecommerce web app with admin panel.

- https://github.com/zendricom/tableus /inactive
  - A react library for rendering highly configurable tables.
  - intended to be integrated fully with your backend to deliver tables with sorting, filtering and pagination.
  - Tableus does not state any requirements on your preferred UI (bootstrap, material UI, etc.) or backend API (REST, GraphQL, etc.), by externalizing those into seperate modules called fetchers and UIs.
  - ref
    - https://github.com/zendricom/tableus-ui-bootstrap5
    - https://github.com/zendricom/tableus-fetcher-laravel-rest

- https://github.com/HeartLee/table-tanstack /202212/ts/starter/wip
  - 使用tanstack table 开发一个满足设计体系定制、性能优秀的Table组件
  - 基于 Ant Design V5 and TanStack Table V8

- https://github.com/sajermann/CustomReactTable
  - Tailwind

- https://github.com/angelfishapp/virtual-tables
  - 仅依赖tanstack-virtual，示例简洁 Test for virtualized tables 

- https://github.com/odpf/apsara
  - https://odpf.github.io/apsara/
  - a UI design system for react written on top of ant design to power the projects for the open data platform.
  - 数据组件不多，表格、表单

- merico-dev-table /15Star/apache2/202212/ts
  - https://github.com/merico-dev/table
  - Dev Table offers a most flexible and powerful low-code data workflow loved by developers.
  - Build your own data presentation using SQL and multiple data sources including big data.

- https://github.com/manuel-mauky/tanstack-table-core-example
  - Trying out TanStack Table without frameworks but only standard HTML and web components

- https://github.com/niloysikdar/react-table
  - example of handling Tabular Data with Advanced Filters, Sorting and Optimizations in React
  - 不依赖tanstack-table，但展示了数据处理方法
  - 依赖tanstack-query、zustand、mui5
# design-system-ui-v8
- https://github.com/saas-js/saas-ui/tree/main/packages/saas-ui-data-table
  - https://saas-ui.dev/docs/components/data-display/data-table
  - A DataTable component for Chakra UI, build with react-table.
  - 功能过于简单
  - 文档样式非常好

- https://github.com/netdata/netdata-ui/tree/master/src/components/table  /js
  - https://netdata.github.io/netdata-ui/
  - 提供了一套设计系统的ui，table实现过于简单
  - Table component Implementation based on react-table lib.
  - Virtualized settings are mostly replicating react-window
  - Requires numeric width and height of the container.

- https://github.com/blockchain/constellation/blob/development/packages/constellation
  - 依赖tanstack-table、radix-ui、headlessui、tailwindcss

- https://github.com/provectus/kafka-ui
  - Open-Source Web UI for Apache Kafka Management

- https://github.com/Localitos/pluto/blob/main/packages/components/src/components/Table/Table.tsx
  - https://pluto-storybook.localyze.com/?path=/docs/components-table--default
- https://github.com/ltht-epr/ltht-react
  - https://ltht-epr.github.io/ltht-react
- https://github.com/coveo/plasma
  - https://plasma.coveo.com/layout/Table
- https://github.com/GetJobber/atlantis
  - Atlantis is a design system for Jobber. The primary objective for Atlantis is to provide a system of reusable components t

- https://github.com/theodorusclarence/aether-design-system
  - https://aether.thcl.dev/sandbox/table

- https://github.com/owenchang1992/Headless-Table-Example
  - Integrate TanStack Table with Chakra UI

- https://github.com/zakodium-oss/react-science
  - React components and tools to build scientific applications.
# examples-v8
- https://github.com/rizqitsani/learn-tanstack-table
  - http://learn-tanstack-table.vercel.app/
  - sort/filter/pagination
- https://github.com/f-starace/Tailwind-Tanstack-Table
  -  Added striped, resizable, condensed, filterGlobal, filterColumns, pagination, striped, footer, verticalLines, bordered and sticky property to table props

- https://github.com/BlackHatMan/Table
  - Table on React with Mui

- https://github.com/huskice/imdb
  - https://imdb-six.vercel.app/
  - MovieDB, nextjs

- https://github.com/freewind-demos/typescript-react-data-grid-table-demo
  - Define a wrapper component for @tanstack/react-table
- https://github.com/polyms/vite-boilerplate
  - A starter for React with Typescript with the fast Vite and all static code testing with Eslint and formatting with Prettier.

- https://github.com/lawrencecchen/planetsheet /202207/ts/inactive
  - https://planetsheet.vercel.app/
  - 依赖 glide-data-grid、radix-ui、trpc、knex、react-query.v3
  - A SQL editor designed for developers and content editors.
  - Today, Planetsheet is an (early) alternative to npx prisma studio, Postico, and TablePlus. 
  - In the future, Planetsheet will give you (and your content editors) an interface as intuitive as Airtable and Google Sheets, while letting you (as a developer) use powerful databases underneath.

- https://github.com/Rayologist/next-template
  - NextJS template: Typescript, Mantine, Zod, React Hook Form, @tanstack/react-table, and @tanstack/react-virtual

- https://github.com/Avila-Tek/full-stack-template /202212/ts
  - A Template for a Full Stack Application for Avila Tek Engineers
  - Turborepo starter

- https://github.com/FreeWall/dbfy /202212/ts
  - http://dbfy.vercel.app/
  - database editor
- https://github.com/jkcorrea/blink-sql
  - open-source SQL database client with a focus on rich data & collaboration

- https://github.com/rvdende/surrealreact
  - SurrealDB explorer UI written in react.
- https://github.com/InformaticsMatters/squonk2-data-manager-ui
  - Web UI for the Squonk Data Manager
- https://github.com/brimdata/brim
  - Zui is a powerful desktop application for exploring and working with data. 
  - The official front-end to the Zed lake.

- https://github.com/DefiLlama/defillama-app
  - http://defillama-ui-git-main-defillama-team.vercel.app/

- https://github.com/Gitseong96/query-Movie-List
  - api https://www.kobis.or.kr/kobisopenapi/webservice/rest

- https://github.com/dogukanakkaya/next-boilerplate
  - Next Auth Prisma tRPC Tailwind React Table React Select

- teamManagement /6Star/NALic/202208/js/MERN
  - https://github.com/sayinmehmet47/teamManagement
  - https://team-management12.herokuapp.com/
  - Team management app with authentication(MERN project)
  - 依赖 redux、reactstrap、socket.io

- https://github.com/pankaspe/Azansca-project
  - http://azansca-project.vercel.app/
  - Azansca.it project bootstrapped with Next js & Chakra UI.
  - 简洁且有设计感，绿色主题

- https://github.com/lqd1434/MatexPro
  - 基于electron的万能工具软件

- https://github.com/ebonstar/dreamlight-recipes
  - Recipe book for Dreamlight Valley

- https://github.com/joangavelan/corteza
  - https://corteza-book-tracker.vercel.app/
  - An app that works with your local storage to keep track of the book(s) you read, save notes, ideas and more.

- https://github.com/wan6sta/cards-quiz
  - https://cards-quiz.vercel.app/

- https://github.com/Danzo7/doctorIO
  - medical management software to improve the connectivity between doctors and patients
  - Clinicord-Client is a desktop/web compatible software. It is an offline software that can connect to a Clinicord-server instance on a LAN to enable it features.
  - 依赖 redux-toolkit、electron、localforage、react-beautiful-dnd、redux-persist

- https://github.com/Saszr/vite-react-chill
  - a react app with Vite / TypeScript / Chakra-UI / Redux Toolkit (include RTK Query) setup.

- https://github.com/Dev-CasperTheGhost/earnings-tracker
  - https://earnings.caspertheghost.me/
  - track your income and expenses with a simple chart and a simple interface.

- https://github.com/RafaelGB/obsidian-db-folder
  - Obsidian Plugin to Allow Notion like database based on folders

- https://github.com/tourist/coinscan-front
  - https://coinscan-front-git-dev-tourist.vercel.app/
  - 暗黑主题，设计感很强

- https://github.com/kuroski/github-issue-viewer
  - https://github-issue-viewer.up.railway.app/
  - A Github issue viewer apps

- https://github.com/m1guelsb/deals-cms
  - SaaS CMS App for manage costumers, deals and tasks, using as backend a json-server with jwt auth and relationships.

- https://github.com/Reza1878/dts-task-fe
  - https://dts-task-fe.vercel.app/
  - 标准的crud界面

- https://github.com/opossum-tool/OpossumUI
  - A light-weight app to audit and inventory large codebases for open source license compliance.

- https://github.com/aoigj100a/react-table-demo
  - react-table v8、chakra-ui

- https://github.com/Mallet1/tanstack-editable-data
  - https://codesandbox.io/s/github/Mallet1/tanstack-editable-data

- https://github.com/sajclarke/react-table-8-rowactions
  - an example of using Tanstack table v8 with row action column displaying Edit and Delete buttons

- https://github.com/evriyanaindrasaputra/react-dashboard
  - https://react-dashboard-pi-ten.vercel.app/
  - Tailwind Css Headless UI Tanstack Query Tanstack Table React Hook Form

- https://github.com/iambinodstha/react-salesforce-admin-ui
  - This application cover admin UI with highchart, tailwindcss, salesforce ui
  - Integration with Lightning Design System

- https://github.com/grkmtsn/smart-table
  - A minimal React Vite starter template.

- https://github.com/wooboo/the-playform
  - https://the-playform.vercel.app/admin/dashboard
  - 提供了典型的仪表板示例
  - 依赖 headlessui、trpc、recharts、prisma、next-auth

- https://github.com/freewind-demos/typescript-tanstack-react-table-global-filter-demo
  - ts+react

- https://github.com/chcoomilk/himitsu
  - https://himitsu-note.netlify.app/
  - A React based "pastebin" web app project

- https://github.com/hmaiermack/daydash /202212/ts/t3-stack
  - Create T3 App

- https://github.com/esponges/t3-ecommerce
  - lets try to build an ecommerce site with t3

- https://github.com/mikeKorakakis/t3Boilerplate
  - Create T3 App
  - https://github.com/tanushm31/react-table-test

- https://github.com/thirdweb-dev/dashboard
  - https://thirdweb.com/
  - full source for all of thirdweb.com and the thirdweb dashboard.
  - The complete web3 development framework
- https://github.com/encacap/baolocre_dashboard
  - https://baolocre-dashboard-dev.vercel.app/auth/login

- https://github.com/sammykisina/charity /202212/ts/t3-stack
  - http://charity-zeta.vercel.app/
  - A Charity Application To Be Used By A Charity Organization To Receive And Management Donations From Members Of The Public
  - 依赖trpc、next、tailwind

- https://github.com/umccr/elsa-data /202212/ts
  - Genomic data sharing support software ("let the data go").

- https://github.com/flipt-io/flipt /go
  - https://flipt.io/
  - open source, self-hosted feature flag solution

- https://github.com/reactioncommerce/kinetic
  - Kinetic introduces a suite of opinionated admin tools that internal teams can use to manage and run their stores on Open Commerce.

- https://github.com/mbrinkl/santorini
  - https://santorini.onrender.com/
  - Santorini Board Game Online with boardgame.io and three.js
# more-table-repos
- https://github.com/cjroth/vertex-solid
  - built a Virtualized table with @solid_js and @tan_stack virtual (also playing with @zag_js and Hope UI!):
  - It's showing the max number of rows that Chrome will support due to max element height.

- react-table /1Star/ISC/202212/ts
  - https://github.com/rsrv1/react-table
  - react data-table implementation for server returned dynamic data source

- https://github.com/zakodium-oss/react-science
  - https://react-science.pages.dev/
  - React components and tools to build scientific applications.
  - https://github.com/zakodium-oss/react-plot
    - Library of React components to render SVG 2D plots.

- https://github.com/InformaticsMatters/squonk2-data-manager-ui
  - http://data-manager-ui.vercel.app/
  - Web UI for the Squonk Data Manager
  - https://github.com/InformaticsMatters/squonk
    - Squonk, both the Squonk Platform and the Squonk Computational Notebook.

- https://github.com/tovyblox/tovy
  - Tovy is an open source staff management platform inspired by Hyra. 

- https://github.com/afk-mario/federike /202212/js
  - Web app to manage your mastodon account

- https://github.com/Elduwani/cashbar-admin-demo
- https://github.com/AbdQaadir/movie-app

- https://github.com/baptisteArno/typebot.io
  - https://typebot.io/
  - Typebot is an open-source alternative to Landbot. 
  - a conversational form builder that you can self-host.
  - builder依赖slate-react、tanstack-table
  - It allows you to create conversational apps/forms (Lead qualification, Product launch, User onboarding, Customer support), embed them anywhere on your web/mobile apps, and collect results in real-time.
