---
title: lib-xplat-react-native-latest-roadmap
tags: [react-native, roadmap]
created: 2021-09-10T14:08:49.875Z
modified: 2021-09-10T14:09:39.770Z
---

# lib-xplat-react-native-latest-roadmap

# guide

# release-notes

# suspended

## [CSS Grid Layout support](https://github.com/react-native-community/discussions-and-proposals/issues/90)

- I'm not sure if it would happen because of the current Fabric re-architecture; probably a bit early.
- A layout feature like this would be implemented in Yoga, which is independent of the Fabric project afaik.

- [/yoga CSS Grids: Is there any interest in integrating a grid implementation?](https://github.com/facebook/yoga/issues/867)
  - Some of you might be interested to know about a year ago an alternative was announced called Stretch(in Rust)
  - Stretch doesn't really enable any new kind of layouts that yoga doesn't but it fixes some fundamental problems in Yoga where Yoga was not compatible with the web implementations.
  - Long term goal of Stretch is to support multiple layout systems including Grid layout I just started with Flexbox because I know that so well :) Look forward to tackling grid layout soonish (contributions / help very welcome).
  - The mentioned stretch project recently started discussing how to start implementing Grid support.
  - Doesn't seem like there's any interest from devs on yoga. 

- [/stretch [Feature] Support CSS Grid](https://github.com/vislyhq/stretch/issues/63)
  - Very curious/excited to see where this goes!
  - 未更新__202007
# news

## [all 1K+ RN screens in the Facebook app use the new Fabric renderer__202107](https://twitter.com/joshuaisgross/status/1415099495285608453)

- Today, React Native reached a major milestone - all 1K+ RN screens in the Facebook app use the new Fabric renderer. 
  - This is something we have been working toward since January 2018!
  - Next, we'll be starting to work on bringing this to open source for everyone to use - stay tuned!

- Is the new architect significantly improving any metric or just making sync communication possible?
  - AFAIK Fabric, ultimately uses JSI instead of the RN bridge, meaning that not only can updates been sync, they should be a lot faster too as you don’t pay the serialize/deserialize cost.
  - TurboModules (now called JSI) is already open source but needs better documentation

- Will this new architecture breaking changes? or we can use it without many of changes in the code?
  - all the native components (I mean libraries which render something) should be rewritten using new API.
  - all the native libraries (which doesn't render something) will benefit from all of it after migration to `TurboModules`, but I guess there is backward compatibility layer.
- AFAIK, on iOS there is a compat layer that can drive all legacy components that don't have a `ShadowView` counterpart (98% of all components). 
  - On Android, IIRC, the compatibility situation is generally should be even better because of some design differences.
  - The caveat is that some of the most popular OSS components naturally have *very* tricky implementations (e.g. `<SVG>`) that cannot be plugged in using the compat layer. 
  - Those have to be completely rethought and rewritten. (The reimplementation should give a huge perf boost though.)
- Another aspect is native modules that heavily interact with UI components (e.g. `Reanimated`). 
  - There are some compat solutions for some of that here and there *but* IMO those just have to be redone to eliminate bugs, quirks, and the endless suffering of all RN folks.

## [React Native's Many Platform Vision__202108](https://reactnative.dev/blog/2021/08/26/many-platform-vision)

- Although React Native was originally created to build mobile apps, we believe that focusing on many platforms and building to each platform’s strengths and constraints has a symbiotic(共生的，相互依赖的) effect.
- Our first guiding principle is to match the expectations people have for each platform. 
- We believe that React Native enables developers to meet users’ expectations while also gaining the benefits of a better developer experience. 
  - By embracing platform constraints, we actually improve the experience on other platforms.
  - We can learn from institutional knowledge to build higher level cross-platform abstractions.
  - Other players on each platform inspire us to build better developer and user experiences.
- For the past year, we have been partnering with Microsoft and the Messenger team to create a truly native video calling experience on Windows and macOS. 
  - our initial implementation of desktop video calling using React Native completely blew away the performance of the Electron implementation that it replaced.
- In summary, our vision is to expand React Native's reach beyond mobile and we've already started by partnering with desktop and VR teams at Facebook.

## [State of React Native 2018__201806](https://reactnative.dev/blog/2018/06/14/state-of-react-native-2018)

- When we started the React Native project in 2013, we designed it to have a single “bridge” between JavaScript and native that is asynchronous, serializable, and batched. 
  - Just as React DOM turns React state updates into imperative, mutative calls to DOM APIs like `document.createElement(attrs)` and `.appendChild()`, React Native was designed to return a single JSON message that lists mutations to perform, like `[["createView", attrs], ["manageChildren", ...]]`. 
- We designed the entire system to never rely on getting a synchronous response back and to ensure everything in that list could be fully serialized to JSON and back. 
  - We did this for the flexibility it gave us: on top of this architecture, we were able to build tools like Chrome debugging, which runs all the JavaScript code asynchronously over a WebSocket connection.

- Over the last 5 years, we found that these initial principles have made building some features harder. 
  - An asynchronous bridge means you can't integrate JavaScript logic directly with many native APIs expecting synchronous answers. 
  - A batched bridge that queues native calls means it's harder to have React Native apps call into functions that are implemented natively. 
  - And a serializable bridge means unnecessary copying instead of directly sharing memory between the two worlds. 
- We're working on a large-scale rearchitecture of React Native to make the framework more flexible and integrate better with native infrastructure in hybrid JavaScript/native apps.

- To make React Native more lightweight and fit better into existing native apps, this rearchitecture has three major internal changes. 
- First, we are changing the threading model. 
  - Instead of each UI update needing to perform work on three different threads, it will be possible to call synchronously into JavaScript on any thread for high-priority updates while still keeping low-priority work off the main thread to maintain responsiveness. 
- Second, we are incorporating async rendering capabilities into React Native to allow multiple rendering priorities and to simplify asynchronous data handling. 
- Finally, we are simplifying our bridge to make it faster and more lightweight; 
  - direct calls between native and JavaScript are more efficient and will make it easier to build debugging tools like cross-language stack traces.

- [The State of the React Native Community in 2018__201901](https://reactnative.dev/blog/2019/01/07/state-of-react-native-community)
- A lot of people are excited about the rewrite of React Native's architecture, widely known as Fabric. 
  - Among other things, this will fix fundamental limitations in React Native's architecture and
  - will set up React Native for success in the future together with JSI and TurboModules.
