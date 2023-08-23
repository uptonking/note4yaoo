---
title: toc-lib-state-redux
tags: [redux, state, toc]
created: 2020-11-02T19:12:24.315Z
modified: 2020-11-02T19:13:04.103Z
---

# toc-lib-state-redux

# redux-popular

- https://github.com/react-dnd/react-dnd
  - core依赖redux
- https://github.com/atlassian/react-beautiful-dnd
  - Beautiful and accessible drag and drop for lists with React
  - 依赖redux、raf-schd、css-box-model
  - react-dnd does an incredible job at providing a set of drag and drop primitives
  - react-beautiful-dnd is a higher level abstraction specifically built for lists (vertical, horizontal, movement between lists, nested lists and so on).

- https://github.com/react-page/react-page
  - highly customizable content editor for the browser - based on React and Redux and written in TypeScript
  - If you are fed up with the limitations of contenteditable, you are in the right place.
- https://github.com/react-designer/react-designer
  - Editable vector graphics in your react apps

- https://github.com/schrodinger/fixed-data-table-2 /js
  - A React table component designed to allow presenting millions of rows of data.

- https://github.com/jshjohnson/Choices
  - configurable select box/text input plugin. Similar to Select2 and Selectize but without the jQuery
  - 依赖redux、fuse.js(fuzzy-search in js)

- https://github.com/microsoft/redux-dynamic-modules /202003/ts/inactive
  - aims to make Redux Reducers and middleware easy to modular-ize and add/remove dynamically.
  - In large Javascript applications, it is often desired to perform some kind of code-splitting, so that the initial script size is small. 
  - However, in Redux, you are required to define your reducers and middleware up-front; 
  - there is no good way to dynamically add/remove these constructs at runtime.
  - designed to make dynamically loading these constructs easier
# react-context-redux
- https://github.com/bergkvist/react-context-toolkit /ts
  - Toolkit for React Context API heavily inspired by @reduxjs/toolkit and react-redux.
  - It uses the React Context API instead of Redux for managing state under the hood.
  - Depends on use-context-selector to prevent unnecessary rerenders.
  - createSlice(): This is exported directly from @reduxjs/toolkit

- https://github.com/didierfranc/react-waterfall /js
  - https://github.com/didierfranc/react-waterfall-example
  - React store built on top of the new context API
  - During development redux-devtools are automatically enabled. 
  - [Replacing Redux with core React APIs | by Didier FRANC | Medium](https://medium.com/@DidierFranc/replacing-redux-with-the-new-react-context-api-8f5d01a00e8c)

- https://github.com/RichardBray/no-redux /js
  - [Replacing redux with react hooks and context (part 1)](https://medium.com/octopus-labs-london/replacing-redux-with-react-hooks-and-context-part-1-11b72ffdb533)
# redux-utils
- https://github.com/rt2zz/redux-persist
  - Persist and rehydrate a redux store.
- https://github.com/piotr-cz/redux-persist-idb-storage
  - Storage adapter to use IndexedDB via idb v3 with `redux-persist` ripped from idb v3

- https://github.com/react-stack/redux-storage
  - Persistence layer for redux with flexible backends
  - install at least one redux-storage-engine, as redux-storage is only the "management core".
  - https://github.com/michaelcontento/redux-storage /201608/js/inactive
    - Persistence layer for redux with flexible backends

- https://github.com/redux-observable/redux-observable
  - RxJS-based middleware for Redux. 
  - Compose and cancel async actions to create side effects and more.

- https://github.com/redux-offline/redux-offline
  - Build Offline-First Apps for Web and React Native
  - 🤔 没必要执着于寻找已有的offline方案，使用 persist + crdt 也可以实现协作

- https://github.com/redux-orm/redux-orm /202104/js/inactive
  - https://redux-orm.github.io/redux-orm/
  - simple and immutable ORM to manage relational data in your Redux store.
  - Redux-ORM deals with related data, structured similar to a relational database. The database in this case is a simple JavaScript object database.
  - For simple apps, writing reducers by hand is alright, but when the number of object types you have increases and you need to maintain relations between them, things get hairy. 
    - ImmutableJS goes a long way to reduce complexity in your reducers, but Redux-ORM is specialized for relational data.
  - [Call for Maintainer and Contributors](https://github.com/redux-orm/redux-orm/issues/123)
    - I've been moving away from redux to things like react-query and lost traction on redux-orm

- redux-database /18Star/MIT/202005/ts/NoDeps/inactive
  - https://github.com/nerdgeschoss/redux-database
  - https://nerdgeschoss.github.io/redux-database
  - Simple reducer based in-memory database with strong typings and immutable documents, with plugins for redux and react.
  - Client side data normalization is hard. This library helps you to organize your state in a relational way, with queries and joins as you would expect from an SQL based database. 
  - There is a storage adaper for redux or you can use it as a standalone library (redux-database has no dependencies!).

- https://github.com/msolvaag/redux-db /201902/ts/inactive
  - provides a normalized redux store and easy object management.
  - Having a normalized state is a good strategy if your data is nested in different ways. 
- https://github.com/cape-io/redux-graph /js/inactive
  - Redux Graph Database
  - basic graph database with entity and triple storage

- https://github.com/lscheibel/redux-yjs-bindings
  - https://lscheibel.github.io/redux-yjs-bindings/
  - Use Yjs to sync your Redux store with other peers!
  - small (roughly 1kB) bridge to connect Redux with a Yjs, allows you to use the synchronization features of Yjs with the data management capabilities of Redux. 
  - It works with any Redux store, whether you use Redux Toolkit or not, and even supports initial values. 
  - Values that are transmitted over the network can be any JSON serializable value, from primitives to deeply nested object structures.
  - Special thanks to Joseph Miles whose zustand-middleware-yjs library was an inspiration.
  - https://github.com/joebobmiles/zustand-middleware-yjs
    - Zustand middleware that enables sharing of state between clients via Yjs.
    - One of the difficult things about using Yjs is that it's not easily integrated with modern state management libraries in React. 
    - This middleware for Zustand solves that problem by allowing a Zustand store to be turned into a CRDT, with the store's state replicated to all peers.
    - This differs from the other Yjs and Zustand solution, `zustand-yjs` by allowing any Zustand store be turned into a CRDT. This contrasts with `zustand-yjs`'s solution, which uses a Zustand store to collect shared types and access them through special hooks.

- https://github.com/iamogbz/react-ducks
  - Implement ducks in React following the redux pattern but using React Context.
  - Uses `immer` to wrap reducers when creating, ensuring atomic state mutations.

- https://github.com/reduxjs/redux-mock-store
  - A mock store for testing Redux async action creators and middleware. T
  - this library is designed to test the action-related logic, not the reducer-related one. 
  - In other words, it does not update the Redux store. 
# redux-saas-crud
- https://github.com/Dbuggerx/react-pokeapi
  - https://dbuggerx.github.io/react-pokeapi
  - A sample of a SPA done with React, Redux-Toolkit, Typescript, Sass, CSS Grid, etc
  - Retrieves data from the Pokémon REST API; 
  - Styles created using SASS with the BEM methodology; 
  - React Router v6 to display details in a different route when an item is clicked; 
  - Tests implemented using Jest, React Testing Library and MSW; 

- https://github.com/rogerndutiye/redux-toolkit-contact-card
  - https://happy-albattani-e6d08a.netlify.app/
  - A sample React TypeScript Redux Toolkit CRUD app
- https://github.com/cmacdonnacha/awesome-address-book
  - https://cmacdonnacha.github.io/awesome-address-book/
  - a basic address book built with ReactJS, Redux Toolkit, React Router and Typescript

- https://github.com/iamyuu/shoes-commerce
  - https://shoes-commerce.vercel.app/
  - Experiment with Redux (Redux Toolkit & RTK Query)
- https://github.com/nxiiln/the-shop
  - https://nxiiln.github.io/the-shop/
  - SPA for e-commerce
  - 纯前端项目
- https://github.com/QuocDat1994/react-fashion-shop
  - http://fashion-shop.quocdat1994.surge.sh/
  - A fashion shop built with react, antd, typescript and redux-toolkits.

- https://github.com/vannizhang/react-redux-boilerplate
  - Boilerplate to start React+Redux project with TypeScript in an easier and faster way.

- https://github.com/santoshshinde2012/react-redux-typescript-boilerplate
  - Our main purpose with this Skeleton is to start frontend application with react with redux toolkit and typescript
- https://github.com/FrameMuse/react-template
  - Typescript react template with basic layouts, buttons, modules that are often used in most websites.
- https://github.com/jyoketsu/react-example
  - 使用 Vite + React + TypeScript + React-Router + Redux-Toolkit + Material-UI + react-i18next 开发。支持多语言和暗黑模式。
  - 登录用的 iframe， https://account.qingtime.cn/
- https://github.com/MajorLift/typescript-fullstack-monorepo-starter
  - React-Redux-Express-SQL monorepo boilerplate boosted with SWC and ESBuild.
  - Frontend: React, Redux Toolkit, Tailwind CSS
  - Backend: Express.js, RTK Query, PostgreSQL

- https://github.com/KASTINpl/react-next-starter
  - ReactJS + Next.js + TypeScript + Redux + MaterialUI + ESLint, Prettier + Cypress + Jest + Storybook

- https://github.com/laststance/vite-rtk-query
  - Redux Toolkit, RTK Query, eslint/prettier, jest/TS/react-testing-library/MSW, tailwindcss, GitHub Actions CI.

- https://github.com/DevlinRocha/banter
  - Banter is a feature-rich Discord clone built with React, Redux Toolkit, Next. JS, TypeScript, styled-components, Tailwind CSS, and uses Firebase to communicate with the back-end.

- https://github.com/matheuscruzhen/redux-toolkit-ts-questions-app
  - A questions app made with React Redux, Redux Toolkit and Typescript.

- https://github.com/typinghare/supervisor-backend
  - Supervisor Backend (NestJS + Moment + TypeORM + JWT)
  - https://github.com/typinghare/supervisor-frontend
    - Supervisor Frontend (React + MUI + Redux + ApexCharts + Moment + Axios + Lodash)

- https://github.com/strlrd-29/bg-react
# redux-repos
- https://github.com/rematch/rematch
  - Rematch is Redux best practices without the boilerplate.
- https://github.com/dvajs/dva
  - React and redux based, lightweight and elm-style framework.

- https://github.com/redux-form/redux-form
  - the general consensus of the community is that you should not put your form state in Redux.
  - The author of Redux Form took all of the lessons he learned about form use cases from maintaining Redux Form and built React Final Form
  - The only good reason, in the author's view, to use Redux Form is if you need really tight coupling of your form data with Redux
  - If you don't have that requirement, use React Final Form.

- https://github.com/rcdexta/react-trello
  - Pluggable components to add a Trello (like) kanban board to your application
  - 依赖redux、styled-components
- https://github.com/markusenglund/react-kanban
  - Trello-like application built with React and Redux
- https://github.com/Wolox/react-chat-widget
  - chat widget for your React App
  - 依赖redux、markdown-it
- https://github.com/gatsbyjs/gatsby
  - During Gatsby’s bootstrap & build phases, the state is stored and manipulated using the Redux library. 
  - The key purpose of using Redux in Gatsby internals is to centralize all of the state logic
- https://github.com/kineticdata/react-kinetic-lib
  - A React library for the Kinetic Platform
- https://github.com/source-academy/cadet-frontend
  - Frontend of Source Academy (React, Redux, Saga, Blueprint)
- https://github.com/bndynet/admin-template-for-react
  - Admin template for React, Redux, Redux Saga, React Router, i18n and integrated OAuth login
- https://github.com/mihailgaberov/chat
  - A React single page chat application (SPA), implementing Socket.io.
- https://github.com/nfriend/tree-online
  - 线段短横树型组件
  - An online tree-like utility for generating ASCII folder structure diagrams.
- https://github.com/jeffersonRibeiro/react-shopping-cart
  - Simple ecommerce cart application built with React Redux
- https://github.com/harryho/react-crm
  - A reusable CRM project for business based on React 16, Redux & Material-UI 4
- https://github.com/JoshuaScript/spresso-search
  - Visual metasearch engine built with TypeScript, React, Redux & Express
- https://github.com/cashapp/misk-web
  - Micro-Frontends React + Redux + Typescript Framework
- https://github.com/wix/repluggable
  - Pluggable micro frontends in React+Redux apps

- https://github.com/rgommezz/react-native-offline
  - Handful of utilities you should keep in your toolbelt to handle offline/online connectivity in React Native. 
  - It supports iOS, Android and Windows platforms.
  - There are 3 features that this library provides in order to leverage offline capabilities in your Redux store: a reducer, a middleware and an offline queue system. You can use all of them or just the ones that suits your needs.

- more-redux
  - https://github.com/swagger-api/swagger-ui
    - https://github.com/swagger-api/swagger-ui-react
  - https://github.com/boardgameio/boardgame.io
