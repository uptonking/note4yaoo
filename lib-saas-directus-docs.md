---
title: lib-saas-directus-docs
tags: [directus, docs]
created: 2024-03-02T15:21:09.587Z
modified: 2024-03-02T15:21:17.619Z
---

# lib-saas-directus-docs

# guide

# [docs](https://docs.directus.io/)
- Directus is an Open Data Platform built to democratize the database.
- Built entirely in Typescript, primarily on Node.js and Vue.js, Directus is 100% open-source, modular and extensible

- At the highest level, Directus organizes its features and functionality into Modules. 
  - Each Module allows you to interact with data in some specific way, such as data and content management, digital file asset management, drag and drop analytics dashboard creation, or whatever.

- How It Works
- Directus is installed as a layer on top of your new or existing SQL database.
  - The App and API dynamically "mirror" your actual schema and content in real-time. 
  - This is similar to how technical database clients (like phpMyAdmin) work
  - Direct database access and the full power of raw, complex SQL queries.
- Directus is plug-and-play. Once linked, it doesn't own your data or file assets, but it does create about 20 new data tables which are required for platform operation. 
  - These tables do not intermingle(混合) with the rest of your data, so you can remove Directus without a trace.

## version-history

- [Content Versions | Directus Docs](https://docs.directus.io/reference/system/versions.html)

- Content Versioning enables users to create unpublished copies of an item (called "Content Versions"), modify them independently from the main version, and promote them to become the new main version when ready.

- ⌛️ [Revisions | Directus Docs](https://docs.directus.io/reference/system/revisions.html)
- Revisions are individual changes to items made. 
- Directus keeps track of changes made, so you're able to revert to a previous state at will
- Revisions are created whenever an Item is updated. 
  - These alternate versions are tracked so that previous states can be recovered. 
  - 🧐 Every change made to items in Directus is stored as a complete versioned snapshot and a set of specific changes made (the delta). 
  - The revisions system is tightly coupled to the activity logs system, with each revision linked to the activity event where it was created.

- [Implementing Content Versioning | Directus Docs](https://docs.directus.io/guides/headless-cms/content-versioning.html)
- A version is a snapshot of a piece of content at a particular point in time. 
  - Each version represents the state of the content at a specific moment, 
  - and it can be used to track changes and maintain a history of the content.
- Main: The main version is the original version of a piece of content that has been created and published. 
  - It is the default version that is displayed to users. 
  - The main version is the "source of truth" for all other versions.
- Promote: Promoting a version means to make it the new main version. 
  - When a new version is promoted, it becomes the main version that is displayed to users, and it replaces the previous main version.

- Under the hood, content versions are stored in the `directus_revisions` collection. 
  - In bigger projects this collection can get large.
  - Some Directus users combat this my periodically purging some or all data in this collection.

## 🔀🤝🏻 [Introducing Content Versioning v10.7.0 _20231023](https://directus.io/blog/introducing-content-versioning)

- Today we're releasing Content Versioning as part of Directus v10.7.
  - This unlocks two powerful new authoring workflows - preparing draft updates of content without publishing them, and collaboration with others without accidentally overwriting content.
- Content Versioning is not just a feature; 
  - it's a step forward in making Directus a more collaborative platform

## [Extensions | Directus Docs](https://docs.directus.io/extensions/introduction.html)

- Extensions provide a way to build, modify or expand Directus' functionality beyond the default
- There are three main categories of extensions:
  - App Extensions
    - App extensions (also known as frontend extensions) provide visual and client-side modifications to the Directus App.
    - ui-elements, Layouts, Panels, Modules, Themes
  - API Extensions
    - API extensions (also known as backend extensions) modify Directus server-side related functionalities such as APIs, data sources and custom workflows.
    - Endpoints, Hooks
  - Hybrid Extensions
    - modify both frontend and backend functionality
    - Flow Operations are small modules inside flows that allow for complex processes
    - Bundles enable you to combine multiple extensions into a single, larger extension.

## [API Reference | Directus Docs](https://docs.directus.io/reference/introduction.html)

- Directus offers both a REST and GraphQL API to manage the data in the database.
- There is no difference in the functionality available between the REST and GraphQL endpoints. 
  - The functionality available in both is mapped to the same set of core services, meaning that you don't lose any performance or capabilities by choosing one or the other.
# more
