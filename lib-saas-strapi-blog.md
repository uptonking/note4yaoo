---
title: lib-saas-strapi-blog
tags: [blog, strapi]
created: 2023-11-28T19:12:10.034Z
modified: 2023-12-15T16:52:28.937Z
---

# lib-saas-strapi-blog

# guide

# blogs

## 🏘️ [Exploring Strapi's Architecture: A Technical Analysis of the Headless CMS Model _202401](https://strapi.io/blog/strapi-architecture)

- Strapi, a blend of an API building framework and a CMS, designed to be both robust and adaptable.
  - unlike a monolithic CMS where the front-end and back-end are tightly coupled, Strapi introduces a headless architecture
  - Headless architecture here means that the back-end -- your content management and API delivery -- is separate from the front-end presentation.

- The server initialization is the critical bootstrapping phase where Strapi's application server, based on Node.js and Koa
  - involves setting up the server configuration, initializing the database connections, and preparing the middleware stack
- Middleware in Strapi is crucial; it processes every incoming request, handling tasks such as CORS, body parsing, session managemen
- Strapi introduces policies and hooks as a means to interject custom logic at various points of the application flow. 
  - The policies registry holds a collection of functions that can be executed before an action in a controller, acting as gatekeepers. 
  - Hooks, on the other hand, provide a way to modify core features or add new ones, enabling integrations and custom behaviors. 
  - They act as middleware, but they are tailored to do specific things and don't just act as generic middleware.
- Content API is the essence of Strapi's content management capabilities. 
  - This segment deals with the CRUD operations defined by the content types.
  - It consists of controllers that handle the routing and processing of requests, services that encapsulate the business logic, and the entity service that interacts with the database layer.

- ⛓️ The flow within Strapi begins at the route, guiding requests to their respective policies. 
  - After passing through any Route Policies that apply, the request is handled by Route Middleware for tasks such as authentication or payload processing. 
  - The request is then handed off to the Controller, specifically a Koa handler, to orchestrate the next steps.
  - Inside the Controller, the logic unfolds, tasking the Service to manage business-specific actions. 
  - The Service then engages the EntityService for any data manipulation, which, in turn, communicates with the QueryEngine. 
  - This engine smartly constructs queries that are executed via Knex.js, ensuring the data interacts seamlessly with the database.

- Each plugin can introduce new functionalities or extend existing ones. 
  - They are registered within the system during server initialization, enabling them to integrate seamlessly into Strapi's core. 
- Plugins interact with Strapi's core by hooking into the server's lifecycle events, registering new controllers, services, routes, and even UI components. 
  - They communicate with the main architecture through well-defined interfaces, ensuring that core updates do not break plugin functionality.

- Strapi has evolved its approach to database interactions, moving away from the Waterline ORM used in earlier versions to a more sophisticated and flexible system in Strapi v4.
  - The platform now employs a custom-built query engine, designed specifically for an agnostic interaction with both SQL and NoSQL databases. 
  - The engine effectively translates queries from Strapi's service layer into the specific commands required by the chosen database, enabling developers to perform Create, Read, Update, and Delete (CRUD) operations using JavaScript
- When services require data operations, they utilize the entity service's ORM to communicate with the database. 
  - This interaction abstracts the complexities of direct database manipulation, providing a unified codebase that can interact with multiple database types
  - Lifecycle hooks add another layer of interaction, allowing developers to run custom code during data processing events.

- Every line of code is an open invitation: come and see how we've built this, tweak it, break it, rebuild it. It's in these interactions that Strapi grows stronger and more attuned to real-world applications.

## [Understanding the Strapi Request Flow: A Journey from KOA to Modern Middleware Architecture _202311](https://strapi.io/blog/understanding-the-strapi-request-flow-a-journey-from-koa-to-modern-middleware-architecture)

- the use of middleware or any middleware-like constructs became a standard practice
  - Frameworks, such as Express.js, Ruby on Rails, Django, and Laravel, provide built-in support for defining and using middlewares as a core feature of their architecture.
- Different web frameworks have different implementations and approaches to middleware architectures, but with it, the fundamental concept of pre-processing; authentication, authorization, Logging, and post-processing; response modification, error handling, and caching, — remains consistent.

- like any typical KOA middleware, strapi middlewares execute sequentially, in the order they’re added onto the stack.

- The Strapi Request Chain is an adaptation of the KOA Request Chain. 
  - The twist here is that the Strapi Request Chain is a more elaborate chain with a bigger bag of tricks. 
  - However, at its core, the Strapi Chain still adheres to several rules found in KOA's Chain, such as the LIFO execution order, middleware cascading, and the use of the callback function 'await next()'

- 🧩 Lifecycles are essentially smaller middlewares at their core, wrapping around various database queries, whether it's for creating, updating, deleting, or any other action.
  - These are essentially default middlewares added to Strapi as part of its abstraction layers.

- Strapi's methodology aligns well with other contemporary frameworks like Ruby on Rails (which follows the "Rails way" of doing things), Django (with its opinionated structure), and Laravel (which provides clear conventions for various aspects of web development). 

## [Different types/categories of Strapi Hooks /v4 _202203](https://strapi.io/blog/understanding-the-different-types-categories-of-strapi-hooks)

- A Content-Type is a JSON representation used to specify the underlying database structure of a content entity we want to store in Strapi's database.
  - lifecycle hooks allow us to extend Strapi's default Content-Type functionality by introducing custom code that will run whenever (before or after) a query is executed over a Content-Type. 
- server hooks allows us to add functionality to Strapi's core
  - A common development pattern of a server hook is to have it run an initialization function when the server boots, and then expose its functionality via methods made available either in [strapi.services] or [strapi.hook]
- Webhooks are not exclusive to Strapi; 
  - an application that implements webhooks is able to notify other applications as a certain event occurs in its context. 
  - webhooks are typically implemented as HTTP POST requests.

### 🌰 [How to Use Lifecycle Hooks for Audit Logs in Strapi v4 _202210](https://strapi.io/blog/how-to-use-lifecyle-hooks-for-audit-logs-in-strapi)

- 
- 
- 

## [Demystifying Strapi’s Populate & Filtering | by Strapi | Strapi | Medium](https://medium.com/strapi/demystifying-strapis-populate-filtering-88a95f4dfd6f)

## [Strapi Internals: Customizing the Backend [Part 1 — Models, Controllers & Routes] _202205](https://strapi.io/blog/strapi-internals-customizing-the-backend-part-1-models-controllers-and-routes)

- 
- 
- [Strapi Internals: Customizing the Backend [Part 2]](https://strapi.io/blog/strapi-internals-customizing-the-backend-part-2-policies-webhooks)
  - Global policies can be associated with any route in the project. 
  - Scoped policies only apply to a specific API or plugin

- 
- 
- 
- 
- 
- 
- 
- 

## 🎯 [Bye 2023, Hello 2024! A year in review_202401](https://strapi.io/blog/bye-2023-hello-2024-a-year-in-review)

- improvements
  - Data Transfer
  - Review Workflows
  - Custom Roles became free: Role-based Access Control, including Custom Roles, became 100% free.
  - TypeScript
  - Bulk Publish: Publish multiple entries at the same time.
  - Rich Text Editor: Easy to use rich text editor.
  - v5: We also made significant progress on Strapi v5

- We have one objective for 2024: To make the Editing and Deployment Experience seamless.

- By splitting the frontend and the CMS, the Editing Experience is not as great as it could be. 
  - Editors (and certainly developers) miss live previews, inline editing, etc. We will fix that. 
  - 2024 will be dedicated to unifying the frontend and the CMS, to offer a fantastic Editing Experience.
- Strapi. v5 will be live by the end of Q2, with solid updates: 
  - full TypeScript support, the ability to have a draft version of an already published entry, Vite instead of Webpack, simpler API format (bye "data.attributes"), and more

## [Important Things to Keep in Mind Before Migrating to Strapi_202211](https://maddevs.io/blog/things-to-keep-in-mind-before-migrating-to-strapi/)

- What disadvantages does Strapi have for our case project?
1. No changing history. Strapi has no built-in history of changes to a particular document/page. You need to install additional plugins.
2. No component/slice previews. There are no previews for components. All components are marked with icons. 
3. Components containing images cause failures of the entire CMS
4. No separation of staging and production servers, CI/CD, and database. You will need to manually configure the process of migration from the staging database to the production database
5. Installing additional plugins. Many simple actions require the installation of additional plugins. 
6. A large number of issues
   - Enterprise Edition of the platform includes various advanced features, such as a Customer Success Manager, custom roles, and support with SLAs.

# blog-usage
- [Implementing i18n for Static Sites with Strapi](https://strapi.io/blog/i18n-for-static-sites-with-strapi)

- [How to Build a Pseudo Multi-Tenant Application in Strapi? | Strapi](https://medium.com/strapi/how-to-build-a-pseudo-multi-tenant-application-in-strapi-5b877e2b2951)

## [Build Offline-First Applications With Flutter and Strapi _202407](https://strapi.io/blog/how-to-build-offline-first-applications-with-flutter-and-strapi)

- https://github.com/Claradev32/offline_first_app

## [Introduction to JWT and Cookie storage _202404](https://strapi.io/blog/introduction-to-jwt-and-cookie-storage)

- Stateless Authentication: Stateless nature eliminating reliance upon central databases. This will enable the scaling and load balancing easier because the server does not have to keep track of the session status of each user

- JWT is Stateless, while the cookies are Stateful

- [Guide on authenticating requests with the REST API _202403](https://strapi.io/blog/guide-on-authenticating-requests-with-the-rest-api)
  - Unlike API tokens, JWT tokens are stateless and eliminate the need for server-side management.
# blog-stars

## 💡 [Schemaless platforms. Architectural considerations _202002](https://medium.com/samanvay-on-tech/schemaless-platforms-e6bbf0a64a24)

- Architectural considerations for products that allow their users to define their own data models

- In most schemaless platform there is a platform-user who defines their specific data model and an end-user who simply uses that solution.

- Three types of schemaless platforms
  - Products where schemalessness is the defining feature of the product — like Google Forms, ODK, AirTable.
  - Products with an embedded schemaless facility in multiple parts of the system— electronic medical records, SalesForce.
  - Products that support the definition of custom fields, but they are not very powerful in what they allow — like multiple data types, skip logic, validations, calculated fields, schema migration, etc.

- Do I need to use NoSQL databases for creating schemaless platforms? 
  - Strictly speaking no, because there are ways to achieve schemalessness on relational databases as well.
- Entity Attribute Value (EAV)— In a nutshell, keep one-row per field value. 
  - A key column that represents the name of the field and a column for storing the value. 
- Embedded schemaless facility within a relational database products. 
  - For example support for JSONB within PostgreSQL.
- User-defined database schema — Here the user can specify the schema, using which the platform creates database objects (tables, columns, index, etc) — providing a schema full structure when deployed. 
  - This is followed by Strapi, Drupal. 
  - One cannot do this if you want to use a single database schema for multiple customers who will all define their schema for themselves.
- Spare columns — The platform provides spare columns in the database tables, where it wants to provide support for user-defined fields. 
  - It can choose to represent all data types as a string or provide spare columns for multiple data types. 
  - Obviously in-elegant, but clever from a performance perspective, as we will see later. This can be further extended to have spare tables with spare columns.

- all schemaless platforms need to provide the ability for the user to define their schema and for the platform to store and serve it. 
- Even though there are many schemaless platforms, this space has lacked standards for defining user schema

- 🆚️ Technical tradeoffs in schemaless platforms
- Relational databases schemas are quite standardised. This allows for reporting tools like Metabase, Tableau and others to provide numerous features 
  - With schemaless platforms, we lose these benefits. These reporting tools do not understand EAV, JSONB, NoSQL very well
- The database constraints like foreign-key, unique, not null, custom constraints cannot be taken for granted anymore. 
- Data migration on schema change
  - In schema full applications, the schema change and its associated re-arrangement of data are handled by the programmers using SQL (with flyway, Liquibase etc). 
  - In schemaless platforms, supporting the change in user-schema over time is simpler to implement but performing data migration to the new schema is tricky.
# blogs-cms

## 🆚 [Directus vs Strapi: which one is better ? _202209](https://www.izoukhai.com/blog/directus-vs-strapi-full-comparison)

- Directus supports 6 DB clients:
  Postgres
  Sqlite3
  MySQL
  OracleDB
  MsSQL
  CockroachDB. 
  Supabase
- Strapi supports only 4: 
  Postgres
  SQLite
  MySQL
  MariaDB

- Strapi's architecture is based on local files: collections models, life-cycle hooks... everything is declared in configuration files.
- Directus stores everything in the database except for custom plugins (hooks, app mods, endpoints...).
  - Personally, I prefer Directus' way mainly because any change is applied instantly, you don't need to wait for the app to restart, unlike Strapi.

- Strapi's admin app is based on React, Directus' on Vue. 
  - Directus clearly outperforms Strapi on this part: customization, snappiness, coherence...  

- Directus' advantages over Strapi
- Directus can be used over an existing database
  - Directus can initialize itself over your existing database, allowing you to manage your tables even if they were not created with the tool (except for relational fields I think). 
  - Strapi forces you to bootstrap your project with it if you want to have control over your database.

- Directus has a powerful role & permission system
  - Directus offers a simple and powerful permissions management interface through the admin app. 
  - Directus lets you create an unlimited number of roles, where Strapi has a limit of 3 roles in its free version.
  - Although Strapi provides an interface to manage permissions per roles, Directus goes much (MUCH) further by allowing you to customize access based on conditions, and per field access.

- Directus supports geographic objects (PostGIS)

- Directus' UI is more customizable
  - Directus allows you customize your admin dashboard much more than Strapi, allowing non-technical users to actually use the dashboard easily.
  - Conditional display
  - Per field aliases
  - Collections grouping
  - Adjust collection page layout 

- Directus Flows allow you to run operations based on different triggers directly from your dashboard in a no-code way, with a beautiful UI composed of blocks connected to each other.

- Why Directus is so unpopular ?
  - Even though Directus has been around longer than Strapi with its PHP version (< v9), the latter just destroyed the game. 

- Conclusion
  - Don't fall for Strapi's powerful marketing

##  [Strapi vs Directus: which one to choose 2023? _202310](https://medium.com/@weframe.tech/strapi-vs-directus-which-one-is-good-ff398e7c9e42)

- Benefits of Directus Compared to Strapi
  - Database Integration: Directus can seamlessly adapt to your existing database, enabling you to manage tables that were not originally created with the tool (excluding relational fields, as far as we know). 
    - In contrast, Strapi requires you to initiate your project with it to gain control over your database.
  - Robust Role & Permission System: Directus boasts a robust and powerful role and permission system.
    - Directus offers the flexibility to create an unlimited number of roles, whereas Strapi’s free version imposes an inexplicable limit of 3 roles. 
    - While Strapi does provide a permissions management interface for roles, Directus takes it to the next level by allowing extensive customization of access conditions and per-field access.
  - Directus’ Geospatial Advantage: PostGIS Support
  - Directus Flows
# blogs-devops

## [How to Deploy and Scale Strapi on a Kubernetes Cluster 1/2 _202302](https://strapi.io/blog/how-to-deploy-and-scale-strapi-on-a-kubernetes-cluster-1-2)

- [How to Deploy and Scale Strapi on a Kubernetes Cluster 2/2](https://strapi.io/blog/how-to-deploy-and-scale-strapi-on-a-kubernetes-cluster-2-2)
  - https://github.com/chepeftw/strapi-k8s-blog-post
  - We currently have our DB and app running with a single replica and nothing that provides high availability. 
  - For the DB, it's highly recommended that, once again, a cloud provider solution is used or a HA DB self-hosted.
  - An initial step for HA is and will always be: let's have more replicas of our application.
  - we can create a Horizontal Pod Autoscaler (HPA). Basically, it's a K8s object that will create more replicas of our Pod based on a defined property such as CPU or memory. We will rely on the CPU, and it's important to highlight that the HPA uses a percentage of the equivalent of the requested resources.
  - The HPA will use by default only basic metrics like CPU and memory. If you implement your own metrics, you might want to switch the autoscaling to use those metrics instead. To achieve this, the most recommended tool would be to rely on the KEDA controller. 
# more
- [Strapi vs Nest.js: A Tale of Simplicity and Flexibility in Back-end Development_202306](https://medium.com/@inni.chang95/strapi-vs-nest-js-a-tale-of-simplicity-and-flexibility-in-back-end-development-640f3a506289)
  - In conclusion, Strapi shines in its simplicity for straightforward use cases, while Nest.js offers a more comprehensive and flexible framework for developers comfortable with TypeScript. 

- [Best Practices of API Security in Strapi | by Strapi | Strapi | Medium](https://medium.com/strapi/best-practices-of-api-security-in-strapi-3ed59aa2b0c0)
