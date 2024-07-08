---
title: lib-fwk-nodejs-feathers-docs
tags: [backend, docs, feathers]
created: 2023-01-20T00:12:14.506Z
modified: 2023-01-20T00:13:00.927Z
---

# lib-fwk-nodejs-feathers-docs

# guide

# blogs
- [Exposing a Feathers. JS HTTP API in Kubernetes using Ingress - DEV Community _201808](https://dev.to/andrejus/exposing-a-feathersjs-http-api-in-kubernetes-using-ingress-ai1)
# docs

## overview

- The Feathers application does not use a complicated dependency injection mechanism. 
  - Instead, the application is wired together using configure functions to split things up into individual files. 
  - They are functions that are exported from a file and that take the Feathers `app` object and then use it to e.g. register services. Those functions are then passed to `app.configure`.

## [Scaling | feathers](https://feathersjs.com/cookbook/general/scaling)

- feathers application may need to provide high availability. Feathers is designed to scale.
  - a feathers app that uses the feathers-rest adapter exclusively will require less scaling configuration because HTTP is a stateless protocol. 
  - If using websockets (a stateful protocol) through the feathers-socketio or feathers-primus adapters, configuration may be more complex to ensure websockets work properly.
- Scaling horizontally refers to either:
  - setting up a cluster, or
  - adding more machines to support your application

- Cluster support is built into core NodeJS. Since NodeJS is single threaded, clustering allows you to easily distribute application requests among multiple child processes (and multiple threads). Clustering is a good choice when running feathers in a multi-core environment.

- When running multiple instances of your Feathers application (e.g. on several Heroku Dynos), service events (created, updated, patched, removed and any custom defined events) do not get propagated to other instances for such cases you may want to use: https://github.com/feathersjs-ecosystem/feathers-sync
  - Which will use a messaging mechanism to propagate all events to all application instances like redis or RabbitMQ

- 
- 
- 

# more
