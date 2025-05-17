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

- ## [reengineering frontend ui rendering · Issue · odoo/odoo _202301](https://github.com/odoo/odoo/issues/109704)
  - this xml view and js is very slow and generating server side makes respones for ui generation is very boring and slow for the user of software

- LOL, even with server side rendering of xml views, odoo web client (it is javascript single page application in v16) is ridiculously slow. You want to make it even slower by transferring view generation code from server to the client ?
  - It is already almost unbearably slow because odoo developers decided to move to a single-page-application design. This made 11+ versions of odoo slower and slower and slower. Just install odoo 10 and compare speed.
# discuss
- ## 

- ## [Support CockroachDB as alternative to PostgreSQL · Issue · odoo/odoo _202202](https://github.com/odoo/odoo/issues/83730)
- if you aren't at scale then you don't really need cockroachdb. Postgres is perfectly acceptable and all the major cloud services off it as a service again perfectly acceptable for even midsized installs.
  - But also being distributed it means sequential index performance sucks. And that is what Odoo uses for primary keys. And for an ERP that makes a whole lot of sense (compared to say GUIID's) if you think about the time value of information and how records are typically inserted.
  - And no support for `pg_trgm` probably the most necessary postgres extension for odoo with any volume, given the typical use case is openended ilike searches. I've followed the project fairly closely and for me it is still just nowhere near requirements.
  - I simply cannot see how you can scale Odoo with CockroachDB's current feature set and Odoo's current architecture. And if you aren't at scale why would you bother? Just use someone else managed service and forget about it.

- [sql: support NOTIFY, LISTEN, and UNLISTEN commands of postgresql · Issue · cockroachdb/cockroach _201910](https://github.com/cockroachdb/cockroach/issues/41522)
  - PostgreSQL has support for NOTIFY, LISTEN, and UNLISTEN commands which generate and listen for a notification, respectively. This is not a part of SQL standard; however, some ORMs (like go-pg) seems to be using it.

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

- The odoo app store is really where I think it will do well. We hade like 4 modules that we purchased and installed for our build

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

- It is open core. More and more parts are removed from the open source part and require a license.
