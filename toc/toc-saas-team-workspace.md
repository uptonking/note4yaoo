---
title: toc-saas-team-workspace
tags: [collaboration, saas, team, toc]
created: 2023-02-07T17:37:17.711Z
modified: 2023-02-07T17:38:05.336Z
---

# toc-saas-team-workspace

> workplace, project management
> team, admin-members

# guide
- tips-team
  - team结合紧密的是chat、project
  - 实时场景案例，如 聊天/游戏

- kanban
  - 看板的ui状态和样式很容易实现
  - 看板的数据模型及持久化要考虑兼容主流看板及任务类产品，如trello、notion-database

- alternatives
  - jira, trello, linear
  - focalboard, nocodb
  - 可以从主流产品的issues/discussions里面找替代品
  - 参考github，实现 repo + issues-forum + gitter-im + proj-mgmt + pr + cicd
  - [10 Best Open Source Trello Alternatives](https://rigorousthemes.com/blog/best-open-source-trello-alternatives/)

- tips
  - 聊天类产品，将聊天室的内容替换成编辑器就成了协同类产品
# popular
- growi /1.2kStar/MIT/202403/ts/remark/偏向文档管理
  - https://github.com/weseek/growi
  - https://docs.growi.org/en/guide/
  - https://demo.growi.org/
  - Team collaboration software using markdown
  - 依赖 express、mongoose、es7、redis、nextjs、swr、i18next、remark-gfm、yjs、y-mongodb-provider、handsontable.v6、react-dnd、react-markdown
  - Create hierarchical pages with markdown
  - Simultaneously edit with multiple people by HackMD(CodiMD) integration
  - 支持notification
  - 支持显示正在浏览或编辑的用户
  - 支持显示编辑历史history
  - Support Authentication with LDAP / Active Directory, OAuth
  - Slack/Mattermost, IFTTT Integration
  - You can find plugins from npm or github
  - 各种集成

- crowi /1.1kStar/MIT/202211/ts/inactive
  - https://github.com/crowi/crowi
  - http://demo.crowi.wiki/
  - The Markdown Wiki - Empower the team with sharing your knowledge
  - URL Based Page Tree
  - pages that end with slashes (/) are automatically generated as list views. 
  - Useful timeline list view
  - 功能和样式都很普通
  - 依赖mongoose、es、redis、swig、Elasticsearch(optional)

- https://github.com/makeplane/plane /AGPLv3/python/ts
  - https://plane.so/
  - Open Source JIRA, Linear and Height Alternative.
  - 后端依赖django、djangorestframework
  - 前端依赖blueprintjs、nivo-chart、remirror、nextjs、swr
  - https://github.com/makeplane/plane-mobile /dart

- https://github.com/JordanKnott/taskcafe /MIT/202209/go/ts/inactive
  - open source project management tool with Kanban boards
  - Manage tasks through a Kanban board interface (set due dates, labels, add checklists)
  - Task comments and activity
  - One of the primary goals of Taskcafe is to provide a project management tool that I personally enjoy using

- https://github.com/ferdium/ferdium-app /2.2kStar/apache2/202401/ts
  - https://ferdium.org/
  - All your services in one place, built by the community
  - Hard-fork of Franz, adding awesome features and removing unwanted ones.
  - 依赖electron-window-state、immutable-js.v4、mobx-react、sqlite3、@adonisjs/ace/auth/lucid
  - a desktop app that helps you organize how you use your favourite apps by combining them into one application. 
  - It is based on Franz - a software already used by thousands of people - with the difference that Ferdium gives you many additional features and doesn't restrict its usage
  - Ferdium is compatible with your existing Franz account, so you can continue right where you left off

- https://github.com/meetfranz/franz /4.4kStar/apachew/202308/js
  - https://meetfranz.com/
  - free messaging app for services like WhatsApp, Slack, Messenger and many more

- https://github.com/netless-io/netless-app /MIT/202312/ts/svelte
  - https://netless-io.github.io/netless-app
  - Official Apps for the Agora Interactive Whiteboard.
  - https://github.com/netless-io/flat /MIT/202401/ts
    - https://flat.whiteboard.agora.io/
    - Project flat is the Web, Windows and macOS client of Agora Flat open source classroom.
  - https://github.com/netless-io/flat-server
    - Node.js server for the Agora Flat open source classroom.
# microsoft-teams/org
- https://github.com/xiweicheng/tms /MIT/202309/js/java
  - TMS是基于频道模式的团队沟通协作+轻量级任务看板，支持mardown、富文本、在线表格和思维导图的团队博文wiki，i18n国际化翻译管理的响应式web开源团队协作系统。

- https://github.com/bissbr01/Command-project-management /202303/ts-fe/inactive
  - A Scrum Management App for teams
  - 依赖reduxjs-toolkit、mantine、dnd-kit、formik
  - 支持create-teams
  - https://github.com/bissbr01/Command-backend /js-be
    - 依赖sequelize6
    - A containerized REST API for the Command project management app.

- https://github.com/vishwajeetraj11/projectboard /MIT/202308/ts/inactive/样式友好
  - https://github.com/vishwajeetraj11/projectboard-backend /202205/js
  - A project management application that allows you to track tasks process
  - 后端js，mongoose
  - 前端ts，redux， react-markdown-editor, react-beautiful-dnd
  - 界面类似linear，支持看板
  - Login/Signup to Auth0

- https://github.com/bennymeier/mern-stack-project-management /202111/ts/js
  - A project management platform built with the MERN-Stack.
  - Jira clone with MongoDB, Express, React and Node.js
  - 后端js，mongoose
  - 前端ts，redux、semantic-ui、react-beautiful-dnd

- https://github.com/linagora/Twake /php
  - Open-source alternative to Microsoft Teams
  - Twake - The Open Digital Workplace
  - Team chat
  - File Storage
  - Team Calendar
  - Task Management
  - Video call and conferencing
  - Real time document collaboration
  - [Slack, gDrive and Trello have a self-hosted baby : Twake : selfhosted](https://www.reddit.com/r/selfhosted/comments/q1pmd7/slack_gdrive_and_trello_have_a_selfhosted_baby/)
    - Frontend is in React and backend in PHP.

- https://github.com/ever-co/ever-teams /AGPLv3/202403/ts
  - https://app.ever.team/
  - Open Work and Project Management Platform
  - Projects / Tasks & Issues Management
  - Ever® Teams™ Platform is built on top of our Business Management Platform (ERP/CRM/HRM) - Ever® Gauzy™ Platform
  - https://github.com/ever-co/ever-gauzy /ts
    - https://gauzy.co/
    - Open-Source Business Management Platform (ERP/CRM/HRM)

- https://github.com/monicahq/monica /AGPLv3/202406/php/vue/inactive
  - https://www.monicahq.com/
  - Open source personal CRM
  - https://www.officelife.io/
# project-management
- https://github.com/jacobrdz77/selfwork /MIT/202402/ts
  - https://selfwork.vercel.app/
  - A project management system for small teams and freelancers.
  - 依赖prisma、next、tanstack-query、zustand
  - Organize your projects and members in different workspaces you create.
  - Full CRUD functionality for projects, clients, sections, tasks, and workspaces.
  - Use intigrated Excalidraw to create diagrams in the sketch view for each project
  - Allows you to log in and register using Google.
  - npx prisma migrate dev --name init
  - npm run seed

- https://github.com/rcamach7/project-management-app /202302/ts/inactive
  - https://project-management-app-eight.vercel.app/
  - Project management application, similar to that of Trello or Jira.
  - 依赖next-auth、mongoose、mui5，不支持拖拽
  - Utilized NextAuth to authenticate users and store their data in a MongoDB database
  - 暗黑主题

- https://github.com/pooridev/Todoooze
  - https://todooooze.vercel.app/
  - minimal project management app, powered by Next.js and Typescript
  - 依赖trpc、next、reduxjs-toolkit、recoil、react-query
  - 样式友好

- vikunja
  - https://vikunja.io/
  - open-source, self-hostable to-do app.
  - https://kolaente.dev/vikunja/frontend /vue
  - web frontend for Vikunja, written in Vue.js.
  - https://kolaente.dev/vikunja/api /go

- https://github.com/climech/grit /go
  - an experimental personal task manager that represents tasks as nodes of a multitree, a class of directed acyclic graphs. 
  - The structure enables the subdivision of tasks

- https://github.com/opf/openproject /GPLv3/202402/ruby
  - https://www.openproject.org/
  - the leading open source project management software

- https://github.com/hcengineering/platform /EPLv2/202404/ts/svelte/Huly
  - https://huly.io/
  - All-in-One Project Management Platform (alternative to Linear, Jira, Slack, Notion, Motion)
  - a robust framework designed to accelerate the development of business applications, such as CRM systems. 
  - This repository includes several applications, such as Chat, Project Management, CRM, HRM, and ATS. 
  - Various teams are building products on top of the Platform, including Huly and TraceX.

- https://github.com/marcelovicentegc/octosync /MIT/202105/ts/inactive
  - An open-source solution to keep Github and Jira issues synchronized. 
  - An alternative to Exalate and Unito.
  - Sync bi-directionally: issue creation/closing/comments

- https://github.com/johnny-estrada/issue-tracker /202403/ts/依赖少
  - Klarity is an issue tracker web application built with MySQL, React, TypeScript, Node.js, Express, and Tailwind CSS. 
  - It provides a platform for managing and tracking project issues, facilitating collaboration and organization within teams
  - 依赖express、sequelize.v6、mysql2、jsonwebtoken、@headlessui/react、@reduxjs/toolkit、recharts2、tailwind-merge
# user/permissions/scrum/Inventory
- https://github.com/pure-admin/pure-admin-backend /ts/echarts
  - pure-admin官方后端
  - 依赖express、mysql，未使用orm
  - https://github.com/pure-admin/pure-admin-thin
    - 基于 vue-pure-admin 官方精简版
    - 提供了权限管理
  - https://github.com/pure-admin/vue-pure-admin
    - Vue3+Vite4+Element-Plus+TypeScript编写的一款后台管理系统，兼容移动端

- https://github.com/shrihari-prakash/liquid
  - Seamless authentication and user management APIs for your projects based on TypeScript, MongoDB and Redis.
  - open source TypeScript implementation of oauthjs/node-oauth2-server based Mongo DB and Redis with user sign up and login
  - you typically find that you are writing the login, account creation and authentication logic over and over again. This repository provides a plug and play boilerplate

- https://github.com/tuan3w/linearapp_clone
  - 依赖material-ui、redux4、styled-components、tailwindcss、rich-markdown-editor
  - 基本可用，且实现了列表组件和看板组件，但编辑器基本未修改

- https://github.com/code-pilots/magner /vue
  - Universal admin panel magnetic to any backend. 
  - Supports authentication, role management, entities view, creation, edition and deletion. I18n, infinitely nested layout and custom components
  - Magner provides a set of tools to bootstrap an admin panel website built with Vue 3 and Element Plus. 
  - All you need to do is writing JSON configurations and backend connectors.

- https://github.com/curefit/react-crux
  - https://curefit.github.io/react-crux-examples
  - a simple to use client side library to create UI for CRUD operations on server side entities.
  - CRUX reads json config and creates a React Component that you can add to your app.
  - Since its a client side library, it is completely agnostic to server side tech stack.
# kanban/board
- focalboard /10.3kStar/AGPL-src + MIT-bin/202203/ts/go/偏看板/参考前端/squirrel-sql-builder
  - https://github.com/mattermost/focalboard
  - https://www.focalboard.com/
  - an open source, multilingual, self-hosted project management tool that's an alternative to Trello, Notion, and Asana.
  - ❓ 用户建表时，似乎没有在db中建表
  - 前端依赖 @reduxjs/toolkit、@tippyjs/react、draft-js、@fullcalendar/react、imagemin-svgo、marked、moment、nanoevents、react-dnd.v14、react-hot-keys、react-intl、react-router-dom.v5
  - 示例使用sqlite

- https://github.com/Fredkiss3/thullo
  - https://thullo.fredkiss.dev/dashboard
  - A Trello Clone
  - 后端依赖express、tsyringe(IoC)、mongoose
  - 前端依赖dnd-kit、react-beautiful-dnd、react-query、headlessui
  - 样式友好

- https://github.com/kanban-org/kanban-board /202402/js
  - https://www.kanban.live/
  - full-stack Kanban task management app
  - 依赖Sequelize

- https://github.com/knowankit/trello-clone /ts
  - Built with Nextjs framework with Typescript and Chakra UI library with support from MongoDB
  - Login/Register with JWT token authentication

- https://github.com/oldboyxx/jira_clone /js/未使用组件库
  - https://jira.ivorreic.com/project/board
  - simplified Jira clone built with React/Babel (Client), and Node/TypeScript (API)
  - 未实现用户组织管理
  - 后端ts依赖express、typeorm、pg、jwt
  - 前端js依赖react-beautiful-dnd、quill、sweet-pubsub
  - 样式友好

- https://github.com/lyn-eva/jira-clone
  - Project management web app for agile teams built with REST architecture
  - 依赖 RTK Query, Tailwindcss, Express, MySQL, Prisma

- https://github.com/automerge/trellis /js/inactive
  - Trello clone/sample app for Automerge persistence library
  - Trellis is a Trello clone built as an Electron desktop application. 

- https://github.com/arthurfigueiredo/Kanban.js /MIT/js
  - http://arthurfigueiredo.github.io/Kanban.js/
  - Javascript plugin to build kanban boards only 2KB

- https://github.com/waterrmalann/kards /MIT/202309/js
  - https://waterrmalann.github.io/kards/
  - A simple cards-based kanban board app inspired by Trello in pure vanilla JS

- https://github.com/riktar/jkanban /914Star/apache2/202111/js/inactive
  - https://www.riccardotartaglia.it/jkanban/
  - Vanilla Javascript plugin for manage kanban boards
  - jKanban use dragula for drag&drop

- https://github.com/otiagosoares/kanban-vanilla-js
  - https://codepen.io/otiagosoares/pen/rNWQGeb
- https://github.com/Eshh/kanban-board /js
  - drag and drop mini project using Vanilla JS
- https://github.com/ThierryRakotomanana/kanban-js /js/NoDeps
  - https://thierryrakotomanana.github.io/kanban-js/
  - simple task manager write enterily with a Vanilla Javascript and CSS. 
  - No framework or any dependencies

- https://github.com/apankrat/nullboard /BSD/js/jquery/单文件
  - https://nullboard.io/preview
  - Nullboard is a minimalist take on a kanban board / a task list manager, designed to be compact, readable and quick in use.
  - All data is stored locally, for now using localStorage.
  - [Kanban board in one HTML using localstorage | Hacker News_202102](https://news.ycombinator.com/item?id=26151207)
    - Exclusive use of jQuery, not using browser drag and drop (manually edits element position), using JS to animate and fade/transition instead of CSS, etc. Is localStorage the only modern/HTML5 concept being used?
    - It was written when I needed a kanban board done to my specs in a minimum amount of time using whatever things I was most comfortable with.
  - https://github.com/justinpchang/nullboard-agent-express /js
    - Local backup agent for Nullboard (MacOS/Linux compat)

- https://github.com/khanh-devos/Capstone2-Kanban /js
  - https://khanh-devos.github.io/Capstone2-Kanban/
  - Kanban board for workload management. 
  - Redux was implemented in only vanila JS for experimenting.

- https://github.com/iamdeadman/airtable-react-kanban /MIT/201906/js/提交多
  - A server-rendered React app inspired by Trello.
  - 依赖redux、React-beautiful-dnd、marked、express、mongodb、passport
  - 支持集成airtable

- https://github.com/atlassian/react-beautiful-dnd
  - https://react-beautiful-dnd.netlify.app/iframe.html?id=board--simple
  - 官方示例就是看板
- https://github.com/alireza-askarpour/kanban-board-frontend /ts
  - React Hook Form
- https://github.com/moaazelsayed1/Koplin /js
  - kanban application built using React, Nodejs, Express, and Postgres.

- https://github.com/nishantpainter/personal-kanban /ts
  - https://personalkanban.js.org/
  - 依赖 material-ui.v4, formik, i18next, moment, react-beautiful-dnd
  - columns and cards
  - an offline capable application or tool that implements kanban to manage work at personal level

- https://github.com/asseinfo/react-kanban
  - https://nvjp3.csb.app/
  - 样式较简单
  - 只依赖 react-beautiful-dnd
  - Yet another Kanban/Trello board lib for React.
- https://github.com/rcdexta/react-trello /1.5kStar/js
  - https://rcdexta.com/react-trello/
  - Pluggable components to add a kanban board to your application
- https://github.com/wekan/wekan
  - https://wekan.github.io/
  - The open-source kanban (built with Meteor).
- https://github.com/markusenglund/react-kanban /1.6kStar/201901
  - https://www.reactkanban.com/b/SyfPfO8CP/tutorial-board
  - React, Redux, React-beautiful-dnd, Express, MongoDB, Passport

- https://github.com/lxerxa/actionview /50Star/202101/php
  - An issue tracking tool based on php laravel-framework in back-end and reactjs+redux in front-end, it's similar to Jira
  - https://github.com/lxerxa/actionview-fe
    - ActionView front-end source code, based on Reactjs＋Redux.

- https://github.com/TiagoDiass/easyboards /202307/ts/inactive
  - front-end app similar to Trello
  - useBoardStore基于zustand
  - 依赖zustand、next、react-beautiful-dnd

- https://github.com/Pedro0505/project-manager-frontend
  - https://github.com/Pedro0505/project-manager-backend
  - NodeJS, Express, JWT, Prisma ORM, Typescript
  - React, React Hooks, Redux, CSS, Typescript, NextJS, Auth0

- https://github.com/mukulchugh/kanboard-notion-kanban-react /js
  - https://notion-kanboard-mukul.netlify.app/
  - 暂不支持视图切换

- https://github.com/shellyln/kanban-board-app /202101/ts/redux/inactive
  - https://shellyln.github.io/knbn
  - Kanban style task management board app
  - 依赖redux、material-ui.v4、pouchdb-find、codemirror5、
  - Calendar view
  - Synchronize multiple device boards with **CouchDB** remote server
  - Write kanban in Markdown syntax

- https://github.com/DawidBugajski/kanban-task-management /ts/提交多/样式友好
  - https://kanban-task-management-ecru.vercel.app/
  - Advanced task management
- https://github.com/Keith-Web3/Kanban-Task-Manager /ts/和上面几乎相同
  - https://incredible-bavarois-17a54a.netlify.app/
  - Kanban task management app with React, TypeScript, SCSS, Zustand, and customizable themes.
  - Create, edit, and delete tasks
  - Automatically save task updates using Zustand 
- https://github.com/BUMBAIYA/kanban
  - https://kannban-board.vercel.app/
  - Kanban board made using Reactjs and tailwindcss to keep track of your tasks
- https://github.com/raiane-oliveira/Kanban /js
  - https://kanbandev.vercel.app/

- https://github.com/distDev/Betsu /ts/redux/firebase
  - an realtime agile planner and calendar web app made with React, Redux-Toolkit, Firebase, React Beautiful DND and Chakra UI. 
  - It is heavily inspired by Trello.

- https://github.com/waterrmalann/task-raft /ts
  - A trello-like kanban board for team based task management

- https://github.com/sakihet/trellith /ts
  - https://trellith.vercel.app/
  - Tiny Trello clone PWA built with Preact and TypeScript, not storing data in cloud storage
  - Data is only stored in your browser's localStorage
  - Since data is stored in `localStorage`, the main thread gets blocked, and there is a `5MB` size limit.

- https://github.com/ritik2358/Kanban-board /js
  - https://kanban-board-ritik2358.vercel.app/
  - Kanban board-inspired task management application
  - 依赖MongoDB、express

- https://github.com/kanboard/kanboard /php
  - Kanban project management software
  - https://github.com/aljawaid/KanboardCSS

- https://github.com/kiswa/TaskBoard /1.1kStar/MIT/202009/php
  - A Kanban-inspired app for keeping track of things that need to get done

- https://github.com/ParabolInc/parabol /ts
  - https://parabol.co/retro-demo
  - open-source application for running agile meetings 
  - 依赖node、graphql、relay

- https://github.com/mgmeyers/obsidian-kanban /ts
  - https://publish.obsidian.md/kanban/
  - Create markdown-backed Kanban boards in Obsidian.

- https://github.com/remix-run/example-trellix /202401/ts
  - https://trellix.fly.dev/
  - A partial trello board clone with Remix

## kanban-fullstack

- https://github.com/ApelsinU/KanbanBoard /202402/ts
  - Fetch, Custom hook for Http
  - Zustand 
  - Fetch, Custom hook for Http
  - Express
  - MongoDB

- https://github.com/MukulSethi123/mini-jira /ts
  - Kanban-style task management application like JIRA

- https://github.com/drodzewicz/Work-Flow /ts
  - web-based Kanban-style list making application used to manage work at personal or organizational level.
  - Inspiration came from Github Projects and Trello
  - built using technologies like React on frontend and and Express and mongodb on backend. 
  - This application is also using websockets so that when working with a team all changes can be seen without refreshing the page.

- https://github.com/KanRule/KanRule /前端js+后端ts
  - https://kanrule.com/
  - A simplified Jira clone built with React and Node

- https://github.com/hironarita/kanban-lite /ts
  - Simplified version of Trello built with React
  - https://github.com/hironarita/kanban-lite-backend /js

- https://github.com/DishaGup/kanban-board /js
  - Kanban Board web application designed to enhance task management

- https://github.com/getlost01/Intelli-Kanban /ts
  - https://intelli-kanban-tec.vercel.app/
  - Frontend of AI based Kanban enhancement tool named Intelli-Kanban
  - Integration of Chat-GPT API for comprehensive task descriptions/breakdown
  - 依赖mui、Redux、nextjs、mongodb
  - https://github.com/getlost01/intelli-kanban-backend /js

- https://github.com/onoseremejohn/kanban-MERN-version /ts
  - full-stack task manager app built with React TS, Node, Express, and MongoDB
  - https://github.com/onoseremejohn/Kanban-Task-Manager

- https://github.com/rapidomize/rTask /apache2/202301/ts/inactive
  - Open source, self-hosted project management, kanban board tool that's an alternative to Trello. 
  - It allows you to track & manage your work.
  - 依赖angular、ngx-quill

## realtime

- https://github.com/plankanban/planka /AGPLv3/202309/js/redux
  - https://plankanban.github.io/planka/
  - The realtime kanban board for workgroups built with React and Redux.
  - React, Redux, Redux-Saga, Redux-ORM, Semantic UI React, react-beautiful-dnd
    - 前端单独分离出来了
  - Sails.js, Knex.js
  - PostgreSQL

- https://github.com/RARgames/4gaBoards /js
  - realtime kanban boards for groups

- https://github.com/inovex/scrumlr.io /MIT/202406/ts/go
  - https://scrumlr.io/
  - an online collaboration tool that helps teams reach new heights. 
  - Start your first retrospective or collaborative session in an instant - no registration required and completely free and open source.
  - 产品的设计，使用从模版开始

## api-trello/kanban

- https://github.com/MrRefactoring/trello.js
  - JavaScript/TypeScript library for Node. JS and browsers to easily interact with Atlassian Trello API

- https://github.com/ocipap/API__Trello-clone-project
  - Using node.js, express, sequelize, JWT

- https://github.com/GiangThanhDat/trello-clone-backend /js
  - https://github.com/GiangThanhDat/trello-clone-frontend /js
  - Build a trello-app basic api using nodejs, mongodb

- https://github.com/oldboyxx/boxd_api
  - Node/Mongo API for a Trello clone; old version written in es5 - es6 
  - 依赖mongoose
- https://github.com/ngudbhav/sept-oct-frontend-trello-app
  - Backend APIs for the trello app

- https://github.com/kvandake/lexorank-ts
  - A reference implementation of a list ordering system like JIRA's Lexorank algorithm

- https://github.com/alejo-ortega/kanban-api-typescript /ts
  - KanBan Project Management REST API made with Node.js, Express.js, TypeScript, zod, prisma and SQLite

## more-kanban

- https://github.com/discourse/discourse-kanban-theme /js
  - https://meta.discourse.org/t/kanban-board/118164
  - A Discourse theme component providing basic kanban-board functionality
  - allows you to display and organise topics using a kanban board interface.

- https://github.com/leif81/bzkanban /js
  - allows you to visualize bugs from a Bugzilla server on a Kanban board.
  - The goal is to compliment the Bugzilla workflow you are already using. 
  - implemented as a client side SPA using Ajax with the Bugzilla 5 server REST API. 
  - your Bugzilla server database is the single source of truth, the bzkanban app is just a view of your Bugzilla database.

- https://github.com/LexMachinaInc/quadro /js
  - kanban board for Github issues

- https://github.com/mrinalxdev/KanToday /ts
  - kanban web app to note down all your daily activates

- https://github.com/loydcose/tusk
  - https://tusk-kanban.vercel.app/
  - minimalist project manager inspired by Trello, designed to help you organize your tasks efficiently.

- https://github.com/mux-mux/kanban /js
  - localStorage & webpack

- https://github.com/d3ward/b2ntp /js
  - https://b2ntp.vercel.app/
  - Kanban style New Tab Page extension with your bookmarks and powerful search
  - support chrome/firefox

- https://github.com/nextcloud/deck /202403/js
  - Kanban-style project & personal management tool for Nextcloud, similar to Trello
# calendar
- https://github.com/calcom/cal.com /AGPLv3/202403/ts
  - https://github.com/calcom/cal.com
  - open-source Calendly alternative, formerly Calendso
  - API-driven and ready to be deployed on your own domain.
  - PostgreSQL
  - 黑色圆角线框风格
  - https://github.com/calcom/ui
# browser/thunderbird-inspired
- products
  - [Rambox | Workspace Simplifier to Boost your Productivity](https://rambox.app/)

- https://github.com/alyssaxuu/omni /js/browser-ext
  - use your browser like a pro. Manage tabs, bookmarks, your browser history, perform all sorts of actions and more with a simple command interface
  - Get it now for Chrome and for Firefox

- https://github.com/getstation/desktop-app /1.2kStar/apache2/202312/ts
  - https://getstation.com/
  - One app to rule them all
  - open-source smart browser for busy people. 
  - 依赖graphql、apollo-client/link、immutable-js.v3、electron-chrome-extension、redux、rxjs

- https://github.com/wavebox/waveboxapp /1.3kStar/MPLv2/js/open2close
  - https://wavebox.io/
  - Browser for Work
  - Wavebox gives you customizable toolbars, sleeping tabs, cookie containers and multiple profile
  - Wavebox 10, a complete **fork of Chromium** launched in 2019, but if you're looking for the Electron based Wavebox Classic, there's an archive of the code here
  - [Introducing Wavebox 10_201911](https://github.com/wavebox/waveboxapp/issues/1133)
  - [Wavebox 10 source](https://github.com/wavebox/waveboxapp/issues/1132)
    - we've decided not to open source the new version of Wavebox
    - I have switched to singlebox.app, which is IMO the best open source alternative out there.

- https://github.com/webcatalog/webcatalog-legacy /MPLv2/202203/js/archived
  - WebCatalog - Turn Websites into Desktop Apps.
  - WebCatalog app's development has been moved to a closed source code base.
  - Legacy code of the core that powers WebCatalog, Singlebox, Clovery and Skywhale.

- https://github.com/sonnyp/Tangram /GPLv2/202304/js
  - https://apps.gnome.org/app/re.sonny.Tangram/
  - Browser for your pinned tabs
  - Tangram is a new kind of browser. It is designed to organize and run your Web applications. Each tab is persistent and independent.
  - Tabs are independent and sandboxed from each others.
  - You can set multiple tabs with different accounts for the same application.
  - Both Flatpak and non-Flatpak versions of Tangram provide sandboxing for Web applications.
    - Flatpak via our restricted permissions
    - Non-Flatpak through `WebkitGTK` Sandboxing (requires WebkitGTK >= 2.26)
# task-format
- https://github.com/imdone/imdone-core /MIT/js
  - https://imdone.io/
  - Imdone is text based kanban processor with a simple syntax that uses comment tags like TODO and FIXME and todo.txt format. 
  - This model allows the user to create and modify tasks using the keyboard and automatically establishes a link between their tasks and work.

- https://github.com/BaldissaraMatheus/Tasks.md /MIT/js
  - A self-hosted, file based task management board that supports Markdown syntax
  - Write cards as Markdown files; 
  - built with SolidJS and Koa. 
  - It also uses Stacks-Editor for text editing and serve-static to serve the css files as-is.

- https://github.com/todomd/todo.md
  - The TODO.md format is based on GFM - GitHub Flavored Markdown - Task Lists.
  - Tasks in TODO.md can be visualized using Kanban Board where sections become columns on the board.

- https://github.com/ransome1/sleek /MIT/202403/ts
  - https://github.com/ransome1/sleek/wiki
  - open-source (FOSS) todo manager based on the todo.txt syntax. 
  - available for Windows, macOS and Linux
# sandbox/all-in-one
- https://github.com/sandstorm-io/sandstorm /apache2/202308/js/cpp
  - https://sandstorm.io/
  - a self-hostable web productivity suite. 
  - It's implemented as a security-hardened web app package manager.
# scheduler-task
- https://github.com/whyour/qinglong /apache2/202401/ts
  - 支持 Python3、JavaScript、Shell、Typescript 的定时任务管理平台
  - 依赖express、nedb、multer、sequelize、ip2region
  - 支持多种脚本语言（python3、javaScript、shell、typescript）
  - 支持在线管理脚本、环境变量、配置文件
  - 支持在线查看任务日志
  - 支持手机端操作
# meetings
- https://github.com/rustdesk/rustdesk /AGPLv3/202401/rust/dart
  - https://rustdesk.com/
  - Yet another remote desktop software, written in Rust. 
  - Works out of the box, no configuration required. 
  - You have full control of your data, with no concerns about security. 
  - You can use our rendezvous/relay server, set up your own, or write your own rendezvous/relay server.
# team-ai
- https://github.com/Teamlinker/Teamlinker /GPLv3/202406/ts/vue
  - https://team-linker.com/
  - Teamlinker is a team collaboration platform that integrates multi-functional modules, such as contact, task management, meeting, IM, Wiki and file management.
  - Teamlinker is developed based on the TeamOS system. It is a web operating system that allows users to process different tasks in parallel
# more
- https://github.com/avisek-official/simple-notes /ts
  - https://next-simple-notes.vercel.app/
  - Simple Apps, your all-in-one productivity companion that consists of two micro apps
  - a powerful note-taking tool, a versatile kanban board application and an AI based knowledge test tool.
  - 依赖nextjs、mongodb、chartjs

- https://github.com/kndwin/solaces
  - Linear clone with different reactive local database POC's

- https://github.com/PradKalkar/microsoft-teams-clone
  - Developed a Microsoft teams clone as a part of Microsoft Engage '21

- https://github.com/atlassian/github-for-jira /MIT/202401/ts
  - Connect your GitHub code with your project management in Jira. 
  - A separate Jira subscription is required.
