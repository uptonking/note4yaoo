---
title: toc-db-indexeddb-examples
tags: [examples, indexeddb]
created: 2022-06-03T22:06:28.976Z
modified: 2022-06-03T22:06:47.464Z
---

# toc-db-indexeddb-examples

# popular

- https://github.com/madmoizo/backinfront
  - Backinfront is both the manager of your browser database and a router which handles requests locally. 
  - If you are building an offline first web app which needs sync capabilities, Backinfront is probably the tool your are looking for.
  - Backinfront is designed to work inside a Service Worker make sure to NOT use it in a window context

- https://github.com/stoxy-js/stoxy
  - Stoxy is a state management API for all modern Web Technologies.
  - Stoxy stores the data in a in-browser Database called IndexedDB, only keeping the latest 5 accessed objects in-memory for faster access.
  - Stoxy utilizes a promise-based use flow making it really easy to asynchronously read and write from the storage.
  - If your browser doesn't support IndexedDB, there's no need to worry. Stoxy recognizes these cases automatically, and opts out of using it and utilizes a in-memory system only.

- https://github.com/mWater/offline-leaflet-map
  - Offline maps in Leaflet using IndexedDb to store tiles
- https://github.com/helgasoft/leaflet.dexie
  - A Leaflet plugin for local persistent storage using library Dexie.js
- https://github.com/yagajs/indexed-db-tile-cache /inactive
  - Spatial tile cache that saves its data into the IndexedDB of your browser

- https://github.com/eyalzh/simple-kanban
  - A lightweight offline kanban board
  - Completely offline (IndexedDB backend)
  - JSON import/export
- https://github.com/roottool/skeban
  - Skeban is an open source Electron based kanban app. It is written in TypeScript and uses React.

- https://github.com/kevinbgreene/indeksd
  - A DSL for defining IndexedDB schemas.
  - Generate a type-safe IndexedDB client from a simple schema file.
  - https://github.com/kevinbgreene/indeksd-example
    - Example app for using indeksd IndexedDB code generation
# indexeddb-apps
- https://github.com/mohitk0208/notes-pwa
  - https://notes-ysau.pages.dev/
  - Make notes page_with_curl in the browser itself, it runs offline and the data is saved in the browser.

- https://github.com/AlisherKonratbaev/Shop
  - https://shop-ruddy.vercel.app/index.html
  - An example of an electronic store with the functionality of authorizing registration, adding, deleting, changing products, placing orders from the basket. 
  - Implemented patterns as "Singleton", "Observer". 
  - The data is stored in indexedDB.

- https://github.com/BaseMax/MyPhonebook
  - https://basemax.github.io/MyPhonebook/src/
  - show how to use IndexedDB internal browser database with dexie
  - MyPhonebook is a web-based phone book page with ability to add contacts and search betweens with internal browser database supporting (IndexedDB full cache), styled powered by TailwindCSS.

- https://github.com/wisdomekpotu/PWA-TodoApp
  - https://wisdomekpotu.github.io/PWA-TodoApp/
  - A simple Todo PWA(Progressive Web Application) using indexedDB as database and can be used offline.
- https://github.com/JamieVaughn/react-todo
  - A todo app with react and indexedDB
- https://github.com/mdn/to-do-notifications
  - an Enhanced version of my basic to-do app, which stores to-do items via IndexedDB, and then also aims to provide notifications when to-do item deadlines are up, via the Notification and Vibration APIs.
- https://github.com/DevTony101/js-todo-app-indexed_db
  - https://indexed-todo-app.netlify.app/
  - The aim is to teach/learn the basics of the IndexedDB API
- https://github.com/RayJune/JustToDo
  - 就是去做：a sample todolist web-app written by plain JavaScript
- more-todo
  - https://github.com/sycancodes/sycan-todo-app

- https://github.com/kkosmowski/react-notes-2
  - https://kkosmowski-notes.netlify.app/
  - Advanced To-Do app with custom drag-to-select, categories and multiple customization options.
  - 依赖localbase操作indexeddb
- https://github.com/SimonPe25/Apple-Note
  - React v18.0, React Router v6, React Context, react Hooks, Ant Design, Sass, BEM, IndexedDB, Markdown
- https://github.com/familyfriendlymikey/JILU
  - free note taking app for psychopaths hosted on Github Pages which directly addresses the problem of realtime organization by combining folder pathing, search, and highly optimized workflows
  - entirely local to your device: No server, no remote database, no accounts, no tracking

- https://github.com/periodo/periodo-client
  - https://client.perio.do/
  - A Web browser application for browsing and editing PeriodO data.
  - Because browsers do not support IndexedDB for pages served from local file systems, during development, you will need to run a process that will serve the root directory over HTTP.

- https://github.com/jpodwys/preact-journal
  - https://preact-journal.herokuapp.com/
  - 14k offline-capable journaling PWA using preact, node, MySQL, and IndexedDB.
  - 使用体验类似文章列表

- https://github.com/AldoHub/React-Dexie
  - React implementation using Hooks, IndexedDb with Dexiejs and file uploading
- https://github.com/brookslybrand/react-indexeddb-example
  - Example of using the Indexed API to persist changes to a simple form in React with dexie.js

- https://github.com/pamelac21/Budget-Tracker
  - NoSQL - MongoDB - A budget tracker with offline functionality
- https://github.com/avaarm/Budget-Tracker
  - Budget Tracker is a progressive web application that allows the user to add and subtract funds online and offline.
- https://github.com/jorgeabrahan/budgtcalc
  - (Responsive) (CRUD) (IndexedDB) budget calculator developed using vanilla JS and storing data on IndexedDB
- https://github.com/JColeCodes/cash-cache
  - https://budget-tracker-jcolecodes.herokuapp.com/index.html
  - A simple budget tracker webpage has been upgraded to a progressive web app (PWA)!

- https://github.com/googlecodelabs/workbox-indexeddb
  - use IndexedDB and Workbox to create a fully offline-capable, data-driven app. 
  - You'll also use Background Sync to sync your app with the server even when your web app is closed.
# more-indexeddb-examples
- https://github.com/chenstarx/GoDB.js
  - indexedDB with Intuitive API, CRUD with one line of code.
- https://github.com/ismaelcallerojas/CRUD-indexeddb
  - CRUD con la api indexed db 单文件使用示例

- https://github.com/yued-fe/yux-storage
  - yux-storage 是一个基于 HTML5 IndexedDB 封装的 Web 本地数据离线存储库。

- https://github.com/assuncaocharles/react-indexed-db
  - wraps IndexedDB database in an "easier to use" service. 
  - It exposes very simple promises API to enable the usage of IndexedDB without most of it plumbing.

- https://github.com/BinaryBitBytes/JustAnotherTextEditor
  - A progressive web application that utilizes IndexedDB API to log text in a database

- https://github.com/coderbennett/text-editor
  - https://joeys-text-editor.herokuapp.com/
  - This is a single-page text editor which stores data to an IndexedDB database. 
  - This application features multiple data persistence techniques in case one of the options aren't supported by the browser. 
  - This application also functions offline when installed.
- https://github.com/siennameow/text-editor
  - https://dreamcatcher-texteditor.herokuapp.com/
    - created as a simple text editor app that can function both online and offline

- https://github.com/corskaya/browser-storages-app
  - An app to manage data in IndexedDB, Cookies, Local and Session Storages

- https://github.com/web2solutions/voodux
  - VooduX - "with bateries included" agnostic scalable "M" layer for React, Vue, ExtJS, DHTMLX

- https://github.com/6fa/AccountBook
  - 一个用原生js+webpack+indexedDB写的记账本应用

- https://github.com/alufers/hn-offline
  - An offline-first client for hackernews that even fetches the article contents for reading on the go.

- https://github.com/HondryTravis/TinyDB
  - easy to use multi-table indexedDB lib

- https://github.com/tykoth/ra-data-dexie
  - Experimental React-Admin data provider using Dexie (IndexedDB)

- https://github.com/Hacker233/IndexedDB
  - 前端本地存储数据库IndexedDB完整教程，仅文字

- https://github.com/Banana021s/music-player
  - a nice theme music playeryum with indexedDB

- https://github.com/gotpop/gotpop
  - A component based portfolio application build with React, Redux and CSS Grid layout.
