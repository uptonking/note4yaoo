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

- ## 📝 [Q3, 2023 — Better Rich Text Editor | Content Editing XP | Strapi](https://feedback.strapi.io/customization/p/q3-2023-better-rich-text-editor)

- [Change Strapi's Default WYSIWYG to a more feature rich Editor_202202](https://github.com/strapi/strapi/issues/12440)

- The current and previous (v3) WYSIWYG editor are more so basic markdown editors
  - Our current editor only supports the bare minimums in terms of markdown support (eg no tables, ect) and support for things like inline youtube video previews, ect are a bit more complex to handle properly.
  - There is already community options in both v3 and v4 such as CKEditor 5, React MD, Toast UI, and Editor.js I do think we should ship something more feature complete then forcing everyone to install one of the community options.
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

- ## 🍃 [MongoDB support in Strapi: Past, Present & Future_202106](https://strapi.io/blog/mongo-db-support-in-strapi-past-present-and-future)
- Since 2017 and Strapi Alpha, we have always supported SQL databases such as MySQL, PostgreSQL, SQLite, MariaDB, and the document database MongoDB.
- I posted a message on the Strapi forum announcing that we were thinking about officially dropping our support for MongoDB in Strapi. 
  - In an attempt to be fully transparent with the Strapi community, we provided some context about the problem and motivation for this important decision. 
  - 👉🏻 In short, having to support two different connectors (SQL + MongoDB) is slowing down our product developments, and MongoDB usage represents less than 0.4% of all the Strapi projects (data is anonymously collected via Telemetry system).
  - For the beta and stable release of the Strapi v4, Strapi won't support MongoDB natively, and no connector will be available (yet).

- [MongoDB compatibility delayed on v4 - Discussions - Strapi Community Forum](https://forum.strapi.io/t/mongodb-compatibility-delayed-on-v4/4549)
# discuss-features
- ## 

- ## [[feat]: feature flags_202312](https://github.com/strapi/strapi/pull/18871)
  - Introduces a new configuration file: features.(j|t)s. By integrating this configuration into our strapi.config, we gain the ability to determine whether to include the content-releases plugin in our application based on an environment variable. This could be used by any new feature we develop. It's also passed to the admin configuration so future flags can be checked

# discuss-issues-done
- ## 

- ## [Can't install strapi - Questions and Answers - Strapi Community Forum](https://forum.strapi.io/t/cant-install-strapi/33500)
- TypeError: Cannot read properties of undefined (reading 'addBreadcrumb')


```shell
# cd to your project and
npm install --legacy-peer-deps
npm run develop

```

- 
# discuss
- ## 

- ## 

- ## 

- ## [What do you guys use for a backend? I've been considering Laravel but it seems like overkill for a simple project. : reactjs_202302](https://www.reddit.com/r/reactjs/comments/117qi4z/what_do_you_guys_use_for_a_backend_ive_been/)
- You may be interested in AdonisJS. Very similar to Laravel (heavily inspired by it), has all the nice DB migration setup, etc and plays very well with React for the bits where you need it.

- I suggest NestJS. I've been using it for the last two years at work and it includes most things you'd need. We use it because we can use the same language for frontend and backend and it's a pretty standard MVC framework with a lot of tools included and great structure.

- ## [How to Build a Notion Clone with Strapi v4 and Next.js (Part 1 of 2) | Hacker News_202206](https://news.ycombinator.com/item?id=31825676)
- Worked at a place that was doing this (creating a notion clone with some specific functionalities). 👉🏻 The hardest/most unstable part was getting a solid WYSIWYG editor experience with a bunch of different media handling. The backend part seemed fairly trivial in comparison, so I'm not sure why would this be used to showcase strapi.

- Every time someone says "Notion clone". I'm like, oh boy, that's a bold statement. I experimented with it a couple of times and its _a lot_ and a serious challenge.
  - Notion has many different content blocks text, callout, tables, images, etc. And those types also have configurations i.e (table calendar, board, timeline). Additionally there are field types with individual configuration as well. These all need to be expressed trough the API, and graphql's interface system might be a candidate for it. But it will be a _lot_ of models.
  - On top of that you need to create the most flexible editor in existence in regarding editing these content blocks.
  - The easy part is storing though so that's good. For a small sized setup. You can just jam it in a postgres jsonb table make some materialised views and indexes and be done with it.

- ## 🚀 [Strapi – Open-source Node.js Headless CMS | Hacker News_202006](https://news.ycombinator.com/item?id=23453530)
- The only issue I had so far is that the admin form customizations seem to be stored in the database instead of application files, so it’s not possible to replicate them easily between environments
  - Model data and customizations needs to be under source control. That's what I'm doing in my . NET Core CMS.

- We tried strapi late last year but found some big deficiencies that made the editing experience subpar. Simple things like being able to order a list of foreign keys, you cannot do and makes it hard for using this for content management - not sure if this has been fixed yet. The editor was very buggy too. Ended up just using wagtail.

- I think a lot of people are missing the point of a tool like Strapi.
  - 1. CMS experience for non-technical teams: marketing, product, content, etc. 
  - 2. Graphql api to avoid lock-in. Tomorrow you can take your data to AWS Appsync, etc 
  - 3. Ownership of the data: Contentful, Prismic, etc are great - but Strapi allows you to own the data. Even in its simplest form, its a sqlite file you can check in to git.

- Question for the connaisseurs, what is the deference between this and something like Hasura for crud rest/ql api's ?
  - Hasura doesn't provide an admin interface. It's just supposed to be a backend, not a CMS.
  - Strapi doesn't have a mechanism for sending events to the client, although it seems GraphQL subscriptions are in their roadmap.
  - Strapi doesn't seem to have a way to do aggregations. The only aggregation I see is "count", and it seems that is there for pagination, which makes sense for their intended audience.
  - While Strapi has simple filters, you can't do more complicated logic by using "and" and "or". You have to write a custom query using the ORM they use. Hasura allows clients to make such queries with no changes to the backend.
- There is overlap between their functionality, but they are clearly meant for two different audiences / types of project.

- We evaluated Strapi (contentful snd others) for a headless CMS to power a web and mobile app. In the end we rolled our own in Rails was much quicker and simpler than these off the shelf tools.
  - Some things are hard/impossible to do: Repeating fields, in order to construct content as we wanted it to look. We needed to be able to determine if we have the latest information without having to go through all database rows. If it does what you need to do out of the box then stick with it, but for us, we needed to do more complex stuff.

- It's difficult to differentiate the products in CMS market. Developer productivity is a solved problem already. Hitting a few buttons and getting an API is nice. Every other CMS has Rest and GraphQL APIs, nice docs for devs, etc.
  - What most CMS products miss is; in real world, a company spends a lot of energy on not just building software, but also operating with the tools they build. I haven't heard any love story about people who write content. Developers build their stuff quicker, editorial teams look at a screen that look completely irrelevant to their work. People hate their jobs and may quite because of the horrible UX experience CMS products deliver.
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
