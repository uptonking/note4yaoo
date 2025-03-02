---
title: web-fwk-dev-solutions-backend
tags: [backend, framework, nestjs, solutions, spring]
created: 2020-12-21T14:53:47.792Z
modified: 2023-01-12T10:24:24.591Z
---

# web-fwk-dev-solutions-backend

# guide

- ref
  - [most popular backend frameworks 时间变化条形图 基于d3实现](https://statisticsanddata.org/data/most-popular-backend-frameworks-2012-2021/)
# node as backend
- ## [Node.js做Web后端优势为什么这么大？](https://www.zhihu.com/question/357717742/answers/updated)
- 从没见过哪个后端开发语言的标准库比js还小的，连leftpad这种常用的功能还有一个npm库，难以想象

- Node自身设计是异步的，而Java的主流框架底层都是同步的，包括io，jdbc等。而异步非阻塞是提高并发能力的不二法门。
  - 我们做过测试，阿里云2u2g的机器，一个http请求读redis的场景，node能做到8000并发，spring boot只能到2000多（一定要有io操作，http请求纯粹只返回一个字符串的场景node干不过spring）
  - 另外这个跟语法层面也有关系，js/ts的async/await是解决回调地域的完美方案，而java目前没有类似的方案，说到底，还是DNA的问题
# backend-solutions
- http-io
  - express
  - koa
  - fastify
- database
  - orm
  - seeding
  - migration
- auth
  - authentication
  - authorization
  - crypt/encryption
  - password reset
  - passport
  - oauth
- test(和前端相同)
  - mocha
- cache
  - redis
- workflow
  - 基于BPMN2.0的工作流: activiti, BPMN是BPM及workflow的建模语言标准之一
- scheduler
  - task queue
  - cron jobs
- validate/verification
  - request
  - password
- security
  - csrf
  - xss
- notification
- rule engine
- search
- storage
- admin
- mailing/email
- ssr
- more
  - configuration: dotenv
  - api docs: swagger
  - logger
  - sentry error reporting

## nestjs ecosystem

- core
  - nest
  - config
    - Configuration module for Nest based on the dotenv (to load process environment variables) package.
  - more
    - event-emitter
- web
  - swagger
  - graphql
  - jwt
  - serve-static
    - Serve static websites (SPA's) using Nest framework
  - throttler
    - A rate limiting module for NestJS to work with Fastify, Express, GQL, Websockets, and RPC 
- security
  - passport
- data
  - typeorm
  - sequelize
  - mongoose
  - cqrs
    - CQRS强调的是从架构上把CRUD系统拆分为两部分，command与query访问的数据模型不同
  - elasticsearch
  - azure-database
  - azure-storage
- cloud-arch
  - serverless-core
  - azure-serverless
- scheduler
  - bull
    - The fastest, most reliable, Redis-based queue for Node.
    - BullMQ is for handling distributed jobs and messages in NodeJS.
  - schedule
    - Schedule module for Nest based on the cron package.
- packages
  - ng-universal
    - Angular Universal module for Nest framework
  - schematics
    - Nest architecture element generation based on Angular schematics
- tooling
  - terminus
    - Terminus module for Nest framework
- more
  - nest-cli
  - typescript-starter

## java spring ecosystem

- core
  - spring-framework
    - core support for dependency injection, transaction management, web apps, data access, messaging, and more
    - core ioc + aop + beans + context + web + webmvc + websocket + jdbc + orm
  - spring-boot
    - an opinionated way of building Spring applications without xml and gets you up and running as quickly as possible.
- web
  - spring-web-flow
    - allows implementing the "flows" of a web application
  - spring-web-services
    - aims to facilitate contract-first SOAP service development
    - allowing for the creation of flexible web services using one of the many ways to manipulate XML payloads
  - spring-session
    - managing a user’s session information.
  - spring-hateoas
    - Simplifies creating REST representations that follow the HATEOAS principle.
  - spring-restdocs
    - frees you from the limitations of tools like Swagger.
- security
  - spring-security
    - comprehensive and extensible authentication and authorization support.
    - oauth2 + ldap + cas + acl + crypto + openid + rsocket
  - spring-security-oauth
    - Support for adding OAuth1(a) and OAuth2 features 
- data
  - spring-data
    - Provides a consistent approach to data access – relational, non-relational, map-reduce, and beyond.
  - spring-data-rest
    - Simplifies building hypermedia-driven REST web services on top of Spring Data repositories
  - spring-data-jpa
    - Simplifies the development of creating a JPA-based data access layer.
  - spring-data-elasticsearch
    - provides integration with the Elasticsearch search engine.
  - more
    - spring-data-redis,spring-data-mongodb,spring-data-neo4j
- big-data
  - spring-hadoop
    - extends Spring Batch by providing support for reading from and writing to HDFS, running various types of Hadoop jobs
    - more
      - spring-data-cassandra,spring-data-solr
- cloud-arch
  - spring-cloud
    - a set of tools for building and deploying microservices.
  - spring-cloud-dataflow
    - an orchestration service for composable data microservice applications on modern runtimes.
- cross-platform
  - spring-android
    - provide components of the Spring family for use in Android apps.
    - A Rest Client for Android; Auth support for accessing secure APIs
- extensions
  - spring-loaded
    - Java agent that enables class reloading in a running JVM
- packages
  - spring-integration
    - provides an extension of the Spring programming model to support the well-known Enterprise Integration Patterns (EIP)
    - enables lightweight messaging within Spring-based applications 
    - and supports integration with external systems via declarative adapters.
    - spring-integration-aws
  - spring-batch
    - optimizes the work of processing high-volume batch operations.
  - spring-amqp
    - applies core Spring concepts to the development of AMQP-based messaging solutions
    - provides a "template" as a high-level abstraction for sending and receiving messages. 
  - spring-kafka
    - Provides Familiar Spring Abstractions for Apache Kafka
  - spring-statemachine
    - aims to provide a common infrastructure to work with state machine concepts in Spring applications.
  - spring-roo
    - roo能根据pojo生成一整套CRUD代码，boot则是根据classpath里的组件使用一套默认配置；
- tooling
  - spring-ide
  - spring-shell
    - Spring based interactive shell
- more
  - spring-petclinic
    - sample pet store
# discuss-backend-solutions
- ## 

- ## 

- ## 

- ## Supabase really is the complete backend stack
- https://x.com/AntWilson/status/1864843592336052625
  - Database: @supabase
  - Auth: @supabase
  - Functions: @supabase
  - Realtime: @supabase
  - Queues: @supabase
  - Crons: @supabase
  - File storage: @supabase
  - Clothing: @supabase

- That one friend who’ll always be there for you... to pause your db

- Add ANALYTICS table and I tattoo your logo on my arm

- Two things missing: 
  1. Payment integration
  2. A starter app in nextjs and other frameworks using all these (at least nextjs)
