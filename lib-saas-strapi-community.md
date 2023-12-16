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

- ## 🍃 [MongoDB support in Strapi: Past, Present & Future_202106](https://strapi.io/blog/mongo-db-support-in-strapi-past-present-and-future)
- Since 2017 and Strapi Alpha, we have always supported SQL databases such as MySQL, PostgreSQL, SQLite, MariaDB, and the document database MongoDB.
- I posted a message on the Strapi forum announcing that we were thinking about officially dropping our support for MongoDB in Strapi. 
  - In an attempt to be fully transparent with the Strapi community, we provided some context about the problem and motivation for this important decision. 
  - 👉🏻 In short, having to support two different connectors (SQL + MongoDB) is slowing down our product developments, and MongoDB usage represents less than 0.4% of all the Strapi projects (data is anonymously collected via Telemetry system).
  - For the beta and stable release of the Strapi v4, Strapi won't support MongoDB natively, and no connector will be available (yet).

- [MongoDB compatibility delayed on v4 - Discussions - Strapi Community Forum](https://forum.strapi.io/t/mongodb-compatibility-delayed-on-v4/4549)
# discuss
- ## 

- ## 

- ## 

- ## 

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
