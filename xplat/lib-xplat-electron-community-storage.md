---
title: lib-xplat-electron-community-storage
tags: [community, electron, storage]
created: 2023-01-02T10:30:28.910Z
modified: 2023-01-02T10:30:48.816Z
---

# lib-xplat-electron-community-storage

# guide

# discuss
- ## 

- ## 

- ## 

- ## [IndexedDB shared between windows? · Discussion · cawa-93/vite-electron-builder](https://github.com/cawa-93/vite-electron-builder/discussions/222)
- > Context:
  - Create main/renderer windows via new BrowserWindow()
  - Create additional "background" processing window that is hidden via new BrowserWindow()
  - Additional window at step 2 handles data fetch processing without affecting main rendered window.
- Problem:
  - IndexedDB is different for renderer window and additional window.

- As far as I know, the chrome engine is responsible for share of states. So for the state of your windows to be synchronized, its must work on one origin and one session.
  - I tried to reproduce your example but did not encounter a problem. 
  - The only time the state of the windows was out of sync was when one of them opened as `http://localhost:3030/` and other as `file://c/path/to/project/file/index.html`.

- Just managed to get this to work (without resorting to Workers
  - Open each window (Renderer and Worker) using same HTML and JS entry script.
  - During new BrowserWindow({...}) call, mark the window as follows:
  - Within renderer.ts read the process.argv array to see which window is being processed and boot accordingly.

```JS
webPreferences: {
  additionalArguments: ["--my-window-identifier"],
}
```
