---
title: lib-saas-strapi-community
tags: [community, lowcode, strapi]
created: 2023-11-28T19:03:50.762Z
modified: 2023-12-15T17:04:36.589Z
---

# lib-saas-strapi-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 🆔️ [Data transfer/import _202403](https://forum.strapi.io/t/data-transfer-import/36810)
- In the data transfer / import/export data options it’s possible to exclude files, config etc… Is it possible to exclude certain tables, for instance user permissions tables?
  - Sadly that is not possible as of yet. It is just a full on db overwrite. It’ll wipe anything that’s already in the db and fill it again with the dump
  - I believe that was because of an issue with auto-increment id’s not working properly across multiple dbs
  - 💡 Though as of v5 all entries will have uuids to identify them, so technically this can be solved in v5

- ## [Is it possible to connect an existing database with Strapi CMS? - Stack Overflow](https://stackoverflow.com/questions/62656356/is-it-possible-to-connect-an-existing-database-with-strapi-cms)
- It seems the only answer is no, because Strapi is not schema-agnostic: you must adopt their database structure to use Strapi.
- The best way is to create a new database with the same structure but created with strapi and after migrate the data.

- ## [Strapi Hide Content Type - Stack Overflow](https://stackoverflow.com/questions/65846609/strapi-hide-content-type)
- You can extend the content type plugin to make updates to the content-type's schema.
  - In Strapi v4 it is `"visible": false`

- ## 🔒 [Customise hide areas of the Admin interface per roles _201804](https://github.com/strapi/strapi/issues/931)
- your can
  - uninstall de content type builder when you're done using it (plugins link on the admin)
  - create role for your users with specific permissions for each content type
  - the admin is currently available to admin users only
  - you can display specific content types in the admin

- [Allow other User roles access to Admin Panel _201805](https://github.com/strapi/strapi/issues/1152)
- 
- 
- 

- ## 🕵🏻 any chance of getting a query engine decorator?  usefull for fake multitenency
- https://discord.com/channels/811989166782021633/1218214776405233754/1218217608676114673
- it was a firm no. I think it's not the technical direction we want to take and it wasn't a great pattern to implement in the first place, we'd rather go forward with lifecycles and middlewares, like the doc service has

- 📡 We are stripping out the decorators we were using before anyway and moving to middlewares/lifecycles ourselves

- What I meant is can we get any way in the query engine to return before doing the DB query and return a result so we can do caching. since to my knowledge the only way to get out of it is trowwing a error. what means I can't return data I think I just found myself a workaround lol

- ## 🐛 [How do I create a new Content type ? : r/Strapi](https://www.reddit.com/r/Strapi/comments/153ntvx/how_do_i_create_a_new_content_type/)
- you’ve never been able to edit content definitions in production
  - Strapi is a bootstrapped API - more than a CMS. Development mode content type creation makes perfect sense given the way Strapi generates the schema, controllers and models for the endpoints.

- Strapi has been designed to be configured in development (local environment) and deployed in production. This is a best practice to make sure editors do not change the content structure in production, which could entirely break the frontend application. 
  - Strapi is a CMS that has been strongly designed for developers and is deeply integrated with their workflows.

- ## 🐛 [Question: What are the main pain points you have using Strapi? (Episode 5) _202305](https://github.com/strapi/strapi/issues/16873)
- Nested components is my main pain point personally. It is supported at the code level at least now, but becomes an issue to maintain for those less knowledgeable with strapi. supporting real nested component at more than just 2 level would be a major thing as it permit the data to be way more self container and reusable.

- A big pain point when building CRUD apps is implementing security policies. Almost every "create", "delete", or "update" route needs an is-owner policy added to make sure the public endpoint isn't being used to delete entries created by other users.
  - It would be great if in v5 we had a system that made implementing this additional security layer possible from the admin panel. 

- Collapsable Menus

- Too many breaking changes between minor and even patch updates and not sticking to semantic versioning.
  - v4.5 aimed to prepare the database for the relation sorting, v4.6 brought the relation sorting but it didn't fully work until v4.6.x and even broke some Strapi instances.

- Not being able to have conditional logic for fields.

- ## 🤝🏻 [Is it possible to create a collaborative platform with Strapi? - Questions and Answers - Strapi Community Forum _202211](https://forum.strapi.io/t/is-it-possible-to-create-a-collaborative-platform-with-strapi/23815)
- definitely possible but it will require some coding and bending. Afaik you can’t really create this just by clicking around in the admin panel.

- ## 💰 [Can I use strapi free in my self-hosted server? - General - Strapi Community Forum_202304](https://forum.strapi.io/t/can-i-use-strapi-free-in-my-self-hosted-server/27666)
- The only restrictions on the free version is that audit-logs and Review Workflows are not available

# discuss-strapi-mongo 🍃
- ## 

- ## We probably will never bring back MongoDB ourselves. _20240302
- https://discord.com/channels/811989166782021633/1095091586452426824/1213168058454114315
  - We are basically "all in" on relational databases.
- DynamoDB is still a NoSQL database and we basically exclusively use Knex.js and would really only work with the databases they support (even that though we don't ever plan on adding support for say Microsoft SQL or OracleDB because of licensing).

- ## [Is MongoDB a terrible choice for Strapi? : Strapi _202207](https://www.reddit.com/r/Strapi/comments/w9069u/is_mongodb_a_terrible_choice_for_strapi/)
- Not a terrible choice, in general: we used MongoDB for all of our v3 instances. However, Mongo is hugely inefficient if you have nested relations between collections (though this makes sense - mongo isn’t a relational DB).
  - In any case, v4 dropped support for Mongo. We’ve been migrating to v4 with Postgres and we’ve seen some great performance gains, even in applications with very few relations.

- ## 🍃📡 [MongoDB support in Strapi: Past, Present & Future _202106](https://strapi.io/blog/mongo-db-support-in-strapi-past-present-and-future)
- Since 2017 and Strapi Alpha, we have always supported SQL databases such as MySQL, PostgreSQL, SQLite, MariaDB, and the document database MongoDB.
- I posted a message on the Strapi forum announcing that we were thinking about officially dropping our support for MongoDB in Strapi. 
  - 💡 In short, having to support two different connectors (SQL + MongoDB) is slowing down our product developments, and MongoDB usage represents less than 0.4% of all the Strapi projects (data is anonymously collected via Telemetry system).
  - For the beta and stable release of the Strapi v4, Strapi won't support MongoDB natively, and no connector will be available (yet).

- [Why MongoDB is not available in Strapi V4 ? _202111](https://github.com/strapi/documentation/issues/520)
  - we won't maintain a MongoDB connector in v4. If MongoDB (the team) builds one that is up to them.
- First-party support has been dropped, there will be an "official" plugin to connect, but not immediately at release.

- ## 🍃 [MongoDB compatibility delayed on v4 - Discussions - Strapi Community Forum _202104](https://forum.strapi.io/t/mongodb-compatibility-delayed-on-v4/4549)
  - When we re-developed from scratch Strapi, in 2017, we decided to use more specific ORMs. One for SQL database called Knex, and one for NoSQL MongoDB called Mongoose. Why? MongoDB was huge at that time. 
  - MongoDB wasn’t the recommended starting database to test and try Strapi. It has been replaced by SQLite
  - Drupal, WordPress, and many other CMSs restrict to one database, often SQL one and these are successful projects.

# discuss-editor
- ## 

- ## the new editor just went stable in 4.15, but are there future plans to allow the Slate instance to be extended with plugins, or the UI to be extended? _202310
- https://discord.com/channels/811989166782021633/1167459042260697238/1167459042260697238
- It's something we currently have in mind, but no decision has been made yet.
- Eventually we'd like everyone to use the Blocks editor, as it's a much better UX, and the JSON format can be more powerful on the frontend too. But we're not there yet. We need:
  - more features so that the value over markdown is clear. 
  - a more mature renderer ecosystem, and potentially HTML/MD conversion tools. 
  - a migration script or tool to ease the transition of existing fields
- Once we have all of that we can look at deprecating and eventually removing markdown

- ## we are going to be building our own WYSIWYG editor in the next few months that will be based on Slate (with a fallback to Lexical if we need to) _20230901
- https://discord.com/channels/811989166782021633/811989167357689922/1146841513742045264
  - and will be part of the v4 lifecycle so at some point in the future you will have a more robust option native to Strapi that doesn't rely on a 3rd party.

- ## 📝 [Q3, 2023 — Better Rich Text Editor | Content Editing XP | Strapi](https://feedback.strapi.io/customization/p/q3-2023-better-rich-text-editor)

- [Change Strapi's Default WYSIWYG to a more feature rich Editor_202202](https://github.com/strapi/strapi/issues/12440)

- The current and previous (v3) WYSIWYG editor are more so basic markdown editors
  - Our current editor only supports the bare minimums in terms of markdown support (eg no tables, ect) and support for things like inline youtube video previews, ect are a bit more complex to handle properly.
  - There is already community options in both v3 and v4 such as CKEditor 5, React MD, Toast UI, and Editor.js. I do think we should ship something more feature complete then forcing everyone to install one of the community options.
  - If anything we could also make it easier to swap out our editor by standardizing methods to build new editors into the Strapi interface.

- 202309: It's Aurélien from Strapi, we released an alpha version today (v14) with a new field type called Blocks. It's based on Slate and provides the same capabilities as any rich-text editor. In the beta, we plan to support links, markdown, keyboard shortcuts (Notion-like), and an expanded view.
  - we made an heavily benchmark. We are currently hesitating between Lexical and Slate. Any recommendation/suggestion?

- I'm looking to swap out my EditorJS editor for a different implementation (the undo/redo just isn't robust enough) and was waiting until this feature appeared to start working on it. Now that Strapi has settled on Slate, I was looking to start working on customising the editor for my own needs, adding additional tools, etc.

- [CMS Recommendations - Customisable Rich Text : nextjs_202309](https://www.reddit.com/r/nextjs/comments/16b5yaz/cms_recommendations_customisable_rich_text/)
- I’m Pierre, co-founder and CEO of Strapi. FYI, we are currently replacing the default editor with Slate.js
  - Even more importantly, you pointed out the most important item of the discussion (which is actually not about the tool you will ended up using): how much control do you want to give to editors?
  - In a traditional CMS, you would typically give editors the ability to edit HTML. This gives them a ton of control. But, with power comes responsibilities. Editors might change colors, paddings, margins, etc. This often makes designers quite upset
  - The concept of Headless CMSs was born not only because companies need to manage content on multiple platforms, but because the way to create a website completely changed over the past few years. 
  - In 2023, "templates" are made with modern frontend frameworks, such as React, Next.js, Vue, Nuxt.js, etc. The common denominator(分母) between these frameworks is the component. 
  - Components are these little blocks you can reuse in multiple places. You can give them props. They are great because they are reusable, while consistent (which is not the case of copy-pasted HTML).
  - In my opinion, the role of Headless CMSs is to make these props dynamic; to give non-technical people the ability to edit the content of these props.
  - By choosing a Headless CMS, do make sure you can leverage these components. They should not necessarily be managed within the rich text editor (which should be a field like any other). In Strapi, we introduced the concept of Dynamic Zones and Components to handle this. You can for example create a "Button" component, which has a "label" (type: "text") and a "theme" (type: "select"), and reuse this component in different Dynamic Zones. 
- Overall we've been pretty happy with Strapi with the exception of the default editor.
  - The custom plugins made it easy to change the default editor to CKEditor instead.
  - But at the same time one certain plugin is also causing us a lot headaches. The biggest problem is that CKEditor version 1 and version 2 are very different
  - So now we have about 300 articles, but stuck without an easy way to upgrade the editor. This is pretty much causing all of our problems.
  - Dynamic zones are quite neat, and we do use it in a few places. But it doesn't work that well for our use case with rich text articles cause the editors want to keep putting content inbetween rich text so you'd have something like: rich text -> CTA -> rich text -> Twitter embedd -> Rich text -> Another CTA
  - This gets almost just as difficult to read as embedding html everywhere, which is what we currently do.
  - Dynamic field is something I also looked into, which I think could work OK. The problem is that they want to add html blocks in the most arbitrary and random places. Sometimes right after the first paragraph, sometimes in the middle, the end. Sometimes there are 10+ html tags in a single Article. They don't have a fixed position. This arbitrary positioning makes it seem like dynamic zone won't work very well. Or maybe I'm missing something ?
  - Anyways, I tried using dynamic zones and it seems to be working pretty well. Seems like getting the most out of Strapi is better than replacing it.
# discuss-feat-version-history
- ## [Q2, 2024 - Content history | Content Editing XP | Strapi](https://feedback.strapi.io/customization/p/q2-2024-content-history)
- Track version history of content: view the different iterations of a piece of content.

- ## 

- ## 💰 history is v5 only & an EE feature. _20230315
- https://discord.com/channels/811989166782021633/1095091586452426824/1218161565052833853
  - You need a license. Enterprise edition, paid for
- I just want to test locally. Is there any workaround
  - No there’s not really, there are checks all over the place

- ## [How to add revision history or track any changes made by user? - Questions and Answers / Database-SQL - Strapi Community Forum _202105](https://forum.strapi.io/t/how-to-add-revision-history-or-track-any-changes-made-by-user/4882)
- there is a complete video of how to create revision history Activity logs 

- [History/Versioning strapi plugin - Questions and Answers - Strapi Community Forum _202105](https://forum.strapi.io/t/history-versioning-strapi-plugin/5343)
  - I believe there is a plugin strapi-plugin-versionioning as well as strapi-plugin-revisions.
# discuss-feat-draft-publish
- ## [Q2, 2024 — Draft & Publish | Content Editing XP | Strapi](https://feedback.strapi.io/customization/p/q2-2024-draft-publish)
- Allow users to manage content by having a published and draft content at the same time.

- ## 

- ## 

- ## 

- ## [How to publish the data I created with entity service? - Questions and Answers / Strapi Backend - Strapi Community Forum](https://forum.strapi.io/t/how-to-publish-the-data-i-created-with-entity-service/27767)
- I think you can set the publishedAt to a Date.now() timestamp. 
  - if publishedAt is null it’s in draft if it has a timestamp it’s considered published.

- ## 👨🏻‍🏫 [Creating a Draft System - Community Guides - Strapi Community Forum _202210](https://forum.strapi.io/t/creating-a-draft-system/22930)
- What we want here is to fetch only data that has a published status.
  - But we don’t want to use parameters  (e.g. `/articles?status=published` ) because you can easily fake the params.
- This guide can be applied to any other controller action.

- ## [How to create draft entry with strapi v4? - Questions and Answers - Strapi Community Forum _202312](https://forum.strapi.io/t/how-to-create-draft-entry-with-strapi-v4/34701)
- To create a Draft entry, just append `status:'draft'` along with the other body params.

- ## [Is it possible to post a entry as draft in the api? - Questions and Answers - Strapi Community Forum _202108](https://forum.strapi.io/t/is-it-possible-to-post-a-entry-as-draft-in-the-api/9068)
- Yes, set the `published_at: null` during the POST request and it will be created as a draft. The default for REST/GraphQL sets that field to the current datetime. Passing over the null value will leave it in a draft state.
- As of 7th February, the field is written `publishedAt` and not `published_at` as said before.

# discuss-schema-change
- ## 

- ## 

- ## 

- ## [Strapi model schema management - Questions and Answers - Strapi Community Forum _202305](https://forum.strapi.io/t/strapi-model-schema-management/28879)
- In order to deploy content model changes to a production system you would initially have to apply the related changes in the db and then deploy a new version of Strapi with the aligned json model definitions

- ## [Data Loss in Content-Type Table After Schema Modification _202401](https://github.com/strapi/strapi/issues/19141)
- In Strapi v5 D&P and i18n won't be able to be disabled (though they don't have to be used) so technically in v5 the D&P delete issue won't be a problem anymore since it'll be forced on for all content-types (though you'll have the option to auto-publish by default or if new content should be a draft state).

- ## [Deleting/Updating content-type doesn't drop/migrate the database ](https://github.com/strapi/strapi/issues/1114)
- 202210: Yes this is currently intended (as you deleted the schema effectively), the best method to hold onto the data is take a database backup.
  - Certainly any modifications a dev is making should be tested in a staging environment. 
  - If you are simply renaming a content-type or field then you will have to (for now) write a custom migration

- ## 🐛 [Renaming a field in a content-type will erase the existing data _202202](https://github.com/strapi/strapi/issues/12626)
- this behavior is the intended one (at least for the moment). 
  - In V3 we weren't cleaning up the DBs as projects were evolving and it created a lot of friction & resentment from the community. 
  - For V4, we decided to tackles this issue and started cleaning up the DB on schema changes (basically a schema/DB sync). 
  - However -and you're right- there is no way today for the schema sync to differentiate when a field is renamed from when one is deleted/created. If we want to allow this kind of distinction, it would imply in-depth modification of the content type builder API as well as some behavior in the schemas themselves. As we lack bandwidth for the moment, this is not something that will be handled in the short term.
  - However, it's true that there is a possible data loss when deploying a field rename from dev to production. Thus, I would advise creating a custom DB migration so that you can transfer the data before the schema sync is done. (more info on Derrick's link)

- ## [Losing data when modifying a model - Discussions - Strapi Community Forum _202302](https://forum.strapi.io/t/losing-data-when-modifying-a-model/25989/2)
- Renaming a field is what is called a non-compatible change. As long as you change your API definition, you’ll have destructive change. These type of changes should be handled with care and with multiple intermediate phasis.
  - you can use the migrations scripts and then create the new column or do a rename with your script, so that Strapi won’t have to do anything when upgrading the schema.

# discuss-news
- ## 

- ## 

- ## 

- ## I would like to know details on transformer i would like go through and maintain it. _202403
- https://discord.com/channels/811989166782021633/1217462664809152553/1219677189801246863
- just a heads up it won't be needed for Strapi 5 as we plan on baking in support into Strapi 5 to simplify the structure and be able to use the v4 syntax throughout Strapi 5. Happy to give it to you though if you want to continue to maintain it on Strapi 4
- Publisher might also be superseded by something from Strapi 

# discuss
- ## 

- ## 

- ## 🌲 [How to create nested categories in V4 - Questions and Answers - Strapi Community Forum](https://forum.strapi.io/t/how-to-create-nested-categories-in-v4/16416)
- creating multiple collection is not practical. since you will have to create new collection for every level 
  - i prefer to have 1 collection only

- [Hierarchical collection ](https://github.com/strapi/strapi/issues/6329)
  - We currently(202203) do not plan to add native support for this at this time. Marking as closed
  - It doesn't follow the project vision that we have for how Strapi will function in the near, mid, and long term future. Something like this is more inline with document databases and not with relational ones.

- ## ⚖️ @strapijs and so #Strapi Cloud will become SOC2 compliant! We just achieved 99%_202401
- https://twitter.com/laurie_jim/status/1746903974442406057
  - YI Strapi Cloud manages for your, the server (up time, scaling, etc), a database, a CDN and backups. All in one
- ⚖️ [What is SOC 2? A Beginners Guide to Compliance | Secureframe](https://secureframe.com/hub/soc-2/what-is-soc-2)
  - SOC 2 is a security framework that specifies how organizations should protect customer data from unauthorized access, security incidents, and other vulnerabilities. 
  - There are a variety of standards and certifications that SaaS companies can achieve to prove their commitment to information security. One of the most well-regarded is the SOC report — and when it comes to customer data, the SOC 2.

- ## [Strapi isn't just a CMS right? Is it not also a fully fledged backend web framework (like Django)? - Discussions - Strapi Community Forum_202207](https://forum.strapi.io/t/strapi-isnt-just-a-cms-right-is-it-not-also-a-fully-fledged-backend-web-framework-like-django/20324)
  - Strapi advertises themselves as a CMS, but I feel it’s much more than that. It feels like a backend web framework like Django. We can create our own APIs with routes & controllers. This means we can create custom endpoint URLs, and custom logic to handle each request. We can query whatever data we need from our database too.

- Django and strapi Both are Backend frameworks, though the big difference here is that Django has more batteries included.
  - In django you can render views and pass data to the “frontend” if you like to call it.

- Based on my experience with Strapi and Django, Strapi has a much more customizable “admin site” than Django, and Django allows you to customize your models more than Strapi. Setting up models in Django is done in code where in Strapi we do it directly in the UI.

- It doesn’t offer a lot of backend capabilities like creating custom APIs with routes and controllers and handling requests with custom logic. 
  - I guess the reason it’s mainly marketed as a CMS is that’s designed to be user-friendly and flexible for content management, making it accessible for ppl with varying levels of backend experience.
  - When it comes to CMS platforms, my personal favorite has always been WordPress. Its intuitive interface and a plethora of fantastic templates to choose from make it a go-to for many users. 

- ## [Can Strapi be used as a no/low-code solution for backend? : Strapi_202204](https://www.reddit.com/r/Strapi/comments/ubbdqx/can_strapi_be_used_as_a_nolowcode_solution_for/)
- Yes. Strapi provides you CRUD endpoints for every entity from the box. There is zero code to create entities. You can create it using admin panel

- You can generate page layouts with dynamic zones.

- ## [What do you guys use for a backend? I've been considering Laravel but it seems like overkill for a simple project. : reactjs_202302](https://www.reddit.com/r/reactjs/comments/117qi4z/what_do_you_guys_use_for_a_backend_ive_been/)
- You may be interested in AdonisJS. Very similar to Laravel (heavily inspired by it), has all the nice DB migration setup, etc and plays very well with React for the bits where you need it.

- I suggest NestJS. I've been using it for the last two years at work and it includes most things you'd need. We use it because we can use the same language for frontend and backend and it's a pretty standard MVC framework with a lot of tools included and great structure.

- ## 🌰 [How to Build a Notion Clone with Strapi v4 and Next.js (Part 1 of 2) | Hacker News_202206](https://news.ycombinator.com/item?id=31825676)
- Worked at a place that was doing this (creating a notion clone with some specific functionalities). 
  - 👉🏻 The hardest/most unstable part was getting a solid WYSIWYG editor experience with a bunch of different media handling. 
  - The backend part seemed fairly trivial in comparison, so I'm not sure why would this be used to showcase strapi.

- Every time someone says "Notion clone". I'm like, oh boy, that's a bold statement. I experimented with it a couple of times and its _a lot_ and a serious challenge.
  - Notion has many different content blocks text, callout, tables, images, etc. And those types also have configurations i.e (table calendar, board, timeline). Additionally there are field types with individual configuration as well. These all need to be expressed trough the API, and graphql's interface system might be a candidate for it. But it will be a _lot_ of models.
  - On top of that you need to create the most flexible editor in existence in regarding editing these content blocks.
  - The easy part is storing though so that's good. For a small sized setup. You can just jam it in a postgres jsonb table make some materialised views and indexes and be done with it.

- ## 🚀 [Strapi – Open-source Node.js Headless CMS | Hacker News_202006](https://news.ycombinator.com/item?id=23453530)
- The only issue I had so far is that the admin form customizations seem to be stored in the database instead of application files, so it’s not possible to replicate them easily between environments
  - Model data and customizations needs to be under source control. That's what I'm doing in my . NET Core CMS.

- We tried strapi late last year but found some big deficiencies that made the editing experience subpar. 
  - Simple things like being able to order a list of foreign keys, you cannot do and makes it hard for using this for content management - not sure if this has been fixed yet. 
  - The editor was very buggy too. Ended up just using wagtail.

- We use Strapi in production alongside Eleventy, a simple static website generator. One thing we've been missing with Strapi however is the possibility to localize content. I know the issue was raised but I'm not aware of any roadmap and we needed to hack our way around this limitation.
  - I'm using Strapi & 11ty too. I have 'pages' and 'posts' with properties 'content' and 'locale'. That's how I manage i18n. That's for the main content. For small strings used in other parts of the UI I'm using json files with i18n strings that 11ty injects into the views.

- I think a lot of people are missing the point of a tool like Strapi.
  - 1. CMS experience for non-technical teams: marketing, product, content, etc. 
  - 2. Graphql api to avoid lock-in. Tomorrow you can take your data to AWS Appsync, etc 
  - 3. Ownership of the data: Contentful, Prismic, etc are great - but Strapi allows you to own the data. Even in its simplest form, its a sqlite file you can check in to git.

- why would a "non-technical" team pick this product over something more universally hostable and well known, with established plugin ecosystem and developers on tap, like Wordpress?
  - so the choice of wordpress or nodejs or whatever is a developer driven decision. However, the non-technical team will want a brilliant CMS experience.
  - If you can convince the tech team to build your entire infrastructure on Wordpress/php...then great, go for it. But most likely the rest of your app is built in different languages.
  - I suspect that most engineering will be happier to touch a reactjs based product versus a PHP based.

- the web is moving away from pure content or shop pages to more holistic interactive experiences where you need to integrate content into complex flows that are more application than website. Plus you might want to reuse said content on mobile apps too. There it really pays off to have your content separated as structured data that you can query for.

- 🆚️ what is the deference between this and something like Hasura for crud rest/ql api's ?
  - Hasura doesn't provide an admin interface. It's just supposed to be a backend, not a CMS.
  - Strapi doesn't have a mechanism for sending events to the client, although it seems GraphQL subscriptions are in their roadmap.
  - Strapi doesn't seem to have a way to do aggregations. The only aggregation I see is "count", and it seems that is there for pagination, which makes sense for their intended audience.
  - While Strapi has simple filters, you can't do more complicated logic by using "and" and "or". You have to write a custom query using the ORM they use. Hasura allows clients to make such queries with no changes to the backend.
- There is overlap between their functionality, but they are clearly meant for two different audiences / types of project.

- We evaluated Strapi (contentful snd others) for a headless CMS to power a web and mobile app. In the end we rolled our own in Rails was much quicker and simpler than these off the shelf tools.
  - Some things are hard/impossible to do: Repeating fields, in order to construct content as we wanted it to look. We needed to be able to determine if we have the latest information without having to go through all database rows. 
  - If it does what you need to do out of the box then stick with it, but for us, we needed to do more complex stuff.

- It's difficult to differentiate the products in CMS market. Developer productivity is a solved problem already. Hitting a few buttons and getting an API is nice. Every other CMS has Rest and GraphQL APIs, nice docs for devs, etc.
  - 👉🏻 What most CMS products miss is; in real world, a company spends a lot of energy on not just building software, but also operating with the tools they build. I haven't heard any love story about people who write content. Developers build their stuff quicker, editorial teams look at a screen that look completely irrelevant to their work. People hate their jobs and may quite because of the horrible UX experience CMS products deliver.
  - This is my feedback. As a developer, I'm not looking for another Schema-to-GraphQL generator. There are too many of those. Good ones and shady ones. Nobody would miss anything if somebody decided not to build another CMS competing with the existing ones today with slight differences.
  - The bigger challenge is to build something not just developers, but non-technical teams love.

- Decoupling content with presentation is always a good idea

- Tried this out. It's a GUI tool for creating CRUD apis with authentication and authorization. It does the job but it's pretty clunky and heavy for what it is. You could probably get similar or better results with Postgres, PostgREST, and some GUI tool for Postgres like Postico.

- We switched from Ghost to Strapi + Gatsby.js when we were facing limitations regarding i18n in Ghost. It works pretty well! Spinning up Strapi is a breeze when using a PaaS like Heroku.

- I've been using airtable to give a bit of dynamic content to an otherwise static site. The API has some limitations, though, like not being able to directly upload images.

- How are the training resources for editors using Strapi? One selling point of the more commonly used CMSs is that you can hire editors that already know it and there are companies that can help you train editors.
  - From my experience you have to do that anyway if you have a custom data model.

- Plone is really heavy duty in comparison to Strapi. Plone is what you use if you want a CMS for an enterprise. Strapi is what you use if you want a very lightweight CMS and you find even something like wordpress too heavy.
  - I did a year of Plone development for an employer and hated it with a passion. It feels like Java implemented in Python.

- ## [如何评价Strapi? - 知乎](https://www.zhihu.com/question/305040758/answers/updated)
- 
