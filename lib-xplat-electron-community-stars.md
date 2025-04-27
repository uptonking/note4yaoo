---
title: lib-xplat-electron-community-stars
tags: [community, electron]
created: 2024-01-31T19:34:36.054Z
modified: 2024-01-31T19:34:47.617Z
---

# lib-xplat-electron-community-stars

# guide

# discuss-stars
- ## 

- ## 

- ## [[Feature] Headless Electron · Issue · microsoft/playwright _202204](https://github.com/microsoft/playwright/issues/13288)
  - I could not find a way to run Electron tests headless like that is possible with browser tests.

- Electron itself does not have the headless mode. It can probably be simulated via hiding the window, but there is no built-in functionality of swapping the graphics stack like there is in Chromium. What do your existing tests do today?

- I was able to get headless electron tests working with this snippet: override the default behavior of showing the browser window once it's ready to show
  - The renderer process is still running, just completely headlessly, without a display, so the tests are all valid. 
  - For this to work on CI (on linux), you need `xvfb`.
# discuss
- ## 

- ## 

- ## 
