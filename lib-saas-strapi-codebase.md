---
title: lib-saas-strapi-codebase
tags: [codebase, strapi]
created: 2024-03-20T15:11:29.948Z
modified: 2024-03-20T15:11:37.860Z
---

# lib-saas-strapi-codebase

# guide

- ee/许可的代码
  - packages/core/core/src/ee
  - packages/core/admin/ee
  - packages/core/admin/admin/src/content-manager/history
  - packages/core/content-manager/server/src/history
  - packages/core/content-releases

- plugins
  - `@strapi/plugin-upload`包的`displayName`是Media Library

- resources
  - 👷🏻 [Strapi contributor documentation | Doc](https://contributor.strapi.io/)
# overview
- init启动流程
  - npm run strapi develop
  - `new Strapi()`; 
    - loadConfiguration
    - add registries
    - createServer > createRouteManager
    - createStrapiFs
    - createEventHub
    - createFeaturesService
    - 🛢️ new Database() > createConnection/createEntityManager > createRepository
  - `const strapiInstance = await strapi.load()`; 
    - 💡 loadApplicationContext > loadSrcIndex/loadPlugins/loadAdmin/loadAPIs(routes/ctrl/srv)
    - add(coreStoreModel).add(webhookModel)
    - transformContentTypesToModels
    - db.init({ models }) > metadata.loadModels
    - this.store = createCoreStore({ db: this.db })
    - 💡 this.entityService = createEntityService
    - this.documents = createDocumentService
    - await this.db.schema.sync();
    - this.server.initMiddlewares();
    - this.server.initRouting();
    - await this.contentAPI.permissions.registerActions();
    - this.cron.start();
  - `strapiInstance.start()`; 
    - listen
    - postListen > openAdmin

- @strapi/strapi作为cli，是执行的入口，基于commander实现

- @strapi/core会load和热加载dist目录的产物
  - 重要的代码都在services

- EventHub是个典型的发布订阅模型，支持多实例
  - listeners(Map) 用于存储带name的事件
  - subscribers(Array) 用于存储全局事件，每次emit都会执行，可不带名称

- 
- 
- 
- 
- 
- 

# plugins
- Strapi automatically loads plugins installed with npm. 
  - Under the hood, Strapi scans every `package.json` file of the project dependencies, and looks for `"strapi": { "kind": "plugin" }`
# db
- core基于cuid2生成增长型id
# admin
- frontend是react-spa
- server是典型的strapi-plugin
# server

# content-type-builder
- `ContentTypeBuilderNav`包括collection/single-types
- `ListView`包括右侧主体，包括 header+list

- 创建collection-type时，先将数据保存到redux，点击save才会提交请求到服务端
  - POST `/content-type-builder/content-types`.
  - content-type-builder-plugin的route会处理创建请求，插件的service会createContentTypes
  - 先创建contentTypes对应的builder，然后builder.writeFiles(), Write all type to files, 
  - ✍🏻️ 会执行 schemaHandler.flush()，执行 写文件ctrl/srv.ts，并将fse.writeJSON将类型定义写到json文件
  - 创建完定义json后，执行 setImmediate(() => strapi.reload()); , process.send('reload')
  - ✍🏻️ 重启使创建route.ts
  - @strapi/strapi的develop.ts，cluster.on('message')会处理'reload'事件
  - cluster处理reload似乎会停止当前process，然后换个process执行

- 删除类型定义时也会删除源码中对应的route/ctrl/srv.ts文件和schema.json文件

- 
- 
- 

# content-manager

# media-library/upload

# user-permissions
- The RBAC permission system relies under the hood on the CASL library.
  - A permission is the combination of an action, a subject, some properties and some conditions. 
  - The logic is that: a user can perform an action on a subject and some of its properties only if it its role has the permission and if the conditions associated to the permission pass.
- Each role can have different permissions independentely. There is no inheritance system.
  - To check if an action can be performed by a user, frontend and backend simply retrieve the list of the permissions associated with the user's roles and check if it contains the permission associated with the action about to be performed
- 
- 
- 

# event
- The event hub is a central system that processes a variety of events in a Strapi application. 
  - These events can be emitted from a variety of sources to trigger associated subscriber functions.
  - Events are mainly used in Strapi to power the webhooks and audit logs features. 
- However, plugin developers can also access the event-hub using the plugin API. 
  - This means plugins can listen to events emitted by Strapi and emit new events to the event hub.
- The event hub is a store of subscriber functions. 
  - When an event is emitted to the hub, each subscriber function in the store will be called with the event's name and a variable number of arguments.
  - This design was inspired by the way Strapi handles lifecycle hooks. It was chosen over the Node.js event emitter because it provides the ability to have a single subscriber function per feature, and does not cause memory leak concerns.
- Performance: Strapi emits a lot of events, so you need to make sure your subscriber functions aren't too expensive to run.
# more
- 🏘️ [Exploring Strapi's Architecture: A Technical Analysis of the Headless CMS Model _202401](https://strapi.io/blog/strapi-architecture)
