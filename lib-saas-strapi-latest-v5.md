---
title: lib-saas-strapi-latest-v5
tags: [changelog, roadmap, strapi]
created: 2023-12-15T19:38:46.847Z
modified: 2023-12-15T19:39:18.123Z
---

# lib-saas-strapi-latest-v5

# guide

```shell
npx create-strapi-app@5.0.0-beta.0 strapi5-app-beta0 --quickstart --ts
```

- [v5-features](https://docs-next.strapi.io/dev-docs/whats-new)
  - all entries will have uuids
  - Draft & Publish feature has been fully reworked.
  - Strapi 5 now use documents and introduces a new Document Service API to replace the Entity Service API from v4

- v5-changes
  - [v4 to v5 breaking changes](https://docs-next.strapi.io/dev-docs/migration/v4-to-v5/breaking-changes)
  - 替换默认markdown编辑器时，v4可用wysiwyg/richtext，v5只能richtext
  - `i18n` is now part of the strapi core
  - `helper-plugin` is deprecated
  - remove old plugin generator in favor of `plugin:init`.

- resources
  - https://v5.contributor.strapi.io/docs/intro
  - [rfcs v5](https://github.com/strapi/rfcs/pulls?q=is%3Aopen+is%3Apr+label%3Av5)
  - [5.0.0 Milestone](https://github.com/strapi/strapi/milestone/256)
# features/rfc
- [Q2, 2024 - Strapi 5 | Content Editing XP | Strapi](https://feedback.strapi.io/customization/p/q2-2024-strapi-5)
  - two exciting new features: Draft & Publish; Content History

## ✨ draft-publish

### [Q1, 2024 — Draft & Publish | Content Editing XP | Strapi](https://feedback.strapi.io/customization/p/q1-2024-draft-publish)

- > Allow users to manage content by having a published and draft content at the same time.

- We tried the content versioning plugin but it didn't work with related content or unique fields, so we are back to waiting for this to be released. Does anyone know if there is an eta?

## ⚖️✨ [v5 Database Design_202309](https://github.com/strapi/rfcs/blob/v5/database/rfcs/xxxx-v5-database.md)

- We need to support development of new features. Most of them are going towards a more CMS like model. 
  - to support this approach we will introduce the notion of documents & links.
- Bringing new features that were not possible in v4. The most important ones:
  - Draft and Publish: simultaneous draft and published entries, leading to the idea of Documents.
  - Synchronized relations across locales: v4 users requested the ability to share the same relation across multiple locales. This led to the concept of Links

- Documents are introduced in v5 as a way to group multiple entries. 
  - That is implemented by adding a new `document_id` column in entries
  - all the variations of that document will have its own column in every entry

- in V5, all identifiers (entry ids and document ids) will now be universally unique identifiers (UUIDs).
  - Previously, transferring data between databases while retaining the same entry IDs was not possible, due to the use of incremental ids.
  - UUIDs, being non-sequential and randomly generated, prevent such easy discovery.

- When relating an article to a specific author in V4, only articles and authors of the same locale could be linked, because localizations were not really grouped in a single document.
  - Links will solve this by referencing a document as a whole, not a specific locale

### 👥 [[V5] Database · strapi/rfcs](https://github.com/strapi/rfcs/pull/52)

- The idea is not to remove the database lifecycles, but to add new ones on the Service layer. Ones where you can hook to listen to document changes.
  - The database lifecycles will still be maintained and what we could do is an evaluation of which issues there could be on db lifecycles when introducing documents.
  - At the moment I can not think of any, and we plan to internally use the db lifecycles too

- What benefit would you see of having this in the ES(entity-service) rather than on the database layer? 
  - ES layer also knows about components and dynamic zones. so has more context. and this would mean if you blocked a request it would also block the components. and not only the highest level of the content-type.
- Leaving lifecycles in DB is a must in V5 imo, as we aim to keep as much compatibility as possible.
  - Understandable I am not saying to remove them I am saying maby add a second layer of them.
- Agreed but I also agree with boegie here around implementing ES lifecycles too so each user can pick the right spot for their code to achieve what they want.
  - Yes! The current proposal is to create lifecycles on the Document Service layer, which also will be responsible to handle components. In my opinion, having lifecycles on that layer will make the DB lifecycles much less necessary for people (but we will keep them neverhteless)

- I am worried too much will be abstracted to the JS/TS side in strapi and the databases (and the data they store) will be useless outside the strapi application. Keep in mind several strapi devs are working on applications that store more than just marketing copy

## ⚖️ [v5 Content API Design](https://github.com/strapi/rfcs/blob/v5/content-api/rfcs/xxxx-v5-content-api.md)

- V5 Content Engine requires some breaking changes to the API, It is also the opportunity to simplify the API Response format following user feedbacks.
  - The main point of this RFC is to propose a simplified and v5 compatible format while offering a smoother migration path with a legacy format.

- Use the internal `documentId` as the only identifier the ContentAPI knows about.
- introduction of a new version of the API response format that flattens the structure
  - No more `data.attributes` , id/title/relation作为直接属性
- Metadata are added information that you can’t work with directly through the main content API endpoints & don’t work the same way as simple attributes that you can select/filter/orderBy

### 👥 [[V5] Init Content API RFC · strapi/rfcs](https://github.com/strapi/rfcs/pull/53)

- Other question I see no where in the RFC how you would reference a specific entry in the document.
  - the document is a virtual thing, fetching a document will always return the content of a single entry. (Based on filters provided or default filters)
  - if you do (just an example) ?locale=en&state=draft you will get the draft entry for the english locale and by default you would get your default locale and the published version of your document.

- After carefully considering the different Options, Option 1 is the most viable one for v5 and is the one we will be moving forward with.

## 🗑️ [fe-apis · Introduce typed imperative APIs as opposed to InjectionZones](https://github.com/strapi/rfcs/blob/v5/fe-apis/rfcs/0056-FE-APIs.md)

- proposes new public facing APIs aimed at plugin developers to be able to augment the EditView of the content-manager, the need came from the design proposals of Draft & Publish and would most likely be implemented only in V5 of the product under the Draft & Publish scope.
- The `addDocumentActions` API is a new API that allows you to add actions to be rendered in the DocumentActions menu (this is new to V5).

### 👥 [[V5]: FE APIs](https://github.com/strapi/rfcs/pull/56)

- Introduce typed imperative APIs to inject DocumentActions, SideBarPanels and DocumentHeaderActions as opposed to InjectionZones in V5.

- I like the idea but why remove the InjectionZones and not build this feature on top of InjectionZones. so it can be an InjectionZones or documentActions, SideBarPanels and DocumentHeaderActions

## 🎨 [RFC: Design System V2 ](https://github.com/strapi/design-system/discussions/1687)

# discuss-v5-breaking-changes
- ## 

- ## 

- ## 🌐️ [chore: refactor i18n _20240220](https://github.com/strapi/strapi/pull/19555)
  - re-implements i18n admin side
  - refactors i18n to use redux-toolkit-query

- [chore: make i18n plugin a dep & required _20240319](https://github.com/strapi/strapi/pull/19843)
  - Add i18N as default & pre installed plugin

- ## lifecycles (in plugins) have stopped working?
- https://discord.com/channels/811989166782021633/1095091586452426824/1224045126083416164
  - I just realized this major thing. Because the draft and the published version of a document are 2 entries, the `beforeCreate` lifecycle will run both on creating the draft and publishing it. 
  - I'm pretty sure lots of people have created lifecycles that aren't supposed to run on both. I think this deserves attention in the breaking changes.
  - everytime i press publish, the `beforeCreate` lifecycle run

- [v5 documents completely change how lifecycles work, not documented as a breaking change _202404](https://github.com/strapi/strapi/issues/19982)
- 
- 

- ## Is there any v5 engineer to help me migrate entityService decorator logic to documentService?
- https://discord.com/channels/811989166782021633/1095091586452426824/1222904152032546856
  - In v5 decorators no longer exist they will be replaced by documentService Middlewares that are currently not yet fully stable 
  - Still there is a version of the new documentService Middlewares in strapi 

- ## I would like to know details on transformer i would like go through and maintain it. _202403
- https://discord.com/channels/811989166782021633/1217462664809152553/1219677189801246863
- just a heads up it won't be needed for Strapi 5 as we plan on baking in support into Strapi 5 to simplify the structure and be able to use the v4 syntax throughout Strapi 5. 
- Publisher might also be superseded by something from Strapi 

- https://discord.com/channels/811989166782021633/1095091586452426824/1222905448722595840
- what's the v5 way to transform response?
  - Document middleware or route middleware.

- from the doc, route middlewares require me to enumerate the model uid. but I need to modify the response for several routes by a rule.
  - You can dynamically inject route middlewares in register.(js/ts)
  - And I assume the same thing is posible for document service middleware but I would have to test that out.
# discuss-v5-changelog
- ## wip

- [feat: webhooks ](https://github.com/strapi/strapi/pull/20129)

- [feat(i18n): non localized fields ](https://github.com/strapi/strapi/pull/19720)
  - Implement non localized fields in v5 using document service middlewares

- [Feat(releases): Bulk Release ](https://github.com/strapi/strapi/pull/19891)
- [Feature: ability to add custom auth providers in plugin ](https://github.com/strapi/strapi/pull/15559)

- 
- 
- 

- ## 

- ## [feat(admin): rbac middleware _20240328](https://github.com/strapi/strapi/pull/19949)
  - so we can use rbac middleware across the app generically, not just isolated to the CM with a weird redux workaround
- adds an RBAC api class to run a middleware system
- removes the content-manager RBAC manager from redux.
- `useRBAC` now returns an array of permissions
- Internally `useRBAC` now preferably wants an array and ignores keys of the object, so the action names are derived from the `action` property of the `permission` .

- ## 🗑️ [chore: remove old plugin generator in favor of `plugin:init` _20240322](https://github.com/strapi/strapi/pull/19875)

- ## [feat: add drag-and-drop to relations _20240315](https://github.com/strapi/strapi/pull/19788)

- ## [feat(cm): reimplement relations for draft & publish _20240313](https://github.com/strapi/strapi/pull/19642)

- ## 🗑️ [chore: deprecate entity-service and delegate to document service _20240314](https://github.com/strapi/strapi/pull/19728)

- ## [feat: add basic pagination to history frontend _20240311](https://github.com/strapi/strapi/pull/19729)

- ## ✨ [feat(cm): add content history _20240306](https://github.com/strapi/strapi/pull/19315)
  - Adds the content history feature

- ## [feat(cm): D&P pt2 _20240223](https://github.com/strapi/strapi/pull/19380)
  - chore: use document from create and update

- ## [chore: merge draft & publish into history _20240209](https://github.com/strapi/strapi/pull/19632)
- update History with new v5 APIs 

- ## [feat(content-manager): display history versions _20240210](https://github.com/strapi/strapi/pull/19458)
- > This PR displays the content of history versions on the history page. We display all the fields in disabled mode.

- To look at previous versions of your content.

- ## ⌛️ [feat: list history versions in the history page sidebar _20240206](https://github.com/strapi/strapi/pull/19421)
- Displays a list of history versions in the history page sidebar

- [feat(history): add history-version content type _20240125](https://github.com/strapi/strapi/pull/19316)
  - Registers a history version content type. 
  - It's a content type for now, but it will converted to a model later when Alex finished his database model API proposal.

- ## [chore(cm): refactor content-manager _202401](https://github.com/strapi/strapi/pull/19341)
- this PR absolutely destroys the CM. But, it shakes off loads of tech debt, makes data transformations clearer and isolated to one place. It also introduces new public APIs for users
  - refactors the CM to be more driven by domains

- ## ✨ [feat: Draft & Publish V5 _20240126](https://github.com/strapi/strapi/pull/18941)
- this is an iteration of handling Documents and D&P in the content manager.
  - Refactored Collection-Types contracts api to return document metadata (available locales and publication status of a document)
  - Refactored entity-manager to work with the document service (we will rename it to document-manager)
  - Refactored collection-types controller to work with documents.

- ## [chore(cm): refactor to use redux-toolkit-query](https://github.com/strapi/strapi/pull/19281/files)
  - 从 react-query.v3 迁移到 redux-toolkit-query

- ## ✨🚨 [feat: Document Service _202311](https://github.com/strapi/strapi/pull/18558)
- Implementation of the document service.

- ## ✨ [[feat]: feature flags _202311](https://github.com/strapi/strapi/pull/18871)
- Introduces a new configuration file: features.(j|t)s. 
  - It's also passed to the admin configuration so future flags can be checked via `window.strapi.future.isEnabled('contentReleases')` .
- This pull request first appeared in v4.16.0

- ## [[v5] use fetch api for strapi.fetch _20231122](https://github.com/strapi/strapi/pull/18508)
- Replaces `strapi.fetch` object with a native `Fetch` wrapper instead of a `node-fetch` wrapper
- Removes dependency for `node-fetch` throughout strapi

- ## 🆔️ [V5: add Document ID _20231115](https://github.com/strapi/strapi/pull/18303)
- Adds document id in strapi/strapi; It defaults to a cuid id
- Doc ID is a hidden and not writtable attribute in CTB and Content Manager
- Added to reserved names

- ## ⤴️ [TS @strapi/strapi _20230921](https://github.com/strapi/strapi/pull/17960)
  - Migrate strapi/strapi to ts
- [feat: Migrate @strapi/admin server to typescript _202311](https://github.com/strapi/strapi/pull/18232)
- [chore(admin): convert review workflows page to TS _202312](https://github.com/strapi/strapi/pull/18984)

- ## [Notice: Community PR Change Freeze for 2023 Holidays & v5_202310](https://github.com/strapi/strapi/issues/18618)
- As the year is winding down and with the holidays coming up we will be placing a community pull request change freeze into effect until March 2024.
  - any new PRs submitted after October 31st (Tuesday) will be closed due to the change freeze unless an exclusion is applied.
  - we have started our major development on Strapi v5 and want to try and limit the amount of merge conflicts that we have between the main branch for Strapi v4 and the v5/* branches.

- ## 🗑️ [Axios instance in strapi - Discussions - Strapi Community Forum](https://forum.strapi.io/t/axios-instance-in-strapi/30425)
- `axios` instance will be deprecated in v5 use `useFetchClient` instead

- ## ⚖️ [Notice: Requesting community feedback on v5 RFCs_202309](https://github.com/strapi/strapi/issues/17958)
- When we launched Strapi v4, we released a few RFCs but did not get enough feedback on them back then and there was quite a bit of feedback shared around some of the changes in v4 that we did and for Strapi v5 we are attempting to prevent making that mistake again. 
- Below you will find 2 RFCs we are making public for community review
  - v5 Database Design
  - v5 Content API Design

- Some other RFCs we are currently working on for v5 are (these aren't confirmed yet, some are still under discussion internally)
  - v5 Content Type Design
  - Environment variable fallbacks for all config options
  - Moving Content-types to their own directory (outside of the API directory to decouple the CTs from the Controllers/Services/ect)
  - Generating complete (but commented) config files
  - Plugin Development tools

- Some of you may have already noticed but we are also in the process of completely converting the Strapi codebase to Typescript and building internal types + the currently WIP "consumer" types
  - For these due to their complexity we aren't taking comments on as it's a massive undertaking and is happening within the v4 lifecycle.

- ## [Notice: Stability and changes to our release process (v4.15.x through 2023)](https://github.com/strapi/strapi/issues/18841)
- here is our internal roadmap for Strapi v5

- Our primarily reason for working on v5 is to be able to release content versioning, content history, and draft & publish (v5 version). 
  - For certain features (mainly content versioning and content history) to be developed we need the breaking changes from v5 hence the focus and deadline as we have already delayed these features for over a year after we identified that v4 changes were not enough to build these features.
# discuss-v5
- ## 

- ## 

- ## 

- ## 

- ## what are the actual improvements of Strapi v5? _20240327
- https://discord.com/channels/811989166782021633/1095091586452426824/1222274834952622081
- Most are internal breaking changes we needed to make for future feature development, 
  - the largest change was the rewrite of the draft + publish system as you can now have a single draft of an already published entity. 
  - In the future this will be expanded with multiple drafts (effectively content versioning).

- ## ⌛️ [How to create archive for blog in strapi and nextjs? _202309](https://forum.strapi.io/t/how-to-create-archive-for-blog-in-strapi-and-nextjs/21247/11)
- the whole reason we need v5 is to build content versioning. We made quite a lot of changes in v4 to try and achieve what we wanted to do but hit some breaking change blockers that required some additional things so it got delayed til v5.

- ## webpack requires a decent amount of ram to build the react output
- https://discord.com/channels/811989166782021633/1187470968009011330/1187486143797792818
  - that's one reason why we are switching away from webpack in v5

- ## On v5 I'm suggesting to have groupBy (and other aggregation methods) within strapi query API, instead of raw sql.
- https://discord.com/channels/811989166782021633/1095091586452426824/1192164947082346546
- It's not something we will do in v5 initially and at the moment I'm not aware of any plan to do so but that's not to say that we can't.
- For groupby/aggregations we do have two feature requests for those
  - Virtual fields are technically already possible but requires a little bit of coding to do, I've done something similar by injecting a custom UUID field and automatically setting it using lifecycles and forcefully setting the "view" as disabled so it's read-only in a v4 projects. Given it's not a native virtual field but functionally it gets to the same end goal

- ## 🗑️ Strapi team has acknowledged the limitations of the injection zones and have proposed an alternative solution that would deprecate the current injection zones for V5
- https://discord.com/channels/811989166782021633/1196439693877854250/1196443802081185942

- https://discord.com/channels/811989166782021633/1095091586452426824/1179487055420596264
  - You can't control what people do in their user applications though? 
  - I get that you want more InjectionZones, but we're not doing it for V5. 
  - 👉🏻 We've been clear that we're not removing any InjectionZones on V5 either but the direction is not to carry on with them

- ## [refactor(core/strapi): move components to registry _202310](https://github.com/strapi/strapi/pull/16273)
- We are starting to work on v5 and won't be adding such a big change in v5. FYI we already created a registry for compos in v5 even if we are not ready yet to allow components coming from plugins this is a 1st step into that direction.

- From what I saw in the repo, in the v5 they already are preparing the ground for that. Components were moved to the registry pattern in v5, and should be easier to move on with implementing plugin components.

- [feat(core): load components from plugins ](https://github.com/strapi/strapi/pull/16132)

- ## Is grouping by relation fields for rest apis going to be available in v5? For example : /api/jobs?groupBy=company
- https://discord.com/channels/811989166782021633/1095091586452426824/1206516283600797717
- I don't believe so. Initial stable release of Strapi v5 is mainly around implementing the breaking changes we need to build some features

- ## 🎯 would you advise to start a new product on the V5 or V4 and then migrate ? _20240210
- https://discord.com/channels/811989166782021633/1095091586452426824/1205577881443639417
- I'd start with v4 for now, we don't expect v5 to be considered "stable" until June-ish
  - the Beta release will still be open to some breaking changes and expect a lot of bugs between the beta <> stable

- https://discord.com/channels/811989166782021633/1095091586452426824/1203012293806264372
- Timelines are in the v5 community committee call but roughly (these might be subject to change)
  - v5 public beta: ~end of march
  - v5 public stable: ~end of june

- the new draft & publish system (having a published version and a single draft version at the same time) will be in v5 stable but not 100% sure about beta. 

- ## I'm quite concern about the new API Format _202401
- https://discord.com/channels/811989166782021633/1095091586452426824/1202240724775747634
- You will still have the transformer plugin to change it back to v4 format if strapi where to not suport it

- There will be a legacy v4 option that you can apply to the request to get the v4 format until you have time to migrate over to the v5 format so think of it like a build in transformer
  - We saw the pain of v3 to v4 and didn't want to replicate it

- ## Apart from maybe breaking compatibility with certain plugins, will the upgrade process to V5 be a fairly seamless transition, or is this going to require a fresh install?
- https://discord.com/channels/811989166782021633/1095091586452426824/1200565021181214731
- It should be fairly painless, we demo'ed it in the January call which will be on Youtube soon but the general gist of the migration:
  - The code changes and all the codemods we can automate will update most of your code automatically 
- There won't be any data migration scripts you need to run manually like v3 -> v4 since it's now going to be baked right into Strapi 5 and run on boot (it'll detect the state of your database and if it's a v4 or v5)
  - You will not be able to go from Strapi v3 to v5 directly, you have to be on Strapi v4 first. 

- https://discord.com/channels/811989166782021633/1095091586452426824/1197515666685689856
  - Currently, there are no plans to add new features to the media library for V5.

- ## we are currently heavily focused on the development of Strapi v5 _20231118
- https://discord.com/channels/811989166782021633/811989167357689918/1175206357339734137
  - we will effectively be heavily slowing down on v4 feature development will largely focus on v4 stability for the remainder of 2023
  - Our timeline for Strapi v5 stable will be around the end of Q1/beginning of Q2 2024 with several weeks of Alpha/Beta testing
