---
title: toc-repos-boilerplate-examples
tags: [boilerplate, examples, starter, toc]
created: 2023-11-16T14:51:47.934Z
modified: 2023-11-16T15:00:11.503Z
---

# toc-repos-boilerplate-examples

# guide
- vanillajs类型的架构可以参考流行的dashboard、shop/ecommerce
# common-examples

## counter

- https://github.com/kentcdodds/dom-testing-library-with-anything
  - This repo is a bunch of simple examples of using DOM Testing Library to test a Counter component in various frameworks

## todomvc

- https://todomvc.com/
- https://github.com/tastejs/todomvc
- https://github.com/twinstae/todomvc-for-all
- https://github.com/rokoroku/react-redux-typescript-boilerplate
- https://github.com/dwyl/javascript-todo-list-tutorial /js
  - A step-by-step complete beginner example/tutorial for building a Todo List App (TodoMVC) from scratch
- https://github.com/1Marc/modern-todomvc-vanillajs /js
  - TodoMVC with Modern (ES6+), Vanilla JavaScript
  - 200 lines of code total, No build tools
  - [TodoMVC App Written in Vanilla JavaScript | Hacker News_202205](https://news.ycombinator.com/item?id=31293750)
    - that's exactly what I would imagine vanilla js code look like, and I'm glad we moved on to frameworks. Just this small app seems not so fun to maintain

## realworld

- resources
  - https://github.com/gothinkster/realworld
  - [RealWorld](https://www.realworld.how/)
  - [CodebaseShow – RealWorld Example Apps](https://codebase.show/projects/realworld)

- https://github.com/chagweyh/react-hooks-typescript-realworld /202011/ts/inactive
  - https://react-hooks-typescript-realworld.netlify.com/
  - Exemplary real world application built with React Hooks + Typescript
  - 依赖react、axios、reach-router
- https://github.com/Allianzcortex/react-typescript-hooks-realworld /202110/ts/redux
  - https://react-typescript-hooks-realworld.vercel.app/
  - React FC + Immer + Redux + Hooks + axios + Testing Library

- https://github.com/adr1enbe4udou1n/react-ts-realworld-example-app /202312/ts
  - https://github.com/adr1enbe4udou1n/nestjs-realworld-example-app
  - 依赖react-query.v5、openapi-typescript-fetch、use-local-storage-state
  - https://github.com/likui628/react-realworld-example-app

- https://github.com/gothinkster/web-components-realworld-example-app /201705/js/archived
  - Exemplary real world application built with Vanilla JS Web Components
- https://github.com/mits-gossau/event-driven-web-components-realworld-example-app /202303/js
  - https://mits-gossau.github.io/event-driven-web-components-realworld-example-app/
  - Exemplary real world application built with Vanilla JS Web Components in an Event Driven Architecture
  - Frontend Event Driven Architecture works basically like the DOM itself. There are loosely coupled components (nodes), which emit events and those get captured by controllers also called stores, routers, etc. Those controllers emit events on their behalf, which the components can consume.

- https://github.com/Ch4mpl00/real-world-app-cqrs-es /202301/ts/inactive
  - demonstrate a fully fledged fullstack application built with Serverless Node.js + Typescript. 
  - It includes such cool patterns as CQRS, EventSourcing and DDD with functional programming flavor
  - Node.js + TS + Dynamodb
- https://github.com/gothinkster/spring-boot-realworld-example-app /MIT/202206/java/inactive
  - demonstrate a fully fledged full-stack application built with Spring boot + Mybatis including CRUD operations, authentication, routing, pagination, and more.
  - implement GraphQL and REST at the same time.

- https://github.com/mutoe/preact-realworld-example-app /202112/js
  - https://mutoe.github.io/preact-realworld-example-app
  - 依赖zustand
- https://github.com/romansndlr/react-vite-realworld-example-app /202204/js
  - 依赖valtio、react-query.v3

- https://github.com/7anshuai/react-mobx-typescript-realworld-example-app /202212/ts
  - https://7anshuai.js.org/react-mobx-typescript-realworld-example-app/
  - Realworld app built with React Hooks + Mobx + TypeScript

- https://github.com/solidjs/solid-realworld /202204/js
  - Solid.js codebase containing real world examples (CRUD, auth, advanced patterns, etc) that adheres to the RealWorld spec and API.

- https://github.com/Coding-Dodo/owl-realworld-app /202112/js
  - OWL RealWorld App Implementation. This application make use of Odoo Web Library as a standalone JavaScript project

- https://github.com/moleculerjs/moleculer-realworld-example-app /MIT/201711/js
  - RealWorld example app with Moleculer microservices framework

- https://github.com/randyscotsmithey/feathers-realworld-example-app /MIT/201902/js/inactive
  - Feathers implementation for RealWorld example app
  - 依赖feathersjs-nedb、mongoose
  - https://github.com/cirosantilli/feathers-realworld-example-app
    - port from MongoDB to sequelize

- https://github.com/maruakinu/couchbase-springboot-realworld-example-app /202305/java
  - a backend project using springboot that uses Couchbase for its Database.
- https://github.com/mgroves/realworld-aspnet-couchbase /MIT/202311/csharp
  - Conduit implementation: ASP. NET Core + Couchbase
  - [How to Build Real World Web Applications with Couchbase_202308](https://www.couchbase.com/blog/build-real-world-web-apps-couchbase/)

- https://github.com/marmelab/argos-realworld /202103/js
  - This repository stores several versions of the database, API and client of the realworld app, for digital footprint measurements.
  - We've cloned and tweaked implementations of the realworld frontend and backend apps, so that they can work together 

### api-realworld

- https://github.com/cirosantilli/node-express-sequelize-nextjs-realworld-example-app /202208/后端js+前端ts
  - Node.js + Express.js + Sequelize + SQLite/PostgreSQL + Next.js fullstack static/SSG/ISG Example Realworld App
  - https://github.com/cirosantilli/node-express-sequelize-realworld-example-app /202106/js

- https://github.com/TonyMckes/conduit-realworld-example-app /202303/js/be+fe
  - created to demonstrate a fully fledged fullstack application built with React / Express.js / Sequelize / PostgreSQL including CRUD operations, authentication, routing, pagination, and more.

- https://github.com/skopekreep/typescript-node-express-realworld-example-app /202007/ts
  - Rewrite of JS-based node-express RealWorld backend app using Typescript
  - 依赖express-jwt、jsonwebtoken、mongoose、passport
  - https://github.com/RaoofJM/nodejs-typescript-realworld-backend /202306/ts/inactive
    - RealWorld Example of a NodeJS Rest API using TypeScript, MongoDB, Redis and Docker
    - 依赖express、mongoose、redis
- https://github.com/tranlehaiquan/nodejs-api-realworld /202308/ts
  - RestFul with Express, Typescript
  - 依赖mongoose、jsonwebtoken

- https://github.com/winterrrrrff/realWorld-server /202212/js
  - server-side of realWorld project using Express.js and MongoDB
  - https://github.com/Raywire/node-express-realworld-conduit /202101/js

- https://github.com/Varun-Hegde/Conduit_NodeJS /202105/js
  - Express and NodeJS based backend implementation of the RealWorld API Spec.
  - MySQL + Sequelize
- https://github.com/coding-blocks-archives/Realworld_NodeJS_Sequelize /201902/js
  - an implementation of Thinkster's realworld.io API 
  - MySQL/SQLite/Postgres

- https://github.com/gothinkster/koa-knex-realworld-example /201910/js
  - Example Node. Js (Koa.js + Knex) codebase containing real world examples (CRUD, auth, advanced patterns, etc) that adheres to the RealWorld spec and API.

- https://github.com/oldmanfleming/koa-boilerplate /MIT/202005/ts
  - Koa + Typescript + TypeORM

- https://github.com/gothinkster/node-express-realworld-example-app /201802/js
- Example Node (Express + Mongoose) codebase containing real world examples (CRUD, auth, advanced patterns, etc) that adheres to the RealWorld API spec

- https://github.com/launchbadge/realworld-axum-sqlx /202203/rust
  - A Rust implementation of the Realworld demo app spec using Axum and SQLx
  - Best practices are always in flux, and a major point of this project was to experiment with project architecture and suss out what those best practices might look like.
- https://github.com/hseeberger/realworld-backend /202311/rust
  - RealWorld backend implementations in Rust, using different frameworks (enabled via respective features)
  - axum
  - poem-openapi
  - https://github.com/hseeberger/realworld-frontend
    - RealWorld frontend implementation in Rust, using Leptos
- https://github.com/dxps/fullstack-rust-axum-dioxus-rwa /202306/rust
  - RealWorld app implementation as a Fullstack Rust project using Axum (be) and Dioxus (fe)
- https://github.com/snamiki1212/realworld-v1-rust-actix-web-diesel /202306/rust
  - RealWorld with Rust + ActixWeb + Diesel on Clean Architecture
- https://github.com/jetli/rust-yew-realworld-example-app /202310/rust
  - https://jetli.github.io/rust-yew-realworld-example-app/
  - Rust + Yew + WebAssembly codebase containing real world examples (CRUD, auth, advanced patterns, etc) that adheres to the RealWorld spec and API.
  - created to demonstrate a fully fledged WebAssembly web application built with Yew including CRUD operations, authentication, routing, pagination, and more.
  - It utilizes Yew's latest function components and hooks. 
  - It also supports desktop application powered by Tauri.
- https://github.com/JoeyMckenzie/realworld-rust-axum-sqlx /202208/rust
  - A fullstack RealWorld implementation using rust, axum, sqlx, and yew!
- https://github.com/fairingrey/actix-realworld-example-app /201909/rust
  - Implementation of the RealWorld backend API spec in Actix

- https://github.com/DataDog/flask-realworld-example-app /202311/python
  - Exemplary real world JSON API built with Flask

- https://github.com/kenyipp/realworld-python-example-app /202306/python
  - scalable RealWorld app implemented with Python, Flask, AWS Lambda, and tested with high-quality unit and integration tests

- https://github.com/err0r500/go-realworld-clean /201808/go
  - a clean architecture implementation of the realworldapp
# vanillajs
- https://github.com/aman-maharshi/vanilla-js /202304/js
  - Projects using pure JavaScript without any external libraries or frameworks

- https://github.com/bradtraversy/vanillawebprojects /202311/js
  - https://vanillawebprojects.com/
  - Mini projects built with HTML5, CSS & JavaScript. No frameworks or libraries
  - This is the main repository for all of the projects in the course.

- DoX /6Star/NALic/202308/js/ejs
  - https://github.com/AlbertCerfeda/DoX
  - https://doxeditor.herokuapp.com/
  - 依赖 prosemirror-collab、express、passport、socket.io、bootstrap4、mongodb、html-to-image
  - features
    - 文档支持简单分享、权限设置
    - 协作支持显示光标
  - DoX Editor aims to be a web text editor application that allows users to create, edit, store and share several documents.
  - A web text editor application that allows users to create, edit, store and share several documents, with support for real-time collaborative editing.
  - DoX is clearly inspired to well known online word processors such as Google Docs

- https://github.com/ibm-watson-data-lab/shopping-list-vanillajs-pouchdb /201802/js
  - Shopping List is an Offline First demo Progressive Web App built using Vanilla JS and PouchDB.

- https://github.com/basir/node-javascript-ecommerce /188Star/202211/js
  - Build ECommerce Like Amazon Using Vanilla JS
  - Node & Express: Web API, Body Parser, File Upload, JWT
  - MongoDB: Mongoose, Aggregation

- https://github.com/HimanshuMishir/Shopping /202302/js
  - a simple Shopping website I tried to make using vanilla JavaScript, nodeJs, MongoDB.

- https://github.com/8mecem8/Vanilla-Js-eCommerce /202108/js
  - Mini Amazon like pure-Js eCommerce project
  - used OOP programming model with JS 'Class' to write components
  - I used dynamic routing with JS without page refresh. For payment Methods I used paypal api.
- https://github.com/mav-raj/eCommerce-vanillaJS /201908/js
  - https://ecommerce-ca4fb.firebaseapp.com/
  - a eCommerce web app built using HTML, CSS and vanilla JS

- https://github.com/Anthony29p/Online-Shop-VanillaJS /202209/js
  - https://online-shop-vanilla-js.vercel.app/
  - online shop on Vanilla JS source.

- https://github.com/egrep6021ad/VanillaJS-MongoDB-FullStack /202210/js
  - https://egrep6021ad.github.io/VanillaJS-MongoDB-FullStack/
  - a collaborative project intended to create a small website that has similar functionality to Zillow or a related website.

- https://github.com/Jaykhun/vanilla-js-online-store /202305/js
  - https://jaykhun.github.io/vanilla-js-online-store
  - My online store built with Vanilla JavaScript and IndexedDB offers product search, registration, login, and cart functions. 
  - It also features an admin panel for adding products, managing users, and changing order status.

- https://github.com/Nemwel-Boniface/awesomeBooksModules /202204/js
  - https://nemwel-boniface.github.io/awesomeBooksModules/
  - a vanilla Javascript which offers CRUD functionalities allowing you to add, remove edit books info and store it to the local storage.

- https://github.com/Flo-314/Members-only /202201/js
  - an app created with PUG(jadeJS), Express, NodeJS, Passport JS, CSS vanilla.

- https://github.com/tmmluis/user-management /202310/ts
  - https://candid-sunburst-c11b14.netlify.app/
  - A simple user management dashboard created with vanilla javascript (and CSS) for educational purposes.
  - to explore some of the native web APIs, most notably custom elements
  - It utilizes Reqres as a source of fake backend data to simulate a login flow and load initial user information
  - https://github.com/Faisalramzan282/User-Admin_Role_Auth_VanillaJS /js

- https://github.com/CodePapa360/Friends-TvSeries-Site /202308/js
  - https://friends-tv-series-codepapa360.netlify.app/
  - Built entirely from scratch using only JavaScript – no frameworks or libraries involved.
- https://github.com/CodePapa360/Forkify-Recipe-App /202304/js
  - https://forkify-alamin.netlify.app/
  - a recipe search and saving app, built with HTML5, CSS3, and JavaScript.
  - The app uses advanced JavaScript concepts like asynchronous programming, ES6 modules, and object-oriented programming

- https://github.com/alireza-mh/multipage-vanilla-js-app /202012/ts
  - create multipage dynamic pages with vanilla JS

- https://github.com/JeremyLikness/vanillajs-deck /202001/js
  - https://blog.jeremylikness.com/series/vanilla.js/
  - A Vanilla.js Single Page App (SPA) slide deck for a presentation about Vanilla.js written with no frameworks.

- https://github.com/Aditya-Mankar/Expenses-Manager /202008/js
  - https://expenses-manager-app.netlify.app/
  - A Vanilla JavaScript application for managing your Expenses
  - https://github.com/hamzayousuf121/expense-tracker /js

- https://github.com/kitsaway/todo-app /202301/js
  - https://kitsaway.github.io/todo-app/
  - Simple Todo app that allows user to create, update, delete and filter items in todo list.

- https://github.com/RobinLinus/snapdrop /GPLv3/202303/js
  - https://snapdrop.net/
  - local file sharing in your browser. Inspired by Apple's Airdrop.
  - Vanilla HTML5/ES6/CSS3 frontend
  - WebRTC/WebSockets

- https://github.com/codersgyan/realtime-chat-app /202006/js/inactive
  - Realtime chat app using socket.io and vanilla JavaScript
- https://github.com/shubhankar-shandilya-india/Talkative /202303/js
  - https://talkative-f5ky.onrender.com/
  - It is a Realtime chat app using socket.io and vanilla JavaScript.
  - https://github.com/ebenezerdon/chat-app-vanilla-js

- https://github.com/oktadev/okta-vanilla-js-example /202201/js
  - A Vanilla JavaScript App with Authentication
  - [Add Authentication to Your Vanilla JavaScript App in 20 Minutes | Okta Developer](https://developer.okta.com/blog/2018/06/05/authentication-vanilla-js)
  - Okta has Authentication and User Management APIs that reduce development time with instant-on

- https://github.com/stanulilic/vanillajs-weatherapp /201910/js
  - https://stanulilic.github.io/vanillajs-weatherapp/
  - Weatherapp made with vanilla Javascript(es6+)
  - https://github.com/wecodeschool/vanilla-weather-app /202310/js
  - https://github.com/fidalgodev/weather-app

- https://github.com/theodoremoreland/WeatherDashboard /202309/js
  - https://theodoremoreland.github.io/WeatherDashboard/
  - A weather dashboard built atop the OpenWeather API using vanilla JavaScript and vanilla CSS.

## vanilla-clone

- https://github.com/anup-a/Linxta-Markdown-Editor /202006/js
  - https://anup-a.github.io/Linxta-Markdown-Editor/
  - A Simple stack edit clone using showdownjs and Vanilla JS.

- https://github.com/eunchurn/vanillajs-notion-clone /202210/ts/starter
  - https://github.com/hr0123/vanillajs-notion-clone-haeri
  - https://eunchurn.github.io/vanillajs-notion-clone/
  - brew install pkg-config cairo pango libpng jpeg giflib

- https://github.com/ryong9rrr/vanilla-notion-v2.0 /202307/ts
  - https://sangyoon-notion-vanilla.vercel.app/
  - Notion Clone using only Vanilla TS(sangyoon-ui).
  - 支持页面树、内容编辑
  - https://github.com/hyoribogo/vanillaJS-notion /js/提交多
  - https://github.com/bbearcookie/Notion_VanillaJS /js
  - https://github.com/MyeonghoonNam/Notion-Clone

- https://github.com/loevray/notion-clone /202310/js
  - notion cloning with vanillaJs
- https://github.com/AlangGY/VanillaJS-Notion-Clone /202201/js
  - DocumentsList
  - DocumentSearch
  - https://github.com/HeeSeok-kim/VanillaJS_clone_notion
  - https://github.com/Jeong-Taeho/-VanillaJS-Notion-Clone
  - https://github.com/Kimbangg/w4-Project_Notion_VanillaJS
  - https://github.com/chasj0326/chacha_notion_js

- https://github.com/tanwarAalok/google-sheet-clone /202309/js
  - https://google-sheet-clone.netlify.app/
  - A google sheets clone developed using Vanilla Javascript
  - more
  - https://github.com/Yashkanekar/excel-vanilla-js
  - https://github.com/Raj-Stark/Google-Sheet-2.0
  - https://github.com/noobCode-69/ExcelClone
  - https://github.com/PrinceAttri/sheets-clone

- https://github.com/SemenSavlook/Excel-SPA /202210/js
  - https://semensavlook.github.io/Excel-SPA/out/
  - Excel-clone SPA on VanillaJS

- https://github.com/amanksdotdev/excel-clone /202105/js
  - https://amanksdotdev.github.io/excel-clone/
  - Clone of Excel using vanilla javascript
  - 依赖只有electron，支持在线和打包

- https://github.com/bisho1995/VanillaJsGoogleSheetClone /202008/js
  - https://loving-jepsen-425599.netlify.app/
  - Google sheets clone, 样式过于简陋

- https://github.com/Charlygraphy23/VanillaJs-sheet /202307/js
  - https://astonishing-bavarois-450233.nelva is backetlify.app/
  - google sheet clone with vanilla JS

- https://github.com/waterrmalann/kards /MIT/202309/js
  - https://waterrmalann.github.io/kards/
  - A simple cards-based kanban board app inspired by Trello in pure vanilla JS
- https://github.com/PawanKolhe/BoardX /202101/js
  - Kanban board web app for project management build with vanilla JavaScript

- https://github.com/manjunath00/Trello-Clone-Using-DOM /202001/js
  - Trello Clone using Vanilla Javascript, HTML5, CSS3
  - https://github.com/Skulkrone/trello_clone-vanillajs /ts
  - https://github.com/Adrien-GOGOIS/Trello_clone_Typescript_Vanilla /ts

- https://github.com/lesterbx/trello-clone-vanilla /201801/js
  - https://lesterbx.github.io/trello-clone-vanilla/
  - Trello like app made with vanillaJS to practice with Drag and Drop API.
- https://github.com/albertoarf13/trelloClone /202011/js
  - Trello clone with vanilla Javascript, HTML and CSS. (web app)

- https://github.com/msawaguchi/paint_xp_clone /202212/js
  - Aesthetic version of Windows XP Paint clone in pure VanillaJS

- https://github.com/vladji/piskel-clone /202306/js
  - https://pixel-art-vladji.netlify.app/
  - Web App (vanilla JS). draw-editor. creating slides, export to .gif/.apng
- https://github.com/JacintoDesign/paint-clone /202007/js/canvas
  - https://jacintodesign.github.io/paint-clone/
  - ZTM VanillaJS: making a paint clone with HTML canvas.
  - https://github.com/RostoRM/PaintClone

- https://github.com/Master-Mind/VanillaWiki /202309/js
  - https://vanilla-wiki.onrender.com/
  - A basic wikipedia clone with vanilla html/css/js/node. 
  - 样式混乱

- https://github.com/chaseottofy/google-calendar-clone-vanilla /202303/js
  - https://chaseottofy.github.io/google-calendar-clone-vanilla/
  - zero dependency clone of google calendar written in vanilla js
  - Zero third party resources used
  - All code is written in vanilla javascript, html, and css.
  - At the moment, the application works using local storage but there are options to backup data and load previously saved data using json.

- https://github.com/AurelianSpodarec/Calendar_Dashboard /202002/js
  - https://calendar-dashboard.netlify.com/#calendar
  - Vanilla JavaScript SPA developed by utilising ideas of React and redux

- https://github.com/trybrito/google-drive-clone /202110/js
  - A Vanilla JavaScript application that proposes to clone, in addition to the interface, the on-demand file upload functionality of Google Drive
  - 后端依赖socket.io、busboy-formdata

- https://github.com/maykbrito/vanilla-ui-clone-dropbox-home /202008/js
  - https://github.com/rocketseat-content/youtube-clone-dropbox-menu
  - https://cranky-einstein-aff725.netlify.app/
  - 模仿dropbox的首页，简洁大方

- https://github.com/chamsom/hacker-news-clone /202008/js
  - https://chamsom.github.io/hacker-news-clone/
  - Project built with Vanilla JS and HTML/CSS.

- https://github.com/altankurt/twitter-ui-clone /202304/js
  - https://twitter-js-clone.vercel.app/
  - Twitter UI clone w/ Vanilla JS
- https://github.com/dylancbailey/Tweeter--Twitter-Clone- /202309/js
  - Twitter clone built with vanilla JS

- https://github.com/about14sheep/survey-donkey /202007/js/pug/inactive
  - Survey Monkey clone, rendered with Pug from Express NodeJS backend. 
  - Frontend in HTML5, CSS3, and vanilla JavaScript

- https://github.com/Sirneij/slack-clone-ui /202010/js
  - https://sirneij.github.io/slack-clone-ui/
  - A responsive and beautiful slack clone UI with rich text editor created from scratch using HTML5, CSS3 and Vanilla JavaScrip
  - [Building Slack UI with pure HTML5, CSS3 and JavaScript: The power of CSS grids and flexbox - DEV Community_202107](https://dev.to/sirneij/building-slack-ui-with-pure-html5-css3-and-javascript-the-power-of-css-grids-and-flexbox-4ban)

- https://github.com/nitishkumar31/imdb-clone /202306/js
  - https://nitishkumar31.github.io/imdb-clone/
  - IMDb clone using vanilla JavaScript, which gives ratings of the latest movies
  - The main feature of the app is its ability to search for movie and provide a trailer of that movie using the tmdb API and youtube API. 

- https://github.com/JS0303/vanillajs-movie-app /202302/ts
  - https://vanillajs-movie-app-kappa.vercel.app/
  - fastcampus Movie search app

- https://github.com/geonwoo-jeong/youtube-clone /201911/ts
  - Youtube clone with VanillaJS, NodeJS, Typescript, Pug
- https://github.com/bbanderson/YouTube. /202008/js
  - Cloning YouTube 99.99% in Full Stack
- https://github.com/jaeyeonling/youtube-clone /201904/js
  - Cloning youtube with VanillaJS, NodeJS, Pug, MongoDB
  - https://github.com/HyeonWooGa/youtube-clone-fullstack-reloaded

- https://github.com/hotaroo-dev/netflix-clone /202304/js
  - https://netflix-clone-nine-sandy.vercel.app/
  - Netflix Clone with vanilla JS
  - Modal pop-up Movie Detail after clickling movie img
  - Add movie to list  localStorage

- https://github.com/sriniD-dev/zoom-clone /202012/js
  - built using Node.js live link:of the zoom clone
  - express for fetching api, used socket-io for real-time api.
- https://github.com/joshua-figueroa/zoom-clone /202009/js
  - Zoom Clone using WebRTC and PeerJS.

- https://github.com/S1lv2R/Desmos /202208/js
  - https://www.desmos.com/calculator
  - clone with vanilla javascript, using for learning Math such as drawing graphs
  - There are 2 interpretation types: math.js; js-eval

- https://github.com/leedokchidok19/clone-vanillaJs-tree /202203/js
  - https://leedokchidok19.github.io/clone-vanillaJs-tree/
  - Draw a tree with JavaScript, 类似插画的黑色树枝无叶树

- https://github.com/Bakaji/simple-postman-clone /202207/js
  - a simple postman clone app using vanillaJS, Ace editor, bootstrap and vite
# admin/dashboard
- https://github.com/webDevSaiF/bank_app_JS /202308/js
  - https://webdevsaif.github.io/bank_app_JS/
  - learn while building an interactive banking application using vanilla JavaScript. 

- https://github.com/zernonia/Dashboard-BI /202003/js/inactive
  - https://zernonia.github.io/Dashboard-BI/
  - Simple Drag-and-Drop Analytics Dashboard using Vanilla Javascript
  - inspired by Business Intelligence tools like Microsoft PowerBI, Tableau, Qliksense and etc.
  - 依赖D3.js, Dc-js, Crossfilter.js

- https://github.com/themesberg/volt-bootstrap-5-dashboard /202107/js/inactive
  - https://themesberg.com/docs/volt-bootstrap-5-dashboard/getting-started/quick-start/
  - https://demo.themesberg.com/volt/
  - built using only Vanilla JS
  - built using the latest version of Bootstrap 5

- https://github.com/adminkit/adminkit /1.3kStar/MIT/202306/js/scss
  - https://demo.adminkit.io/
  - Dashboard template based on Bootstrap 5
  - 依赖bootstrap、flatpickr、chartjs.v2、simplebar
  - AdminKit, and all third-party libraries used in the admin template, do not require jQuery as a dependency.
  - 付费版才提供多个color schemes

- https://github.com/PlainAdmin/plain-free-bootstrap-admin-template /202309/js
  - https://plainadmin.com/
  - open-source Vanilla JS admin dashboard template based on Bootstrap 5

- https://github.com/mostafizurhimself/admintoolkit-html /202307/js
  - https://getadmintoolkit.com/
  - Admin template based on TailwindCSS and Vanilla JavaScript

- https://github.com/asterginete/vanillajs-admin-dashboard /202308/js/jquery
  - An admin dashboard using VanillaJS and Jquery
  - This admin dashboard provides CRUD functionality for user profiles.

## admin-fwk

- https://github.com/jetlinks/jetlinks-ui-antd
  - 演示地址：http://demo.jetlinks.cn
  - 项目多处采用了SSE接口交互，开发需要使用dev环境变量（生产环境使用nginx代理了EventSource接口）

- https://github.com/CoCreate-app/CoCreate-dashboard /202311/js/单文件
  - A simple dashboard component in vanilla javascript.
  - 依赖CoCreate.js
# apps
- https://github.com/Veri5ied/slack-ui-clone /202012/js
  - React, Vanilla CSS, Material UI Icons, Reach Router and Firestore Slack Clone
# apps-api
- https://github.com/hiteshchoudhary/apihub /MIT/202401/js
  - https://freeapi.app/
  - Your own API Hub to learn and master API interaction.
  - We are trying to build a single source API hub that can be used to learn api handling in any programming language.
  - our API hub offers custom endpoints that provide a hands-on experience in handling API responses.
  - our API hub also provides advanced APIs to challenge and stretch your skills.
  - Our open-source project is currently hosted on a remote server, where we are forced to reset the entire server, including the file system and MongoDB database, every 2 hours to avoid incurring additional costs.

- https://github.com/1FarZ1/Task-Manager-NodeJs /202310/js
  - A Complete Task Manager Built Using NodeJs, Express, MongoDb, VanillaJs

- https://github.com/matt212/Nodejs_Postgresql_VanillaJS_Fastify /202208/js
  - Config based Node.js and PostgreSQL Web App Boilerplate/Scaffolding with custom RBAC and stream-based CSV upload and download mechanics.
# auth
- https://github.com/auth0-blog/spa-jwt-authentication-tutorial /201507/js
  - Add authentication to a vanilla js single page app

- https://github.com/rajeshpillai/node-jwt-step-by-step /202005/js
  - A simple express jwt server with vanilla javascript client for testing
  - backend + frontend

- https://github.com/LeeSoMyoung/Express-NodeJS-Auth-with-JWT /202202/js
  - NodeJS, Express, MySQL, Vanilla JS로 구현한 Authentication

- https://github.com/cornflourblue/node-mongo-registration-login-api /202007/js
  - NodeJS + MongoDB API for User Management, Authentication and Registration
  - [NodeJS + MongoDB - Simple API for Authentication, Registration and User Management | Jason Watmore's Blog](https://jasonwatmore.com/post/2018/06/14/nodejs-mongodb-simple-api-for-authentication-registration-and-user-management)
# pwa
- https://github.com/hemanth/awesome-pwa
  - Useful resources for creating Progressive Web Apps

- https://github.com/tastejs/hacker-news-pwas /202010/ts/archived
  - https://hnpwa.com/
  - Hacker News readers as Progressive Web Apps. A spiritual successor to TodoMVC
- https://github.com/cristianbote/hnpwa-vanilla /202111/js
  - Hacker News PWA implement ed using no framework just javascript
# notes
- https://github.com/HarshitRoy812/notes-app /202301/js
  - Developed a full-authenticated notes app using Vanilla and Express JS. Authenticated the app using JWT library.

- https://github.com/dcode-youtube/single-page-app-vanilla-js /js
  - Taken from my YouTube Tutorial: https://www.youtube.com/watch?v=6BozpmSjk-Y
- https://github.com/dcode-youtube/notes-app-javascript-localstorage /2020107/js
  - A Notes App built with vanilla JavaScript and Local Storage.
- https://github.com/navdeepm20/Notes_app_in_JavaScript /202211/js
  - Notes App build using Vanilla Js that saves notes on your browser local storage

- https://github.com/BernardoAguayoOrtega/google-keep-clone /202011/js
  - https://bernardoaguayoortega.github.io/google-keep-clone/public/
  - Google keep clone created with vanilla.js, css and html <3
- https://github.com/nikldev0/google-keep-clone
  - https://kind-villani-04f47c.netlify.app/
- https://github.com/AjayShukla007/KeepNote-clone-vanillaJS
  - a clone of google KeepNote from scratch using html, css, JavaScript, anime.css, all.js and combination.js(a js library created by me by combining different js libraries like hammer.js, fabric.js)

- https://github.com/MeheliR/Notables /MIT/202401/js
  - https://mehelir.github.io/Notables/
  - Create, Read, Update, Delete (CRUD) in Vanilla JavaScript : Note Taking Application
# more
