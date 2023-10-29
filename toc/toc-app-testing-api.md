---
title: toc-app-testing-api
tags: [api, testing, toc, tool]
created: 2023-02-08T07:57:21.326Z
modified: 2023-02-08T10:25:14.173Z
---

# toc-app-testing-api

# guide

# postman-like
- https://github.com/hoppscotch/hoppscotch /MIT/ts/vue
  - Install as a PWA on your device.
  - Offline support
  - WebSocket: Establish full-duplex communication channels over a single TCP connection.
- https://github.com/EsperoTech/yaade /Kotlin
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

- https://github.com/Kong/insomnia /MIT/ts/桌面版
  - https://insomnia.rest/
  - cross-platform API client for GraphQL, REST, WebSockets and gRPC.
  - available for Mac, Windows, and Linux
  - [Comparison of API development environments: Postman vs Insomnia](https://gist.github.com/samoshkin/c0a2c0dd85b1d5b02d893a0f6ac0e93c)
  - https://chrome.google.com/webstore/detail/insomnia-rest-client/gmodihnfibbjdecbanmpmbmeffnmloel?hl=en-US
    - not updated

- https://github.com/usebruno/bruno /MIT/js/tauri
  - https://www.usebruno.com/
  - Opensource IDE For Exploring and Testing Api's (lightweight alternative to postman/insomnia)
  - Bruno stores your collections directly in a folder on your filesystem. We use a plain text markup language, Bru, to save information about API requests.
  - Bruno is offline-only. There are no plans to add cloud-sync to Bruno, ever. 

- https://github.com/kubeshop/tracetest /go/ts
  - Generate end-to-end tests automatically from your traces. For QA, Dev, & Ops.

- https://github.com/stoplightio/prism
  - packages for API mocking and contract testing with OpenAPI v2 (formerly known as Swagger) and OpenAPI v3.x.
  - 命令行工具
  - Mock Servers: Life-like mock servers from any API Specification Document.
  - Comprehensive API Specification Support: OpenAPI v3.1, OpenAPI v3.0, OpenAPI v2.0 (formerly Swagger) and Postman Collections.
# api-utils

## openapi

- https://github.com/drwpow/openapi-typescript
  - Generate TypeScript types from OpenAPI 3 specs
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
# web-performance
- https://github.com/nolanlawson/fuite /js
  - a CLI tool for finding memory leaks in web apps.
# web-testing
- https://github.com/puppeteer/puppeteer
  - Node.js API for Chrome

- https://github.com/microsoft/playwright
  - a framework for Web Testing and Automation. 
  - It allows testing Chromium, Firefox and WebKit with a single API.
  - microsoft/playwright-python is almost call-for-call compatible with puppeteer, and gives you access to Firefox and Webkit as well.
# web-debug
- https://github.com/liriliri/eruda /js
  - https://eruda.liriliri.io/
  - Console for Mobile Browsers.
# more
