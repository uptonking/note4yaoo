---
title: thread-web-browser-caniuse-compatibility
tags: [browser, compatibility, css, js, thread, web]
created: '2021-07-28T12:54:43.589Z'
modified: '2021-07-29T11:15:44.100Z'
---

# thread-web-browser-caniuse-compatibility

# discuss

- ## 

- ## In new Chromium 92, PWAs can register themselves as handlers of custom URL protocols/ schemes using their installation manifest, making them all the more appy.
- https://twitter.com/brucel/status/1420775444287303680
  - [URL protocol handler registration for PWAs](https://web.dev/url-protocol-handler/)

- ## Safari quirk: when an element has pointerCapture, the event's movementX and movementY will always be zero. 
- https://twitter.com/steveruizok/status/1420844366617264132

- ## CSS Module scripts were just merged into the HTML spec! __20210715
- https://twitter.com/justinfagnani/status/1415383208359645184
  - [Feature: CSS module scripts: ](https://chromestatus.com/feature/5948572598009856)
  - import styleSheet from "./styles.css" assert { type: "css" }; 
- how will this work in webpack or other bundlers? currently we import "style.css" and it adds it automatically or it's configured as a css-module. will this interfere with that?
  - Bundlers will have to adapt to the ever-evolving web platform as they always do.
  - I'm this case there's a straightforward transform to a JS module that exports a CSSStyleSheet. Later there may be more options around Web Bundles or multi-sheet CSS files.
  - I think with the import assertions, bundlers can use those as flags to fairly skip or delegate this process and then generate a chunk for the target file. But who knows Man shrugging, I'm still yet unsure if bundlers right now supports assertions.

- ## Things I didn't know are apparently impossible – positioning something exactly above the virtual keyboard on iOS Safari.
- https://twitter.com/tommoor/status/1420469267057844227
- You can use `window.visualViewport.height` .  (Try creating a new issue with a long description in linear for example)

- ## This week it was working around the fact that Safari dispatches two _mousemove_ events whenever you press a modifier key like Shift, Alt etc.
- https://twitter.com/brianskold/status/1420312185444601856
- whoa, is that per mouse move?
  - No, per key press. One on keydown, one on keyup.
- Safari fires a mousemove event on keydown/up if the key is shift, ctrl, alt, cmd etc, even if the mouse hasn't actually moved. 
  - Neither Chrome or Firefox do this. Safari doesn't do it for other keys.
- In Safari's defence, the MouseEvent objects have boolean properties for the state of those keys, so it's kinda sort-of reasonable to fire another event when that state changes.
  - But yeah, firing mousemove when the mouse didn't move feels weird.
