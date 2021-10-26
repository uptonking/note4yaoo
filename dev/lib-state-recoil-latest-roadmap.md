---
title: lib-state-recoil-latest-roadmap
tags: [react, recoil, roadmap, state]
created: '2020-07-06T03:26:56.138Z'
modified: '2021-05-13T03:18:37.764Z'
---

# lib-state-recoil-latest-roadmap

# limitations

- render twice on component mount (useRecoilValue, useRecoilState) in non-StrictMode
  - https://github.com/facebookexperimental/Recoil/issues/307
- [recoil change state outside of components](https://github.com/facebookexperimental/Recoil/issues/410)

# guide

- We have an internal roadmap that we can publish soon. 
  - It's mostly about making the implementation more efficient and making the APIs more flexible to work with a wider range of apps.
  - We talk with people on the React team and it's possible that future changes in React **might simplify Recoil to the point where it's just some nice utility hooks**. 
  - I can't speak in specifics about when or how that might happen, though.
  - https://github.com/facebookexperimental/Recoil/issues/169
- ref  
  - https://recoiljs.org/blog
  - https://github.com/facebookexperimental/Recoil/issues/428

# roadmap

- unofficial
  - Internal cleanup (ongoing)
  - Memory Leaks in 0.10 #366
  - Fast Refresh support #353 #12 #247
  - Add internal FB playground/app to open source repo as example, codesandbox template for PR's #11
  - DevTools (FB intern was working on it, but currently stalled) #194
  - Server Rendering #131 #53
  - React Native #108
  - Docs
