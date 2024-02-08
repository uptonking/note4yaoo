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

# more
- [Strapi vs Nest.js: A Tale of Simplicity and Flexibility in Back-end Development_202306](https://medium.com/@inni.chang95/strapi-vs-nest-js-a-tale-of-simplicity-and-flexibility-in-back-end-development-640f3a506289)
  - In conclusion, Strapi shines in its simplicity for straightforward use cases, while Nest.js offers a more comprehensive and flexible framework for developers comfortable with TypeScript. 

- [Understanding the Strapi Request Flow: A Journey from KOA to Modern Middleware Architecture _202311](https://strapi.io/blog/understanding-the-strapi-request-flow-a-journey-from-koa-to-modern-middleware-architecture)
