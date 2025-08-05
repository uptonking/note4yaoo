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

# discuss
- ## 

- ## 

- ## 🔒 [OpenID Connect (OIDC) _202503](https://github.com/suitenumerique/docs/issues/735)
  - OpenID Connect is a robust standard across the industry (supported with other solutions, e.g. Authelia, Authentik)

- Looks like it has support for OIDC because it is mentioned in the code and k8s deployment documentation as well as development environmental values .

- Looking at the track record of auth0, octa etc in recent years, I think there is zero guarantee that external auth providers do actually provide better security than just sticking to django builtins. OIDC still may make sense for larger installations, though.

- We do support OIDC so I'll close this. For user management we're building a separate product : suitenumerique/people
  - People is not live yet so we don't tackle user management out of what's offered in Django Admin

- ## is it possible to deploy Docs without any AuthN whatsoever? _202503
- https://matrix.to/#/!pKqGwFDkjqlFyJabhP:matrix.org/$nvAFuaU-kjXn8fXzL0AVRsrihaVblOLDG9spe-WVjto?via=matrix.org&via=linagora.com&via=tchncs.de
- it's possible to deploy it but nobody will be able to use it 
- It would not be hard to install a third party user account management app like https://github.com/incuna/django-user-management/

- User management is handle via keycloak (or your own oidc sso)
# discuss-devops/toolchain
- ## 

- ## 

- ## 

- ## I'm looking for a lightweight alternative to Keycloak that's more suitable for small development teams. 
- https://matrix.to/#/!pKqGwFDkjqlFyJabhP:matrix.org/$M0nsa9zzmntwzlEN63wCVyvRjS97Rtubu5a8SgjH_sQ?via=matrix.org&via=linagora.com&via=tchncs.de
  - Ideally, something easy to set up, less resource-intensive, and focused on core authentication and authorization features (OIDC/OAuth2).
  - I've already looked into Authelia and tried Hydra+Kratos, but I'm specifically interested in solutions that also include managing user identities for web applications — not just authorization servers.

- Authentik sounded like a good modern alternative last time i checked.
# discuss-internals/codebase
- ## 

- ## 

- ## 

- ## 

- ## [Allow organizing documents in a tree structure · Pull Request _202501](https://github.com/suitenumerique/docs/pull/516)
  - This pull request introduces a hierarchical organization for documents by implementing a tree structure. 
  - It integrates the `django-treebeard` library to manage the tree hierarchy, allowing documents to be nested within parent documents. 
  - Update document models to include parent-child relationships.

- Looks perfect frontside, 1million docs, 5000 per users, works great, we are not even using db index apparently so it even lets room to speed improvement.

- ## 🤔 [Store documents in a stable format _202506](https://github.com/suitenumerique/docs/issues/1043)
  - Currently, Docs stores all documents in a Y.js buffer format, which does not have any stability guarantee. 
  - Y.js messages are only supposed to be stored in order to be sent to currently-offline users. If Y.js breaks their format, or if BlockNote breaks their own (which happens from time to time), many documents will break. 
  - Documents should be stored in a stable format, be it Markdown, HTML, anything really, even a standardized JSON object would be fine
  - I recently had the opportunity to discuss with some of the (lovely) persons working on BlockNote, and I understand that my initial comment was wrong ; Docs doesn't store update buffers but rather snapshots that can be used to rebuild the original Y.js document. 
  - But, you can absolutely make realtime work without storing Y.js documents. That's what we do in our app that also uses BlockNote, and it works flawlessly.
- Basically the way we do it in our project is:
  - If the client is the first to connect, the editor is directly initialized with the document's content
  - If there are other players in the realtime session, we sync the current user with them

- It is important to save a YDoc to have the collaboration working correctly.
  - initially we saved the Blocknote json, but when users are collaborating and a new user arrives, it didn't sync correctly.

- The Y.js update encoding has been stable & backwards compatible since it began as a project (~2011)
  - It is always extract-able to json, if you can read the document in clear text.
  - Side note, it isn't technically a "format", a format determines the structure of some data, whereas Y.js is merely an encoding for document content in this case (since you can go from Y.js <-> JSON interchangeably).
  - While we can talk more about the formats that docs should support (especially in regards to durability when projects are changing like BlockNote), Y.js should be treated as the source of truth for collaborative documents (since it's merging properties are only valid against other Y.js update). It is okay to break this rule of thumb in specific scenarios like single user editing but, not in the general case.
  - One approach often recommended is to store not just Y.js updates in the database, but also to store some secondary format alongside it. This makes it easier to retrieve the document content for things which are read-only, but all writes should be made by Y.js updates.

- yjs allows the user to come back from being offline & their changes would sync just like any other.
- it wouldn't be possible if the "raw" document (e.g. Markdown) was used. Is that right?  
  - Yep, that is exactly right, Y.js would support that.

- ## Django uses the Cookie header of the request to authenticate, 
- https://matrix.to/#/!pKqGwFDkjqlFyJabhP:matrix.org/$e6xbeZ40igEQ3f-vjQUpRZKJ8OXMJxxk9aSu7vOli9c?via=matrix.org&via=linagora.com&via=tchncs.de
  - the session middleware parses it, reads the session id from it, and then searches for the the correct user and attaches it to the session object.
- I had to do now a couple of things to get it running:
  - frontend and backend should indeed run on the same domain, so that I do not have to override any cookie policies. cookies are per default not transported cross-domain
  - as the dev backend now runs with a path prefix, I needed to tell the django stack, that there is a prefix. Otherwise it simply omits it when e.g. constructing redirect uris for the authenticate requests to keycloak.
  - I needed to change the CSRF trusted domains for the django stack.

- ## What are the features where celery is required? _202507
- https://matrix.to/#/!pKqGwFDkjqlFyJabhP:matrix.org/$E9yxykAo7ED3CAQpNIdZqOGtwiuhqIx_1Q8Z6UVyfks?via=matrix.org&via=linagora.com&via=tchncs.de
- Celery allocates some RAM, 150Mb in the best case, which can seem very much OK in many cases but can be heavy in the context of self-hosting

- it's used for asynchronous tasks. To this day only one task is asynchronous: send email to admins when user ask for access
  - I feel like it remains lots of effort for something that does not bring much added value. I would prefer something to just by-pass celery and run the tasks synchronously to "ask for access".
  - But maybe I should disable Celery for now, until there exists some task that justifies its reintroduction (regarding the amount of resources and the effort required).

- Third packages have also shared task used. For example in `django-lasuite` package, the `malware_detection` application is using shared tasks

- the simplest way to get rid of celery in this situation is to replace it with postgresql with something like https://github.com/PaulGilmartin/django-pgpubsub
# discuss-ai 👾
- ## 

- ## 

- ## [Blocknote AI _202505](https://github.com/suitenumerique/docs/pull/1016)
  - Possibility to revert what the AI made
  - Collaborative friendly - Other collaborators will see the AI changes only when changes are accepted
  - This feature is under AGPL license.

- ## [Improve AI requests _202503](https://github.com/suitenumerique/docs/issues/694)
  - Translation seems to be an easy task, we can use meta-llama/Llama-3.1-8B-Instruct, the request will be faster
  - We can stream the response, by streaming the response we will be able to display content the the user gradually.

# discuss-roadmap
- ## 

- ## 

- ## 👀 [Templates library _202507](https://github.com/suitenumerique/docs/issues/1125)
  - Users have templates for meeting minutes, product requirement documents, briefs etc.

- ## [Doc of Docs _202501](https://github.com/suitenumerique/docs/issues/576)
  - we will improve the documentation of Docs with md files, in the root/documentations folder.

- For tech docs, the docs-as-code approach supposes that the tech stack is mastered by several members of the team, and that the stack automates as many moving parts as possible (for instance, merging a doc-changing PR triggers a workflow to update the live site).

- I think that Docs documentation should be using Docs. It would be a grate showcase of the project.

- I'm not entirely convinced by using Docs for the Documentation. While indeed it makes it a great showcase for Docs, the workflow would be too complicated at the moment. It would be a great solution in the future though.

- I agree that requiring contributors to use git in order to contribute to a Docs-hosted documentation would be counter-productive. Either Docs is use as-is, or it's not used.

- ## 🤔 [Folder view -> integration with Drive _202505](https://github.com/suitenumerique/docs/issues/964)
  - Organise drive files in folders / shared workspaces that exist in Drive.

- Being able to create docs from drive is definitely in the roadmap yes !
  - Having a folder view in Docs is not.

- ## [Support WOPI protocol for Nextcloud / OpenCloud integration _202503](https://github.com/suitenumerique/docs/issues/815)
  - Are there any plans on nextcloud integration yet?

- WOPI support would also enable integration in OpenCloud. We would happily integrate.

- I study the server part of the WOPI protocol in order to implement it in the drive project.
  - For docs, it is the client part of the WOPI protocol that should be implemented.

- ## [Which external file format should we support first for imports ? _202503](https://github.com/suitenumerique/docs/issues/806)

- ## 📈 [Adding support for formulas _202504](https://github.com/suitenumerique/docs/issues/859)
  - As a Coda user (a tool very much like Notion), I do a lot of formulas in my docs.
  - By typing = the formulae form would show up, allowing user to enter a "math" expression, allowing referencing cells from table.

- ## 📈 [Notion like databases _202501](https://github.com/suitenumerique/docs/issues/538)
- I believe that the experience of using Notion is awesome because of the databases it allows things as different as:
  - creating a Kanban board
  - mapping your organisation to entities linking them together and providing infinite options of navigation, filtering, views

# discuss-changelog
- ## 

- ## 

- ## [✨(frontend) add multi columns support for editor _20250725](https://github.com/suitenumerique/docs/commit/11d0bafc94ff277232bcc4cfedbf80f6fc97e24f)

- ## I saw the feature for Subpages got merged into main. v3.4.0 _20250710

- [✨(frontend) create page from slash menu _20250731](https://github.com/suitenumerique/docs/commit/afa48b6675063bc8682bcd6df45b554541a89345)

- ## [downgrade to docx 9.5.0 _202506](https://github.com/suitenumerique/docs/commit/9f222bbaa3c732d9e9fc5a391a868f6997f84806)
  - Prob compatibility issue with docx 9.5.1 and BlockNote. We downgrade to 9.5.0 for now until BlockNote is updated to support docx 9.5.1

- ## [(back) remove usage of deprecated db engine _202506](https://github.com/suitenumerique/docs/commit/6964686f7c0a08935e7bbfaca0aa6f5662dc3d6d)
  - The db engine `postgresql_psycopg2` does not exists anymore in django but for BC compat it is possible to use it in the configuration and it is replace by postgresql at runtime.
  - `django.db.backends.postgresql_psycopg2` > `django.db.backends.postgresql`
