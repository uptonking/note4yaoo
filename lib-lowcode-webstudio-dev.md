---
title: lib-lowcode-webstudio-dev
tags: [designer, lowcode, webstudio]
created: 2023-06-04T20:36:55.354Z
modified: 2023-06-04T20:37:37.337Z
---

# lib-lowcode-webstudio-dev

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

- ## As for commercial usage, you can use open source builder, we are licensing it under MIT. 
- https://discord.com/channels/955905230107738152/955905231227609158/1080408017595535440
  - If you don't need advanced permissions management, image optimizer, real-time collaboration and other advanced things, which are part of the saas product and isn't available in the builder repo.
  - Core builder is OSS and will stay that way
