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

- ## Skia in React Native is implemented as an imperative API for doing 2D canvas-like drawing operations with full support for filters, shaders, transforms etc. using the Skia graphics library.
- https://twitter.com/chrfalch/status/1434880480650932232
- It lets you define a callback function for drawing 2d graphics 
- In addition it has a loose integration with Reanimated (and maybe Animated as well if needed) where changes in an animated value will trigger a redraw of the SkiaView - which in turn can use the animated value when drawing.
- We're discussing/working on building some nice declarative components around the API to make it even easier to integrate with React Native. A draft for a custom reconciler is already in place.
- Compared to Flutter it has a few really nice features like transparent drawing over React Native primitives meaning that integration with other components (both React Native and Native components) will be doable
- **The library is built using JSI (not crossing the bridge), and rendering is currently done on the JS thread**. 
  - The rendering is really fast, it takes a couple of milliseconds to render a view on both Android and iOS.
- The **existing `react-native-skia` library is a platform for React Native where everything is rendered by Skia**
  - our project aims to bridge React Native with Skia - meaning you can integrate it into an existing React Native solution and take advantage of 2D drawing directly.
- The library itself links in the Skia binaries, which we're working on getting as small as possible. 
  - The mono/SkiaSharp project has had nice progress with this, so hopefully it will add somewhere around 10 mb to your app.

- How this compressor(压气机，压缩机) competes with reanimated2? Do you use them both or you chose between them? Any use cases?
  - `Reanimated` is about running animations. You can create animated values and animated them. 
  - Then you can actually use `Reanimated.View` to render something you can do with RN and animated it. Or you'll be able to use `Skia.View` and `onDrawCallback` to animate some "canvas" stuff

- Another good reason why I think React-Native has the best tradeoffs for cross-platform. 
  - It is even possible that React-Native could end up being a better choice for using Skia than using Flutter 
- I guess eventually someone will create a wrapper around this Skia API to support html5 canvas and then lots of cool stuff from the web will work perfectly fine on mobile too.
- You mean something like React Three Fiber could run on mobile?
  - Yep. Kinda. Lots of cool stuff can be easier built with canvas. Such as charts. Or lots of 2d graphics. And not it will be possible.
  - maybe not the 3d part but a subset

- still prefer the 1-1 mapping from rn-native views/widgets, that's the main reason why i don't like flutter. + if we're serious about all the UI w/ skia, we need accessibility as well. that being said, having skia in the rn land is a game charger (games, complex ui, drawing, etc)

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
