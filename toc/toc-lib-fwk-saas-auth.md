---
title: toc-lib-fwk-saas-auth
tags: [auth, saas, toc]
created: 2025-09-23T09:27:58.490Z
modified: 2025-09-23T09:28:08.532Z
---

# toc-lib-fwk-saas-auth

# guide
- tips
  - 用户管理的参考方案, 可直接在现有cms的基础上提取部分代码
# popular
- https://github.com/goauthentik/authentik /18.2kStar/MIT+EE/202509/python
  - https://goauthentik.io/
  - open-source Identity Provider (IdP) for modern SSO. 
  - It supports SAML, OAuth2/OIDC, LDAP, RADIUS, and more, designed for self-hosting from small labs to large production clusters.
  - 管理ui方便易用

- https://github.com/keycloak/keycloak /29.7kStar/apache2/202509/java
  - https://www.keycloak.org/
  - Open Source Identity and Access Management solution for modern Applications and Services.
  - Add authentication to applications and secure services with minimum effort. No need to deal with storing users or authenticating users.
  - Keycloak provides user federation, strong authentication, user management, fine-grained authorization, and more.
  - 依赖quarkus、jboss、wildfly、hibernate, 未使用spring

- https://github.com/authelia/authelia /25.3kStar/apache2/202509/go
  - https://www.authelia.com/
  - open-source authentication and authorization server providing two-factor authentication and single sign-on (SSO) for your applications via a web portal. 
  - It acts as a companion for reverse proxies by allowing, denying, or redirecting requests.
  - Authelia can be installed as a standalone service from the AUR, APT, FreeBSD Ports, or using a static binary, .deb package, as a container on Docker or Kubernetes.

- https://github.com/casdoor/casdoor /12.3kStar/apache2/202509/go/国人主导
  - https://casdoor.org/
  - open-source UI-first Identity and Access Management (IAM) / Single-Sign-On (SSO) platform with web UI supporting OAuth 2.0, OIDC, SAML, CAS, LDAP, SCIM, WebAuthn, TOTP, MFA and RADIUS

- https://github.com/better-auth/better-auth /20.8kStar/MIT/202509/ts
  - https://better-auth.com/
  - Better Auth is framework-agnostic authentication (and authorization) library for TypeScript
  - It provides a comprehensive set of features out of the box and includes a plugin ecosystem that simplifies adding advanced functionalities
  - Plugin Ecosystem
  - Built-in support for secure email and password authentication
  - Built-In Rate Limiter
  - Multiple social sign-on providers
  - Two Factor Authentication

- https://github.com/nextauthjs/next-auth /21.4kStar/ISC/202403/ts
  - https://authjs.dev/
  - a set of open-source packages that are built on Web Standard APIs for authentication in modern applications with any framework on any platform in any JS runtime.
  - Designed to work with any OAuth service, it supports 2.0+, OIDC
  - Built-in support for many popular sign-in services
  - Built-in email/passwordless/magic link authentication
  - Built-in support for MySQL, MariaDB, Postgres, Microsoft SQL Server, MongoDB, SQLite, etc.
  - [database adapters](https://authjs.dev/reference/adapters)
    - 支持sequelize、prisma、drizzle
  - When JSON Web Tokens are used, they are encrypted by default (JWE) with A256CBC-HS512
  - [NextAuth.js is becoming Auth.js_20221215](https://twitter.com/balazsorban44/status/1603082914362986496)
    - Runtime/framework agnostic
  - [Integration with an existing project _202006](https://github.com/nextauthjs/next-auth/issues/296)
    - These are the options that are probably most relevant
  - https://github.com/nextauthjs/next-auth-example
    - Example showing how to use NextAuth.js with Next.js

- https://github.com/logto-io/logto /10.8kStar/MPLv2/202509/ts
  - https://logto.io/
  - https://docs.logto.io/
  - a modern Auth0 alternative for building identity infrastructure with minimal effort
  - Multi-tenancy, enterprise SSO, and RBAC: ready to use, no workarounds.
  - Pre-built sign-in flows, customizable UIs, and SDKs for 30+ frameworks.
  - Full support for OIDC, OAuth 2.1, and SAML without the protocol pain.
  - Various sign-in options, such as social, email, phone number, and username, including passwordless authentication
  - Multi-tenancy & organizations: Organization RBAC, member invites, just-in-time provisioning, and more.
  - User management and audit logs help you understand user identity-related information and keep your security on track.
  - https://github.com/logto-io/js
    - The monorepo for SDKs and working samples written in JavaScript (Well, mostly in TypeScript).

- https://github.com/panva/node-oidc-provider /3.5kStar/MIT/202509/js
  - OpenID Certified™ OAuth 2.0 Authorization Server implementation for Node.js
# examples
- https://github.com/auth0-blog/spa-jwt-authentication-tutorial /201507/js
  - Add authentication to a vanilla js single page app

- https://github.com/rajeshpillai/node-jwt-step-by-step /202005/js
  - A simple express jwt server with vanilla javascript client for testing
  - backend + frontend

- https://github.com/LeeSoMyoung/Express-NodeJS-Auth-with-JWT /202202/js
  - NodeJS, Express, MySQL, Vanilla JS로 구현한 Authentication

- https://github.com/cornflourblue/node-mongo-registration-login-api /202007/js
  - NodeJS + MongoDB API for User Management, Authentication and Registration
  - [NodeJS + MongoDB - Simple API for Authentication, Registration and User Management | Jason Watmore's Blog](https://jasonwatmore.com/post/2018/06/14/nodejs-mongodb-simple-api-for-authentication-registration-and-user-management)
# jwt
- https://github.com/rajeshpillai/node-jwt-step-by-step /202005/js
  - A simple express jwt server with vanilla javascript client for testing
  - backend + frontend

- https://github.com/braitsch/node-login /MIT/202104/js
  - A template for quickly building login systems on top of Node.js & MongoDB

- https://github.com/cornflourblue/node-mongo-registration-login-api /MIT/202007/js
  - NodeJS + MongoDB API for User Management, Authentication and Registration
  - 依赖mongoose、express-jwt、jsonwebtoken、bcryptjs
  - https://github.com/cornflourblue/react-redux-registration-login-example /202008/js
  - https://github.com/cornflourblue/react-redux-jwt-authentication-example /202006/js
- https://github.com/cornflourblue/node-mysql-registration-login-api /MIT/202008/js
  - Node.js + MySQL API for User Management, Authentication and Registration
  - 依赖sequelize6、express-jwt、express-jwt、bcryptjs
# fwk-better-auth
- https://github.com/better-auth/awesome
  - Adapters, Plugins
  - https://github.com/better-auth/examples
    - framework-specific projects that demonstrate how to implement authentication with Better Auth

- https://github.com/daveyplate/better-auth-ui /1kStar/MIT/202509/ts
  - https://better-auth-ui.com/
  - shadcn/ui components built for better-auth
  - Sign In/Up, Forgot Password, UserAvatar, Email Template, Settings Cards
  - styled with TailwindCSS and shadcn/ui
- https://github.com/Kinfe123/better-auth-ui /202509/ts
  - https://better-auth.farmui.com/
  - Custom + Pre built Auth UI for better-auth that you can copy / paste with their functionality

- https://github.com/daveyplate/better-auth-nextjs-starter /202509/ts
  - https://nextjs.better-auth-starter.com/
  - Better Auth Next.js starter template with PostgreSQL, Drizzle, shadcn/ui and TanStack Query
  - https://github.com/daveyplate/better-auth-nextjs-pages-starter
    - Better Auth Next.js (Pages Router) starter template with PostgreSQL, Drizzle, shadcn/ui and TanStack Query

- https://github.com/daveyplate/better-auth-tanstack-starter /202504/ts/inactive
  - Better Auth TanStack starter template with PostgreSQL, Drizzle, shadcn/ui and TanStack Query
  - https://github.com/daveyplate/better-auth-tanstack /MIT/202505/ts
    - Tanstack Query hooks for Better Auth.

- https://github.com/ping-maxwell/better-auth-kit /MIT/archived
  - A collection of plugins, tools, libraries, examples, and more for Better-Auth
  - [STATE OF BETTER-AUTH-KIT ](https://github.com/ping-maxwell/better-auth-kit/issues/37)
    - I don’t believe I can continue maintaining everything myself. I already work on Better-Auth full-time, and with other parts of life taking up time, it’s not sustainable. Because of this, the current project will be deprecated.
    - https://github.com/MUKE-coder/better-auth-v2-kit
- https://github.com/better-auth-extended/better-auth-extended /MIT/202509/ts
  - https://better-auth-extended.jsolano.de/
  - A curated set of plugins, tools, and libraries for Better Auth
  - meant as a successor to ping-maxwell's Better-Auth-Kit which has been archived

- https://github.com/ping-maxwell/better-auth-dashboard /202505/ts/archived
  - A Better-Auth powered admin dashboard.
  - Configure plugins straight from the dashboard.
  - Advanced route protection.

- https://github.com/zexahq/better-auth-starter /MIT/202507/ts
  - A modern Next.js boilerplate with authentication, admin dashboard, and user management built with Better Auth, Drizzle ORM, and PostgreSQL

- https://github.com/foxlau/react-router-v7-better-auth /202508/ts
  - a template that can be deployed on Cloudflare Workers, built with React Router v7 (Remix), Better Auth, Drizzle ORM, and D1.
  - 仅使用router部分，remix几乎没用
- https://github.com/matthewlynch/better-auth-react-router-cloudflare-d1 /MIT/202502/ts
  - https://better-auth-react-router-cloudflare-d1.mattlynch.workers.dev/
  - Example of Better Auth integrated with React Router (v7) which is setup to deploy to Cloudflare & use D1 for the database
  - 代码非常简单，仅2路由
  - https://github.com/atman-33/react-router-cloudflare-boilerplate /202507/ts/inactive
    - Full-stack boilerplate with React Router v7, Cloudflare, Drizzle ORM, Tailwind, and better-auth.
    - 路由有点乱

- https://github.com/yeasin2002/bulletproof-nextjs-starter /202509/ts
  - https://bulletproof-nextjs-starter.vercel.app/
  - A production-ready Next.js boilerplate with modern tooling, comprehensive testing, and enterprise-grade features
- https://github.com/cahyawibawa/whelve /202508/ts
  - A opinionated SaaS starter w/ Next 15 & better-auth
  - Next.js 15, NeonDB, Drizzle, Better Auth

- https://github.com/laduniestu/nextstart /202509/ts
  - Nextjs starterkit using Better Auth
  - https://github.com/laduniestu/better-next /legacy

- https://github.com/rudrodip/titan /MIT/202506/ts
  - Next.js 15 fullstack template with better-auth for authentication and drizzle-orm as the orm
  - Drizzle ORM with PostgreSQL support
  - Multi-provider support (Neon, PlanetScale, Turso, Xata)

- https://github.com/TheOrcDev/better-auth-starter /202509/ts
  - The Better Auth Starter is simple starter pack using Next.js, Better Auth, Shadcn, Drizzle, and Neon
- https://github.com/indieceo/Indiesaas /202508/ts
  - Next.js Saas Starter. Built with Better Auth UI, Shadcn/Ui, Drizzle ORM, UploadThing, Resend and Stripe

- https://github.com/blefnk/relivator-nextjs-template /MIT/202505/ts
  - next.js 15 react 19 ecommerce template
  - better-auth polar shadcn/ui tailwind drizzle orm typescript ts radix, postgres neon, app router

- https://github.com/nicksan222/Halo /202509/ts
  - A sleek monorepo template powered by Vercel, Neon, Drizzle, Better Auth, and shadcn/ui.

- https://github.com/RvDstudio/nextjs_drizzle_better-auth /202508/ts
  - A Next.js starter kit integrating Drizzle ORM for type-safe database operations, Better Auth
- https://github.com/JavaScript-Mastery-Pro/e-commerce
  - Nike-style eCommerce built with Devin AI, Next.js, TS, Tailwind, and Better Auth. Features product pages, cart
  - https://github.com/Achour/nextjs-better-auth
  - https://github.com/mtcnbzks/better-auth-starter

- https://github.com/wrsrsh/startstack /MIT/202507/ts/paused
  - i have since moved away from next.js as the base building block for my applications

- https://github.com/Bekacru/nextjs-better-auth-SaaS-stater /MIT/202411/ts/inactive
  - Forked from https://github.com/leerob/next-saas-starter
  - Changes the jwt authentication to better-auth

- https://github.com/Its-Satyajit/nextjs-typescript-tailwind-shadcn-postgresql-drizzle-orm-better-auth-template /202503/ts
  - https://nextjs-template-its-satyajits-projects.vercel.app/
  - full-stack web app template built with Next.js, TypeScript, Tailwind CSS, PostgreSQL, Drizzle ORM, and Better Auth.

- https://github.com/caru-ini/fullstack-template /MIT/202509/ts
  - https://template-demo.caru.moe/
  - fullstack template built with Next.js, featuring authentication, database integration, and beautiful UI components
- https://github.com/rayandripo/nextjs_drizzle_better-auth /202509
  - A Next.js starter kit integrating Drizzle ORM for type-safe database operations, Better Auth for secure authentication, and NeonDB
  - https://github.com/ItisSubham/Better-Auth-Starter
  - https://github.com/DimitarY/next-starter

- https://github.com/thaitype/thaitype-stack-mongodb-template /MIT/202509/ts
  - Type-Safe Next.js Stack using Simple Clean Architecture with MongoDB Template For AI Friendly
  - Enterprise Architecture - Entity-based repository pattern
  - Full TypeScript with `tRPC` API layer
  - MongoDB with audit logging via Monguard
  - https://github.com/codeSTACKr/better-auth-mongodb
  - https://github.com/renanwilliam/better-auth-dynamodb

- https://github.com/CW-Codewalnut/monorepo-template /202509/ts
  - Full Stack TypeScript first Monorepo template. 
  - Uses Bun, Hono, tRPC, Better Auth, Drizzle, Sqlite, React, React Router, Shadcn UI, Vite, Turborepo, Biome.

- https://github.com/LovelessCodes/hono-better-auth /202506/ts/仅后端/太简单
  - combines the power of Hono, Better Auth, and Drizzle ORM to provide a robust and scalable authentication solution.
  - https://github.com/naolson2025/hono-react-better-auth
  - https://github.com/Lostovayne/Production-Grade-Authentication

- https://github.com/JuanPabloGilA/hono-react-boilerplate /MIT/202509/ts
  - a boilerplate for react, postgres, hono, drizzle, ai, better-auth, tanstack-query, tanstack-router, shadcn and tailwind
  - https://github.com/alwaysnomads/better-hono

- https://github.com/mockkey/flarekit /MIT/202508/ts
  - https://flarekit.mockkey.com/
  - Flarekit is a modern full-stack SaaS starter kit built with React Router v7, Better Auth, Hono, and Cloudflare Workers

- https://github.com/dotnize/react-tanstarter /Unlic/202505/ts
  - https://tanstarter.nize.ph/
  - minimal TanStack Start template with Better Auth, Drizzle ORM, shadcn/ui
  - React 19 + React Compiler
  - TanStack Start + Router + Query
  - Drizzle ORM + PostgreSQL
  - Tailwind CSS + shadcn/ui
- https://github.com/jellekuipers/kolm-start-admin
  - A TanStack Start + better-auth admin starter with Drizzle ORM, React Aria.

- https://github.com/ThallesP/nestjs-better-auth /202509/ts
  - A comprehensive NestJS integration library for Better Auth, providing seamless authentication and authorization for your NestJS applications.
  - https://github.com/laakal/nestjs-better-auth-template
  - https://github.com/buiducnhat/nest-better-auth
    - A NestJS integration library for better-auth, providing seamless authentication support for both Express and Fastify platforms
  - https://github.com/underfisk/nestjs-better-auth
    - A nestjs module to integrate better-auth

- https://github.com/lifefloating/nestjs-project-template /MIT/202509/ts
  - https://lifefloating.github.io/nestjs-project-template/
  - NestJS Bun project template, Boilerplate. Auth, Better-Auth, Prisma, MongoDB, Pino, Docker.

- https://github.com/Nick-Lucas/mcp-server-client-betterauth /202509/ts
  - minimal NodeJS MCP Server and Client implementation with oauth provided by Better Auth

- https://github.com/codinginflow/better-auth-tutorial /202509/ts
  - https://better-auth-tutorial-two.vercel.app/
  - Learn how to implement Better-Auth with Next.js 15 and Prisma Postgres in this YouTube tutorial: https://www.youtube.com/watch?v=w5Emwt3nuV0

- https://github.com/amal-chandran/sso-better-auth /202504/ts/inactive
  - Better Auth SSO Example with Clerk OAuth Provider

## better-auth-utils

- https://github.com/nikeokoronkwo/better-auth.go /202509/go
  - a port of the popular better-auth library in Go. 
  - Most of the features in better-auth are equivalent in Go, but implementations may differ.

- https://github.com/azizndao/better-auth /202509/go/NoDeps
  - framework-agnostic authentication and authorization library for Go, inspired by Better Auth. 
  - This implementation provides all essential authentication features using the latest net/http capabilities with zero external framework dependencies, making it pluggable into any Go web application.
  - Framework Agnostic: Uses standard `net/http` interfaces
  - JWT Support - Full JWT token generation and validation
  - Plugin Architecture - Extensible plugin system

- https://github.com/better-auth-rs/better-auth-rs /MIT/202508/rust
  - https://better-auth.rs/
  - A Rust authentication framework inspired by Better-Auth, providing a plugin-based architecture and type-safe authentication solutions.
  - Full support for asynchronous operations
  - Support for multiple databases through adapter pattern
  - Support for Axum (extensible to other frameworks)

- https://github.com/kriasoft/better-auth /MIT/202509/ts
  - https://kriasoft.com/better-auth/
  - 18 enterprise plugins for Better Auth - cloud storage, security, analytics & more
  - better-auth-feature-flags - Feature flags and gradual roll-outs with user targeting, A/B testing, and admin controls

- https://github.com/Zastinian/better-auth-typeorm /MIT/202508/ts
  - A typeorm adapter for better-auth

- https://github.com/octet-stream/better-auth-mikro-orm /MIT/202508/ts
  - MikroORM Adapter for Better Auth

- https://github.com/kursattkorkmazzz/better-auth-sequelize-adapter /202509/ts
  - a adapter for Sequelize ORM

- https://github.com/Daanish2003/validation-better-auth /MIT/202505/ts
  - A flexible and extensible validation plugin for the Better Auth framework. 
  - This package allows developers to validate API request using standard schema library

- https://github.com/GeKorm/better-auth-harmony /MIT/202507/ts
  - A better-auth plugin for email & phone normalization and additional validation, blocking over 55, 000 temporary email domains.

- https://github.com/marcellosso/better-auth-localization /MIT/202509/ts
  - A localization plugin for Better Auth that automatically translates error messages.

- https://github.com/cnbrown04/better-auth-abac /202507/ts
  - A plugin for ABAC in better-auth

- https://github.com/BartoszTrading/affiliate-better-auth /202509/ts
  - A tiny affiliate/referral plugin for Better Auth.
# fwk-authentik
- https://github.com/alicrossnet/sso-frontend-app /202409/js/inactive
  - This a Demo app for implementing SSO.
  - [Implementing SSO using Authentik _202407](https://medium.com/@ali.ravian1308/implementing-sso-using-authentik-74a727826c3b)

- https://github.com/authentik-community/sdk-integrations /MIT/202409/python
  - Examples on how to integrate authentik with various SDKs (Oauth2/OpenID, SAML, etc.) in various languages

- https://github.com/OpenRailAssociation/authentik-user-manager
  - Manage users and their groups on Authentik instances by local configuration YAML files

- https://github.com/svetlyopet/authentik-cli /apache2/202508/go
  - CLI tool for managing Authentik in a way that allows multi-tenancy
  - Creates a tenant abstraction with RBAC controls over resources
  - Create, list, update, and delete Authentik resources
  - Designed for scripting & automation (JSON/YAML output)

- https://github.com/patchmonkey/opencloud-authentik-specific-config /202505/yaml
  - My personal configuration for integrating authentik with opencloud 2.3.0 for external OIDC.

- https://github.com/burritosoftware/Outline-Authentik-Connector
  - Syncs groups between Authentik and Outline
  - https://github.com/mnixry/outline-authentik-groupsync

- https://github.com/UltimatumGamer/unleash-sso-authentik
  - Unleash configuration that supports authentik as sso provider

- https://github.com/tagoKoder/idp-auth-flow /202509/go/dart/java
  - Multi-platform OpenID Connect (OIDC) authentication using a single IdP (Authentik).
  - Both the mobile app (Flutter) and the web admin (Angular) share the same login flow.
  - A Go gateway validates issued tokens (multi-issuer support) and communicates with a Spring Boot identity microservice via gRPC to link/upsert users and return a compact profile.

- https://github.com/VULGA01/Authentik-Login-theme-Glassmorphism /MIT/202509/css
  - A custom glassmorphism login theme for Authentik, designed by VULGA.
  - [My new Authentik Theme ! : r/Authentik](https://www.reddit.com/r/Authentik/comments/1n9o3nd/my_new_authentik_theme/)

- https://github.com/nelsonlaidev/e2e-testing-with-better-auth /202509/ts
  - This repository demonstrates how to perform end-to-end (E2E) testing on a web application that uses Better Auth for authentication. It includes examples of setting up a test environment.
  - [E2E Testing with Better Auth _202509](https://nelsonlai.dev/blog/e2e-testing-with-better-auth)
# authentication
- https://github.com/libregraph/lico /51Star/apache2/202507/go
  - LibreGraph Connect implements an OpenID provider (OP) with integrated web login and consent forms.
  - LibreGraph Connect has it origin in Kopano Konnect and is meant as its vendor agnostic successor.
  - Lico can provide user login based on available backends.

- https://github.com/casbin/node-casbin /ts
  - https://casbin.org/
  - An authorization library that supports access control models like ACL, RBAC, ABAC in Node.js and Browser

- https://github.com/stalniy/casl /5.4kStar/MIT/202401/ts
  - https://casl.js.org/
  - CASL is an isomorphic authorization JavaScript library which restricts what resources a given user is allowed to access
  - designed to be incrementally adoptable and can easily scale between a simple claim based and fully featured subject and attribute based authorization.
  - Heavily inspired by cancan(from ruby-on-rails).
  - ⚖️ CASL implements Attribute Based Access Control
  - who is using #casl
    - strapi
  - https://github.com/fratzinger/feathers-casl /ts
    - a convenient layer to use CASL in feathers.js.
    - Fully powered by Feathers 5 & CASL 6
# authorization

# auth-client/ui

- https://github.com/clerk/javascript /1.6kStar/MIT/202509/ts
  - https://clerk.com/
  - Official JavaScript repository for Clerk authentication

- https://github.com/stack-auth/stack-auth /5.9kStar/MIT/202506/ts
  - https://stack-auth.com/
  - Open-source Auth0/Clerk alternative
  - It is developer-friendly and fully open-source (licensed under MIT and AGPL). MIT for the client libraries, AGPL for the serverside
  - Our managed service is completely optional and you can export your user data and self-host, for free, at any time.
  - We support Next.js, React, and JavaScript frontends, along with any backend that can use our REST API. 
  - Authentication components that support OAuth, password credentials, and magic links
  - Multi-tenancy & teams
  - Role-based access control
  - Impersonate(扮演) users for debugging and support, logging into their account as if you were them
  - You can now open the dev launchpad at http://localhost:8100. From there, you can navigate to the dashboard at http://localhost:8101, API on port 8102, demo on port 8103, docs on port 8104, Inbucket (e-mails) on port 8105, and Prisma Studio on port 8106. 
  - [Show HN: Stack, an open-source Clerk/Firebase Auth alternative | Hacker News _202404](https://news.ycombinator.com/item?id=40031090)

- https://github.com/openauthjs/openauthjs /202411/ts
  - openauthjs

- https://github.com/oslo-project/jwt /MIT/202409/ts
  - https://jwt.oslojs.dev/
  - https://oslojs.dev/
  - Oslo is an open-source project that aims to provide high-quality auth packages for server-side JS. 
  - Runtime agnostic. Zero third-party dependencies. Fully typed.
- https://github.com/lucia-auth/lucia /6.8kStar/MIT/202403/ts
  - https://lucia-auth.com/
  - a simple and flexible user and session management library that provides an abstraction layer between your app and your database. 
  - Middleware allows Lucia to read the request and response since these are different across frameworks and runtime
    - 支持express、fastify、nextjs、astro
  - [A database is required for storing your users and sessions](https://lucia-auth.com/database/)
    - 支持mongoose、sqlite、pg、prisma、drizzle-orm、kysely
  - [Future plans · lucia-auth/lucia _20241007](https://github.com/lucia-auth/lucia/discussions/1707)
    - I am planning to deprecate the library early next year. It has become abundantly clear to me that Lucia, in the current state, is not working. 
    - I now implement sessions from scratch and don't use the library for my personal projects.
    - I could make Lucia into something more of a framework, akin to Auth.js. However, they come with their own issues on top of Lucia's, and it should be its own package anyway.
    - https://x.com/pilcrowonpaper/status/1843258855280742481
    - I will continue to maintain all my other projects, including Oslo and Arctic
    - This is exactly what make dev’s lose total trust in small half baked libs.
  - 🎯 [Lucia 3.0 · Discussion _20240127](https://github.com/lucia-auth/lucia/discussions/1361)
    - Lucia doesn't use JWTs
    - We used to support JWT and it was a broken mess. Token rotation requires additional complexity, you need to sync state in the client, and the added security risks requires you to just do more. Even if it was simple, sessions and JWTs are 2 totally different things and require different db tables. Supporting both with a single library doesn't make any sense.
    - I would prefer a jwt session. Is it possible with Lucia? Any reason why a db approach is used instead?
      - it's beyond the scope of what lucia was initially designed to do (manage sessions), and maintaining the implementation was a mess.
      - Refresh token rotation is really tricky to abstract away in a flexible manner. 
      - And on the other hand, in-memory DB nicely pollyfills all of the benefits of JWT, so it might actually not make a lot of sense to maintain that solution.

- https://github.com/nickredmark/ooth /MIT/201902/ts/archived
  - https://nickredmark.github.io/ooth/
  - a user identity management system for node.js
  - Architecture - A typical scenario has 3 components:
    - The authentication/identity management server
    - A resource API (optional, can be integrated with the auth server or standalone)
    - The client
  - example with a starting UI with all the main user account flow is programmed with next.js. 

- https://github.com/Swizec/useAuth
  - The simplest way to add authentication to your React app.
  - You'll need an account with Auth0 or Netlify Identity and the appropriate access keys.
  - We use XState behind the scenes to manage authentication state for you.
# more
