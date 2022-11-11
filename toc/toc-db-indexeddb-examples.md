---
title: toc-db-indexeddb-examples
tags: [examples, indexeddb]
created: 2022-06-03T22:06:28.976Z
modified: 2022-06-03T22:06:47.464Z
---

# toc-db-indexeddb-examples

# popular

- https://github.com/HiWayne/large-file-uploader
  - 专为上传功能而优化，file uploader, supporting file segmentation, resume from break point, offline storage...
  - 断点续传，不必重头再来
  - 基于 indexedDB 的文件缓存，离线也能恢复进度
  - 多线程计算，面对大文件处理更快
  - 只提供下载队列的状态数据，你可以自由定制 UI
  - 丰富的配置，你可以限制文件类型、每个切片大小、线程数、请求并发数、是否开启离线缓存等

- https://github.com/rpecuch/text-editor /js
  - The purpose of this project was to build a single-page application that meets Progressive Web Application criteria. 
  - 后端只依赖express
  - 前端依赖codemirror5、idb、workbox

- https://github.com/mWater/offline-leaflet-map
  - Offline maps in Leaflet using IndexedDb to store tiles
- https://github.com/yagajs/indexed-db-tile-cache /inactive
  - Spatial tile cache that saves its data into the IndexedDB of your browser

- https://github.com/nareshbhusal/roadmap
  - A kanban board, project and idea management app built with React and IndexedDB.
  - 依赖TailwindCSS、Chakra-ui、dexie、dnd-kit
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
# crud-api
- https://github.com/simplifyjs/indexeddb-crud
  - Comparison between native IndexedDB API and using IDB library in operating CRUD workaround

- https://github.com/chenstarx/GoDB.js
  - indexedDB with Intuitive API, CRUD with one line of code.

- https://github.com/ismaelcallerojas/CRUD-indexeddb
  - CRUD con la api indexed db 单文件使用示例
# react-vue
- https://github.com/assuncaocharles/react-indexed-db
  - wraps IndexedDB database in an Declarative way. 
  - It exposes very simple promises API to enable the usage of IndexedDB 

- https://github.com/bernabe9/redux-react-session
  - Simple Session API storage for Redux and React

- https://github.com/jpodwys/preact-journal /202103
  - 14k offline-capable journaling PWA using preact, node, MySQL, and IndexedDB.

- https://github.com/hc-oss/use-indexeddb
  - hook w/ promises for easy IndexedDB access in React

- https://github.com/eldomagan/vuex-orm-localforage
  - VuexORMLocalforage is a plugin for the amazing VuexORM that let you sync your Vuex Store with an IndexedDB database using LocalForage.
# apps
- https://github.com/Tesfaye-Eshetie/movie-search-pwa /js
  - https://tesfaye-eshetie.github.io/movie-search-pwa/
  - Movie Search PWA using React, vite, PWA and IndexedDB

- https://github.com/alexeagleson/template-indexeddb
  - A simple template for getting started with IndexedDB
  - IndexedDB is known to be quite fast on inserting reasonably large quantities of data on a single transaction, but can slow down significantly when these inserts/updates are made across multiple transactions.
  - ensure you are developing your application to batch data modifications into as few transactions as possible.

- https://github.com/wizexplorer/excel-clone /202210/js
  - An excel clone using HTML-CSS-JavaScript. Change properties of different cells. 
  - Capable of applying formulas, copying/cutting/pasting multiple cells. 

- https://github.com/mohitk0208/notes-pwa
  - https://notes-ysau.pages.dev/
  - Make notes page_with_curl in the browser itself, it runs offline and the data is saved in the browser.

- graph /7Star/MIT/202210/ts
  - https://github.com/graphcentral/graph
  - https://graphcentral.github.io/graph
  - Performant graph visualization on the web with WebGL + Webworkers + IndexedDB
  - You can visualize Notion pages on force layout graph using this library


- https://github.com/crossjs/cofe
  - No-Code System
  - core依赖unist-builder

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
# more-indexeddb
- https://github.com/yued-fe/yux-storage
  - yux-storage 是一个基于 HTML5 IndexedDB 封装的 Web 本地数据离线存储库。

- https://github.com/Jeremy664K/crud-drag-drop
  - App that contains the indexedDB API and Drag-And-Drop API.

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

- https://github.com/Hacker233/IndexedDB
  - 前端本地存储数据库IndexedDB完整教程，仅文字

- https://github.com/Banana021s/music-player
  - a nice theme music playeryum with indexedDB

- https://github.com/gotpop/gotpop
  - A component based portfolio application build with React, Redux and CSS Grid layout.
