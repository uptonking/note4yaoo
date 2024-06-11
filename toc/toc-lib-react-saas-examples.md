---
title: toc-lib-react-saas-examples
tags: [examples, react, saas, toc]
created: 2022-08-13T06:59:34.253Z
modified: 2022-08-13T06:59:54.741Z
---

# toc-lib-react-saas-examples

# guide
- 经典示例
  - todo-mvc
  - realworld
  - bookshelf
# popular
- react-admin /21.1kStar/MIT/202212/ts
  - https://github.com/marmelab/react-admin
  - https://marmelab.com/react-admin-demo/
  - A frontend Framework for building data-driven applications on top of REST/GraphQL APIs, React and Material Design.
  - core依赖react-query.v3、react-hook-form
  - 提供了权限管理
  - Backend Agnostic: Connects to any API (REST or GraphQL)
  - React-admin uses an adapter approach, with a concept called Data Providers.
  - designed as loosely coupled React components and hooks exposing reusable controller logic. It is very easy to replace any part of react-admin with your own
  - 🍴 forks
  - https://github.com/ITopGun/B2BAdmin-React

- https://github.com/plantain-00/protocol-first-design-demo
  - API 协议优先，相关数据只需要相对集中地、相对方便地定义一次，其它信息由此派生或生成出来
  - graphql 的一个特点是，用户可以控制需要返回哪些字段，而 RESTful API 一般默认不会实现这个。
  - 这里的实现，不像 graphql 那样需要列出所有需要的字段，而是默认返回所有字段，根据参数中的 ignoredFields，把不需要的字段排除掉。
- https://github.com/plantain-00/protocol-based-web-framework
  - A protocol and code generation based web framework.
  - db支持sqlite、postgres、mongodb

- https://github.com/pure-admin/pure-admin-backend /ts/echarts
  - pure-admin官方后端
  - 依赖express、mysql，未使用orm
  - https://github.com/pure-admin/pure-admin-thin
    - 基于 vue-pure-admin 官方精简版
    - 提供了权限管理
  - https://github.com/pure-admin/vue-pure-admin
    - Vue3+Vite4+Element-Plus+TypeScript编写的一款后台管理系统，兼容移动端

- https://github.com/winwiz1/crisp-react
  - Crisp React can optionally split a monolithic React app into multiple Single Page Applications (SPAs) and selectively prerender the landing/index page of any SPA at the build time.
  - Helps to split a monolithic React app into multiple SPAs and avoid vendor lock-in.
  - in each SPA the routing is managed by a separate instance of React Router 
  - By default SSR is enabled for the first SPA and disabled for the second SPA.
  - On the contrary to popular belief that SEO requires SSR, this solution innovatively demonstrates how to get all SPA pages indexed by Google and specific
  - [How to achieve SEO for React SPA without SSR or prerendering](https://stackoverflow.com/questions/70390808/how-to-achieve-seo-for-react-spa-without-ssr-or-prerendering-and-preferably-kee)
  - [Single Page Application: Dispelling SEO Myths | HackerNoon](https://hackernoon.com/single-page-application-dispelling-seo-myths)

- https://github.com/horacioh/multi-tenancy-react-example
  - Multi tenant architecture example

- async-labs/saas /3.2kStar/MIT/202209/ts/inactive
  - https://github.com/async-labs/saas
  - https://saas-app.async-await.com/
  - Open source web app that saves you many days of work when building your own SaaS product.
  - 前端依赖mui5, Next, MobX, 
  - 后端依赖Express, socket.io, Mongoose, MongoDB
  - https://github.com/async-labs/async
    - sync was built from our popular open source saas
    -  (1) Chat for real-time, synchronous communication, (2) Discussions for asynchronous communication,

- saas-ui /436Star/MIT/202212/ts
  - https://github.com/saas-js/saas-ui
  - https://saas-ui.dev/docs/pro/overview
  - The React component library for startups, built with Chakra UI.

- https://github.com/paralect/ship /202212/ts/c#
  - Ship is a toolkit for makers to ship better products faster
  - Full-stack boilerplate tested on production projects 

- https://github.com/adarshaacharya/MentorLabs /ts
  - MentorLabs is a a WebRTC based video conferencing app.
  - 前端依赖 redux/toolkit
  - 后端依赖 express、typeorm
# react-starter
- https://github.com/alan2207/bulletproof-react /star多
  - A simple, scalable, and powerful architecture for building production ready React applications.
  - It is an opinionated guide that shows how to do some things in a certain way. 
  - You are not forced to do everything exactly as it is shown here

- https://github.com/habx/lib-ts-template
  - Template for client library in typescript
- https://github.com/KaiHotz/react-rollup-boilerplate
  - Boilerplate for creating React component libraries, bundled with Rollup.js to ES6 Modules, React Styleguidist, Typescript
- https://github.com/matthewdowns/react-component-library-boilerplate
  - Optimized template repository for React component libraries.

- https://github.com/nanlabs/react-webpack-boilerplate
  - This project was generated using create-react-webpack-app.
  - https://github.com/Create-Node-App/create-react-webpack-app

- https://github.com/GR34SE/react-typescript-starter
  - Minimalist React 18 starter template with TypeScript atom_symbol without usage of create-react-app.
- https://github.com/akunzai/react-boilerplate
  - React Boilerplate to kick-start new project

- https://github.com/three11/react-template-ts
  - Opinionated React starter template using TypeScript, Redux, React Router, Redux Saga, SCSS, PostCSS and more, offering PWA and offline capabilities and many more.
- https://github.com/monstar-lab-oss/reactjs-boilerplate
  - A starter kit for easily customized when you start developing with React
  - 各项可选

- https://github.com/alan2207/bulletproof-react
  - 依赖 react-query.v3, headless-ui, zustand

- https://github.com/santospatrick/nextjs-boilerplate-advanced
  - https://sample-nextjs-app.santospatrick.com/
  - Next.js boilerplate made with Chakra-UI + Typescript + React-table + React-hook-form
  - 依赖 react-table.v7、react-query

- https://github.com/ThaddeusJiang/react-app-starter
  - 依赖 nextjs、tailwindcss、react-hook-form、react-query、react-table、storybook、react-testing、mock-service-worker
- https://github.com/gabriel-hahn/react-next-boilerplate
  - A NextJS boilerplate with RTL, Styled Components, Storybook, TypeScript, Husky, Babel, ESLint and Next PWA 
- https://github.com/iamdevmarcos/my-boilerplate
  - project starter to work with TypeScript, React, NextJS and Styled Components
- https://github.com/Kamahl19/react-starter
  - Full-featured typescript starter for React application
  - recoil, recoil-persist

- https://github.com/SeanCassiere/nextshop-mern
  - following Brad Traversy's MERN stack online course. udemy

- https://github.com/wmartzh/r-rubi-react
  - https://github.com/wmartzh/r-rubi-nest
  - 前端js、后端ts

- https://github.com/DimiMikadze/fest
  - SaaS boilerplate built with Node.js & React.
  - 依赖nestjs、prisma、nextjs、mui
  - User authentication and authorization with email verification and password reset.
  - Organizations management system.
  - Secure API endpoints and Front-end routes with role-based authorization.

- https://github.com/cheeterLee/messenger
  - https://messenger-beta-drab.vercel.app/
  - Fullstack real time chatting app.

- https://github.com/oedotme/full-stack-typescript-with-turborepo-demo
  - Full stack TypeScript with Turborepo demo
# nextjs
- https://github.com/shadcn/ui
  - https://ui.shadcn.com/
  - Beautifully designed components built with Radix UI and Tailwind CSS.

- https://github.com/steven-tey/precedent
  - https://precedent.dev/
  - An opinionated collection of components, hooks, and utilities for your Next.js project.
  - Typescript-first ORM for Node.js
# crud
- https://github.com/taniarascia/react-hooks /js
  - https://taniarascia.github.io/react-hooks/
  - [Build a CRUD App in React with Hooks](https://www.taniarascia.com/crud-app-in-react-with-hooks/)
  - a simple CRUD app that can add, update, or delete users.

- https://github.com/bezkoder/react-hooks-crud-web-api
  - 教程示例丰富
  - [React Hooks CRUD example with Axios and Web API](https://www.bezkoder.com/react-hooks-crud-axios-api/)
  - [build a server api: Express, Sequelize & PostgreSQL](https://www.bezkoder.com/node-express-sequelize-postgresql/)
# fullstack-api/mern
- https://github.com/gilamran/fullstack-typescript
  - FullStack React with TypeScript starter kit.
  - 依赖react-router.v6、mui5
  - 未使用状态管理，未使用数据库，实现简单
  - Client and server can share code (And types)
  - The client is bundled using Webpack
  - The server is emitted by TypeScript because node now supports es6.

- https://github.com/biantris/asktris
  - Fullstack Playground
  - 依赖koa、mongoose、jwt、react

- https://github.com/shanhuiyang/TypeScript-MERN-Starter
  - Build a real fullstack app (backend+website+mobile) in 100% Typescript
  - mongodb+oauth2+redux
  - Android/iOS client is created from Expo
- https://github.com/afteracademy/nodejs-backend-architecture-typescript
  - build a backend server for Blogging platform like Medium, FreeCodeCamp
  - 依赖express、mongoose
  - Open-Source Project By AfterAcademy
- https://github.com/sidhantpanda/docker-express-typescript-boilerplate
  - A dockerized TypeScript-Express App boilerplate with MongoDB and Github Actions

- https://github.com/GeekyAnts/express-typescript
  - Express + TypeScript + Boilerplate for Web / API App
  - For Database - Repo contains the use of Mongoose 
  - For Cache - Repo contains the use of memory-cache 
  - For Strategies Auth - Repo contains the use of the Passport.js
  - For views - Repo contains the use of PUG template engine.
  - For background queues - Repo contains the use of Kue. 

- https://github.com/flaviuse/mern-authentication
  - authentication boilerplate: password reset, email verification, server sessions, redux, typescripts, hooks and docker for dev and prod.
- https://github.com/rooneyrulz/simple-auth-app
  - Simple role-based authentication app with MERN stack for Ecologital.
  - 后端依赖 express, mongoose

- https://github.com/sjohnatas7/Articles-Management
  - a full-stack web application for articles management
  - Frontend: React, Redux, HTML, CSS, JavaScript
  - Backend: Node.js, Express.js, MongoDB, PostgreSQL
  - Authentication and authorization: Passport.js

- https://github.com/nagytommy76/ComputerStoreMERN
  - learn the fundamentals of Node.js (Express.js), React.js, and a NoSQL database like MongoDB.

- https://github.com/ivanlori/Fullstacco
  - Express.js/Node.js MongoDB React.js Typescript Redux.js React testing library

- https://github.com/hicmtrex/TypeShop-Frontend
  - https://type-shop.vercel.app/
  - Mern Stack Ecommerce with TypeScript
  - React.js React Bootstrap Redux Toolkit

- https://github.com/Seikho/fullstack-starter
  - opinionated full-stack starter: TypeScript, Node. JS, Express, CQRS + Event Sourcing, React, and Redux
  - 依赖 zustand， mongodb

- https://github.com/gadingnst/fullstack-next-template
  - Next.js Boilerplate with TypeScript, MongoDB & MVC architecture
- https://github.com/olafsulich/fullstack-nextjs-ecommerce
  - Fullstack Next.js E-Commerce made with NextAuth + Prisma, Docker + TypeScript + React Query + Stripe + Tailwind Sentry and much more 
- https://github.com/alexeagleson/nextjs-fullstack-app-template
  - A fullstack template for a NextJs App

- https://github.com/bradtraversy/mern_shopping_list
  - Shopping List built with MERN and Redux
- https://github.com/viclafouch/meme-studio
  - website building in React/Express for creating and sharing "internet memes"
  - ReactJS - Framework JS React-Helmet - SEO Immer - Immutability library React-i18next - Internationalization ExpressJS - Server side Sequelize - Database
- https://github.com/vidarshan/mern-gadget-shop
  - An ecommerce web app created with React and Node.
# saas-apps

## blog

- https://github.com/planetscale/beam
  - Beam is a simple tool that allows members to write posts to share across your organization. Think of it like a lightweight internal blog.
  - 依赖trpc、prisma、next、textarea-markdown-editor

- https://github.com/KevinSilvester/mern-movie
  - A fullstack movie website

## ecommerce

- https://github.com/saddamarbaa/Ecommerce-website-next.js-typeScript
  - Next Js + TypeScript + Node Js + Express + MongoDB + Material-UI + Redux + Tailwind-CSS
  - https://github.com/saddamarbaa/node-express-typescript-ecommerce-rest-api
  - REST API built with | Nodejs + Express + Mongodb 

- https://github.com/brandnewjinah/ecommerce
  - my attempt to create a full stack e-commerce platform.

- https://github.com/ElieB77/audiophile
  - my solution to the Audiophile e-commerce website challenge created by Frontend Mentor. 
  - using ReactJS, Typescript and NextJS on the client-side, and Node, Typescript and Express on the server-side with MySQL
- https://github.com/jrussbautista/dress-shop
  - full stack e-commerce website for clothing store.
# react-examples
- https://github.com/algolia/algolia-react-boilerplate
  - customizable boilerplate, made with ReactInstantSearchHooks and with many Algolia's features.

- https://github.com/code-soham/React-Form-Builder
  - Form Builder in MERN
  - https://www.youtube.com/watch?v=EzlqD5P3DdI

- https://github.com/shriproperty/client
  - About Website for purchasing, selling, renting real estate

- https://github.com/pankod/superplate
  - A well-structured production-ready frontend boilerplate with Typescript, Jest, testing-library, styled-component, Sass, Css, .env, Fetch, Axios, Reverse Proxy, Bundle Analyzer and 30+ plugins. 
  - For now, it only creates projects for React and Next.js.
  - Superplate lets you start rock-solid, production-ready React and Next. JS projects just in seconds. 
  - The command-line interface guides the user through setup and no additional build configurations are required.
# onboarding-guide-tour
- https://github.com/plantain-00/tour-component
  - A vuejs and reactjs tour component.
  - highlight target element
  - scroll to target
# more-react-examples
