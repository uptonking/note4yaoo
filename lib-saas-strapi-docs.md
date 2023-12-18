---
title: lib-saas-strapi-docs
tags: [docs, strapi]
created: 2023-11-28T19:04:44.522Z
modified: 2023-12-15T16:52:36.718Z
---

# lib-saas-strapi-docs

# guide

# docs
- strapi /57.5kStar/MIT+EE/202311/ts
  - https://github.com/strapi/strapi
  - https://strapi.io/
  - https://strapi.io/demo 一定时长后数据会清除
  - the leading open-source headless CMS
  - 核心功能是提供了通过ui操作实现rest api的功能
    - 系统内容通过ui操作编写
    - 系统前端strapi没有限制，strapi只提供了api
  - The original purpose of the project was to help Bootstrap your API
  - Now, Strapi is an open-source headless CMS that gives developers the freedom to choose their favorite tools and frameworks and allows editors to manage and distribute their content using their application's admin panel.

## overview

- The original purpose of the project was to help Bootstrap your API: that's how Strapi was created
  - Now, Strapi is an open-source headless CMS that gives developers the freedom to choose their favorite tools and frameworks and allows editors to manage and distribute their content using their application's admin panel
  - Based on a plugin system, Strapi is a flexible CMS whose admin panel and API are extensible - and which every part is customizable to match any use case.
  - Strapi also has a built-in user system to manage in detail what the administrators and end users have access to.

- 
- 
- 

## usage

- This user guide contains the functional documentation related to all features available in the admin panel of your Strapi v4 application.

- Content Manager is a core plugin of Strapi. 
  - It is a feature that is always activated by default and cannot be deactivated
  - It is accessible both when the application is in a development and production environment.
- a sub navigation displaying 2 categories: Collection types and Single types. 

- Content-type Builder is a core plugin of Strapi. 
  - administrators can create and manage content-types: collection types and single types but also components.

- Media Library is a Strapi plugin that is always activated by default and cannot be deactivated
  - Assets uploaded to the Media Library can be inserted into content-types using the Content Manager.

- Depending on what users and their roles and permissions you want to manage, you should either use the Role Based Access Control (RBAC) feature, or the Users & Permissions plugin.

- Strapi is built around different types of plugins

## faq

### Can Strapi be run in serverless environments?

- Strapi is not well suited for serverless environments due to how the application is structured. 
  - Several actions happen while Strapi is booting that can take several seconds. Serverless deployment usually requires an application to cold boot very quickly. Strapi is designed to run as an always-on service, and we don't plan to decrease the cold boot time for the foreseeable future. Therefore, running Strapi in serverless environments is not a great experience, as every request will take seconds to respond to instead of milliseconds. 
  - Choosing between a cold boot or a warm boot is an architectural decision that many software developers need to take from a very early stage, so please consider this when choosing to use Strapi.

### Does Strapi allow me to change the default ID type or name?

- No, currently does not have the ability to allow for changing the default id name nor does it allow you to switch the data type (such as UUID in PostgreSQL), support for this is being looked at in future.
# more
