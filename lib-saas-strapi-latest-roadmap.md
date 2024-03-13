---
title: lib-saas-strapi-latest-roadmap
tags: [changelog, cms, roadmap, strapi]
created: 2023-12-15T18:28:51.837Z
modified: 2023-12-15T18:29:23.105Z
---

# lib-saas-strapi-latest-roadmap

# guide

# roadmap
- [Strapi Feedback & Roadmap](https://feedback.strapi.io/)
# [changelog](https://strapi.io/changelog)

## v5

## v4.0.0_20211130

- resources
  - [Announcing Strapi v4 with a new UI, Plugin API, Query Engine and more_202111](https://strapi.io/blog/announcing-strapi-v4)
  - [Release v4.0.0 · strapi/strapi](https://github.com/strapi/strapi/releases/tag/v4.0.0)

- We have deeply reworked the Strapi core to make it easier to extend Strapi with plugins, smoothly migrate from one version to another, and boost API performance. 
  - The new `Plugin API` lets developers create plugins without pain. 
  - In Strapi v3, plugins were loaded based on a file structure. To create a plugin, one would need to configure many files. This approach didn't provide code flexibility and made it difficult to maintain the plugin.
  - In v4, we've moved to a programmatic approach, which means that plugins can have their own file structure. Plugin developers only need to configure two files at the root of the package
- 🚨 The v3 plugins will not be compatible with the v4 and must be migrated.
  - the plugins created for the v4 will not be compatible with older Strapi versions.

- We have improved the way queries to the database are done: you can now select which fields and relations you will load from the database
  - We have also added the OR, AND & NOT operators and filtering on components. It means that you will get only the data you need instead of ALL data, which improves your project's performance.

- 🚨🗑️ MongoDB Support dropped with V4

- New user interface with improved navigation and accessibility.
- Plugin API allowing everyone to easily create and maintain plugins thanks to a programmatic approach.
- Database query engine that allows to make precise queries and load only necessary data
- Updated REST & GraphQL API with better filtering, pagination, standardised request and response format.
- API Token that allows to manage the permissions of the Content API requests more smoothly.

- [Add new Blocks rich text editor (alpha) using slate_202309](https://github.com/strapi/strapi/pull/18166)

## v3.0.0_20200526

- resources
  - [Release v3.0.0 · strapi/strapi](https://github.com/strapi/strapi/releases/tag/v3.0.0)
  - [Migrate Guides - Strapi v3](https://docs-v3.strapi.io/developer-docs/latest/update-migration-guides/migration-guides.html)
  - [End of The Road for Strapi v3_20221130](https://strapi.io/blog/end-of-the-road-for-strapi-v3)
  - [Everything you need to know about Strapi (v3) | by Strapi _201610](https://medium.com/strapi/everything-you-need-to-know-about-strapi-v3-6e26a2324c9d)

- content type builder
- rich markdown editor
- JWT authentication
- dynamic zones
- webhooks
- media library
- plug-in providers

## v0.x

# more

# discuss-changelog
- ## 

- ## 

- ## [Add Audit Logs feature _202301](https://github.com/strapi/strapi/pull/15536)
- Go to Settings -> Audit Logs, you will see a list with a log of events, you should see also the details of each event in a specific modal if you click the details icon at the right

- ## 💡 [Database Transactions | Developer Experience | Strapi](https://feedback.strapi.io/developer-experience/p/database-transactions)
- While this is still experimental and is subject to changes in the future versions, there is the possibility to use transactions.
  - We had been using this internally for the past months but I can not give an exact date of when this will released as stable _202306

- ## [Use transactions and expose a transactional API _202301](https://github.com/strapi/strapi/pull/14389)
  - /#merged
- This is a working PR to introduce and use transactions within Strapi.

- [simple implementation of transactions](https://github.com/strapi/strapi/pull/12715)
