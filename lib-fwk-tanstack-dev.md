---
title: lib-fwk-tanstack-dev
tags: [dev-xp, meta-framework, nextjs, tanstack]
created: 2025-12-31T15:42:53.774Z
modified: 2025-12-31T15:43:19.960Z
---

# lib-fwk-tanstack-dev

# guide

- tanstack 大量库的类型都采用全局 declare module 的设计, 不方便实现多实例，包括table/router
# router
- resources
  - 🆚 [Comparison | TanStack Router/Start vs Next.js vs React Router/Remix](https://tanstack.com/router/latest/docs/framework/react/comparison)

- tanstack-start vs nextjs
  - History, Memory & Hash Routers
  - Typesafe Routes
  - Code-based Routes
  - Virtual/Programmatic File-based Routes
  - Custom Search Param parsing/serialization
  - ElementScroll Restoration
  - Generic RPCs
  - Route Mount/Transition/Unmount Events
  - 🐛 cons
    - Parallel Routes
    - Runtime Route Manipulation (Fog of War)
    - React Server Components

- tanstack-router vs react-router
  - SWR Loader Caching
  - Custom Search Param parsing/serialization
  - ElementScroll Restoration
  - Route Mount/Transition/Unmount Events
  - Generic RPCs
  - React Server Functions
  - 🐛 cons
    - Runtime Route Manipulation (Fog of War)

- Should I use TanStack Start or just TanStack Router?
  - 90% of any framework usually comes down to the router, and TanStack Start is no different. TanStack Start relies 100% on TanStack Router for its routing system. 
  - Full-document SSR - Server-side rendering for better performance and SEO
  - Streaming - Progressive page loading for improved user experience
  - Server Routes & API Routes - Build backend endpoints alongside your frontend
  - Server Functions - Type-safe RPCs between client and server
  - Middleware & Context - Powerful request/response handling and data injection
  - Full-Stack Bundling - Optimized builds for both client and server code
  - Universal Deployment - Deploy to any Vite-compatible hosting provider

## issues-router

## dev-xp

- react-router 容易迁移到 code-based router
# start

## issues-start

## dev-xp

# query

## issues-query

## dev-xp

# db

## issues-db

## dev-xp

# virtual

## issues-virtual

## dev-xp
