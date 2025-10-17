---
title: toc-repos-lang-golang
tags: [examples, golang, toc]
created: 2025-04-17T08:16:51.748Z
modified: 2025-04-17T08:17:04.770Z
---

# toc-repos-lang-golang

# guide

# popular

# starter/template

- https://github.com/gothinkster/golang-gin-realworld-example-app /MIT/202208/go/inactive
  - Exemplary real world application built with Golang + Gin/gorm
  - 🍴 forks
  - https://github.com/alphawy45/golang-gin-realworld-example-app /202407
  - https://github.com/Alero-Awani/golang-gin-realworld-example-app /202405/ci
  - https://github.com/didietsuryadi95/invite-me /202204
  - https://github.com/jcolemorrison/golang-gin-realworld-example-app /202109
  - https://github.com/GHruXebia/golang-gin-realworld-example-app /ci-only
  - https://github.com/DimaMend/golang-gin-realworld-example-app /MIT/202408/go
    - built with Golang/Gin 

- https://github.com/ryanpenn/go-realworld /MIT/202412/go/gin/gorm
  - A realworld app implementation built with Go.

- https://github.com/amberxcc/realworld-backend-gin-gorm /202304/go
  - mysql， ✅ 可替换为sqlite
  - 实现清晰简单

- https://github.com/smy-101/gin_realworld /202408/go/mysql
  - 操作数据库混合使用了 gorm 和 sqlx, 只有一张表使用了sqlx

- https://github.com/clindseywsdemo/golang-gin-realworld-example-app /MIT/202204
  - sqlite + wire

- https://github.com/labasubagia/realworld-backend /MIT/202401/go/inactive
  - Golang Hexagonal Architecture codebase containing real world examples (CRUD, auth, advanced patterns, etc) that adheres to the RealWorld spec and API.
  - The hexagonal architecture is simply push any external dependency to the edge of the app and keep business logic (service) in the core part. With this architecture we can easily swap external dependencies such as swap restful API to gRPC, mongo to postgres etc.

- https://github.com/AngusGMorrison/realworld-go /MIT/202310/go/sqlite/inactive
  - Hexgonally Architected, Production-Ready, Golang Modular Monolith Example App
  - The example uses JSON over HTTP as its transport layer and SQLite as its datastore, but our business logic doesn't care. If we moved to gRPC and MongoDB, nothing in the business logic would need to change. 

- https://github.com/k0kishima/golang-realworld-example-app /202408/go/mysql/inactive
  - built with Gin and the Ent framework
  - You might also check out the Frontend implementation in Nuxt3.

- https://github.com/techschool/simplebank
  - Backend master class: build a simple bank service in Go
# web-fwk
- https://github.com/gin-gonic/gin /81.8kStar/MIT/202504/go
  - https://gin-gonic.com/
  - Gin is a HTTP web framework
  - It features a Martini-like API with much better performance -- up to 40 times faster thanks to httprouter.
  - Zero allocation router
  - Route grouping
  - Middleware support
  - Built-in rendering

- https://github.com/SteveCastle/modelpad /MIT/202509/go/ts
  - Modelpad is an Open Source AI assisted writing app with Notepad like features. 
  - Connect to cloud assisted writing models, or to your own locally hosted LLMs using Ollama.
  - 依赖gin、sonic、pgvector、supertokens
  - [How to Run an Open Source AI Text Editor - YouTube _202409](https://www.youtube.com/watch?v=InxEMuPLCx4)
# utils
- https://github.com/go-echarts/go-echarts /7.4kStar/MIT/202510/go
  - https://go-echarts.github.io/go-echarts/
  - go-echarts aims to provide a simple yet powerful data visualization library for Golang.
  - there have many program languages interactive with Echarts, such as pyecharts, which go-echarts learns and has evolved a lot from, and the echarts4j either.

## filesystem

- https://github.com/orbstack/fsnotify-macvirt
  - fsnotify is a Go library to provide cross-platform filesystem notifications on Windows, Linux, macOS, BSD, and illumos.
# gin
- https://github.com/appleboy/gorush /8.6kStar/MIT/202509/go
  - A push notification micro server using Gin framework written in Go (Golang) and see the demo app.
  - Support Firebase Cloud Messaging using go-fcm library for Android.
  - Support different Queue as backend like NSQ, NATS or Redis streams, defaut engine is local Channel.
  - 依赖gin、httpsnoop、nsq、nats

- https://github.com/openimsdk/open-im-server /15.3kStar/AGPL > apache2/202510/go
  - https://openim.io/
  - Unlike standalone chat applications such as Telegram, Signal, and Rocket. Chat, OpenIM offers an open-source instant messaging solution designed specifically for developers rather than as a directly installable standalone chat app
  - Comprising OpenIM SDK and OpenIM Server, it provides developers with a complete set of tools and services to integrate instant messaging functions into their applications
  - 依赖gin、gorm、rockscache、jwt、websocket、grpc、gokit、cobra、kafka
  - 202311改为使用mongodb，未使用gorm，[Feat/mongo pr](https://github.com/openimsdk/open-im-server/pull/1447)
  - 依赖多，有点乱
  - 🏠 Microservices Architecture: Supports cluster mode, including a gateway and multiple rpc services.
  - Diverse Deployment Options: Supports source code, Kubernetes, or Docker deployment.
  - Supports large-scale groups with hundreds of thousands, millions of users, and billions of messages.
  - OpenIM aims to provide developers with the necessary tools and framework to implement efficient instant messaging solutions in their applications.
  - OpenIMSDK, designed for OpenIMServer, is an IM SDK created specifically for integration into client applications.
  - https://github.com/openimsdk/openim-sdk-core /447Star/AGPL/202509/go
    - the core SDK of OpenIM, serving as the cross-platform foundation for all open-source OpenIM SDKs (excluding mini web).
    - All open-source OpenIM SDKs (except mini web) are built upon this core layer, ensuring consistency, stability, and seamless cross-platform integration.
  - https://github.com/openimsdk/openim-electron-demo /AGPL
    - Instant Messaging web desktop Windows/Mac/Linux
# examples

# more
