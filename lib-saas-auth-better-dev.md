---
title: lib-saas-auth-better-dev
tags: [auth, better-auth]
created: 2025-09-24T14:52:28.334Z
modified: 2025-09-24T14:52:43.269Z
---

# lib-saas-auth-better-dev

# guide
- pros
  - Framework Agnostic
  - Plugin Ecosystem: 2factor, magic link, passkey, email-otp...
  - multi-tenancy/rbac: Manage organizations and access control
  - Multiple social sign-on providers

- cons
  - 默认未使用jwt而是基于session, 但可通过plugin支持jwt

- features
  - Built-in support for secure email and password authentication
  - Manage user accounts and sessions with ease
  - Built-in rate limiter with custom rules
  - Automatic database management and migrations
  - Two Factor Authentication

- who is using #better-auth
  - ?
# draft

# dev-xp

- db-adapters-offcial
  - drizzle
  - prisma
  - mongodb
- db-adapters-community
  - typeorm
  - payloadcms
  - surrealdb
  - convex
  - instantdb
  - ronin
# codebase
- 内部的数据库操作大量使用了 Kysely
# more
