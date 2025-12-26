---
title: toc-lib-utils-services
tags: [backend, mq, redis, search, utils]
created: 2025-12-26T08:55:30.089Z
modified: 2025-12-26T08:56:31.035Z
---

# toc-lib-utils-services

# guide

# cache
- https://github.com/redis/node-redis /17.4kStar/MIT/202512/ts
  - https://redis.js.org/
  - a modern, high performance Redis client for Node.js.
  - [ioredis vs node-redis _202311](https://github.com/redis/node-redis/issues/2658)
    - ioredis was created as an alternative client 9 years ago by an individual: @luin. It was acquired by Redis Ltd. in 2023.
    - it's effectively unmaintained now.
    - For a long time, it had more functionality than this library (including sentinel support). However, over time there was an increasing amount of functionality with no direct support, and those had to be hand-rolled using raw commands. e.g. JSON commands. This is especially painful with TypeScript,
    - This project is now a monorepo that's written in TypeScript and includes direct support for more of the modern features
# message-queue

# middlewares

# more
