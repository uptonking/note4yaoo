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

- ## 🆚️ I recently migrated PPResume's API server from strapi to payload
- https://twitter.com/xiaohanyu1988/status/1743954693821493676
  - It is a hard decision and cost me almost a month for the migration. Here's why.
- Strapi's pain points: 
  - 1) it does not allow one user to have multiple authentication providers, which is a very almost a deal breaker if you want to allow users to sign in via multiple social providers (googlo/facebook etc).
  - 2) Strapi's TypeScript is poor, the core modules (services/controllers etc) have a very tiny type annotations and often you need to console.log() in order to see which methods are available if you want to do some customizations.
  - 3) Strapi's DB migration is still experimental. And the common to initialize a DB is to click via GUI (and GUI will generate some code for you).
  - 4) Strapi provide a builtin RBAC system, which also has its own pros and cons. The cons here is, it is tightly coupled with strapi, and it by default generate around 10+ tables just for strapi RBAC. If strapi's RBAC don't fit you case, it is very hard to get rid of it.
- @payloadcms provides: 
  - 1) very flexible access control (in global/collection/field level), which makes it very easy to plug in your own auth system, 
  - 2) native TypeScript, DX is fun and easy, 
  - 3) declarative model and DB migration.
  - Last but not least, @payloadcms generated only 3 builtin tables, which makes the DB very clean and tidy, while strapi by default generated 20+ tables in your DB, no matter whether you need it or not. 

# discuss-strapi-directus
- ## 

- ## 

- ## [Strapi vs Directus : r/Strapi _202205](https://www.reddit.com/r/Strapi/comments/uwnosc/strapi_vs_directus/)
- in Strapi our i18n feature is very similar as a functional manyToMany relation but we abstract it away 
  - But the major difference between us and Directus is our approach to schemas. 
  - Directus is database first whereas we focus on source-control based. Kinda the difference between a "one and done" deployment or a CI/CD application.

- ## [Directus vs Strapi : Comparing the headless CMS features : r/node _202301](https://www.reddit.com/r/node/comments/108fc3k/directus_vs_strapi_comparing_the_headless_cms/)
- Directus has no role based access control for their Admin UI. You can either give a user access to the entire Admin or let them be with no access. Their role based access control is only for the APIs.
  - In contrast, Strapi allows a granular role based Admin UI access (in addition to the same for API).
  - From my experience on this - it's a big limitation for enterprise CMS implementations where multiple content teams have access to the CMS and each need to be provided access only to some CMS tables/functionalities via the Admin UI.
- Not true, within Directus you can create new roles as you like, and append which 'collection' it is able to create, read, update or delete within the Admin UI.
  - You might tried Directus before this was implemented, but it's definitely possible.

- Directus' REST API is so nice with their HTTP 'search' method for querying data

- Yes! Strapi 4.5 has contains and containsi (I think that is the name) for searches too. Strapi 4.x is a lot better but their data migration for upgrades from 3.x to 4.x is super complicated.

- ## 🆚️💡 [Strapi vs Directus: why you should go for Directus : r/webdev _202209](https://www.reddit.com/r/webdev/comments/xphtbk/strapi_vs_directus_why_you_should_go_for_directus/)

- Things I missed while trying out Directus that Strapi did better:
  - a decent way to model a multi level navigation module / component
  - intuitive way for components / reusable blocks like a page builder, the m2a is honestly not as good as strapi
  - support for multiple languages on directus seems hacky
- Other than that I loved the speed of the running bunny and no need to wait for restarts.

- 🐛 Some of these things listed as pros kinda fall apart when you use Directus in production. Here's some of my pain points of using Directus in production 
- The search is not very useful, this is probably the biggest problem with directus since search is obviously very important feature. 
  - If you have articles with translations, the search wont find articles by title, it won't find articles by text included in articles, it won't find articles by your tagged authors. 
  - That's because the search only works on direct fields on the articles table and doesn't work for relations. 
  - Now there is a flexible search system where you click through lots of relations and write filters, but good luck finding a non engineer who understands how it is used.
- Another pain point which is pointed as a pro in the article: The views are not that good. 
  - You can edit custom views for your editors to use, but once they open the view even once it will be "forked" for them and now any changes you make to the views won't show up to the editors anymore. 
  - Also, there's no way to give view columns custom names which is obviously a problem since if you add author.name column the column name will be "name". 
- While the UI looks good, it's somewhat unintuitive, especially translations. 
  - Even though it's somewhat "natively supported" by directus. Opening a content that has translations just selects some language for you, instead of showing the language that actually has translation. That leaves editors wondering why the content is empty.
- Another super common issue is that the editor will write their content to the wrong language and then they have to switch between languages copypasting the content. 
- I think the configuration is obvious, I think it's better to have the configuration in files instead of in database because it makes it so much easier to automatically deploy stuff.
- Flows kinda look cool as some sort of tech demo, but I don't really see any actual usecase for them. 
  - A non programmer can't really use them since you need to still understand lots of stuff and know all the magic variables that are available. 
  - And when a dev is doing it, it's way easier to just write the hook in typescript/javascript. For example you can't really make dele
- Overall the process of how Directus works with automatic deployments doesn't seem to be thought about that much meaning that you'll have to resort to hacky stuff to make things work. 
  - For example you really need 2 different kind of migrations, those that run before directus migrations and those that run after. But there's really no support for this and I think some "official" answer around this was to move the after. 
  - There is this schema import/export but it doesn't really export everything you need, so you'll still need migrations or some other way to populate rest of the stuff you need. 
  - Also you're going to have to figure out why after every deployment you can't edit any content, because directus has cached your db schema and for some reason directus cli cache apply doesn't reset the cache.
- The javascript SDK isn't very good which is why we're considering just using the database directly when reading data from directus. 
  - Especially any proper support for typescript would be really needed. Directus already knows my schema so it's a shame I have to write it again for some ORM to have proper data access.

- Strapi is more popular because they received funding rounds early on in their project development. This lead them to sussing out tech bloggers, youtubers and other people and making them try their cms.

- directus support websockets (also in and out). a few other flows that strapi doesn't . Actually this seems to be one of the big diff on features from Directus side because it have websocket, cron, manual, hook and you can chain an combine flows even run custom js code based on the flow.

- Having worked with both as a freelancer, here's my brief take:
  - Directus seems more polished and really works with whatever database schema you got. This was perfect for reusing existing data rather than having a whole migration process set up. 
    - The UI is a lot cleaner too. Bonus points for it being Vue. 
    - Only downside was during the v9 beta were a lot of things were breaking but that was to be expected.
  - Strapi is decent if you're trying to introduce end users to a Wordpress alternative. I think this is the closest one to looking like Wordpress. 
    - The only downside was in building extensions. It was a bit convoluted the way I had to fetch and render certain models.

- ## [Is strapi(or headless cms in general) the right tool to use if I already have an existing backend api? : Strapi_202203](https://www.reddit.com/r/Strapi/comments/tj5afk/is_strapior_headless_cms_in_general_the_right/)
- 🐛 We do not support importing existing databases yet, sadly I don't think we are what you are looking for
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
# discuss-lowcode
- ## 

- ## 低代码这东西老板不会用，程序员不会用。
- https://twitter.com/xicilion/status/1756797587896873445
- 基本上低码只能handle简单重复的那部分开发， 复杂的和customized 的部分用低码比自己写的麻烦恶心多了
- 降本增效的情况下，让低水平的外包用，甚至产品和业务人员直接用（一些标准化的简单流程，报表类）

- https://twitter.com/belliedmonkey/status/1756720462326088150
- 我觉得低代码这个名字就取得不好，让专业程序员天然想排斥。
  - 应该叫类似于shipfast，“快搭” 这样的名字。
  - 因为代码量减少是手段，提高效率降低成本才是目标。客户更喜欢你直接帮他完成目标而不是给他一个方法。
- 甚至更垂直一点，线上商城快搭平台
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
