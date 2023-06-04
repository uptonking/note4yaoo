---
title: lib-collab-immerjs-community
tags: [collaboration, community, immerjs]
created: 2023-06-04T21:26:40.284Z
modified: 2023-06-04T21:27:01.100Z
---

# lib-collab-immerjs-community

# guide

- who is using #immer-patches
  - webstudio
  - luckysheet

- resources
  - [Distributing state changes using snapshots, patches and actions — Part 1 | by Michel Weststrate | Medium](https://medium.com/@mweststrate/distributing-state-changes-using-snapshots-patches-and-actions-part-1-2811a2fcd65f)
  - [Distributing state changes using snapshots, patches and actions — Part 2 | by Michel Weststrate | Medium](https://medium.com/@mweststrate/distributing-state-changes-using-snapshots-patches-and-actions-part-2-2f50d8363988)
  - [Using Immer to compress Immer patches](https://medium.com/@dedels/using-immer-to-compress-immer-patches-f382835b6c69)
# dev

# discuss

- ## 

- ## 

- ## 

- ## 
# discuss-collaboration
- ## 

- ## 

- ## [Maintaining invariants with non-Immer managed derived state through applyPatches](https://github.com/immerjs/immer/issues/940)
  - Does Immer have any recommended "best practices" for this sort of thing?

- ## [Rebasing patches in collaborative editing](https://github.com/immerjs/immer/issues/410)
  - Implement a `rebase` function that transforms patches so that they can be applied to the state created by another array of patches.
  - Inspired by ProseMirror rebasing logic
- I've wrote about it a while ago
  - Beyond that, there are many ways in which one can reason about patches, but doing such things is not the goal of this library and can be implemented just as well in user-land / another library. 
  - Immer provides the raw patches, but any post processing as normalizing, minimising, compressing and rebasing go beyond the scope of this package.
- I didn't find the answer there unfortunately. It seems like replaying pending actions doesn't always preserve the right intent. Any tips on that? How do you deal with collab conflicts at Mendix?
  - That is because there is no generic solution to the problem, as it depends on the semantics.
- So telling how we solved it at Mendix is kind of irrelevant, because we are not operating in the same domain. 
  - But what we do is have meta information on every property and collection, that allows us to set conflict resolutions, e.g; is last winner ok, or should it cause conflict? 
  - And for collections: is ordering important, or not? As with non-important ordering concurrent adds are fine, just apply them in any order. Etc. etc. For further research, I suggest to google on "Operational Transformation", its a more advanced solution that might take you further.
