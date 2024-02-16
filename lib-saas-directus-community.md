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

- ## 
# discuss-feat-version-history
- ## 

- ## 

- ## 🐛⚡️ [Performance issues with revisions and activity _202303](https://github.com/directus/directus/issues/17894)
- There is a problem with the reveisions and activity queries.
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

- ## [Content Versioning · Issue #19796 · directus/directus _202309](https://github.com/directus/directus/issues/19796)
- Comments and Shares might have to be adjusted to be branch-specific.

- Instead of saving just the delta to Directus Revisions, a secondary “cloned” table could be considered, however there’s some downsides

- ## ✨ [Save Item as Future Revision (Draft of Published Item) · directus/directus](https://github.com/directus/directus/discussions/2975)
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
