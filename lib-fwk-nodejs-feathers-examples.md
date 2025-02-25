---
title: lib-fwk-nodejs-feathers-examples
tags: [crud, examples, feathers, toc]
created: 2023-01-20T00:18:26.811Z
modified: 2023-01-20T00:18:44.282Z
---

# lib-fwk-nodejs-feathers-examples

# guide
- 后端常用场景
  - headless CMS, page builder, form builder, file manager, admin-area
  - admin/dashboard
  - forum/community
  - content内容或文档系统
  - lowcode integration
  - 流程自动化

- tips
  - 不必执着于框架与crdt集成的标准方案，crdt的数据层参考示例有很多，本身与框架无关

- ref
  - https://feathersjs.com/ecosystem/?sort=lastPublish
  - https://github.com/feathersjs/awesome-feathersjs
  - https://stackblitz.com/@daffl/collections/feathers-quick-start
# popular
- https://github.com/feathersjs/playground
  - A demo feathers-chat project for learning and demonstration purposes.
  - A real-time chat app and server

- https://github.com/feathersjs/feathers-chat
  - A Feathers real-time chat application
  - initialize an SQLite database in the feathers-chat.sqlite file.

- https://github.com/featherscloud/chat /MIT/202406/ts
  - https://featherscloud.github.io/chat
  - A local-first chat application with user login
  - A local-first chat application built with different frameworks.
  - Works offline
  - Does not need a server, Can be deployed like any static website
  - 依赖 @featherscloud/auth、@automerge/automerge-repo

- https://github.com/josx/ra-data-feathers /202202/js/inactive
  - Feathers data provider for react-admin. 
  - A feathers rest client for react-admin
  - https://github.com/kfern/feathers-aor-test-integration

- https://github.com/humaans/figbird /js
  - https://humaans.github.io/figbird/
  - realtime data management for React + Feathers applications.
  - In principle, you could use Figbird with any REST API as long as several conventions are followed or are mapped to.
  - In fact, Figbird does not have any code dependencies on Feathers. It's only the Feathers patterns and conventions that the library is designed for. 
- https://github.com/unesic/trello-clone /js
  - Popular kanban-style project management tool's clone.
  - 依赖figbird、styled-compo、mongoose

- https://github.com/jscomponent/casket /js
  - Casket Content Management System - Built on FeathersJS using MongoDB with Mongoose and Socket. IO

- https://github.com/lwhiteley/feathers-lowdb
  - a database service adapter for Lowdb, a small JSON database for Node, Electron and the browser powered by Lodash. 

- https://github.com/silvestreh/feathers-react
  - a handful of React Components to help you display data coming from your Feathers API in real-time
- https://github.com/indatawetrust/use-feathers
  - This package is based on feathers js client packages.
  - https://github.com/indatawetrust/use-feathers/tree/master/demo

- https://github.com/feathersjs-offline/localforage
  - A FeathersJS standard CRUD adapter wrapping localForage to simplify storage in IndexedDB, and LocalStorage.
  - https://github.com/feathersjs-offline/simple-example
    - An example client and server showcasing FeathersJS offline-first realtime support for own-data and own-net protocols as described in the docs here.
    - https://github.com/feathersjs-offline/owndata-ownnet /202112/js/inactive

- https://github.com/mosaiqo/feathers-microservices
  - This is my humble opinionated approach to connect different microservices written in Feathers JS.

- https://github.com/feathersjs-ecosystem/feathers-permissions
  - Simple role and service method permissions for Feathers
  - [Access control strategies with FeathersJS](https://blog.feathersjs.com/access-control-strategies-with-feathersjs-72452268739d)

- https://github.com/marshallswain/feathers-pinia
  - Connect your Feathers API to the elegant data store for Vue

- https://github.com/3CordGuy/listen-up /js
  - Listen Up is a very rudimentary webhook listening platform that will display your POST requests to generated endpoints in realtime.
  - This is meant to be useful for prototyping and developing webhooks.
  - feathers used on the back-end and front-end
  - Vue for some front-end (is currently rudimentary)
  - Atlas for hosting a simple hobby instance of MongoDB

- https://github.com/swina/feathersjs-webpush-notifications
  - [WebPush Notifications with Feathersjs_201902](https://swina.github.io/2019/02/webpush-notifications-with-feathersjs/)

- https://github.com/eddyystop/feathers-live-query /MIT/201610/js
  - Live query. Mirror part of a DB on the client.
  - The clients communicate with the server using socket.io websockets. 

- https://github.com/dmccuskey/feathers-gui /202306/ts/vue/v5不支持
  - https://feathersgui.dev/
  - A FireStore-like interface for Feathersjs servers
  - A record editor for Feathersjs-wrapped databases. 
  - It can be run locally or used online.
  - I've been using Feathersjs for several years and this is a tool I created to view and edit my data records during development.
  - All configuration info is stored locally in localStorage

- https://github.com/Nubuck/z1-core /202311/js
  - an incrementally adoptable modular software system aiming to automate the labor and complexity out of developing composable multi-platform projects.
  - The Z1 core packages augment the Feathers, React, Redux and Tailwind frameworks.
# api
- https://github.com/adaptable/feathers-template
  - Adaptable.io template for deploying an autoscaling, Serverless Feathers API. 
  - Can also be used to deploy other Node.js HTTP apps.

- https://github.com/KleitonBarone/feathersjs-crud-api
  - Simple Crud Api using FeatherJs Framework

- https://github.com/bervProject/FeathersJS-Boilerplate /MIT/202308/ts
  - FeathersJS Boilerplate for my own project
  - Upload into Google Cloud Storage

- https://github.com/feathersjs-ecosystem/feathers-nedb /js
  - a database service adapter for NeDB

- https://github.com/ivanob/rf-coding-challenge
  - A backend coding challenge using feathersjs, react, axios, mongoDB

- https://github.com/DuilioQuavanti/lends-backend /js
  - REST API that allows the connection of our application, in addition to saving data in mongodb using feathersjs
  - https://github.com/DuilioQuavanti/lends-app /js
    - Mobile application developed in react native, which allows the rental of different products
# examples
- https://github.com/jamesvillarrubia/feathers-openai /js
  - An open.ai adapter for FeathersJS
  - This library enables a series of FeathersJS services that map to the entities and routes of the OpenAI API.

- https://github.com/timothyhoover/supporty /ts
  - Simple ticket management system built with React, Feathers.js, and Tailwind

- https://github.com/anthonymunene/reservation-apps /202312/ts
  - A reservation airbnb clone API built with feathersjs knex ORM and PostgreSQL

- https://github.com/r1pk/surveo /js
  - https://surveo.vercel.app/
  - Responsive web application built with React, React-Router, Redux, Material-UI and Feathers that allows users to create online surveys with basic security features and analyse the results using different types of presentation

- https://github.com/kalisio/krawler /js
  - https://kalisio.github.io/krawler/
  - A minimalist (geospatial) ETL
  - 依赖node-gdal, abstract-blob-store
  - 示例
    - csv2db
    - dem2csv
    - rest -> geojson -> local-file
  - krawler is powered by Feathers and rely on two of its main abstractions: services (opens new window)and hooks

- https://github.com/shopping-busket/backend
  - FeathersJS backend for all the Busket clients. 
  - Made with FeathersJS and Sequelize SQL
  - https://github.com/shopping-busket/web
    - Busket web client made with Vue3.
  - https://github.com/shopping-busket/busket-android

- https://github.com/fratzinger/feathers-openweathermap
  - This is thin layer around the OpenWeatherMap API wrapped in a feathers.js service.

- https://github.com/lehao190/Dev-Blog-App-Backend-FeathersJS
  - https://github.com/lehao190/Dev-Blog-App-Frontend-Quasar
  - https://agitated-mclean-5f9de9.netlify.app/

- https://github.com/ShinChven/multiple-authentication-services-on-feathers-app
  - an example to show how to implement multiple authentication services on a FeathersJS app
# feathers-v4
- https://github.com/feathersjs-ecosystem/feathers-authentication-management
  - Adds sign up verification, forgotten password reset, and other capabilities to local feathers-authentication

- https://github.com/feathersjs-ecosystem/feathers-blob
  - Feathers service for blob storage, like S3.
  - https://github.com/kalisio/feathers-s3

- https://github.com/lwhiteley/feathers-lowdb
  - a database service adapter for Lowdb, a small JSON database for Node, Electron and the browser powered by Lodash.
# cluster/scaling
- https://github.com/kalisio/feathers-distributed /MIT/202407/js
  - Distribute your Feathers services as microservices
  - 依赖cote(微服务)
  - cote requires your cloud provider to support IP broadcast or multicast.
  - Please note that the underlying architecture has been changed from one requester/publisher and responder/subscriber per service to one requester/publisher and responder/subscriber per application between v0.7 and v1.x. 

- https://github.com/feathersjs-ecosystem/feathers-sync /MIT/202305/js/inactive
  - Synchronize service events between Feathers application instances
  - When running multiple instances of your Feathers application (e.g. on several Heroku Dynos), service events (created, updated, patched, removed and any custom defined events) do not get propagated to other instances.
  - feathers-sync uses a messaging mechanism to propagate all events to all application instances. 
  - It currently supports redis, amqp/RabbitMQ
  - This allows to scale real-time websocket connections to any number of clients.
  - With feathers-sync enabled all events are going to get propagated to every application instance. 
    - This means, that any event listeners registered on the server should not perform any actions that change the global state (e.g. write something into the database or call to an external API) because it will end up running multiple times (once on each instance). 
    - Instead, event listeners should only be used to update the local state (e.g. a local cache) and send real-time updates to all its clients.
  - [Scale server on kubernetes ](https://github.com/feathersjs-ecosystem/feathers-sync/issues/55)
    - With your setup I would force Socket.io to only use Websockets and not polling

- https://github.com/polst/feathers-socketcluster /MIT/201701/js
  - The Feathers SocketCluster real-time API provider
  - This provider exposes Feathers services through a SocketCluster real-time API. It is compatible with Feathers 2.x (1.x not tested).

- https://github.com/dekelev/feathers-http-distributed /MIT/202008/js
  - Distribute FeathersJS apps over the network with inter-service communication using HTTP protocol
  - https://github.com/feathersjs/feathers/issues/939
    - The feathers-http-distributed module was built as preparation for migrating all our FeathersJS services to Kubernetes, though it can be used for a broad range of use cases besides Kubernetes.

- https://github.com/codeanker/feathers-kubernetes /201808/js
  - this package can expose 2 endpoint that are good for the use of a kubernetes cluster. The healthz endpoint for kubernetes pod lifecycle. And the metrics endpoint a Prometheus endpoint to collect feathers service metrics.
# utils
- https://github.com/feathersjs-ecosystem/feathers-hooks-common
  - Useful hooks for use with FeathersJS services.
- https://github.com/bervProject/feathers-advance-hook
  - Feathers Advance Hook Extensible
- https://github.com/fratzinger/feathers-utils
  - utils for feathers.js

- https://github.com/feathersjs-ecosystem/dataloader
  - Reduce requests to backend services by batching calls and caching records.

- https://gitlab.com/lpgroup/lpgroup /MIT/202407/js
  - We are an organisation involved in several startups. This is our main monorepo for javascript npms:s that are used in some of our projects
  - 依赖feathers.v4

- https://github.com/mkalus/self-cleaning-blob-storage-example
  - [Create a Self-Cleaning Blob Storage using Express, FeathersJS, MongoDB, and Abstract Blob Storage | by Max Kalus | The Startup | Medium](https://medium.com/swlh/create-a-self-cleaning-blob-storage-using-express-feathersjs-mongodb-and-abstract-blob-storage-7840e4f78682)

- https://github.com/remedyred/feathers-plugins
  - Monorepo for FeathersJS tools and plugins

- https://github.com/lwhiteley/feathers-alive-ready
  - a plugin to add health check endpoints to a feathersjs application

- https://github.com/feathersjs-ecosystem/feathers-reactive
  - Reactive API extensions for Feathers services
  - adds a watch() method to services. The returned object implements all service methods as RxJS v6 observables that automatically update on real-time events.
  - 依赖rxjs、sift

- https://github.com/feathersjs-ecosystem/feathers-sequelize
  - A Feathers service adapter for the Sequelize ORM. 
  - Supporting MySQL, MariaDB, Postgres, SQLite, and SQL Server

- https://github.com/gobengo/activitypub-server
  - 依赖 activitystreams2

- https://github.com/litsdm/feather-fastify /202105/js/inactive
  - Feather BE re-made using fastify
  - [What's New in v5 | feathers](https://feathersjs.com/guides/whats-new)
    - Feathers just got a huge speed upgrade, now including its own Radix Trie router. This means that the algorithm behind Fastify's speed is now built into Feathers, and it works no matter which framework transport you use under the hood
- https://github.com/Sieabah/feathers-fastify /201806/js/archived
  - This plugin turns a Feathers v3+ application into a drop-in replacement for any Express application
# auth
- https://www.npmjs.com/package/@admitad-x3/feathers-rbac
  - 几乎无依赖
# ssr
- [Server Side Rendering | feathers](https://feathersjs.com/cookbook/express/view-engine.html)

- https://github.com/leob/feathers-next
  - This project shows how to integrate a Next.js application with a Feathers backend, including authentication (with user name/password) and Redux.
  - Contrary to feathers-next-example, I decided to keep the Feathers backend (the API) separated from the "server" (SSR) part of the Next.js frontend. This means that we're running two separate server (node.js) processes.
  - This might add a (tiny) bit of overhead, but ultimately it makes the app easier to develop and maintain (and configure) because we don't mingle Feathers API backend code with Next.js server rendering code.

- https://github.com/deniapps/nextfeathers
  - nextJS + feathersJS = Perfect Javascript Full-Stack!
# more
- https://github.com/AshotN/adminjs-feathers
  - Adapter for AdminJS to use FeathersJS services

- https://github.com/k-flynn-webdev/app-short-cal-api
  - Create a fancy calendar pages from iCal data

- https://github.com/Dahkenangnon/feathers-demos /202304/ts
  - demoz apis (v4 & v5) for the https://github.com/Dahkenangnon/flutter_feathersjs.dart package
