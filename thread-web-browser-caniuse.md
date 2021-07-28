---
title: thread-web-browser-caniuse
tags: [browser, css, js, thread, web]
created: '2021-07-28T12:54:43.589Z'
modified: '2021-07-28T12:55:28.842Z'
---

# thread-web-browser-caniuse

# discuss

- ## 

- ## 

- ## 

- ## 

- ## 

- ## This week it was working around the fact that Safari dispatches two _mousemove_ events whenever you press a modifier key like Shift, Alt etc.
- https://twitter.com/brianskold/status/1420312185444601856
- whoa, is that per mouse move?
  - No, per key press. One on keydown, one on keyup.
- Safari fires a mousemove event on keydown/up if the key is shift, ctrl, alt, cmd etc, even if the mouse hasn't actually moved. 
  - Neither Chrome or Firefox do this. Safari doesn't do it for other keys.
- In Safari's defence, the MouseEvent objects have boolean properties for the state of those keys, so it's kinda sort-of reasonable to fire another event when that state changes.
  - But yeah, firing mousemove when the mouse didn't move feels weird.
