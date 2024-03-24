---
title: lib-saas-directus-docs
tags: [directus, docs]
created: 2024-03-02T15:21:09.587Z
modified: 2024-03-02T15:21:17.619Z
---

# lib-saas-directus-docs

# guide

# [docs](https://docs.directus.io/)

## overview

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

- 〰️ Webhooks are configured within the App (no code required) and send HTTP requests to an external service when a specific event is triggered.
  - 🗑️ Webhooks are a deprecated feature and will be removed from the platform. 
  - This functionality has been fully replaced by Flows

## version-history

### [Content Versions | Directus Docs](https://docs.directus.io/reference/system/versions.html)

- Content Versioning enables users to create unpublished copies of an item (called "Content Versions"), modify them independently from the main version, and promote them to become the new main version when ready.

### ⌛️ [Revisions | Directus Docs](https://docs.directus.io/reference/system/revisions.html)

- Revisions are individual changes to items made. 
- Directus keeps track of changes made, so you're able to revert to a previous state at will
- Revisions are created whenever an Item is updated. 
  - These alternate versions are tracked so that previous states can be recovered. 
  - 🧐 Every change made to items in Directus is stored as a complete versioned snapshot and a set of specific changes made (the delta). 
  - The revisions system is tightly coupled to the activity logs system, with each revision linked to the activity event where it was created.

### [Implementing Content Versioning | Directus Docs](https://docs.directus.io/guides/headless-cms/content-versioning.html)

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

### ⌛️🌵 [Introducing Content Versioning v10.7.0 _20231023](https://directus.io/blog/introducing-content-versioning)

- Today we're releasing Content Versioning as part of Directus v10.7.
  - This unlocks two powerful new authoring workflows - preparing draft updates of content without publishing them, and collaboration with others without accidentally overwriting content.
- Content Versioning is not just a feature; 
  - it's a step forward in making Directus a more collaborative platform

### [Activity | Directus Docs](https://docs.directus.io/reference/system/activity.html)

- All events within Directus are tracked and stored in the activities collection. 
  - This gives you full accountability over everything that happen
- 
- 
- 
- 
- 

## 🔌 [Extensions | Directus Docs](https://docs.directus.io/extensions/introduction.html)

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

- App Extensions and Sandboxed Extensions are available from the Marketplace in all Directus projects 

- 
- 
- 

### [Sandboxed Extensions | Directus Docs](https://docs.directus.io/extensions/sandbox/introduction.html)

- Sandboxed Extensions Framework is designed to provide robust security to your data and maintain strict control over interactions with the external environment by running extension code in an isolated sandbox
- The main purpose of this sandbox is to allow configurations that limit how extensions access your information and communicate externally.
  - they don't have any access to the database, network, or filesystem by default.
- The Sandboxed Extensions Framework is available for API and Hybrid Extensions.

- Isolates only have access to JavaScript standard built-in objects. This means that common runtime functions such as `console` and `setTimeout` are not available.

- In order for extensions to interact with the project's database or host environment, it has to use functions that are made available through the virtual `directus:api` Sandbox SDK.
- 
- 
- 
- 
- 
- 

## [API Reference | Directus Docs](https://docs.directus.io/reference/introduction.html)

- Directus offers both a REST and GraphQL API to manage the data in the database.
- There is no difference in the functionality available between the REST and GraphQL endpoints. 
  - The functionality available in both is mapped to the same set of core services, meaning that you don't lose any performance or capabilities by choosing one or the other.

## 〰️ [Flows | Directus Docs](https://docs.directus.io/app/flows.html)

- Flows enable custom, event-driven data processing and task automation within Directus. 

- Each flow is composed of one trigger, followed by a series of operations.
  - Each flow is made up of three elements: A trigger, operations, and a data chain.

- a trigger defines the action or event that starts the Flow. 
  - This action or event could be some type of transaction within the app, an incoming webhook, a cron job, etc.
- An operation is an action or process performed within the flow. 
  - These enable you to manage data: send off emails, push in-app notifications, send webhooks, and beyond.
- Data Chains
  - In order for a flow's operations to track and access the same data, each flow creates its own data chain. 
  - Every operation has access to this data chain and each operation appends some value onto this object after it runs. 
  - This means you can dynamically access data from a previous operation in the current operation with data chain variables.

- flows let you implement control flow, by providing success paths and failure paths within a flow

- logs store information for each flow execution. 
  - Each log will display information from triggers as well as each operation in the flow
  - Logs are not a 1:1 mapping to the data chain. 
  - Each trigger and operation gets its own dropdown, which stores its relevant data. 

- 
- 
- 

## [Authentication | Directus Docs](https://docs.directus.io/reference/authentication.html)

- There are three types of tokens that can be used to authenticate within Directus.
- Temporary Token (JWT) are returned by the `login` endpoint/mutation. 
  - These tokens have a relatively short expiration time, and are thus the most secure option to use. 
  - The tokens are returned with a refresh token that can be used to retrieve a new access token via the `refresh` endpoint/mutation. Session Token (JWT) can also be returned by the login endpoint/mutation. Session tokens combine both a refresh token and access token in a single cookie. These tokens should not have a short expiration time like the Temporary Tokens as you cannot refresh these after they have expired.
- Session Token (JWT) can also be returned by the `login` endpoint/mutation. 
  - Session tokens combine both a refresh token and access token in a single cookie. 
  - These tokens should not have a short expiration time like the Temporary Tokens as you cannot refresh these after they have expired.
- Static Tokens can be set for each platform user, and never expire. 
  - They are less secure, but quite useful for server-to-server communication. 
  - They are saved as plain-text 

- 
- 
- 

# more
