---
title: lib-saas-directus-codebase
tags: [codebase, directus]
created: 2024-03-24T06:28:01.463Z
modified: 2024-03-24T06:28:12.838Z
---

# lib-saas-directus-codebase

# guide

- code-main
  - api/src/app.ts

- flows
  - 基于vuedraggable实现，未使用其他外部依赖

- graphql用的不多
  - 前端app主要是insights部分
  - 后端包括controller/**service**/middleware, 移除需要一定的工作量
# not-yet
- 表的关系是如何实现的

- 每个router的每个controller都创建了ItemsService，好处是每个请求都可以单独配置track/revision/permission, 但是否创建太多了

- 
- 
- 

# overview
- 整体是class风格, 未使用装饰器

- 两层架构
  - controller使用service处理业务
  - 通用的ItemsService可以处理配置过的collection, 所以可以作为通用的DAO使用
  - ItemsService内部直接使用knex操作数据库，还能控制业务流程
  - 其他业务Service内部也基于ItemsService操作，所有表都通过ItemsService操作
  - 整体架构的插件化不强，但提供了很多hooks

- init启动流程
  - loadExtensions > extensionManager.initialize() 
    - load, getExtensionsSettings()会注册ext到db
    - register
    - router.use
  - createApp
  - extensionManager.initialize(); 
  - flowManager.initialize(); 
  - app.use('/items', itemsRouter); 
  - app.use('/flows', flowsRouter)
  - http.createServer

- 
- 
- 

# extensions

- 
- 
- 

# db
- To create an M2O relationship, we add a foreign key field to the parent collection. for cities and countries, we can create a `cities.country_id` foreign key field
- configuring an O2M creates an `Alias` field, which lets us access related items.
- O2O is almost exactly the same as an M2O. The only difference is that an O2O enforces cardinality. 

- 
- 
- 

# model/collection/table
- Collections are the individual collections of items, similar to tables in a database. 
  - Changes to collections will alter the schema of the database
- `folder` collections do not hold any data, hence their schema would be `null`.

- Create a new Collection. This will create a new table in the database as well.
  - To create a collection folder that doesn't have an underlying table, you can set schema to `null`.

- `POST /collections` Create a Collection
  - controller: `new CollectionsService()`; 
  - collectionsService.createOne
  - 先查询已有表 knex.select('collection').from('directus_collections')
  - new FieldsService({schema})
  - trx.schema.createTable
  - fieldsService.addColumnToTable(table, field)
  - fieldItemsService = new ItemsService('directus_fields')
  - fieldItemsService.createMany(sortedFieldPayloads)
  - collectionItemsService = new ItemsService('directus_collections')
  - collectionItemsService.createOne
  - new PayloadService
  - payloadService.processM2O // 处理表的关系
  - payloadService.processA2O
  - `trx.insert(payloadWithoutAliases).into(collection)` // 类型入库
  - new ActivityService // save activity row
  - new RevisionsService // If revisions are tracked, create revisions record

- Create the collection/fields in a transaction so it'll be reverted in case of errors or permission problems. 
  - This might not work reliably in MySQL, as it doesn't support DDL in transactions.
- Directus heavily relies on the primary key of a collection, so we have to make sure that every collection that is created has a primary key. 
  - If no primary key field is created while making the collection, we default to an auto incremented id named `id`.

- 
- 
- 
- 

# content
- `POST /items/:collection` Create a new item in the given collection
  - new ItemsService(collection)
  - service.createOne
    - new PayloadService
    - new AuthorizationService
    - payloadService.processM2O
    - payloadService.processA2O
    - `insert(payloadWithoutAliases).into(this.collection)` // 创建
    - payloadService.processO2M
    - new ActivityService
    - activityService.createOne
    - new RevisionsService
    - revisionDelta = await payloadService.prepareDelta
    - revisionsService.createOne({data: revisionDelta,delta: revisionDelta})
    - revisionsService.updateMany(childrenRevisions)
    - opts.onRevisionCreate(revision) // hooks
    - emitter.emitAction('items.create') // hooks
    - return primaryKey
  - service.readOne
    - this.readByQuery(queryWithKey)
    - ast = getASTFromQuery(this.collection)
    - authorizationService.processAST(ast)
    - records = await runAST(ast)
    - filteredRecords
    - emitter.emitAction('items.read')

```JS
trx
  .insert(payloadWithoutAliases)
  .into(this.collection)
  .returning(primaryKeyField)
  .then((result) => result[0])
```

- 
- 

- `PATCH /items/:collection/:id` Update an existing item
  - new ItemsService(req.collection)
  - sanitizeQuery(req.body.query)
  - keys = service.updateByQuery(sanitizedQuery)
    - keys = await this.getKeysByQuery(query);
    - new ItemsService
    - itemsService.readByQuery
    - this.updateMany(keys, data)
    - new AuthorizationService
    - new PayloadService
    - payloadService.processM2O
    - payloadService.processA2O
    - payloadService.processValues
    - `trx(this.collection).update(payload).whereIn()` // 更新
    - payloadService.processO2M
    - new ActivityService
    - activityService.createManythis.readByQuery
    - new RevisionsService
    - payloadService.prepareDelta
    - revisionsService.createMany
    - opts.onRevisionCreate
    - emitter.emitAction('items.update')
  - service.readMany(keys)
    - this.readByQuery

```JS
await trx(this.collection).update(payloadWithTypeCasting).whereIn(primaryKeyField, keys);
```

- 
- 
- 
- 

# flow

# dashboard/insights

# notes

## FieldsService

- 对fields的crud基于ItemsService实现

## other-api

- PayloadService
  - Process a given payload for a collection to ensure the special fields (hash, uuid, date etc) are handled correctly.
# more
