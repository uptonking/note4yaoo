---
title: lib-saas-strapi-blog
tags: [blog, strapi]
created: 2023-11-28T19:12:10.034Z
modified: 2023-12-15T16:52:28.937Z
---

# lib-saas-strapi-blog

# guide

# blogs

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
