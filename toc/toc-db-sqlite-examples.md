---
title: toc-db-sqlite-examples
tags: [examples, sqlite, toc]
created: 2022-06-03T22:05:28.840Z
modified: 2022-06-03T22:07:49.519Z
---

# toc-db-sqlite-examples

# guide

- resources
  - https://github.com/asg017/sqlite-ecosystem

- db-manager
  - /home/yaoo/.local/share/DBeaverData/workspace6/.metadata/sample-database-sqlite-1/
# popular
- https://github.com/karlb/litespread /202108/js/inactive
  - https://github.com/karlb/litespread/wiki
  - https://www.litespread.com/
  - Webapp that uses SQLite as a spreadsheet engine
  - Litespread is viewer and editor for SQLite and CSV files with basic spreadsheet functionality.
  - Litespread runs in your browser without the need for any server-side code
  - 依赖sql.js、blueprintjs、file-saver、moment、papaparse、react
  - Sync data via Remote Storage
  - Use SQL syntax in formulas

- https://github.com/ShivamJoker/SQL-Play
  - Simple app to practice and learn SQL in React Native using SQLite

- api-server-nodejs-mongo /11Star/MIT/202212/ts/代码简单
  - https://github.com/app-generator/api-server-nodejs-mongo
  - Can be used with other React Starters for a complete Full-Stack experience
  - 典型的dashboard的后端示例
  - 依赖express、mongoose、passport-jwt
- api-server-nodejs /178Star/Paid/202212/ts
  - https://github.com/app-generator/api-server-nodejs
  - Express Starter with JWT authentication, and SQLite persistance - Provided by AppSeed App Generator. 
  - 依赖Express, SQLite, TypeORM, passport-jwt
  - Authentication Flow uses json web tokens via Passport library - passport-jwt strategy.
  - TypeScript, Joy for validation

- https://github.com/lana-k/sqliteviz
  - https://lana-k.github.io/sqliteviz/
  - Sqliteviz is a single-page offline-first PWA for fully client-side visualisation of SQLite databases or CSV files.
  - 依赖vue2、jquery、pivottable、plotly.js.v1、sql.js、react-chart-editor
  - 依赖很多plotly的产品
  - Instant offline SQL-powered data visualisation in your browser

- https://github.com/cloudflare/d1-northwind /202211/js
  - https://northwind.d1sql.com/
  - Northwind Traders D1 Demo
  - 使用cf全家桶
  - a demo of the Northwind dataset, running on Cloudflare Workers, and D1 - Cloudflare's newest SQL database, running on SQLite.

- memos /260Star/NALic/202206/ts/go
  - https://github.com/usememos/memos
  - https://usememos.com/
  - 后端依赖 go
  - 前端依赖 redux-toolkit, dayjs, axios
  - ui高度复刻flomo，中文开发者作品，代码量不大
  - self-hosted knowledge base that works with a SQLite db file.
  - 编辑器使用的是简单 textarea，Write in the plain textarea without any burden
  - It has no external dependency.

- https://github.com/thevahidal/soul /js
  - A SQLite REST and realtime server
  - Soul is command line tool, after installing it, Run soul -d sqlite.db -p 8000 and it'll start a REST API on http://localhost:8000 and a Websocket server on ws://localhost:8000.
  - Soul Studio provides a GUI to work with your database.

- https://github.com/assafmo/SQLiteProxy
  - A simple HTTP JSON proxy for SQLite.
  - Must use HTTP POST with content-type=application/json.

- https://github.com/gromnitsky/naif-blog-engine
  - A static blog generator powered by GNU Make, Node.js & SQLite. 
  - Includes support for podcast feeds & FTS (full text search).
  - write blog posts in markdown, and create themes using ejs.

- https://github.com/sqlighter/sqlighter /ts
  - SQLighter is a database explorer born for SQLite that helps you design and deploy your application database in minutes. 
  - SQLighter is built in Typescript using Next.js with a React frontend and Node backend. 
  - 依赖mui5、nextjs、react-dnd、sql.js、swr、express、knex
# crud-rest-api
- https://github.com/machelslack/api-with-sqlite
  - node express api using a sqlite in memory database

- https://github.com/TeamThinkpad/express-typescript-api
  - API created using Typescript, Express, and SQLite using the Prisma ORM

- https://github.com/olsonpm/sqlite-to-rest
  - Koa routing middleware allowing you to expose a sqlite database via RESTful CRUD

- https://github.com/DevJonathanMendes/API-Com-Express.JS
  - API CRUD, com Express. JS e SQLite.

- https://github.com/wpcodevo/node-react-trpc-crud-app  /ts
  - create a full-stack note application that follows the CRUD  architecture with tRPC and use Prisma ORM to store data in an SQLite database
# react
- https://github.com/sql-js/react-sqljs-demo
  - a template repository demonstrating the use of sql.js with create-react-app.

- https://github.com/alexdevero/bookshelf-react-express-sqlite-app
  - App for collecting books built with React, Express and SQLite.
# electron
- https://github.com/spenserblack/favlist.vue
  - Edit tables/lists with a SQLite backend and JSON imports/exports
  - Manage lists with dynamic columns backed by a SQLite database.

- https://github.com/patrickmoffitt/local-sqlite-example
  - This project demonstrates how to install and use a local SQLite3 database in Electron using SQL.js.

- https://github.com/sjmelia/electron-boilerplate-sqlite
  - minimal Electron app with SQLite support

- https://github.com/tarikguney/electron-with-sqlite3
  - Sample application for ElectronJS working with Sqlite3

- https://github.com/fmacedoo/ers-stack
  - A basic application made with Electron, React, and SQLite tech stack

- https://github.com/synle/sqlui-native
  - simple UI client for most SQL Engines written in Electron.
  - It supports multiple Windows, so you can have different sets of queries and connections side by side.

- https://github.com/garrylachman/ElectroCRUD
  - ElectroCRUD is Open Source Database CRUD (Create, Read, Update, Delete) Software. No Code Needed
- https://github.com/vazra/electron-react-ts-rxdb-realm-sqlite
  - Demo of Native Databases with Electron and ReactJS. Realm, SQLite and RxDB ( with LevelDB/IndexedDB/InMemory adapters)
  - The electron & react part is bootstraped with electron-webpack-typescript-react boilerplate
# apps

# utils

- https://github.com/aergoio/litetree 202003/c/inactive
  - It is a modification of the SQLite engine to support branching, like git!
  - Each database transaction is saved as a commit, and each commit has an incremental number
  - We cannot write to the database when we are in a defined commit, writing is only possible at the head of each branch. If you want to make modifications to some previous commit you must create a new branch that starts at that commit.
# more-sqlite-examples
