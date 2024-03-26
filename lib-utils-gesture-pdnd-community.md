---
title: lib-utils-gesture-pdnd-community
tags: [community, dnd, programatic-drag-drop]
created: 2024-03-08T05:29:05.014Z
modified: 2024-03-08T05:29:35.446Z
---

# lib-utils-gesture-pdnd-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-news-pdnd
- ## 

- ## 

- ## Working on a @tan_stack virtual list example, with drag and drop powered by Pragmatic drag and drop
- https://twitter.com/alexandereardon/status/1772394493943091270

- ## 🌰 Seamless dragging between windows; second columns are in iframes
- https://twitter.com/alexandereardon/status/1765874214471614652
  - Yes, this works in Safari and Firefox
  - It’s a vanilla js library, so it can be used with anything like react/svelte
- Wait, doesn't the only way to drag rich elements out of a window, using the native drag and drop APIs, require the image of the thing being dragged to be translucent?
  - It's not too translucent (thankfully)
- Ah yeah from desktop I can see that it's not fully opaque. On the phone it looked impossibly perfect. It still looks very good though

- Does this mean you can drag between tabs? Kind of like dragging an image into messages?
  - Yep

- From experience you can support with browser <-> native application as well. The nice thing about data transfer

- https://twitter.com/oriSomething/status/1765963434489757878
  - Basically it’s `dataTransfer` of `DragEvent`. Can support native applications too without much work. 
  - I’ve made experiments with that in the past, but it’s too advanced feature for 99% of the users
- By the way, the real issue of supporting this feature is you already have the item in the list on a different window, what is the right UX? If you receive item with missing data locally what to do you do? In real apps it can lead to many UX/sync issues that mostly don’t worthy
  -  I’ve tried to support it at AnyDo, and very fast I got to the conclusion it will cause more problems. Moreover,  `dataTransfer` is cool, it’s the same mechanism when drop files or anything else. In reality dropping files are most usable and he could do some cool demo too. Think of Dropbox like

- These are the drag and drop edge cases nobody wants to write code for. Massive respect 

- ## 🌰 Pragmatic drag and drop 1.0 adds cross browser support for dragging into an out of iframes _202403
- https://twitter.com/alexandereardon/status/1765523608682795227
  - 示例动画
  - Some applications leverage iframes for sandboxing (eg for addons), Site builders, etc
  - I'm pretty hyped about this, as achieving something like  this on your own is really hard. pdnd makes it real safe and straight forward to set up

- postMessage?
# discuss
- ## 

- ## 

- ## 
