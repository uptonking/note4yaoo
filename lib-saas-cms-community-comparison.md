---
title: lib-saas-cms-community-comparison
tags: [cms, community, comparison]
created: 2023-12-15T18:58:03.877Z
modified: 2023-12-15T18:58:15.432Z
---

# lib-saas-cms-community-comparison

# guide
- [w3techs: Usage Statistics and Market Share of Content Management Systems](https://w3techs.com/technologies/overview/content_management)
  - WordPress, Wix, Squarespace, Joomla, Drupal, Adobe, PrestaShop, Webflow, TYPO3, Weebly, Gatsby, Hugo, Zendesk, Ghost, Odoo, MediaWiki, Gitbook, Jekyll, Salesforce
# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## [What’s your favorite CMS? : webdev_202209](https://www.reddit.com/r/webdev/comments/x7ct03/whats_your_favorite_cms/)
- Strapi, for me, was inflexible. It doesn't namespace its admin tables, it doesn't provide unlimited RBAC for self-hosted, and it's a bit more interested in its API endpoints than its database integration.
  - Another big issue we found was with workflows. We spoke with Strapi's engineering support and weren't able to arrive at a solution that didn't involve basically writing a publication workflow from scratch for our use case. It's on their roadmap, but they weren't able to give us a timeline on launch.
  - Overall, as an enterprise client we found Directus much less restrictive and liked the feature set better for our use case (a content creation company). But if Strapi's existing features fit your use case, and you don't have any conflicting table names (ours was admin_users) then you should be fine.
- Directus is very nice. I especially like true open source model, polished admin UI, fresh codebase after big migration from php to node.js (this looked very risky to me, when I learned what they are trying to do, but it worked out very well for them), active dev team, and MySQL/postgres instead of mongodb as first class citizen.

- Some people mentioned here strapi. I'm using it at work right now and it was so cool at first, but as I'm doing more and more complicated things its not as cool as it seems to be. I'd recommend it only and only if you need simple schemas and need other html requests like POST.
  - There is a problem with using nested components on depth 2 or more - your data just wont be saved... I have no idea why its the case, but devs are aware of it and dont even want to think about this actually serious problem in the future
  - Also there is a cool thing that you can use relations between many collections with many types of relationship. But they wont brag with the fact that if you use this relation, order of the connected elements wont be the same as you entered and there is no chance to change it...
  - Not to mention strange decisions like pushing v4 without transaction support like it v3 had. Also many not reliable information in docs.

- Recently discovered Directus and absolutely love it. Even installed on top of an existing schema and it just works.
- Installed on top of an existing schema is a big part of why I love directus. For developers (or companies with a development team), the advantages are huge. Currently in the process of migrating from Sanity to directus, since our data was split awkwardly between a web API and a postgres database that we designed/controlled, and it's been a breeze getting directus set up.
- Why? Largely control. It's open source, self-hosted, and extensible. Solid data types and defaults, including markdown as an option for rich text, and it takes no time to spin up and start running with.
- Best part of all, it integrates well into an existing database. You can utilize tables you already have, create new tables in the existing schema, and control what is and isn't editable through the UI.
- Directus is very nice. I especially like true open source model, polished admin UI, fresh codebase after big migration from php to node.js (this looked very risky to me, when I learned what they are trying to do, but it worked out very well for them), active dev team, and MySQL/postgres instead of mongodb as first class citizen.
