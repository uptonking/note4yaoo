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
  - https://marmelab.com/react-admin/Demos.html
  - [demo E-commerce](https://marmelab.com/react-admin-demo/)
  - [demo CRM](https://marmelab.com/react-admin-crm/)
  - [demo HelpDesk](https://marmelab.com/react-admin-helpdesk/)
  - [demo Music Player 黑色主题](https://demo.navidrome.org/app/)
  - A frontend Framework for building data-driven applications on top of REST/GraphQL APIs, React and Material Design.
  - core依赖react-query.v3、react-hook-form
  - 默认帐号是 login/password
  - Backend Agnostic: Connects to any API (REST or GraphQL)
  - React-admin uses an adapter approach, with a concept called Data Providers.
  - designed as loosely coupled React components and hooks exposing reusable controller logic. It is very easy to replace any part of react-admin with your own
  - [Who is using #react-admin? · Issue](https://github.com/marmelab/react-admin/issues/4027)
  - [React-admin - Supported Data Provider Backends](https://marmelab.com/react-admin/DataProviderList.html)
  - [Using React-Admin With Your Favorite UI Library](https://marmelab.com/blog/2023/11/28/using-react-admin-with-your-favorite-ui-library.html)
    - React-admin relies on Material UI for its user interface by default. 
    - However, you can use react-admin with any UI library
    - This is made possible by the very architecture of react-admin, built over a headless package named ra-core.

- https://github.com/BlackBoxVision/react-admin-extensions
  - Packages for improving your development workflow with react admin
  - 已提供: rbac, layout
  - wip: search
- https://github.com/BlackBoxVision/ra-data-simple-microservices
  - React Admin DataProvider with support for micro-services architecture.
- https://github.com/BlackBoxVision/ra-data-jsonapi-microservices
  - React Admin provider with support for microservices with JSON API Spec
- https://github.com/BigBasket/ra-components /js
  - Opensource components for react-admin.
- https://github.com/ValentinnDimitroff/ra-compact-ui /js
  - Enhanced components for popular framework react-admin.

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

- https://github.com/josx/ra-data-feathers /js
  - Feathers data provider for react-admin. A feathers rest client for react-admin
  - https://github.com/kfern/feathers-aor-test-integration

- https://github.com/slax57/admin-e-commerce-demo
  - Redo the React Admin E-Commerce Demo App as training

- https://github.com/prowebdev119/react-admin
  - Open sourced and maintained by marmelab.

- https://github.com/marmelab/ra-in-memory-jwt
  - Manage React-admin authentication with jwt in memory, not in local storage
  - [The Ultimate Guide to handling JWTs on frontend clients (GraphQL)](https://hasura.io/blog/best-practices-of-using-jwt-with-graphql/)

- https://github.com/marmelab/ra-example-oauth
  - An example of OpenID Connect implementation on React Admin
- https://github.com/marmelab/ra-auth-auth0
  - An auth provider for react-admin which handles authentication via a Auth0 instance.
# api/server
- https://github.com/henvo/ra-jsonapi-client /js
  - A JSONAPI compatible data provider for react-admin.

- https://github.com/JavanShen/ra-admin-api
  - api for ra-admin

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

- https://github.com/Weakky/ra-data-opencrud
  - A react-admin data provider for Prisma and GraphCMS
# more
- https://github.com/Groopit/ra-data-odata-server
  - OData Data Provider for react-admin

- https://github.com/guillemfondin/ra-datagrid-sortable
  - Drag'n'drop sortable datagrid for react-admin base on react-sortablejs
