---
title: lib-saas-strapi-docs
tags: [docs, strapi]
created: 2023-11-28T19:04:44.522Z
modified: 2023-12-15T16:52:36.718Z
---

# lib-saas-strapi-docs

# guide

- resources
  - [Strapi contributor documentation | Doc](https://contributor.strapi.io/)
  - [Strapi 中文文档](https://www.strapi.cn/)
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

## configuration

- conf
  - db
  - server
  - admin
  - middleware
  - api calls
  - plugins
  - lifecycle
  - sso
  - rbac
  - assets
  - api tokens
  - cron jobs

## api

- your content can be accessed through Strapi's Content API, which is exposed: by default through the REST API
- REST and GraphQL APIs represent the top-level layers of the Content API exposed to external applications. 
- Strapi also provides 2 lower-level APIs:
  - The Entity Service API is the recommended API to interact with your application's database within the backend server or through plugins. The Entity Service is the layer that handles Strapi's complex data structures like components and dynamic zones, which the lower-level layers are not aware of.
  - The Query Engine API interacts with the database layer at a lower level and is used under the hood to execute database queries. It gives unrestricted internal access to the database layer, but should be used only if the Entity Service API does not cover your use case.

- Plugins also have their dedicated APIs: the Server API and the Admin Panel API. These plugin-related APIs are offered to develop plugins and allow a plugin to interact either with the back-end server of Strapi (Server API) or with the admin panel of Strapi (Admin Panel API).

- Entity Service API is built on top of the Query Engine API. 
  - The Entity Service is the layer that handles Strapi's complex data structures like components and dynamic zones, and uses the Query Engine API under the hood to execute database queries.
  - If you need direct access to `knex` functions, use `strapi.db.connection`.

- Query Engine API should mostly be used by plugin developers and developers adding custom business logic to their applications.
  - In most use cases, it's recommended to use the Entity Service API instead of the Query Engine API.
- To avoid performance issues, bulk operations are not allowed on relations.

- Providers add an extension to the core capabilities of the plugin, for example to upload media files to AWS S3 instead of the local server
  - Only the Upload and Email plugins are currently designed to work with providers.

## plugins

- your experience with Strapi plugins will fall under the following 4 use cases:
  - Some built-in plugins can already be pre-installed 
  - 3rd-party plugins can be browsed from the admin panel or from the Marketplace website
  - You might want to develop your own plugins. these plugins are called "local plugins", or can be submitted to the Marketplace
  - You might want to extend an existing plugin 

- Built-in plugins
  - Content Source Map plugin, used with Vercel Visual Editing, enhances the content edition experience
  - i18n plugin allows creating, managing and distributing localized content in different languages
  - Upload plugin powers the Media Library and allows versatile file uploads.
  - Users & Permissions plugin offers JWT-based authentication and ACL strategies for API protection and user permissions.

- The Admin Panel API is about the front end part, i.e. it allows a plugin to customize Strapi's admin panel.
- The Server API is about the back-end part, i.e. how the plugin interacts with the server part of a Strapi application.

- Once created or added to Strapi via plugins, custom fields can be used in the Content-Type Builder and Content Manager just like built-in fields.
  - It is recommended that you develop a dedicated plugin for custom fields. 
  - Custom field plugins include both a server and admin panel part. 
  - The custom field must be registered in both parts before it is usable in Strapi's admin panel.
  - Though the recommended way to add a custom field is through creating a plugin, app-specific custom fields can also be registered within the global `register` function

- Plugins can be extended in 2 ways:
  - extending the plugin's content-types
  - extending the plugin's interface (e.g. to add controllers, services, policies, middlewares and more)

- A plugin's Content-Types can be extended in 2 ways: using the programmatic interface within `strapi-server.js` and by overriding the content-types schemas using `schema.json`.

- When a Strapi application is initializing, plugins, extensions and global lifecycle functions events happen in the following order:
  - Plugins are loaded and their interfaces are exposed.
  - Files in ./src/extensions are loaded.
  - The register() and bootstrap() functions in ./src/index.js are called.

- To store data with a Strapi plugin, use a plugin content-type. 
  - Plugin content-types work exactly like other content-types. 
  - Once the content-type is created, you can start interacting with the data.

- Within the /server folder you have access to the Strapi object and can do database queries whereas in the /admin folder you can't
- Passing data from the /server to the /admin folder can be done using the admin panel's Axios instance
# more
