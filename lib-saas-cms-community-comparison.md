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
# discuss-strapi
- ## 

- ## 

- ## [Is strapi(or headless cms in general) the right tool to use if I already have an existing backend api? : Strapi_202203](https://www.reddit.com/r/Strapi/comments/tj5afk/is_strapior_headless_cms_in_general_the_right/)
- 🚫 We do not support importing existing databases yet, sadly I don't think we are what you are looking for
- This video suggests there is a way to import existing database with some extra effort(still have to create the content type manually and edit some code). Does it still work?
  - Given it's age I would say no. Even if that did work, it's not something I'd recommend. Especially in our v4, the database code will go through and delete any columns or tables that Strapi isn't aware of and our relational structure is very specific.

- You would have to migrate the data into strapi and then you can manage it going forward.

- ## [[AskJS] What do you think of Strapi? : javascript_202003](https://www.reddit.com/r/javascript/comments/febof5/askjs_what_do_you_think_of_strapi/)
- Strapi is dreadful(糟糕的)... the only thing i like is the ease of table relationships. You have to customize it so much its just not worth it. You even have to customize jwt removal... thats not default! Very little is default.
  - I even had to write my own CAID system because i didn't want the default user id 1, 2, 3, 4 etc
  - You will find yourself writing so much code wondering why you are even using strapi, and then... they want to upsell you!
  - API's are not as complex as you think.
- I second this. Strapi and Directus both have their pain points and I'm considering just switching back to a simple Node/Express stack again. For simple headless CMS stuff they're quite good - but as soon as you want just a LITTLE complexity they're really bad.

- Strapi is great and gives you a lot of flexibility for customizing its core and plugin source code. This is one of its more advanced features and should breached with caution but very handy if you're committed to tracing through someone else's code without hand-holding.

- ## [what's the pros and cons of strapi ? : Frontend_202302](https://www.reddit.com/r/Frontend/comments/1183gl1/whats_the_pros_and_cons_of_strapi/)
- I found it to have a terrible user interface. It's clunky to work with (too many clicks). 
  - The API it offers is okay but I would rather use Next.js to directly connect to its database instead of querying the API of Strapi. 
  - Their version updates (majors) are a pain in the ass to upgrade. 
  - And if you create things, it creates the tables for you, but never cleans them up.
  - I found it nice to get started with a project, but I quickly decided to replace Strapi in its entirety in favor of my own hand-crafted CMS.

- I use Strapi and I am somewhat satisfied with it.
- Pros:
  -Most used of all Jamstacks
  -Quick to set up, easy to extend, comes packaged properly.
  -Works as expected for most basic operations and has the vast majority of features you need for static sites built right in
  -Good differentiation of roles and access
  -Free
  -Fairly easy to deploy
  -Works immediately after installing with a GUI that rarely breaks.
  -The parameters work as expected in DB calls
  -Once you get the hang of it, it's actually pretty convenient and makes managing DB calls, controlling access and making DB data visible to non-programmers, it's pretty useful.
- Cons
  -The default set up with SQLite is not helpful. SQLite only allows one CRUD call at a time. 
  -There are annoying things like "draft", which you have to disable manually and can be confusing
  -There is a learning curve and some of it is very frustrating

- ## [Opinion on CMS (Strapi, WordPress, Custom) : Frontend_202306](https://www.reddit.com/r/Frontend/comments/14i2288/opinion_on_cms_strapi_wordpress_custom/)
- Sanity is not only expensive, but also locks you into their platform. Sanity's GROQ query language is super awkward. 
  - Strapi is a nightmare to develop in, and their way of defining collections/access control inside an admin panel is a developer's hell for anything slightly more complex or custom
  - Payload is made with React and allows you to even customize the entire frontend of the CMS. It uses Node. JS + Express and has ready-to-use Next.js and e-commerce templates. Even has a Stripe plugin.

- And Strapi has a habit of creating tables in your database if you're playing around with things, but never cleans them up (though I hope that fixed this or will fix it).
# discuss
- ## 

- ## 

- ## [Any Experience with Strapi or Directus HeadlessCMS? : node_202112](https://www.reddit.com/r/node/comments/r7c7fy/any_experience_with_strapi_or_directus_headlesscms/)
- Directus is brilliant. It's just an overlay over your SQL, so you don't need to migrate at all, all you need to do is tell it which fields are relations.
  - And if you ever do decide to move on, you can just delete the tables Directus adds, and your data is pure again.


- Strapi uses both SQL and NoSQL databases(NoSQL removed after v4), it's not SQL database-minded, and it's very slow compared to Directus. But on the other hand, it's more simple. Also, there are no field-level permissions, and If you need it, you have to code it. I just mentioned some issues. Of course, Strapi has many, many features and benefits.


- 
- 
- 
- 
- 
- 

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
