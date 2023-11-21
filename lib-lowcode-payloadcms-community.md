---
title: lib-lowcode-payloadcms-community
tags: [community, payloadcms]
created: 2023-02-05T18:40:16.729Z
modified: 2023-02-05T18:40:43.969Z
---

# lib-lowcode-payloadcms-community

# guide

- https://github.com/sanity-io/content-source-maps
  - Content Source Maps is a standard representation to annotate fragments in a JSON document with metadata about its origin: the field, document, and dataset it originated from. 
  - We do this with a separate document alongside the content that provides the metadata without changing the layout of the original document.
  - Today Content Source Maps enables annotating JSON documents with “source” metadata, allowing end users to navigate directly to the source to edit it. 
  - In the future, content source maps will also enable annotating JSON documents with arbitrary metadata for other use cases.
  - Normalised JSON Path: A string representing the location of a value within a JSON document in a standardised format
# discuss-stars
- ## [MongoDB support in Strapi: Past, Present & Future_202106](https://strapi.io/blog/mongo-db-support-in-strapi-past-present-and-future)
- Since 2017 and Strapi Alpha, we have always supported SQL databases such as MySQL, PostgreSQL, SQLite, MariaDB, and the document database MongoDB.
- I posted a message on the Strapi forum announcing that we were thinking about officially dropping our support for MongoDB in Strapi. 
  - In an attempt to be fully transparent with the Strapi community, we provided some context about the problem and motivation for this important decision. 
  - In short, having to support two different connectors (SQL + MongoDB) is slowing down our product developments, and MongoDB usage represents less than 0.4% of all the Strapi projects (data is anonymously collected via Telemetry system).
  - For the beta and stable release of the Strapi v4, Strapi won't support MongoDB natively, and no connector will be available (yet).

- [MongoDB compatibility delayed on v4 - Discussions - Strapi Community Forum](https://forum.strapi.io/t/mongodb-compatibility-delayed-on-v4/4549)

- ## [Roadmap: Multiple Database Support](https://github.com/payloadcms/payload/discussions/287)

- Feathers (Node API framework) did something similar recently with the v5 release and put adapters for MongoDB and SQL (Knex) in the core 
  - With the resolvers functionality and hooks its easy to use and avoids an ORM altogether

- Just want to throw two precedents in the mix here in case people are not aware of them.
  - KeystoneJS has a lot of similarities with Payload, and it may be worth taking some time looking at how they've integrated Prisma
  - a review of the decisions Statamic made when they implemented a database driver for their flatfile based content model has a lot of parallels with some of the paths suggested above (Statamic effectively goes the put it all in a JSON field route). 
    - From my pretty limited use of the Statamic database driver, I might consider their implementation an anti-pattern. 
    - Though it solves the issue of a large number of records that the flatfile solution just can't support, it doesn't address most of the underlying reasons why many of us prefer a RDBMS. 
    - The main things that come to mind that make us very nervous with Mongo: relationships and the associated complex queries, and search (and relatedly usage of opensearch/elasticsearch).
- I personally really respect Keystone a lot. 
  - They would be my go-to solution if Payload did not exist 
  - but their implementation of Prisma does create some hard-to-accomplish things that Payload supports, like our blocks field, array field, group field, etc.
  - I do agree that dropping everything in a JSON field is an anti-pattern for sure. For us to continue to support these complex nested field types, we have 2 options:
    - Over-use a JSON field (yuck, not gonna happen)
    - Create unique tables for every level of "nested" fields.... harder, but better I think.
- Just to clarify, I think at the block/nested field level a JSON field is actually fine (though not ideal I agree) - the Statamic solution puts the entire record data in a single JSON field (yuck!). 
  - Every CMS I've worked with that supports a dynamic field like blocks (and nearly everyone does now) stores the data in a single JSON field 
  - and I think to keep it all kinds of dynamic and not suffer death by 1000 joins, it may be an ok solution (yes makes migrations very hard, lots of yucky implications) - 
  - but again there's a lot of anti-patterns out there to improve on while still harnessing JSON for those dynamic fields (see crafts matrix field, wagtails streamfield, etc).
  - We use Wagtail(django) extensively and their Streamblock is also a JSON field and tbh it's a mess. 

- coming from over 10 years of TYPO3(cms): 
  - do use JSON fields for special content like blocks, array and group, 
  - creating tables and fields for every possible combination is a pain and usually even less performant (mostly because developers other than core team do not understand the structure anyway)
  - Looks like they are catching on though, adding migration support/helper utils is now on the near release roadmap for wagtail.

- 👀 This conversation is super important. I can relate to everything that's been said above. Here are my thoughts:
  - We are never going to plop(落下、躺下) entire docs in a Postgres JSON column (nasty)
  - I don't even want to plop entire blocks / array fields in a JSON col. If we do this, it will be because we had to.
  - The goal will be to do a different table per "dynamic" field, and build traditional SQL table structures for all other fields. The problem will be that we'll need to do lots of joins here, but hey, that's the name of the game in SQL. If performance suffers for your schema due to too many joins, go back to Mongo.

- The problem of separate tables is not about putting the data there, but maintaining the schema and data when there are schema changes (cf. Drupal CCK schema design ~2006-2013). Amount of JOINs are limited depending on engine. Fields allowing multiple values or supporting translations need a separate table.
  - You can establish one table per field (all of them), but the resulting queries are not nice to look at and you cannot query anything without a query builder (cf. Drupal entity/field schema design today).
  - I'm with @ssyberg, JSON fields for complex fields wouldn't be that much of a problem, especially considering the cost/complexity of the extra tables.

- I am not an expert in this field, but Strapi seems to create another table for each "nested" field(In Strapi it is called "component" field). I should add that Strapi uses "separate records" for translated fields, not separate tables.
  - I would not look to Strapi as a precedent here, their lack of deeply nested dynamic fields is a major reason it's largely avoided by anyone looking for a serious CMS solution. (Perhaps they've recently removed that limit, but it was previously limited to depth of 2 which is extremely limiting in how you can build your fields/models.)

- My suggestion: The adapter driver should be responsible to determine the best strategy for nested fields and other edge cases. In PostgreSQL, for example, we could use JSON columns if user wants (via adapter config), whereas in other drivers like SQLiteAdapter only nested table would be applicable and so on so forward.
  - I'm not sure what the benefit would be in following a table pattern with one adapter and JSON in another, since both would still need to support core behavior you'd have all the limitations of both paths to contend with.

- I think it should be avoided to use operations which are not provided by cloud database providers like Planetscale or Neon.tech. Especially starting from scratch It is easy to avoid these kind of things.

- what kind of schema are you going for in sqlite?
  - We're working through some prototypes right now. The goal is to not lean too heavily on JSON. As long as we can get the level of normalization, query performance and dev experience, we're going to make it work like a traditional relational database. More on this later.
- Great stuff! Really excited for this. I hope schemas will be supported for Postgres. It would be awesome to be able to keep a full database of `public` schema for app related records and a `content` schema for the CMS. This way we can also manually query between the two without cluttering(使杂乱) the public schema.

- Another thing to note is that in Directus/Strapi, they have some pretty serious limitations when it comes to using their equivalent of our more complex field types, including the array field.
  - For example, Directus goes straight to a JSON column for their array field, which means that you can't have relationships or localized content within array rows. 
  - We would never let that fly - in Payload, we use relationships within array rows constantly. Relations within a JSON column might be possible, but it could be argued that it would be more complex to join relations on JSON array column data.
- I can't promise that we will jump right to JSON columns, though, and the problems above are just a small snippet of what we are foreseeing now.

- 
- 
- 
- 
- 
- 

- ## vercel: We’re introducing visual editing of content from headless CMSes bringing back one of the best features of monolithic CMSes for composable architectures–with no changes to your code!
- https://twitter.com/cramforce/status/1653792488770125826
  - The key new technology: Content source maps. They allow your content to pass through N layers of abstractions that obscure where it came from, yet enable the visual editors to trace its origin to the correct source data in the CMS.
  - We developed the technology with our launch partner @sanity_io but would love every CMS, e-commerce platform, and other content sources to start emitting content source maps.

- Super interesting! We've talked about HTML source maps a few times over the years (for the CMS/WordPress/Shopify use-cases). Are content source maps analogous to this, or are they different?
- Yup it looks to me link this is more about how they annotate the CMS data to know which item and field to send you to edit. 
  - HTML source maps in my opinion would still be amazing for instrumenting the HTML for visual editing. 
  - Not clear to me how @vercel is instrumenting the HTML
- Thank you so much. We've built our own sort of HTML source map for webflow and we've never been terribly satisfied with the approach.
  - Our solution is somewhat similar to the one found in an SVG visual editor called sketch-n-sketch
  - If you search that document for "Provenance Tracing" you'll find a great explanation. The TLDR is that you instrument your interpreter to track evaluation.
  - The goal is that if a particular element is the result of a function call, you may want to edit the function body (or just the call) and you need a bread crumb all the way through when building a visual editor for a tool like that.
  - At webflow we end up stamping each of the nodes at Design time with guids that map back to pieces in the AST. This breaks down for certain types of sources that can project many nodes from a single one. I'm looking forward to reading that doc to see what I can learn. Thanks again
- It's a very interesting problem space. The http://editable.website approach is to do it all inline (it's basically building an app) but using a CMS comes in handy once I'd start replicating things like publishing workflows, permissions etc.
# discuss-examples
- [User CSV Import for a Collection](https://github.com/payloadcms/payload/discussions/1660)
# discuss
- ## 

- ## 

- ## 快捷指令的编辑体验太屎了，难以想象做 20 行以上的指令有多痛苦。
- https://twitter.com/acghnu/status/1726963155585417612
- No code 所以并不会成为全部的未来

- ## 🤔🎯 Should Payload move to @nextjs from Express?_20231027
- https://twitter.com/payloadcms/status/1717643250201219245
- Why associate your starter with a react only framework when you can be used with any front end?
- Deployment (cheap and easy) is still the biggest problem. Making it serverless, no matter how you achieve it, is a real win and definitely the future. Edge runtime for cold starts would be the icing on the cake
- Only if you make that as an option. There are benefits with express, since I need it for central tendency functionality

- ## drizzle doesn't support Mongo, would it even be a potential option for payload?_20230504
- https://discord.com/channels/967097582721572934/1102950643259424828/1103351664188076144
- Our expectation is that there will never be an ORM that handles SQL and noSQL well. It is on us to abstract all of Payload's database interactions into an adapter pattern. This way a project can choose which database adapter plugin to use and only install the dependencies for that ORM.
- interesting! Prisma does it though, doesn't it? And so basically, Payload itself would act as some kind of pseudo ORM wouldn't it?
  - We're looking at prisma as one option. We still need to figure out how to make SQL friendly schema out of what we have for all the field types and localization

- Yeah, an adapter needs to be able to take the incoming fields on a collection and determine how to create the appropriate schema for that config. Then also it needs to be able to set up how to query it, paginate results, handle database operations, etc. What would be the alternative?
- https://discord.com/channels/967097582721572934/1103355335571411014

- ## Have thoughts on additional database support? @PostgreSQL
- https://twitter.com/payloadcms/status/1652021212996829184
  - We're not dropping mongodb! We're adding support for additional databases to make Payload even more extensible 
- Drizzle doesn’t support MongoDB. Keystone implement prisma support somehow 🤷‍♂️ many other frameworks and cmses using knex under the hood (only sql) @MikroOrm supports both mongo and postgres and looks promising
- Prisma doesn't work at the edge. Not even with the new JSON protocol.

- ## Very early work has begun around planning and researching ORMs. 
- https://discord.com/channels/967097582721572934/967097582721572937/1098256442148003882
  - This will be in active development starting next week. I won't know how long it will take until we get a bit further though.
- My guess probably not Prisma. It's too big, slow and bulky to be able to use it in serverless

- Prisma is too big, we need to tighten it up. Some notes on what to expect:
  - Refactors to core to allow for an adapter pattern that encompasses all of the database touchpoints in the core.
  - Adapter(s) for SQL, Mongoose, and MongoDB (without the overhead of Mongoose)
  - Migrations included
  - Access to underlying database transactions

- Sweet, thanks. We're thinking of migrating from Directus, because it doesn't handle S3 images very well (all are streamed through the directus server rather than with S3 links). Currently just using it as a PIM for ecommerce data, but will hopefully be powering our new website and potentially B2B web store

- ## 🆚️ [Self-hosted headless cms - WEBINY OR PAYLOAD? : opensource](https://www.reddit.com/r/opensource/comments/zbq7z9/selfhosted_headless_cms_webiny_or_payload/)
- I'm part of the core team at Payload and I want to get your thoughts on how to show the security standards for Payload.
  - We do a bunch of best practices that anyone building their own Node/Express app should. 
  - The auth that we have is built to a higher standard than some of other competitors as it uses http only secure cookies.
  - If you dig a little you'll find that other headless CMS are not doing this meaning that any javascript code in your project could have access to the user state where it really shouldn't. 
  - We have other cool things in place that make it easy to turn on user verification, locking accounts, API rate limiting, CSRF and CORS.
- Regarding security, BCMS provides, out of the box, even in its (generous) free plan, fine-grained control over the API keys and user roles. It offers enterprise-grade permissions features, making it super secure at no cost. Other than the server.

- https://www.reddit.com/r/selfhosted/comments/zbp1z7/exploring_webiny_and_payload_for_a_web_project/
- Webiny co-founder here. 
  - If you're looking for a system that's not developer dependant, we are just wrapping up several new features on the Page Builder side of our product, making it much more powerful and easier to use and in Q1/2023 
  - we'll be launching also the ability to build fully dynamic pages by combining our Page Builder with our Headless CMS. Happy to share more details if you're interested.
