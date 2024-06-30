---
title: lib-saas-webstudio-dev
tags: [designer, lowcode, webstudio]
created: 2023-06-04T20:36:55.354Z
modified: 2023-12-15T17:04:43.276Z
---

# lib-saas-webstudio-dev

# guide

# dev

# collaboration

- [Single-player mode_202305](https://github.com/webstudio-is/webstudio-builder/issues/1664)
  - When webstudio is used in a single-player mode, without real-time collaboration, we need to protect the user from unwanted effects of accidentally having multiple tabs or multiple users overwriting each other builds.
  - Multi-player mode is more complex infra and should be opt-in.
  - We discussed that we can generate an id of the active "builder/maintainer" who can update the build. Whoever reloaded the latest automatically becomes maintainer and receives the id that we send with every patch. If user has outdated id, they get an error: "In single-player mode only one user can edit at a time. Please reload the window to enable editing from it."
# more

# discuss-collab

- ## 

- ## 

- ## [Explore realtime collaboration](https://github.com/webstudio-is/webstudio-builder/issues/46)
- There is a lot of things to consider when building a realtime multiplayer UI
  - offline first
  - state management
  - server architecture
  - database: sqlite/rxdb
  - conflicts: yjs/automerge/hlc
  - change types

- ## thinking of conflicts resolution, why not roll back every change that has resulted in a conflict, make it obvious in the UI, 
- https://twitter.com/oleg008/status/1525422477362573312
  - You can't do that if you are operating on a single blob, but it could be viable if your changes are atomic and have specific semantic meaning, right?

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 🏘️ I have always admired Merrick and this is a great writeup on Webflow architecture
- https://x.com/oleg008/status/1806846905642864805
  - Here is what we did differently at @getwebstudio
- Webflow:
  1. A custom higher-level language that includes everything you want to be able  to express on a site in it's WFDL syntax
  2. Converts to JSON Data
  3. Uses React for designer canvas
  4. Generates html/css for published sites
- Webstudio:
  1. Components meta JSON that describes how components integrate into visual environment 
  2. Build data describes elements tree, styles, bindings etc 
  3. SDK renders leaf components (currently React only, later others) 

- Reason I went for a completely different architecture with Webstudio (downsides of WFDL)
1. A higher level language that has to be able to describe anything you could do with modern js frameworks and more will have to be inevitably very complex. It may be less complex than JavaScript + 
React but it is a very custom language and it will inevitably become more and more complex over time.
2. Every time you need to add a new control for the builder or a new behavior to the component on canvas you need to modify that language. This is difficult to develop fast and well as every piece of it has to adhere to high quality standards and have to be viewed hollistically.
3. Creating a compiler from WFDL to other frameworks will be equally hard as implementing the leaf components in each framework. It's a lot of work in any case and very hard to get right.
- Overall my strategy is to create a well-defined minimal format that builder/designer needs to operate and leave the behavior on canvas to implementation details of the components on canvas, implemented using industry standards well known to everyone.

- ## Webstudio automatically converts all your uploads to the best format 
- https://twitter.com/getwebstudio/status/1755517023734341847
  - WebP images are the gold standard when it comes to site speed.

- ## As for commercial usage, you can use open source builder, we are licensing it under MIT. 
- https://discord.com/channels/955905230107738152/955905231227609158/1080408017595535440
  - If you don't need advanced permissions management, image optimizer, real-time collaboration and other advanced things, which are part of the saas product and isn't available in the builder repo.
  - Core builder is OSS and will stay that way
