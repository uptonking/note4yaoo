---
title: lib-xplat-react-native-skia
tags: [cross-platform, react-native, skia]
created: '2021-09-05T13:19:47.408Z'
modified: '2021-09-05T13:20:14.519Z'
---

# lib-xplat-react-native-skia

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## Flutter 2 announced last week to show off the cross platform power.
- https://twitter.com/kudochien/status/1369491495892316160
  - However, for the web support, since it's based on skia. 
  - It should be difficult to use SSR or prerender for SEO.
  - For embedded Linux, we also has an ongoing plan by react-native-skia.
- By react-native-skia, we could extend react-native to other platforms like Flutter.
  - Although I didn't have much time on this project, but people from NAGRA OpenTV invested a lot.

- ## It's Flutter. But in React Native.
- https://twitter.com/wcandillon/status/1433831742302003227
- How does this new effort differ from react-native-skia
  - this is a single skia canvas and you need to rebuild the world inside that canvas (like Flutter did). 

    - Our effort is to bring Skia views in regular RN. In fact some of the demos in the video feature many skia views at the same time.

  - Makes sense! **This library might then mean that RN can do some things with Skia that Flutter itself can’t** – I remember an issue that you couldn’t lay any Skia views atop of certain native views. e.g. you couldn’t show a toast over a `WKWebView` .
