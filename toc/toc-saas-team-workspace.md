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
- alternatives
  - jira, trello, linear
# popular
- https://github.com/xiweicheng/tms /js/java
  - TMS是基于频道模式的团队沟通协作+轻量级任务看板，支持mardown、富文本、在线表格和思维导图的团队博文wiki，i18n国际化翻译管理的响应式web开源团队协作系统。
# microsoft-teams/org
- growi /1.1kStar/MIT/202301/ts/remark
  - https://github.com/weseek/growi
  - https://docs.growi.org/en/guide/
  - https://demo.growi.org/
  - Team collaboration software using markdown
  - 依赖 express、mongoose、es、redis、swr
  - Simultaneously edit with multiple people by HackMD(CodiMD) integration
  - Create hierarchical pages with markdown
  - Slack/Mattermost, IFTTT Integration
  - 各种集成

- crowi /1.1kStar/MIT/202211/ts
  - https://github.com/crowi/crowi
  - http://demo.crowi.wiki/
  - The Markdown Wiki - Empower the team with sharing your knowledge
  - URL Based Page Tree
  - pages that end with slashes (/) are automatically generated as list views. 
  - 功能和样式都很普通
  - 依赖mongoose、es、redis、swig

- https://github.com/bennymeier/mern-stack-project-management
  - A project management platform built with the MERN-Stack.
  - Jira clone with MongoDB, Express, React and Node.js
  - 后端js，mongoose
  - 前端ts，redux、semantic-ui、react-beautiful-dnd

- https://github.com/vishwajeetraj11/projectboard
  - https://github.com/vishwajeetraj11/projectboard-backend
  - A project management application that allows you to track tasks process
  - 后端js，mongoose
  - 前端ts，redux， react-markdown-editor, react-beautiful-dnd

- https://github.com/linagora/Twake
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
# project-management
- https://github.com/jacobrdz77/selfwork
  - A project management system for small teams and freelancers.
  - 依赖prisma、next、tanstack-query、zustand
  - Organize your projects and members in different workspaces you create.
  - Full CRUD functionality for projects, clients, sections, tasks, and workspaces.
  - Use intigrated Excalidraw to create diagrams in the sketch view for each project
  - Allows you to log in and register using Google.
  - npx prisma migrate dev --name init
  - npm run seed

- https://github.com/rcamach7/project-management-app
  - Project management application, similar to that of Trello or Jira.
  - Utilized NextAuth to authenticate users and store their data in a MongoDB database
  - 依赖next-auth、mongoose、mui5，不支持拖拽

- https://github.com/pooridev/Todoooze
  - https://todooooze.vercel.app/
  - minimal project management app, powered by Next.js and Typescript
  - 依赖trpc、next、reduxjs-toolkit、recoil、react-query
  - 样式友好
# user/permissions/scrum/Inventory
- https://github.com/bissbr01/Command-project-management /ts
  - A Scrum Management App for teams
  - 依赖reduxjs-toolkit、mantine、dnd-kit、formik
  - https://github.com/bissbr01/Command-backend /js
    - 依赖sequelize6
    - A containerized REST API for the Command project managment app.

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
# kanban/board
- https://github.com/Fredkiss3/thullo
  - A Trello Clone
  - 后端依赖express、tsyringe(IoC)、mongoose
  - 前端依赖dnd-kit、react-beautiful-dnd、react-query、headlessui
  - 样式友好

- https://github.com/knowankit/trello-clone
  - Built with Nextjs framework with Typescript and Chakra UI library with support from MongoDB
  - Login/Register with JWT token authentication

- https://github.com/oldboyxx/jira_clone
  - simplified Jira clone built with React/Babel (Client), and Node/TypeScript (API)
  - 未实现用户组织管理
  - 后端ts依赖express、typeorm、pg、jwt
  - 前端js依赖react-beautiful-dnd、quill、sweet-pubsub
  - 样式友好

- https://github.com/lyn-eva/jira-clone
  - Project management web app for agile teams built with REST architecture
  - 依赖 RTK Query, Tailwindcss, Express, MySQL, Prisma

- https://github.com/atlassian/react-beautiful-dnd
  - https://react-beautiful-dnd.netlify.app/iframe.html?id=board--simple
  - 官方示例就是看板
- https://github.com/riktar/jkanban /630Star/202012
  - https://www.riccardotartaglia.it/jkanban/
  - Vanilla Javascript plugin for manage kanban boards
- https://github.com/asseinfo/react-kanban
  - https://nvjp3.csb.app/
  - 样式较简单
  - 只依赖 react-beautiful-dnd
  - Yet another Kanban/Trello board lib for React.
- https://github.com/rcdexta/react-trello /1.5kStar/202012
  - https://rcdexta.com/react-trello/
  - Pluggable components to add a kanban board to your application
- https://github.com/wekan/wekan
  - https://wekan.github.io/
  - The open-source kanban (built with Meteor).
- https://github.com/markusenglund/react-kanban /1.6kStar/201901
  - https://www.reactkanban.com/b/SyfPfO8CP/tutorial-board
  - React, Redux, React-beautiful-dnd, Express, MongoDB, Passport
- https://github.com/plankanban/planka
  - https://plankanban.github.io/planka/#/
  - The realtime kanban board for workgroups built with React and Redux.
  - React, Redux, Redux-Saga, Redux-ORM, Semantic UI React, react-beautiful-dnd
    - 前端单独分离出来了
  - Sails.js, Knex.js
  - PostgreSQL
- https://github.com/lxerxa/actionview-fe
  - ActionView front-end source code, based on Reactjs＋Redux.
  - https://github.com/lxerxa/actionview /50Star/202101
  - An issue tracking tool based on php laravel-framework in back-end and reactjs+redux in front-end, it's similar to Jira

- https://github.com/nishantpainter/personal-kanban
  - https://personalkanban.js.org/
  - 依赖 material-ui.v4, formik, i18next, moment, react-beautiful-dnd
  - columns and cards
  - an offline capable application or tool that implements kanban to manage work at personal level
  - The application is registered with service workers and behaves as a progressive web application (PWA)

- https://github.com/TiagoDiass/easyboards
  - front-end app similar to Trello
  - 依赖zustand、next、react-beautiful-dnd

- https://github.com/Pedro0505/project-manager-frontend
  - https://github.com/Pedro0505/project-manager-backend
  - NodeJS, Express, JWT, Prisma ORM, Typescript
  - React, React Hooks, Redux, CSS, Typescript, NextJS, Auth0

- https://github.com/mukulchugh/kanboard-notion-kanban-react /js
  - https://notion-kanboard-mukul.netlify.app/
  - 暂不支持视图切换

## kanban/trello-api

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
# more
- https://github.com/kndwin/solaces
  - Linear clone with different reactive local database POC's

- https://github.com/PradKalkar/microsoft-teams-clone
  - Developed a Microsoft teams clone as a part of Microsoft Engage '21
