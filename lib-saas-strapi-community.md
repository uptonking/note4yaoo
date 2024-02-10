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

- ## [Is it possible to create a collaborative platform with Strapi? - Questions and Answers - Strapi Community Forum _202211](https://forum.strapi.io/t/is-it-possible-to-create-a-collaborative-platform-with-strapi/23815)
- definitely possible but it will require some coding and bending. Afaik you can’t really create this just by clicking around in the admin panel.

- ## 💰 [Can I use strapi free in my self-hosted server? - General - Strapi Community Forum_202304](https://forum.strapi.io/t/can-i-use-strapi-free-in-my-self-hosted-server/27666)
- The only restrictions on the free version is that audit-logs and Review Workflows are not available

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
# discuss-news
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

# discuss-issues-not-yet
- ## 

- ## 🐛 [Inconsistency between responses gotten from the REST API and the Entity service API_202401](https://forum.strapi.io/t/inconsistency-between-responses-gotten-from-the-rest-api-and-the-entity-service-api/34975)
- strapi-plugin-transformer plugin was what I was going to recommend. Another approach you can use, is to write a transformer function to flatten the response.

- Yes, the transform plugin is the way to go. 
  - But I’ve recently learned that it’s all a joke. 
  - You see, core controllers invoke the transformResponse function which iterates over the service response and produces this highly impractical data/meta/attributes structure. This takes time. Then, the middleware offered by the transform plugin iterates again over that transformed response and flattens it. Which takes time again. 
  - A performant way would be to disable that transformResponse function alltogether, or at least the part that wraps all non-id field within attributes. Maybe patch-package could be used for that.
# discuss-strapi-mongo 🍃
- ## 

- ## 

- ## [Is MongoDB a terrible choice for Strapi? : Strapi _202207](https://www.reddit.com/r/Strapi/comments/w9069u/is_mongodb_a_terrible_choice_for_strapi/)
- Not a terrible choice, in general: we used MongoDB for all of our v3 instances. However, Mongo is hugely inefficient if you have nested relations between collections (though this makes sense - mongo isn’t a relational DB).
  - In any case, v4 dropped support for Mongo. We’ve been migrating to v4 with Postegres and we’ve seen some great performance gains, even in applications with very few relations.

- ## 🍃📡 [MongoDB support in Strapi: Past, Present & Future _202106](https://strapi.io/blog/mongo-db-support-in-strapi-past-present-and-future)
- Since 2017 and Strapi Alpha, we have always supported SQL databases such as MySQL, PostgreSQL, SQLite, MariaDB, and the document database MongoDB.
- I posted a message on the Strapi forum announcing that we were thinking about officially dropping our support for MongoDB in Strapi. 
  - 💡 In short, having to support two different connectors (SQL + MongoDB) is slowing down our product developments, and MongoDB usage represents less than 0.4% of all the Strapi projects (data is anonymously collected via Telemetry system).
  - For the beta and stable release of the Strapi v4, Strapi won't support MongoDB natively, and no connector will be available (yet).

- [Why MongoDB is not available in Strapi V4 ? _202111](https://github.com/strapi/documentation/issues/520)
  - we won't maintain a MongoDB connector in v4. If MongoDB (the team) builds one that is up to them.

- ## 🍃 [MongoDB compatibility delayed on v4 - Discussions - Strapi Community Forum _202104](https://forum.strapi.io/t/mongodb-compatibility-delayed-on-v4/4549)
  - When we re-developed from scratch Strapi, in 2017, we decided to use more specific ORMs. One for SQL database called Knex, and one for NoSQL MongoDB called Mongoose. Why? MongoDB was huge at that time. 
  - MongoDB wasn’t the recommended starting database to test and try Strapi. It has been replaced by SQLite
  - Drupal, WordPress, and many other CMSs restrict to one database, often SQL one and these are successful projects.

# discuss
- ## 

- ## 

- ## 

- ## 

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
- 
- 
