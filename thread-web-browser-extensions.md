---
title: thread-web-browser-extensions
tags: [browser, chrome, extensions, firefox, safari]
created: 2025-03-01T09:05:19.751Z
modified: 2025-03-01T09:05:43.976Z
---

# thread-web-browser-extensions

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-safari/ios
- ## 

- ## 

- ## 

- ## 
# discuss-fwk-extensions
- ## 

- ## [The Journey of Migrating Our Browser Extension from Plasmo to WXT Framework - ChatGPT Writer _202409](https://chatgptwriter.ai/blog/migrate-plasmo-to-wxt)

- ## [Plasmo – A framework for building modern Chrome extensions | Hacker News _202408](https://news.ycombinator.com/item?id=41304508)
- I also suggest checking out WXT as an alternative (it's also faster using Vite and supports more frameworks).

- If you’re looking for a Vue-flavored dev experience as opposed to a react one, I recommend this:
  - https://github.com/antfu-collective/vitesse-webext

- Importantly for anyone who dislikes ads: seems to support Firefox too

- Wxt was mentioned elsewhere in this thread and will build from a single codebase for multiple target browsers. It's built on top of a polyfill from Mozilla

- ## 🆚️ [WXT vs. Plasmo. Some thoughts on migrating from Plasmo to WXT. · wxt-dev/wxt · Discussion _202406](https://github.com/wxt-dev/wxt/discussions/782)
- This is the conclusion I got after spending a day migrating my extension from Plasmo to WXT
- Something better than Plasmo in WXT.
- Effective HMR
  - Plasmo HMR is not "React-only", in fact in the extensions I've written using React, HMR only works when the page is very small, most of the time HMR doesn't work.
  - But WXT HMR works really well, I rarely have to refresh Popup and Options pages, content script changes trigger automatic page refreshes
- Based on Vite
  - Anyone familiar with plasmo will have encountered a bunch of Parcel bugs upstream
  - WXT allows us to fully utilize Vite existing features and plug-ins, while Plasmo does not allow us to intervene at all.
- Better maintenance of the status quo
  - Plasmo is dead. The maintainers have spent very little time on maintaining Plasmo in one year. No one is handling PRs and issues, and most of the bugs do not exist in WXT.
- Expose UI framework mount process
  - Just using Vue as an example, Plasmo completely hides the `app.mount` process, the problem is that many libraries rely on `app.use(...)` , hiding this makes it impossible for developers to use these libraries smoothly, especially component libraries.
  - WXT will add some boilerplate code by exposing this process, but I think it's worth it compared to the flexibility it brings.
- Hooks and Assets
  - Plasmo doesn't make any hooks public, nor does it have a public directory, and can't even do the simple function of adding a few files to the build product, whereas that flexibility should be necessary.
- Config File
  - Plasmo doesn't support `plasmo.config.ts` , manifest.json overrides can only be written in `package.json` , 
  - `wxt.config.ts` lets me utilize TypeScript to prevent spelling errors and more.
  - Not to mention that WXT has many configurable items and hooks that can be used, a separate configuration file is very necessary.
- More DX improvements
  - WXT formats the manifest.json file in development mode.
  - WXT tree-shaking is much more efficient than Plasmo
  - WXT does not add hashcode to file names in the build product, which helps speed up store reviews.

- 🐛 WXT
  - WXT does not have a built-in messaging module now. Plasmo built-in messaging tool is very useful and can automatically generate types. Migration can use @webext-core/messaging, but the types need to be written manually. This may change in the future.
  - `wxt/utils/storage` is not compatible with Plasmo. The behavior of wxt/utils/storage is closer to `chrome.storage.*`. The two have inconsistent formats for the same object stored in storage. 

- Moving from plasmo to wxt has the benefits of decreasing my bundled extension (I mean the zip file) from 5MB to 500KB. I guess the tree shaking is effective here, and wasn't using plasmo

- Plasmo has paid functionality to deploy it via enterprise feature of chrome on their paid plan
  - I'd love for WXT to have something similar to this. If anyone knows how to match that functionality in WXT let me know.

- ## 🆚️🆚️ [Compare – WXT](https://wxt.dev/guide/resources/compare)
  - 官方比较列表

# discuss
- ## 

- ## 

- ## 

- ## 
