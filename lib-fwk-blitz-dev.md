---
title: lib-fwk-blitz-dev
tags: [blitz, fwk, lib, nextjs, node, react-query]
created: '2021-07-28T18:58:44.922Z'
modified: '2021-07-28T19:00:16.604Z'
---

# lib-fwk-blitz-dev

# guide
- Foundational Principles
  - API Not Required
  - Fullstack & Monolithic
  - Convention over Configuration
  - Loose Opinions
  - Easy to Start, Easy to Scale
  - Stability
  - Community over Code
  - api风格是functional，很少使用class/this

- Why use Blitz instead of Next.js?
  - Fullstack instead of Frontend
  - Data Layer
  - Built-in Authentication
  - Conventions
  - Code Scaffolding
  - Recipes with mdx and react components
  - New App Development
  - Relaxed Restrictions
  - Route Manifest
# docs

> The Fullstack React Framework with "Zero-API" Data Layer — Built on Next.js — Inspired by Ruby on Rails

## overview

- “Zero-API” data layer lets you import server code directly into your React components 
  - instead of having to manually add API endpoints and do client-side fetching and caching.

- **Features:**
  - Built on Next.js
  - Don't have to build an API for client-side rendering
  - Client-side rendering, Server-side rendering, and fully static pages all in the same app
  - Full Typescript support with static, end-to-end typing (no code generation step needed like with GraphQL)
  - Database/ORM agnostic, but Prisma 2 is default
  - CLI with code scaffolding, Rails-style console REPL, etc
  - GraphQL Ready
  - Deploy serverless or serverful
  - Highly secure authentication 
  - Authorization you can use on both server and client
  - Recipes for easily adding libraries like Tailwind, CSS-in-JS, etc.
  - React Concurrent Mode enabled
- **Other key features coming:**
  - Model validation you can use on both server and client
  - React native support
  - GUI so you don't have to use the CLI
