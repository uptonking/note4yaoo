---
title: lib-saas-react-admin-dev
tags: [cms, dashboard, react-admin]
created: 2023-12-19T17:28:54.752Z
modified: 2023-12-19T17:29:35.708Z
---

# lib-saas-react-admin-dev

# guide

- pros
  - customizable
  - thin deps: react-query
  - sustainable: no vc-backed

- cons
  - react-only

- features
  - Backend Agnostic
  - Relationships
  - headless logic behind react-admin components is agnostic of the UI library, and is exposed via ... Base components and controller hooks
  - Guessers & Scaffolding: generate a complete CRUD UI based on an API response
  - Powerful Datagrid Components
  - Search & Filtering
  - Forms & Validation
  - Roles & Permissions
  - Audit Log: templates for displaying such audit logs, and helpers to automatically record user actions
  - Calendar
  - Tree View
  - Pub/Sub and Live Updates
  - Configurable UI
  - Theming
  - i18n

- who is using #react-admin
  - [Who is using react-admin? · Issue_201911](https://github.com/marmelab/react-admin/issues/4027)
# dev

# changelog

## [v4.0.0_202204](https://marmelab.com/blog/2022/04/13/react-admin-v4.html)

- v4 focuses on modernizing the inner workings of the library
  - As this release was mostly an internal refactoring, for the most part, the API and the user interface remain the same as in v3.
  - Some major dependencies were swapped (`react-query` instead of `redux`,  `react-hook-form` instead of `react-final-form`).
  - Material UI v5
  - React-router v6

## [v3.0.0_201911](https://marmelab.com/blog/2019/11/20/react-admin-3-0.html)

- we embraced modern React practices - including Hooks
# more
