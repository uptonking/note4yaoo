---
title: toc-lib-fwk-baas
tags: [baas, firebase, framework, toc]
created: 2021-05-25T09:40:21.484Z
modified: 2021-05-25T09:40:55.797Z
---

# toc-lib-fwk-baas

# guide

- 比较了parse、firebase、couchdb、kuzzle、remoteStorage、Hoodie
  - [How does Kinto compare to other solutions?](https://docs.kinto-storage.org/en/stable/faq.html)
# firebase-like
- supabase /68.1kStar/apache2/202406/ts
  - https://github.com/supabase/supabase
  - https://supabase.com/
  - an open source Firebase alternative.
  - Hosted Postgres Database
    - `PostgREST` is a web server that turns your PostgreSQL database directly into a RESTful API
  - Realtime subscriptions
    - Realtime is an `Elixir` server that allows you to listen to PostgreSQL inserts, updates, and deletes using websockets. 
    - broadcasts the JSON over websockets to authorized clients.
  - Authentication and authorization
    - GoTrue is a JWT based API for managing users and issuing JWT tokens.
  - Auto-generated APIs: rest, graphql
  - File Storage
    - Storage provides a RESTful interface for managing Files stored in S3, using Postgres to manage permissions.
  - AI + Vector/Embeddings Toolkit
  - Dashboard

- https://github.com/niledatabase/niledatabase /972Star/NonOpen/202508/ts
  - https://thenile.dev/
  - Nile is a Postgres platform that decouples storage from compute, virtualizes tenants, and supports vertical and horizontal scaling globally to ship B2B applications fast while being safe with limitless scale
  - [Are there any plans on Open Sourcing Database? · Issue #395 · niledatabase/niledatabase](https://github.com/niledatabase/niledatabase/issues/395)
    - I just want to know if the Database is closed source and only offers cloud subscription or will it open source at some point in future?
    - Yes, we definitely have plans to open source

- parse-server /20.5kStar/apache2/202401/js
  - https://github.com/parse-community/parse-server
  - https://parseplatform.org/
  - https://docs.parseplatform.org/parse-server/guide/
  - https://github.com/parse-community/parse-server/wiki
  - Parse Server is an open source backend that can be deployed to any infrastructure that can run Node.js. 
  - 依赖express、graphql、mongodb、pg-promise、redis
  - Parse Server works with the Express web application framework. It can be added to existing web applications, or run by itself.
  - In addition to the traditional REST API, Parse Server automatically generates a GraphQL API based on your current application schema. 
  - Parse Server uses MongoDB or PostgreSQL as a database.
    - 🍃 The preferred database is MongoDB but Postgres is a great option if you’re starting a new project and you expect to have a stable Schema.
    - When using MongoDB with your Parse app, you need to manage your indexes yourself. You will also need to size up your database as your data grows.
    - In order to allow for better scaling of your data layer, it is possible to direct queries to a MongoDB secondary for read operations.
    - 🐘 When using Postgres with your Parse app, you need to manage your indexes yourself.

- appwrite /27.4kStar/BSD/202211/ts/php
  - https://github.com/appwrite/appwrite
  - https://appwrite.io/
  - Appwrite is an end-to-end backend server for Web, Mobile, Native, or Backend apps packaged as a set of Docker microservices. 

- https://github.com/javascriptdb/jsdb-server /SSPL/202211/js/inactive
  - https://javascriptdb.com/
  - The open source firebase alternative that uses SQLite.
  - Arrays and Objects operations read and write into your database. Magic.
  - JSDB is very much a work in progress, expect things to fail here and there, up and down.
    - When you use .filter to search over an array, we are not using indexes. 
  - https://github.com/javascriptdb/jsdb-sdk
  - https://github.com/javascriptdb/jsdb-react

- https://github.com/eugeneware/firedup /201306/js/inactive
  - A node.js implementation of firebase based on leveldb/levelup.

- kuzzle /1.3kStar/apache2/202312/js
  - https://github.com/kuzzleio/kuzzle
  - https://kuzzle.io/
  - Kuzzle is a generic backend offering the basic building blocks common to every application.
  - API First: use a standardised multi-protocol API.
  - Realtime Notifications: use the pub/sub system or subscribe to database notifications.
  - User Management: login, logout and security rules are no more a burden.

- https://github.com/asheghi/NeoBase /202209/ts/inactive
  - The open source Firebase alternative
  - NeoBase is a hosted platform. You can sign up and start using NeoBase without installing anything. You can also self-host and develop locally.
  - 依赖 express、mongoose、vue

- https://github.com/asheghi/waterbase /202104/js
  - an attempt to create an alternative for CloudFlare realtime database, Cloud FireStore
  - add `Subscription` to Keystone.js CMS GraphQL api

- https://github.com/TheHadiAhmadi/minibase /202211/js
  - minimal (and slow) firebase alternative

- https://github.com/soketi/soketi /4.4kStar/AGPL3/202402/ts
  - https://soketi.app/
  - Next-gen, Pusher-compatible, open-source WebSockets server
  - built on top of uWebSockets.js - a C application ported to Node.js
  - soketi implements the Pusher Protocol v7. Therefore, any Pusher-maintained or compatible client can connect to it
  - Soketi is capable to hold thousands of active connections with high traffic on less than 1 GB and 1 CPU in the cloud

- https://github.com/endpointservices/mps3 /ts
  - Infraless Database over any s3 storage API.
  - [mps3 - Offline-first DB over S3-compatible storage](https://observablehq.com/@tomlarkworthy/mps3-vendor-examples)
  - https://twitter.com/tomlarkworthy/status/1688132733246033920
    - I've been noodling with the concept of a vendorless BaaS by using an s3-compatible API as the backend. 
    - By hacking object versioning you get serialisability and atomic bulk updates. 
    - Its a real DB! Here it's using a local minio instance. Might try backblaze next.
    - Oh I have to expose the ETag header in the CORS config thats improved things to 400ms sometimes but I still have too many preflight requests
    - The sync protocol was designed using object versioning so that the logical names intuitively map to storage names, but then I realised R2, my favourite s3-like doesn't do versions. So now I had to redo it with timestamped suffixes. Total redesign with tricky clock skew defenses

- CoCreateJS /19Star/MIT/202212/js
  - https://github.com/CoCreate-app/CoCreateJS
  - https://cocreate.app/
  - A collaborative low code headless CMS and Javascript framework for building collaborative no code platforms, apps and UI
  - https://github.com/CoCreate-app/CoCreate-crud-client /202212/js
  - An useful CRUD api operate Create, read, update, delete with built in database. 
  - Can be used as a firebase alternative
 - https://github.com/CoCreate-app/CoCreateWS
    - Server Side for CoCreateJS. Containing websocket, crud, auth, server side rendering, and permission components.
  - https://github.com/CoCreate-app/CoCreate-admin
    - A No Code Admin, CRM, CMS, Website Builder platform. 
    - Powered by CoCreateJS to provide Realtime and Collaborative CRUD functionality.

- kinto /4.2kStar/apache2/202210/python
  - https://github.com/Kinto/kinto
  - http://docs.kinto-storage.org/
  - A generic JSON document store with sharing and synchronisation capabilities.
  - Backends: In-memory (development), PostgreSQL 9.5+ (production)
  - [Kinto by Mozilla – An open-source Parse alternative | Hacker News_201601](https://news.ycombinator.com/item?id=10994736)

- https://github.com/pocketbase/pocketbase /MIT/202312/go/svelte
  - https://pocketbase.io/
  - PocketBase is an open source Go backend
  - embedded database (SQLite) with realtime subscriptions
  - built-in files and users management
  - convenient Admin dashboard UI
  - [Show HN: PocketBase – Open Source realtime backend in one file | Hacker News _202207](https://news.ycombinator.com/item?id=32013330)
    - Have you thought about adding Operational Transform or CRDT primitives to your offering?
    - Currently any additional data transformation is left to the developers to extend via event hooks or custom client side handling.
    - I've worked with CRDT in the past (yjs), but it may not be very useful in PocketBase considering that the application was designed to run on a single server and db writes are practically queued (you can have only one sqlite writer at a time)

- https://github.com/easycrud/easycrud
  - https://easycrud.org/
  - This project is aimed at providing a series of handy packages for the development of a typical CRUD web application.
  - The packages are work around a kind of schema written in JSON for database table.

- https://github.com/InsForge/InsForge /610Star/apache2/202510/ts
  - https://insforge.dev/
  - the Agent-Native Supabase Alternative. 
  - We are building the features of Supabase in an AI-native way, enabling AI agents to build and manage full-stack applications autonomously.
  - [I built a backend that agents can understand and control through MCP : r/CLine _202510](https://www.reddit.com/r/CLine/comments/1nz29qb/i_built_a_backend_that_agents_can_understand_and/)
    - The coding agent didn’t really understand my backend. It didn’t know my database schema, which functions existed, or how different parts were wired together. To avoid hallucinations, I had to keep repeating the same context manually. 
    - That’s why I built InsForge, a backend as a service designed for AI coding. It follows many of the same architectural ideas as Supabase, but is customized for agent driven workflows. Through MCP, agents get structured backend context and can interact with real backend tools directly.
# baas/backend-as-a-service
- https://github.com/lagonapp/lagon /rust/ts
  - Lagon is an open-source runtime and platform that allows developers to run TypeScript and JavaScript Serverless Functions close to users.
  - I've been building this fully open-source edge runtime and platform as an alternative to CF Workers & Deno Deploy for the past 10 months
# python-framework
- https://github.com/jam-py/jam-py /BSD/python/js
  - https://jam-py.com/
  - Jam.py is an object oriented, event driven framework with hierarchical structure, modular design and very tight DB/GUI coupling. 
  - The server side of Jam.py is written in Python, 
  - the client utilizes JavaScript, jQuery and Bootstrap.
  - 依赖werkzeug、sqlalchemy
  - https://jampyapplicationbuilder.com/
    - https://jampyapp.pythonanywhere.com/
    - https://northwind.pythonanywhere.com/
# scaling
- tips
  - feathears提供了 [框架级scaling方案](https://feathersjs.com/cookbook/general/scaling)
  - scaling参考: hocuspocus, strapi, dify

- https://github.com/piyush-repo/scaling-nodejs-services-loadbalancing /apache2/202204/js/inactive
  - [Scaling a Node JS Application](https://dzone.com/articles/scaling-a-node-js-application)
  - In this blog, we will mainly focus on horizontal scaling and we will build up a small Node JS application, and then we will scale it horizontally.

- https://github.com/vbarzokas/scalable-rest-api-boilerplate /MIT/202210/js/inactive
  - A sample system demonstrating a highly scalable and fault tolerant application that implements a REST API for product ordering, by leveraging node.js, mongoDB replica sets and `nginx` as a load balancer, wrapped with docker-compose.

- https://github.com/Maximization/scaling-nodejs-with-docker /MIT/202509/js/inactive
  - Sample Node.js project showing how to scale horizontally with Docker
  - [From PM2 to Docker: Cluster Mode - Maxim Orlov](https://maximorlov.com/from-pm2-to-docker-cluster-mode/)

- https://github.com/bytesleo/nodetomic /202108/MIT/js/inactive
  - https://bytesleo.github.io/nodetomic/
  - Minimalist boilerplate for nodejs, designed for vertical and horizontal scalability.
  - 依赖mongo、socket、redis
  - Add Redis to shared state
  - Added multiple servers and pm2 load balancing
  - Added database and load balancer
  - Added redis cluster and mongodb sharded clusters
  - https://github.com/bytesleo/nodetomic-api-swagger /MIT/202005/js/legacy

- https://github.com/Nehonix-Team/XyPriss /MIT/202510/ts
  - https://docs.xypriss.nehonix.space/
  - powerful, TypeScript-first, open-source Node.js web framework that enhances your development experience with built-in security middleware, clustering, and performance optimizations.
  - Built-in Security: Includes 12+ security middleware modules for common protections like CSRF, XSS, and rate limiting.
  - File Upload Support: Seamless integration with multer and other multipart form-data parsers.
  - Multi-Server Mode: Run multiple server instances with different configurations from a single setup.
  - Flexible Routing: Supports parameters, wildcards, and modular routers.
  - Works Great With Express: XyPriss is designed to complement the Node.js ecosystem, not replace it
  - XyPriss is the successor to FortifyJS, which will be deprecated
  - [Multi-Server - XyPriss Documentation](https://docs.xypriss.nehonix.space/multi-server.html)
    - XyPriss supports running multiple server instances with different configurations, ports, and route scopes. 

- https://github.com/TanishValesha/Scalable-Realtime-Multiplayer-System /202509/ts
  - A cloud-native, horizontally scalable real-time multiplayer WebSocket server implementation built with Node.js, TypeScript, Redis Pub/Sub, and Redis Queues. 
  - It supports room-based matchmaking, low-latency state synchronization, and dynamic scaling via Kubernetes’ Horizontal Pod Autoscaler (HPA). 
  - Deployed on AWS EKS with an AWS Load Balancer, Redis (for Pub/Sub and task queues), and Docker.
  - Real-time, bidirectional multiplayer communication
  - Room/Matchmaking support with fast state sync
  - Horizontally scalable with HPA on Kubernetes
  - Redis Pub/Sub for event distribution
  - Redis Queues for matchmaking task
  - Dockerized for easy CI/CD and portability
  - Cloud-native deployment using Kubernetes
- https://github.com/omkargade04/Scalable-Websocket-Server /MIT/202411/ts/与上面的repo架构图相同
  - A Scalable WebSocket server implementation using Redis Pub/Sub for message distribution across multiple server instances. 
  - This architecture allows for horizontal scaling via kubernetes' horizontal pod auto-scaler while maintaining real-time message delivery across all connected clients.

- https://github.com/The-ForgeBase/forgebase-ts /MIT/202505/ts/vue/inactive
  - A flexible, scalable Backend as a Service (BaaS) framework that works with multiple backend frameworks. 
  - Built to overcome the limitations of existing BaaS solutions with support for horizontal scaling and robust database integrations.
  - Our mission is to simplify backend development by providing a highly flexible, language-agnostic BaaS framework that developers can plug into their existing server setup.
  - While we are 70% inspired by Pocketbase, we recognized its limitations—particularly its dependency on SQLite and its inability to scale horizontally.

- https://github.com/civilcoder55/scalable-nest-websockets /MIT/202501/ts/inactive
  - A demonstration project showcasing a scalable Socket. IO implementation using NestJS. 
  - This project implements a horizontally scalable WebSocket server architecture that can handle real-time communications across multiple server instances.
  - Socket. IO Server: NestJS-based WebSocket server with adapter for horizontal scaling
  - Adapters: Used for Socket. IO pub/sub between multiple server instances. eg. Redis
  - Message Brokers: for handling event distribution. eg. RabbitMQ
  - Microservice architecture using NestJS

- https://github.com/mutasim77/fast-redis-chat /MIT/202408/ts/inactive
  - calable real-time chat app with WebSockets and Redis, featuring horizontal scaling and live connection tracking.
  - Live user connection count across multiple instances using Redis Pub/Sub
  - Horizontally scalable architecture with multiple backend instances
  - Load balancing with Caddy as a reverse proxy

- https://github.com/rajneesh069/scaling-in-node.js /202409/ts/偏理论/inactive
  - This repo is about Vertical and Horizontal scaling. It contains information about ASGs(Auto Scaling Groups)
  - Comparison: Single-threaded Async vs Cluster-based Multi-Processing

- https://github.com/francescocartelli/wss-for-horizontal-scaling-back-end /
202509/js
  - [Developing WebSocket for Horizontal Scaling: Using Redis as Message Queue _202405](https://blog.stackademic.com/developing-websocket-for-horizontal-scaling-using-redis-as-message-queue-a97cabd769d7)

- https://github.com/Wittline/RESTful-APIs-Nodejs /MIT/202010/js/inactive
  - https://wittline.github.io/RESTful-APIs-Nodejs/
  - Building RESTful API REST services with Node.js, Express.js and Mongoose.js
  - Scalable The existing code is non-blocking code, because of this, it can be easily scaled, if there is an APIs that are more in demand than others, it could be separated in another server or container, this allows copying the code quickly because each api is related to a set of separate modules

## utils-scaling

- https://github.com/aldrinjenson/node-balancer /202208/ts/inactive
  - Load balancer system for horizontal scaling implemented in Node. Js
  - The system consists of one master server and a template slave server
  - As shown in the demo, you can run as many instances of slave servers as needed. This can be run in multiple computers/nodes.
  - The system will poll the slave server at regular intervals to check if they are alive

- https://github.com/faranalytics/socketnaut /MIT/202501/ts/inactive
  - Socketnaut makes scaling native Node.js servers easy. 
  - A Socketnaut Service typically consists of a TCP proxy and a pool of HTTP servers.
  - Socketnaut will uniformly distribute incoming TCP sockets across the pool of allocated servers. This strategy allows for both distribution and parallel processing of incoming requests.
  - Socketnaut can be used in order to scale the main module of web applications built on performant Node.js web frameworks (e.g., Fastify, Koa, Express).
  - Socketnaut requires 0 out-of-org dependencies. Socketnaut's dependencies are published and maintained by the FAR Analytics & Research org
  - The Socketnaut ServiceProxy and ServiceAgent constructors consume native Node net. Server, http. Server, https. Server, and tls. Server instances; you can configure them however you choose.

## utils-socket

- https://github.com/socketio/socket.io-redis-adapter /MIT/202403/ts/inactive
  - https://socket.io/docs/v4/redis-adapter/
  - Adapter to enable broadcasting of events to multiple separate socket.io server nodes.
  - 🍴 forks
  - https://github.com/arunp0/socket.io-multi-redis
    - Horizontally scale up servers with multiple redis server.

- https://github.com/gsllucas/scaling-sockets-rabbitmq /202404/ts/inactive
  - This a proof of concept to scaling websockets application with messaging broker.
  - ws-service: service that has a messaging broker consumer that listens to a queue to send a custom socket event according to necessity
  - ws-client: service that has a socket client to listen to socket events emitted by ws-service throught the socket channel
  - broker-publisher: service that is emitting events through a messaging broker publisher
  - Any another service can connect to ws-service through messaging HOST URL to send real time messages in socket as broker publisher (rabbitMQ chosen here).

- https://github.com/veliovgroup/josk /BSD/202404/js/inactive
  - "JoSk" is a Node.js task manager for horizontally scaled apps and apps that would need to scale horizontally quickly at some point of growth.
  - "JoSk" mimics the native API of setTimeout and setInterval and supports CRON expressions. 
  - All queued tasks are synced between all running application instances via Redis, MongoDB, or a custom adapter.
  - The "JoSk" package is made for a variety of horizontally scaled apps, such as clusters, multi-servers, and multi-threaded Node.js instances, that are running either on the same or different machines or even different data centers. ✨ JoSk ensures that the only single execution of each task occurs across all running instances of the application.
  - "JoSk" is not just for multi-instance apps. It seamlessly integrates with single-instance applications as well, showcasing its versatility and adaptability.
  - Note: JoSk is the server-only package.

- https://github.com/kesimo/groWs /MIT/202402/go/inactive
  - Framework for building Structured and scalable Websocket Servers
  - It is built on top of the gobwas/ws library, that provides a performant API for working with Websocket connections.
  - The Idea behind groWs is to provide a simple and easy to use API for building Websocket Servers, that are Structured, Horizontally Scalable by default, and Maintainable.
  - Multi-Router support, that allows you to create multiple routers for different purposes.
  - Rooms support, that allows you to group connections into rooms, and broadcast messages to them.
  - Redis Pub-Sub support, that allows you to broadcast messages to multiple servers.

- https://github.com/bytesleo/redis-jwt /MIT/201709/js/inactive
  - Management of sessions by Redis and JWT for horizontal scalability, with the possibility of having one session at a time or multiple for the same user
# ha/high-availability
- https://github.com/dashersw/cote /MIT/202406/js
  - http://cote.js.org/
  - A Node.js library for building zero-configuration microservices.
  - cote lets you write zero-configuration microservices in Node.js without nginx, haproxy, redis, rabbitmq or anything else. 
  - Zero-configuration: No IP addresses, no ports, no routing to configure
  - Decentralized: No fixed parts, no "manager" nodes, no single point of failure
  - Scalable: Horizontally scale to any number of machines
  - Typically, in a microservices system, the application is broken into smaller chunks that communicate with each other.
  - It replaces queue protocols and service registry software by clever use of IP broadcast/IP multicast systems. cote needs an environment that allows the use of IP broadcast or multicast, in order to scale beyond a single machine. 

- https://github.com/ValentinBELYN/OnionHA /GPL/202009/python
  - a simple way to add high availability to a cluster.
  - Scalable: Onion HA can operate on a large number of nodes. Whether you have two nodes or ten nodes, Onion HA will work the same way.

- https://github.com/caprover/caprover /202406/ts
  - https://caprover.com/
  - CapRover is an extremely easy to use app/database deployment & web server manager for your NodeJS, Python, PHP, ASP. NET, Ruby, MySQL, MongoDB, Postgres, WordPress (and etc...) applications!
  - It's blazingly fast and very robust as it uses Docker, nginx, LetsEncrypt and NetData under the hood behind its simple-to-use interface
  - Docker Swarm under the hood for containerization and clustering
# more
- https://github.com/nils-simons/spackoDB /202206/js/starter
  - Firestore Alternative
