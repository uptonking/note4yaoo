---
title: toc-lib-editor-builder-dashboard-react-admin
tags: [crud, dashboard, lowcode, react-admin]
created: 2023-02-17T21:47:40.266Z
modified: 2023-02-17T21:48:01.840Z
---

# toc-lib-editor-builder-dashboard-react-admin

# guide

# react-admin
- react-admin /21.1kStar/MIT/202212/ts
  - https://github.com/marmelab/react-admin
  - https://marmelab.com/react-admin-demo/
  - A frontend Framework for building data-driven applications on top of REST/GraphQL APIs, React and Material Design.
  - core依赖react-query.v3、react-hook-form
  - 默认帐号是 login/password
  - Backend Agnostic: Connects to any API (REST or GraphQL)
  - React-admin uses an adapter approach, with a concept called Data Providers.
  - designed as loosely coupled React components and hooks exposing reusable controller logic. It is very easy to replace any part of react-admin with your own
  - [Who is using #react-admin? · Issue](https://github.com/marmelab/react-admin/issues/4027)
  - [React-admin - Supported Data Provider Backends](https://marmelab.com/react-admin/DataProviderList.html)

- https://github.com/BlackBoxVision/react-admin-extensions
  - Packages for improving your development workflow with react admin
  - 已提供: rbac, layout
  - wip: search

- https://github.com/NathanAdhitya/express-mongoose-ra-json-server /7Star/MIT/202209/ts
  - creates express.js routes from a mongoose model for ra-data-json-server
  - https://github.com/NathanAdhitya/express-mongoose-ra-json-server-demo

- https://github.com/raphiniert-com/ra-data-postgrest /75Star/MIT/202211/ts
  - PostgREST Data Provider for react-admin
  - react admin client for postgREST

- https://github.com/lalalilo/express-crud-router /113Star/MIT/202201/ts/无db
  - Expose resource CRUD routes for Express & Sequelize. 
  - Compatible with React Admin Simple Rest Data Provider. 
  - The lib is ORM agnostic
  - https://github.com/lalalilo/express-crud-router-sequelize-v6-connector

- https://github.com/marmelab/ra-sqlite-dataprovider
  - here is a POC to generate a react-admin administration not relying on an API but directly on a SQLite database hosted on a static server (in this case the Github pages server).

- https://github.com/slax57/admin-e-commerce-demo
  - Redo the React Admin E-Commerce Demo App as training

- https://github.com/prowebdev119/react-admin
  - Open sourced and maintained by marmelab.
# api/server
- https://github.com/henvo/ra-jsonapi-client
  - A JSONAPI compatible data provider for react-admin.

- https://github.com/tykoth/ra-data-dexie
  - Experimental React-Admin data provider using Dexie (IndexedDB)

- https://github.com/codeledge/ra-data-simple-prisma
  - Prisma tools and Data Adapter for React Admin

- https://github.com/LoicMahieu/react-admin-git-provider
  - Gitlab data provider for React Admin

- api-more
  - https://github.com/FusionWorks/react-admin-nestjsx-crud-dataprovider /nestjs
  - https://github.com/panter/ra-data-prisma /GraphQL
  - https://github.com/marmelab/ra-data-google-sheets
# utils
- https://github.com/Nooul/ra-component-factory
  - provides a centralized way to easily configure visibility and permissions related business logic, including access to forms/views, visibility/immutability of resource fields/inputs
# more
- https://github.com/Groopit/ra-data-odata-server
  - OData Data Provider for react-admin
