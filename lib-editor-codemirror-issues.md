---
title: lib-editor-codemirror-issues
tags: [codemirror, issues]
created: 2024-08-11T03:31:29.849Z
modified: 2024-08-11T03:31:52.955Z
---

# lib-editor-codemirror-issues

# guide

# issues-stars
- ## 

- ## 

- ## 
# issues-not-yet
- ## 

- ## 

- ## 
# issues
- ## 

- ## 

- ## 

- ## .pnpm/@marijn+find-cluster-break@1.0.2/node_modules/@marijn/find-cluster-break/src/index.js:17     SyntaxError: Unexpected token 'export'
- https://github.com/codemirror/website/issues
  - `at Object.<anonymous> (../../node_modules/.pnpm/@codemirror+state@6.5.2/node_modules/@codemirror/state/dist/index.cjs:3:26)`

- 实测是由于旧版pnpm.v7安装的依赖state最新版本有问题，导致jest test未通过
  - 解决方法1: 降级到旧版本 "@codemirror/state": "6.4.1"
  - 解决方法2: 升级pnpm到最新版v10

- ## [Allow alternate editor components: Monaco editor, ACE · executablebooks/thebe _202402](https://github.com/executablebooks/thebe/issues/730)
- The current editor component codemirror from jupyter, has issues with CSS transforms.
  - CSS transforms is used by `reveal.js` to zoom slides from "design size" to "screen size".
  - This causes codemirror component to be quite unusable within reveal.js slides, as the visible cursor, line indicator and similar can be complely off.

- Apparently @codemirror/view 6.18.0 added some code to detect when the view component is scaled. But Thebe appears to currently use codemirror 5.

- ## Why do you want to run codemirror on server side _202405
- https://discord.com/channels/437048931827056642/437067256049172491/1238441369379405926
- nextjs renders stuff server side
- Since nobody fixed it before im assuming you are the first one on the planet prerendering cm6
