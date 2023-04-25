---
title: lib-lowcode-payloadcms-community
tags: [community, payloadcms]
created: 2023-02-05T18:40:16.729Z
modified: 2023-02-05T18:40:43.969Z
---

# lib-lowcode-payloadcms-community

# guide

# discuss
- ## 

- ## 

- ## 

- ## [Roadmap: Multiple Database Support](https://github.com/payloadcms/payload/discussions/287)
- coming from over 10 years of TYPO3: do use JSON fields for special content like blocks, array and group, creating tables and fields for every possible combination is a pain and usually even less performant (mostly because developers other than core team do not understand the structure anyway)
- Totally, this problem is rampant across CMS' that support dynamic fields and it's extremely solvable. I'm floored by the lack of documentation on the streamfield structure in wagtail. Just a paragraph or two would have saved us about a week of development time on our most recent project.
  - Looks like they are catching on though, adding migration support/helper utils is now on the near release roadmap for wagtail.
- This conversation is super important. I can relate to everything that's been said above. Here are my thoughts:
  - We are never going to plop entire docs in a Postgres JSON column (nasty)
  - I don't even want to plop entire blocks / array fields in a JSON col. If we do this, it will be because we had to.
  - The goal will be to do a different table per "dynamic" field, and build traditional SQL table structures for all other fields. The problem will be that we'll need to do lots of joins here, but hey, that's the name of the game in SQL. If performance suffers for your schema due to too many joins, go back to Mongo.
- The problem of separate tables is not about putting the data there, but maintaining the schema and data when there are schema changes (cf. Drupal CCK schema design ~2006-2013). Amount of JOINs are limited depending on engine. Fields allowing multiple values or supporting translations need a separate table.
  - You can establish one table per field (all of them), but the resulting queries are not nice to look at and you cannot query anything without a query builder (cf. Drupal entity/field schema design today).
  - I'm with @ssyberg, JSON fields for complex fields wouldn't be that much of a problem, especially considering the cost/complexity of the extra tables.

- I think it should be avoided to use operations which are not provided by cloud database providers like Planetscale or Neon.tech. Especially starting from scratch It is easy to avoid these kind of things.

- 
- 
- 
