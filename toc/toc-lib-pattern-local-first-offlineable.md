---
title: toc-lib-pattern-local-first-offlineable
tags: [lib, local-first, pattern, toc]
created: '2021-08-25T15:50:00.635Z'
modified: '2021-09-04T14:03:39.046Z'
---

# toc-lib-pattern-local-first-offlineable

# guide

- search: local-first, local first, offline first
# popular
- https://github.com/redux-offline/redux-offline
  - Build Offline-First Apps for Web and React Native
  - Persistent Redux store for Reasonaboutable Offline-First applications, with first-class support for optimistic UI. 
  - Use with React, React Native, or as standalone state container for any web app.

- https://github.com/jaredly/local-first
  - This aims to eventually be a fully-featured solution for managing, syncing, and storing application data, in a way that works offline, and collaboratively.

- https://github.com/logux/client
  - https://logux.io/
  - Logux is a new way to connect client and server. 
  - Instead of sending HTTP requests (e.g., AJAX and GraphQL) it synchronizes log of operations between client, server, and other clients.
  - Logux and WebSocket client/server framework to make:
    - Logux has features inspired by CRDT to resolve edit conflicts between users. Real-time updates to prevent conflicts
    - Logux combines WebSocket with modern reactive client architecture. It synchronizes Redux actions between clients and servers, and keeps the same order of actions.
    - Offline-first for the next billion users or New York City Subway. Logux saves Redux actions to IndexedDB and has a lot of features to merge changes from different users.
    - Compatible with modern stack: Redux, Vuex and pure JS API, works with any back-end language and any database.

- https://github.com/nornagon/autowiki
  - Autowiki is a tool for creating networked documents.
  - Autowiki is a local-first app: you own all the data you put into it, and your data never leaves your own machine unless you want it to.
  - Autowiki uses automerge under the hood to resolve edit conflicts automatically.

- https://github.com/hoodiehq/hoodie
  - Hoodie lets you build apps without thinking about the backend and makes sure that they work great independent of connectivity.
  - https://github.com/hoodiehq/hoodie-app-tracker

- https://github.com/local-first-web/state
  - A Redux-based state container for local-first software, offering seamless synchronization using Automerge CRDTs. (Formerly known as fish Cevitxe).
  - @localfirst/state is an automatically replicated Redux store that gives your app offline capabilities and secure peer-to-peer synchronization superpowers.

- https://github.com/tinyplex/tinybase
  - https://tinybase.org/
  - TinyBase is a smarter way to structure your application state
  - Familiar concepts of tables, rows, and cells, and schematization to model your data domain.
  - Flexibly reactive to reconciled updates, so you only spend cycles on the data that changes.
  - Indexing, metrics, relationships - and even an undo stack for your app state!
  - Easily sync your data to local or remote storage, and use idiomatic bindings to your React UI.

- https://github.com/pubkey/rxdb
  - A client side, offline-first, reactive database for JavaScript Applications
  - RxDB is not a self contained database. It is a wrapper arround another database that implements the `RxStorage` interface. At the moment you can either use PouchDB or Dexie.js or LokiJS as underlaying storage. Each of them respectively has it's own adapters that can be swapped out, depending on your needs. For example you can use and IndexedDB based storage in the browser, and an SQLite storage in your hybrid app
# local-first examples
- https://github.com/unigraph-dev/unigraph-dev
  - A local-first and universal knowledge graph, personal search engine, and workspace for your life.

- https://github.com/digidem/mapeo-desktop
  - An offline map editing application for indigenous territory mapping in remote environments. 
  - It uses mapeo-core for offline peer-to-peer synchronization of an OpenStreetMap database, without any server. 
  - The map editor is based on iDEditor. 
  - The app is built with Electron.
# offline
- https://github.com/localForage/localForage
  - Offline storage, improved. Wraps IndexedDB, WebSQL, or localStorage using a simple but powerful API.

- https://github.com/hoodiehq/hoodie
  - A generic backend with a client API for Offline First applications

- https://github.com/lana-k/sqliteviz
  - Instant offline SQL-powered data visualisation in your browser
  - Sqliteviz is a single-page offline-first PWA for fully client-side visualisation of SQLite databases or CSV files.
  - run SQL queries against a SQLite database and create Plotly charts and pivot tables based on the result sets
# collab
- https://github.com/YousefED/Matrix-CRDT
  - Use Matrix as a backend for local-first applications with the Matrix-CRDT Yjs provider.

- https://github.com/rocicorp/replicache
  - Realtime Sync for Any Backend Stack
# more
- https://github.com/cwise89/react-detect-offline
  - Components that track offline and online state. Render certain content only when online (or only when offline).

- https://github.com/dxxzst/OfflineMap
  - 基于MySQL + Node.js + Leaflet的离线地图展示，支持百度、谷歌、高德、腾讯地图
