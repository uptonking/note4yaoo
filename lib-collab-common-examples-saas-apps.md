---
title: lib-collab-common-examples-saas-apps
tags: [collaboration, examples, saas, toc]
created: 2022-11-05T10:35:19.525Z
modified: 2023-01-17T19:14:47.611Z
---

# lib-collab-common-examples-saas-apps

# guide
- sync-xp
  - 基于缓存实现sync有点类似于react-query
  - 参考vlcn

- 协作方案参考
  - Liveblocks, synced-store, FluidFramework, gun
  - automerge (2017), yjs (2015), sharedb (2013)
# collab-platform
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

- https://github.com/excalidraw/excalidraw-room
  - Collaboration server for Excalidraw

- cryptpad /AGPLv3/202301/js
  - https://github.com/xwiki-labs/cryptpad
  - https://cryptpad.org/
  - CryptPad is a collaboration suite that is end-to-end-encrypted and open-source. 
  - It is built to enable collaboration, synchronizing changes to documents in real time. 
  - Because all data is encrypted, the service and its administrators have no way of seeing the content being edited and stored.
  - https://github.com/xwiki-labs/chainpad-server
    - Implements a websocket server compatible with netflux-websocket client as per the Netflux 2.0 specification.
    - https://github.com/xwiki-labs/netflux-spec2
  - https://github.com/xwiki-labs/chainpad-listmap
    - collaborative lists and maps in the browser

- https://github.com/SerenityNotes/serenity-notes-clients
  - Serenity Notes iOS/Android/macOS
  - 不支持web
  - 依赖prosemirror
  - [Serenity Notes](https://www.serenity.re/en/notes/technical-documentation)
    - end-to-end encryption must using the Olm & Megolm cryptographic ratchets
- https://github.com/SerenityNotes/Serenity
  - End-to-end encrypted collaborative notes
- https://github.com/SerenityNotes/serenity-notes-backend
  - End-to-end encrypted collaborative notes app
- https://github.com/SerenityNotes/naisho
  - architecture to relay end-to-end encrypted CRDTs over a central service.
  - It was created out of the need to have an end-to-end encrypted protocol to allow data synchronization/fetching incl.

- CoCreateJS /19Star/MIT/202212/js
  - https://github.com/CoCreate-app/CoCreateJS
  - https://cocreate.app/
  - A collaborative low code headless CMS and Javascript framework for building collaborative no code platforms, apps and UI
  - A dependency free, vanilla javascript Realtime CRUD and Collaboration Framework. 
  - https://github.com/CoCreate-app/CoCreate-crud-client /202212/js
  - An useful CRUD api operate Create, read, update, delete with built in database. 
  - Can be used as a firebase alternative
 - https://github.com/CoCreate-app/CoCreateWS
    - Server Side for CoCreateJS. Containing websocket, crud, auth, server side rendering, and permission components.
  - https://github.com/CoCreate-app/CoCreate-admin
    - A No Code Admin, CRM, CMS, Website Builder platform. 
    - Powered by CoCreateJS to provide Realtime and Collaborative CRUD functionality.

- https://github.com/Zeekg-zk/Collaborative-Platform /202210/ts/inactive
  - 团队协作与管理平台，具有在线多人聊天、消息实时推送、协同编辑等功能
  - 前端使用 NextJS 12.2.0，后端使用 NestJS 8.0
  - 后台管理界面使用 Ant Design Pro
  - 支持多人协作文档（使用 Quill 富文本编辑器）

- https://github.com/adarshaacharya/MentorLabs /ts
  - MentorLabs is a a WebRTC based video conferencing app.
  - 前端依赖 redux/toolkit
  - 后端依赖 express、typeorm

- https://github.com/IdrisIsra/phantom-notepad-T3 /202210/ts
  - A collaborative notepad using T3 stack with websockets and Redis
  - 依赖nextjs、tanstack-query.v4、trpc

- https://github.com/Unleash/unleash
  - https://demo.unleash-hosted.com/
  - Unleash is the open source feature toggle service.
  - Unleash increases efficiency and gives teams full control of how and when they enable new functionality for end users.
- https://github.com/flipt-io/flipt /go
  - https://flipt.io/
  - open source, self-hosted feature flag solution

- https://github.com/hedgedoc/hedgedoc
  - HedgeDoc (formerly known as CodiMD) is an open-source, web-based, self-hosted, collaborative markdown editor.

- https://github.com/plankanban/planka /AGPLv3/js
  - https://plankanban.github.io/planka/
  - The realtime kanban board for workgroups built with React and Redux.
  - React, Redux, Redux-Saga, Redux-ORM, Semantic UI React, react-beautiful-dnd
  - Sails.js, Knex.js, PostgreSQL

- https://github.com/MicroHealthLLC/mSuite /ruby/vue
  - Real Time Collaboration Made Simple for concept maps, kanban, documents and spreadsheets.

- https://github.com/RocketChat/Rocket.Chat
  - fully customizable communications platform developed in JavaScript for organizations with high standards of data protection.
  - We are a MERN based application enabling real-time conversations
- https://github.com/bigbluebutton/bigbluebutton
  - open source web conferencing system.
  - supports real-time sharing of audio, video, slides (with whiteboard controls), chat, and the screen. 
  - https://github.com/fmeringdal/nettu-meet
    - Open source video conferencing system for tutors.

- https://github.com/elicesw2-project2/synergy
  - All-in-one Workspace Collaboration Tools

- https://github.com/atharmohammad/Code-N-Collab /202110/js/inactive
  - a Collaborative Website for developers and competitive coders who likes to code and discuss about topics , problems or issues

- https://github.com/sagemathinc/cocalc
  - CoCalc is web-based software that enables collaboration in research, teaching, and scientific publishing.
# collab-apps
- https://github.com/configu/configu
  - A generic standard for managing and collaborating software configurations 

- https://github.com/scarfacedotcom/NANCY-APP
  - Nancy App has been built with React and Firebase, something similar to asana.com 

- sanity /4kStar/MIT/202301/ts/slate
  - https://github.com/sanity-io/sanity
  - Sanity Studio – Collaborate in real-time on structured content
  - It comes with an open-source editing environment called Sanity Studio that you can customize with JavaScript and a real-time hosted data store. 
  - Sanity is a platform for creating and working with structured content. Your content is stored in the cloud
  - [Provide a (real) self hosted version](https://github.com/sanity-io/sanity/issues/3258)
    - how to run Sanity frontend without depending on privative Sanity backend? 
    - Sanity Studio is only the editor interface, though. Sanity's hosted content backend, the Sanity Content Lake, on the other hand, is not open-source.

- https://github.com/hanse/groceries
  - Real-time Collaborative Grocery Lists
- https://github.com/saiboten/onskdeg
  - Wish List App - collaborative wish lists
- https://github.com/moryyiim/task-list
  - A collaborative project for a to-do list

- https://github.com/ShariqAli-Dev/bug-tracker
  - collaborative bug tracking app that monitors and eliminates bugs in software development projects
  - 前端 + 后端

- https://github.com/hyoo-ru/talks.hyoo.ru
  - Embeddable/standalone offline-first messenger with collaborative abilities and speech recognition.
  - Application based on `$mol` framework in MAM ecosystem. 
  - It uses $hyoo_sync_server to share reactive state between clients and merge changes without conflicts.

- https://github.com/knohow/palanote
  - A creative, collaborative note taking and sharing app

- https://github.com/Thomas-Basham/collab-done
  - A social media React web app for musicians to connect and collaborate. 
  - Built with NextJS, ReactJS, Supabase

- https://github.com/docs-plus/docs.plus
  - real-time collaborative tool that enables communities to share and organize knowledge in a hierarchical manner

- https://github.com/Slatebox/slatebox
  - https://slatebox.com/
  - Real-time visual team collaboration for remote teams
# realtime-room
- https://github.com/Poujhit/Chatzilla
  - Chat Room Application made using React/Typescript and NodeJs-Web sockets.
  - All your chats are not stored anywhere. Even the chat rooms are not stored anywhere.

- https://github.com/nshosain/real-time-chat-app-with-rooms
  - real-time chat app with rooms : TypeScript, NodeJs, Express, React, Socket IO and MongoDB

- https://github.com/geckosio/geckos.io
  - Geckos.io offers real-time client/server communication over UDP using WebRTC and Node.js
  - People who have never build a multiplayer game, should probably use a library like socket.io instead, since there are way more examples/tutorial available.
  - Socket.io and geckos.io use a similar API. The switch from socket.io to geckos.io should be easy.

- https://github.com/deepstreamIO/deepstream.io
  - open source server inspired by concepts behind financial trading technology. 
  - It allows clients and backend services to sync data, send messages and make rpcs at very high speed and scale.
# utils
- clientdb /506Star/apache2/202207/ts/同步未完成
  - https://github.com/clientdb/clientdb
  - ClientDB is an in-memory database for enabling real-time web apps.
  - The architecture of clientdb is inspired by the Linear app
  - 依赖flexsearch、knex、express、socket.io、lodash
  - [sync-engine work in progress](https://github.com/clientdb/clientdb/pull/10)
  - [differences and advantages compared to RxDB](https://github.com/clientdb/clientdb/issues/12)
- https://github.com/Bhavik-ag/B-Docs
  - an online document editor to create, edit and collaborate on online documents.
  - Version Control and Hosting : Git for Source Code Management and Github for Hosting

- https://github.com/orda-io/orda /go
  - A client and server written in Go. 
  - CRDT-based data synchronization supporting document database.
  - Orda project is a multi-device data synchronization platform based on MongoDB 
  - Orda is based on CRDT(conflict-free data types), which enables operation-based synchronization.
  - https://github.com/orda-io/orda-js
    - Javascript(or Typescript) SDK for Orda project. 

- sync_server-nedb /33Star/MIT/201807/js
  - https://github.com/nponiros/sync_server
  - A simple server which can be used to synchronize data from multiple devices
  - A small node server which uses NeDB to write data to the disk. 
    - The database used to store the data. Currently only NeDB is supported
  - The server can be used with a client for example `SyncClient` to save change sets which can later be synchronized with other devices. 
    - The server was made to work with the `ISyncProtocol` and `Dexie.Syncable`. 
    - 👉🏻 It supports the poll pattern using AJAX and the react pattern using nodejs-websocket.
- sync_client-dexie /29Star/MIT/201804/js
  - https://github.com/nponiros/sync_client
  - This module can be used to write data to IndexedDB using `Dexie` and to synchronize the data in IndexedDB with a server.
  - `Dexie.Syncable` is used for the synchronization. This module contains an implementation of the `ISyncProtocol`. 
  - It was primarily written to work with `sync-server` but should work with other servers which offer the same API.

- gun/gundb /16.9kStar/MIT/202302/js
  - https://github.com/amark/gun
  - GUN is an ecosystem of tools that let you build community run and encrypted applications - like an Open Source Firebase or a Decentralized Dropbox.
  - GUN supports more than just key/value pairs, it is a graph database that can store SQL-like tables, JSON-like documents, files and livestreaming video, plus relational and hypergraph data!
  - [Is GUN suitable for building collaborative text editor using causal-tree merging strategy?](https://github.com/amark/gun/issues/459)
  - Gun is a graph database. I don't think Orbit uses a graph system, but instead uses feeds or KV stores. So that's a another difference. But Gun can use IPFS as a storage adapter if you wanted.

- https://github.com/holochain/holochain /202212/rust
  - Holochain is an open-source framework to develop peer-to-peer applications with high levels of security, reliability, and performance.
  - simplified version of Holochain on Rust (sometimes called Holochain RSM for Refactored State Model)

- https://github.com/gundb/panic-server
  - Panic is an end-to-end testing framework, designed specifically for distributed systems and collaborative apps.
  - At gunDB, we're building a real-time, distributed JS database.
  - We needed a testing tool that could simulate complex scenarios, and programmatically report success or failure. 

- https://github.com/earthstar-project/react-earthstar
  - https://earthstar-project.org/
  - A library for using React with Earthstar, a library for building syncing, decentralised online tools.
- https://github.com/earthstar-project/earthstar
  - Earthstar is a specification and Javascript library for building online tools you can truly call your own.

- https://github.com/google/ot-crdt-papers
  - This repository will hold papers Raph Levien is writing on technologies for collaborative text editing, in particular at the intersection of Operational Transformation and Conflict-free Replicated Data Types (CRDT's).
  - It also holds a prototype implementation in JavaScript, using socket.io.
# more
- https://github.com/linagora/Twake
  - 后端php
  - Twake is a secure open source collaboration platform to improve organizational productivity.
  - Team chat
  - File Storage
  - Team Calendar
  - Task Management
  - 前端依赖minimongo

- https://github.com/digitallyinduced/thin-backend /202211/js/ts/inactive
  - a Blazing Fast, Universal Web App Backend for Making Realtime Single Page Apps
  - Thin Backend has a built-in GUI-based schema designer, helps to quickly build the DDL statements for your database schema
  - Thin Backend is built on top of the production-proven [IHP](https://github.com/digitallyinduced/ihp) architecture & libraries.

- https://github.com/shadyy41/codeshack
  - a WebRTC based collaborative coding app which also supports peer-to-peer video calling.