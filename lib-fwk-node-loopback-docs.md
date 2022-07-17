---
title: lib-fwk-node-loopback-docs
tags: [docs, loopback, node]
created: 2021-07-28T19:01:34.196Z
modified: 2021-07-28T19:02:15.922Z
---

# lib-fwk-node-loopback-docs

> LoopBack makes it easy to build modern API applications that require complex integrations.

# guide

# [Crafting LoopBack 4](https://loopback.io/doc/en/lb4/Crafting-LoopBack-4.html)
- LoopBack is an open-source Node.js framework built for API developers. 
  - Its primary goal is to help create APIs as microservices from existing services/databases and expose them as endpoints for client applications, such as web, mobile, and IoT.
- Up to version 3.x, LoopBack built on the popular Express framework
  - In retrospect, basing LoopBack on Express was the right decision
  - Standing on the shoulders of Express enabled LoopBack to focus on adding value for API creation experience without reinventing the wheel. 
  - LoopBack also has benefitted from the Express ecosystem, especially ready-to-use middleware modules from npm as well as valuable knowledge and support by the community.
- LoopBack uses Express routing and middleware as the plumbing to a request/response pipeline for API use cases, such as authentication, authorization, and routing. 
  - Beyond inbound HTTP processing, LoopBack provides integration facilities such as models, datasources, and connectors to allow API logic to interact with various backend systems, including but not limited to, databases, REST APIs, SOAP web services and gRPC microservices. 
  - The ability to glue inbound communication and outbound integration makes LoopBack a very powerful framework for API developers. 

- Why LoopBack 4?
- The code base becomes more complicated over time with more modules and more functionality. 
- Technical debt is accumulating, for example inconsistent designs across modules and feature flags for different behaviors.
- It is becoming more difficult to add new features or fix bugs as some areas start to reach the limit of the current design.
- It’s not easy to extend the framework without requesting the core team to make code changes in LoopBack modules. 

- LoopBack 4’s goals are:
- Catch up with latest and greatest technology advances.
  - es2016, typescript, openapi, graphql
- Promote extensibility to grow the ecosystem.
- Align with cloud native experience for microservices.
- Remove the complexity and inconsistency across modules.
- Separate concerns for better composability.

- Design principles
  - Imperative first, declarative later
  - Build minimum features and add more later if necessary
  - Developer experience first

- LoopBack had always been built on Express so we can leverage the vast community and middleware in the Express ecosystem 
  - BUT it presented some challenges for LoopBack. 
  - **With LoopBack 4 we considered moving away from Express (and even built the framework without Express) but eventually circled back to Express** because of its vast ecosystem.
- Some of the gaps between what Express offers and LoopBack’s needs are:
  - Lack of extensibility
    - Express is only extensible via middleware. 
    - It neither exposes a registry nor provides APIs to manage artifacts such as middleware or routers.
  - Lack of composability
    - Express is not composable. 
    - For example, `app.use()` is the only way to register a middleware. 
    - The order of middleware is determined by the order of `app.use`.
  - Lack of declarative support
    - In Express, everything is done by JavaScript 
    - In contrast, LoopBack is designed to facilitate API creation and composition by conventions and patterns as best practices.

- Circling back to Express with a twist(弯曲；转折)
  - The main purpose of LoopBack is to make API creation easy, interacting with databases, services, etc., not middleware for CORS, static file serving, etc.
  - We didn’t want to reinvent the wheel by writing new middleware for LoopBack 4.
- The team explored leveraging Express or Koa (but only for their middleware support). 
  - The final decision was to use Express in a way that bridges the gap by addressing the gaps identified above as follows
  - LoopBack provides its own Controller/OpenAPI metadata optimized routing engine
  - Express is used exclusively for allowing us to consume Express middleware (CORS, Static File Serving)
  - LoopBack uses a Sequence of Actions to craft the response in a composable manner and leverages `@loopback/context` as a registry.

- Deep dive into LoopBack 4 extensibility
  - Context, the IoC container to manage services
  - Dependency injection to facilitate composition
  - Decorators to supply metadata using annotations
  - Components as the packaging model to bundle extensions
