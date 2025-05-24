---
title: lib-saas-odoo-community
tags: [community, odoo]
created: 2025-05-17T18:55:01.438Z
modified: 2025-05-17T18:55:18.257Z
---

# lib-saas-odoo-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-not-yet
- ## 

- ## 

- ## [Support CockroachDB as alternative to PostgreSQL · Issue · odoo/odoo _202202](https://github.com/odoo/odoo/issues/83730)
- if you aren't at scale then you don't really need cockroachdb. Postgres is perfectly acceptable and all the major cloud services off it as a service again perfectly acceptable for even midsized installs.
  - But also being distributed it means sequential index performance sucks. And that is what Odoo uses for primary keys. And for an ERP that makes a whole lot of sense (compared to say GUIID's) if you think about the time value of information and how records are typically inserted.
  - And no support for `pg_trgm` probably the most necessary postgres extension for odoo with any volume, given the typical use case is openended ilike searches. I've followed the project fairly closely and for me it is still just nowhere near requirements.
  - I simply cannot see how you can scale Odoo with CockroachDB's current feature set and Odoo's current architecture. And if you aren't at scale why would you bother? Just use someone else managed service and forget about it.

- [sql: support NOTIFY, LISTEN, and UNLISTEN commands of postgresql · Issue · cockroachdb/cockroach _201910](https://github.com/cockroachdb/cockroach/issues/41522)
  - PostgreSQL has support for NOTIFY, LISTEN, and UNLISTEN commands which generate and listen for a notification, respectively. This is not a part of SQL standard; however, some ORMs (like go-pg) seems to be using it.

- ## [reengineering frontend ui rendering · Issue · odoo/odoo _202301](https://github.com/odoo/odoo/issues/109704)
  - this xml view and js is very slow and generating server side makes respones for ui generation is very boring and slow for the user of software

- LOL, even with server side rendering of xml views, odoo web client (it is javascript single page application in v16) is ridiculously slow. You want to make it even slower by transferring view generation code from server to the client ?
  - It is already almost unbearably slow because odoo developers decided to move to a single-page-application design. This made 11+ versions of odoo slower and slower and slower. Just install odoo 10 and compare speed.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## [Odoo现在流行吗，如果从事Odoo开发，以后前景怎样呢？ - 知乎](https://www.zhihu.com/question/335807070)
- ODOO 没前途，从openerp到现在，版本之间不兼容，模块变化也很大。二次开发的很多方法也不兼容。
  - 10多年前改了几个版本，受够了，连基本的版本兼容也做不到。
- 202311: 血泪经验：不要用它做大量的定制化开发。。。主要问题：
  - 1、版本兼容问题，13、14、15、16，最近的几个版本，底层架构变化太大（特别是前端实现），基本上无法平滑升级，当然如果小应用，你说我就一直不升级，当然也可以，最后造成的结果，可能就是你有一堆版本的Odoo应用； 
  - 2、性能问题，并发量一大就很明显，谁用谁知道；
  - 3、模块虽多，但是符合国情的非常少；
  - 4、不好招人，因为没有几个人愿意学，这是企业和新人都需要考虑的一个很现实的问题

- 看以odoo免费，实际定制开发的成本更高，还不如一个用友、或者金蝶呢。

- 金蝶太贵了，小企业根本消费不起


- ## [What's SAP, and why's it worth $163B? (2020) | Hacker News _202209](https://news.ycombinator.com/item?id=32776276)
- Every single company I interacted with used SAP. It is the de facto software in its field and is deeply entrenched. Its UX is the most horribly wicked thing I’ve ever come across. 
  - The initial learning curve felt far too high. 

- Customizing odoo is a nightmare it is similar to "It doesn't do everything you want, but it does everything your business needs". (quote by Larry Ellison about Oracle ERP). Underneath its a mess but at least its open source.
- What did you find is a mess about Odoo? And why is customizing it a nightmare?
  - SQL database was a large amount of tables alike and if you try to add a feature that it doesn't implement yet (such as drop shipping capabilities) I couldn't figure it out because its not as simple as creating a new set of forms like in Django you basically have to understand the whole system and I think the task would take a year. It would have been better to integrate an existing system instead.

- There are two major ERP software out there right now: SAP and Peoplesoft.
  - SAP is the "European" way of doing things, which means there's one right way and you need to align your business to SAP's way of doing things. If you do that, things work very well.
  - Peoplesoft is the "American" way of doing it, which means that you make your software fit around you. This means a lot of customizations. This makes integrations much more challenging if you're too far off kilter, and things like upgrading is much much harder, because there's too many customizations.
  - That's the information I had about 10 years old and not sure how much SAP has evolved since then.
- Oracle acquired Peoplesoft and Netsuite long ago. Oracle has its Fusion product where it attempts to fuse their acquisitions into one platform
- PeopleSoft became part of Oracle (and now uses the Oracle brand) and some of their people left and founded Workday.

- If anyone thinks about going for odoo - which I did for a customer - do yourself a favor and try anything else. Here's why:
  - The developer experience is terrible, simple template changes need a your modules to be "upgraded" which means every change takes several seconds at least.
  - The quality of the app ecosystem is so bad you almost can't install any non-core apps if you want to be able to maintain your project. And apps are incredibly expensive (250€ for a GDPR compliant cookie banner). 
  - The documentation is partially non-existing and you're supposed to read odoo's code to know how things works - which is true, but quite time consuming.

- ## [Open source ERP written in Go : r/golang _202412](https://www.reddit.com/r/golang/comments/1hnf6nx/open_source_erp_written_in_go/)
  - developing an Odoo alternative with Go, Alpine.js, Templ and HTMX
- There are many OpenSource ERP other than Odoo. Some things that Odoo has, and I don't believe can be decently achieved in a compiled language is:
  - the capacity to extend existing models seamlessly
  - this includes extending methods to change their behaviors
  - a fool proof ORM with automatic search features, view generation, ..
  - model-based permissions (compared to route-based/action-based) with configurable permission system (i.e. no hardcoded groups)
- These features are IMO the strongest points of Odoo if you want to compare to it specifically.

- This is why I don't believe that a compiled language can offer has much extensiom capabilities has an interpreted one.
  - Odoo uses the same metaclass everywhere and uses the "__inherit__" attribute to classify the definitions. Then, a class is gemerated at runtime from the aggregated definitions. This is the runtime aggregation capability that is missing in Go and in all compiled languages. In python, you could replace the "models. Model" inheritance by something like: registry.add("mymodel", MyModel) This generation has massive advantages compared to inheritance.

- I’ve worked for a startup which used Odoo. It has a lot of features and plug-ins people buy which could be how you can maybe revenue. A marketplace like steam and you take a cut is also another avenue.
  - One major pain point personally for odoo was the dev experience. We used odoo 14 which was tightly coupled with Postgres 12. Upgrading odoo felt scary because there would be breaking changes. Also things like Celery was not easy to integrate.

- What other hurdles(障碍；围栏) did you have with Odoo that we could improve on?
  - The odoo ORM was atrocious(恶劣的, 糟糕的), they made their own implementation on top of psycopg. Since it’s on python, had dependency hell which as i mentioned made celery impossible to add without breaking everything.
  - They had very bad default implementation like using the file system to store session cookies. To use redis for session store you can buy a plug-in but it was a 1 week task for me. I found this shady.
  - The database migration system is super slow with no reason to be. We had a small product for a B2B where we had 1000 weekly active users. Our codebase wasn’t that big but still took 10s of minutes to migrate.
  - For their UI system they used their own XML which was very convoluted. Strange inheritance rules.
  - Access management for data was also half baked, could add rules on entire tables but not on columns via their dashboard. Example we have a table called Products, one group can add, edit product details. Only admin should be able to change the price. Would need to add those rules in code in a hacky way by an if condition.
  - The dashboard was very very slow for the amount data and users we had. Would take minutes to filter, search and load screens.

- 
- 
- 

- ## [What doesn't Odoo get more love? : r/Odoo _202410](https://www.reddit.com/r/Odoo/comments/1fvwmzh/what_doesnt_odoo_get_more_love/)
- I still believe Odoo is the best and most affordable ERP you can get. There is nothing else out there that matches the flexibility for the price you get from Odoo.
  - Numbers of users is irrelevant for the implementation cost. It's about apps, industry, complexity, specifics on configuration, ...

- as soon as you want something a little bit specific, you'll learn you have to use a module someone is selling. To use that module, you need Odoo.sh. That's, like 800$ a year more than the plan you were probably paying.

- To be honest Odoo has flexibility other ERR systems users don't even expect to have. We're doing Acumatica implementation and Odoo implementation. Odoo get way more flexibility. Acumatica get more manuals. Odoo bigger community. Acumatica get some features better tested

- For me, I believe that the issue is the complexity of the app. As a single person shop using Odoo is problematic due to the configuration overhead as compared to using more simplistic but specialized software.

- We have spent hundreds of thousands of dollars on support and “Success Packs” to get it working correctly and accurately. We all have come to accept that it was not a good choice, and it definitely is not inexpensive.

- Because there is a lot of competitors, and they are very localized

- ## [Ask HN: Which NoCode platforms are fine? | Hacker News _202110](https://news.ycombinator.com/item?id=28984955)
- Odoo is actively updated by large team in Belgium if I remember correctly, and their paid support is quite good. Odoo is Python atop Postgres, and uses a simple HTML/CSS/js for the frontend. Quite customizable

- ## [Odoo competitors : r/Odoo _202402](https://www.reddit.com/r/Odoo/comments/1amdixa/odoo_competitors/)
- A spin off is flectra. https://flectrahq.com/
  - Another one is Tryton. https://www.tryton.org/
  - Both projects are forks from Odoo from many years ago and went different direction and approach. But still similar in many ways. 
  - Flectra is the most similar to Odoo. In fact some modules from Odoo from older versions work nearly flawless straight in flectra.
- Another one is ErpNext from Frappe. https://erpnext.com/
  - This one also has a lot of traction. It's less advanced than Odoo but in my opinion it looks more clean Ui somehow. Sometimes for small and simple client projects, we propose Erpnext instead of Odoo. They also have way less friction with upgrades. It's not as crazy as Odoo year over year.
- Flectra would be illegal to even exist in many countries. It is a legit scripted copy paste replacing "Odoo" by "Flectra".

- 🛒 The odoo app store is really where I think it will do well. We hade like 4 modules that we purchased and installed for our build

- ERPNEXT could be the best alternative. Much cheaper for startups and 100% open source plus can be self hosted, which you own your data.

- ## [Story of Odoo: Open-Sourced Competitor to Oracle, SAP | Hacker News _201912](https://news.ycombinator.com/item?id=21865699)
- The good
  - The backwards compatibility and desire to not break the core APIs is generally good from what I’ve seen so far. Individual modules depends how much Odoo themselves lean on it afaict. 
- The bad
  - imho testing is a pain. The ORM uses Polish notation to build filters. The ORM itself is quite clever, but it’s also not like any ORM I’ve worked with. 
  - The last few versions have seen more accounting features drop out of community edition. Some of the official apps are basic.
- > The last few versions have seen more accounting features drop out of community edition.
  - V12 saw accounting reports, and iirc budgets and assets moved to enterprise. 
- If they move components to enterprise in a new version, how hard is it for the community to fork the last open source version of those components and port them to work with the newer version?
  - That has happened several times already. The best known fork is probably Tryton, which forked during the OpenERP transition. It has seen a lot of independent development since then
- No, Odoo is not going into that direction. We invest more and more in the community version.

- There are enough open platforms that are at least as good to create "enterprise" functionality, including database frameworks etc. Why would one use a proprietary framework that you have to adapt to, instead of a general purpose platform with some libraries that you can pick and choose from?

- Tryton is a fork of Odoo when it was still called TinyERP, motivated by disagreements among TinyERP founders and early developers on the technical and business directions.

- Odoo is essentially a Python web framework (ORM, UI framework, etc) that happens to include a bunch of apps for typical business needs.

- Odoo is not comparable to SAP or Oracle. We focus mostly on SMEs, with an approach "per app" rather than an ERP.

- It is open core. More and more parts are removed from the open source part and require a license.

- ## [Odoo: The new OpenERP | Hacker News _201405](https://news.ycombinator.com/item?id=7750020)
- > built on the solid foundation of openERP.
  - Solid foundation is a joke. OpenERP is probably one of the shittiest pieces of code every written in Python. Take a look at their ORM code. And, of course they still use floating points for accounting
- the core and base modules (and in theory, all community modules, since they're derived works) of Odoo are Free Software (APGL) and available on Github
