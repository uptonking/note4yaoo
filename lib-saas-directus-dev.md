---
title: lib-saas-directus-dev
tags: [cms, directus]
created: 2024-02-16T14:55:26.345Z
modified: 2024-02-16T14:55:58.271Z
---

# lib-saas-directus-dev

# guide
- pros
  - 支持 content versioning
  - 数据修改更新的架构采用delta的设计
  - 在admin添加新的data-model时，数据库会创建对应的表，但后端无需生成代码，
    - 支持动态访问，相比之下，strapi不支持在生产环境中添加model
  - Works with new or existing SQL databases, no migration required.
  - Extensions provide a way to modify or expand Directus' functionality

- cons
  - license: GPLv3 > BSL

- features
  - instant REST+GraphQL API on top of any SQL database
  - Our no-code Vue.js app is intuitive for non-technical users
# dev
- 在admin添加新的data-model时，数据库会创建对应的表，~~同时后端src/api下面会自动生成对应的schema/router/controller/service~~
# examples

## utils

- https://github.com/tractr/directus-sync /MIT/202403/ts
  - A CLI tool for synchronizing the schema and configuration of Directus across various environments.
  - By leveraging Directus's REST API, it aligns closely with the native actions performed within the application
  - Updates are granular, focusing on differential data changes rather than blunt table overwrites, which means only the necessary changes are applied, preserving the integrity and history of your data.
  - directus-sync organizes backups into multiple files, significantly improving readability and making it easier to track and review changes. 
  - directus-sync operates on a tagging system similar to Terraform, where each trackable element within Directus is assigned a unique synchronization identifier (SyncID). This system is key to enabling version control for the configurations and schema within Directus.

- https://github.com/bcc-code/directus-schema-sync /apache2/202402/ts
  - The better way to sync your Directus schema, configuration and selected data between environments.
  - Automatically export and import both the schema and data when you make changes via Directus or in the json data files

- https://github.com/fabian-hiller/directus-sdk /202306/ts
  - This repository can be seen as an alternative proposal to the current Directus SDK.
  - Modular design
  - This SDK builds on existing web APIs like the Fetch API and therefore has no dependencies and can run in any environment. 
# more
