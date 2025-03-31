---
title: toc-app-testing-api
tags: [api, testing, toc, tool]
created: 2023-02-08T07:57:21.326Z
modified: 2023-02-08T10:25:14.173Z
---

# toc-app-testing-api

# guide

- [Testing Distributed Systems | Curated list of resources on testing distributed systems](https://asatarin.github.io/testing-distributed-systems/)
# postman-like
- https://github.com/hoppscotch/hoppscotch /MIT/202401/ts/vue
  - https://hoppscotch.io/
  - Open Source API Development Ecosystem
  - Install as a PWA on your device.
  - Offline support
  - WebSocket: Establish full-duplex communication channels over a single TCP connection.
- https://github.com/EsperoTech/yaade /1.5kStar/MIT/202406/ts/Kotlin
  - self-hosted, collaborative API development environment.
  - Even though popular solutions like Hoppscotch exist, their self-hosted app does not come with authentication and relies on Firebase for persistency. 
  - Yaade is developed from the ground up with self-hosting and security in mind.
  - Multi-user: manage users and their permissions
  - Backend built with Kotlin.
  - H2 file-based database

- https://github.com/mockoon/mockoon /ts
  - Mockoon is the easiest and quickest way to run mock APIs locally. 
  - No remote deployment, no account required, open source.
  - It's a desktop application and a CLI that help you work faster with APIs by mocking them. 
  - Integrate third-party APIs quicker, improve your integration tests, speed up your development, etc.

- https://github.com/Kong/insomnia /apache2/ts/仅桌面版
  - https://insomnia.rest/
  - cross-platform API client for GraphQL, REST, WebSockets and gRPC.
  - available for Mac, Windows, and Linux
  - [Comparison of API development environments: Postman vs Insomnia](https://gist.github.com/samoshkin/c0a2c0dd85b1d5b02d893a0f6ac0e93c)
  - https://chrome.google.com/webstore/detail/insomnia-rest-client/gmodihnfibbjdecbanmpmbmeffnmloel?hl=en-US
    - not updated

- https://github.com/usebruno/bruno /MIT/202405/js/tauri
  - https://www.usebruno.com/
  - Opensource IDE For Exploring and Testing Api's (lightweight alternative to postman/insomnia)
  - Bruno stores your collections directly in a folder on your filesystem. 
  - We use a plain text markup language, Bru, to save information about API requests.
  - 🧐 Bruno is offline-only. There are no plans to add cloud-sync to Bruno, ever. 

- https://github.com/firecamp-dev/firecamp /AGPLv3/202403/ts
  - https://firecamp.dev/
  - Developer-first OpenSource API DevTool, Postman/Insomnia alternative.
  - a dx-first API development platform that helps developers design, develop, test, and document their APIs
  - multi-protocol testing capabilities with Rest, GraphQL, Websocket, and SocketIO APIs.

- https://github.com/flawiddsouza/Restfox /MIT/202406/ts/vue
  - https://restfox.dev/
  - Offline-First Minimalistic HTTP & Socket Testing Client for the Web & Desktop

- https://github.com/kubeshop/tracetest /go/ts
  - Generate end-to-end tests automatically from your traces. For QA, Dev, & Ops.

- https://github.com/stoplightio/prism
  - packages for API mocking and contract testing with OpenAPI v2 (formerly known as Swagger) and OpenAPI v3.x.
  - 命令行工具
  - Mock Servers: Life-like mock servers from any API Specification Document.
  - Comprehensive API Specification Support: OpenAPI v3.1, OpenAPI v3.0, OpenAPI v2.0 (formerly Swagger) and Postman Collections.

- https://github.com/rookie-luochao/openapi-ui /MIT/202407/ts
  - http://www.openapi-ui.com/
  - 基于 OpenAPI/Swagger 规范的接口文档，快速模拟请求参数并调用接口，也是简化版 postman 工具
# api-utils

## openapi

- https://github.com/drwpow/openapi-typescript
  - Generate TypeScript types from OpenAPI 3 specs
# mock-api
- https://github.com/mwinteringham/restful-booker /GPLv3/202312/js
  - https://automationintesting.com/training/apitesting/
  - https://restful-booker.herokuapp.com/
  - An API playground created by Mark Winteringham for those wanting to learn more about API testing and tools
  - 依赖express、nedb、js2xmlparser、nedb、pug

- https://github.com/ServeRest/ServeRest /GPLv3/202401/js
  - https://serverest.dev/
  - REST server for API testing study
  - 依赖express、nedb-promises
  - GET, POST, PUT and DELETE verbs with data persistence
  - In the online environment, registered data is removed daily, while on-site, simply restart ServeRest.
# proxy
- https://github.com/bubenshchykov/ngrok
  - Expose your localhost to the web. Node wrapper for ngrok.
# events-webhook
- https://github.com/TwilioDevEd/webhooks-course
  - notes and code for the Understanding Webhooks course

- https://github.com/Commit451/skyhook
  - Parses webhooks and forwards them in the proper format to Discord.
- https://github.com/discohook/site
  - The easiest way to build and send Discord messages using webhooks

- https://github.com/octokit/webhooks.js
  - GitHub webhook events toolset for Node.js
  - https://github.com/octokit/webhooks
    - machine-readable, always up-to-date GitHub Webhooks specifications

- https://github.com/probot/smee.io /js
  - https://smee.io/
  - Smee is a webhook payload delivery service - it receives webhook payloads, and sends them to listening clients. 
  - Smee works with two components: the public website smee.io and the smee-client. They talk to each other via Server-Sent Events
  - Webhook payloads are never stored on the server, or in any database; 
    - the Smee.io server is simply a pass-through. 
    - However, we do store payloads in localStorage in your browser
# performance
- https://github.com/sirupsen/napkin-math /rust/go
  - Techniques and numbers for estimating system's performance from first-principles

- https://github.com/nolanlawson/fuite /202401/js
  - a CLI tool for finding memory leaks in web apps.
  - fuite launches Chrome using Puppeteer, loads a web page, and runs a scenario against it. 
  - It runs the scenario some number of iterations (7 by default) and looks for objects that leaked 7 times (or 14 times, or 28 times). 
  - This might sound like a strange approach, but it's useful for cutting through the noise in memory analysis.
# web-testing
- https://github.com/puppeteer/puppeteer /202311/ts
  - https://pptr.dev/
  - Node.js API for Chrome

- https://github.com/cloudflare/puppeteer /202308/ts
  - https://developers.cloudflare.com/
  - Puppeteer Core fork that works with Cloudflare Browser Workers
  - https://twitter.com/Barret_China/status/1730047181028212992
    - 1）首先在云端预热一批 Chrome/Chromium 会话窗口，有点类似 Serverless Function 的冷启动
    - 2）每次发起 Puppeteer 任务的时候，会通过 API 从会话池中获取一个 ws 连接地址，这块工作在框架和工具层面做了完善的处理（网页上配置不了，需要走 CLI）
    - 3）云端对回话窗口池进行自动伸缩容管理，同时也会对获取 ws 连接的任务做队列管理

- https://github.com/microsoft/playwright
  - a framework for Web Testing and Automation. 
  - It allows testing Chromium, Firefox and WebKit with a single API.
  - microsoft/playwright-python is almost call-for-call compatible with puppeteer, and gives you access to Firefox and Webkit as well.
# web-debug
- https://github.com/liriliri/eruda /MIT/202411/js/inactive
  - https://eruda.liriliri.io/
  - Console for Mobile Browsers.

- https://github.com/hellof2e/vite-plugin-dev-inspector /MIT/202409/ts
  - 一个Vite插件，点击页面元素，IDE直接打开对应代码文件。支持 Vue2, Vue3, React, Svelte, Angular, SSR等任何前端工程
  - Vite-plugin-dev-inspector was inspired by vite-plugin-vue-inspector, but it does not repy on front-end frameworks. It can support any front-end technology stack at the same time, such as Vue 2 & 3, React, Angular, Svelte, Nuxt and SSR.
# jmeter
- https://github.com/anthonygauthier/jmeter-es-backendlistener-dashboard /201810/js
  - Dashboard to visualize JMeter results generated via the ElasticSearch Backend Listener. 
  - Alternative to Grafana & Kibana.
# more
