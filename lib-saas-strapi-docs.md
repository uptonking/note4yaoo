---
title: lib-saas-strapi-docs
tags: [docs, strapi]
created: 2023-11-28T19:04:44.522Z
modified: 2023-12-15T16:52:36.718Z
---

# lib-saas-strapi-docs

# guide

- resources
  - 👷🏻 [Strapi contributor documentation | Doc](https://contributor.strapi.io/)
  - [Strapi 中文文档](https://www.strapi.cn/)
  - [Backend Customization Examples Cookbook | Strapi Documentation](https://docs.strapi.io/dev-docs/backend-customization/examples)
    - Examples are meant to extend the features of FoodAdvisor
  - https://docs.strapi.io/openapi/
# docs

## overview

- The original purpose of the project was to help Bootstrap your API: that's how Strapi was created
  - Now, Strapi is an open-source headless CMS that gives developers the freedom to choose their favorite tools and frameworks and allows editors to manage and distribute their content using their application's admin panel
  - Based on a plugin system, Strapi is a flexible CMS whose admin panel and API are extensible - and which every part is customizable to match any use case.
  - Strapi also has a built-in user system to manage in detail what the administrators and end users have access to.

- we utilize future flags, which provide a way to enable unstable features at your own risk

- 
- 
- 

## usage

- Media Library is a Strapi plugin that is always activated by default and cannot be deactivated
  - Assets uploaded to the Media Library can be inserted into content-types using the Content Manager.

- Depending on what users and their roles and permissions you want to manage, you should either use the Role Based Access Control (RBAC) feature, or the Users & Permissions plugin.

- Strapi is built around different types of plugins

- If you disabled the Draft & Publish feature, saving your content means saving and publishing at the same time.

- Strapi applications are not meant to be connected to a pre-existing database, not created by a Strapi application, nor connected to a Strapi v3 database. The Strapi team will not support such attempts. 
  - Attempting to connect to an unsupported database may, and most likely will, result in lost data.

- By default Strapi provides a provider that uploads files to a local directory, which by default will be `public/uploads/` in your Strapi project. Additional providers are available should you want to upload your files to another location.
  - By default Strapi accepts localServer configurations for locally uploaded files. These will be passed as the options for `koa-static`.

- The authenticated `user` object is a property of `ctx.state`.

- 
- 
- 
- 

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

- Transfer tokens allow users to authorize the strapi transfer CLI command 

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

- Some plugins can be further extended through the configuration of providers, packages designed to be used on top of an existing plugin and add a specific integration to it.
- Currently, the only plugins designed to work with providers are the:
  - Email plugin, and
  - Media Library plugin (implemented via the Upload plugin).

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
- A plugin can only interact with data from the `/server` folder. If you need to update data from the admin panel, please refer to the passing data guide

- Within the /server folder you have access to the Strapi object and can do database queries whereas in the /admin folder you can't
- Passing data from the /server to the /admin folder can be done using the admin panel's Axios instance

## providers

- Providers add an extension to the core capabilities of the plugin, for example to upload media files to AWS S3 instead of the local server
  - Only the Upload and Email plugins are currently designed to work with providers.

- A provider can be configured to be private to ensure asset URLs will be signed for secure access.
# content-manager
- Content Manager is a core plugin of Strapi. 
  - It is a feature that is always activated by default and cannot be deactivated
  - It is accessible both when the application is in a development and production environment.

- Components are a combination of several fields, which are grouped together in the edit view.
  - There are 2 types of components: non-repeatable and repeatable components.
  - Non-repeatable components are a combination of fields that can be used only once. By default, the combination of fields is not directly displayed in the edit view
  - Repeatable components allow the creation of multiple component entries, all following the same combination of fields. The repeatable component entries can be reordered or deleted directly in the edit view

- Dynamic zones are a combination of components, which themselves are composed of several fields. 
  - Writing the content of a dynamic zone requires additional steps in order to access the fields.
  - Dynamic zones' components can also be reordered or deleted directly in the edit view
  - Unlike regular fields, the order of the fields and components inside a dynamic field is important. It should correspond exactly to how end users will read/see the content.

- Relation-type fields added to a content-type from the Content-type Builder allow establishing a relation with another collection type. These fields are called "relational fields".
  - The content of relational fields is written from the edit view of the content-type they belong to

- With the Internationalization plugin installed, it is possible to manage content in more than one language, called "locale".
  - With the Internationalization plugin installed, it is possible to manage content in more than one language, called "locale".
# content-type-builder
- Content-type Builder is a core plugin of Strapi. 
  - It is a feature that is always activated by default and cannot be deactivated. 
  - The Content-type Builder is only accessible to create and update content-types when your Strapi application is in a development environment, else it will be in a read-only mode in other environments.

- administrators can create and manage content-types: collection types and single types but also components.
  - Collection types are content-types that can manage several entries.
  - Single types are content-types that can only manage one entry.
  - Components are a data structure that can be used in multiple collection types and single types.

- Custom fields are a way to extend Strapi’s capabilities by adding new types of fields to content-types or components. Once installed (see Marketplace documentation), custom fields are listed in the Custom tab when selecting a field for a content-type.

- Components are a combination of several fields. Components allow to create reusable sets of fields, that can be quickly added to content-types, dynamic zones but also nested into other components.
- Dynamic zones are a combination of components that can be added to content-types. 
  - When using dynamic zones, different components cannot have the same field name with different types (or with enumeration fields, different values).

- 🚨 keep in mind that regarding the database, renaming a field means creating a whole new field and deleting the former one. 
  - Although nothing is deleted from the database, the data that was associated with the former field name will not be accessible from the admin panel of your application anymore.

- Deleting a content-type automatically deletes all entries from the Content Manager that were based on that content-type. 
  - The same goes for the deletion of a component, which is automatically deleted from every content-type or entry where it was used.
- Deleting a content-type only deletes what was created and available from the Content-type Builder, and by extent from the admin panel of your Strapi application.   
  - All the data that was created based on that content-type is however kept in the database
# media-library
- The Media Library displays all assets uploaded in the application, either via the Media Library itself or via the Content Manager when managing a media field. 
- Assets uploaded to the Media Library can be inserted into content-types using the Content Manager.

- A variety of media types and extensions are supported by the Media Library:
  - image/video/audio
  - files: pdf, csv, xlsx, json, zip

- Folders in the Media Library help you organize uploaded assets. 

- Folders follow the permission system of assets (see Users, Roles & Permissions). It is not yet possible to define specific permissions for a folder.
# roles/permissions
- Depending on what users and their roles and permissions you want to manage, you should either use the Role Based Access Control (RBAC) feature, or the Users & Permissions plugin. 
  - Both are managed from Settings, accessible from the main navigation of the admin panel.

- By default, 3 administrator roles are defined for any Strapi application:
  - Author: to be able to create and manage their own content.
  - Editor: to be able to create content, and manage and publish any content.
  - Super Admin: to be able to access all features and settings. This is the role attributed by default to the first administrator at the creation of the Strapi application.

- end-user accounts are managed from the Content Manager, but end-user roles and permissions are managed in the Settings interface.
- By default, 2 end-user roles are defined for any Strapi application:
  - Authenticated: for end users to access content only if they are logged in to a front-end application.
  - Public: for end users to access content without being logged in to a front-end application.

- With the Users & Permissions plugin, the end users and their account information are managed as a content-type.
  - Registering new end users in a front-end application with the Users & Permissions plugin consists in adding a new entry to the User collection type

- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 

# more
