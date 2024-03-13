---
title: lib-saas-strapi-blog
tags: [blog, strapi]
created: 2023-11-28T19:12:10.034Z
modified: 2023-12-15T16:52:28.937Z
---

# lib-saas-strapi-blog

# guide

# blogs

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
# more
- [Strapi vs Nest.js: A Tale of Simplicity and Flexibility in Back-end Development_202306](https://medium.com/@inni.chang95/strapi-vs-nest-js-a-tale-of-simplicity-and-flexibility-in-back-end-development-640f3a506289)
  - In conclusion, Strapi shines in its simplicity for straightforward use cases, while Nest.js offers a more comprehensive and flexible framework for developers comfortable with TypeScript. 

- [Understanding the Strapi Request Flow: A Journey from KOA to Modern Middleware Architecture _202311](https://strapi.io/blog/understanding-the-strapi-request-flow-a-journey-from-koa-to-modern-middleware-architecture)
