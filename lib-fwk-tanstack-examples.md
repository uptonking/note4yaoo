---
title: lib-fwk-tanstack-examples
tags: [examples, frontend, tanstack, web]
created: 2025-12-16T06:24:15.002Z
modified: 2025-12-16T06:25:12.641Z
---

# lib-fwk-tanstack-examples

# guide

# draft
- react-admin: migrated to tanstack-router
# popular
- https://github.com/KevinVandy/react-data-fetching /202507/ts
  - I have now built the same app 22 times for my workshop where I teach different data loading patterns in React Router, TanStack Router, Next.js, and even a bit of Astro and Sveltekit too.
  - https://x.com/KevinVanCott/status/1949121990066868591
    - how to use TanStack Query with all of them.

- https://github.com/osadavc/tanchat /93Star/apache2/202512/ts
  - Chat SDK is a free, open-source template built with TanStack Start and the AI SDK that helps you quickly build powerful chatbot applications.
  - a fork of `vercel/ai-chatbot`, adapted for the TanStack ecosystem.

- https://github.com/rs-4/tanstack-ai-demo /278Star/MIT/202512/ts
  - A modern AI chat template built with TanStack Start, featuring multi-model support, real-time streaming, and a clean, responsive UI.
  - Multi-Provider AI - OpenAI, Anthropic, Google Gemini, Ollama (local)
  - Persistent History - Chat history stored in PostgreSQL
  - TanStack Start, TanStack Router, TanStack Query, React, Tailwind CSS, shadcn/ui
  - TanStack AI, Drizzle ORM, PostgreSQL
  - Bun (recommended) or Node.js

- https://github.com/netlify-templates/tanstack-template /MIT/202512/ts
  - https://tanstack-starter.netlify.app/
  - A modern chat template built with TanStack Router, Claude AI, Sentry, and Convex integrations, featuring a clean and responsive interface.
  - State Management: TanStack Store
  - Database: Convex (optional)
  - 👀 Build Tool: Vite 6 with Vinxi

- https://github.com/taro-28/tanstack-table-search-params /202511/ts
  - React Hook for syncing TanStack Table state with URL search params.
  - 支持nextjs, tanstack-router, react-router

- https://github.com/sidiDev/next-to-tanstack /202512/ts
  - A CLI to migrate Next.js 14 or 15 projects to TanStack Start
  - Swaps Next.js dependencies for TanStack Router and Start
  - Converts layout.tsx → __root.tsx
  - Converts page.tsx → index.tsx
  - Coming soon:
    - Support for additional pages and nested routes
    - Dynamic routes

- https://github.com/PaulBratslavsky/strapi-tanstack-start-starter /MIT/202512/ts
  - A full-stack starter project combining Strapi headless CMS with TanStack Start for building modern web applications.
  - User authentication (local signup/signin + GitHub OAuth)
  - User authentication with JWT
  - Session management with HTTP-only cookies
  - [Hey I built this project with TanStack Start and Strapi and looking for some feedback : r/Strapi _202511](https://www.reddit.com/r/Strapi/comments/1ow6ozk/hey_i_built_this_project_with_tanstack_start_and/)
# starter/templates
- https://github.com/TanStack/create-tsrouter-app /1.1kStar/MIT/202512/ts
  - drop-in replacement for create-react-app that builds TanStack Router based SPA applications

- https://github.com/agustinusnathaniel/vite-react-tailwind-starter /MIT/202512/ts
  - http://vite-react-tailwind-starter.sznm.dev/
  - template to initialize TanStack router app with TailwindCSS setup
  - https://github.com/lightsound/tanstack-start-start
    - minimal starter template for TanStack Start

- https://github.com/instructa/constructa-starter-min /MIT/202511/ts
  - https://constructa-starter-min.vercel.app/
  - Minimal Tanstack Starter with shadcn, tailwind v4

- https://github.com/Abhirup-99/tanstack-demo /202509/ts
  - https://abhirup-99.github.io/tanstack-demo/
  - a minimal setup to get React working in Vite with HMR and some ESLint rules.

- https://github.com/backpine/tanstack-start-on-cloudflare /202512/ts
  - full-stack React application built with TanStack Start and deployed on Cloudflare Workers. 
  - This template showcases server functions, middleware, type-safe data fetching, and seamless integration with Cloudflare's edge computing platform
  - https://github.com/backpine/tanstack-start-beta-on-cloudflare

- https://github.com/laoer536/vite-react-TypeScript-TanStack-zustand-Eslint-prettier-template /MIT/202509/ts/inactive
  - https://laoer536.github.io/vite-react-TypeScript-TanStack-zustand-Eslint-prettier-template/
  - simple generic example template. And it includes front-end Docker deployment capability.

- https://github.com/Vijayabaskar56/tanstack-start-faster /202512/ts
  - https://tanstack-faster.tancn.dev/
  - performant e-commerce template using TanStack and Cloudflare, inspired by NextFaster
  - showcases the power of TanStack Router, Query, and Start deployed on Cloudflare's edge platform.
  - https://github.com/ethanniser/NextFaster /MIT/202512/ts
    - https://next-faster.vercel.app/
    - performant e-commerce template using Next.js

- https://github.com/daveyplate/better-auth-tanstack-starter /202512/ts
  - https://tanstack.better-auth-starter.com/
  - Better Auth TanStack starter template with PostgreSQL, Drizzle, shadcn/ui and TanStack Query
  - https://github.com/daveyplate/better-auth-tanstack /MIT/202505/ts
    - Tanstack Query hooks for Better Auth.
  - https://github.com/TheOrcDev/tanstack-start-better-auth-starter
    - TanStack Start Better Auth playground

- https://github.com/dotnize/react-tanstarter /897Star/unlic/202512/ts
  - https://tanstarter.nize.ph/
  - minimal TanStack Start template with Better Auth, Drizzle ORM, shadcn/ui
  - React 19 + React Compiler
  - TanStack Start + Router + Query
  - Drizzle ORM + PostgreSQL
  - Tailwind CSS + shadcn/ui

- https://github.com/jackytea/tanstack-starter /AGPL/202512/ts
  - https://tanstack-starting.vercel.app/
  - Full-stack starter template for tanstack-start, batteries included.
  - Inspired by dotnize/react-tanstarter.
  - nitro + better-auth + i18next
- https://github.com/vijaysingh2219/build-elevate
  - Turborepo template with Next.js, TypeScript, shadcn/ui, Tailwind CSS, Better-Auth, and TanStack Query.

- https://github.com/bskimball/tanstack-hono /MIT/202512/ts
  - A simple example of using Tanstack Router SSR with Hono in a monolith
  - full-stack React application template combining TanStack Router with Hono for server-side rendering

- https://github.com/paceui/saaskit-starter /NCLic/202512/ts  
  - https://saaskit.paceui.com/
  - Launch your next SaaS idea faster with power that scales

- https://github.com/JuanPabloGilA/hono-react-boilerplate /MIT/202509/ts
  - a boilerplate for react, postgres, hono, drizzle, ai, better-auth, tanstack-query, tanstack-router, shadcn and tailwind
- https://github.com/Kroro1208/tanstack-hono-start
  - modern fullstack applications with TanStack Router, Hono, and AI

- https://github.com/jellekuipers/kolm-start-admin /MIT/202512/ts
  - A TanStack Start + better-auth admin starter with Prisma ORM, React Aria, Tailwind, i18next.

- https://github.com/thecodingmontana/tauri-tanstarter /202512/ts
  - boilerplate for building native desktop applications with Tauri, React, TanStack Router

- https://github.com/CarterPerez-dev/fullstack-template /41Star/MIT/202512/python/ts
  - Full Stack template for FastAPI, React 19 TypeScript, SCSS, Tanstack Query, Zustand, Nginx, Docker
# examples
- https://github.com/Kiranism/tanstack-start-dashboard /MIT/202512/ts
  - https://dub.sh/tanstack-start-dashboard
  - Admin Dashboard Starter with Tanstack Start + Shadcn Ui
  - This template uses an older version with Vinxi, and I’m working on updating it to the Vite version.

- https://github.com/kurochenko/tanstack-start-breadcrumbs-example /202512/ts
  - https://tanstack-start-breadcrumbs-example.netlify.app/
  - A demonstration of how to implement dynamic breadcrumbs in TanStack Start that automatically update after mutations using router.invalidate().
  - Server-Side Rendering: Organizations and employees are loaded via server functions
  - Dynamic Breadcrumbs: Breadcrumbs are prerendered on the server and update reactively on the client
  - Real-time Updates: Edit organization/employee names and watch the breadcrumbs update instantly
  - File-based Routing: Uses TanStack Router's file-based routing system
  - https://x.com/kurochenko/status/2000643718215303344
    - A few months back, I shared how to implement dynamic breadcrumbs in TanStack Router. It worked well for client-side routing, so I ported the example to TanStack Start to add proper SSR support
    - This is super similar to what I built back before devinxi but way cleaner. 
  - https://github.com/kurochenko/tanstack-router-breadcrumbs-example /202412/ts
    - demonstrates how to implement dynamic breadcrumbs in a React application using TanStack Router 

- https://github.com/Vijayabaskar56/tancn /MIT/202512/ts
  - https://tancn.dev/
  - powerful form and table builder application built with TanStack technologies. 
  - Create dynamic, type-safe forms and performant, customizable tables with a drag-and-drop interface, real-time preview, and automatic code generation.
  - Seamlessly integrated with ShadCN UI components

- https://github.com/Balastrong/confhub /202512/ts
  - https://confhub.tech/
  - Discover the best tech conferences, meetups, and workshops happening around the world.
  - 典型的 list-item 视图

- https://github.com/murabcd/docufy /202512/ts
  - https://docufy-oss.vercel.app/
  - Notion-like Platform Built with TanStack Start, TanStack AI and Convex
  - Tiptap v3
  - Collaborative editing with ProseMirror Sync from Convex

- https://github.com/blinkdisk/blinkdisk /FSL/202512/ts
  - https://blinkdisk.com/
  - Modern backups for absolutely everyone.
  - End-to-End Encrypted: All backups are encrypted before they ever leave your device.
  - macOS, Windows, or Linux

- https://github.com/notKamui/miniverso /MIT/202512/ts
  - Self-hostable grouping of mini web applications for everyday use
  - uses TanStack Router. The initial setup is a file based router
  - State Management: TanStack Store provides a great starting point 
# utils
- https://github.com/morinokami/tanstack-meta /MIT/202512/ts
  - A small library that helps you manage document heads type-safely in TanStack Router/Start
  - A small library that transforms structured, Next.js Metadata-like objects into metadata compatible with TanStack Router/Start, helping you manage document heads type-safely.
  - enables you to manage metadata as more structured objects and provides type-safe autocompletion.

- https://github.com/yornaath/batshit /MIT/202512/ts
  - https://batshit-example.vercel.app/
  - A batch manager that will deduplicate and batch requests for a certain data type made within a window. Useful to batch requests made from multiple react components that uses react-query

- https://github.com/hey-api/openapi-ts /3.8kStar/MIT/202512/ts
  - https://heyapi.dev/
  - The OpenAPI to TypeScript code generator used by Vercel, OpenCode, and PayPal.
  - Generate production-ready SDKs, Zod schemas, TanStack Query hooks, or choose from 20+ other plugins.
  - accepts any OpenAPI specification
  - core plugins for SDKs, types, and schemas
  - HTTP clients for Fetch API, Angular, Axios, Next.js, Nuxt, and more
  - 20+ plugins to reduce third-party boilerplate
  - sync with Hey API Registry for spec management
  - https://github.com/7nohe/openapi-react-query-codegen
    - OpenAPI React Query Codegen is a code generator for creating React Query (also known as TanStack Query) hooks based on your OpenAPI schema.
  - https://github.com/astahmer/typed-openapi
    - Generate a headless Typescript API client from an OpenAPI spec - optionally with a @tanstack/react-query client using queryOptions
  - https://github.com/rametta/rapini
    - OpenAPI to React Query (or SWR) & Axios
  - https://github.com/OpenAPI-Qraft/openapi-qraft
    - Full TanStack Query power in type-safe OpenAPI hooks for React

- https://github.com/Hugo-Dz/exe /474Star/MIT/202512/ts
  - https://jesterkit.com/exe
  - A build tool to distribute your full-stack web app as a single executable binary with zero runtime dependencies.
  - Unlike static builds that strip away server capabilities, EXE preserves all server-side features of your full stack framework: SSR, API endpoints, server middleware, server-side authentication, etc.
  - Single binary, no runtime dependencies.
  - A full-stack SvelteKit web app tilemap engine compiled with EXE. Running locally.
  - Nuxt and TanStack are also supported but experimental.
  - [Tanstack build error ](https://github.com/Hugo-Dz/exe/issues/14)
    - install via package.json overrides
  - [Feature request: support for webview/arbitrary code in server ](https://github.com/Hugo-Dz/exe/issues/15)
    - I think EXE is not really the right path to ship desktop apps. It's meant for server self-hosting and serving. And while one might use compiled apps locally, it's not the it's main purpose.
    - I'd recommend using Tauri for anything desktop apps, I'm using it for Sprite Fusion and it works super well.
  - [Question about the project _202509](https://github.com/Hugo-Dz/exe/issues/3)
    - Why the executable is too large (arround 106 MB for a small project)
    - It indeed packs the Bun runtime so regarding the platform, the size of the executable is between 60 and 100 MB. I'm working on something to divide its size by 2 with compression, but at runtime, the decompressed binary will be loaded in memory anyway.

- https://github.com/connectrpc/connect-query-es /apache2/202512/ts
  - https://connectrpc.com/docs/web/query/getting-started
  - TypeScript-first expansion pack for TanStack Query that gives you Protobuf superpowers.
  - wrapper around TanStack Query (react-query), written in TypeScript and thoroughly tested. It enables effortless communication with servers that speak the Connect Protocol.
  - [Connect Protocol Reference | Connect](https://connectrpc.com/docs/protocol/)
    - This document specifies the Connect protocol for making RPCs over HTTP. 
    - Remain conceptually close to gRPC's HTTP/2 protocol, so Connect implementations can support both protocols.
    - When used with Protocol Buffer schemas, the Connect protocol supports unary, client streaming, server streaming, and bidirectional streaming RPCs, with either binary Protobuf or JSON payloads.
    - The protocol doesn't use HTTP trailers at all, so it works with any networking infrastructure.

- https://github.com/hsuanyi-chou/react-page-tracker /MIT/202512/ts
  - https://react-page-tracker.typeart.cc/
  - zero-dependency library providing accurate navigation tracking, fixed document.referrer value, and complete history support for React frameworks. 
  - Fully compatible with Next.js, Remix, TanStack Query, and React Router.
  - Identifies whether the user navigated to the page via browser back/forward buttons or by clicking a link
  - Offers a complete history browsing record.
# integrations

# ai

# query
- https://github.com/mugglim/build-your-own-tanstack-query /202506/ts/inactive
  - https://mugglim.github.io/build-your-own-tanstack-query
  - Build your own TanStack Query and useQuery hook

- https://github.com/devlinduldulao/zustand-immer-react-query-course /MIT/202506/ts/inactive
  - State management using Zustand, immer, and Tanstack Query

- https://github.com/instructure/idb-cache /202505/ts/inactive
  - IndexedDB-based caching library with encryption and chunked storage, designed for performance and security. Implements `AsyncStorage` interface.
  - Web Worker: Offloads encryption and decryption tasks to prevent blocking the main thread.
  - Chunking: Efficiently handles large data by splitting it into chunks.
  - Garbage collection: Expires and cleans up outdated cache entries.
  - Task processing: Uses parallelism and queue to mitigate crypto/CPU overload.
# db/sync 
- https://github.com/rocicorp/ztunes /202512/ts
  - https://ztunes.rocicorp.dev/
  - An ecommerce store built with Zero, TanStack, Drizzle, and PlanetScale for Postgres.
  - A sync-based ecommerce app with 88k artists and 200k albums from the 1990's.

- https://github.com/electric-sql/electric/tree/main/examples/tanstack-db-web-starter
  - TanStack Start / DB + Electric app
  - This starter implements a secure authentication pattern for Electric sync.
  - https://github.com/mrwade/tanstack-db-electric-sql-demo
    - Debt Payoff Calculator - using TanStack DB, Electric SQL, Better Auth, TanStack Start, Postgres, Docker Compose

- https://github.com/get-convex/convex-saas /MIT/202408/ts/inactive
  - https://convex-saas.netlify.app/
  - A production-ready Convex Stack for your next SaaS application with Convex Auth, Stripe, TanStack, Resend, Tailwindcss, and shadcn.
  - https://github.com/get-convex/convex-tanstack-start
  - https://github.com/jherr/convex-ts-auth
    - Auth demo on Convex + TanStack Start

- https://github.com/cellajs/cella /442Star/MIT/202512/ts
  - https://cellajs.com/
  - Template to build web apps with sync engine and offline support using pg, node, hono, drizzle, react, electric-sync, tanstack.

- https://github.com/doeixd/triplit-tanstackdb /MIT/202511/ts
  - Triplit Collection for TanStack DB
  - real-time collection for TanStack DB powered by the Triplit sync engine. 
  - This library provides the bridge to connect Triplit's real-time, offline-first power with the unified, reactive query engine of TanStack DB.

- https://github.com/typeonce-dev/sync-engine-web /202503/ts/inactive
  - A Sync Engine for the web: React (TanStack Router), Web Workers, Effect, Loro

- https://github.com/andrelandgraf/contacts-app-tanstack-db-demo /202508/ts/inactive
  - https://contacts-app-tanstack-db-demo.vercel.app/
  - A demo app using TanStack DB for real-time updates and end-to-end reactivity.
  - a simple demo application showcasing TanStack DB with ElectricSQL and a Neon Postgres database
  - a Next.js project, deployed on Vercel. However, the same sync code would work also with TanStack Start, Remix, and React Router.

- https://github.com/HimanshuKumarDutt094/tanstack-dexie-db-collection 
  - Dexiejs collection (indexDB) for tanstackDB

- https://github.com/fulopkovacs/trytanstackdb.com /202512/ts
  - https://trytanstackdb.com/
  - An interactive guide for taking the first steps with @tanstack/tanstack-db by fuko.
# router
- https://github.com/Balastrong/tanstack-router-demo /202512/ts
  - TanStack Router Tutorial (code for each chapter is on its own branch)
# start

# virtual
- https://github.com/niikeec/virtual-grid /202411/ts/inactive
  - Simplified virtualization using @tanstack/virtual.
# more
