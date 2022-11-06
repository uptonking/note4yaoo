---
title: toc-lib-fwk-node-restful-http
tags: [ajax, framework, http, restful, toc]
created: 2020-12-13T09:14:01.137Z
modified: 2021-06-02T16:35:46.166Z
---

# toc-lib-fwk-node-restful-http

# guide

- mock-api
  - [fetch-mock vs json-server vs nock](https://www.npmtrends.com/fetch-mock-vs-json-server-vs-nock)
# rest-api
- https://github.com/restify/node-restify
  - 依赖mime、qs、http-signature、send(for streaming files)
  - restify is a framework, utilizing connect style middleware for building REST APIs.
  - There are actually three separate clients shipped in restify: JsonClient, StringClient, HttpClient
  - One of the coolest features of restify is that it automatically creates DTrace probes for you whenever you add a new route/handler.

- https://github.com/typicode/json-server
  - Get a full fake REST API with zero coding in less than 30 seconds (seriously)

- https://github.com/thiagobustamante/typescript-rest
  - annotation-based expressjs extension for typescript.
  - typescript-rest、typescript-ioc、typescript-rest-ioc

- https://github.com/developit/express-es6-rest-api
  - boilerplate for building REST APIs with ES6 and Express.

- https://github.com/albingroen/typescript-express-server
  - express server template with Typescript

- https://github.com/dalenguyen/rest-api-node-typescript
  - Building RESTful Web APIs with Node.js, Express, MongoDB and TypeScript
- https://github.com/nerdeveloper/hackathon-starter-kit
  - A Node-Typescript/Express Boilerplate with Authentication(Local, Github, Facebook, Twitter, Google, LinkedIn, Dropbox, Slack, Discord), Authorization, and CRUD functionality + PWA Support!

- https://github.com/aichbauer/express-rest-api-boilerplate
  - Express REST API with JWT Authentication and support for sqlite, mysql, and postgresql
  - routes mapping via express-routes-mapper
# rest-examples
- https://github.com/taniarascia/node-api-postgres
  - https://blog.logrocket.com/setting-up-a-restful-api-with-node-js-and-postgresql-d96d6fc892d8/
  - Create, read, update, delete in a Node.js app with an Express server and Postgres database.

- https://github.com/andregardi/jwt-express-typeorm
  - use TypeScript, Express.js and TypeORM to create an enterprise level Rest API with JWT authentication and role based authorization. 

- https://github.com/javieraviles/node-typescript-koa-rest
  - REST API boilerplate using NodeJS and KOA2, typescript. 
  - Logging and JWT as middlewares.

- https://github.com/w3tecch/express-typescript-boilerplate
  - RESTful API with NodeJs & TypeScript 
- https://github.com/contiamo/restful-react
  - declarative way of interacting with RESTful backends, featuring code-generation from Swagger and OpenAPI spec
- https://github.com/kunalkapadia/express-mongoose-es6-rest-api
  - A boilerplate application for building RESTful APIs Microservice in Node.js using express and mongoose
  - ES6 with code coverage and JsonWebToken Authentication

- https://github.com/Melzar/onion-architecture-boilerplate
  - a real life example of Onion Architecture with use of Node.js, Express and Typescript

- https://github.com/parse-community/parse-server
  - API server module for Node/Express
  - an open source backend that can be deployed to any infrastructure that can run Node.js.
- https://github.com/r-spacex/SpaceX-API
  - Open Source REST API for rocket, core, capsule, pad, and launch data
