---
title: toc-db-sync-pouchdb-couchdb
tags: [couchdb, pouchdb, synchronization, toc]
created: 2022-11-30T18:55:16.304Z
modified: 2022-11-30T18:56:07.072Z
---

# toc-db-sync-pouchdb-couchdb

# guide

- pouchdb的同步协议参考 [CouchDB Replication Protocol](https://docs.couchdb.org/en/stable/replication/protocol.html)

- alternatives
  - pouchdb server    /inactive

- [CouchDB Best Practices](https://jo.github.io/couchdb-best-practices/)
  - https://github.com/jo/couchdb-best-practices
  - Apache CouchDB™ is a database that uses JSON for documents, JavaScript for MapReduce indexes, and regular HTTP for its API.
# couchdb-pouchdb
- pouchdb /15.4kStar/apache2/202211/js/core代码量不大
  - https://github.com/pouchdb/pouchdb
  - https://pouchdb.com/
  - PouchDB is an open-source JavaScript database inspired by Apache CouchDB that is designed to run well within the browser.
  - It enables applications to store data locally while offline, then synchronize it with CouchDB and compatible servers when the application is back online
  - PouchDB is not a self-contained database; 
    - it is a CouchDB-style abstraction layer over other databases. 
    - PouchDB supports all modern browsers, using IndexedDB under the hood and falling back to WebSQL where IndexedDB isn't supported.
    - In Node.js, PouchDB uses LevelDB under the hood, and also supports many other backends via the LevelUP ecosystem.
  - The main benefit is to be able to replicate data with any CouchDB compatible endpoint. 
    - Because of the CouchDB compatibility, PouchDB has to do a lot of overhead in handling the revision tree of document, which is why it can show bad performance for bigger datasets.
    - RxDB was originally build around PouchDB until the storage layer was abstracted out in version 10.0.0(202107)
    - PouchDB has some performance issues because of how it has to store the document revision tree to stay compatible with the CouchDB API.

- pouchdb-server /894Star/apache2/202108/js/内存/sqlite
  - https://github.com/pouchdb/pouchdb-server
  - PouchDB Server is a drop-in replacement for CouchDB, using PouchDB and Node.js.
  - 依赖pouchdb、bluebird、couchdb-render、express、xhr2
  - PouchDB Server can run fully in-memory (no changes are saved)
    - Or it can run using SQLite rather than LevelDB
  - It is modeled after the single-node design of CouchDB 1.x, although it contains some CouchDB 2.x features such as Mango queries.
  - PouchDB Server is much less battle-tested than CouchDB, but it does pass the full PouchDB test suite.
  - https://github.com/gr2m/pouchdb-security
    - fork of pouchdb-security package, fixes pouchdb-server#97
- https://github.com/gr2m/spawn-pouchdb-server /202103/js
  - Configurable per-app pouchdb-server as a drop-in replacement for CouchDB
  - Simplify development setup
- https://github.com/demon24ru/PouchDB-server-test
  - pouchdb-adapter-websql-core + SQLite
  - https://github.com/demon24ru/PouchDB-websql-SQLite-server
- https://github.com/demon24ru/PouchDB-server-test-proxy
  - pouchdb proxy with JWT authentication

- microcouch-js /3Star/apache2/202209/js
  - https://github.com/jo/microcouch-js
  - A minimal Pouch-like implementation of a CouchDB compatible in-browser couch, for educational purpose.
  - Data model is the same as PouchDBs new `indexeddb` adapter.
  - Microcouch uses PouchDBs `pouchdb-merge` module.
  - Microcouch is quiet small, currently less than 30kB minified. It is about five times smaller and replicates almost ten times faster than PouchDB, depending on the document structure.
- https://github.com/jo/microcouch-rs /202205/rust
  - A minimal Pouch-like implementation of a CouchDB compatible embeddable couch. 
  - Work in progress.
- https://github.com/jo/rouchdb /202204/rust
  - Minimal CouchDB compatible database written in Rust.

- delta-pouch /184Star/apache2/201706/js
  - https://github.com/redgeoff/delta-pouch
  - Conflict-free collaborative editing for PouchDB
  - A PouchDB plugin for partial updates that uses the every-doc-is-a-delta storage pattern. 
  - You can use delta pouch to enable conflict-free collaborative editing of the same docs.

- pouchdb-sync-to-anything /43Star/MIT/201807/js
  - https://github.com/karlwestin/pouchdb-sync-to-anything
  - This is a plugin that lets you use CouchDBs replication algorithm with checkpointing, resuming, etc, but provide your own function to write the documents. 
  - This can be used to sequentially write updates to a REST API, 
  - This is a partial implementation of the CouchDB replication protocol. 
    - It allows you to use PouchDB's tools to save replication checkpoints for syncing with your API. 
    - Using those checkpoints, we can start the next replication from the last good checkpoint.

- jscouch /159Star/apache2/201202/js
  - https://github.com/janl/jscouch
  - A partial JavaScript re-implementation of CouchDB.

- shootingstick /1Star/apache2/202210/ts
  - https://github.com/AndyA/shootingstick
  - A CouchDB clone
  - 依赖sqlite、express、lodash

- couchdb /5.5kStar/apache2/202211/erlang
  - https://github.com/apache/couchdb
  - https://couchdb.apache.org/
  - Seamless multi-master syncing database with an intuitive HTTP/JSON API, designed for reliability
  - CouchDB is a database that completely embraces the web. 
    - Store your data with JSON documents. 
    - Access your documents with your web browser, via HTTP. 
    - Query, combine, and transform your documents with JavaScript. 
    - You can distribute your data, efficiently using CouchDB’s incremental replication.
    - CouchDB comes with a suite of features, such as on-the-fly document transformation and real-time change notifications
  - [CouchDB Replication Protocol](https://docs.couchdb.org/en/stable/replication/protocol.html)
    - Couch Replication Protocol is implemented in a variety of projects and products that span every imaginable computing environment from globally distributed server-clusters, over mobile phones to web browsers.
- https://github.com/apache/couchdb-nano
  - The official Apache CouchDB library for Node.js

- hoodie /4.3kStar/apache2/202101/js
  - https://github.com/hoodiehq/hoodie
  - The Offline First JavaScript Backend
  - hoodie can be used standalone or as a hapi plugin. 
  - https://github.com/hoodiehq/hoodie-server
    - Hapi plugin for Hoodie’s server core module
  - https://github.com/hoodiehq/hoodie-client
    - Client API for the Hoodie server

- https://github.com/cloudant/meteor-couchdb
  - Meteor database driver for CouchDB and Cloudant
  - an efficient Livequery implementation providing real-time updates from the database by consuming the CouchDB _changes feed
  - Distributed Data Protocol (DDP) RPC end-points for updating the data from clients connected over the wire
# mobile-pc
- https://github.com/craftzdog/pouchdb-adapter-react-native-sqlite /202108/js
  - PouchDB adapter using ReactNative SQLite as its backing store
  - SQLite storage performs much faster than AsyncStorage, especially with secondary index.

- https://github.com/craftzdog/pouchdb-react-native-demo /202108/js
  - A working demo for PouchDB on React Native with SQLite3 storage

- pouchdb-react-native /472Star/MIT/202010/js
  - https://github.com/seigel/pouchdb-react-native
  - PouchDB, the React Native-only edition. A preset representing the PouchDB code that runs in React Native.
  - preset contains the version of PouchDB that is designed for React Native. In particular, it ships with the AsyncStorage adapter as its default adapter. 

- https://github.com/craftzdog/react-native-sqlite-2 /202211/ts
  - SQLite3 Native Plugin for React Native for Android, iOS, Windows and macOS.
  - It works pretty well with PouchDB on React Native app.
  - The reason for this plugin is that react-native-sqlite-storage has some problems when used with PouchDB

- https://github.com/demon24ru/pouchdb-adapter-sqlite-node /202108/js
  - pouchdb-adapter-sqlite for Node.js

- https://github.com/cozy-labs/cozy-desktop
  - File Synchronisation for Cozy on Desktop and Laptop
# pouchdb-utils
- https://github.com/pouchdb-community/relational-pouch /202211/ts
  - a plugin for PouchDB that allows you to interact with PouchDB/CouchDB like a relational data store, with types and relations.
  - The main goal of this is to provide an API that is as similar to Ember Data and jsonapi as possible, while still being performant and Pouch-like.
- https://github.com/iyobo/pouchorm /202205/ts
  - The definitive ORM for working with PouchDB.
  - Introduces the concept of Collections to pouchdb
  - Supports web, electron, react-native, and anything else
- https://github.com/Agrejus/pouchdb-entity-fabric /202209/ts
  - PouchDB ORM modeled after .net's Entity Framework
- https://github.com/compactd/slothdb /201808/ts
  - A typescript ORM that uses annotation and classes to describe the database

- https://github.com/infinity-arc/ts-express-pouchdb-server /202003/js
  - powerful API that can be run as a micro service to power progressive web applications.
- https://github.com/pouchdb/pouchdb-express-router /201911/js
  - an expressjs routing module that provides the minimal API to allow PouchDB instance to replicate over HTTP, 
  - it is designed to be mounted into expressjs web application to prove the an endpoint for PouchDB applications to sync with.
- https://github.com/marten-de-vries/pouchdb-seamless-auth /201706/js
  - Seamless switching between online (CouchDB) and offline (PouchDB) authentication.
  - This plug-in stores password hashes in a local PouchDB, not a smart thing

- https://github.com/pouchdb-community/pouchdb-quick-search /370Star/apache2/201702/js/lunr/inactive
  - efficient and accurate full-text search engine built on top of PouchDB
  - The underlying tokenization/stemming/stopword engine is Lunr, which is optimized for English text, using a variant of the Porter stemmer. 
  - This is a local plugin, so it is not designed to work against CouchDB/Cloudant/etc. 
  - If you'd like to search against the server, use the CouchDB Lucene plugin, Cloudant's search indexes, or something similar.

- https://github.com/onyxcodes/dbmanager-ui /202208/ts
  - UI for managing PouchDB databases through DBManager interface layer

- https://github.com/vicentedealencar/redux-pouchdb /201912/js
  - sync store state to pouchdb
  - The PouchDB database persists the state of chosen parts of the Redux store every time it changes.
- https://github.com/medihack/redux-pouchdb-plus /201806/js
  - Synchronize Redux store with PouchDB to have a persistent store.

- https://github.com/Terreii/use-pouchdb /202206/ts
  - a collection of React Hooks to access data in a PouchDB database from React components.
- https://github.com/davidmartinez10/use-pouchdb-collection /202204/ts
  - simple React hook for PouchDB. 
  - Designed to be as simple and easy to use as React.useState().
- https://github.com/stanlemon/react-pouchdb /202205/ts
  - https://github.com/stanlemon/javascript/tree/main/packages/react-pouchdb
  - React components for interacting with PouchDB documents. 
  - These components can be used to wrap parts of an application and both load and save state to a document. 
  - These components can be used both with React and React Native.
- https://github.com/ArnoSaine/react-pouchdb /202009/js
  - React wrapper for PouchDB that also subscribes to changes.

- https://github.com/NotWoods/csv-to-pouch /202204/js
  - Parse CSV files and save their data to a PouchDB database.

- https://github.com/pouchdb-community/transform-pouch /202108/js
  - PouchDB plugin for modifying documents before and after storage in the database.
  - Apply a transform function to documents before and after they are stored in the database. 
- https://github.com/snowyu/pouchdb-transform.js /202210/ts
  - PouchDB Advanced Transform Library
- https://github.com/chorpler/pouchdb-auth-utils /202209/ts
  - PouchDB Authentication plugin, revised for PouchDB >=7.0.0 and requiring promises
  - To get started, just install CouchDB, throw in a little SSL, and you've got everything you need for your site's authentication.
  - This plugin uses vanilla CouchDB.
- https://github.com/Aam-Digital/replication-backend /202209/ts
  - This backend service can be used to filter the replication between a PouchDB and a CouchDB instance based on permission rules. 
  - It does this by overriding some of CouchDB's endpoints where permissions are checked on the transmitted entities. 
  - The permission rules are defined through CASL.

- https://github.com/MazeMap/Leaflet.TileLayer.PouchDBCached /202203/js
  - A Leaflet tile layer which caches into PouchDB for offline use

- https://github.com/cdaringe/pouchy /202107/ts
  - Pouchy wraps & extends PouchDB and provides various sorely needed sugar methods.
  - most methods provided are very simple PouchDB-native method modifiers, but are targeted to save you frequent boilerplate re-typing!

- https://github.com/calvinmetcalf/crypto-pouch /202110/js
  - plugin for encrypted pouchdb/couchdb databases
  - This only encrypts the contents of documents, not the `_id` or `_rev`, nor view keys and values
  - encrypts documents using TweetNaCl.js, an audited encryption library. It uses the xsalsa20-poly1305 algorithm.
- https://github.com/garbados/comdb
  - A PouchDB plugin that transparently encrypts and decrypts its data

- https://github.com/pouchdb-community/worker-pouch /201802/js
  - Adapter plugin to use PouchDB over Web Workers and Service Workers. 
  - Transparently proxies all PouchDB API requests to the worker, so that the most expensive database operations are run in a separate thread.

- https://github.com/pouchdb-community/pouchdb-full-sync /201607/js
  - Fully replicate two PouchDB or CouchDB databases, while preserving absolutely all document history and conflicts.
  - Useful for: Implementing infinite undo/redo in your app
  - Normally, the CouchDB replication protocol only replicates the leafs between two databases. This preserves conflicts (which is awesome!), but it discards non-leafs for performance reasons.

- https://github.com/pietervandereems/PeerPouch /201501/js
  - PouchDB over WebRTC
  - A plugin for PouchDB which allows a remote PouchDB instance to be used locally. 
  - It transfers data over WebRTC, for simple lower-latency remote access and even particularly peer-to-peer replication!
- https://github.com/scottmtp/pouch-replicate-webrtc /201510/js
  - Replicate a PouchDB over a WebRTC DataChannel, for NodeJS and the Browser.

- https://github.com/dpmcmlxxvi/pouchdb-geospatial /202211/js
  - PouchDB geospatial query plugin.
  - provides spatial querying of GeoJSON objects. 
  - Any GeoJSON object inserted into the database via the the plugin API is spatially indexed using an `R-Tree`.
  - GeoJSON objects within a PouchDB database can be queried against an input GeoJSON object to test if they satisfy one of the DE-9IM spatial predicates

- https://github.com/neojski/visualizeRevTree /201606/js
  - Visualize couchdb/pouchdb revision tree right in your browser

- https://github.com/genbliz/mocody
  - Implementation of single table design, and unified query access for MongoDB, CouchDB, and dynamoDB.

- https://github.com/thaibault/couchdb-web-node-plugin
  - PouchDB with model specification/checking, user authentication and right management as web-node plugin.
  - A database server, model instance conflict handler, rest api, authentication, session management, schema validator and model relation guarantee for webNode.
# couchdb-utils
- https://github.com/glynnbird/couchmigrate
  - CouchDB command-line design document migration tool
  - https://github.com/glynnbird/couchimport
  - https://github.com/glynnbird/couchfirehose

- https://github.com/demsking/fakecouch /202101/ts/inactive
  - A fake CouchDB server for testing.
  - a fake CouchDB server which implements endpoints used in common applications.
  - It does not claim to be use as a regular CouchDB server. 
  - It uses some static data as result for some database requests.

- https://github.com/mikeal/couchup /201307/js
  - A CouchDB implementation on top of levelup.
  - The goal is to build a data model well suited for mobile applications that may need to work offline and sync later on and maintain smart client side caches. 
  - The goal is to build a data model well suited for mobile applications that may need to work offline and sync later on and maintain smart client side caches. 
  - This data model is inspired by CouchDB but diverges greatly in the way it handles and resolves the revision history and conflicts. 
  - couchup implements a "most writes wins" conflict resolution scheme and does not require or even allow user specific conflict resolution.

- https://github.com/kowsik/memcouchd /201103/js
  - It's a pure JavaScript in-memory implementation of some aspects of CouchDB with a nodejs/connect Web front-end.

- https://github.com/chris-l/mock-couch /201807/js
  - A node.js module designed to mock a CouchDB server, mostly for unit testing purposes.

- https://github.com/medic/couch2pg /202209/js
  - Library and app to replicate a CouchDB database to PostgreSQL
- https://github.com/sysadminmike/couch-to-postgres /201710/js
  - Node libary to stream CouchDB changes into PostgreSQL

- https://github.com/iriscouch/couchjs
  - CouchJS is a command-line Node.js program. 
  - It is 100% compatible with Apache CouchDB's built-in JavaScript system.

- https://github.com/jcrugzz/changes-stream
  - A fault tolerant changes stream with builtin retry HEAVILY inspired by follow.

- https://github.com/mehtaarn000/reactdrive /202211/js
  - File storage system built with Reactjs, Expressjs, Nodejs, and CouchDB.
# examples
- https://github.com/acailly/easy-pouchdb-server /202105/js
  - Deploy a PouchDB server easily
  - running pouchdb server is perfect for small hobby projects or proof of concepts. 

- https://github.com/mradultiw/Wassup /202105/js
  - a client-server based desktop chat application written in Javascript
  - It has a central server and database which is used to connect clients together. 
  - Each client has it's own local database. 

- https://github.com/roldaojr/ra-data-pouchdb /202204/js
  - PouchDB/CouchDB data provider for [react-admin](https://github.com/marmelab/react-admin)
  - This data provider takes a PouchDB object as input, then creates a client-side data provider around it.

- https://github.com/starikan/pouchdb-viewer /202104/js
  - Standalone PouchDB viewer powered by Electron and pouchdb-server

- https://github.com/kbrisso/file-base /202210/js/ts
  - Filebase is a database for your files and directories.
  - Filebase does not modify your existing files or directories 

- https://github.com/GustavoLopez04/pouchdb
  - getting started tutorial for PouchDB
  - The newest push has code to replicate the PouchDB database to CouchDB and UI testing with WDIO.

- https://github.com/genglefr/my-gallery /201804/js
  - Image gallery, in sync thx to PouchDB and Couchbase Sync Gateway websocket
  - a proof of concept for synching pouchdb - couchdb databases, using base64 images as documents. 
  - Since 19/02/2018, the sync is done over websocket of sync gateway.

- https://github.com/pouchdb/pouchbase /201604/js
  - PouchBase is a service that lets your PouchDB applications easily provide login and online sync functionality.
- https://github.com/daleharvey/pouchbase
  - a test server for PouchDB, it provides open online databases that you can use to test PouchDB sync with.

- https://github.com/wonderwhy-er/offline-first-seed /201603/js
  - Minimalistic JavaScript offline first application seed using PouchDB and ServiceWorker
  - Uses Express/Node for server. Runs PouchDB both on server and client to allow working offline and sync when online Uses ServiceWorker to allow running page/app while offline Uses MaterializeCSS for styling

- https://github.com/fasiha/gotanda-pouchdb-server /202011/ts
  - A centralized Node.js server for your PouchDB-wielding local-first apps to sync to. Multiple users ok, multiple apps ok. Login with GitHub.
  - This repo, Gotanda PouchDB, is intended to service apps that use PouchDB to store their data locally—web apps or mobile apps or wherever PouchDB is supported.
  - your apps direct users to log into Gotanda with their GitHub login. Gotanda stores a minimal amount of data from GitHub.
  - Your app creates a remote PouchDB, pointing to a Gotanda URL, which logs in with cookie authentication (Gotanda also supports token authentication).

- https://github.com/cozy/pouchdb-playground /202104/js
  - Make queries with PouchDB and measure performances.
  - Hacking the Cozy Pouchdb playground app requires you to setup a dev environment.

- https://github.com/ibm-watson-data-lab/shopping-list-react-pouchdb /202004/js
  - an Offline First demo Progressive Web App built using React and PouchDB
  - PouchDB syncs its data with a remote IBM Cloudant database.
  - PouchDB can synchronize with CouchDB and compatible servers.
- https://github.com/ibm-watson-data-lab/shopping-list-preact-pouchdb /201808/js
  - a reference implementation of an Offline First shopping list app, built as a Progressive Web App using Preact and PouchDB.

- https://github.com/mohammadnazari110/pwa_offline_video_download /201905/js
  - this is a sample PWA app for download video and store to indexedDB with pouchDB

- https://github.com/ayastreb/money-tracker /202211/js
  - an open-source progressive web app that allows you to track your income and expenses.
  - Data is stored locally on device in PouchDB database and can be synced to the cloud.

- https://github.com/duytq94/react-native-note-with-pouchdb /201910/js
  - Making a simple note app with PouchDB in React Native

- https://github.com/YuJiaHao/pouch-note-app /202206/js
  - a practice with react pouchdb and couchdb
- https://github.com/IvanAprea/react-client-couchdb 202206/ts
  - sudo docker-compose -f docker-compose.dev.yml

- https://github.com/Tunetown/Notes /202210/js
  - https://notes.webertom.net/
  - This is a Notes Taking App based purely on CouchDB and JavaScript

- https://github.com/danobot/notorious /202102/ts
  - Offline-first note taking application for desktop and the web
  - Notorious backend is a CouchDB database and an optional web interface for accessing Notorious through a web browser. 
# more
- https://github.com/KouchDB/replication-source-poc /202211/java
  - CouchDB mock replication source Proof Of Concept. 
  - Demonstrates how to stand-up a Java Springboot service as a source for CouchDB replication.
