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

- ref
  - https://github.com/feathersjs/awesome-feathersjs
# popular
- https://github.com/feathersjs-ecosystem/feathers-permissions
  - Simple role and service method permissions for Feathers
  - [Access control strategies with FeathersJS](https://blog.feathersjs.com/access-control-strategies-with-feathersjs-72452268739d)

- https://github.com/humaans/figbird
  - realtime data management for React + Feathers applications.
  - In principle, you could use Figbird with any REST API as long as several conventions are followed or are mapped to.
  - In fact, Figbird does not have any code dependencies on Feathers. It's only the Feathers patterns and conventions that the library is designed for. 

- https://github.com/kalisio/feathers-distributed
  - Distribute your Feathers services as microservices
- https://github.com/mosaiqo/feathers-microservices
  - This is my humble opinionated approach to connect different microservices written in Feathers JS.

- https://github.com/feathersjs-ecosystem/feathers-sync
  - Synchronize service events between Feathers application instances
  - When running multiple instances of your Feathers application (e.g. on several Heroku Dynos), service events (created, updated, patched, removed and any custom defined events) do not get propagated to other instances.
  - feathers-sync uses a messaging mechanism to propagate all events to all application instances. 
  - It currently supports redis, amqp/RabbitMQ
# examples
- https://github.com/kalisio/krawler
  - A minimalist (geospatial) ETL
  - 依赖node-gdal, abstract-blob-store
  - 示例
    - csv2db
    - dem2csv
    - rest -> geojson -> local-file
  - krawler is powered by Feathers (opens new window)and rely on two of its main abstractions: services (opens new window)and hooks
# feathers-v4
- https://github.com/feathersjs-ecosystem/feathers-authentication-management
  - Adds sign up verification, forgotten password reset, and other capabilities to local feathers-authentication

- https://github.com/feathersjs-ecosystem/feathers-blob
  - Feathers service for blob storage, like S3.
  - https://github.com/kalisio/feathers-s3

- https://github.com/lwhiteley/feathers-lowdb
  - a database service adapter for Lowdb, a small JSON database for Node, Electron and the browser powered by Lodash.
# utils
- https://github.com/gobengo/activitypub-server
  - 依赖 activitystreams2
# auth
- https://www.npmjs.com/package/@admitad-x3/feathers-rbac
  - 几乎无依赖
# more
- https://github.com/AshotN/adminjs-feathers
  - Adapter for AdminJS to use FeathersJS services

- https://github.com/k-flynn-webdev/app-short-cal-api
  - Create a fancy calendar pages from iCal data
