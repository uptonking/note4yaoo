---
title: lib-saas-strapi-latest-v5
tags: [changelog, roadmap, strapi]
created: 2023-12-15T19:38:46.847Z
modified: 2023-12-15T19:39:18.123Z
---

# lib-saas-strapi-latest-v5

# guide

# blogs

### [Strapi V5 Features and Updates — Restack](https://www.restack.io/docs/strapi-knowledge-strapi-v5-overview)

- Plugin System: The new plugin system allows for easier customization and extension of Strapi's functionalities.
- Database Layer: Enhanced database layer offers better performance and scalability.
- API improvements ensure faster response times and more efficient data handling.
- Admin Panel: A revamped(翻新; 改进) admin panel provides a more intuitive user interface.
# rfc

## [v5 Database Design_202309](https://github.com/strapi/rfcs/blob/v5/database/rfcs/xxxx-v5-database.md)

- We need to support development of new features. Most of them are going towards a more CMS like model. to support this approach we will introduce the notion of documents & links.
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

## [v5 Content API Design](https://github.com/strapi/rfcs/blob/v5/content-api/rfcs/xxxx-v5-content-api.md)

- V5 Content Engine requires some breaking changes to the API, It is also the opportunity to simplify the API Response format following user feedbacks.
  - The main point of this RFC is to propose a simplified and v5 compatible format while offering a smoother migration path with a legacy format.

- Use the internal documentId as the only identifier the ContentAPI knows about.
- Introduce a simplified format
# discuss-v5
- ## 

- ## 

- ## [Notice: Community PR Change Freeze for 2023 Holidays & v5_202310](https://github.com/strapi/strapi/issues/18618)
- As the year is winding down and with the holidays coming up we will be placing a community pull request change freeze into effect until March 2024.
  - any new PRs submitted after October 31st (Tuesday) will be closed due to the change freeze unless an exclusion is applied.
  - we have started our major development on Strapi v5 and want to try and limit the amount of merge conflicts that we have between the main branch for Strapi v4 and the v5/* branches.

- ## [Notice: Requesting community feedback on v5 RFCs_202309](https://github.com/strapi/strapi/issues/17958)
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
