---
title: lib-saas-directus-latest-roadmap
tags: [changelog, directus, roadmap]
created: 2024-03-02T13:33:38.680Z
modified: 2024-03-02T13:33:54.693Z
---

# lib-saas-directus-latest-roadmap

# guide

# roadmap

# changelog
- resources
  - [Releases · directus/directus](https://github.com/directus/directus/releases)
  - [Breaking Changes | Directus Docs](https://docs.directus.io/releases/breaking-changes.html)

## [v10.0.0_20230427](https://github.com/directus/directus/releases/tag/v10.0.0)

- v10.9.0_20240207
  - Enabled theme override permissions to be set on a per role basis 
  - Added enable/disable support for bundle type extensions

- v10.8.0_20231117
  - Added theme-selector interface to settings and users
  - Added support for themes as an extension type
  - Added configuration to allow extensions to be managed in a configured storage location
  - Renamed the type `ExtensionItem` to `DirectusExtension`, allowed extending the type with custom fields

- v10.7.0_20231023
  - ✨🌵 Add support for Content Versioning
  - Allow enabling/disabling extensions through app and api 
  - Added a new section to settings that lists all the installed extensions
  - Added support for the optional sandbox flag in API extensions 
  - Added Sorting by Aggregated Queries

- v10.6.0
  - ✨ Replaced `vm2` with `isolated-vm` for sandboxing the "Run Script"-Operation in Flows
  - Introduced new JSON Web Token (JWT) operation to Flows

- v10.5.0
  - First release of the new SDK 
  - Add support for Supabase Storage for files

- v10.4.0_20230628
  - Dropped support for Memcached
    - Directus used to support either memory, Redis, or Memcached for caching and rate-limiting storage. 
    - Since the 10.3 release, Redis has been used more integrated as part of WebSockets/Subscriptions 
    - we've decided to sunset Memcached in favor of focussing on Redis as the primary solution for pub/sub and hot-storage across load-balanced Directus installations.
  - The New SDK is available in beta
    - We've been working hard on redesigning the SDK from the ground up
  - Ensured all caches are flushed when applying diff

- v10.3.0
  - Integrated Websockets Subscriptions for REST and GraphQL in Directus 
  - A CRUD implementation over WebSockets

- v10.2.0
  - Added live preview functionality to the Data Studio App to easily and instantly track the impact of item changes on web pages

- v10.1.0
  - ✨ Added Kanban layout
    - [Move in kanban layout exclusive extension _20230510](https://github.com/directus/directus/pull/18516)
  - ✨ Added block editor interface
    - [Move in block editor exclusive extension _20230512](https://github.com/directus/directus/pull/18525)
    - 基于editorjs实现
    - This first iteration is going to be just the "regular" JSON structure. That being said, we are about to dive into improving the M2A builder and potentially also creating an editorjs-type setup that works with that data model 
  - Added Pressure-based rate limiter
  - Added support for building API extensions to ESM format and default to ESM for new extensions 

- In v10.0.0, Directus is adopting BSL 1.1 
  - All Directus source code will still be open and available on GitHub
  - Non-production use of Directus is still completely free for everyone
  - Production use of Directus is still completely free for nearly all users
  - Code released under this new license converts to GPLv3 (OSS) after 3 years

- 保持MIT协议的包
  - @directus/extensions-sdk
  - @directus/composables
  - @directus/constants
  - @directus/types
  - @directus/utils

- [Change license to BSL-1.1_20230427](https://github.com/directus/directus/pull/18330)

- [Sustainable Open Source: Why We're Relicensing Directus _20230426](https://directus.io/blog/why-we-are-relicensing-directus)

## [v9.0.0_20211105](https://github.com/directus/directus/releases/tag/v9.0.0)

- Remove collection listing option from role settings
- Removes "Collections Navigation" setting from roles detail page
- Move union query application to `applyQuery`, fix where clause
- Use hash instead of random for default index name

## v8.0 /php

- built with php
# more
- [An Overnight Success (Two Decades In The Making) _20240228](https://directus.io/blog/directus-two-decades)
  - We weren’t in it for the “quick buck.” We wanted to build a premium product, without technical debt, that would stand the test of time
  - The answer was to take our time distilling all the specific features and requirements we’d seen over decades of building one-off projects, abstracting everything into an agnostic solution.
  - we focused on making Directus a collaborative project, embracing new engineers from around the world, all joining us as contributors to our open source project.
# discuss-changelog
- ## 

- ## 

- ## 

- ## 🛒 our Leap Week 02 keynote was yesterday. Here's the full recording, but check out the thread for key announcements _20240305
- https://twitter.com/directus/status/1765014721294397655
  - Announcing the Directus Marketplace Beta, focused on publishing, discovery, and installation of extensions in all Directus projects - both self-hosted and on Directus Cloud.
  - A brand new hackathon taking place this March focused on payments.
  - Level Up With Directus+ - a companion subscription with starter kits, exclusive workshops, and more.

- ## 🔁 [Integrating Websockets in Directus _202306](https://github.com/directus/directus/pull/14737)
  - Integrating two-way communication into the Directus server to enable real-time functionality.
  - This pull request first appeared in v10.3.0

- A CRUD implementation over WebSockets
- A REST Subscriptions implementation
- Heartbeat signal to keep the connection alive
- Follows the Directus permission model
- Extensible event driven design
