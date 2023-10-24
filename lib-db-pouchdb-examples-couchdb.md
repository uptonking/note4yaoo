---
title: lib-db-pouchdb-examples-couchdb
tags: [couchdb, database, examples, pouchdb, toc]
created: 2022-11-30T18:55:16.304Z
modified: 2023-09-28T20:35:56.153Z
---

# lib-db-pouchdb-examples-couchdb

# guide

- [CouchDB Best Practices](https://jo.github.io/couchdb-best-practices/)
  - https://github.com/jo/couchdb-best-practices
  - Apache CouchDB™ is a database that uses JSON for documents, JavaScript for MapReduce indexes, and regular HTTP for its API.

- fans-pouchdb
  - https://github.com/redgeoff/delta-pouch
  - https://github.com/garrensmith/couch_hack_week
  - https://github.com/daleharvey/pouchbase
  - https://github.com/nolanlawson/pouchdb-find
    - https://github.com/nolanlawson/pouchdb-mapreduce-no-ddocs
    - https://news.ycombinator.com/threads?id=nolanl
# pouchdb-couchdb
- https://github.com/pubkey/client-side-databases
  - https://pubkey.github.io/client-side-databases/database-comparison/index.html
  - I have implemented the exact same chat application with different database technologies.
  - The chat app is a web based angular application, with functionality similar to Whatsapp Web.
  - PouchDB with IndexedDB adapter & CouchDB replication
  - RxDB PouchDB with PouchDB Storage & GraphQL replication
  - RxDB LokiJS with LokiJS Storage & GraphQL replication
  - RxDB Dexie.js with Dexie.js Storage & GraphQL replication
  - WatermelonDB with LokiJS adapter (no backend sync atm)

- https://github.com/AugurProject/pouchdb-perf /ts
  - https://augurproject.github.io/pouchdb-perf/
  - PouchDB Perf Test

- https://github.com/ezpaarse-project/dbbench /201412/archived
  - A basic benching tool to compare node.js embedded databases
  - It inserts randomly generated objects with string identifiers, then queries random identifiers for a given period of time.

- pouchdb /16kStar/apache2/202310/js/core代码量不大
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
  - [how to to do partial (descending)l sync? F.e. chat messages](https://github.com/pouchdb/pouchdb/issues/8221)
    - You can use filtered replication
  - forks
  - https://github.com/emtee40/pouchdb-js

- pouchdb-server /894Star/apache2/202108/js/内存/sqlite
  - https://github.com/pouchdb/pouchdb-server
  - PouchDB Server is a drop-in replacement for CouchDB, using PouchDB and Node.js.
  - 依赖pouchdb、bluebird、couchdb-render、express、xhr2
  - PouchDB Server can run fully in-memory (no changes are saved)
    - Or it can run using SQLite rather than LevelDB
  - It is modeled after the single-node design of CouchDB 1.x, although it contains some CouchDB 2.x features such as Mango queries.
  - PouchDB Server is much less battle-tested than CouchDB, but it does pass the full PouchDB test suite.
  - https://github.com/eingress/docker-pouchdb-server
    - a drop-in replacement for CouchDB, using PouchDB and Node.js
  - https://github.com/CliffCrerar/poucdb-server-docker-image
    - Create a couchdb like pouchdb server docker image with a fauxton console
  - forks
  - https://github.com/VislaLabs/pouchdb-server
  - https://github.com/qiaogaojian/contribute_pouchdb-server
  - https://github.com/grengojbo/pouchdb-server
  - https://github.com/cognition-app/pouchdb-server
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
  - A PouchDB plugin for partial updates that uses the **every-doc-is-a-delta** storage pattern. 
  - You can use delta pouch to enable conflict-free collaborative editing of the same docs.
  - Delta pouch stores every change as a doc.
  - [Question: a helpful link describing the "every-doc-is-a-delta storage pattern"?](https://github.com/redgeoff/delta-pouch/issues/53)
    - Sounds like "every-doc-is-a-delta" is another way of saying "log database". Is that right?
    - I would look up anything related to "Event Sourcing" which perhaps is a superset of this idea. Basically, the idea is that you save the events that happen in your system and then compile those into views.
  - forks
    - https://github.com/Brainsway-Cloud/delta-pouch

- https://github.com/IconCMO/pouch-datalog /js/inactive
  - Datomic-like Datalog queries for PouchDB
  - The query engine is a fork from Datascript.
  - 依赖datascript
  - https://github.com/IconCMO/datascript
    - An immutable in-memory database and Datalog query engine in ClojureScript.
  - https://github.com/dahjelle/dataquery
    - Forked the query language from Datascript, and changed to only utilize external indexes in an asynchronous manner.

- https://github.com/delta-db/deltadb /201602/js/inactive
  - DeltaDB is an offline-first database designed to talk directly to clients and works great offline and online.
  - Stores all data as a series of deltas, which allows for smooth collaborative experiences even in frequently offline scenarios.
  - I have decided to suspend development of DeltaDB for the following reasons:
  - last-write-wins policy is nice when starting a new project as it is automatic, but other conflict resolution policies that force the user to manually resolve the conflict, like CouchDB’s revision protocol, have become more of the standard in the offline-first world.
  - Building a DB that scales and is Building a DB that scales and is distributed over many nodes, takes a lot of work. distributed over many nodes, takes a lot of work. 

- pouchdb-sync-to-anything /43Star/MIT/201807/js
  - https://github.com/karlwestin/pouchdb-sync-to-anything
  - This is a plugin that lets you use CouchDBs replication algorithm with checkpointing, resuming, etc, but provide your own function to write the documents. 
  - This can be used to sequentially write updates to a REST API, 
  - This is a partial implementation of the CouchDB replication protocol. 
    - It allows you to use PouchDB's tools to save replication checkpoints for syncing with your API. 
    - Using those checkpoints, we can start the next replication from the last good checkpoint.

- shootingstick /1Star/apache2/202210/ts
  - https://github.com/AndyA/shootingstick
  - A CouchDB clone
  - 依赖sqlite、express、lodash

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

## couch-like

- https://github.com/demsking/fakecouch /202101/ts/inactive
  - A fake CouchDB server for testing.
  - a fake CouchDB server which implements endpoints used in common applications.
  - It does not claim to be use as a regular CouchDB server. 
  - It uses some static data as result for some database requests.

- jscouch /159Star/apache2/201202/js
  - https://github.com/janl/jscouch
  - A partial JavaScript re-implementation of CouchDB.

- https://github.com/garrensmith/couch_hack_week /rust/inactive
  - An implementation of CouchDB using Rust and FoundationDB for Cloudant's hackweek 25 May 2020 - 4 June 2020.
  - The aim was to be able to read `/{db}/_all_docs`.
  - [MiniCouchDB in Rust_202006](https://www.garrensmith.com/minicouchdb-in-rust/)

- https://github.com/mikeal/couchup /201307/js
  - A CouchDB implementation on top of levelup.
  - The goal is to build a data model well suited for mobile applications that may need to work offline and sync later on and maintain smart client side caches. 
  - The goal is to build a data model well suited for mobile applications that may need to work offline and sync later on and maintain smart client side caches. 
  - This data model is inspired by CouchDB but diverges greatly in the way it handles and resolves the revision history and conflicts. 
  - couchup implements a "most writes wins" conflict resolution scheme and does not require or even allow user specific conflict resolution.

- https://github.com/kowsik/memcouchd /201103/js
  - a pure JavaScript in-memory implementation of some aspects of CouchDB with a nodejs/connect Web front-end.

- https://github.com/chris-l/mock-couch /201807/js
  - A node.js module designed to mock a CouchDB server, mostly for unit testing purposes.

- https://github.com/marten-de-vries/chairdb /python/inactive
  - A small CouchDB-compatible database with sync support

- https://github.com/fiatjaf/summadb /go/inactive
  - A hierarchical database that stores computed values.
  - For more fine-grained permissions and other features I'm also developing a small Go database compatible with PouchDB
  - https://github.com/fiatjaf/summuladb
    - A SummaDB that runs in the browser.
# mobile-pc
- https://github.com/craftzdog/pouchdb-adapter-react-native-sqlite /202108/js
  - PouchDB adapter using ReactNative SQLite as its backing store
  - SQLite storage performs much faster than AsyncStorage, especially with secondary index.

- https://github.com/craftzdog/pouchdb-react-native-demo /202108/js
  - A working demo for PouchDB on React Native with SQLite3 storage

- https://github.com/craftzdog/react-native-sqlite-2 /202211/ts
  - SQLite3 Native Plugin for React Native for Android, iOS, Windows and macOS.
  - It works pretty well with PouchDB on React Native app.
  - The reason for this plugin is that react-native-sqlite-storage has some problems when used with PouchDB

- https://github.com/seigel/pouchdb-react-native /472Star/MIT/202010/js
  - PouchDB, the React Native-only edition. A preset representing the PouchDB code that runs in React Native.
  - preset contains the version of PouchDB that is designed for React Native. In particular, it ships with the AsyncStorage adapter as its default adapter. 

- https://github.com/demon24ru/pouchdb-adapter-sqlite-node /202108/js
  - pouchdb-adapter-sqlite for Node.js

- https://github.com/cozy-labs/cozy-desktop
  - File Synchronisation for Cozy on Desktop and Laptop
# pouchdb-event
- https://github.com/stockulus/pouchdb-event-store /201708/js
  - mimimal eventStore on top of pouchdb

- https://github.com/EternalDeiwos/panmnesia /201712/js
  - An action registry and redux-based aggregate store for a PouchDB-based event stream.

- https://github.com/thomastoye/field-journal /ts/pouchdb
  - https://field-journal.pages.dev/
  - An experimental browser-based, offline-first, event-sourced dispatching, messaging, and incident tracking application.

- https://github.com/patrickpang/perpetual /201809/js
  - A WIP Life Management System = Todos + Calendar + Notes Implemented as a Progressive Web App
  - Offline editing
  - PouchDB
  - Workbox

- https://github.com/twilson63/vflow-pouchdb /201502/js
  - an abstraction around pouchDB's changes feed and it creates a simple api for interacting with the write stream system. 
  - It basically breaks it down into an event emitter.
# server
- https://github.com/infinity-arc/ts-express-pouchdb-server /202003/js
  - powerful API that can be run as a micro service to power progressive web applications.
- https://github.com/pouchdb/pouchdb-express-router /201911/js
  - an expressjs routing module that provides the minimal API to allow PouchDB instance to replicate over HTTP, 
  - it is designed to be mounted into expressjs web application to prove the an endpoint for PouchDB applications to sync with.

- https://github.com/CoMfUcIoS/session-pouchdb-store /js
  - PouchDB express session store. Can do realtime session data synchronization via PouchDB server
  - Default in-memory PouchDB instance.

- https://github.com/CoMfUcIoS/socket.io-pouch /js
  - PouchDB and CouchDB over WebSockets, using Socket.io

- https://github.com/DEEJ4Y/pouchdb-services /ts
  - A set of PouchDB service functions and a class version of them, with `mongodb` style `ObjectID` id's for all your documents.

- https://github.com/stanlemon/couchdb-userdb /js
  - A tool for managing user specific databases in an Apache CouchDB tool. If you are using CouchDB and are able to flip on the "user db" setting you have no need for this tool
# pouchdb-utils
- https://github.com/i-mizzle/electron-react-pouchdb-boilerplate /202309/js
  - Boilerplate template for an electron application. with react and pouchDB
- https://github.com/quepas/electron-leveldown-pouchdb-webpack /202211/js
  - example

- https://github.com/nicolas-albert/prebuilt-pouchdb
  - Experiment the duration of a prebuilt PouchDB database, including replication and index computing to allow a fast client initialization.

- https://github.com/serby/save /js
  - A simple CRUD based persistence abstraction for storing objects to any backend data store. eg. Memory, MongoDB, Redis, CouchDB, Postgres, Punch Card etc.

- https://github.com/pouchdb-community/relational-pouch /202211/ts
  - a plugin for PouchDB that allows you to interact with PouchDB/CouchDB like a relational data store, with types and relations.
  - The main goal of this is to provide an API that is as similar to Ember Data and jsonapi as possible, while still being performant and Pouch-like.
- https://github.com/Agrejus/pouchdb-entity-fabric /202209/ts
  - PouchDB ORM modeled after .net's Entity Framework
- https://github.com/iyobo/pouchorm /202205/ts
  - The definitive ORM for working with PouchDB.
  - Introduces the concept of Collections to pouchdb
  - Supports web, electron, react-native, and anything else
- https://github.com/compactd/slothdb /201808/ts
  - A typescript ORM that uses annotation and classes to describe the database
- https://github.com/ldavidsp/pouchdb-sql /js
  - plugin that allows SQL queries to be performed against PouchDB databases
  - It requires the pouchdb-find plugin.

- https://github.com/marten-de-vries/pouchdb-seamless-auth /201706/js
  - Seamless switching between online (CouchDB) and offline (PouchDB) authentication.
  - This plug-in stores password hashes in a local PouchDB, not a smart thing
- https://github.com/pouchdb-community/pouchdb-authentication
  - User authentication plugin for PouchDB and CouchDB.
- https://github.com/dscsa/pouch /js
  - Library to add validation and syncing to PouchDB

- https://github.com/pouchdb-community/pouchdb-quick-search /370Star/apache2/201702/js/lunr/inactive
  - efficient and accurate full-text search engine built on top of PouchDB
  - The underlying tokenization/stemming/stopword engine is Lunr, which is optimized for English text, using a variant of the Porter stemmer. 
  - This is a local plugin, so it is not designed to work against CouchDB/Cloudant/etc. 
  - If you'd like to search against the server, use the CouchDB Lucene plugin, Cloudant's search indexes, or something similar.

- https://github.com/onyxcodes/dbmanager-ui /202208/ts
  - UI for managing PouchDB databases through DBManager interface layer

- https://github.com/puncoz-official/redux-pouchdb-middleware /202001/ts
  - redux middleware to sync data between redux with pouchdb and vice-versa.
- https://github.com/vicentedealencar/redux-pouchdb /201912/js
  - sync store state to pouchdb
  - The PouchDB database persists the state of chosen parts of the Redux store every time it changes.
- https://github.com/medihack/redux-pouchdb-plus /201806/js
  - Synchronize Redux store with PouchDB to have a persistent store.
- https://github.com/alexcorvi/PouchX /mobx
  - Seamless synchronization between PouchDB and MobX

- https://github.com/Terreii/use-pouchdb /apache2/202304/ts
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

- https://github.com/pouchdb/geopouch /201703/js
  - Spatial plugin from PouchDB extracted and supporting N dimensional coordinates.
  - https://github.com/couchbase/geocouch /erlang

- https://github.com/hermanho/react-leaflet-pouchdb-tilelayer /202309/ts
  - React version of Leaflet. TileLayer. PouchDBCached
- https://github.com/MazeMap/Leaflet.TileLayer.PouchDBCached /202203/js
  - A Leaflet tile layer which caches into PouchDB for offline use

- https://github.com/cdaringe/pouchy /202107/ts
  - Pouchy wraps & extends PouchDB and provides various sorely needed sugar methods.
  - most methods provided are very simple PouchDB-native method modifiers, but are targeted to save you frequent boilerplate re-typing!

- https://github.com/Zardoz89/filestore-pouchdb /js
  - Handles a simple file storage over PouchDB. Mimics some functionality of a virtual file system like directories and file hierarchy, but avoids to try to be a full virtual file system.

- https://github.com/garbados/comdb /202205/js
  - A PouchDB plugin that transparently encrypts and decrypts its data
- https://github.com/calvinmetcalf/crypto-pouch /202110/js
  - plugin for encrypted pouchdb/couchdb databases
  - This only encrypts the contents of documents, not the `_id` or `_rev`, nor view keys and values
  - encrypts documents using TweetNaCl.js, an audited encryption library. It uses the xsalsa20-poly1305 algorithm.
- https://github.com/jo/pouch-box /201505/js
  - Asymmetric encrypted PouchDB, powered by NaCl's curve25519-xsalsa20-poly1305.
  - uses TweetNaCl.js, a port of TweetNaCl / NaCl to JavaScript for modern browsers and Node.js by Dmitry Chestnykh

- https://github.com/pouchdb-community/worker-pouch /201802/js
  - Adapter plugin to use PouchDB over Web Workers and Service Workers. 
  - Transparently proxies all PouchDB API requests to the worker, so that the most expensive database operations are run in a separate thread.

- https://github.com/pouchdb-community/pouchdb-full-sync /201607/js
  - Fully replicate two PouchDB or CouchDB databases, while preserving absolutely all document history and conflicts.
  - Useful for: Implementing infinite undo/redo in your app
  - Normally, the CouchDB replication protocol only replicates the leafs between two databases. 
    - This preserves conflicts (which is awesome!), but it discards non-leafs for performance reasons.
  - Notice that all the revisions are kept, even the non-leafs. 

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

- https://github.com/sudzy-group/pouchable /ts
  - PouchDB simplified by TypeScript Decorators

- https://github.com/thaibault/couchdb-web-node-plugin
  - PouchDB with model specification/checking, user authentication and right management as web-node plugin.
  - A database server, model instance conflict handler, rest api, authentication, session management, schema validator and model relation guarantee for webNode.

- https://github.com/balazsgrill/tw-pouchdb-sync /js
  - TiddlyWiki synchronizer plugin for CouchDB/PouchDB

- https://github.com/thaibault/couchdb-web-node-plugin /ts
  - A couchdb server, model instance conflict handler, rest api, authentication, session management, schema validator and model relation guarantee for webNode.
  - PouchDB with model specification/checking, user authentication and right management as web-node plugin.
# couchdb-utils
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

- https://github.com/couchbase/couchbase-lite-core /202310/cpp/c
  - Cross-platform C++ core library for Couchbase Lite

- https://github.com/dianabarsan/couchdb-perf /js
  - CouchDb 2 vs CouchDb 3 superficial performance bench

- https://github.com/apache/couchdb-fauxton /js
  - the new Web UI for CouchDB

- https://github.com/antal0x11/express-couchdb /js
  - A simple CRUD application with ExpressJS and CouchDB.
- https://github.com/NinjaGrandpa/nodejs-couchdb-demo /js
  - A simple customer database built with CouchDB and NodeJs

- https://github.com/ermouth/covercouch /js
  - CoverCouch implements per-document r/w/d ACL for CouchDB. 
  - CoverCouch acts as proxy – original CouchDB REST API kept untouched, but all requests to Couch – r/w/d, _changes feed, _view, _update, _list or other fn call, replication – everything is filtered.

- https://github.com/glynnbird/couchmigrate
  - CouchDB command-line design document migration tool
  - https://github.com/glynnbird/couchimport
  - https://github.com/glynnbird/couchfirehose

- https://github.com/garrensmith/fortuna-rs /js/rust
  - A javascript view engine for CouchDB 4.x written in Rust using Google V8.
  - Install FoundationDB Install CouchDB dependancies Setup CouchDB
  - [Building a faster CouchDB View Server in Rust](https://www.garrensmith.com/building-a-faster-couchdb-view-server-in-rust/)

- https://github.com/felixge/node-couchdb /201906/js
  - A thin node.js idiom based module for CouchDB's REST API that tries to stay close to the metal.

- https://github.com/medic/couch2pg /202209/js
  - Library and app to replicate a CouchDB database to PostgreSQL
- https://github.com/sysadminmike/couch-to-postgres /201710/js
  - Node libary to stream CouchDB changes into PostgreSQL

- https://github.com/iriscouch/couchjs
  - a command-line Node.js program. 
  - It is 100% compatible with Apache CouchDB's built-in JavaScript system.

- https://github.com/jcrugzz/changes-stream
  - A fault tolerant changes stream with builtin retry HEAVILY inspired by follow.

- https://github.com/mehtaarn000/reactdrive /202211/js
  - File storage system built with Reactjs, Expressjs, Nodejs, and CouchDB.

- https://github.com/pgte/dribbledb /201112/js/inactive
  - MVCC database written in javascript
  - a browser local store capable of remote syncing.
  - It supports several storage strategies and remote pushing and pulling strategies.
  - It works with CouchDB-style APIs and a lot more to come.

- https://github.com/rnewson/couchdb-lucene /java
  - Enables full-text searching of CouchDB documents using Lucene

- https://github.com/MalekovAzat/CouchDbStressTesting /python/ts
  - CouchDb synchronization stress testing
# collab/sync
- resources
  - [(Alpha) PouchDB integration for Yjs](https://gist.github.com/samwillis/1465da23194d1ad480a5548458864077)
    - [Inline attachment Blob ignored during deterministic _rev generation resulting in _rev hash collision](https://github.com/pouchdb/pouchdb/issues/8257)

- https://github.com/jo/pouch-resolve-conflicts /201803/js
  - plugin to assist in PouchDB conflict resolving.

- https://github.com/garbados/pouchdb-hypercore /js
  - Synchronize PouchDB or CouchDB with P2P Hypercores
  - A PouchDB plugin that maps records in hypercores, a P2P append-only datastructure, to a PouchDB or CouchDB instance. 
  - The plugin allows you to follow changes in hypercores locally and remotely.

- https://github.com/garbados/pouchdb-cabal /js
  - Interact with Cabal using PouchDB
  - Comparable to cabal-core

- https://github.com/redgeoff/spiegel /202303/js
  - Scalable replication and change listening for CouchDB
- https://github.com/iriscouch/follow /201709/js
  - CouchDB changes and db updates notifier for NodeJS

- https://github.com/pouchdb-community/pouchdb-replication-stream /js
  - Replicate PouchDB/CouchDB databases with Node.js-style streams
  - you can replicate two databases by just attaching the streams together

- https://github.com/pouchdb/pouchbase /201604/js
  - Server that lets PouchDB applications sync with passwordless logins

- https://github.com/Mo0812/MKNote
  - a note web app, which uses Markdown to render your notes.
  - verything works totally offline, all the data is stored on your browser and on your machine - no fancy backend
  - Even if its offline you can sync your notes over multi instances by running your own CouchDB backend

- https://github.com/patgoddard/codeMate /2014/js
  - A code editor for online or offline use using the chromium or chrome browser. It uses AceEditor, Pouchdb and an optional remote couchdb.

- https://github.com/natevw/PeerPouch /js/inactive
  - A plugin for PouchDB which allows a remote PouchDB instance to be used locally. 
  - It transfers data over WebRTC, for simple lower-latency remote access and even particularly peer-to-peer replication!
# examples
- https://github.com/acailly/easy-pouchdb-server /202105/js
  - Deploy a PouchDB server easily
  - running pouchdb server is perfect for small hobby projects or proof of concepts.

- https://github.com/shellyln/kanban-board-app /202101/ts/redux/inactive
  - https://shellyln.github.io/knbn
  - Kanban style task management board app
  - 依赖redux、material-ui.v4、pouchdb-find、codemirror5、
  - Calendar view
  - Synchronize multiple device boards with **CouchDB** remote server
  - Write kanban in Markdown syntax

- https://github.com/mradultiw/Wassup /202105/js
  - a client-server based desktop chat application written in Javascript
  - It has a central server and database which is used to connect clients together. 
  - Each client has it's own local database. 

- https://github.com/roldaojr/ra-data-pouchdb /LGPLv3/202204/js/inactive
  - PouchDB/CouchDB data provider for [react-admin](https://github.com/marmelab/react-admin)
  - This data provider takes a PouchDB object as input, then creates a client-side data provider around it.
  - Requires PouchDB-find plugin.
  - working: pagination, sorting(requires secondary indexes)
  - not working： filtering by column，full text search

- https://github.com/starikan/pouchdb-viewer /202104/js
  - Standalone PouchDB viewer powered by Electron and pouchdb-server

- https://github.com/thomastoye/field-journal /ts/pouchdb
  - https://field-journal.pages.dev/
  - An experimental browser-based, offline-first, event-sourced dispatching, messaging, and incident tracking application.

- https://github.com/kbrisso/file-base /202210/js/ts
  - Filebase is a database for your files and directories.
  - You can tag, add notes, organize, categorize, filter, search and quickly find your needed files with an easy-to-use application
  - Filebase does not modify your existing files or directories 

- https://github.com/GustavoLopez04/pouchdb
  - getting started tutorial for PouchDB
  - The newest push has code to replicate the PouchDB database to CouchDB and UI testing with WDIO.

- https://github.com/terichadbourne/offline-first-project-manager /js
  - Offline First project management tool, built as a Progressive Web App with PouchDB, CouchDB, and service workers

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
  - This repo is intended to service apps that use PouchDB to store their data locally—web apps or mobile apps or wherever PouchDB is supported.
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
  - https://moneytracker.cc/
  - an open-source progressive web app that allows you to track your income and expenses.
  - Data is stored locally on device in PouchDB database and can be synced to the cloud.
- https://github.com/medic/cht-core
  - The CHT Core Framework makes it faster to build responsive, offline-first digital health apps that equip health workers to provide better care in their communities.

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

- https://github.com/cloudless-hq/atreyu /js/svelte
  - https://atreyu.dev/docs/
  - an edge- and serviceworker first metaframework for personal, data centric web applications. 
  - It supports real time data sync, offline usage and values minimal boilerplate with opt in to most features.
  - Falcor is used for state management, caching, batching and data sharing. 
  - Svelte views are bound to a virtual data object with a js proxy based store implementation

- https://github.com/NoteSelf/NoteSelf.github.io /202005/js/inactive
  - https://noteself.org/
  - built on top of TiddlyWiki, a powerful, free, highly customizable and open-source personal wiki.
  - We took the best of it, it's powerful customization system, and mixed it with one of the best embedded databases available, PouchDb, to bring in the synchronization capabilities you need.

- https://github.com/steve-1820/memex /ts/inactive
  - This a POC on how a memex could potentially work.
  - [Show HN: Open-Source Memex – Alternative Approach to Roam/Obsidian | Hacker News](https://news.ycombinator.com/item?id=24572449)
    - This blog is a summary of a fun 1 month adventure I had with Knowledge Management Systems and building a POC
# more
- https://github.com/KouchDB/replication-source-poc /202211/java
  - Demonstrates how to stand-up a Java Springboot service as a source for CouchDB replication
  - CouchDB mock replication source Proof Of Concept.

- https://github.com/oknosoft/metadata.js
  - Library for building offline-first browser-based applications 
  - To manage data on the browser side, Pouchdb and AlaSQL are used
  - Couchdb was chosen as the main server data storage
  - Supported the ability to connect data adapters to 1C and other ORM, SQL and NoSQL servers
  - For developers of mobile and browser applications who are cramped(受限制) within the 1C platform
