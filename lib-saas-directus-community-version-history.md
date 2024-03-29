---
title: lib-saas-directus-community-version-history
tags: [directus, version-control]
created: 2024-03-29T14:00:28.152Z
modified: 2024-03-29T14:00:38.977Z
---

# lib-saas-directus-community-version-history

# guide

# discuss-stars
- ## 

- ## 

- ## 🌵 I personally love the branch concept, but I'm 99% sure it would be lost on the newsroom. _202309
- https://discord.com/channels/725371605378924594/1144680972382646455/1149334537474691133
  - My view is very narrow here (using Directus to create and publish news content for the web), but I think there are existing patterns that will be more universally understood.
  - WordPress, for instance, have the concept of 'save' and 'publish/update'.
  - Imo, `save` should always be a safe action (pre and post publishing). `Publish/update` on the other hand has weight & consequence, and should always be a deliberate action.
- I'm thinking we should/could add a toggle that switches between "simple" draft/publish and "full" branching modes as a setting
- Any change on a branch itself is a revision, so every branch has it's own revision history as well 

- just out of curiosity: is it based on Git internally?
  - Nope

- I like this idea of a "simple mode" and an "advanced mode"
- simple mode is a single default branch (so no naming required)
  - every new version created in simple mode is a new entry in that default branch (thus superceding any previously existing versions that were created in simple mode)
  - when the simple mode branch is "promoted" or whatever term we want to use, there would be no "merging" step, the latest version in the branch would simply be made the main version exactly how it is

- I'd want it to be possible to create both simple and advanced branches on the same item

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
# discuss-not-yet
- ## 

- ## 

- ## 

- ## [Proposed Content Versioning Enhancement for Directus _202311](https://github.com/directus/directus/discussions/20372)
  - Require a permission for users to promote a version to main.
  - Allow admins to set the main version as read-only for a user.

- ## [Content Versioning _202309](https://github.com/directus/directus/issues/19796)
- Comments and Shares might have to be adjusted to be branch-specific.

- Instead of saving just the delta to Directus Revisions, a secondary “cloned” table could be considered, however there’s some downsides
# discuss
- ## 

- ## 

- ## I'm trying to setup previews using content versioning. _202312
- https://discord.com/channels/725371605378924594/1151320093565927504/1184512066086785044
  - When fetching a page by version using REST I do get a response. But I expected to get the complete page, not a modified object with create, delete, update. Is this the intended result?
  - If it's meant to work this way, I guess I need to fetch the complete page without version, then the version diff and merge them both for the CMS preview?

- Correct. content versions only stores a delta not the complete object 

- ## ⌛️ [Save Item as Future Revision (Draft of Published Item)](https://github.com/directus/directus/discussions/2975)
- This has been released in 10.7_20231028

- ## [delta stored but not displayed _201611](https://github.com/directus/directus/issues/1301)
  - I noticed that the delta for changes are stored in the `directus_activity` table, but isn't displayed on the interface itself. 

- you're correct, we're storing the full item at each change, as well as the delta (with user for accountability). Activity is shown inline with comments at the bottom of the Item Detail page. And while we used to have an interface for "rolling back" we've disabled it due to unintended and far-reaching consequences of relational data.
  - We're actually in the middle of a design refresh that addresses this issue which will be rolling out in v6.5

- [how to restore revision via gui? _201709](https://github.com/directus/directus/issues/1809)
  - the revisions are stored in the `directus_activity` table for all changes, but we don't have a GUI for restoring previous deltas yet. 
