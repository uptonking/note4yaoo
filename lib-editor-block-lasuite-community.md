---
title: lib-editor-block-lasuite-community
tags: [community, lasuite-docs, notion-like]
created: 2025-07-17T14:39:47.645Z
modified: 2025-07-17T14:40:07.230Z
---

# lib-editor-block-lasuite-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 🚀 [Docs – Open source alternative to Notion or Outline | Hacker News _202503](https://news.ycombinator.com/item?id=43378239)

- https://x.com/YousefED/status/1901367050435465362
  - The open source and collaborative document editor we're building with the French and German governments just hit the top of HN. _202503
  - Really wish there is a proper browser based Notion Alternative but with the Obsidian Editing Experience (Liveview). All those Notion like Block Editors really struggle with copy/paste the content imo, especially when using it with LLMs.

- The hard part in a project like Docs is the text editor. We built Docs on top of [Blocknotejs]

- What led to the choice of using Blocknote over other editor packages? 
  - We've built BlockNote to come "batteries-included" with common UI components and a simpler API to make it easy for you to add a modern, block-based editor to your app.
  - The BlockNotejs team researched the live editing space thoroughly so we could just follow the tracks: BlockNotejs, HocusPocus, Yjs. We "just" had to build the wrapper around with authentication, docs permissions and search and boom you have Docs!

- Does this provide database functionality like seen in Notion?
  - The database of La Suite is `Grist`.

- Did you consider building on top of some existing open source solutions like Docmost, Appflowy, or AFFiNE?
  - we dedided to take an approach where we build on top of libraries like BlockNotejs, Yjs, HocusPocus but build our own wrapper around it in Django and Next.js. This allows to iterate really fast and to catter our own need (we are large organizations we don't have the same as startups or SMEs).

- Tchap looks neat as a Slack alternative, but it seems like it's still only for government workers.
  - Tchap is just Element/Matrix with some gov specific features.

- Honestly it's a reasonable set of dependencies:
  * Postgres for permanent storage
  * an OIDC identity provider so you don't have to make your own password system
  * Redis for caching
  * S3-compatible object storage (so you don't have to reinvent file uploads)
  * The app itself

- Have you tried TriliumNext? It doesn't have collaboration for editing but sharing is built in, It lets you structure your notes in a way that's reminiscent of object oriented programming (you've got templates to define types, inheritance of attributes to instantiate and specialize them, etc). I have hierarchies of hundreds/thousands of notes that for all intent and purposes are as good as Notion's Databases

- This is a really great project from both the French and German governments.
  - I think state-funded open source solutions to digital platforms is a fantastic opportunity to get away from the big tech walled gardens. 
  - Of course, there is always the risk that this becomes unmaintained in the future, but the community at least can take over.

- Notion has a very flexible data model. We use it mainly for documents, but it also can contain databases, which can be viewed as kanban boards, timelines, etc.
  - It's really nice to have one place to go for all kinds of content, but that content can link within itself, @mention other pieces of content, etc.

- Evernote had the best mechanism, giving you an XML file and an official XSLT to read/verify/transform what they give you. However, Evernote feels very underpowered when you start to use formulae and automation across your database.

- please name some open source (or lower priced) alternatives that support: comments on documents, database functionality to a similar level, publishing websites, scripting for properties. I'm very curious!
  - I was going to say git, but really you need the whole environment.

- 
- 
- 
- 
- 
- 
- 
- 

# discuss-suite-docs
- ## 

- ## 

- ## 

- ## 
# discuss-suite-docs-internals
- ## 

- ## 

- ## 

- ## What are the features where celery is required? _202507
- https://matrix.to/#/!pKqGwFDkjqlFyJabhP:matrix.org/$E9yxykAo7ED3CAQpNIdZqOGtwiuhqIx_1Q8Z6UVyfks?via=matrix.org&via=linagora.com&via=tchncs.de
- it's used for asynchronous tasks. To this day only one task is asynchronous

- Third packages have also shared task used. For example in `django-lasuite` package, the `malware_detection` application is using shared tasks

- I feel like it remains lots of effort for something that does not bring much added value. I would prefer something to just by-pass celery and run the tasks synchronously to "ask for access".
# discuss-suite-docs-roadmap
- ## 

- ## 

- ## [Support WOPI protocol for Nextcloud / OpenCloud integration _202503](https://github.com/suitenumerique/docs/issues/815)
  - Are there any plans on nextcloud integration yet?

- WOPI support would also enable integration in OpenCloud. We would happily integrate.

- I study the server part of the WOPI protocol in order to implement it in the drive project.
  - For docs, it is the client part of the WOPI protocol that should be implemented.

- ## [Which external file format should we support first for imports ? _202503](https://github.com/suitenumerique/docs/issues/806)

# discuss-suite-docs-changelog
- ## 

- ## I saw the feature for Subpages got merged into main. v3.4.0 _20250710

- ## [downgrade to docx 9.5.0 _202506](https://github.com/suitenumerique/docs/commit/9f222bbaa3c732d9e9fc5a391a868f6997f84806)
  - Prob compatibility issue with docx 9.5.1 and BlockNote. We downgrade to 9.5.0 for now until BlockNote is updated to support docx 9.5.1

- ## [(back) remove usage of deprecated db engine _202506](https://github.com/suitenumerique/docs/commit/6964686f7c0a08935e7bbfaca0aa6f5662dc3d6d)
  - The db engine `postgresql_psycopg2` does not exists anymore in django but for BC compat it is possible to use it in the configuration and it is replace by postgresql at runtime.
  - `django.db.backends.postgresql_psycopg2` > `django.db.backends.postgresql`
