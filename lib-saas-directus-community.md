---
title: lib-saas-directus-community
tags: [cms, community, directus]
created: 2024-02-16T14:56:05.247Z
modified: 2024-02-16T14:56:17.057Z
---

# lib-saas-directus-community

# guide

# discuss-stars
- ## 

- ## 

- ## 🆚️ [GraphQL/REST/SDK: is there any principal difference? _202212](https://github.com/directus/directus/discussions/16889)
- They all support the same functionality set. The SDK is a thin wrapper around axios which calls the regular REST API endpoints, so there's no functional difference between the two.
  - 💡 In general, Directus converts requests coming in (through rest/graphql or soon websockets) into a generic `AST` which is then parsed through the data pipeline to be queried/modified. 
  - That allows all of these interfaces to support the same feature sets and generally have the same performance

- ## 🌰〰️ [Explanation on transmitting data inside flows _202308](https://github.com/directus/directus/discussions/19471)
- [directus flows - How to all field value pass in payload when record update in direct us - Stack Overflow](https://stackoverflow.com/questions/76613284/how-to-all-field-value-pass-in-payload-when-record-update-in-direct-us)

- Choose the collection Support and set the IDs to `"{{$trigger.keys[0]}}"` (be aware of In Read Data operation flow IDs stays blank despite the Raw value)
  - 思路是 update-trigger > read-updated > create/email
  - 注意填写id可能保存值为空，可切换id编辑器的模式raw/json再写id

- ## 🧩 [Directus EAV · directus/directus _202009](https://github.com/directus/directus/discussions/2840)
- Use relationships
  - A single product with multiple attributes could be configured as a one-to-many from products->attributes. 
  - If an attribute can be used by multiple products, use a many-to-many instead

- ## 📈 [CSV/Excel File Import](https://github.com/directus/directus/discussions/7246)
- Yes u can already do that through api
  - I'm talking about the DIrectus GUI. A button to upload the file/select from the file library

- This has since been implemented _20230511

- ## 📡📈 [Add a Spreadsheet Layout _20210201](https://github.com/directus/directus/discussions/3874)
- I'm torn between two options:
  - Spreadsheet style, showing and editing raw values
  - Table Layout Plus... where clicking a field will open a context popup with the proper interface

- I'd prefer a third option: Use the correct interfaces and only make them pop up if necessary from a layout perspective. That way in the mockup above probably only the Image fields would need context popup, as text/dropdown should work with really little space.
  - Of course the decision which mode to use could be manual (but per field), in the layout settings.

- I'd advice you not to build the spreadsheet yourself but to reuse a dedicated component (like Revogrid, with proper patches and customization ?) or you'll end up with endless requests for new features everyone expect from spreadsheets but were not in your 80/20 plan (selection, copy paste, moving values, infinite loading...).

- Maybe nocodb.com can be used as a spreadsheet for the collections? Directus can integrate NocoDB by sharing the same DB connection, and can have a button "Open in NocoDB" (opens collection in a new tab and in NocoDB loaded) in the collection toolbar.
  - Interesting. This platform actually seems far more robust than a library we can leverage... more like a secondary competitor. Still, we'll look into it

- This feature request has received over 15 votes from the community. This means we'll move this feature request to the Under Review state _202305

- ## 请教下 表结构更改了（使用外部数据库工具修改的）, 除了重启directus以外，有办法热加载表结构吗？ _20231214
- https://discord.com/channels/725371605378924594/946422284426551346/1184739818568171620
- 可以试试看清除缓存 https://docs.directus.io/reference/system/utilities.html#clear-the-internal-cache

- 感谢 亲测有效，之前一直是重启容器来重新加载schema， 最近突然重新要5min左右， 所以在寻找原因和方案。 
  - 测试/utils/cache/clear 接口成功实现了 新增表/字段后的变更

- ## ✨🔀 [[RFC] Directus Offline First SDK_202303](https://github.com/directus/directus/discussions/17808)
- I think RxDB is an excellent choice for responsive offline-first applications. During my initial research I found multiple points, why I wouldn't want to use it
  - It ships a whole db with 45kb gziped
  - Interfacing with IndexedDB is via a commercial plugin
  - I want to interface with any HTTP endpoint and not rely on GraphQL or other demanding server side requirements
- At the end of the day, it is a tradeoff. RxDB can free you from getting locked down to one specific backend, but it has its drawbacks.

- 💡 Conflict Resolution Approaches: 4 methods for handling edit conflicts
- Generally, conflict resolution falls into four categories, with developers selecting the most suitable strategy. 
  - Performance and usability with CRDTs have come a long way since their inception 2011. 
  - For most small to mid-scale Directus use cases CRDTs will work fine. They will probably still be a rarely used data type.
- 👉🏻 Last Write Wins (LWW): 
  - This default method resolves conflicts by prioritizing the most recent write operation in a CRUD app. Earlier edits are overwritten.
- 👉🏻 Operational Transformation (OT): 
  - This method can be implemented using a Directus flow operating on the `article_event` data, updating the articles collection accordingly.
- 👉🏻 Conflict-free Replicated Data Types (CRDTs): 
  - This method employs data structures that automatically merge, resolving conflicts. 
  - CRDT implementation would be facilitated by Directus' support for views in relational databases. 
  - However, developers should be be able to fully choose their preferred implementation, because developers may utilize resources like Yjs or Automerge.
- 👉🏻 Return Conflict List to Last Writer or Arbitrator: 
  - This approach requires handling user responses to conflicts, similar to git. 
  - It places a significant burden on users and developers, and should only be considered as a last resort for specific use cases.

- I'm very curious to hear some more thoughts around the different conflict resolution techniques though. It sounds like that's something that you might have to be able to override method call to method call (eg what happens if you need a different resolution for articles than for authors etc) 
  - Totally agree. CRDTs are a data model problem. A CRDT – as opposed to a normal data type – might require that you send different (or usually more) data to the server. The proposed API still expects you to be explicit about what you send to the server.

- ## 💰 [Funding, Focus, and What's Next? · directus/directus _20230329](https://github.com/directus/directus/discussions/17977)
- I am also a user of odoo.com which is an open source product too.
- What odoo team is offering are :
  - A community version of product, similar to Directus we have for now
  - A cloud service, also similar to Directus cloud
  - A partner program, company can pay to be a listed partner, to get leads for customers need odoo and some other trainings, advanced product features.
  - Some advance features, for example rapid development tools, extensions etc for paid subscribers (paid user).
- Odoo is with a lot of vertical/industry related solutions which can be used by a company without too many customization. This will make odoo relatively easier in finding customers.
  - Directus is more developer focused.

- I really like directus and want to give some advices on how to make the project financeable and continuously grow.
  - make a marketplace (inside sell your own layouts, plugins or general extensions) example: plugins.craftcms.com or apps.shopify.com; users can earn from their plugins and directus can have their own also.
  - create some boilerplates to be sold (for example i want an ecommerce, and have no time to develop all models or schemas, so by adding some ready-to-use boilerplates to the marketplace would be great)
  - create an expert or developers part - shopify.com/it/partner
  - create an video academy craftquest.io
# discuss-schema-change
- ## 

- ## 

- ## [Migrations vs Schemas, what is the way to go? _202204](https://github.com/directus/directus/discussions/12713)
- Sounds like schema migrations is what you'd be looking for. Those allow you to create a snapshot of the current configuration, and apply that to another instance. Migrations could also be used for this purpose, but are intended for more edge-case uses (it's an escape hatch in case schema migrations doesn't offer what you need) 

- ## 🐛🆔️ [Ability to rename collections and fields  _202005](https://github.com/directus/directus/discussions/2711)
- 202401: Realistically the only way to support this natively is to start relying on UUIDs for collections/fields instead of the database key. Trying to update the name in like 30 places every time you want to change the key feels very error prone

- 202401: For anyone here that is only concerned about what the Directus user sees and not names in the underlying database, you can use `field name translations` and `collection naming translations` to change the name throughout the Directus Studio. It doesn't change anything for the underlying database or the API, but it's better than nothing!

- [Change Field Name / Type after creation](https://github.com/directus/directus/discussions/14037)

- [The ability to rename columns in table layout, especially for those that are properties of relations ](https://github.com/directus/directus/discussions/13277)

- ## 💡🏘️ [Code-first configuration of schema, roles and permissions _202204](https://github.com/directus/directus/discussions/13041)
  - It would be great if schemas, roles and permissions could be managed via code. 
  - Often custom permissions contain logic that is of a fairly technical nature and should ideally be versioned and repeatable between dev/staging/prod environments.

- Here is my approach on this issue:
  - A module (with UI) where you can download config/collections piece by piece in JSON format
  - Save the downloaded files in a template directory in the repo
  - A hook reacting on server start that reads the files in the template directory and patches everything
  - This way, 'everything' can be version controlled and synced between environments.
- Patching and reading files like this on server start will greatly increase startup times leading to lower horizontal scaling performance.

- 202311: Hi, I've just built a tool called `directus-sync` that could help streamline the way we handle Directus configurations and schema management. It’s inspired by the principles of infrastructure-as-code, with a touch of the familiar workflow from Terraform. This is currently a beta release, and I’m seeking collaborators who are up for testing, providing feedback, and contributing to its evolution. 

- I still prefer the idea of starting to create schema changes, adding roles, or configure permissions on the UI rather than generating migration files manually because I love Directs UI and it is way faster/easier to create, setup and experiment.
- I have been experimenting with DrizzleORM recently to manage migrations outside of Directus just to find out how this could be managed

- ⚖️ The general idea is that schemas, roles and permissions could be developed in code (e.g. yaml) and applied to the database the next time directus is started. 
  - An extension of this would be that changes made via the UI (locally) are reflected back to code and can be reviewed and committed to source control. 
  - Applying changes to production could be part of a CI/CD pipeline (e.g. Github Actions) which could use the directus API.

- 🔒 There should also be a locked mode, where it's only possible to change data, but not schemas, permissions and so on in a production environment. 
  - Could be enabled by an environment variable or something similar outside the application. This would make sure a production environment is predictable.

- ## [Separate Directus tables from content _202010](https://github.com/directus/directus/discussions/2882)
- One approach could be kind of like Wordpress' ACF Pro solves it with their acf-json directory:
  - The database stays as it is, but additionally for each model/role/permission, a json file is saved somewhere in the filesystem, containing all the details to reproduce it. (Also giving dev teams the chance to check them into git.)
  - Whenever the schema changes, the json file changes.
  - Each file has a "modified" timestamp and when directus discovers a newer json definition (for example because of a git pull), it will offer a sync button to incorporate the changes into the db schema.
- Or if you prefer thinking in terms of migrations (because these json files can get messy): Each change to the schema creates a new migration file. 
  - Directus tracks which migrations have been run and when a new migration is discoverd, gives the developer an option to run it to update their database. (Or even run them automatically, analog to the EXTENSIONS_AUTO_RELOAD function, or on server start.)

- This is basically what we currently do through the schema snapshotting feature _202206
# discuss-collaborative/realtime
- ## 

- ## 

- ## 

- ## 

- ## [Add "Multiple Users Editing Page" Warning _202009](https://github.com/directus/directus/discussions/4793)
- Not sure about a locking system - that could really cause headaches. I do really like the idea of a warning however.
  - Maybe the warning should tie into the permissions system so that it's only triggered if someone is on a detail page for an item that they have permission to edit?

- Wordpress solves this by having a "Take Over" button, so no one is truely locked out, but they are made very aware something might be lost if they proceed.

- ## 🔀 [Users overwrite each others changes if they save the same collection item _202101](https://github.com/directus/directus/issues/3558)
- In this case, your reported situation feels like the expected behavior here. If user A is setting title to "Hello", while user B is making it "Hello World", whoever saves last is the one that becomes the saved value.

- ## 🤝🏻 [Realtime App Updates _202011](https://github.com/directus/directus/discussions/3221)
- Next to websockets, also worth looking into MQTT support (needs more research

- 🚀 This was implemented in version 10.3 _202306
  - Not so quick Connor! WebSockets support in the API was implemented, but the app isn't using it yet. That's what this feature request is about 
# discuss-editor
- ## 

- ## 

- ## 

- ## 🐛↩️ [CMD Z (or ctrl z) won't work after paste in blockeditor _202312](https://github.com/directus/directus/issues/20655)
  - It only applies when you paste more then one paragraph (so a new block is started in the json).
- This seems to be an open issue for editor.js (the block editor library)
  - [未修复 [Bug] Undo is ignored, when Copy-paste 2-3 paragraph from Wikipedia · codex-team/editor.js _202207](https://github.com/codex-team/editor.js/issues/2110)

- ## 📝 [Block Editor_202105](https://github.com/directus/directus/discussions/5776)
  - It would be great to add a Block Editor aka Medium or the new Wordpress.
  - The main usefulness of this versus a WYSIWYG editor is it can be controlled in a better way with only very specific output, which is then easier to transform with CSS/JS when in use.

- ✨ [已实现 Move in block editor exclusive extension _202305](https://github.com/directus/directus/pull/18525)
  - This first iteration is going to be just the "regular" JSON structure.

- ## 📝 [State of WYSIWYG interface _202003](https://github.com/directus/directus/issues/2613)
- we did not want to have two WYSIWYG editors in the core suite any longer, and TipTap was not feature-rich enough to be the single/only editor. Since TinyMCE is proven (WordPress) and quite feature-rich, we chose that library.

# discuss-news
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## [Collection folders as route _202209](https://github.com/directus/directus/discussions/15772)
- I think one "roadblock" for this structure is it's not possible to have 2 collections (or more precisely, 2 database tables) of the same name, as your example would require 2 articles tables and 2 news tables.
  - It should technically be possible to create a custom endpoint extension to do `/:folder/:collection` (eg. /app1/articles1, /app2/articles2) for a structure such as this
  - but then it would be more straightforward to use /items/articles1 and /items/articles2 instead.

- Perhaps an alternative structure would be to create an "app" collection (for app1 and `app2), and create relationships between the app collection to articles and news, so that it will be much easier to filter the results based on the app.

- ## [We're the small team behind Directus, an open-source data platform for managing any SQL database. We'd love your feedback before releasing v9! : r/programming _202103](https://www.reddit.com/r/programming/comments/m8hrgs/were_the_small_team_behind_directus_an_opensource/)
- it's free, self-hosted, has roles, webhooks, supports sqlite (because this was a small project), and supports (unlimited) locales. 

- ## 🚀 [Show HN: Directus – Free and Open-Source Headless CMS | Hacker News _201609](https://news.ycombinator.com/item?id=12496964)
- 🆚️ What is the difference with for example Active Admin (for Ruby on Rails)?
  - Certainly similar in concept. Other than the server-side language, the biggest difference seems to be how it saves the actual data. 
  - AA has file-based exports (csv, json, etc), not seeing a relational datastore (maybe Mongo?) – 
  - Directus is built on top of your custom-schema SQL database so it scales with large/complex datasets.
  - Also, while AA has a good set of simple features, Directus has comprehensive user management ACL, more robust file control, and is generally a bit more full-featured.

- What's the benefit of a headless CMS?
  - A headless (or decoupled) CMS is one that only manages content, as opposed to most “CMS” out there now that overreach by managing your views, templates, logic, routing, etc. 
  - That means that most current “CMS” are built specifically for websites only (more specifically, blogs), however a headless CMS only manages the data itself, and therefore is appropriate for anything from native apps, content syndications, interactive walls, or other data-driven projects. 
  - In fact a more important distinction is that it can manage content for MULTIPLE clients, for example a project where an app, widget, and website all pull the same content.
  - Since the content is decoupled from the application/view, you access your data through an API or SDK. For Directus, you can use our API, one of our language SDKs, or just connect to the database directly. That gives developers freedom over their workflow, process, libraries, and database architecture – which can expedite(加快；加速) development and optimize performance.
