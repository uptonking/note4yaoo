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

- ## 请教下 表结构更改了（使用外部数据库工具修改的） 除了重启directus以外，有办法热加载表结构吗？ _20231214
- https://discord.com/channels/725371605378924594/946422284426551346/1184739818568171620
- 可以试试看清除缓存 https://docs.directus.io/reference/system/utilities.html#clear-the-internal-cache

- 感谢 亲测有效，之前一直是重启容器来重新加载schema， 最近突然重新要5min左右， 所以在寻找原因和方案。 
  - 测试/utils/cache/clear 接口成功实现了 新增表/字段后的变更

- ## ✨ [[RFC] Directus Offline First SDK_202303](https://github.com/directus/directus/discussions/17808)
- I think RxDB is an excellent choice for responsive offline-first applications. During my initial research I found multiple points, why I wouldn't want to use it
  - It ships a whole db with 45kb gziped
  - Interfacing with IndexedDB is via a commercial plugin
  - I want to interface with any HTTP endpoint and not rely on GraphQL or other demanding server side requirements
- At the end of the day, it is a tradeoff. RxDB can free you from getting locked down to one specific backend, but it has its drawbacks.

- 💡 Conflict Resolution Approaches: 4 methods for handling edit conflicts
- Generally, conflict resolution falls into four categories, with developers selecting the most suitable strategy. 
  - Performance and usability with CRDTs have come a long way since their inception 2011. 
  - For most small to mid-scale Directus use cases CRDTs will work fine. They will probably still be a rarely used data type.
- Last Write Wins (LWW): 
  - This default method resolves conflicts by prioritizing the most recent write operation in a CRUD app. Earlier edits are overwritten.
- Operational Transformation (OT): 
  - This method can be implemented using a Directus flow operating on the `article_event` data, updating the articles collection accordingly.
- Conflict-free Replicated Data Types (CRDTs): 
  - This method employs data structures that automatically merge, resolving conflicts. 
  - CRDT implementation would be facilitated by Directus' support for views in relational databases. 
  - However, developers should be be able to fully choose their preferred implementation, because developers may utilize resources like Yjs or Automerge.
- Return Conflict List to Last Writer or Arbitrator: 
  - This approach requires handling user responses to conflicts, similar to git. 
  - It places a significant burden on users and developers, and should only be considered as a last resort for specific use cases.

- I'm very curious to hear some more thoughts around the different conflict resolution techniques though. It sounds like that's something that you might have to be able to override method call to method call (eg what happens if you need a different resolution for articles than for authors etc) 
  - Totally agree. CRDTs are a data model problem. A CRDT – as opposed to a normal data type – might require that you send different (or usually more) data to the server. The proposed API still expects you to be explicit about what you send to the server.
# discuss-feat-version-history
- ## 

- ## 

- ## 🐛⚡️ [Performance issues with revisions and activity _202303](https://github.com/directus/directus/issues/17894)
- There is a problem with the revisions and activity queries.
  - When I navigate in my directus instance, I regularly get a popup that says that a request failed with status 504.
  - When I look in my devtools, it's the requests fetching the revisions for a particular item.
  - I have to purge the activity and revisions often to avoid that, even though I don't have a particularly big database (there are ~ 1 million in activity and 500 000 in revisions).
  - I have to purge the activity and revisions often to avoid that, even though I don't have a particularly big database (there are ~ 1 million in activity and 500 000 in revisions).

- Same issue here. Revisions take a really long time to load. Have about 700, 000 records in the directus_revisions table.

- 💡 I added an index on the item column of the directus_revisions table and it greatly improved performance. It would be great if it was added by default or possible to enable as a config flag.

- On top of the index suggestion we should also have a configuration to limit the amount of revisions per item, so they are rotative. For example, only save last 0, 5, 10, 20, 50 revisions per item. Probably can be configured per collection.
  - This is because Directus can crash because it does not have sufficient memory (OOMKilled - Out of Memory). 
  - It happens when the machine has limited memory and there's some WYSIWYG, JSON or any other column that can have a great amount of data. 
  - Because `directus_revisions` will store every column of the record in data and will store the huge data column in delta, it can crash sooner than later.
- Another thing we can do is truncate data and delta and only retrieve those columns in full when we want to restore a specific version or when we retrieve that single revision 

- I implements two new env vars to control the max retention in time for activity and revisions separately.

- Also want to mention this became more trickier with the addition of Content Versioning. Now, we cannot simply just remove the records from Activity and Revisions. We must check if field version is populated in directus_revisions and not remove it if that's the case

- ## [Content Versioning _202309](https://github.com/directus/directus/issues/19796)
- Comments and Shares might have to be adjusted to be branch-specific.

- Instead of saving just the delta to Directus Revisions, a secondary “cloned” table could be considered, however there’s some downsides

- ## ✨ [Save Item as Future Revision (Draft of Published Item)](https://github.com/directus/directus/discussions/2975)
- This has been released in 10.7_20231028

- ## [delta stored but not displayed _201611](https://github.com/directus/directus/issues/1301)
  - I noticed that the delta for changes are stored in the `directus_activity` table, but isn't displayed on the interface itself. 

- you're correct, we're storing the full item at each change, as well as the delta (with user for accountability). Activity is shown inline with comments at the bottom of the Item Detail page. And while we used to have an interface for "rolling back" we've disabled it due to unintended and far-reaching consequences of relational data.
  - We're actually in the middle of a design refresh that addresses this issue which will be rolling out in v6.5

- [how to restore revision via gui? _201709](https://github.com/directus/directus/issues/1809)
  - the revisions are stored in the `directus_activity` table for all changes, but we don't have a GUI for restoring previous deltas yet. 
# discuss
- ## 

- ## 

- ## 
