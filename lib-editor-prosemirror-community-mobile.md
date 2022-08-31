---
title: lib-editor-prosemirror-community-mobile
tags: [community, mobile, prosemirror]
created: 2022-08-30T18:17:24.603Z
modified: 2022-08-30T19:05:07.625Z
---

# lib-editor-prosemirror-community-mobile

# guide

# discuss
- ## 

- ## 

- ## 

- ## Contenteditable on Android is the Absolute Worst_202106
- https://discuss.prosemirror.net/t/contenteditable-on-android-is-the-absolute-worst/3810
- Issue 1: Lack of keydown keys
- Issue 2: The cursor wrapper
- Issue 3: The composition text node swap
- Issue 4: Android Chrome is afraid of unselectable atoms
- Issue 5: Input bugs are unique across different webview versions, keyboards, keyboard versions, types of devices, and OS versions.
  - there are still some nasty and stupid bugs that come up that are specific to a combination of certain webview versions on specific devices with specific keyboards. 
  - We are actually using our native app to tell our editor which keyboard types (e.g. Gboard, Samsung, LG, etc.) are enabled at any given time so we can have workarounds for specific keyboards if absolutely necessary. 
  - Many of our fixes in these scenarios end up using cursor parking but this is still an area where we are all bound to have blind spots.

- Where to go next?
  - Honestly unless there are serious efforts on the Chrome front to improve contenteditable on Chrome Android and how the IME views contenteditable, there isn’t much we can do fundamentally that ProseMirror isn’t already doing. 
  - I’m sure there are a few additional fixes that could be made but issues like the mark cursor seem to be unfixable without breaking the mark cursor feature at least some of the time.
  - The best approach may be to just have less functionality on mobile, especially around key handling and advanced node views, but I’d love to hear what others think

- It should also be noted that Mobile Safari on iOS isn’t much better here. 
  - It doesn’t use composition for most languages, so many users don’t run into the bizarre things it does during composition, 
  - but Chinese or Japanese users run into about as many bugs on that platform as on Chrome Android.
